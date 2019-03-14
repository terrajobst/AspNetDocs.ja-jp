---
title: 作成し、Razor のコンポーネントを使用
author: guardrex
description: 作成してデータにバインドする、イベントを処理およびコンポーネントのライフ サイクルを管理する方法を含む、Razor のコンポーネントを使用する方法について説明します。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/13/2019
uid: razor-components/components
ms.openlocfilehash: 1533587f9f11e99f24d860c02f0efb6713119308
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031099"
---
# <a name="create-and-use-razor-components"></a><span data-ttu-id="e72a3-103">作成し、Razor のコンポーネントを使用</span><span class="sxs-lookup"><span data-stu-id="e72a3-103">Create and use Razor Components</span></span>

<span data-ttu-id="e72a3-104">によって[Luke Latham](https://github.com/guardrex)、 [Daniel Roth](https://github.com/danroth27)、および[Morné Zaayman](https://github.com/MorneZaayman)</span><span class="sxs-lookup"><span data-stu-id="e72a3-104">By [Luke Latham](https://github.com/guardrex), [Daniel Roth](https://github.com/danroth27), and [Morné Zaayman](https://github.com/MorneZaayman)</span></span>

<span data-ttu-id="e72a3-105">[サンプル コードを表示またはダウンロード](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)します ([ダウンロード方法](xref:index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="e72a3-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="e72a3-106">前提条件については、[作業開始](xref:razor-components/get-started)に関するトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e72a3-106">See the [Get started](xref:razor-components/get-started) topic for prerequisites.</span></span>

<span data-ttu-id="e72a3-107">使用して razor コンポーネント アプリを構築*コンポーネント*します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-107">Razor Components apps are built using *components*.</span></span> <span data-ttu-id="e72a3-108">コンポーネントは、ページ、ダイアログ ボックスで、フォームなどのユーザー インターフェイス (UI) の自己完結型のチャンクです。</span><span class="sxs-lookup"><span data-stu-id="e72a3-108">A component is a self-contained chunk of user interface (UI), such as a page, dialog, or form.</span></span> <span data-ttu-id="e72a3-109">コンポーネントには、HTML マークアップとデータを挿入または UI のイベントに応答するために必要な処理ロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e72a3-109">A component includes HTML markup and the processing logic required to inject data or respond to UI events.</span></span> <span data-ttu-id="e72a3-110">コンポーネントは、柔軟かつ軽量なです。</span><span class="sxs-lookup"><span data-stu-id="e72a3-110">Components are flexible and lightweight.</span></span> <span data-ttu-id="e72a3-111">入れ子になった、再利用してできるプロジェクト間で共有します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-111">They can be nested, reused, and shared among projects.</span></span>

## <a name="component-classes"></a><span data-ttu-id="e72a3-112">コンポーネント クラス</span><span class="sxs-lookup"><span data-stu-id="e72a3-112">Component classes</span></span>

<span data-ttu-id="e72a3-113">コンポーネントは、通常の実装 *.cshtml*の組み合わせを使用してファイルをC#と HTML マークアップ。</span><span class="sxs-lookup"><span data-stu-id="e72a3-113">Components are typically implemented in *.cshtml* files using a combination of C# and HTML markup.</span></span> <span data-ttu-id="e72a3-114">コンポーネントの UI を定義するには、HTML を使用します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-114">The UI for a component is defined using HTML.</span></span> <span data-ttu-id="e72a3-115">動的なレンダリング ロジック (たとえばループ、条件、式) が、[Razor](xref:mvc/views/razor) と呼ばれる埋め込みの C# 構文を使って追加されています。</span><span class="sxs-lookup"><span data-stu-id="e72a3-115">Dynamic rendering logic (for example, loops, conditionals, expressions) is added using an embedded C# syntax called [Razor](xref:mvc/views/razor).</span></span> <span data-ttu-id="e72a3-116">Razor のコンポーネント アプリをコンパイルするときに、HTML マークアップとC#レンダリング ロジックは、コンポーネントのクラスに変換されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-116">When a Razor Components app is compiled, the HTML markup and C# rendering logic are converted into a component class.</span></span> <span data-ttu-id="e72a3-117">生成されたクラスの名前では、ファイルの名前と一致します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-117">The name of the generated class matches the name of the file.</span></span>

<span data-ttu-id="e72a3-118">コンポーネント クラスのメンバーが定義されている、`@functions`ブロック (1 つ以上`@functions`ブロックが許容されます)。</span><span class="sxs-lookup"><span data-stu-id="e72a3-118">Members of the component class are defined in a `@functions` block (more than one `@functions` block is permissible).</span></span> <span data-ttu-id="e72a3-119">`@functions`ブロック、コンポーネントの状態 (プロパティ、フィールド) がイベント処理のため、またはその他のコンポーネントのロジックを定義するためのメソッドと共に指定します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-119">In the `@functions` block, component state (properties, fields) is specified along with methods for event handling or for defining other component logic.</span></span>

<span data-ttu-id="e72a3-120">ロジックを使用して、コンポーネントの一部のレンダリングと、コンポーネントのメンバーを使用しできるC#で始まる式`@`します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-120">Component members can then be used as part of the component's rendering logic using C# expressions that start with `@`.</span></span> <span data-ttu-id="e72a3-121">たとえば、C#フィールドを付けることによって表示`@`フィールド名にします。</span><span class="sxs-lookup"><span data-stu-id="e72a3-121">For example, a C# field is rendered by prefixing `@` to the field name.</span></span> <span data-ttu-id="e72a3-122">次の例では、評価し、レンダリングします。</span><span class="sxs-lookup"><span data-stu-id="e72a3-122">The following example evaluates and renders:</span></span>

* <span data-ttu-id="e72a3-123">`_headingFontStyle` CSS プロパティの値に`font-style`します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-123">`_headingFontStyle` to the CSS property value for `font-style`.</span></span>
* <span data-ttu-id="e72a3-124">`_headingText` コンテンツを`<h1>`要素。</span><span class="sxs-lookup"><span data-stu-id="e72a3-124">`_headingText` to the content of the `<h1>` element.</span></span>

```cshtml
<h1 style="font-style:@_headingFontStyle">@_headingText</h1>

@functions {
    private string _headingFontStyle = "italic";
    private string _headingText = "Put on your new Blazor!";
}
```

<span data-ttu-id="e72a3-125">コンポーネントが最初にレンダリングした後、コンポーネントには、イベントに応答には、そのレンダリング ツリーが再生成します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-125">After the component is initially rendered, the component regenerates its render tree in response to events.</span></span> <span data-ttu-id="e72a3-126">Razor のコンポーネントは、前の 1 つに対して新しいレンダリング ツリーを比較しますし、ブラウザーのドキュメント オブジェクト モデル (DOM) に変更を適用します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-126">Razor Components then compares the new render tree against the previous one and applies any modifications to the browser's Document Object Model (DOM).</span></span>

## <a name="using-components"></a><span data-ttu-id="e72a3-127">コンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-127">Using components</span></span>

<span data-ttu-id="e72a3-128">コンポーネントは、それらを宣言することでその他のコンポーネントを含めることができます HTML 要素の構文を使用します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-128">Components can include other components by declaring them using HTML element syntax.</span></span> <span data-ttu-id="e72a3-129">コンポーネントを使うためのマークアップは、そのコンポーネントの種類をタグ名とする HTML タグのようになります。</span><span class="sxs-lookup"><span data-stu-id="e72a3-129">The markup for using a component looks like an HTML tag where the name of the tag is the component type.</span></span>

<span data-ttu-id="e72a3-130">次のマークアップをレンダリングする`HeadingComponent`(*HeadingComponent.cshtml*) インスタンス。</span><span class="sxs-lookup"><span data-stu-id="e72a3-130">The following markup renders a `HeadingComponent` (*HeadingComponent.cshtml*) instance:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/Index.cshtml?name=snippet_HeadingComponent)]

## <a name="component-parameters"></a><span data-ttu-id="e72a3-131">コンポーネントのパラメーター</span><span class="sxs-lookup"><span data-stu-id="e72a3-131">Component parameters</span></span>

<span data-ttu-id="e72a3-132">コンポーネントを持つことができます*コンポーネント パラメーター*を使用して定義されている*非パブリック*で装飾されたコンポーネントのクラスのプロパティを`[Parameter]`します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-132">Components can have *component parameters*, which are defined using *non-public* properties on the component class decorated with `[Parameter]`.</span></span> <span data-ttu-id="e72a3-133">マークアップ内でコンポーネントの引数を指定するには、属性を使います。</span><span class="sxs-lookup"><span data-stu-id="e72a3-133">Use attributes to specify arguments for a component in markup.</span></span>

<span data-ttu-id="e72a3-134">次の例では、`ParentComponent`の値を設定、`Title`のプロパティ、 `ChildComponent`:</span><span class="sxs-lookup"><span data-stu-id="e72a3-134">In the following example, the `ParentComponent` sets the value of the `Title` property of the `ChildComponent`:</span></span>

<span data-ttu-id="e72a3-135">*ParentComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-135">*ParentComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ParentComponent.cshtml?name=snippet_ParentComponent&highlight=5)]

<span data-ttu-id="e72a3-136">*ChildComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-136">*ChildComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ChildComponent.cshtml?highlight=7-8)]

## <a name="child-content"></a><span data-ttu-id="e72a3-137">子コンテンツ</span><span class="sxs-lookup"><span data-stu-id="e72a3-137">Child content</span></span>

<span data-ttu-id="e72a3-138">コンポーネントは、別のコンポーネントのコンテンツを設定できます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-138">Components can set the content of another component.</span></span> <span data-ttu-id="e72a3-139">割り当てのコンポーネントは、受信側のコンポーネントを指定するタグの間でコンテンツを提供します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-139">The assigning component provides the content between the tags that specify the receiving component.</span></span> <span data-ttu-id="e72a3-140">たとえば、`ParentComponent`を追加できますコンテンツ レンダリング子コンポーネント内のコンテンツを配置することで`<ChildComponent>`タグ。</span><span class="sxs-lookup"><span data-stu-id="e72a3-140">For example, a `ParentComponent` can provide content for rendering by a Child component by placing the content inside `<ChildComponent>` tags.</span></span>

<span data-ttu-id="e72a3-141">*ParentComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-141">*ParentComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ParentComponent.cshtml?name=snippet_ParentComponent&highlight=6-7)]

<span data-ttu-id="e72a3-142">子コンポーネントには、`ChildContent`プロパティを表す、`RenderFragment`します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-142">The Child component has a `ChildContent` property that represents a `RenderFragment`.</span></span> <span data-ttu-id="e72a3-143">値`ChildContent`が配置されている子コンポーネントのマークアップでコンテンツをレンダリングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e72a3-143">The value of `ChildContent` is positioned in the child component's markup where the content should be rendered.</span></span> <span data-ttu-id="e72a3-144">次の例の値で`ChildContent`親コンポーネントから受け取り、ブートス トラップのパネルの内部に表示されます`panel-body`します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-144">In the following example, the value of `ChildContent` is received from the parent component and rendered inside the Bootstrap panel's `panel-body`.</span></span>

<span data-ttu-id="e72a3-145">*ChildComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-145">*ChildComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ChildComponent.cshtml?highlight=3,10-11)]

> [!NOTE]
> <span data-ttu-id="e72a3-146">プロパティの受信、`RenderFragment`コンテンツを指定する必要があります`ChildContent`慣例です。</span><span class="sxs-lookup"><span data-stu-id="e72a3-146">The property receiving the `RenderFragment` content must be named `ChildContent` by convention.</span></span>

## <a name="data-binding"></a><span data-ttu-id="e72a3-147">データ バインディング</span><span class="sxs-lookup"><span data-stu-id="e72a3-147">Data binding</span></span>

<span data-ttu-id="e72a3-148">両方のコンポーネントと DOM 要素へのデータ バインディングに抑え、`bind`属性。</span><span class="sxs-lookup"><span data-stu-id="e72a3-148">Data binding to both components and DOM elements is accomplished with the `bind` attribute.</span></span> <span data-ttu-id="e72a3-149">次の例では、バインド、 `ItalicsCheck`  チェック ボックスのプロパティは、状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-149">The following example binds the `ItalicsCheck` property to the check box's checked state:</span></span>

```cshtml
<input type="checkbox" class="form-check-input" id="italicsCheck" 
    bind="@_italicsCheck" />
```

<span data-ttu-id="e72a3-150">プロパティの値が更新のチェック ボックスが選択され、クリア、`true`と`false`、それぞれします。</span><span class="sxs-lookup"><span data-stu-id="e72a3-150">When the check box is selected and cleared, the property's value is updated to `true` and `false`, respectively.</span></span>

<span data-ttu-id="e72a3-151">チェック ボックスは、プロパティの値の変更への応答ではなく、コンポーネントが表示される場合にのみ、UI で更新されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-151">The check box is updated in the UI only when the component is rendered, not in response to changing the property's value.</span></span> <span data-ttu-id="e72a3-152">イベント ハンドラーのコードの実行後に、コンポーネント自体の表示に、ためプロパティの更新は、通常 UI に反映されます、すぐにします。</span><span class="sxs-lookup"><span data-stu-id="e72a3-152">Since components render themselves after event handler code executes, property updates are usually reflected in the UI immediately.</span></span>

<span data-ttu-id="e72a3-153">使用して`bind`で、`CurrentValue`プロパティ (`<input bind="@CurrentValue" />`) は本質的には、次と同じです。</span><span class="sxs-lookup"><span data-stu-id="e72a3-153">Using `bind` with a `CurrentValue` property (`<input bind="@CurrentValue" />`) is essentially equivalent to the following:</span></span>

```cshtml
<input value="@CurrentValue" 
    onchange="@((UIChangeEventArgs __e) => CurrentValue = __e.Value)" />
```

<span data-ttu-id="e72a3-154">コンポーネントが表示されるときに、`value`からは、入力要素の`CurrentValue`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="e72a3-154">When the component is rendered, the `value` of the input element comes from the `CurrentValue` property.</span></span> <span data-ttu-id="e72a3-155">ユーザーがテキスト ボックスに、ときに、`onchange`イベントが発生した、`CurrentValue`プロパティが変更された値に設定します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-155">When the user types in the text box, the `onchange` event is fired and the `CurrentValue` property is set to the changed value.</span></span> <span data-ttu-id="e72a3-156">実際には、コード生成は、もう少し複雑なので`bind`型変換が実行するいくつかのケースを処理します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-156">In reality, the code generation is a little more complex because `bind` handles a few cases where type conversions are performed.</span></span> <span data-ttu-id="e72a3-157">原則として、`bind`を持つ式の現在の値を関連付けます、`value`属性とハンドルの変更が登録済みのハンドラーを使用します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-157">In principle, `bind` associates the current value of an expression with a `value` attribute and handles changes using the registered handler.</span></span>

<span data-ttu-id="e72a3-158">**書式指定文字列**</span><span class="sxs-lookup"><span data-stu-id="e72a3-158">**Format strings**</span></span>

<span data-ttu-id="e72a3-159">データ バインディングが連携<xref:System.DateTime>書式指定文字列。</span><span class="sxs-lookup"><span data-stu-id="e72a3-159">Data binding works with <xref:System.DateTime> format strings.</span></span> <span data-ttu-id="e72a3-160">この時点で、通貨、数値の形式などの他の式の形式は使用できません。</span><span class="sxs-lookup"><span data-stu-id="e72a3-160">Other format expressions, such as currency or number formats, aren't available at this time.</span></span>

```cshtml
<input bind="@StartDate" format-value="yyyy-MM-dd" />

@functions {
    [Parameter]
    private DateTime StartDate { get; set; } = new DateTime(2020, 1, 1);
}
```

<span data-ttu-id="e72a3-161">`format-value`属性に適用する日付の書式を指定します、`value`の`input`要素。</span><span class="sxs-lookup"><span data-stu-id="e72a3-161">The `format-value` attribute specifies the date format to apply to the `value` of the `input` element.</span></span> <span data-ttu-id="e72a3-162">値を解析するの形式を使用してもときに、`onchange`イベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-162">The format is also used to parse the value when an `onchange` event occurs.</span></span>

<span data-ttu-id="e72a3-163">**コンポーネントのパラメーター**</span><span class="sxs-lookup"><span data-stu-id="e72a3-163">**Component parameters**</span></span>

<span data-ttu-id="e72a3-164">バインディングでは、コンポーネントのパラメーターも認識している`bind-{property}`コンポーネント間でプロパティ値をバインドすることができます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-164">Binding also recognizes component parameters, where `bind-{property}` can bind a property value across components.</span></span>

<span data-ttu-id="e72a3-165">次のコンポーネントを使用して`ChildComponent`し、バインド、`ParentYear`を親からのパラメーター、`Year`子コンポーネントにパラメーター。</span><span class="sxs-lookup"><span data-stu-id="e72a3-165">The following component uses `ChildComponent` and binds the `ParentYear` parameter from the parent to the `Year` parameter on the child component:</span></span>

<span data-ttu-id="e72a3-166">親コンポーネント:</span><span class="sxs-lookup"><span data-stu-id="e72a3-166">Parent component:</span></span>

```cshtml
@page "/ParentComponent"

<h1>Parent Component</h1>

<p>ParentYear: @ParentYear</p>

<ChildComponent bind-Year="@ParentYear" />

<button class="btn btn-primary" onclick="@ChangeTheYear">
    Change Year to 1986
</button>

@functions {
    [Parameter]
    private int ParentYear { get; set; } = 1978;

    void ChangeTheYear()
    {
        ParentYear = 1986;
    }
}
```

<span data-ttu-id="e72a3-167">子コンポーネント:</span><span class="sxs-lookup"><span data-stu-id="e72a3-167">Child component:</span></span>

```cshtml
<h2>Child Component</h2>

<p>Year: @Year</p>

@functions {
    [Parameter]
    private int Year { get; set; }

    [Parameter]
    private Action<int> YearChanged { get; set; }
}
```

<span data-ttu-id="e72a3-168">`Year`コンパニオンがあるために、パラメーターがバインド可能な`YearChanged`の型と一致するイベント、`Year`パラメーター。</span><span class="sxs-lookup"><span data-stu-id="e72a3-168">The `Year` parameter is bindable because it has a companion `YearChanged` event that matches the type of the `Year` parameter.</span></span>

<span data-ttu-id="e72a3-169">読み込み、`ParentComponent`次のマークアップを生成します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-169">Loading the `ParentComponent` produces the following markup:</span></span>

```html
<h1>Parent Component</h1>

<p>ParentYear: 1978</p>

<h2>Child Component</h2>

<p>Year: 1978</p>
```

<span data-ttu-id="e72a3-170">場合の値、`ParentYear`でボタンを選択してプロパティを変更、 `ParentComponent`、`Year`のプロパティ、`ChildComponent`が更新されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-170">If the value of the `ParentYear` property is changed by selecting the button in the `ParentComponent`, the `Year` property of the `ChildComponent` is updated.</span></span> <span data-ttu-id="e72a3-171">新しい値`Year`が UI に表示されるときに、`ParentComponent`持続は。</span><span class="sxs-lookup"><span data-stu-id="e72a3-171">The new value of `Year` is rendered in the UI when the `ParentComponent` is rerendered:</span></span>

```html
<h1>Parent Component</h1>

<p>ParentYear: 1986</p>

<h2>Child Component</h2>

<p>Year: 1986</p>
```

## <a name="event-handling"></a><span data-ttu-id="e72a3-172">イベント処理</span><span class="sxs-lookup"><span data-stu-id="e72a3-172">Event handling</span></span>

<span data-ttu-id="e72a3-173">Razor のコンポーネントは、イベント処理機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-173">Razor Components provide event handling features.</span></span> <span data-ttu-id="e72a3-174">HTML 要素の属性の名前付き`on<event>`(たとえば、 `onclick`、 `onsubmit`) デリゲートに型指定された値では、Razor のコンポーネントがイベント ハンドラーとして属性の値を処理します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-174">For an HTML element attribute named `on<event>` (for example, `onclick`, `onsubmit`) with a delegate-typed value, Razor Components treats the attribute's value as an event handler.</span></span> <span data-ttu-id="e72a3-175">属性の名前は常に始まる`on`します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-175">The attribute's name always starts with `on`.</span></span>

<span data-ttu-id="e72a3-176">次のコードは、`UpdateHeading`メソッド、UI で、ボタンが選択されている場合。</span><span class="sxs-lookup"><span data-stu-id="e72a3-176">The following code calls the `UpdateHeading` method when the button is selected in the UI:</span></span>

```cshtml
<button class="btn btn-primary" onclick="@UpdateHeading">
    Update heading
</button>

@functions {
    void UpdateHeading(UIMouseEventArgs e)
    {
        ...
    }
}
```

<span data-ttu-id="e72a3-177">次のコードは、`CheckboxChanged`メソッド、UI で、チェック ボックスが変更されたとき。</span><span class="sxs-lookup"><span data-stu-id="e72a3-177">The following code calls the `CheckboxChanged` method when the check box is changed in the UI:</span></span>

```cshtml
<input type="checkbox" class="form-check-input" onchange="@CheckboxChanged" />

@functions {
    void CheckboxChanged()
    {
        ...
    }
}
```

<span data-ttu-id="e72a3-178">イベント ハンドラーと非同期の戻り値できます、<xref:System.Threading.Tasks.Task>します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-178">Event handlers can also be asynchronous and return a <xref:System.Threading.Tasks.Task>.</span></span> <span data-ttu-id="e72a3-179">手動で呼び出す必要はありません`StateHasChanged()`します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-179">There's no need to manually call `StateHasChanged()`.</span></span> <span data-ttu-id="e72a3-180">発生したとき、例外が記録されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-180">Exceptions are logged when they occur.</span></span>

```cshtml
<button class="btn btn-primary" onclick="@UpdateHeading">
    Update heading
</button>

@functions {
    async Task UpdateHeading(UIMouseEventArgs e)
    {
        ...
    }
}
```

<span data-ttu-id="e72a3-181">一部のイベントのイベント固有のイベント引数の型が許可されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-181">For some events, event-specific event argument types are permitted.</span></span> <span data-ttu-id="e72a3-182">これらのイベントの種類のいずれかへのアクセスが必要でない場合は、メソッド呼び出しで必要はありません。</span><span class="sxs-lookup"><span data-stu-id="e72a3-182">If access to one of these event types isn't necessary, it isn't required in the method call.</span></span>

<span data-ttu-id="e72a3-183">サポートされているイベントの引数の一覧です。</span><span class="sxs-lookup"><span data-stu-id="e72a3-183">The list of supported event arguments is:</span></span>

* <span data-ttu-id="e72a3-184">UIEventArgs</span><span class="sxs-lookup"><span data-stu-id="e72a3-184">UIEventArgs</span></span>
* <span data-ttu-id="e72a3-185">UIChangeEventArgs</span><span class="sxs-lookup"><span data-stu-id="e72a3-185">UIChangeEventArgs</span></span>
* <span data-ttu-id="e72a3-186">UIKeyboardEventArgs</span><span class="sxs-lookup"><span data-stu-id="e72a3-186">UIKeyboardEventArgs</span></span>
* <span data-ttu-id="e72a3-187">UIMouseEventArgs</span><span class="sxs-lookup"><span data-stu-id="e72a3-187">UIMouseEventArgs</span></span>

<span data-ttu-id="e72a3-188">ラムダ式も使用できます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-188">Lambda expressions can also be used:</span></span>

```cshtml
<button onclick="@(e => Console.WriteLine("Hello, world!"))">Say hello</button>
```

<span data-ttu-id="e72a3-189">など、追加の値を終了すると便利では多くの場合、一連の要素を反復処理するときにします。</span><span class="sxs-lookup"><span data-stu-id="e72a3-189">It's often convenient to close over additional values, such as when iterating over a set of elements.</span></span> <span data-ttu-id="e72a3-190">次の例が 3 つを作成呼び出しの各ボタン`UpdateHeading`イベント引数を渡す (`UIMouseEventArgs`) やボタンの番号 (`buttonNumber`) UI で選択した場合。</span><span class="sxs-lookup"><span data-stu-id="e72a3-190">The following example creates three buttons, each of which calls `UpdateHeading` passing an event argument (`UIMouseEventArgs`) and its button number (`buttonNumber`) when selected in the UI:</span></span>

```cshtml
<h2>@message</h2>

@for (var i = 1; i < 4; i++)
{
    var buttonNumber = i;

    <button class="btn btn-primary" 
            onclick="@(e => UpdateHeading(e, buttonNumber))">
        Button #@i
    </button>
}

@functions {
    string message = "Select a button to learn its position.";

    void UpdateHeading(UIMouseEventArgs e, int buttonNumber)
    {
        message = $"You selected Button #{buttonNumber} at " +
            "mouse position: {e.ClientX} X {e.ClientY}.";
    }
}
```

## <a name="capture-references-to-components"></a><span data-ttu-id="e72a3-191">コンポーネントへの参照をキャプチャします。</span><span class="sxs-lookup"><span data-stu-id="e72a3-191">Capture references to components</span></span>

<span data-ttu-id="e72a3-192">コンポーネントの参照方法 get コンポーネントのインスタンスへの参照をように指定などのそのインスタンスにコマンドを発行できます`Show`または`Reset`します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-192">Component references provide a way get a reference to a component instance so that you can issue commands to that instance, such as `Show` or `Reset`.</span></span> <span data-ttu-id="e72a3-193">コンポーネントの参照をキャプチャするには、追加、`ref`子コンポーネントに属性し、子コンポーネントと同じ名前と同じ型のフィールドを定義します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-193">To capture a component reference, add a `ref` attribute to the child component and then define a field with the same name and the same type as the child component.</span></span>

```cshtml
<MyLoginDialog ref="loginDialog" ... />

@functions {
    MyLoginDialog loginDialog;

    void OnSomething()
    {
        loginDialog.Show();
    }
}
```

<span data-ttu-id="e72a3-194">コンポーネントが表示されるときに、`loginDialog`フィールドに入力されますが、`MyLoginDialog`子コンポーネントのインスタンス。</span><span class="sxs-lookup"><span data-stu-id="e72a3-194">When the component is rendered, the `loginDialog` field is populated with the `MyLoginDialog` child component instance.</span></span> <span data-ttu-id="e72a3-195">コンポーネントのインスタンス上の .NET メソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-195">You can then invoke .NET methods on the component instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e72a3-196">`loginDialog`コンポーネントが表示され、その出力に含まれる後にのみ変数が設定されます、`MyLoginDialog`要素。</span><span class="sxs-lookup"><span data-stu-id="e72a3-196">The `loginDialog` variable is only populated after the component is rendered and its output includes the `MyLoginDialog` element.</span></span> <span data-ttu-id="e72a3-197">その時点までは何も参照します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-197">Until that point, there's nothing to reference.</span></span> <span data-ttu-id="e72a3-198">コンポーネントには、レンダリングが完了した後は、コンポーネントの参照を操作、使用、`OnAfterRenderAsync`または`OnAfterRender`メソッド。</span><span class="sxs-lookup"><span data-stu-id="e72a3-198">To manipulate components references after the component has finished rendering, use the `OnAfterRenderAsync` or `OnAfterRender` methods.</span></span>

<span data-ttu-id="e72a3-199">同様の構文を使用してコンポーネントの参照をキャプチャ中に[要素の参照をキャプチャ](xref:razor-components/javascript-interop#capture-references-to-elements)、わけで、 [JavaScript の相互運用機能](xref:razor-components/javascript-interop)機能します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-199">While capturing component references uses a similar syntax to [capturing element references](xref:razor-components/javascript-interop#capture-references-to-elements), it isn't a [JavaScript interop](xref:razor-components/javascript-interop) feature.</span></span> <span data-ttu-id="e72a3-200">JavaScript コードに渡されたいないコンポーネントの参照.NET コードでのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-200">Component references aren't passed to JavaScript code; they're only used in .NET code.</span></span>

> [!NOTE]
> <span data-ttu-id="e72a3-201">**いない**コンポーネント参照を使用して子コンポーネントの状態を変更します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-201">Do **not** use component references to mutate the state of child components.</span></span> <span data-ttu-id="e72a3-202">代わりに、通常の宣言型のパラメーターを使用して、子コンポーネントにデータを渡します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-202">Instead, use normal declarative parameters to pass data to child components.</span></span> <span data-ttu-id="e72a3-203">これにより、正しい時刻に自動的にレンダリングする子コンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="e72a3-203">This causes child components to rerender at the correct times automatically.</span></span>

## <a name="lifecycle-methods"></a><span data-ttu-id="e72a3-204">ライフ サイクル メソッド</span><span class="sxs-lookup"><span data-stu-id="e72a3-204">Lifecycle methods</span></span>

<span data-ttu-id="e72a3-205">`OnInitAsync` `OnInit`コンポーネントを初期化するコードを実行します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-205">`OnInitAsync` and `OnInit` execute code to initialize the component.</span></span> <span data-ttu-id="e72a3-206">非同期操作を実行するには使用`OnInitAsync`と`await`操作にキーワード。</span><span class="sxs-lookup"><span data-stu-id="e72a3-206">To perform an asynchronous operation, use `OnInitAsync` and the `await` keyword on the operation:</span></span>

```csharp
protected override async Task OnInitAsync()
{
    await ...
}
```

<span data-ttu-id="e72a3-207">同期操作では、使用`OnInit`:</span><span class="sxs-lookup"><span data-stu-id="e72a3-207">For a synchronous operation, use `OnInit`:</span></span>

```csharp
protected override void OnInit()
{
    ...
}
```

<span data-ttu-id="e72a3-208">`OnParametersSetAsync` `OnParametersSet`コンポーネントがその親からパラメーターを受信し、値がプロパティに割り当てられている場合に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-208">`OnParametersSetAsync` and `OnParametersSet` are called when a component has received parameters from its parent and the values are assigned to properties.</span></span> <span data-ttu-id="e72a3-209">これらのメソッドは、コンポーネントの初期化後に実行され、たびに、コンポーネントがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-209">These methods are executed after component initialization and then each time the component is rendered:</span></span>

```csharp
protected override async Task OnParametersSetAsync()
{
    await ...
}
```

```csharp
protected override void OnParametersSet()
{
    ...
}
```

<span data-ttu-id="e72a3-210">`OnAfterRenderAsync` `OnAfterRender`は、コンポーネントには、レンダリングが完了した後に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-210">`OnAfterRenderAsync` and `OnAfterRender` are called after a component has finished rendering.</span></span> <span data-ttu-id="e72a3-211">要素とコンポーネントの参照は、この時点で設定されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-211">Element and component references are populated at this point.</span></span> <span data-ttu-id="e72a3-212">この段階を使用すると、レンダリングされた DOM 要素を操作するサードパーティ製の JavaScript ライブラリをアクティブ化など、描画されるコンテンツを使用して追加の初期化手順を実行できます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-212">Use this stage to perform additional initialization steps using the rendered content, such as activating third-party JavaScript libraries that operate on the rendered DOM elements.</span></span>

```csharp
protected override async Task OnAfterRenderAsync()
{
    await ...
}
```

```csharp
protected override void OnAfterRender()
{
    ...
}
```

<span data-ttu-id="e72a3-213">`SetParameters` パラメーターが設定される前にコードを実行する上書きできます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-213">`SetParameters` can be overridden to execute code before parameters are set:</span></span>

```csharp
public override void SetParameters(ParameterCollection parameters)
{
    ...

    base.SetParameters(parameters);
}
```

<span data-ttu-id="e72a3-214">場合`base.SetParameters`いない呼び出されると、カスタム コードは必要な方法で受信したパラメーター値を解釈できます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-214">If `base.SetParameters` isn't invoked, the custom code can interpret the incoming parameters value in any way required.</span></span> <span data-ttu-id="e72a3-215">たとえば、受信パラメーターは、クラスのプロパティに割り当てられる必要ありません。</span><span class="sxs-lookup"><span data-stu-id="e72a3-215">For example, the incoming parameters aren't required to be assigned to the properties on the class.</span></span>

<span data-ttu-id="e72a3-216">`ShouldRender` UI の更新を抑制するのにはオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-216">`ShouldRender` can be overridden to suppress refreshing of the UI.</span></span> <span data-ttu-id="e72a3-217">実装を返す場合`true`UI が更新されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-217">If the implementation returns `true`, the UI is refreshed.</span></span> <span data-ttu-id="e72a3-218">場合でも`ShouldRender`がオーバーライドされると、コンポーネントは常に最初にレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="e72a3-218">Even if `ShouldRender` is overridden, the component is always initially rendered.</span></span>

```csharp
protected override bool ShouldRender()
{
    var renderUI = true;

    return renderUI;
}
```

## <a name="component-disposal-with-idisposable"></a><span data-ttu-id="e72a3-219">IDisposable とコンポーネントの破棄</span><span class="sxs-lookup"><span data-stu-id="e72a3-219">Component disposal with IDisposable</span></span>

<span data-ttu-id="e72a3-220">コンポーネントを実装している場合<xref:System.IDisposable>、 [Dispose メソッド](/dotnet/standard/garbage-collection/implementing-dispose)UI からコンポーネントを削除するときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-220">If a component implements <xref:System.IDisposable>, the [Dispose method](/dotnet/standard/garbage-collection/implementing-dispose) is called when the component is removed from the UI.</span></span> <span data-ttu-id="e72a3-221">次のコンポーネントを使用して`@implements IDisposable`と`Dispose`メソッド。</span><span class="sxs-lookup"><span data-stu-id="e72a3-221">The following component uses `@implements IDisposable` and the `Dispose` method:</span></span>

```csharp
@using System
@implements IDisposable

...

@functions {
    public void Dispose()
    {
        ...
    }
}
```

## <a name="routing"></a><span data-ttu-id="e72a3-222">ルーティング</span><span class="sxs-lookup"><span data-stu-id="e72a3-222">Routing</span></span>

<span data-ttu-id="e72a3-223">Razor のコンポーネントでのルーティングは、アプリでアクセス可能な各コンポーネントにルート テンプレートを提供することによって実現されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-223">Routing in Razor Components is achieved by providing a route template to each accessible component in the app.</span></span>

<span data-ttu-id="e72a3-224">ときに、 *.cshtml*ファイルと、`@page`ディレクティブをコンパイルすると、生成されたクラスが指定された、<xref:Microsoft.AspNetCore.Mvc.RouteAttribute>ルート テンプレートを指定します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-224">When a *.cshtml* file with an `@page` directive is compiled, the generated class is given a <xref:Microsoft.AspNetCore.Mvc.RouteAttribute> specifying the route template.</span></span> <span data-ttu-id="e72a3-225">ルーターが持つクラスでコンポーネントが、実行時に、`RouteAttribute`どのコンポーネントが要求された URL に一致するルート テンプレートを表示します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-225">At runtime, the router looks for component classes with a `RouteAttribute` and renders whichever component has a route template that matches the requested URL.</span></span>

<span data-ttu-id="e72a3-226">コンポーネントには、複数のルート テンプレートを適用できます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-226">Multiple route templates can be applied to a component.</span></span> <span data-ttu-id="e72a3-227">次のコンポーネントがの要求に応答`/BlazorRoute`と`/DifferentBlazorRoute`:</span><span class="sxs-lookup"><span data-stu-id="e72a3-227">The following component responds to requests for `/BlazorRoute` and `/DifferentBlazorRoute`:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?name=snippet_BlazorRoute)]

## <a name="route-parameters"></a><span data-ttu-id="e72a3-228">ルート パラメーター</span><span class="sxs-lookup"><span data-stu-id="e72a3-228">Route parameters</span></span>

<span data-ttu-id="e72a3-229">コンポーネントで提供されるルート テンプレートからルート パラメーターを受け取ることができます、`@page`ディレクティブ。</span><span class="sxs-lookup"><span data-stu-id="e72a3-229">Components can receive route parameters from the route template provided in the `@page` directive.</span></span> <span data-ttu-id="e72a3-230">ルーターでは、ルート パラメーターを使用して、対応するコンポーネントのパラメーターを設定します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-230">The router uses route parameters to populate the corresponding component parameters.</span></span>

<span data-ttu-id="e72a3-231">*RouteParameter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-231">*RouteParameter.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?name=snippet_RouteParameter)]

<span data-ttu-id="e72a3-232">省略可能なパラメーターはサポートされていませんので、2 つ`@page`ディレクティブは、上記の例に適用されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-232">Optional parameters aren't supported, so two `@page` directives are applied in the example above.</span></span> <span data-ttu-id="e72a3-233">最初のパラメーターを指定せず、コンポーネントへの移動を許可します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-233">The first permits navigation to the component without a parameter.</span></span> <span data-ttu-id="e72a3-234">2 番目の`@page`ディレクティブは、`{text}`ルート パラメーターと値を割り当てます、`Text`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="e72a3-234">The second `@page` directive takes the `{text}` route parameter and assigns the value to the `Text` property.</span></span>

## <a name="base-class-inheritance-for-a-code-behind-experience"></a><span data-ttu-id="e72a3-235">「分離コード」エクスペリエンスのための基本クラスの継承</span><span class="sxs-lookup"><span data-stu-id="e72a3-235">Base class inheritance for a "code-behind" experience</span></span>

<span data-ttu-id="e72a3-236">コンポーネント ファイル (*.cshtml*) の HTML マークアップを混在させるとC#同じファイル内のコードを処理します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-236">Component files (*.cshtml*) mix HTML markup and C# processing code in the same file.</span></span> <span data-ttu-id="e72a3-237">`@inherits`ディレクティブを使用して、Razor コンポーネント アプリ コンポーネントのマークアップを処理のコードから分離する「分離コード」エクスペリエンスを提供することができます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-237">The `@inherits` directive can be used to provide Razor Components apps with a "code-behind" experience that separates component markup from processing code.</span></span>

<span data-ttu-id="e72a3-238">[サンプル アプリ](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)コンポーネントが、基底クラスを継承する方法を示しています。 `BlazorRocksBase`、コンポーネントのプロパティとメソッドを提供します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-238">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) shows how a component can inherit a base class, `BlazorRocksBase`, to provide the component's properties and methods.</span></span>

<span data-ttu-id="e72a3-239">*BlazorRocks.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-239">*BlazorRocks.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRocks.cshtml?name=snippet_BlazorRocks)]

<span data-ttu-id="e72a3-240">*BlazorRocksBase.cs*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-240">*BlazorRocksBase.cs*:</span></span>

[!code-csharp[](common/samples/3.x/BlazorSample/Pages/BlazorRocksBase.cs)]

<span data-ttu-id="e72a3-241">基底クラスの派生元`BlazorComponent`します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-241">The base class should derive from `BlazorComponent`.</span></span>

## <a name="razor-support"></a><span data-ttu-id="e72a3-242">Razor サポート</span><span class="sxs-lookup"><span data-stu-id="e72a3-242">Razor support</span></span>

<span data-ttu-id="e72a3-243">**Razor ディレクティブ**</span><span class="sxs-lookup"><span data-stu-id="e72a3-243">**Razor directives**</span></span>

<span data-ttu-id="e72a3-244">Razor ディレクティブは、次の表に表示されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-244">Razor directives are shown in the following table.</span></span>

| <span data-ttu-id="e72a3-245">ディレクティブ</span><span class="sxs-lookup"><span data-stu-id="e72a3-245">Directive</span></span> | <span data-ttu-id="e72a3-246">説明</span><span class="sxs-lookup"><span data-stu-id="e72a3-246">Description</span></span> |
| --------- | ----------- |
| [<span data-ttu-id="e72a3-247">\@関数</span><span class="sxs-lookup"><span data-stu-id="e72a3-247">\@functions</span></span>](xref:mvc/views/razor#section-5) | <span data-ttu-id="e72a3-248">追加、C#コンポーネントにコード ブロックです。</span><span class="sxs-lookup"><span data-stu-id="e72a3-248">Adds a C# code block to a component.</span></span> |
| `@implements` | <span data-ttu-id="e72a3-249">生成されたコンポーネントのクラスのインターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-249">Implements an interface for the generated component class.</span></span> |
| [<span data-ttu-id="e72a3-250">\@継承</span><span class="sxs-lookup"><span data-stu-id="e72a3-250">\@inherits</span></span>](xref:mvc/views/razor#section-3) | <span data-ttu-id="e72a3-251">コンポーネントが継承するクラスの完全に制御を提供します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-251">Provides full control of the class that the component inherits.</span></span> |
| [<span data-ttu-id="e72a3-252">\@挿入します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-252">\@inject</span></span>](xref:mvc/views/razor#section-4) | <span data-ttu-id="e72a3-253">サービスからの挿入のことができます、[サービス コンテナー](xref:fundamentals/dependency-injection)します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-253">Enables service injection from the [service container](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="e72a3-254">詳しくは、「[ビューへの依存関係の挿入](xref:mvc/views/dependency-injection)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e72a3-254">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span> |
| `@layout` | <span data-ttu-id="e72a3-255">レイアウト コンポーネントを指定します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-255">Specifies a layout component.</span></span> <span data-ttu-id="e72a3-256">レイアウト コンポーネントは、コードの重複や不整合を回避するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-256">Layout components are used to avoid code duplication and inconsistency.</span></span> |
| [<span data-ttu-id="e72a3-257">\@ページ</span><span class="sxs-lookup"><span data-stu-id="e72a3-257">\@page</span></span>](xref:razor-pages/index#razor-pages) | <span data-ttu-id="e72a3-258">コンポーネントの処理で要求が直接処理する必要がありますを指定します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-258">Specifies that the component should handle requests directly.</span></span> <span data-ttu-id="e72a3-259">`@page`ディレクティブは、ルートと省略可能なパラメーターで指定できます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-259">The `@page` directive can be specified with a route and optional parameters.</span></span> <span data-ttu-id="e72a3-260">Razor ページとは異なり、`@page`ディレクティブは、ファイルの先頭で最初のディレクティブを指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="e72a3-260">Unlike Razor Pages, the `@page` directive doesn't need to be the first directive at the top of the file.</span></span> <span data-ttu-id="e72a3-261">詳細については、[ルーティング](xref:razor-components/routing)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="e72a3-261">For more information, see [Routing](xref:razor-components/routing).</span></span> |
| [<span data-ttu-id="e72a3-262">\@using</span><span class="sxs-lookup"><span data-stu-id="e72a3-262">\@using</span></span>](xref:mvc/views/razor#using) | <span data-ttu-id="e72a3-263">追加、 C# `using`ディレクティブを生成されたコンポーネントのクラスにします。</span><span class="sxs-lookup"><span data-stu-id="e72a3-263">Adds the C# `using` directive to the generated component class.</span></span> |
| [<span data-ttu-id="e72a3-264">\@addTagHelper</span><span class="sxs-lookup"><span data-stu-id="e72a3-264">\@addTagHelper</span></span>](xref:mvc/views/razor#tag-helpers) | <span data-ttu-id="e72a3-265">使用して、`@addTagHelper`アプリのアセンブリよりも別のアセンブリでコンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-265">Use `@addTagHelper` to use a component in a different assembly than the app's assembly.</span></span> |

<span data-ttu-id="e72a3-266">**条件付き属性**</span><span class="sxs-lookup"><span data-stu-id="e72a3-266">**Conditional attributes**</span></span>

<span data-ttu-id="e72a3-267">属性は、.NET の値に基づく条件付きで表示されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-267">Attributes are conditionally rendered based on the .NET value.</span></span> <span data-ttu-id="e72a3-268">値が場合`false`または`null`属性は表示されません。</span><span class="sxs-lookup"><span data-stu-id="e72a3-268">If the value is `false` or `null`,  the attribute isn't rendered.</span></span> <span data-ttu-id="e72a3-269">値が場合`true`属性はレンダリングを最小限に抑えます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-269">If the value is `true`, the attribute is rendered minimized.</span></span>

<span data-ttu-id="e72a3-270">次の例では、`IsCompleted`かどうかを`checked`コントロールのマークアップに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-270">In the following example, `IsCompleted` determines if `checked` is rendered in the control's markup:</span></span>

```cshtml
<input type="checkbox" checked="@IsCompleted" />

@functions {
    [Parameter]
    private bool IsCompleted { get; set; }
}
```

<span data-ttu-id="e72a3-271">場合`IsCompleted`は`true`、チェック ボックスとしてレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-271">If `IsCompleted` is `true`, the check box is rendered as:</span></span>

```html
<input type="checkbox" checked />
```

<span data-ttu-id="e72a3-272">場合`IsCompleted`は`false`、チェック ボックスとしてレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-272">If `IsCompleted` is `false`, the check box is rendered as:</span></span>

```html
<input type="checkbox" />
```

<span data-ttu-id="e72a3-273">**Razor で追加情報**</span><span class="sxs-lookup"><span data-stu-id="e72a3-273">**Additional information on Razor**</span></span>

<span data-ttu-id="e72a3-274">Razor の詳細については、次を参照してください。、 [Razor 構文リファレンス](xref:mvc/views/razor)します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-274">For more information on Razor, see the [Razor syntax reference](xref:mvc/views/razor).</span></span>

## <a name="raw-html"></a><span data-ttu-id="e72a3-275">生の HTML</span><span class="sxs-lookup"><span data-stu-id="e72a3-275">Raw HTML</span></span>

<span data-ttu-id="e72a3-276">文字列は通常を使用してレンダリング DOM テキスト ノード、つまりを含めることはすべてのマークアップは無視され、リテラル テキストとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-276">Strings are normally rendered using DOM text nodes, which means that any markup they may contain is ignored and treated as literal text.</span></span> <span data-ttu-id="e72a3-277">生の HTML をレンダリングするの HTML コンテンツをラップする`MarkupString`値。</span><span class="sxs-lookup"><span data-stu-id="e72a3-277">To render raw HTML, wrap the HTML content in a `MarkupString` value.</span></span> <span data-ttu-id="e72a3-278">値が HTML または SVG として解析され、DOM に挿入</span><span class="sxs-lookup"><span data-stu-id="e72a3-278">The value is parsed as HTML or SVG and inserted into the DOM.</span></span>

> [!WARNING]
> <span data-ttu-id="e72a3-279">いずれかから構築された生の HTML のレンダリングには、ソースが信頼されていない、**セキュリティ リスク**と避ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="e72a3-279">Rendering raw HTML constructed from any untrusted source is a **security risk** and should be avoided!</span></span>

<span data-ttu-id="e72a3-280">次の例を使用して、`MarkupString`コンポーネントの出力に静的な HTML コンテンツのブロックを追加する型。</span><span class="sxs-lookup"><span data-stu-id="e72a3-280">The following example shows using the `MarkupString` type to add a block of static HTML content to the rendered output of a component:</span></span>

```html
@((MarkupString)myMarkup)

@functions {
    string myMarkup = "<p class='markup'>This is a <em>markup string</em>.</p>";
}
```

## <a name="templated-components"></a><span data-ttu-id="e72a3-281">テンプレート化されたコンポーネント</span><span class="sxs-lookup"><span data-stu-id="e72a3-281">Templated components</span></span>

<span data-ttu-id="e72a3-282">テンプレート化されたコンポーネントは、コンポーネントのレンダリング ロジックの一部として使用できますし、パラメーターとして 1 つまたは複数の UI テンプレートをそのまま使用するコンポーネント。</span><span class="sxs-lookup"><span data-stu-id="e72a3-282">Templated components are components that accept one or more UI templates as parameters, which can then be used as part of the component's rendering logic.</span></span> <span data-ttu-id="e72a3-283">テンプレート化されたコンポーネントを使用するより正規のコンポーネントも再利用可能なよりは上位レベルのコンポーネントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-283">Templated components allow you to author higher-level components that are more reusable than regular components.</span></span> <span data-ttu-id="e72a3-284">いくつかの例は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e72a3-284">A couple of examples include:</span></span>

* <span data-ttu-id="e72a3-285">ユーザーがテーブルのヘッダー、行、およびフッターのテンプレートを指定できるテーブル コンポーネント。</span><span class="sxs-lookup"><span data-stu-id="e72a3-285">A table component that allows a user to specify templates for the table's header, rows, and footer.</span></span>
* <span data-ttu-id="e72a3-286">ユーザーがリスト アイテムのレンダリング用のテンプレートで指定できるリスト コンポーネント。</span><span class="sxs-lookup"><span data-stu-id="e72a3-286">A list component that allows a user to specify a template for rendering items in a list.</span></span>

### <a name="template-parameters"></a><span data-ttu-id="e72a3-287">テンプレート パラメーター</span><span class="sxs-lookup"><span data-stu-id="e72a3-287">Template parameters</span></span>

<span data-ttu-id="e72a3-288">型の 1 つまたは複数のコンポーネント パラメーターを指定して、テンプレート化されたコンポーネントが定義されている`RenderFragment`または`RenderFragment<T>`します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-288">A templated component is defined by specifying one or more component parameters of type `RenderFragment` or `RenderFragment<T>`.</span></span> <span data-ttu-id="e72a3-289">レンダリングのフラグメントでは、コンポーネントによって表示される UI のセグメントを表します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-289">A render fragment represents a segment of UI that is rendered by the component.</span></span> <span data-ttu-id="e72a3-290">レンダリングのフラグメントは、必要に応じて、レンダリングのフラグメントが呼び出されたときに指定できるパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="e72a3-290">A render fragment optionally takes a parameter that can be specified when the render fragment is invoked.</span></span>

<span data-ttu-id="e72a3-291">*Components/TableTemplate.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-291">*Components/TableTemplate.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/TableTemplate.cshtml)]

<span data-ttu-id="e72a3-292">パラメーターの名前に一致する子要素を使用して、テンプレート パラメーターを指定できます、テンプレート化されたコンポーネントを使用する場合 (`TableHeader`と`RowTemplate`次の例)。</span><span class="sxs-lookup"><span data-stu-id="e72a3-292">When using a templated component, the template parameters can be specified using child elements that match the names of the parameters (`TableHeader` and `RowTemplate` in the following example):</span></span>

```cshtml
<TableTemplate Items="@pets">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate>
        <td>@context.PetId</td>
        <td>@context.Name</td>
    </RowTemplate>
</TableTemplate>
```

### <a name="template-context-parameters"></a><span data-ttu-id="e72a3-293">テンプレートのコンテキスト パラメーター</span><span class="sxs-lookup"><span data-stu-id="e72a3-293">Template context parameters</span></span>

<span data-ttu-id="e72a3-294">型のコンポーネントの引数`RenderFragment<T>`要素があるという名前の暗黙のパラメーターとして渡された`context`(たとえば、上記のコード サンプルから`@context.PetId`)、使用して、パラメーター名を変更することが、`Context`子の属性要素。</span><span class="sxs-lookup"><span data-stu-id="e72a3-294">Component arguments of type `RenderFragment<T>` passed as elements have an implicit parameter named `context` (for example from the preceding code sample, `@context.PetId`), but you can change the parameter name using the `Context` attribute on the child element.</span></span> <span data-ttu-id="e72a3-295">次の例では、`RowTemplate`要素の`Context`属性を指定します、`pet`パラメーター。</span><span class="sxs-lookup"><span data-stu-id="e72a3-295">In the following example, the `RowTemplate` element's `Context` attribute specifies the `pet` parameter:</span></span>

```cshtml
<TableTemplate Items="@pets">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate Context="pet">
        <td>@pet.PetId</td>
        <td>@pet.Name</td>
    </RowTemplate>
</TableTemplate>
```

<span data-ttu-id="e72a3-296">または、指定することができます、`Context`コンポーネント要素の属性。</span><span class="sxs-lookup"><span data-stu-id="e72a3-296">Alternatively, you can specify the `Context` attribute on the component element.</span></span> <span data-ttu-id="e72a3-297">指定した`Context`属性は、すべての指定したテンプレート パラメーターに適用されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-297">The specified `Context` attribute applies to all specified template parameters.</span></span> <span data-ttu-id="e72a3-298">暗黙の型の子コンテンツのコンテンツのパラメーター名を指定する場合に便利なこのできます (任意の折り返しなしの子要素)。</span><span class="sxs-lookup"><span data-stu-id="e72a3-298">This can be useful when you want to specify the content parameter name for implicit child content (without any wrapping child element).</span></span> <span data-ttu-id="e72a3-299">次の例では、`Context`属性に表示されます、`TableTemplate`要素と、すべてのテンプレート パラメーターに適用されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-299">In the following example, the `Context` attribute appears on the `TableTemplate` element and applies to all template parameters:</span></span>

```cshtml
<TableTemplate Items="@pets" Context="pet">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate>
        <td>@pet.PetId</td>
        <td>@pet.Name</td>
    </RowTemplate>
</TableTemplate>
```

### <a name="generic-typed-components"></a><span data-ttu-id="e72a3-300">汎用型のコンポーネント</span><span class="sxs-lookup"><span data-stu-id="e72a3-300">Generic-typed components</span></span>

<span data-ttu-id="e72a3-301">テンプレート化されたコンポーネントは、多くの場合、一般的に入力します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-301">Templated components are often generically typed.</span></span> <span data-ttu-id="e72a3-302">汎用リスト ビュー テンプレートのコンポーネントを使用して、表示するために、`IEnumerable<T>`値。</span><span class="sxs-lookup"><span data-stu-id="e72a3-302">For example, a generic List View Template component can be used to render `IEnumerable<T>` values.</span></span> <span data-ttu-id="e72a3-303">汎用のコンポーネントを定義するには、使用、`@typeparam`型パラメーターを指定するディレクティブ。</span><span class="sxs-lookup"><span data-stu-id="e72a3-303">To define a generic component, use the `@typeparam` directive to specify type parameters.</span></span>

<span data-ttu-id="e72a3-304">*Components/ListViewTemplate.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-304">*Components/ListViewTemplate.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/ListViewTemplate.cshtml?highlight=1)]

<span data-ttu-id="e72a3-305">ジェネリック型指定されたコンポーネントを使用する場合、型パラメーターが可能であれば推論されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-305">When using generic-typed components, the type parameter is inferred if possible:</span></span>

```cshtml
<ListViewTemplate Items="@pets">
    <ItemTemplate Context="pet">
        <li>@pet.Name</li>
    </ItemTemplate>
</ListViewTemplate>
```

<span data-ttu-id="e72a3-306">それ以外の場合、型パラメーターする必要があります明示的に指定する型パラメーターの名前に一致する属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-306">Otherwise, the type parameter must be explicitly specified using an attribute that matches the name of the type parameter.</span></span> <span data-ttu-id="e72a3-307">次の例では、`TItem="Pet"`種類を指定します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-307">In the following example, `TItem="Pet"` specifies the type:</span></span>

```cshtml
<ListViewTemplate Items="@pets" TItem="Pet">
    <ItemTemplate Context="pet">
        <li>@pet.Name</li>
    </ItemTemplate>
</ListViewTemplate>
```

## <a name="cascading-values-and-parameters"></a><span data-ttu-id="e72a3-308">カスケード型の値とパラメーター</span><span class="sxs-lookup"><span data-stu-id="e72a3-308">Cascading values and parameters</span></span>

<span data-ttu-id="e72a3-309">一部のシナリオで便利ではありませんフローのデータを使用して子孫コンポーネントに先祖コンポーネントから[コンポーネント パラメーター](#component-parameters)いくつかのコンポーネントのレイヤーがある場合は特に、します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-309">In some scenarios, it's inconvenient to flow data from an ancestor component to a descendent component using [component parameters](#component-parameters), especially when there are several component layers.</span></span> <span data-ttu-id="e72a3-310">カスケード型の値およびパラメーターは、先祖コンポーネントをすべてその子孫のコンポーネントの値を指定する便利な方法を提供することでこの問題を解決します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-310">Cascading values and parameters solve this problem by providing a convenient way for an ancestor component to provide a value to all of its descendent components.</span></span> <span data-ttu-id="e72a3-311">カスケード型の値とパラメーターは、コンポーネントを調整するための方法も提供します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-311">Cascading values and parameters also provide an approach for components to coordinate.</span></span>

### <a name="theme-example"></a><span data-ttu-id="e72a3-312">テーマの使用例</span><span class="sxs-lookup"><span data-stu-id="e72a3-312">Theme example</span></span>

<span data-ttu-id="e72a3-313">次に*テーマ*例、サンプル アプリから、`ThemeInfo`クラスのすべてのアプリの特定の部分内でボタンと同じスタイルを共有できるように、コンポーネントの階層の下位に伝達するテーマ情報を指定します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-313">In the following *Theme* example from the sample app, the `ThemeInfo` class specifies the theme information to flow down the component hierarchy so that all of the buttons within a given part of the app share the same style.</span></span>

<span data-ttu-id="e72a3-314">*UIThemeClasses/ThemeInfo.cs*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-314">*UIThemeClasses/ThemeInfo.cs*:</span></span>

```csharp
public class ThemeInfo
{
    public string ButtonClass { get; set; }
}
```

<span data-ttu-id="e72a3-315">先祖、コンポーネントには、カスケード型の値のコンポーネントを使用してカスケード型の値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-315">An ancestor component can provide a cascading value using the Cascading Value component.</span></span> <span data-ttu-id="e72a3-316">値のカスケード コンポーネントは、コンポーネントの階層のサブツリーをラップし、そのサブツリー内のすべてのコンポーネントの 1 つの値を提供します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-316">The Cascading Value component wraps a subtree of the component hierarchy and supplies a single value to all components within that subtree.</span></span>

<span data-ttu-id="e72a3-317">たとえば、サンプル アプリには、テーマ情報を指定します。 (`ThemeInfo`) のレイアウトの本文を構成するすべてのコンポーネントのカスケード型パラメーターとして、アプリのレイアウトのいずれかで、`@Body`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="e72a3-317">For example, the sample app specifies theme information (`ThemeInfo`) in one of the app's layouts as a cascading parameter for all components that make up the layout body of the `@Body` property.</span></span> <span data-ttu-id="e72a3-318">`ButtonClass` 値が割り当てられている`btn-success`レイアウト コンポーネント。</span><span class="sxs-lookup"><span data-stu-id="e72a3-318">`ButtonClass` is assigned a value of `btn-success` in the layout component.</span></span> <span data-ttu-id="e72a3-319">任意の子孫のコンポーネントを使用してこのプロパティを使用できる、`ThemeInfo`カスケード型のオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="e72a3-319">Any descendent component can consume this property through the `ThemeInfo` cascading object.</span></span>

<span data-ttu-id="e72a3-320">*Shared/CascadingValuesParametersLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-320">*Shared/CascadingValuesParametersLayout.cshtml*:</span></span>

```cshtml
@inherits BlazorLayoutComponent
@using BlazorSample.UIThemeClasses

<div class="container-fluid">
    <div class="row">
        <div class="col-sm-3">
            <NavMenu />
        </div>
        <div class="col-sm-9">
            <CascadingValue Value="@theme">
                <div class="content px-4">
                    @Body
                </div>
            </CascadingValue>
        </div>
    </div>
</div>

@functions {
    ThemeInfo theme = new ThemeInfo { ButtonClass = "btn-success" };
}
```

<span data-ttu-id="e72a3-321">させるのカスケード型の値を使用して、コンポーネントを使用してカスケード型パラメーターの宣言、`[CascadingParameter]`属性または名前の文字列値に基づきます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-321">To make use of cascading values, components declare cascading parameters using the `[CascadingParameter]` attribute or based on a string name value:</span></span>

```cshtml
<CascadingValue Value=@PermInfo Name="UserPermissions">...</CascadingValue>

[CascadingParameter(Name = "UserPermissions")] PermInfo Permissions { get; set; }
```

<span data-ttu-id="e72a3-322">文字列名の値を持つバインドは、同じサブツリー内で区別する必要があり、同じ種類の複数のカスケード型の値をした場合に関連します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-322">Binding with a string name value is relevant if you have multiple cascading values of the same type and need to differentiate them within the same subtree.</span></span>

<span data-ttu-id="e72a3-323">カスケード型の値は、型でカスケード型パラメーターにバインドされます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-323">Cascading values are bound to cascading parameters by type.</span></span>

<span data-ttu-id="e72a3-324">サンプル アプリで、値パラメーターのテーマのカスケード コンポーネントのバインドを`ThemeInfo`カスケード型パラメーターをカスケード型の値。</span><span class="sxs-lookup"><span data-stu-id="e72a3-324">In the sample app, the Cascading Values Parameters Theme component binds to the `ThemeInfo` cascading value to a cascading parameter.</span></span> <span data-ttu-id="e72a3-325">パラメーターは、コンポーネントによって表示されるボタンのいずれかの CSS クラスの設定に使用されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-325">The parameter is used to set the CSS class for one of the buttons displayed by the component.</span></span>

<span data-ttu-id="e72a3-326">*Pages/CascadingValuesParametersTheme.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-326">*Pages/CascadingValuesParametersTheme.cshtml*:</span></span>

```cshtml
@page "/cascadingvaluesparameterstheme"
@layout CascadingValuesParametersLayout
@using BlazorSample.UIThemeClasses

<h1>Cascading Values & Parameters</h1>

<p>Current count: @currentCount</p>

<p>
    <button class="btn" onclick="@IncrementCount">
        Increment Counter (Unthemed)
    </button>
</p>

<p>
    <button class="btn @ThemeInfo.ButtonClass" onclick="@IncrementCount">
        Increment Counter (Themed)
    </button>
</p>

@functions {
    int currentCount = 0;

    [CascadingParameter] protected ThemeInfo ThemeInfo { get; set; }

    void IncrementCount()
    {
        currentCount++;
    }
}
```

### <a name="tabset-example"></a><span data-ttu-id="e72a3-327">タブの例</span><span class="sxs-lookup"><span data-stu-id="e72a3-327">TabSet example</span></span>

<span data-ttu-id="e72a3-328">カスケード型パラメーターでは、コンポーネント、コンポーネントの階層全体で共同作業を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-328">Cascading parameters also enable components to collaborate across the component hierarchy.</span></span> <span data-ttu-id="e72a3-329">たとえば、次*タブ*サンプル アプリでの使用例です。</span><span class="sxs-lookup"><span data-stu-id="e72a3-329">For example, consider the following *TabSet* example in the sample app.</span></span>

<span data-ttu-id="e72a3-330">サンプル アプリには、`ITab`タブを実装するインターフェイス。</span><span class="sxs-lookup"><span data-stu-id="e72a3-330">The sample app has an `ITab` interface that tabs implement:</span></span>

[!code-cs[](common/samples/3.x/BlazorSample/UIInterfaces/ITab.cs)]

<span data-ttu-id="e72a3-331">値パラメーターのタブのカスケード コンポーネント タブのいくつかのコンポーネントが含まれています、タブ設定コンポーネントを使用します。</span><span class="sxs-lookup"><span data-stu-id="e72a3-331">The Cascading Values Parameters TabSet component uses the Tab Set component, which contains several Tab components:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/CascadingValuesParametersTabSet.cshtml?name=snippet_TabSet)]

<span data-ttu-id="e72a3-332">タブの子コンポーネントは タブの設定を明示的にパラメーターとして渡されます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-332">The child Tab components aren't explicitly passed as parameters to the Tab Set.</span></span> <span data-ttu-id="e72a3-333">代わりに、タブの子コンポーネントには、タブのセットの子コンテンツの一部です。</span><span class="sxs-lookup"><span data-stu-id="e72a3-333">Instead, the child Tab components are part of the child content of the Tab Set.</span></span> <span data-ttu-id="e72a3-334">ただし、タブの設定も知る必要がある タブの各コンポーネント、ヘッダーとアクティブなタブを表示するためです。コードを追加するコンポーネント タブの設定を必要とせずにこの調整を有効にする*自体をカスケード型の値として入力できます*し、取得される子孫タブ コンポーネント。</span><span class="sxs-lookup"><span data-stu-id="e72a3-334">However, the Tab Set still needs to know about each Tab component so that it can render the headers and the active tab. To enable this coordination without requiring additional code, the Tab Set component *can provide itself as a cascading value* that is then picked up by the descendent Tab components.</span></span>

<span data-ttu-id="e72a3-335">*Components/TabSet.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-335">*Components/TabSet.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/TabSet.cshtml)]

<span data-ttu-id="e72a3-336">子孫のタブのコンポーネントのキャプチャ、カスケード型パラメーターとして含むのタブの設定 タブのコンポーネントが、タブのセットと座標に自分自身を追加、どの タブではアクティブです。</span><span class="sxs-lookup"><span data-stu-id="e72a3-336">The descendent Tab components capture the containing Tab Set as a cascading parameter, so the Tab components add themselves to the Tab Set and coordinate on which tab is active.</span></span>

<span data-ttu-id="e72a3-337">*Components/Tab.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-337">*Components/Tab.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/Tab.cshtml)]

## <a name="razor-templates"></a><span data-ttu-id="e72a3-338">Razor テンプレート</span><span class="sxs-lookup"><span data-stu-id="e72a3-338">Razor templates</span></span>

<span data-ttu-id="e72a3-339">レンダリングのフラグメントは、Razor テンプレートの構文を使用して定義できます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-339">Render fragments can be defined using Razor template syntax.</span></span> <span data-ttu-id="e72a3-340">Razor テンプレートでは、UI のスニペットを定義し、次の形式を想定する方法です。</span><span class="sxs-lookup"><span data-stu-id="e72a3-340">Razor templates are a way to define a UI snippet and assume the following format:</span></span>

```cshtml
@<tag>...</tag>
```

<span data-ttu-id="e72a3-341">次の例は、指定する方法を示しています。`RenderFragment`と`RenderFragment<T>`値。</span><span class="sxs-lookup"><span data-stu-id="e72a3-341">The following example illustrates how to specify `RenderFragment` and `RenderFragment<T>` values.</span></span>

<span data-ttu-id="e72a3-342">*RazorTemplates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e72a3-342">*RazorTemplates.cshtml*:</span></span>

```cshtml
@{
    RenderFragment template = @<p>The time is @DateTime.Now.</p>;
    RenderFragment<Pet> petTemplate = (pet) => @<p>Your pet's name is @pet.Name.</p>;
}
```

<span data-ttu-id="e72a3-343">Razor テンプレート化されたコンポーネントに引数として渡されるまたは直接レンダリングできるテンプレートを使用して定義されたフラグメントをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="e72a3-343">Render fragments defined using Razor templates can be passed as arguments to templated components or rendered directly.</span></span> <span data-ttu-id="e72a3-344">たとえば、以前のテンプレートは次の Razor マークアップで直接レンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="e72a3-344">For example, the previous templates are directly rendered with the following Razor markup:</span></span>

```cshtml
@template

@petTemplate(new Pet { Name = "Rex" })
```

<span data-ttu-id="e72a3-345">表示される出力:</span><span class="sxs-lookup"><span data-stu-id="e72a3-345">Rendered output:</span></span>

```
The time is 10/04/2018 01:26:52.

Your pet's name is Rex.
```

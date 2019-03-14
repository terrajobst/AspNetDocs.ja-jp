---
title: Razor の JavaScript のコンポーネントの相互運用
author: guardrex
description: .NET および .NET から JavaScript 関数を呼び出す方法について説明します Blazor と剃刀コンポーネントのアプリの JavaScript からのメソッド。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/javascript-interop
ms.openlocfilehash: 9f822fee8990b03ff15ffa9857a2ddd95328a6ce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050369"
---
# <a name="razor-components-javascript-interop"></a>Razor の JavaScript のコンポーネントの相互運用

によって[Javier Calvarro Nelson](https://github.com/javiercn)、 [Daniel Roth](https://github.com/danroth27)、および[Luke Latham](https://github.com/guardrex)

Razor のコンポーネント アプリが .NET および .NET から JavaScript 関数を呼び出すことができますの JavaScript コードからメソッド。

## <a name="invoke-javascript-functions-from-net-methods"></a>.NET のメソッドからの JavaScript 関数を呼び出す

.NET コードが JavaScript 関数を呼び出すために必要な場合もあります。 たとえば、JavaScript の呼び出しでは、ブラウザーの機能または JavaScript ライブラリから、アプリの機能を公開できます。

.NET から JavaScript を呼び出すを使用して、`IJSRuntime`抽象化します。 `InvokeAsync<T>`メソッド`IJSRuntime`と任意の JSON シリアル化可能な引数の数を起動する JavaScript 関数の識別子を受け取る。 関数識別子は、グローバル スコープの相対的な (`window`)。 呼び出す場合`window.someScope.someFunction`、識別子は`someScope.someFunction`します。 これを呼び出す前に、関数を登録する必要はありません。 戻り値の型`T`も JSON シリアル化できなければなりません。

サーバー側の ASP.NET Core の Razor コンポーネント向け。

* 複数のユーザー要求は、サーバー側のアプリによって処理されます。 呼び出さない`JSRuntime.Current`で JavaScript 関数を呼び出すためのコンポーネント。
* 挿入、`IJSRuntime`抽象化と相互運用機能の JavaScript 呼び出しを発行するため、挿入されたオブジェクトを使用します。

次の例がに基づいて[TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder)、試験段階の JavaScript ベースのデコーダーです。 例からの JavaScript 関数を呼び出す方法を示します、C#メソッド。 JavaScript 関数はからのバイト配列を受け取り、C#メソッドは、配列をデコードし、コンポーネントの表示にテキストを返します。

内で、`<head>`要素の*wwwroot/index.html*を使用する関数を提供`TextDecoder`渡された配列をデコードします。

```html
<script>
  window.ConvertArray = (win1251Array) => {
    var win1251decoder = new TextDecoder('windows-1251');
    var bytes = new Uint8Array(win1251Array);
    var decodedArray = win1251decoder.decode(bytes);
    console.log(decodedArray);
    return decodedArray;
  };
</script>
```

スクリプト ファイルへの参照での JavaScript ファイルで、前の例に示すコードなどの JavaScript コードを読み込むことも、 *wwwroot/index.html*ファイル。

次のコンポーネント:

* 呼び出す、 `ConvertArray` JavaScript 関数を使用して`JsRuntime`コンポーネント ボタン (**変換配列**) が選択されています。
* JavaScript 関数が呼び出されると、渡された配列を文字列に変換されます。 表示コンポーネントに、文字列が返されます。

```cshtml
@page "/"
@using Microsoft.JSInterop;
@inject IJSRuntime JsRuntime;

<h1>Call JavaScript Function Example</h1>

<button type="button" class="btn btn-primary" onclick="@ConvertArray">
    Convert Array
</button>

<p class="mt-2" style="font-size:1.6em">
    <span class="badge badge-success">
        @ConvertedText
    </span>
</p>

@functions {
    // Quote (c)2005 Universal Pictures: Serenity
    // https://www.uphe.com/movies/serenity
    // David Krumholtz on IMDB: https://www.imdb.com/name/nm0472710/

    private MarkupString ConvertedText =
        new MarkupString("Select the <b>Convert Array</b> button.");

    private uint[] QuoteArray = new uint[]
        {
            60, 101, 109, 62, 67, 97, 110, 39, 116, 32, 115, 116, 111, 112, 32,
            116, 104, 101, 32, 115, 105, 103, 110, 97, 108, 44, 32, 77, 97,
            108, 46, 60, 47, 101, 109, 62, 32, 45, 32, 77, 114, 46, 32, 85, 110,
            105, 118, 101, 114, 115, 101, 10, 10,
        };

    async void ConvertArray()
    {
        var text =
            await JsRuntime.InvokeAsync<string>("ConvertArray", QuoteArray);

        ConvertedText = new MarkupString(text);

        StateHasChanged();
    }
}
```

クライアント側 Blazor アプリの場合、`IJSRuntime`抽象化はからアクセスできる`JSRuntime.Current`、これは現在のユーザーの要求を指します。 使用してクライアント側の Blazor アプリの 1 人のユーザーのみがあるため、`JSRuntime.Current`関数が正常に動作を JavaScript を呼び出します。 のみを使用して、 `JSRuntime.Current` Blazor アプリのクライアント側でします。

このトピックに付属しているクライアント側のサンプル アプリでは、2 つの JavaScript 関数をユーザー入力を受信して、ようこそメッセージを表示する DOM と対話するクライアント側のアプリを使用できます。

* `showPrompt` &ndash; ユーザー入力 (ユーザーの名前) に同意を求めるメッセージを生成し、呼び出し元に名前を返します。
* `displayWelcome` &ndash; ようこそメッセージを呼び出し元からの DOM オブジェクトに割り当てて、`id`の`welcome`します。

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=2-7)]

場所、`<script>`タグで JavaScript ファイルを参照する、 *wwwroot/index.html*ファイル。

[!code-html[](./common/samples/3.x/BlazorSample/wwwroot/index.html?highlight=16)]

スクリプト タグを動的に更新できないために、コンポーネントのファイルにスクリプト タグを置かないでください。

.NET メソッドを呼び出して、JavaScript 関数での相互運用機能`InvokeAsync<T>`メソッド`IJSRuntime`します。

サンプル アプリで使用する 1 組のC#メソッド、`Prompt`と`Display`を呼び出す、`showPrompt`と`displayWelcome`JavaScript 関数。

*JsInteropClasses/ExampleJsInterop.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=6-8,14-16)]

`IJSRuntime`抽象化はサーバー側のシナリオ用に非同期です。 クライアント側でアプリを実行して、同期的に、JavaScript 関数を呼び出す場合にダウン キャスト`IJSInProcessRuntime`を呼び出すと`Invoke<T>`代わりにします。 ほとんどの JavaScript ライブラリを相互運用機能の使用、async ライブラリを確認するための Api がすべてのシナリオ、クライアント側またはサーバー側で使用できることをお勧めします。

サンプル アプリには、JS 相互運用機能を示すために、コンポーネントが含まれています。 コンポーネント:

* JS プロンプトを使用してユーザー入力を受け取ります。
* コンポーネントの処理にテキストを返します。
* ようこそメッセージを表示する DOM とやり取りする 2 つ目の JS 関数を呼び出します。

*Pages/JSInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=1&end=21&highlight=2-3,9-11,13,16-20)]

1. ときに`TriggerJsPrompt`ことで、コンポーネントの実行は**トリガー JavaScript プロンプト** ボタン、`ExampleJsInterop.Prompt`メソッドC#コードが呼び出されます。
1. `Prompt`メソッドの実行、JavaScript`showPrompt`で提供される関数、 *wwwroot/exampleJsInterop.js*ファイル。
1. `showPrompt`関数は、HTML でエンコードされに返されるは、ユーザー入力 (ユーザーの名前) を受け入れる、`Prompt`メソッドし、最終的には、コンポーネントをバックアップします。 コンポーネントがローカル変数では、ユーザーの名前を格納`name`します。
1. 格納されている文字列`name`は 1 秒あたりに渡される、ようこそメッセージに組み込まれますC#メソッド、`ExampleJsInterop.Display`します。
1. `Display` JavaScript 関数を呼び出して`displayWelcome`、ようこそメッセージに見出しタグをレンダリングします。

## <a name="capture-references-to-elements"></a>要素への参照をキャプチャします。

いくつか[JavaScript の相互運用機能](xref:razor-components/javascript-interop)シナリオには、HTML 要素への参照が必要があります。 たとえば、UI ライブラリでは、初期化の要素の参照がありますまたはなど、要素をコマンドのような Api を呼び出す必要があります`focus`または`play`します。

追加することで、コンポーネントでの HTML 要素への参照をキャプチャすることができます、 `ref` HTML 要素に属性し、型のフィールドを定義し、`ElementRef`名前の値に一致する、`ref`属性。

次の例では、ユーザー名の入力要素への参照をキャプチャは示しています。

```csharp
<input ref="username" ... />

@functions {
    ElementRef username;
}
```

> [!NOTE]
> **いない**DOM を読み込む方法としてキャプチャされた要素の参照を使用 そうは、宣言型のレンダリング モデルに干渉する可能性があります。

.NET コードに関する限り、`ElementRef`は、不透明なハンドルです。 *のみ*して実行できる方法は、JavaScript の相互運用機能を介しての JavaScript コードに渡すことで。 これを行うときに、JavaScript 側コードを受け取る、`HTMLElement`インスタンスで、通常の DOM Api を使用できます。

たとえば、次のコードでは、要素にフォーカスを設定できるようにする .NET 拡張機能メソッドを定義します。

*mylib.js*:

```javascript
window.myLib = {
  focusElement : function (element) {
    element.focus();
  }
}
```

*ElementRefExtensions.cs*:

```csharp
using Microsoft.AspNetCore.Blazor;
using Microsoft.JSInterop;
using System.Threading.Tasks;

namespace MyLib
{
    public static class MyLibElementRefExtensions
    {
        public static Task Focus(this ElementRef elementRef)
        {
            return JSRuntime.Current.InvokeAsync<object>("myLib.focusElement", elementRef);
        }
    }
}
```

これで、コンポーネントのいずれかで入力を集中できます。

```cshtml
@using MyLib

<input ref="username" />
<button onclick="@SetFocus">Set focus</button>

@functions {
    ElementRef username;

    void SetFocus()
    {
        username.Focus();
    }
}
```

> [!IMPORTANT]
> `username`コンポーネントをレンダリングし、その出力に含まれる後にのみ変数が設定されます、`<input>`要素。 値を渡そうとすると場合`ElementRef`、JavaScript コードを JavaScript コードを受け取る`null`します。 コンポーネントでの表示 (要素で初期フォーカスを設定する) の使用が終了した後、要素の参照を操作する、`OnAfterRenderAsync`または`OnAfterRender`[コンポーネントのライフ サイクル メソッド](xref:razor-components/components#lifecycle-methods)します。

## <a name="invoke-net-methods-from-javascript-functions"></a>JavaScript 関数からの .NET メソッドを呼び出し

### <a name="static-net-method-call"></a>.NET の静的メソッド呼び出し

JavaScript から静的 .NET メソッドを呼び出すを使用して、`DotNet.invokeMethod`または`DotNet.invokeMethodAsync`関数。 静的メソッドを呼び出すには、関数、および任意の引数を含むアセンブリの名前の識別子を渡します。 ここでも、非同期バージョンでは、サーバー側のシナリオをサポートするために優先されます。 パブリック (静的) とで装飾するには JavaScript から呼び出し可能な .NET メソッドがあります`[JSInvokable]`します。 既定では、メソッドの識別子には、メソッド名を使用して、別の識別子を指定することができます、`JSInvokableAttribute`コンス トラクター。 オープン ジェネリック メソッドを呼び出すことは現在サポートされていません。

サンプル アプリでは、C#の配列を返すメソッドを`int`秒。 メソッドがで修飾された、`JSInvokable`属性。

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=47&end=58&highlight=7-11)]

クライアントに提供する JavaScript を呼び出す、 C# .NET メソッド。

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=8-12)]

ときに、**トリガー .NET 静的メソッド ReturnArrayAsync**ボタンが選択されている場合、ブラウザーの web 開発ツールでコンソール出力を確認します。

```console
Array(4) [ 1, 2, 3, 4 ]
```

4 番目の配列の値が配列にプッシュされます (`data.push(4);`) によって返される`ReturnArrayAsync`します。

### <a name="instance-method-call"></a>インスタンス メソッドの呼び出し

JavaScript から .NET インスタンス メソッドを呼び出すこともできます。 JavaScript から .NET インスタンス メソッドを呼び出すには、まず、.NET インスタンスに渡す JavaScript でラップして、`DotNetObjectRef`インスタンス。 .NET のインスタンスが、JavaScript への参照によって渡され、.NET のインスタンスを使用して、インスタンス メソッドを呼び出すことができます、`invokeMethod`または`invokeMethodAsync`関数。 JavaScript からその他の .NET メソッドを呼び出すときに、.NET インスタンスを引数として渡すもできます。

> [!NOTE]
> サンプル アプリでは、クライアント側のコンソールにメッセージを記録します。 サンプル アプリで示されている次の例では、ブラウザーの開発者ツールで、ブラウザーのコンソール出力を調べてください。

ときに、**トリガー .NET インスタンス メソッド HelloHelper.SayHello**ボタンを選択すると、`ExampleJsInterop.CallHelloHelperSayHello`と呼びます。 名前を渡します`Blazor`、メソッドにします。

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=60&end=69&highlight=8)]

`CallHelloHelperSayHello` JavaScript 関数を呼び出す`sayHello`の新しいインスタンスを使って`HelloHelper`します。

*JsInteropClasses/ExampleJsInterop.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=19-25)]

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=15-17)]

名前が渡される`HelloHelper`のコンス トラクターは、設定、`HelloHelper.Name`プロパティ。 ときに、JavaScript 関数`sayHello`が実行される`HelloHelper.SayHello`を返します、`Hello, {Name}!`メッセージで、JavaScript 関数で、コンソールに書き込まれます。

*JsInteropClasses/HelloHelper.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/HelloHelper.cs?name=snippet1&highlight=5,10-11)]

コンソールがブラウザーの web 開発者ツールで出力する場合:

```console
Hello, Blazor!
```

## <a name="share-interop-code-in-a-razor-component-class-library"></a>Razor のコンポーネントのクラス ライブラリでの相互運用機能のコードを共有します。

相互運用機能の JavaScript コードは Razor コンポーネントのクラス ライブラリに含めることができます (`dotnet new blazorlib`)、NuGet パッケージのコードを共有できます。

Razor のコンポーネントのクラス ライブラリでは、ビルドされたアセンブリに埋め込みの JavaScript リソースを処理します。 JavaScript ファイルに配置されます、 *wwwroot*ライブラリのビルド時に、リソースの埋め込みのフォルダー、およびツールを行います。

組み込みの NuGet パッケージは、通常、NuGet パッケージが参照されていると同様に、アプリのプロジェクト ファイルで参照されます。 場合と、アプリのコードを JavaScript を呼び出すことが、アプリを復元した後C#します。

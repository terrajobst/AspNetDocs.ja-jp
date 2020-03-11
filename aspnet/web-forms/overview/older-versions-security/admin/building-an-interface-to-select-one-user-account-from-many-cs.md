---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-cs
title: 多くの (C#) から1つのユーザーアカウントを選択するインターフェイスを構築するMicrosoft Docs
author: rick-anderson
description: このチュートリアルでは、ページ分割されたフィルター可能なグリッドを使用してユーザーインターフェイスを作成します。 特に、ユーザーインターフェイスは、一連のリンクボタンで構成されています。
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 9e4e687c-b4ec-434f-a4ef-edb0b8f365e4
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-cs
msc.type: authoredcontent
ms.openlocfilehash: 8057cfbcd33c74376076363bc27940cebd522c08
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522028"
---
# <a name="building-an-interface-to-select-one-user-account-from-many-c"></a>多くの中からユーザー アカウントを 1 つ選択するインターフェイスを構築する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.12.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_cs.pdf)

> このチュートリアルでは、ページ分割されたフィルター可能なグリッドを使用してユーザーインターフェイスを作成します。 特に、ユーザーインターフェイスは、ユーザー名の開始文字に基づいて結果をフィルター処理するための一連のリンクボタンと、一致するユーザーを表示する GridView コントロールで構成されています。 まず、GridView のすべてのユーザーアカウントを一覧表示します。 次に、手順3では、[LinkButtons] フィルターを追加します。 手順 4. では、フィルター処理された結果がページングされます。 手順 2. ~ 4. で作成したインターフェイスは、その後のチュートリアルで特定のユーザーアカウントの管理タスクを実行するために使用されます。

## <a name="introduction"></a>はじめに

<a id="_msoanchor_1"> </a>[*ユーザーへのロールの割り当て*](../roles/assigning-roles-to-users-cs.md)に関するチュートリアルでは、管理者がユーザーを選択してロールを管理するための基本的なインターフェイスを作成しました。 具体的には、インターフェイスは、すべてのユーザーのドロップダウンリストを管理者に提示します。 このようなインターフェイスは、ユーザーアカウントが1つしかない場合に適していますが、数百または数千のアカウントを持つサイトでは扱いにくいものです。 ページ分割されたフィルター可能なグリッドは、大規模なユーザーベースを持つ web サイトに適したユーザーインターフェイスです。

このチュートリアルでは、このようなユーザーインターフェイスを作成します。 特に、ユーザーインターフェイスは、ユーザー名の開始文字に基づいて結果をフィルター処理するための一連のリンクボタンと、一致するユーザーを表示する GridView コントロールで構成されています。 まず、GridView のすべてのユーザーアカウントを一覧表示します。 次に、手順3では、[LinkButtons] フィルターを追加します。 手順 4. では、フィルター処理された結果がページングされます。 手順 2. ~ 4. で作成したインターフェイスは、その後のチュートリアルで特定のユーザーアカウントの管理タスクを実行するために使用されます。

作業開始

## <a name="step-1-adding-new-aspnet-pages"></a>手順 1: 新しい ASP.NET ページを追加する

このチュートリアルと次の2つでは、管理に関連するさまざまな機能について説明します。 これらのチュートリアル全体で検討したトピックを実装するには、一連の ASP.NET ページが必要です。 これらのページを作成し、サイトマップを更新してみましょう。

まず、`Administration`という名前のプロジェクトに新しいフォルダーを作成します。 次に、2つの新しい ASP.NET ページをフォルダーに追加し、各ページを `Site.master` マスターページとリンクします。 ページに名前を指定します。

- `ManageUsers.aspx`
- `UserInformation.aspx`

また、web サイトのルートディレクトリに2つのページを追加します。 `ChangePassword.aspx` と `RecoverPassword.aspx`です。

この4つのページには、この時点で2つのコンテンツコントロールが含まれている必要があります。1つは、`MainContent` と `LoginContent`の各マスターページの ContentPlaceHolders です。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample1.aspx)]

これらのページの `LoginContent` ContentPlaceHolder のマスターページの既定のマークアップを表示します。 そのため、`Content2` コンテンツコントロールの宣言型マークアップを削除します。 その後、ページのマークアップにはコンテンツコントロールを1つだけ含める必要があります。

`Administration` フォルダー内の ASP.NET ページは、管理ユーザー専用です。 <a id="_msoanchor_2"> </a>[*ロールの作成と管理*](../roles/creating-and-managing-roles-cs.md)に関するチュートリアルで、システムに管理者ロールを追加しました。このロールに対して、これら2つのページへのアクセスを制限します。 これを行うには、`Administration` フォルダーに `Web.config` ファイルを追加し、管理者ロールのユーザーを許可し、他のユーザーを拒否するように `<authorization>` 要素を構成します。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample2.xml)]

この時点で、プロジェクトのソリューションエクスプローラーは、図1に示すスクリーンショットのようになります。

[![4 つの新しいページと web.config ファイルが web サイトに追加されました。](building-an-interface-to-select-one-user-account-from-many-cs/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image1.png)

**図 1**: 4 つの新しいページと `Web.config` ファイルが web サイトに追加された ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-cs/_static/image3.png)されます)

最後に、[`ManageUsers.aspx`] ページにエントリを含めるようにサイトマップ (`Web.sitemap`) を更新します。 ロールのチュートリアル用に追加した `<siteMapNode>` の後に、次の XML を追加します。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample3.xml)]

サイトマップが更新されたら、ブラウザーを使用してサイトにアクセスします。 図2に示すように、左側のナビゲーションには管理チュートリアルの項目が含まれるようになりました。

[サイトマップに、ユーザーの管理者という名前のノードが含まれている ![](building-an-interface-to-select-one-user-account-from-many-cs/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image4.png)

**図 2**: サイトマップに、[ユーザーの管理] という名前のノードが含まれている ([クリックしてフルサイズの画像を表示する](building-an-interface-to-select-one-user-account-from-many-cs/_static/image6.png))

## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>手順 2: GridView 内のすべてのユーザーアカウントを一覧表示する

このチュートリアルの最終的な目的は、管理者が管理対象のユーザーアカウントを選択できる、ページングされたフィルター処理されたグリッドを作成することです。 まず、GridView の*すべて*のユーザーを一覧表示しましょう。 この操作が完了したら、フィルター処理とページングのインターフェイスと機能を追加します。

`Administration` フォルダーの [`ManageUsers.aspx`] ページを開き、GridView を追加して、`ID` を `UserAccounts`に設定します。 現時点では、`Membership` クラスの `GetAllUsers` メソッドを使用して、ユーザーアカウントのセットを GridView にバインドするコードを記述します。 前のチュートリアルで説明したように、GetAllUsers メソッドは、`MembershipUser` オブジェクトのコレクションである `MembershipUserCollection` オブジェクトを返します。 コレクション内の各 `MembershipUser` には、`UserName`、`Email`、`IsApproved`などのプロパティが含まれます。

GridView で目的のユーザーアカウント情報を表示するには、GridView の `AutoGenerateColumns` プロパティを False に設定し、`IsApproved`、`IsLockedOut`、および `IsOnline` の各プロパティに対して `UserName`、`Email`、および `Comment` のプロパティと CheckBoxFields の連結フィールドを追加します。 この構成は、コントロールの宣言型マークアップまたは [フィールド] ダイアログボックスを使用して適用できます。 図3は、[フィールドの自動生成] チェックボックスがオフになっていて、BoundFields と CheckBoxFields が追加および構成された後の [フィールド] ダイアログボックスのスクリーンショットを示しています。

[![3 つの BoundFields と3つの CheckBoxFields を GridView に追加します。](building-an-interface-to-select-one-user-account-from-many-cs/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image7.png)

**図 3**: 3 つの boundfields と3つの CheckBoxFields を GridView に追加[する (クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-cs/_static/image9.png)されます)

GridView を構成した後、その宣言型マークアップが次のようになっていることを確認します。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample4.aspx)]

次に、ユーザーアカウントを GridView にバインドするコードを記述する必要があります。 このタスクを実行する `BindUserAccounts` という名前のメソッドを作成し、最初のページにアクセスしたときに `Page_Load` イベントハンドラーから呼び出します。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample5.cs)]

ブラウザーでページをテストしてみましょう。 図4に示すように、`UserAccounts` GridView は、システム内のすべてのユーザーのユーザー名、電子メールアドレス、およびその他の関連するアカウント情報を一覧表示します。

[GridView にユーザーアカウントが表示される ![](building-an-interface-to-select-one-user-account-from-many-cs/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image10.png)

**図 4**: GridView にユーザーアカウントが表示される ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-cs/_static/image12.png)されます)

## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>手順 3: ユーザー名の最初の文字で結果をフィルター処理する

現在 `UserAccounts` GridView には、*すべて*のユーザーアカウントが表示されます。 数百または数千のユーザーアカウントを持つ web サイトでは、表示されているアカウントをユーザーがすばやく省いできるようにすることが重要です。 これは、ページにフィルターリンクボタンを追加することによって実現できます。 ページに 27 LinkButtons を追加してみましょう。1つはアルファベットの各文字につき1つの LinkButton です。 ビジターが All LinkButton をクリックすると、GridView にすべてのユーザーが表示されます。 ユーザーが特定の文字をクリックすると、ユーザー名が選択した文字で始まるユーザーのみが表示されます。

最初のタスクでは、27 LinkButton コントロールを追加します。 1つの方法として、27リンクボタンを宣言によって一度に1つ作成する方法があります。 より柔軟な方法は、LinkButton をレンダリングする `ItemTemplate` で Repeater コントロールを使用し、その後、フィルターオプションを `string` 配列としてリピータにバインドすることです。

まず、`UserAccounts` GridView の上のページに Repeater コントロールを追加します。 リピータの `ID` プロパティを `FilteringUI`に設定します。 リピータのテンプレートを構成して、`Text` と `CommandName` プロパティが現在の配列要素にバインドされている LinkButton を `ItemTemplate` にレンダリングするようにします。 <a id="_msoanchor_3"> </a>[*ユーザーへのロールの割り当て*](../roles/assigning-roles-to-users-cs.md)に関するチュートリアルで説明したように、これは `Container.DataItem` databinding 構文を使用して実現できます。 リピータの `SeparatorTemplate` を使用して、各リンクの間に垂直線を表示します。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample6.aspx)]

このリピータに必要なフィルター処理オプションを設定するには、`BindFilteringUI`という名前のメソッドを作成します。 最初のページの読み込み時に、`Page_Load` イベントハンドラーからこのメソッドを呼び出すようにしてください。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample7.cs)]

このメソッドは、`string` 配列 `filterOptions`の要素としてフィルター処理オプションを指定します。 リピータは、配列内の要素ごとに、`Text` を持つ LinkButton と、配列要素の値に割り当てられた `CommandName` プロパティを表示します。

図5は、ブラウザーを使用して表示するときの `ManageUsers.aspx` ページを示しています。

[リピータ ![リンクボタンの一覧27](building-an-interface-to-select-one-user-account-from-many-cs/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image13.png)

**図 5**: リピータは、27フィルターリンクボタンを一覧表示しています ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-cs/_static/image15.png)されます)

> [!NOTE]
> ユーザー名は、数字や句読点を含む任意の文字で始めることができます。 これらのアカウントを表示するために、管理者は All LinkButton オプションを使用する必要があります。 または、LinkButton を追加して、番号で始まるすべてのユーザーアカウントを返すこともできます。 この作業をリーダーの演習として残しておきます。

フィルターリンクボタンのいずれかをクリックすると、ポストバックが発生し、リピータの `ItemCommand` イベントが発生しますが、結果をフィルター処理するコードをまだ記述していないため、グリッドは変わりません。 `Membership` クラスには、ユーザー名が指定した検索パターンに一致するユーザーアカウントを返す[`FindUsersByName` メソッド](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx)が含まれています。 このメソッドを使用すると、ユーザー名が、クリックされたフィルター選択された LinkButton の `CommandName` で指定された文字で始まるユーザーアカウントだけを取得できます。

まず、`UsernameToMatch`という名前のプロパティが含まれるように、`ManageUser.aspx` ページの分離コードクラスを更新します。 このプロパティは、ポストバック間でユーザー名フィルター文字列を永続化します。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample8.cs)]

`UsernameToMatch` プロパティは、キー UsernameToMatch を使用して、`ViewState` コレクションに割り当てられている値を格納します。 このプロパティの値が読み込まれると、`ViewState` コレクションに値が存在するかどうかが確認されます。そうでない場合は、既定値である空の文字列が返されます。 `UsernameToMatch` プロパティは、共通のパターンを示しています。つまり、プロパティに対する変更がポストバック間で保持されるように、状態を表示するための値を保持します。 このパターンの詳細については、「 [ASP.NET ビューステート](https://msdn.microsoft.com/library/ms972976.aspx)について」を参照してください。

次に、`BindUserAccounts` メソッドを更新して、`Membership.GetAllUsers`を呼び出すのではなく、`Membership.FindUsersByName`を呼び出し、SQL のワイルドカード文字% で追加された `UsernameToMatch` プロパティの値を渡します。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample9.cs)]

ユーザー名が A で始まるユーザーだけを表示するには、`UsernameToMatch` プロパティをに設定し、`BindUserAccounts`を呼び出します。 この場合、`Membership.FindUsersByName("A%")`が呼び出されます。これにより、ユーザー名がで始まるすべてのユーザーが返されます。同様に、*すべて*のユーザーを返すには、`UsernameToMatch` プロパティに空の文字列を割り当てて、`BindUserAccounts` メソッドが `Membership.FindUsersByName("%")`を呼び出し、その結果、すべてのユーザーアカウントを返すようにします。

リピータの `ItemCommand` イベントのイベントハンドラーを作成します。 このイベントは、フィルターリンクボタンの1つがクリックされたときに発生します。クリックされた LinkButton の `CommandName` 値が `RepeaterCommandEventArgs` オブジェクトを介して渡されます。 `UsernameToMatch` プロパティに適切な値を割り当て、`BindUserAccounts` メソッドを呼び出す必要があります。 `CommandName` が All の場合は、すべてのユーザーアカウントが表示されるように、`UsernameToMatch` に空の文字列を割り当てます。 それ以外の場合は、`CommandName` 値を `UsernameToMatch`に割り当てます。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample10.cs)]

このコードを使用して、フィルター処理機能をテストします。 ページに最初にアクセスしたときに、すべてのユーザーアカウントが表示されます (図5を参照)。 A LinkButton をクリックすると、ポストバックが発生し、結果がフィルター処理されて、で始まるユーザーアカウントのみが表示されます。

[[フィルターリンク] ボタンを使用して、ユーザー名が特定の文字で始まるユーザーを表示 ![](building-an-interface-to-select-one-user-account-from-many-cs/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image16.png)

**図 6**: [フィルターリンク] ボタンを使用して、ユーザー名が特定の文字で始まるユーザーを表示する ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-cs/_static/image18.png)されます)

## <a name="step-4-updating-the-gridview-to-use-paging"></a>手順 4: ページングを使用するように GridView を更新する

図5および6に示されている GridView は、`FindUsersByName` メソッドから返されるすべてのレコードを一覧表示します。 数百または数千のユーザーアカウントがある場合は、すべてのアカウントを表示すると情報が過負荷になる可能性があります (すべての LinkButton をクリックした場合や、最初にページにアクセスしたときに発生した場合のように)。 より管理しやすいチャンクでユーザーアカウントを表示するには、一度に10個のユーザーアカウントを表示するように GridView を構成してみましょう。

GridView コントロールでは、次の2種類のページングが提供されます。

- **既定のページング**-実装は簡単ですが、非効率的です。 簡単に言うと、既定のページングでは、GridView はデータソースの*すべて*のレコードを想定しています。 次に、適切なレコードのページのみが表示されます。
- **カスタムページング**-実装にはより多くの作業が必要ですが、既定のページングよりも効率的です。これは、カスタムページングでは、表示するレコードの正確なセットのみを返すためです。

既定のページングとカスタムページングのパフォーマンスの違いは、何千ものレコードをページングする場合に非常に大きくなる可能性があります。 このインターフェイスは、数百または数千のユーザーアカウントがあると仮定して構築されているため、カスタムページングを使用します。

> [!NOTE]
> 既定のページングとカスタムページングの違い、およびカスタムページングの実装に関連する課題の詳細については、「[大量のデータを効率的にページング](https://asp.net/learn/data-access/tutorial-25-cs.aspx)する」を参照してください。 既定のページングとカスタムページングのパフォーマンスの違いの分析については、「 [SQL Server 2005 を使用した ASP.NET のカスタムページング](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)」を参照してください。

カスタムページングを実装するには、まず、GridView によって表示されるレコードの正確なサブセットを取得するためのメカニズムが必要です。 優れたニュースとして、`Membership` クラスの `FindUsersByName` メソッドには、ページインデックスとページサイズを指定できるオーバーロードがあり、その範囲内にあるユーザーアカウントのみが返されます。

特に、このオーバーロードには、 [`FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)`](https://msdn.microsoft.com/library/fa5st8b2.aspx)というシグネチャがあります。

*PageIndex*パラメーターは、返されるユーザーアカウントのページを指定します。*pageSize*は、1ページあたりに表示するレコードの数を示します。 *Totalrecords*パラメーターは、ユーザーストア内のユーザーアカウントの合計数を返す `out` パラメーターです。

> [!NOTE]
> `FindUsersByName` によって返されるデータはユーザー名で並べ替えられます。並べ替え条件をカスタマイズすることはできません。

GridView は、ObjectDataSource コントロールにバインドされている場合にのみ、カスタムページングを使用するように構成できます。 ObjectDataSource コントロールでカスタムページングを実装するには、開始行インデックスと表示するレコードの最大数を渡す2つの方法が必要です。また、そのスパン内に含まれるレコードの詳細なサブセットを返します。およびは、ページングされているレコードの合計数を返すメソッドです。 `FindUsersByName` のオーバーロードは、ページインデックスとページサイズを受け入れ、`out` パラメーターを使用してレコードの合計数を返します。 ここでは、インターフェイスが一致していません。

1つの方法として、ObjectDataSource が想定しているインターフェイスを公開するプロキシクラスを作成し、`FindUsersByName` メソッドを内部的に呼び出します。 この記事で使用するもう1つの方法として、独自のページングインターフェイスを作成し、GridView の組み込みページングインターフェイスではなくそれを使用する方法があります。

### <a name="creating-a-first-previous-next-last-paging-interface"></a>最初、前、次、最後のページングインターフェイスを作成する

最初、前、次のリンクボタンと最後のリンクボタンを使用して、ページングインターフェイスを作成してみましょう。 最初の LinkButton がクリックされると、ユーザーはデータの最初のページに移動しますが、Previous は前のページに戻ります。 同様に、[次へ] と [最後] では、ユーザーをそれぞれ次のページと最後のページに移動します。 `UserAccounts` GridView の下に4つの LinkButton コントロールを追加します。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample11.aspx)]

次に、LinkButton の `Click` イベントごとにイベントハンドラーを作成します。

図7は、Visual Web Developer デザインビューを通じて表示する場合の4つの LinkButtons を示しています。

[GridView の下に First、Previous、Next、および Last LinkButtons を追加 ![には](building-an-interface-to-select-one-user-account-from-many-cs/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image19.png)

**図 7**: GridView の下に First、Previous、Next、および Last linkbuttons を追加[する (クリックすると、フルサイズのイメージが表示](building-an-interface-to-select-one-user-account-from-many-cs/_static/image21.png)されます)

### <a name="keeping-track-of-the-current-page-index"></a>現在のページインデックスを追跡する

ユーザーが最初に [`ManageUsers.aspx`] ページにアクセスしたとき、またはいずれかのフィルターボタンをクリックしたときに、GridView に最初のデータページが表示されます。 ただし、ユーザーがナビゲーションリンクボタンのいずれかをクリックしたときに、ページインデックスを更新する必要があります。 ページインデックスとページごとに表示するレコード数を維持するには、次の2つのプロパティをページの分離コードクラスに追加します。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample12.cs)]

`UsernameToMatch` プロパティと同様に、`PageIndex` プロパティはその値をビューステートに永続化します。 読み取り専用の `PageSize` プロパティは、ハードコーディングされた値10を返します。 このプロパティを更新して `PageIndex`と同じパターンを使用するように、関心のある読者を招待します。次に、ページにアクセスするユーザーがページごとに表示するユーザーアカウントの数を指定できるように `ManageUsers.aspx` ページを拡張します。

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>現在のページのレコードだけを取得し、ページインデックスを更新し、ページングインターフェイスリンクボタンを有効または無効にします。

ページングインターフェイスが配置され、`PageIndex` と `PageSize` のプロパティが追加されたので、適切な `FindUsersByName` オーバーロードを使用するように `BindUserAccounts` メソッドを更新する準備ができました。 また、表示されるページに応じて、このメソッドでページングインターフェイスを有効または無効にする必要があります。 データの最初のページを表示する場合は、最初のリンクと前のリンクを無効にする必要があります。最後のページを表示する場合は、[次へ] と [最後] を無効にする必要があります。

`BindUserAccounts` メソッドを次のコードで更新します。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample13.cs)]

ページングされるレコードの合計数は、`FindUsersByName` メソッドの最後のパラメーターによって決定されることに注意してください。 これは `out` パラメーターであるため、まずこの値 (`totalRecords`) を保持する変数を宣言し、次に `out` キーワードでプレフィックスを付ける必要があります。

指定されたページのユーザーアカウントが返された後、データの最初のページまたは最後のページが表示されているかどうかに応じて、4つのリンクボタンが有効または無効になります。

最後の手順では、4つの LinkButtons `Click` イベントハンドラーのコードを記述します。 これらのイベントハンドラーは、`PageIndex` プロパティを更新し、`BindUserAccounts`の呼び出しを使用してデータを GridView に再バインドする必要があります。 1つ目、前のイベント、および次のイベントハンドラーは非常に単純です。 ただし、最後の LinkButton の `Click` イベントハンドラーは少し複雑になります。これは、最後のページインデックスを判別するために、表示されているレコードの数を確認する必要があるためです。

[!code-csharp[Main](building-an-interface-to-select-one-user-account-from-many-cs/samples/sample14.cs)]

図8と9は、カスタムページングインターフェイスが動作していることを示しています。 図8は、すべてのユーザーアカウントの最初のデータページを表示するときの `ManageUsers.aspx` ページを示しています。 表示されるのは、13個のアカウントのうち10個だけであることに注意してください。 次のリンクまたは最後のリンクをクリックすると、ポストバックが発生し、`PageIndex` が1に更新され、ユーザーアカウントの2番目のページがグリッドにバインドされます (図9を参照)。

[最初の10個のユーザーアカウントが表示される ![](building-an-interface-to-select-one-user-account-from-many-cs/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image22.png)

**図 8**: 最初の10個のユーザーアカウントが表示される ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-cs/_static/image24.png)されます)

[次のリンクをクリック ![と、ユーザーアカウントの2ページ目が表示されます。](building-an-interface-to-select-one-user-account-from-many-cs/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-cs/_static/image25.png)

**図 9**: 次のリンクをクリックすると、ユーザーアカウントの2ページ目が表示されます ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-cs/_static/image27.png)されます)

## <a name="summary"></a>まとめ

管理者は、多くの場合、アカウントの一覧からユーザーを選択する必要があります。 前のチュートリアルでは、ユーザーに設定されたドロップダウンリストの使用について説明しましたが、この方法はうまくいきません。 このチュートリアルでは、結果がページングされた GridView に表示されるフィルター可能なインターフェイスである、より優れた代替方法について説明します。 このユーザーインターフェイスを使用すると、管理者は数千単位で1つのユーザーアカウントをすばやく効率的に検索して選択できます。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [SQL Server 2005 を使用した ASP.NET のカスタムページング](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [大量のデータを効率的にページングする](https://asp.net/learn/data-access/tutorial-25-cs.aspx)
- [独自の Web サイト管理ツールのロール](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは Alicja Maziarz でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [Next](recovering-and-changing-passwords-cs.md)

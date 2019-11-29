---
uid: web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-cs
title: マスターページと ASP.NET AJAX (C#) |Microsoft Docs
author: rick-anderson
description: ASP.NET AJAX およびマスターページを使用するためのオプションについて説明します。 ScriptManagerProxy クラスを使用していることを確認します。さまざまな JS ファイルがどのように読み込まれているかについて説明します...
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 0c55eb66-ba44-4d49-98e8-5c87fd9b1111
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-cs
msc.type: authoredcontent
ms.openlocfilehash: 8cd1d57b4d2aa01654da53ab2b1cc01f71ad8a87
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639650"
---
# <a name="master-pages-and-aspnet-ajax-c"></a>マスター ページと ASP.NET AJAX (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_08_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_08_CS.pdf)

> ASP.NET AJAX およびマスターページを使用するためのオプションについて説明します。 ScriptManagerProxy クラスを使用していることを確認します。ScriptManager がマスターページとコンテンツページのどちらで使用されているかに応じて、さまざまな JS ファイルがどのように読み込まれるかについて説明します。

## <a name="introduction"></a>はじめに

これまで数年で、 [AJAX](http://en.wikipedia.org/wiki/Ajax_(programming))対応の web アプリケーションを構築している開発者が増えています。 AJAX 対応の web サイトでは、関連するさまざまな web テクノロジを使用して、より応答性の高いユーザーエクスペリエンスを提供します。 AJAX 対応の ASP.NET アプリケーションの作成は、Microsoft の[ASP.NET AJAX フレームワーク](../../../../ajax/index.md)を使用すると驚くほど簡単です。 ASP.NET AJAX は ASP.NET 3.5 と Visual Studio 2008 に組み込まれています。また、ASP.NET 2.0 アプリケーションの個別のダウンロードとして入手することもできます。

AJAX 対応の web ページを ASP.NET AJAX フレームワークでビルドする場合は、フレームワークを使用するすべてのページに、 [ScriptManager コントロール](https://msdn.microsoft.com/library/bb398863.aspx)を正確に1つずつ追加する必要があります。 その名前が示すように、ScriptManager は、AJAX 対応 web ページで使用されるクライアント側スクリプトを管理します。 ScriptManager は、少なくとも、ASP.NET AJAX クライアントライブラリを含む JavaScript ファイルをダウンロードするようにブラウザーに指示する HTML を出力します。 また、カスタム JavaScript ファイル、スクリプト対応の web サービス、およびカスタムアプリケーションサービス機能の登録にも使用できます。

サイトでマスターページを使用する場合 (必要に応じて)、ScriptManager コントロールをすべてのコンテンツページに追加する必要はありません。代わりに、ScriptManager コントロールをマスターページに追加することができます。 このチュートリアルでは、ScriptManager コントロールをマスターページに追加する方法について説明します。 また、ScriptManagerProxy コントロールを使用して、カスタムスクリプトとスクリプトサービスを特定のコンテンツページに登録する方法についても説明します。

> [!NOTE]
> このチュートリアルでは、ASP.NET AJAX フレームワークを使用した AJAX 対応の web アプリケーションの設計または構築については説明しません。 AJAX の使用方法の詳細については、 [ASP.NET ajax のビデオ](../../../videos/aspnet-ajax/index.md)と[チュートリアル](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)に関するほか、このチュートリアルの最後にある「その他の情報」セクションに記載されているリソースも参照してください。

## <a name="examining-the-markup-emitted-by-the-scriptmanager-control"></a>ScriptManager コントロールによって出力されたマークアップを調べる

ScriptManager コントロールは、ASP.NET AJAX クライアントライブラリを含む JavaScript ファイルをダウンロードするようにブラウザーに指示するマークアップを出力します。 また、このライブラリを初期化するインライン JavaScript をページに追加します。 次のマークアップは、ScriptManager コントロールを含むページのレンダリングされた出力に追加される内容を示しています。

[!code-html[Main](master-pages-and-asp-net-ajax-cs/samples/sample1.html)]

`<script src="url"></script>` タグは、 *url*で JavaScript ファイルをダウンロードして実行するようにブラウザーに指示します。 ScriptManager コントロールは、次の3つのタグを出力します。1つはファイル `WebResource.axd`を参照し、もう1つはファイル `ScriptResource.axd`を参照します。 これらのファイルは、実際には web サイト内のファイルとしては存在しません。 代わりに、これらのいずれかのファイルに対する要求が web サーバーに到着すると、ASP.NET エンジンはクエリ文字列を調べて、適切な JavaScript コンテンツを返します。 これら3つの外部 JavaScript ファイルによって提供されるスクリプトは、ASP.NET AJAX フレームワークのクライアントライブラリを構成します。 ScriptManager コントロールによって出力されるその他の `<script>` タグには、このライブラリを初期化するインラインスクリプトが含まれます。

ScriptManager によって生成される外部スクリプト参照とインラインスクリプトは、ASP.NET AJAX フレームワークを使用するページには不可欠ですが、フレームワークを使用しないページには必要ありません。 そのため、ASP.NET AJAX フレームワークを使用するページに ScriptManager を追加することだけが理想的であると考えられます。 これで十分ですが、フレームワークを使用するページが多数ある場合は、すべてのページに ScriptManager コントロールを追加する必要があります (反復的なタスク)。 または、ScriptManager をマスターページに追加して、この必要なスクリプトをすべてのコンテンツページに挿入することもできます。 この方法では、ASP.NET AJAX フレームワークを使用する新しいページに ScriptManager を追加する必要はありません。これは、既にマスターページに含まれているためです。 手順 1. では、ScriptManager をマスターページに追加します。

> [!NOTE]
> マスターページのユーザーインターフェイス内に AJAX 機能を組み込む場合は、どのような選択肢もありません。そのため、ScriptManager をマスターページに含める必要があります。

ScriptManager をマスターページに追加する場合の欠点の1つは、必要に応じて、上記のスクリプトが*すべて*のページで出力されることです。 これにより、ScriptManager が含まれているページ (マスターページ経由) では、ASP.NET AJAX フレームワークの機能を使用しなくても、帯域幅が無駄になることが明らかになります。 しかし、浪費される帯域幅はどれくらいですか。

- ScriptManager によって出力された実際のコンテンツ (上記を参照) は、1 KB を少し超えています。
- ただし、`<script>` 要素によって参照される3つの外部スクリプトファイルは、圧縮されていない約450KB のデータを構成します。gzip 圧縮を使用する web サイトでは、この合計帯域幅を 100 KB 近くに減らすことができます。 ただし、これらのスクリプトファイルはブラウザーによって1年間キャッシュされます。つまり、一度ダウンロードする必要があるだけで、サイトの他のページで再利用することができます。

最良のケースでは、スクリプトファイルがキャッシュされると、総コストは 1 KB になります。これはごくわずかです。 ただし、最悪のケースでは、スクリプトファイルがまだダウンロードされておらず、web サーバーが何らかの形式の圧縮を使用していない場合、帯域幅のヒットは約450KB になります。これにより、ブロードバンド接続を介して1秒または2秒の間で、 ダイヤルアップモデムを経由したユーザー。 これは、外部スクリプトファイルがブラウザーによってキャッシュされるため、この最悪のケースシナリオはあまり発生しないということです。

> [!NOTE]
> まだ ScriptManager コントロールがマスターページに配置されていないと思われる場合は、Web フォーム (マスターページの `<form runat="server">` マークアップ) を検討してください。 ポストバックモデルを使用するすべての ASP.NET ページには、正確に1つの Web フォームを含める必要があります。 Web フォームを追加すると、追加のコンテンツが追加されます。複数の非表示フォームフィールド、`<form>` タグ自体、および必要に応じて、スクリプトからポストバックを開始するための JavaScript 関数。 ポストバックされないページでは、このマークアップは不要です。 この余分なマークアップは、マスターページから Web フォームを削除し、必要な各コンテンツページに手動で追加することで除去できます。 ただし、マスターページに Web フォームを配置する利点は、特定のコンテンツページに不必要に追加されることによる欠点を上回ることがあります。

## <a name="step-1-adding-a-scriptmanager-control-to-the-master-page"></a>手順 1: ScriptManager コントロールをマスターページに追加する

ASP.NET AJAX フレームワークを使用するすべての web ページには、正確に1つの ScriptManager コントロールが含まれている必要があります。 この要件により、通常は、すべてのコンテンツページに ScriptManager コントロールが自動的に含まれるように、1つの ScriptManager コントロールをマスターページに配置するのが理にかなっています。 さらに、ScriptManager コントロールは、UpdatePanel や UpdateProgress などの ASP.NET AJAX サーバーコントロールの前に記述する必要があります。 そのため、ScriptManager コントロールを Web フォーム内の ContentPlaceHolder コントロールの前に配置することをお勧めします。

`Site.master` マスターページを開き、ScriptManager コントロールを Web フォーム内のページに追加します。ただし、`<div id="topContent">` 要素の前に追加します (図1を参照)。 Visual Web Developer 2008 または Visual Studio 2008 を使用している場合は、[AJAX 拡張] タブの [ツールボックス] に ScriptManager コントロールが配置されます。Visual Studio 2005 を使用している場合は、最初に ASP.NET AJAX フレームワークをインストールし、コントロールをツールボックスに追加する必要があります。 ASP.NET 2.0 のフレームワークを入手するには、 [ASP.NET AJAX Wiki](https://github.com/DevExpress/AjaxControlToolkit/wiki)にアクセスしてください。

ScriptManager コントロールをページに追加した後、その `ID` を `ScriptManager1` から `MyManager`に変更します。

[ScriptManager コントロールをマスターページに追加 ![には](master-pages-and-asp-net-ajax-cs/_static/image2.png)](master-pages-and-asp-net-ajax-cs/_static/image1.png)

**図 01**: ScriptManager をマスターページに追加する ([クリックすると、フルサイズの画像が表示](master-pages-and-asp-net-ajax-cs/_static/image3.png)されます)

## <a name="step-2-using-the-aspnet-ajax-framework-from-a-content-page"></a>手順 2: コンテンツページからの ASP.NET AJAX フレームワークの使用

マスターページに ScriptManager コントロールが追加されたので、ASP.NET AJAX フレームワークの機能を任意のコンテンツページに追加できるようになりました。 ここでは、Northwind データベースからランダムに選択された製品を表示する新しい ASP.NET ページを作成します。 ASP.NET AJAX フレームワークの Timer コントロールを使用して、15秒ごとにこの表示を更新し、新しい製品を表示します。

まず、`ShowRandomProduct.aspx`という名前のルートディレクトリに新しいページを作成します。 忘れずにこの新しいページを `Site.master` マスターページにバインドしてください。

[新しい ASP.NET ページを Web サイトに追加 ![には](master-pages-and-asp-net-ajax-cs/_static/image5.png)](master-pages-and-asp-net-ajax-cs/_static/image4.png)

**図 02**: web サイトに新しい ASP.NET ページを追加する ([クリックすると、フルサイズの画像が表示](master-pages-and-asp-net-ajax-cs/_static/image6.png)されます)

[ *「マスターページでタイトル、メタタグ、およびその他の HTML ヘッダーを指定*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)する」チュートリアルでは、明示的に設定されていない場合にページのタイトルを生成する `BasePage` という名前のカスタム基本ページクラスを作成しました。 `ShowRandomProduct.aspx` ページの分離コードクラスにアクセスし、`System.Web.UI.Page`からではなく `BasePage` から派生させます。

最後に、このレッスンのエントリを含めるように `Web.sitemap` ファイルを更新します。 [マスター to コンテンツ] ページの相互作用レッスンの `<siteMapNode>` の下に、次のマークアップを追加します。

[!code-xml[Main](master-pages-and-asp-net-ajax-cs/samples/sample2.xml)]

この `<siteMapNode>` 要素の追加は、レッスンの一覧に反映されます (図5を参照)。

### <a name="displaying-a-randomly-selected-product"></a>ランダムに選択された製品の表示

`ShowRandomProduct.aspx`に戻ります。 デザイナーから、UpdatePanel コントロールをツールボックスから `MainContent` コンテンツコントロールにドラッグし、その `ID` プロパティを `ProductPanel`に設定します。 UpdatePanel は、ページの部分ポストバックによって非同期的に更新できる画面上の領域を表します。

最初のタスクでは、UpdatePanel 内のランダムに選択された製品に関する情報を表示します。 まず、DetailsView コントロールを UpdatePanel にドラッグします。 DetailsView コントロールの `ID` プロパティを `ProductInfo` に設定し、その `Height` および `Width` プロパティをクリアします。 DetailsView のスマートタグを展開し、[データソースの選択] ドロップダウンリストから、DetailsView を `RandomProductDataSource`という名前の新しい SqlDataSource コントロールにバインドすることを選択します。

[DetailsView を新しい SqlDataSource コントロールにバインド ![には](master-pages-and-asp-net-ajax-cs/_static/image8.png)](master-pages-and-asp-net-ajax-cs/_static/image7.png)

**図 03**: DetailsView を新しい SqlDataSource コントロールにバインドする ([クリックすると、フルサイズの画像が表示](master-pages-and-asp-net-ajax-cs/_static/image9.png)されます)

`NorthwindConnectionString` を使用して Northwind データベースに接続するように SqlDataSource コントロールを構成します (これは、「[*コンテンツページからのマスターページ*](interacting-with-the-content-page-from-the-master-page-cs.md)の操作」チュートリアルで作成したものです)。 Select ステートメントを構成するときに、カスタム SQL ステートメントを指定することを選択し、次のクエリを入力します。

[!code-sql[Main](master-pages-and-asp-net-ajax-cs/samples/sample3.sql)]

`SELECT` 句の `TOP 1` キーワードは、クエリによって返された最初のレコードのみを返します。 [`NEWID()` 関数](https://msdn.microsoft.com/library/ms190348.aspx)は、新しい[グローバル一意識別子の値 (GUID)](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)を生成し、`ORDER BY` の句で使用して、テーブルのレコードをランダムな順序で返すことができます。

[ランダムに選択された単一のレコードを返すように SqlDataSource を構成 ![](master-pages-and-asp-net-ajax-cs/_static/image11.png)](master-pages-and-asp-net-ajax-cs/_static/image10.png)

**図 04**: 1 つのランダムに選択されたレコードを返すように SqlDataSource を構成する ([クリックしてフルサイズの画像を表示](master-pages-and-asp-net-ajax-cs/_static/image12.png)する)

ウィザードを完了すると、上記のクエリによって返された2つの列の BoundField が Visual Studio によって作成されます。 この時点で、ページの宣言型マークアップは次のようになります。

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample4.aspx)]

図5は、ブラウザーを使用して表示するときの `ShowRandomProduct.aspx` ページを示しています。 ブラウザーの [更新] ボタンをクリックして、ページを再読み込みします。ランダムに選択された新しいレコードの `ProductName` と `UnitPrice` の値が表示されます。

[ランダムな製品名と価格が表示され ![](master-pages-and-asp-net-ajax-cs/_static/image14.png)](master-pages-and-asp-net-ajax-cs/_static/image13.png)

**図 05**: ランダムな製品名と価格が表示される ([クリックすると、フルサイズの画像が表示](master-pages-and-asp-net-ajax-cs/_static/image15.png)されます)

### <a name="automatically-displaying-a-new-product-every-15-seconds"></a>新しい製品を15秒ごとに自動的に表示する

ASP.NET AJAX フレームワークには、指定された時間にポストバックを実行するタイマーコントロールが含まれています。ポストバック時に、タイマーの `Tick` イベントが発生します。 タイマーコントロールが UpdatePanel 内に配置されている場合は、部分ページポストバックがトリガーされます。その間、データを DetailsView に再バインドして、ランダムに選択された新しい製品を表示できます。

これを行うには、[ツールボックス] からタイマーをドラッグして、UpdatePanel にドロップします。 タイマーの `ID` を `Timer1` から `ProductTimer` に、`Interval` プロパティを6万から15000に変更します。 `Interval` プロパティは、ポストバックの間隔をミリ秒単位で示します。この値を15000に設定すると、タイマーが部分ページポストバックを15秒ごとにトリガーします。 この時点で、タイマーの宣言型マークアップは次のようになります。

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample5.aspx)]

タイマーの `Tick` イベントのイベントハンドラーを作成します。 このイベントハンドラーでは、DetailsView の `DataBind` メソッドを呼び出すことによって、データを DetailsView に再バインドする必要があります。 これにより、DetailsView は、データソースコントロールからデータを再取得するように指示します。これは、ランダムに選択された新しいレコードを選択して表示します (ブラウザーの [更新] ボタンをクリックしてページを再読み込みするときと同様です)。

[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample6.cs)]

必要な作業は以上です。 ブラウザーを使用してページを再度参照してください。 最初に、ランダムな製品情報が表示されます。 我慢強くを見ると、15秒後に、新しい製品に関する情報が既存の表示を魔法のように置き換えられることがわかります。

ここで何が起こっているかをよりよく確認するために、表示が最後に更新された時刻を表示するラベルコントロールを UpdatePanel に追加してみましょう。 UpdatePanel 内にラベル Web コントロールを追加し、その `ID` を `LastUpdateTime`に設定して、`Text` プロパティをクリアします。 次に、UpdatePanel の `Load` イベントのイベントハンドラーを作成し、ラベルに現在の時刻を表示します。 (UpdatePanel の `Load` イベントは、ページの完全ポストバックまたは部分ポストバックごとに発生します)。

[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample7.cs)]

この変更が完了すると、ページには現在表示されている製品が読み込まれた時間が含まれます。 図6に、最初にアクセスしたときのページを示します。 図7に、タイマーコントロールが "終了" した後の15秒後に、新しい製品に関する情報を表示するために UpdatePanel が更新されたことを示します。

[ランダムに選択された製品がページの読み込み時に表示される ![](master-pages-and-asp-net-ajax-cs/_static/image17.png)](master-pages-and-asp-net-ajax-cs/_static/image16.png)

**図 06**: ランダムに選択された製品がページの読み込み時に表示される ([クリックすると、フルサイズの画像が表示](master-pages-and-asp-net-ajax-cs/_static/image18.png)されます)

[ランダムに選択された新しい製品が15秒ごとに表示される ![](master-pages-and-asp-net-ajax-cs/_static/image20.png)](master-pages-and-asp-net-ajax-cs/_static/image19.png)

**図 07**: ランダムに選択された新しい製品が15秒ごとに表示される ([クリックすると、フルサイズの画像が表示](master-pages-and-asp-net-ajax-cs/_static/image21.png)されます)

## <a name="step-3-using-the-scriptmanagerproxy-control"></a>手順 3: ScriptManagerProxy コントロールの使用

ScriptManager は、ASP.NET AJAX framework クライアントライブラリに必要なスクリプトを含むと共に、カスタム JavaScript ファイル、スクリプト対応 Web サービスへの参照、およびカスタム認証、承認、およびプロファイルサービスを登録することもできます。 通常、このようなカスタマイズは特定のページに固有です。 ただし、カスタムスクリプトファイル、Web サービス参照、認証、承認、またはプロファイルサービスが、マスターページの ScriptManager サイトで参照されている場合は、web サイトの*すべて*のページに含まれます。

ScriptManager に関連するカスタマイズをページごとに追加するには、ScriptManagerProxy コントロールを使用します。 ScriptManagerProxy をコンテンツページに追加した後、カスタム JavaScript ファイル、Web サービス参照、認証、承認、またはプロファイルサービスを ScriptManagerProxy から登録できます。これにより、これらのサービスを特定のコンテンツページに登録した場合の効果があります。

> [!NOTE]
> ASP.NET ページには、ScriptManager コントロールを1つだけ含めることができます。 そのため、ScriptManager コントロールがマスターページで既に定義されている場合、ScriptManager コントロールをコンテンツページに追加することはできません。 ScriptManagerProxy の唯一の目的は、開発者がマスターページで ScriptManager を定義できるようにすることですが、ページ単位で ScriptManager カスタマイズを追加することもできます。

動作中の ScriptManagerProxy コントロールを確認するには、`ShowRandomProduct.aspx` の UpdatePanel を増やして、タイマーコントロールを一時停止または再開するクライアント側スクリプトを使用するボタンを追加します。 Timer コントロールには、この必要な機能を実現するために使用できる3つのクライアント側メソッドがあります。

- `_startTimer()`-タイマーコントロールを開始します
- `_raiseTick()`-タイマーコントロールを "tick" にします。これにより、サーバーで `Tick` イベントがポストバックされ、発生します。
- `_stopTimer()`-タイマーコントロールを停止します

`timerEnabled` という名前の変数と `ToggleTimer`という名前の関数を含む JavaScript ファイルを作成してみましょう。 `timerEnabled` 変数は、タイマーコントロールが現在有効か無効かを示します。既定値は true です。 `ToggleTimer` 関数は、2つの入力パラメーターを受け取ります。これは、[一時停止/再開] ボタンへの参照と、タイマーコントロールのクライアント側の `id` 値です。 この関数は、`timerEnabled`の値を切り替えるか、タイマーコントロールへの参照を取得して (`timerEnabled`の値に応じて) タイマーを開始または停止し、ボタンの表示テキストを "Pause" または "Resume" に更新します。 この関数は、[一時停止/再開] ボタンがクリックされるたびに呼び出されます。

まず、`Scripts`という名前の web サイトに新しいフォルダーを作成します。 次に、JScript ファイル型の `TimerScript.js` という名前の Scripts フォルダーに新しいファイルを追加します。

[新しい JavaScript ファイルを Scripts フォルダーに追加 ![には](master-pages-and-asp-net-ajax-cs/_static/image23.png)](master-pages-and-asp-net-ajax-cs/_static/image22.png)

**図 08**: `Scripts` フォルダーに新しい JavaScript ファイルを追加する ([クリックすると、フルサイズの画像が表示](master-pages-and-asp-net-ajax-cs/_static/image24.png)されます)

[新しい JavaScript ファイルが Web サイトに追加され ![](master-pages-and-asp-net-ajax-cs/_static/image26.png)](master-pages-and-asp-net-ajax-cs/_static/image25.png)

**図 09**: 新しい JavaScript ファイルが web サイトに追加されました ([クリックすると、フルサイズの画像が表示](master-pages-and-asp-net-ajax-cs/_static/image27.png)されます)

次に、次のスクリプトを TimerScript .js ファイルに追加します。

[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample8.cs)]

ここで、このカスタム JavaScript ファイルを `ShowRandomProduct.aspx`に登録する必要があります。 `ShowRandomProduct.aspx` に戻り、ページに ScriptManagerProxy コントロールを追加します。`ID` を `MyManagerProxy`に設定します。 カスタム JavaScript ファイルを登録するには、デザイナーで ScriptManagerProxy コントロールを選択し、プロパティウィンドウにアクセスします。 プロパティの1つに、[スクリプト] というタイトルが付いています。 このプロパティを選択すると、図10に示す System.web.ui.scriptreference Collection Editor が表示されます。 [追加] ボタンをクリックして新しいスクリプト参照を追加し、[パス] プロパティにスクリプトファイルへのパスを入力します (`~/Scripts/TimerScript.js`)。

[スクリプト参照を ScriptManagerProxy コントロールに追加 ![には](master-pages-and-asp-net-ajax-cs/_static/image29.png)](master-pages-and-asp-net-ajax-cs/_static/image28.png)

**図 10**: スクリプト参照を ScriptManagerProxy コントロールに追加する ([クリックすると、フルサイズの画像が表示](master-pages-and-asp-net-ajax-cs/_static/image30.png)されます)

スクリプト参照を追加した後、次のマークアップのスニペットに示すように、ScriptManagerProxy コントロールの宣言型マークアップは、1つの `ScriptReference` エントリを含む `<Scripts>` コレクションを含むように更新されます。

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample9.aspx)]

`ScriptReference` エントリは、表示されたマークアップに JavaScript ファイルへの参照を含めるように ScriptManagerProxy に指示します。 つまり、カスタムスクリプトを ScriptManagerProxy に登録すると、`ShowRandomProduct.aspx` ページの表示される出力に、別の `<script src="url"></script>` タグ: `<script src="Scripts/TimerScript.js" type="text/javascript"></script>`が含まれるようになります。

これで、`ShowRandomProduct.aspx` ページのクライアントスクリプトから `TimerScript.js` で定義されている `ToggleTimer` 関数を呼び出すことができるようになりました。 UpdatePanel 内に次の HTML を追加します。

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample10.aspx)]

これにより、"Pause" というテキストのボタンが表示されます。 クリックするたびに、JavaScript 関数 `ToggleTimer` が呼び出され、ボタンへの参照とタイマーコントロールの id 値 (`ProductTimer`) が渡されます。 タイマーコントロールの `id` 値を取得するための構文に注意してください。 `<%=ProductTimer.ClientID%>` は、`ProductTimer` Timer コントロールの `ClientID` プロパティの値を出力します。 [*コンテンツページでのコントロール ID の名前付け*](control-id-naming-in-content-pages-cs.md)に関するチュートリアルでは、サーバー側の `ID` 値と結果として得られるクライアント側の `id` 値の違いと、`ClientID` がクライアント側の `id`を返す方法の違いについて説明しました。

図11は、ブラウザーを使用して最初にアクセスしたときにこのページを示しています。 タイマーが現在実行されており、表示されている製品情報を15秒ごとに更新します。 図12は、[一時停止] ボタンがクリックされた後の画面を示しています。 [一時停止] ボタンをクリックすると、タイマーが停止し、ボタンのテキストが "Resume" に更新されます。 ユーザーが [再開] をクリックすると、製品情報が更新されます (15 秒ごとに更新が続きます)。

[![[一時停止] ボタンをクリックして、タイマーコントロールを停止します。](master-pages-and-asp-net-ajax-cs/_static/image32.png)](master-pages-and-asp-net-ajax-cs/_static/image31.png)

**図 11**: [一時停止] ボタンをクリックしてタイマーコントロールを停止する ([クリックすると、フルサイズの画像が表示](master-pages-and-asp-net-ajax-cs/_static/image33.png)されます)

[![[再開] ボタンをクリックしてタイマーを再開します。](master-pages-and-asp-net-ajax-cs/_static/image35.png)](master-pages-and-asp-net-ajax-cs/_static/image34.png)

**図 12**: [再開] ボタンをクリックしてタイマーを再起動する ([クリックすると、フルサイズの画像が表示](master-pages-and-asp-net-ajax-cs/_static/image36.png)されます)

## <a name="summary"></a>要約

Ajax 対応の web アプリケーションを ASP.NET AJAX フレームワークを使用してビルドする場合、すべての AJAX 対応 web ページに ScriptManager コントロールが含まれている必要があります。 このプロセスを容易にするために、scriptmanager を各コンテンツページに追加することを忘れずに、ScriptManager をマスターページに追加することができます。 手順 1. では、ScriptManager をマスターページに追加する方法について説明しましたが、手順 2. では、コンテンツページへの AJAX 機能の実装について見てきました。

カスタムスクリプト、スクリプトを有効にした Web サービスへの参照、またはカスタマイズされた認証、承認、またはプロファイルサービスを特定のコンテンツページに追加する必要がある場合は、[コンテンツ] ページに ScriptManagerProxy コントロールを追加し、次のように構成します。カスタマイズします。 ステップ3では、ScriptManagerProxy を使用して、特定のコンテンツページにカスタム JavaScript ファイルを登録する方法を確認しています。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET AJAX フレームワーク](../../../../ajax/index.md)
- [ASP.NET AJAX チュートリアル](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)
- [ASP.NET AJAX のビデオ](../../../videos/aspnet-ajax/index.md)
- [Microsoft ASP.NET AJAX を使用した対話型ユーザーインターフェイスの構築](http://aspnet.4guysfromrolla.com/articles/101007-1.aspx)
- [NEWID を使用してレコードをランダムに並べ替える](http://www.sqlteam.com/article/using-newid-to-randomly-sort-records)
- [Timer コントロールの使用](http://aspnet.4guysfromrolla.com/articles/061808-1.aspx)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(複数の asp/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 3.5 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)ています。 Scott は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](interacting-with-the-content-page-from-the-master-page-cs.md)
> [次へ](specifying-the-master-page-programmatically-cs.md)

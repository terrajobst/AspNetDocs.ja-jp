---
uid: mvc/overview/performance/bundling-and-minification
title: バンドルと縮小 |Microsoft Docs
author: Rick-Anderson
description: バンドルと縮小は、要求の読み込み時間を向上させるために ASP.NET 4.5 で使用できる2つの手法です。 バンドルと縮小によって、reducin による読み込み時間が向上します...
ms.author: riande
ms.date: 08/23/2012
ms.assetid: 5894dc13-5d45-4dad-8096-136499120f1d
msc.legacyurl: /mvc/overview/performance/bundling-and-minification
msc.type: authoredcontent
ms.openlocfilehash: 239980d747c6e0d6be1e9b4fe0371e276e37cf21
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519285"
---
# <a name="bundling-and-minification"></a>バンドル化と縮小

[Rick Anderson]((https://twitter.com/RickAndMSFT))

> バンドルと縮小は、要求の読み込み時間を向上させるために ASP.NET 4.5 で使用できる2つの手法です。 バンドルと縮小は、サーバーへの要求の数を減らし、要求された資産のサイズ (CSS や JavaScript など) を減らすことによって、読み込み時間を短縮します。

現在の主要なブラウザーのほとんどは、各ホスト名の[同時接続](http://www.browserscope.org/?category=network)数を6に制限しています。 つまり、6つの要求が処理されている間に、ホスト上の資産に対する追加の要求は、ブラウザーによってキューに登録されます。 次の図では、IE F12 開発者ツールの [ネットワーク] タブに、サンプルアプリケーションの [About] ビューで必要とされる資産のタイミングが示されています。

![B/M](bundling-and-minification/_static/image1.png)

灰色のバーは、ブラウザーが6つの接続制限を待機しているときに、要求がキューに入れられた時間を示します。 黄色のバーは、最初のバイトまでの要求時間 (つまり、要求の送信とサーバーからの最初の応答の受信にかかった時間) です。 青色のバーは、サーバーからの応答データの受信にかかった時間を示します。 資産をダブルクリックすると、詳細なタイミング情報を取得できます。 たとえば、次の図は、 */Scripts/MyScripts/JavaScript6.js*ファイルを読み込むためのタイミングの詳細を示しています。

![](bundling-and-minification/_static/image2.png)

上の図は、ブラウザーが同時接続の数を制限しているために要求がキューに入れられた時間を示す**開始**イベントを示しています。 この場合、要求は別の要求の完了を待機している46ミリ秒間キューに登録されました。

## <a name="bundling"></a>まとめる

バンドルは ASP.NET 4.5 の新機能で、複数のファイルを簡単に1つのファイルに結合したりバンドルしたりすることができます。 CSS、JavaScript、その他のバンドルを作成できます。 ファイルの数が減ると、HTTP 要求が減り、最初のページ読み込みのパフォーマンスが向上します。

次の図は、前に示した [About] ビューと同じタイミングビューを示していますが、今回はバンドルと縮小が有効になっています。

![](bundling-and-minification/_static/image3.png)

## <a name="minification"></a>縮小

縮小は、スクリプトや css に対してさまざまなコードの最適化を実行します。たとえば、不要な空白やコメントを削除し、変数名を1文字に短縮します。 次の JavaScript 関数を考えてみます。

[!code-javascript[Main](bundling-and-minification/samples/sample1.js)]

縮小の後、関数は次のように縮小されます。

[!code-javascript[Main](bundling-and-minification/samples/sample2.js)]

コメントや不要な空白文字を削除するだけでなく、次のようなパラメーターと変数名が変更されました (短縮)。

| **Original** | **変わり** |
| --- | --- |
| imageTagAndImageID | n |
| imageContext | t |
| imageElement | i |

## <a name="impact-of-bundling-and-minification"></a>バンドルと縮小の影響

次の表は、サンプルプログラムですべての資産を個別に一覧表示し、バンドルと縮小 (B/M) を使用する場合の、いくつかの重要な違いを示しています。

|  | **B/M を使用する** | **B/M なし** | **変更** |
| --- | --- | --- | --- |
| **ファイル要求** | 9 | 34 | 256% |
| **送信済み KB** | 3.26 | 11.92 | 266% |
| **受信した KB** | 388.51 | 530 | 36% |
| **読み込み時間** | 510ミリ秒 | 780 MS | 53% |

送信されるバイト数は、ブラウザーが要求に適用される HTTP ヘッダーとかなり冗長であるため、バンドルによって大幅に削減されました。 最大のファイル (*スクリプト\\jquery-ui-1.8.11* and *scripts\\jquery-1.7.1*) は、既に縮小されているため、受信バイト数の減少はそれほど大きくありません。 注: サンプルプログラムのタイミングでは、 [Fiddler](http://www.fiddler2.com/fiddler2/)ツールを使用して低速ネットワークをシミュレートしています。 (Fiddler の **[規則]** メニューで、 **[パフォーマンス]** 、 **[モデムの速度をシミュレート]** する の順に選択します)。

## <a name="debugging-bundled-and-minified-javascript"></a>バンドルされた、縮小された JavaScript のデバッグ

Javascript ファイルがバンドルまたは縮小されていないため、開発環境で JavaScript を簡単にデバッグ*できます (web.config ファイルの*[コンパイル要素](https://msdn.microsoft.com/library/s10awwz0.aspx)は `debug="true"` に設定されています)。 JavaScript ファイルがバンドルおよび縮小されたリリースビルドをデバッグすることもできます。 IE F12 開発者ツールを使用すると、次の方法を使用して、縮小されたバンドルに含まれる JavaScript 関数をデバッグできます。

1. **[スクリプト]** タブを選択し、 **[デバッグの開始]** ボタンを選択します。
2. [アセット] ボタンを使用して、デバッグする JavaScript 関数を含むバンドルを選択します。  
    ![](bundling-and-minification/_static/image4.png)
3. [**構成] ボタン**![](bundling-and-minification/_static/image5.png)を選択し、 **[Javascript の書式設定]** を選択して、表示されている javascript の書式を設定します。
4. **[検索スクリプト]** 入力ボックスで、デバッグする関数の名前を選択します。 次の図では、 **[検索スクリプト]** 入力ボックスに**Addalttoimg**が入力されています。  
    ![](bundling-and-minification/_static/image6.png)

F12 開発者ツールを使用したデバッグの詳細については、MSDN の記事「 [f12 開発者ツールを使用した JavaScript エラーのデバッグ」を](https://msdn.microsoft.com/library/ie/gg699336(v=vs.85).aspx)参照してください。

## <a name="controlling-bundling-and-minification"></a>バンドルと縮小の制御

バンドルと縮小*は、web.config ファイルの*[コンパイル要素](https://msdn.microsoft.com/library/s10awwz0.aspx)の debug 属性の値を設定することによって有効または無効になります。 次の XML では、バンドルと縮小が無効になるように `debug` が true に設定されています。

[!code-xml[Main](bundling-and-minification/samples/sample3.xml?highlight=2)]

バンドルと縮小を有効にするには、`debug` 値を "false" に設定します。 `BundleTable` クラスの `EnableOptimizations` プロパティを*使用して web.config 設定を*オーバーライドできます。 次のコードを使用すると、バンドルと縮小が可能に*なり、web.config ファイルの*設定が上書きされます。

[!code-csharp[Main](bundling-and-minification/samples/sample4.cs?highlight=7)]

> [!NOTE]
> `EnableOptimizations` が `true` さ*れてい*ない場合、または web.config ファイルの[コンパイル要素](https://msdn.microsoft.com/library/s10awwz0.aspx)の debug 属性が `false`に設定されている場合を除き、ファイルはバンドルまたは縮小されません。 また、ファイルの最小バージョンが使用されないため、完全なデバッグバージョンが選択されます。 `EnableOptimizations` は、web.config ファイルの[コンパイル要素](https://msdn.microsoft.com/library/s10awwz0.aspx)の debug 属性よりも優先され*ます。*

## <a name="using-bundling-and-minification-with-aspnet-web-forms-and-web-pages"></a>ASP.NET Web フォームと Web ページでのバンドルと縮小の使用

- Web ページについては、web[ページサイトへの Web 最適化の追加に](https://docs.microsoft.com/archive/blogs/rickandy/adding-web-optimization-to-a-web-pages-site)関するブログエントリを参照してください。
- Web フォームについては、 [Web フォームへのバンドルと縮小の追加に](https://docs.microsoft.com/archive/blogs/rickandy/adding-bundling-and-minification-to-web-forms)関するブログエントリを参照してください。

## <a name="using-bundling-and-minification-with-aspnet-mvc"></a>ASP.NET MVC でのバンドルと縮小の使用

このセクションでは、ASP.NET MVC プロジェクトを作成して、バンドルと縮小を確認します。 まず、既定値を変更せずに、 **Mvcbm**という名前の新しい ASP.NET MVC インターネットプロジェクトを作成します。

*アプリ\\を開き \_\\BundleConfig.cs*ファイルを起動し、バンドルの作成、登録、および構成に使用される `RegisterBundles` 方法を確認します。 次のコードは、`RegisterBundles` メソッドの一部を示しています。

[!code-csharp[Main](bundling-and-minification/samples/sample5.cs)]

上記のコードは、すべての適切な (デバッグまたは縮小) を含む、 */bundles/jquery*という名前の新しい JavaScript バンドルを作成します。*vsdoc*) ワイルドカード文字列 "~/Scripts/jquery-{version}.js" に一致する*Scripts*フォルダー内のファイル。 ASP.NET MVC 4 の場合、これはデバッグ構成で、ファイル*jquery-1.7.1*がバンドルに追加されることを意味します。 リリース構成では、 *jquery-1.7.1*が追加されます。 バンドルフレームワークは、次のようないくつかの一般的な規則に従います。

- ファイルが存在*する場合に*、release の ". min" ファイルを選択*します*。
- デバッグの非 ". min" バージョンを選択しています。
- "-Vsdoc" ファイル ( *jquery-1.7.1*など) は無視されます。これは、IntelliSense によってのみ使用されます。

上に示した `{version}` ワイルドカード一致は、適切なバージョンの jQuery を*Scripts*フォルダーに自動的に作成するために使用されます。 この例では、ワイルドカードを使用すると、次のような利点があります。

- では、ビューページで前のバンドルコードや jQuery 参照を変更することなく、NuGet を使用して新しい jQuery バージョンに更新することができます。
- では、デバッグ構成の完全バージョンと、リリースビルドの ". 分" バージョンが自動的に選択されます。

## <a name="using-a-cdn"></a>CDN の使用

 次のコードは、ローカルの jQuery バンドルを CDN jQuery バンドルに置き換えます。

[!code-csharp[Main](bundling-and-minification/samples/sample6.cs)]

上記のコードでは、リリースモードでは CDN から jQuery が要求され、デバッグバージョンの jQuery はデバッグモードでローカルにフェッチされます。 CDN を使用する場合は、CDN 要求が失敗した場合に備えてフォールバックメカニズムが必要です。 レイアウトファイルの末尾にある次のマークアップフラグメントは、CDN が失敗したことを要求するために追加されたスクリプトを示しています。

[!code-cshtml[Main](bundling-and-minification/samples/sample7.cshtml?highlight=5-13)]

## <a name="creating-a-bundle"></a>バンドルの作成

[バンドル](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx)クラス `Include` メソッドは、文字列の配列を受け取ります。各文字列はリソースへの仮想パスです。 アプリの `RegisterBundles` メソッドの次のコードでは *\\BundleConfig.cs file の開始 \_\\* 、バンドルへの複数のファイルの追加方法を示しています。

[!code-csharp[Main](bundling-and-minification/samples/sample8.cs)]

[バンドル](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx)クラス `IncludeDirectory` メソッドは、検索パターンに一致するディレクトリ (および必要に応じてすべてのサブディレクトリ) 内のすべてのファイルを追加するために用意されています。 [バンドル](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx)クラス `IncludeDirectory` API を以下に示します。

[!code-csharp[Main](bundling-and-minification/samples/sample9.cs)]

バンドルは、Render メソッドを使用してビュー内で参照されます (CSS の場合は`Styles.Render`、JavaScript の場合は `Scripts.Render`)。 *Views\\Shared \_\\のビュー*の次のマークアップは、既定の ASP.NET internet プロジェクトビューが CSS と JavaScript バンドルを参照する方法を示しています。

[!code-cshtml[Main](bundling-and-minification/samples/sample10.cshtml?highlight=5-6,11)]

Render メソッドが文字列の配列を受け取ることに注意してください。そのため、1行のコードに複数のバンドルを追加できます。 通常は、アセットを参照するために必要な HTML を作成する Render メソッドを使用します。 `Url` メソッドを使用して、資産を参照するために必要なマークアップなしでアセットへの URL を生成できます。 新しい HTML5[非同期](http://www.whatwg.org/specs/web-apps/current-work/#attr-script-async)属性を使用するとします。 次のコードは、`Url` メソッドを使用して、modernizr を参照する方法を示しています。

[!code-cshtml[Main](bundling-and-minification/samples/sample11.cshtml?highlight=11)]

## <a name="using-the--wildcard-character-to-select-files"></a>"\*" ワイルドカード文字を使用したファイルの選択

`Include` メソッドで指定した仮想パスと、`IncludeDirectory` メソッドの検索パターンでは、最後のパスセグメントののプレフィックスまたはサフィックスとして、1つの "\*" ワイルドカード文字を使用できます。 検索文字列の大文字と小文字は区別されません。 `IncludeDirectory` メソッドには、サブディレクトリを検索するオプションがあります。

次の JavaScript ファイルを含むプロジェクトを考えてみましょう。

- *スクリプト\\共通\\AddAltToImg*
- *スクリプト\\共通\\ToggleDiv*
- *スクリプト\\共通\\ToggleImg*
- *スクリプト\\共通\\Sub1\\ToggleLinks*

![dir imag](bundling-and-minification/_static/image7.png)

次の表は、ワイルドカードを使用してバンドルに追加されるファイルを示しています。

| **Call** | **追加または例外が発生したファイル** |
| --- | --- |
| Include("~/Scripts/Common/\*.js") | *Addalttoimg .js*、 *ToggleDiv*、 *ToggleImg* |
| Include("~/Scripts/Common/T\*.js") | 無効なパターン例外です。 ワイルドカード文字は、プレフィックスまたはサフィックスに対してのみ使用できます。 |
| Include("~/Scripts/Common/\*og.\*") | 無効なパターン例外です。 ワイルドカード文字は1つだけ使用できます。 |
| Include ("~/スクリプト/Common/t\*") | *ToggleDiv*、 *ToggleImg* |
| Include ("~/スクリプト/Common/\*") | 無効なパターン例外です。 純粋ワイルドカードセグメントが無効です。 |
| IncludeDirectory("~/Scripts/Common", "T\*") | *ToggleDiv*、 *ToggleImg* |
| IncludeDirectory ("~/スクリプト/共通"、"T\*"、true) | *ToggleDiv*、 *ToggleImg*、 *ToggleLinks*のようになります。 |

一般に、各ファイルをバンドルに明示的に追加することは、次のような理由で、ファイルのワイルドカード読み込みよりも優先されます。

- ワイルドカードを使用してスクリプトを追加すると、既定ではアルファベット順に読み込まれます。これは通常は必要ありません。 CSS ファイルと JavaScript ファイルは、多くの場合、特定の (アルファベット順ではない) 順序で追加する必要があります。 このリスクを軽減するには、カスタム[IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx)実装を追加しますが、各ファイルを明示的に追加するとエラーが発生しやすくなります。 たとえば、将来的にはフォルダーに新しい資産を追加し、 [IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx)の実装を変更することが必要になる場合があります。
- ワイルドカードによる読み込みを使用してディレクトリに追加された特定のファイルを表示すると、そのバンドルを参照するすべてのビューに含めることができます。 ビュー固有のスクリプトがバンドルに追加されると、バンドルを参照する他のビューで JavaScript エラーが発生することがあります。
- 他のファイルをインポートする CSS ファイルは、インポートされたファイルを2回読み込むことになります。 たとえば、次のコードでは、ほとんどの jQuery UI テーマ CSS ファイルが2回読み込まれたバンドルが作成されます。 

    [!code-csharp[Main](bundling-and-minification/samples/sample12.cs)]

  ワイルドカードセレクター "\*.css" は、フォルダー内の各 CSS ファイル (*コンテンツ\\テーマ\\base\\jquery. ui. すべての .css*ファイル) を取り込みます。 *すべての .css*ファイルは、他の css ファイルをインポートします。

## <a name="bundle-caching"></a>バンドルキャッシュ

バンドルは、バンドルの作成時に、HTTP Expires ヘッダーを1年に設定します。 以前に表示されていたページに移動した場合、Fiddler は、バンドルに対する条件付き要求を作成しないことを示します。つまり、バンドルに対する IE からの HTTP GET 要求とサーバーからの HTTP 304 応答がありません。 F5 キーを使用して各バンドルの条件付き要求を実行するように、IE に強制することができます (その結果、各バンドルに対して HTTP 304 応答が返されます)。 ^ F5 を使用して完全更新を強制的に実行できます (その結果、各バンドルに対して HTTP 200 応答が返されます)。

次の図は、Fiddler response ウィンドウの **キャッシュ** タブを示しています。

![fiddler キャッシュイメージ](bundling-and-minification/_static/image8.png)

要求   
`http://localhost/MvcBM_time/bundles/AllMyScripts?v=r0sLDicvP58AIXN_mc3QdyVvVj5euZNzdsa2N1PKvb81`  
 はバンドル**Allmyscripts**用であり、クエリ文字列 pair **v = R0sLDicvP58AIXN\\\_mc3QdyVvVj5euZNzdsa2N1PKvb81**を含んでいます。 クエリ文字列**v**には、キャッシュに使用される一意の識別子である値トークンがあります。 バンドルが変更されない限り、ASP.NET アプリケーションはこのトークンを使用して**Allmyscripts**バンドルを要求します。 バンドル内のいずれかのファイルが変更された場合、ASP.NET optimization framework は新しいトークンを生成します。これにより、バンドルに対するブラウザーの要求が最新のバンドルを取得することが保証されます。

IE9 F12 developer tools を実行し、以前に読み込まれたページに移動した場合、IE では、各バンドルに対して行われた条件付き GET 要求と、HTTP 304 を返すサーバーが誤って表示されます。 IE9 に問題がある理由を確認するには、CDNs を使用したブログエントリで条件付き要求が行われたかどうかを判断し、 [Web サイトのパフォーマンスを向上させるために期限切れに](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)します。

## <a name="less-coffeescript-scss-sass-bundling"></a>LESS、CoffeeScript、SCSS、Sass のバンドル。

バンドルと縮小フレームワークには、 [SCSS](http://sass-lang.com/)、 [sass](http://sass-lang.com/)、 [LESS](http://www.dotlesscss.org/) 、または[Coffeescript](http://coffeescript.org/)などの中間言語を処理し、縮小などの変換を結果のバンドルに適用するメカニズムが用意されています。 たとえば、追加する[.less](http://www.dotlesscss.org/) MVC 4 プロジェクト ファイル。

1. コンテンツの少ないフォルダーを作成します。 次の例では、*コンテンツ\\MyLess*フォルダーを使用しています。
2. 追加、 [.less](http://www.dotlesscss.org/) NuGet パッケージ**ドット**をプロジェクトにします。  
    ![NuGet のドットのないインストール](bundling-and-minification/_static/image9.png)
3. [IBundleTransform](https://msdn.microsoft.com/library/system.web.optimization.ibundletransform(VS.110).aspx)インターフェイスを実装するクラスを追加します。 .Less トランス フォームをプロジェクトに次のコードを追加します。

    [!code-csharp[Main](bundling-and-minification/samples/sample13.cs)]
4. `LessTransform` と[CssMinify](https://msdn.microsoft.com/library/system.web.optimization.cssminify(VS.110).aspx)変換を使用して、LESS ファイルのバンドルを作成します。 *アプリ\\_Start\\BundleConfig.cs*ファイルの `RegisterBundles` メソッドに次のコードを追加します。

    [!code-csharp[Main](bundling-and-minification/samples/sample14.cs)]
5. LESS バンドルを参照するすべてのビューに次のコードを追加します。

    [!code-cshtml[Main](bundling-and-minification/samples/sample15.cshtml)]

## <a name="bundle-considerations"></a>バンドルに関する考慮事項

バンドルを作成する場合は、バンドル名にプレフィックスとして "バンドル" を含めることをお勧めします。 これにより、[ルーティングの競合](https://forums.asp.net/post/5012037.aspx)を防ぐことができます。

バンドル内の1つのファイルを更新すると、バンドルクエリ文字列パラメーターに対して新しいトークンが生成され、バンドルを含むページを次回クライアントが要求したときに完全なバンドルをダウンロードする必要があります。 各資産が個別に一覧表示される従来のマークアップでは、変更されたファイルのみがダウンロードされます。 頻繁に変更される資産は、バンドルに適していない可能性があります。

バンドルと縮小は、主に最初のページ要求の読み込み時間を短縮します。 Web ページが要求されると、ブラウザーはアセット (JavaScript、CSS、およびイメージ) をキャッシュするので、バンドルと縮小では、同じページを要求しても、同じ資産を要求している同じサイト上のページを要求しても、パフォーマンスが向上しません。 資産に expires ヘッダーを正しく設定しておらず、バンドルと縮小を使用していない場合は、ブラウザーの鮮度ヒューリスティックによって、数日後に資産が古くなっているとマークされ、ブラウザーは各資産に対する検証要求を必要とします。 この場合、バンドルと縮小によって、最初のページ要求の後にパフォーマンスが向上します。 詳細については、「 [CDNs を使用する」および「Web サイトのパフォーマンスを向上させるための期限切れ](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)」を参照してください。

ブラウザーでは、各ホスト名につき6つの同時接続が制限されているため、 [CDN](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)を使用して軽減できます。 CDN はホスティングサイトとは異なるホスト名を持つため、CDN からの資産要求は、ホスト環境に対する6つの同時接続の制限に対してカウントされません。 CDN では、一般的なパッケージキャッシュとエッジキャッシュの利点も提供されます。

バンドルは、それらを必要とするページでパーティション分割する必要があります。 たとえば、インターネットアプリケーションの既定の ASP.NET MVC テンプレートでは、jQuery とは別の jQuery 検証バンドルが作成されます。 作成される既定のビューには入力がなく、値がポストされないため、検証バンドルは含まれません。

`System.Web.Optimization` 名前空間は、 *system.web. Optimization*に実装されています。 これは、縮小機能に WebGrease library (*webgrease .dll*) を利用し、さらに*Antlr3*を使用します。

*Twitter を使用して、リンクをすばやく投稿し、共有します。Twitter のハンドルは次の*とおりです: [@RickAndMSFT](http://twitter.com/RickAndMSFT)

## <a name="additional-resources"></a>その他の技術情報

- ビデオ: [Howard Dierking](https://twitter.com/#!/howard_dierking)による[バンドルと最適化](https://channel9.msdn.com/Events/aspConf/aspConf/Bundling-and-Optimizing)
- Web[ページサイトに Web 最適化を追加する](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx)。
- [Web フォームへのバンドルと縮小の追加](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx)。
- [Henrik](http://en.wikipedia.org/wiki/Henrik_Frystyk_Nielsen) [@frystyk](https://twitter.com/frystyk) F による[Web 閲覧のバンドルと縮小のパフォーマンスへの影響](https://blogs.msdn.com/b/henrikn/archive/2012/06/17/performance-implications-of-bundling-and-minification-on-http.aspx)
- Rick Anderson によって[Web サイトのパフォーマンスを向上させるために、CDNs と有効期限を使用することが](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx) [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)
- [RTT を最小化する (ラウンドトリップ時間)](https://developers.google.com/speed/docs/best-practices/rtt)

## <a name="contributors"></a>寄稿者

- Hao Kung
- [Howard Dierking](https://twitter.com/#!/howard_dierking)
- Diana LaRose

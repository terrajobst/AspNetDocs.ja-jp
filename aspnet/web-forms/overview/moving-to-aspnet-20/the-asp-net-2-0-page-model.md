---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 ページモデル |Microsoft Docs
author: microsoft
description: ASP.NET 1.x では、開発者はインラインコードモデルとコードビハインドコードモデルのどちらかを選択できました。 分離コードを実装するには、Src attr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: bcb71b2b5a484e8756406867e08e8aa699a9024d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440710"
---
# <a name="the-aspnet-20-page-model"></a>ASP.NET 2.0 ページモデル

[Microsoft](https://github.com/microsoft)

> ASP.NET 1.x では、開発者はインラインコードモデルとコードビハインドコードモデルのどちらかを選択できました。 分離コードは、@Page ディレクティブの Src 属性または CodeBehind 属性を使用して実装できます。 ASP.NET 2.0 では、開発者はインラインコードと分離コードのどちらかを選択できますが、分離コードモデルは大幅に拡張されています。

ASP.NET 1.x では、開発者はインラインコードモデルとコードビハインドコードモデルのどちらかを選択できました。 分離コードは、@Page ディレクティブの Src 属性または CodeBehind 属性を使用して実装できます。 ASP.NET 2.0 では、開発者はインラインコードと分離コードのどちらかを選択できますが、分離コードモデルは大幅に拡張されています。

## <a name="improvements-in-the-code-behind-model"></a>分離コードモデルの機能強化

ASP.NET 2.0 の分離コードモデルの変更を完全に理解するために、ASP.NET 1.x に存在するモデルをすばやく確認することをお勧めします。

## <a name="the-code-behind-model-in-aspnet-1x"></a>ASP.NET 1.x の分離コードモデル

ASP.NET 1.x では、分離コードモデルは ASPX ファイル (Web フォーム) とプログラミングコードを含む分離コードファイルで事前に記述されています。 2つのファイルは、ASPX ファイルの @Page ディレクティブを使用して接続されていました。 ASPX ページの各コントロールには、分離コードファイル内の対応する宣言がインスタンス変数として含まれていました。 分離コードファイルには、Visual Studio デザイナーに必要なイベントバインドおよび生成されたコードのコードも含まれています。 このモデルは非常にうまく機能しましたが、ASPX ページのすべての ASP.NET 要素が分離コードファイル内に対応するコードを必要としていたため、コードとコンテンツの分離は実際には行われませんでした。 たとえば、デザイナーが Visual Studio IDE の外部にある ASPX ファイルに新しいサーバーコントロールを追加した場合、分離コードファイル内にそのコントロールの宣言がないため、アプリケーションは中断されます。

## <a name="the-code-behind-model-in-aspnet-20"></a>ASP.NET 2.0 の分離コードモデル

このモデルでは、ASP.NET 2.0 が大幅に改善されています。 ASP.NET 2.0 では、ASP.NET 2.0 で提供される新しい*部分クラス*を使用して分離コードが実装されます。 ASP.NET 2.0 の分離コードクラスは部分クラスとして定義されます。これは、クラス定義の一部だけが含まれることを意味します。 クラス定義の残りの部分は、実行時に ASPX ページを使用して ASP.NET 2.0 によって動的に生成されるか、Web サイトがプリコンパイルされます。 分離コードファイルと ASPX ページ間のリンクは、引き続き @ Page ディレクティブを使用して確立されます。 ただし、CodeBehind 属性または Src 属性の代わりに、ASP.NET 2.0 では、CodeFile 属性が使用されるようになりました。 継承属性は、ページのクラス名を指定するためにも使用されます。

一般的な @ Page ディレクティブは次のようになります。

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

ASP.NET 2.0 分離コードファイルの一般的なクラス定義は、次のようになります。

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C#と Visual Basic は、現在部分クラスをサポートしている唯一のマネージ言語です。 そのため、J# を使用する開発者は、ASP.NET 2.0 で分離コードモデルを使用することはできません。

新しいモデルでは、コードビハインドモデルが拡張されます。これは、開発者が作成したコードのみを含むコードファイルがあるためです。 また、分離コードファイルにインスタンス変数宣言がないため、コードとコンテンツの真の分離も提供します。

> [!NOTE]
> ASPX ページの部分クラスはイベントバインドが行われる場所であるため、Visual Basic 開発者は、分離コードで Handles キーワードを使用してイベントをバインドすることで、わずかなパフォーマンスの向上を実感できます。 C#には同等のキーワードがありません。

## <a name="new--page-directive-attributes"></a>新しい @ Page ディレクティブ属性

ASP.NET 2.0 では、@ Page ディレクティブに多くの新しい属性が追加されます。 ASP.NET 2.0 では、次の属性が追加されています。

## <a name="async"></a>非同期

Async 属性を使用すると、ページを非同期に実行するように構成できます。 非同期ページについては、このモジュールで後ほど説明します。

## <a name="asynctimeout"></a>AsyncTimeout

非同期ページのタイムアウトを指定しました。 既定値は45秒です。

## <a name="codefile"></a>CodeFile

CodeFile 属性は、Visual Studio 2002/2003 の CodeBehind 属性に代わるものです。

### <a name="codefilebaseclass"></a>CodeFileBaseClass

CodeFileBaseClass 属性は、1つの基底クラスから複数のページを派生させる場合に使用します。 ASP.NET では部分クラスが実装されているため、この属性がないと、共有共通フィールドを使用する基本クラスは、ASPX ページで宣言されたコントロールを参照するために適切に機能しません。これは、ASP.NET コンパイルエンジンがページ内のコントロールに基づいて新しいメンバーを自動的に作成するためです。 このため、ASP.NET の2つ以上のページに共通の基本クラスが必要な場合は、CodeFileBaseClass 属性で基底クラスを指定し、その基底クラスから各 pages クラスを派生させる必要があります。 この属性を使用する場合は、CodeFile 属性も必要です。

## <a name="compilationmode"></a>CompilationMode

この属性を使用すると、ASPX ページの CompilationMode プロパティを設定できます。 CompilationMode プロパティは、値**Always**、 **Auto**、および**Never**を含む列挙体です。 既定値は**常に**です。 **自動**設定では、可能であれば、ASP.NET がページを動的にコンパイルできないようにします。 動的コンパイルからページを除外すると、パフォーマンスが向上します。 ただし、除外されたページにコンパイルする必要があるコードが含まれている場合、ページが参照されるとエラーがスローされます。

## <a name="enableeventvalidation"></a>EnableEventValidation

この属性は、ポストバックイベントとコールバックイベントを検証するかどうかを指定します。 これが有効になっている場合、ポストバックまたはコールバックイベントの引数は、最初に表示されたサーバーコントロールから生成されたものであることを確認するためにチェックされます。

## <a name="enabletheming"></a>EnableTheming

この属性は、ページで ASP.NET テーマを使用するかどうかを指定します。 既定値は **false** です。 ASP.NET のテーマについては、[モジュール 10](profiles-themes-and-web-parts.md)で説明します。

## <a name="linepragmas"></a>LinePragmas

この属性は、コンパイル時に行プラグマを追加する必要があるかどうかを指定します。 行プラグマは、コードの特定のセクションをマークするためにデバッガーによって使用されるオプションです。

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

この属性は、ポストバック間のスクロール位置を維持するために、ページに JavaScript を挿入するかどうかを指定します。 既定では、この属性は**false**です。

この属性が**true**の場合、ASP.NET は次のような &lt;スクリプト&gt; ブロックをポストバックに追加します。

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

このスクリプトブロックの src は Webresource.axd です。 このリソースは物理パスではありません。 このスクリプトが要求されると、ASP.NET はスクリプトを動的に構築します。

### <a name="masterpagefile"></a>MasterPageFile

この属性は、現在のページのマスターページファイルを指定します。 相対パスと絶対パスのどちらでも構いません。 マスターページについては、[モジュール 4](master-pages.md)で説明します。

## <a name="stylesheettheme"></a>StyleSheetTheme

この属性を使用すると、ASP.NET 2.0 テーマによって定義されたユーザーインターフェイスの外観プロパティをオーバーライドできます。 テーマについては、[モジュール 10](profiles-themes-and-web-parts.md)で説明します。

## <a name="theme"></a>テーマ

ページのテーマを指定します。 StyleSheetTheme 属性に値が指定されていない場合、ページ上のコントロールに適用されるすべてのスタイルが Theme 属性によってオーバーライドされます。

## <a name="title"></a>タイトル

ページのタイトルを設定します。 ここで指定した値は、表示されるページの &lt;title&gt; 要素に表示されます。

### <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

ViewStateEncryptionMode 列挙体の値を設定します。 使用できる値は、**常**に、 **Auto**、および**Never**です。 既定値は**Auto**です。この属性が**Auto**の値に設定されている場合、viewstate は暗号化されます。これは、 **RegisterRequiresViewStateEncryption**メソッドを呼び出すことによってコントロールが要求します。

## <a name="setting-public-property-values-via-the--page-directive"></a>@ Page ディレクティブを使用したパブリックプロパティの値の設定

ASP.NET 2.0 の @ Page ディレクティブのもう1つの新機能は、基底クラスのパブリックプロパティの初期値を設定できることです。 たとえば、基底クラスに**テキスト**と呼ばれるパブリックプロパティがあり、ページが読み込まれるときに**Hello**に初期化されるとします。 これは、次のように @ Page ディレクティブの値を設定するだけで実現できます。

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

@ Page ディレクティブの**text**属性では、基底クラスのテキストプロパティの初期値が*Hello!* に設定されています。 次のビデオでは、@ Page ディレクティブを使用して基底クラスのパブリックプロパティの初期値を設定する方法を説明しています。

![](the-asp-net-2-0-page-model/_static/image1.png)

[全画面表示のビデオを開く](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>ページクラスの新しいパブリックプロパティ

ASP.NET 2.0 では、次のパブリックプロパティが追加されています。

## <a name="apprelativetemplatesourcedirectory"></a>AppRelativeTemplateSourceDirectory

ページまたはコントロールへのアプリケーション相対パスを返します。 たとえば、 http://app/folder/page.aspxにあるページの場合、プロパティは ~/folder/. を返します。

## <a name="apprelativevirtualpath"></a>AppRelativeVirtualPath

ページまたはコントロールへの相対仮想ディレクトリパスを返します。 たとえば、 http://app/folder/page.aspxにあるページの場合、プロパティは ~/folder/page.aspx. を返します。

## <a name="asynctimeout"></a>AsyncTimeout

非同期ページ処理に使用されるタイムアウトを取得または設定します。 (非同期ページについては、このモジュールで後ほど説明します)。

## <a name="clientquerystring"></a>ClientQueryString

要求された URL のクエリ文字列部分を返す読み取り専用のプロパティ。 この値は、URL でエンコードされます。 設定クラスの UrlDecode メソッドを使用してデコードできます。

## <a name="clientscript"></a>ClientScript

このプロパティは、クライアント側スクリプトの ClientScriptManager を管理するために使用できる、オブジェクトを返します。 (ClientScriptManager クラスについては、このモジュールで後ほど説明します)。

## <a name="enableeventvalidation"></a>EnableEventValidation

このプロパティは、ポストバックイベントとコールバックイベントに対してイベントの検証を有効にするかどうかを制御します。 有効にすると、ポストバックまたはコールバックイベントの引数が検証され、最初に表示したサーバーコントロールからのものであることが確認されます。

## <a name="enabletheming"></a>EnableTheming

このプロパティは、ASP.NET 2.0 テーマがページに適用されるかどうかを指定するブール値を取得または設定します。

## <a name="form"></a>Form

このプロパティは、ASPX ページの HTML フォームを HtmlForm オブジェクトとして返します。

## <a name="header"></a>ヘッダー

このプロパティは、ページヘッダーを含む HtmlHead オブジェクトへの参照を返します。 返された HtmlHead オブジェクトを使用して、スタイルシートやメタタグなどを取得/設定できます。

## <a name="idseparator"></a>IdSeparator

この読み取り専用プロパティは、ASP.NET がページ上のコントロールの一意の ID を作成しているときに、コントロール識別子を区切るために使用される文字を取得します。 コードから直接使用するためのものではありません。

## <a name="isasync"></a>IsAsync

このプロパティでは、非同期ページを使用できます。 非同期ページについては、このモジュールで後ほど説明します。

## <a name="iscallback"></a>IsCallback

この読み取り専用プロパティは、ページがコールバックの結果である場合に**true**を返します。 コールバックについては、このモジュールで後ほど説明します。

## <a name="iscrosspagepostback"></a>IsCrossPagePostBack

この読み取り専用プロパティは、ページがクロスページポストバックの一部である場合に**true**を返します。 ページ間のポストバックについては、このモジュールで後ほど説明します。

## <a name="items"></a>アイテム

ページコンテキストに格納されているすべてのオブジェクトを含む IDictionary インスタンスへの参照を返します。 この IDictionary オブジェクトに項目を追加すると、コンテキストの有効期間全体にわたって使用できるようになります。

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostBack

このプロパティは、ポストバックが発生した後にブラウザーでページのスクロール位置を保持する JavaScript を ASP.NET が出力するかどうかを制御します。 (このプロパティの詳細については、このモジュールで既に説明しました)。

## <a name="master"></a>Master

この読み取り専用プロパティは、マスターページが適用されているページのマスターインスタンスへの参照を返します。

## <a name="masterpagefile"></a>MasterPageFile

ページのマスターページのファイル名を取得または設定します。 このプロパティは、PreInit メソッドでのみ設定できます。

## <a name="maxpagestatefieldlength"></a>MaxPageStateFieldLength

このプロパティは、ページの状態の最大長をバイト単位で取得または設定します。 プロパティが正の値に設定されている場合、ページビューステートは、指定されたバイト数を超えないように、複数の非表示フィールドに分割されます。 プロパティが負の数の場合、ビューステートはチャンクに分割されません。

## <a name="pageadapter"></a>PageAdapter

要求側のブラウザーのページを変更する PageAdapter オブジェクトへの参照を返します。

## <a name="previouspage"></a>PreviousPage

サーバー転送またはクロスページポストバックの場合に、前のページへの参照を返します。

## <a name="skinid"></a>SkinID

ページに適用する ASP.NET 2.0 スキンを指定します。

## <a name="stylesheettheme"></a>StyleSheetTheme

このプロパティは、ページに適用されるスタイルシートを取得または設定します。

## <a name="templatecontrol"></a>TemplateControl

ページのコントロールを格納しているへの参照を返します。

## <a name="theme"></a>テーマ

ページに適用される ASP.NET 2.0 テーマの名前を取得または設定します。 この値は、PreInit メソッドの前に設定する必要があります。

## <a name="title"></a>タイトル

このプロパティは、ページヘッダーから取得されたページのタイトルを取得または設定します。

## <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

ページの ViewStateEncryptionMode を取得または設定します。 このモジュールで前に説明したこのプロパティの詳細については、こちらを参照してください。

## <a name="new-protected-properties-of-the-page-class"></a>ページクラスの新しいプロテクトプロパティ

ASP.NET 2.0 のページクラスの新しいプロテクトプロパティを次に示します。

## <a name="adapter"></a>アダプター

要求したデバイス上でページをレンダリングする ControlAdapter への参照を返します。

## <a name="asyncmode"></a>AsyncMode

このプロパティは、ページが非同期に処理されるかどうかを示します。 これは、コード内で直接使用するのではなく、ランタイムによって使用されることを意図しています。

## <a name="clientidseparator"></a>ClientIDSeparator

このプロパティは、コントロールの一意のクライアント Id を作成するときに区切り記号として使用される文字を返します。 これは、コード内で直接使用するのではなく、ランタイムによって使用されることを意図しています。

## <a name="pagestatepersister"></a>PageStatePersister

このプロパティは、ページの PageStatePersister オブジェクトを返します。 このプロパティは、主に ASP.NET コントロールの開発者によって使用されます。

## <a name="uniquefilepathsuffix"></a>UniqueFilePathSuffix

このプロパティは、ブラウザーをキャッシュするためのファイルパスに追加される一意のサフィックスを返します。 既定値は \_\_ufps = および6桁の数字です。

## <a name="new-public-methods-for-the-page-class"></a>ページクラスの新しいパブリックメソッド

次のパブリックメソッドは、ASP.NET 2.0 のページクラスに新しく追加されたものです。

## <a name="addonprerendercompleteasync"></a>AddOnPreRenderCompleteAsync

このメソッドは、非同期ページ実行のイベントハンドラーデリゲートを登録します。 非同期ページについては、このモジュールで後ほど説明します。

## <a name="applystylesheetskin"></a>ApplyStyleSheetSkin

ページスタイルシートのプロパティをページに適用します。

## <a name="executeregisteredasynctasks"></a>ExecuteRegisteredAsyncTasks

このメソッドは非同期タスクです。

### <a name="getvalidators"></a>GetValidators

指定された検証グループの検証コントロールのコレクションを返します。何も指定されていない場合は、既定の検証グループを返します。

## <a name="registerasynctask"></a>RegisterAsyncTask

このメソッドは、新しい非同期タスクを登録します。 非同期ページについては、このモジュールで後ほど説明します。

## <a name="registerrequirescontrolstate"></a>RegisterRequiresControlState

このメソッドは、ページコントロールの状態を永続化する必要があることを ASP.NET に通知します。

## <a name="registerrequiresviewstateencryption"></a>RegisterRequiresViewStateEncryption

このメソッドは、ページ viewstate に暗号化が必要であることを ASP.NET に通知します。

## <a name="resolveclienturl"></a>ResolveClientUrl

イメージに対するクライアント要求に使用できる相対 URL を返します。

## <a name="setfocus"></a>SetFocus

このメソッドは、ページが最初に読み込まれるときに指定されるコントロールにフォーカスを設定します。

## <a name="unregisterrequirescontrolstate"></a>UnregisterRequiresControlState

このメソッドは、コントロールの状態の永続化を必要としないように、渡されたコントロールの登録を解除します。

## <a name="changes-to-the-page-lifecycle"></a>ページのライフサイクルの変更

ASP.NET 2.0 のページライフサイクルは大幅に変更されていませんが、注意する必要がある新しい方法がいくつかあります。 ASP.NET 2.0 ページのライフサイクルは次のとおりです。

## <a name="preinit-new-in-aspnet-20"></a>PreInit (ASP.NET 2.0 の新)

PreInit イベントは、開発者がアクセスできる、ライフサイクルの最も早い段階です。 このイベントを追加すると、ASP.NET 2.0 のテーマ、マスターページ、ASP.NET 2.0 プロファイルのアクセスプロパティをプログラムで変更できるようになります。ポストバック状態の場合、Viewstate は、ライフサイクルのこの時点でコントロールにまだ適用されていないことを認識することが重要です。 このため、開発者がこの段階でコントロールのプロパティを変更すると、後でページのライフサイクルで上書きされる可能性があります。

## <a name="init"></a>Init

Init イベントは ASP.NET 1.x から変更されていません。 ここでは、ページ上のコントロールのプロパティを読み取りまたは初期化します。 この段階では、マスターページ、テーマなどが既にページに適用されています。

## <a name="initcomplete-new-in-20"></a>InitComplete (2.0 の新)

InitComplete イベントは、ページ初期化ステージの最後に呼び出されます。 ライフサイクルのこの時点では、ページ上のコントロールにアクセスできますが、その状態はまだ設定されていません。

## <a name="preload-new-in-20"></a>プリロード (2.0 の新)

このイベントは、すべてのポストバックデータが適用された後、ページ\_の読み込みの直前に呼び出されます。

## <a name="load"></a>[読み込み]

Load イベントは ASP.NET 1.x から変更されていません。

## <a name="loadcomplete-new-in-20"></a>LoadComplete (2.0 の新)

LoadComplete イベントは、ページ読み込みステージの最後のイベントです。 この段階では、すべてのポストバックと viewstate データがページに適用されています。

## <a name="prerender"></a>PreRender

ページに動的に追加されるコントロールに対して viewstate を適切に管理するには、PreRender イベントを追加する最後の機会とします。

## <a name="prerendercomplete-new-in-20"></a>PreRenderComplete (2.0 の新)

PreRenderComplete 段階では、すべてのコントロールがページに追加され、ページを表示する準備ができました。 PreRenderComplete イベントは、ページ viewstate が保存される前に発生する最後のイベントです。

## <a name="savestatecomplete-new-in-20"></a>SaveStateComplete (2.0 の新)

SaveStateComplete イベントは、すべてのページ viewstate とコントロールの状態が保存された直後に呼び出されます。 これは、ページが実際にブラウザーにレンダリングされる前の最後のイベントです。

## <a name="render"></a>レンダー

ASP.NET 1.x 以降、Render メソッドは変更されていません。 ここで HtmlTextWriter が初期化され、ページがブラウザーに表示されます。

## <a name="cross-page-postback-in-aspnet-20"></a>ASP.NET 2.0 のクロスページポストバック

ASP.NET 1.x では、同じページにポストバックする必要がありました。 ページ間のポストバックは許可されませんでした。 ASP.NET 2.0 では、IButtonControl インターフェイスを使用して別のページにポストバックする機能が追加されています。 新しい IButtonControl インターフェイス (サードパーティのカスタムコントロールに加えて Button、LinkButton、および ImageButton) を実装するコントロールは、PostBackUrl 属性を使用することによって、この新しい機能を利用できます。 次のコードは、2番目のページにポストバックするボタンコントロールを示しています。

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

ページがポストバックされると、ポストバックを開始するページは、2ページ目の PreviousPage プロパティを使用してアクセスできます。 この機能は、コントロールが別のページにポストバックしたときに ASP.NET 2.0 がページに表示する新しい Web フォーム\_DoPostBackWithOptions クライアント側関数によって実装されます。 この JavaScript 関数は、クライアントにスクリプトを出力する新しい Webresource.axd ハンドラーによって提供されます。

次のビデオは、ページ間のポストバックのチュートリアルです。

![](the-asp-net-2-0-page-model/_static/image2.png)

[全画面表示のビデオを開く](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>クロスページポストバックの詳細

### <a name="viewstate"></a>Viewstate

クロスページポストバックシナリオでは、最初のページから viewstate に対して何が起こるかについて、既にたずねているかもしれません。 結局のところ、IPostBackDataHandler を実装していないコントロールは viewstate によって状態を保持するので、ページ間のポストバックの2ページ目でそのコントロールのプロパティにアクセスするには、ページの viewstate にアクセスできる必要があります。 ASP.NET 2.0 は、\_\_PREVIOUSPAGE と呼ばれる2番目のページの新しい隠しフィールドを使用して、このシナリオを処理します。 \_\_PREVIOUSPAGE フォームフィールドには、最初のページの viewstate が含まれています。これにより、2番目のページのすべてのコントロールのプロパティにアクセスできるようになります。

### <a name="circumventing-findcontrol"></a>FindControl の回避

クロスページポストバックのビデオチュートリアルでは、FindControl メソッドを使用して、最初のページの TextBox コントロールへの参照を取得しました。 この方法は、その目的に適していますが、FindControl は高価であり、追加のコードを記述する必要があります。 幸いにも、ASP.NET 2.0 では、この目的のために FindControl の代わりに、多くのシナリオで動作するようになっています。 PreviousPageType ディレクティブを使用すると、TypeName または VirtualPath 属性を使用して、前のページへの厳密に型指定された参照を持つことができます。 TypeName 属性では、前のページの種類を指定できます。 VirtualPath 属性では、仮想パスを使用して前のページを参照できます。 PreviousPageType ディレクティブを設定したら、パブリックプロパティを使用してアクセスを許可するコントロールなどを公開する必要があります。

## <a name="lab-1-cross-page-postback"></a>ラボ1ページ間ポストバック

このラボでは、ASP.NET 2.0 の新しいクロスページポストバック機能を使用するアプリケーションを作成します。

1. Visual Studio 2005 を開き、新しい ASP.NET Web サイトを作成します。
2. Page2 という名前の新しい Web フォームを追加します。
3. デザインビューで default.aspx を開き、ボタンコントロールとテキストボックスコントロールを追加します。 

    1. ボタンコントロールに**Submitbutton**の id を指定し、テキストボックスコントロールに**ユーザー名**の id を指定します。
    2. ボタンの PostBackUrl プロパティを page2 に設定します。
4. ソースビューで page2 を開きます。
5. 次に示すように、@ PreviousPageType ディレクティブを追加します。
6. ページに次のコードを追加して、page2 の分離コードの\_読み込みます。 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. [ビルド] メニューの [ビルド] をクリックして、プロジェクトをビルドします。
8. Default.aspx の分離コードに次のコードを追加します。 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. Page2 での\_の読み込みページを次のように変更します。 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. プロジェクトをビルドします。
11. プロジェクトを実行します。
12. テキストボックスに名前を入力し、ボタンをクリックします。
13. 結果は何ですか。

## <a name="asynchronous-pages-in-aspnet-20"></a>ASP.NET 2.0 の非同期ページ

ASP.NET の競合に関する多くの問題は、外部呼び出し (Web サービスやデータベースの呼び出しなど) の待機時間、ファイル IO の待機時間などによって発生します。ASP.NET アプリケーションに対して要求が行われると、ASP.NET はそのワーカースレッドの1つを使用してその要求を処理します。 この要求は、要求が完了し、応答が送信されるまで、そのスレッドを所有します。 ASP.NET 2.0 は、ページを非同期的に実行する機能を追加することで、これらの種類の問題の待機時間の問題を解決することを目指しています。 これは、ワーカースレッドが要求を開始し、別のスレッドに対して追加の実行をハンドオフして、使用可能なスレッドプールにすばやく戻ることができることを意味します。 ファイル IO、データベース呼び出しなどが完了すると、新しいスレッドがスレッドプールから取得され、要求が完了します。

ページを非同期で実行するための最初の手順は、次のようにページディレクティブの**Async**属性を設定することです。

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

この属性は、ページの IHttpAsyncHandler を実装するように ASP.NET に指示します。

次の手順では、PreRender の前に、ページのライフサイクルのポイントで AddOnPreRenderCompleteAsync メソッドを呼び出します。 (通常、このメソッドは、ページ\_の読み込み時に呼び出されます)。AddOnPreRenderCompleteAsync メソッドは2つのパラメーターを受け取ります。BeginEventHandler と EndEventHandler。 BeginEventHandler は、パラメーターとして EndEventHandler に渡される IAsyncResult を返します。

次のビデオは、非同期ページ要求のチュートリアルです。

![](the-asp-net-2-0-page-model/_static/image3.png)

[全画面表示のビデオを開く](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> EndEventHandler が完了するまで、非同期ページはブラウザーに表示されません。 当然のことですが、一部の開発者は非同期要求を非同期コールバックに似ていると考えています。 そうではないことに注意することが重要です。 非同期要求の利点は、新しい要求を処理するために最初のワーカースレッドをスレッドプールに返すことができることです。これにより、IO バインドが原因で競合が減少します。

## <a name="script-callbacks-in-aspnet-20"></a>ASP.NET 2.0 のスクリプトコールバック

Web 開発者は、コールバックに関連するちらつきを防ぐ方法を常に探していました。 ASP.NET 1.x では、SmartNavigation はちらつきを避けるための最も一般的な方法でしたが、クライアントでの実装が複雑になるため、SmartNavigation は一部の開発者にとって問題を引き起こしました。 ASP.NET 2.0 では、スクリプトコールバックに関するこの問題に対処しています。 スクリプトコールバックは、XMLHttp を利用して、Web サーバーに対して JavaScript 経由で要求を行います。 XMLHttp 要求は、ブラウザーの DOM を使用して操作できる XML データを返します。 XMLHttp コードは、新しい Webresource.axd ハンドラーによってユーザーに表示されません。

ASP.NET 2.0 でスクリプトコールバックを構成するために必要な手順がいくつかあります。

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>手順 1: ICallbackEventHandler インターフェイスを実装する

ASP.NET がスクリプトコールバックに参加しているとしてページを認識できるようにするには、ICallbackEventHandler インターフェイスを実装する必要があります。 これは、分離コードファイルで次のように実行できます。

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

この操作は、次のように @ Implements ディレクティブを使用して行うこともできます。

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

インライン ASP.NET コードを使用する場合は、通常、@ Implements ディレクティブを使用します。

## <a name="step-2--call-getcallbackeventreference"></a>手順 2: GetCallbackEventReference を呼び出す

前述のように、XMLHttp 呼び出しは Webresource.axd ハンドラーにカプセル化されています。 ページが表示されると、ASP.NET は、Webresource.axd によって提供されるクライアントスクリプトである Web フォーム\_DoCallback への呼び出しを追加します。 Web フォーム\_DoCallback 関数は、コールバックの \_\_doPostBack バック関数を置き換えます。 \_\_doPostBack バックは、プログラムによってページにフォームを送信することに注意してください。 コールバックシナリオでは、ポストバックを防止する必要があるため、\_\_doPostBack バックでは十分ではありません。

> [!NOTE]
> \_\_doPostBack バックは、クライアントスクリプトコールバックシナリオのページに引き続き表示されます。 ただし、コールバックには使用されません。

Web フォーム\_DoCallback クライアント側関数の引数は、通常はページ\_読み込みで呼び出されるサーバー側の関数 GetCallbackEventReference を介して提供されます。 GetCallbackEventReference の一般的な呼び出しは次のようになります。

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> この場合、cm は ClientScriptManager のインスタンスです。 ClientScriptManager クラスについては、このモジュールで後ほど説明します。

GetCallbackEventReference には、いくつかのオーバーロードされたバージョンがあります。 この場合、引数は次のようになります。

`this`

GetCallbackEventReference が呼び出されているコントロールへの参照。 この例では、ページ自体です。

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

クライアント側のコードからサーバー側のイベントに渡される文字列引数。 この場合、Im は ddlCompany というドロップダウンの値を渡します。

`ShowCompanyName`

サーバー側のコールバックイベントから (文字列として) 戻り値を受け取るクライアント側関数の名前。 この関数は、サーバー側のコールバックが成功した場合にのみ呼び出されます。 そのため、堅牢性を確保するために、通常は、オーバーロードされたバージョンの GetCallbackEventReference を使用することをお勧めします。これは、エラーが発生した場合に実行するクライアント側関数の名前を指定する追加の文字列引数を受け取ります。

`null`

サーバーへのコールバックの前に開始したクライアント側の関数を表す文字列。 この場合、このようなスクリプトは存在しないため、引数は null になります。

`true`

コールバックを非同期的に実行するかどうかを指定するブール値。

クライアント上で Web フォーム\_DoCallback を呼び出すと、これらの引数が渡されます。 このため、このページがクライアントに表示されると、そのコードは次のようになります。

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

クライアント上の関数のシグネチャが少し異なることに注意してください。 クライアント側の関数は、5つの文字列とブール値を渡します。 追加の文字列 (上の例では null) には、サーバー側のコールバックからのエラーを処理するクライアント側の関数が含まれています。

## <a name="step-3--hook-the-client-side-control-event"></a>手順 3: クライアント側のコントロールイベントをフックする

上記の GetCallbackEventReference の戻り値が文字列変数に割り当てられていることに注意してください。 この文字列は、コールバックを開始するコントロールのクライアント側イベントをフックするために使用されます。 この例では、コールバックはページのドロップダウンによって開始されるため、 *OnChange*イベントをフックします。

クライアント側のイベントをフックするには、次のように、クライアント側のマークアップにハンドラーを追加するだけです。

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

*CGetCallbackEventReference f*は、呼び出しからの戻り値であることを思い出してください。 これには、上に示した Web フォーム\_DoCallback の呼び出しが含まれています。

## <a name="step-4--register-the-client-side-script"></a>手順 4: クライアント側のスクリプトを登録する

GetCallbackEventReference を呼び出すことで、サーバー側のコールバックが成功したときに**Showcompanyname**というクライアント側のスクリプトが実行されることが指定されたことを思い出してください。 このスクリプトは、ClientScriptManager インスタンスを使用してページに追加する必要があります。 (ClientScriptManager クラスについては、このモジュールで後ほど説明します)。次のようにします。

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>手順 5: ICallbackEventHandler インターフェイスのメソッドを呼び出す

ICallbackEventHandler には、コードに実装する必要がある2つのメソッドが含まれています。 これらは**RaiseCallbackEvent**と**GetCallbackEvent**です。

**RaiseCallbackEvent**は、引数として文字列を受け取り、nothing を返します。 文字列引数は、クライアント側の呼び出しから Web フォーム\_DoCallback に渡されます。 この場合、その値は ddlCompany というドロップダウンリストの*value*属性です。 サーバー側のコードは、RaiseCallbackEvent メソッドに配置する必要があります。 たとえば、コールバックが外部リソースに対して WebRequest を作成する場合、そのコードは RaiseCallbackEvent に配置する必要があります。

**GetCallbackEvent**は、クライアントへのコールバックの戻り値を処理します。 引数を取らず、文字列を返します。 返される文字列は、クライアント側の関数 (この場合は*Showcompanyname*) に引数として渡されます。

上記の手順を完了すると、ASP.NET 2.0 でスクリプトコールバックを実行する準備が整います。

![](the-asp-net-2-0-page-model/_static/image4.png)

[全画面表示のビデオを開く](the-asp-net-2-0-page-model/_static/callback1.wmv)

ASP.NET のスクリプトコールバックは、XMLHttp 呼び出しをサポートするすべてのブラウザーでサポートされています。 これには、現在使用されているすべての最新のブラウザーが含まれます。 Internet Explorer は、XMLHttp ActiveX オブジェクトを使用しますが、その他の最新のブラウザー (今後の IE 7 を含む) は、組み込みの XMLHttp オブジェクトを使用します。 ブラウザーがコールバックをサポートしているかどうかをプログラムで判断するには、 **SupportCallback**プロパティを使用します。 このプロパティは、要求元のクライアントがスクリプトコールバックをサポートしている場合に**true**を返します。

## <a name="working-with-client-script-in-aspnet-20"></a>ASP.NET 2.0 でのクライアントスクリプトの使用

ASP.NET 2.0 のクライアントスクリプトは、ClientScriptManager クラスを使用して管理されます。 ClientScriptManager クラスは、型と名前を使用して、クライアントスクリプトを追跡します。 これにより、同じスクリプトが1ページに複数回、プログラムによって挿入されるのを防ぐことができます。

> [!NOTE]
> ページにスクリプトが正常に登録されると、その後、同じスクリプトを登録しようとすると、スクリプトが2回目に登録されなくなるだけです。 重複するスクリプトは追加されず、例外は発生しません。 不要な計算を避けるために、スクリプトが既に登録されているかどうかを判断するために使用できるメソッドがあります。これにより、スクリプトを複数回登録することはできません。

ClientScriptManager のメソッドは、現在のすべての ASP.NET 開発者を対象としています。

## <a name="registerclientscriptblock"></a>RegisterClientScriptBlock

このメソッドは、レンダリングされたページの先頭にスクリプトを追加します。 これは、クライアントで明示的に呼び出される関数を追加する場合に便利です。

このメソッドには、2つのオーバーロードされたバージョンがあります。 4つの引数のうち3つは共通です。 これらは次のとおりです。

`type (string)`

***型***引数は、スクリプトの型を識別します。 一般に、このページの種類を使用することをお勧めします (これは、型に対して GetType ()) を使用します。

`key (string)`

***キー***引数は、スクリプトのユーザー定義キーです。 これは、スクリプトごとに一意である必要があります。 既に追加されているスクリプトと同じキーおよび種類のスクリプトを追加しようとすると、そのスクリプトは追加されません。

`script (string)`

***スクリプト***引数は、追加する実際のスクリプトを含む文字列です。 StringBuilder を使用してスクリプトを作成した後、StringBuilder で ToString () メソッドを使用して***スクリプト***の引数を割り当てることをお勧めします。

3つの引数のみを受け取るオーバーロードされた RegisterClientScriptBlock を使用する場合は、スクリプトにスクリプト要素 (&lt;script&gt; と &lt;/script&gt;) を含める必要があります。

4番目の引数を受け取る RegisterClientScriptBlock のオーバーロードを使用することもできます。 4番目の引数は、ASP.NET がスクリプト要素を追加する必要があるかどうかを指定するブール値です。 この引数が**true**の場合、スクリプトにはスクリプト要素を明示的に含めないでください。

IsClientScriptBlockRegistered メソッドを使用して、スクリプトが既に登録されているかどうかを確認します。 これにより、既に登録されているスクリプトの再登録を避けることができます。

### <a name="registerclientscriptinclude-new-in-20"></a>RegisterClientScriptInclude (2.0 の新)

RegisterClientScriptInclude タグは、外部スクリプトファイルにリンクするスクリプトブロックを作成します。 2つのオーバーロードがあります。 1つはキーと URL を受け取ります。 2番目の引数は、型を指定する3番目の引数を追加します。

たとえば、次のコードでは、アプリケーションの scripts フォルダーのルートにある jsfunctions にリンクするスクリプトブロックが生成されます。

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

このコードでは、表示されるページに次のコードが生成されます。

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> スクリプトブロックはページの下部に表示されます。

Isclientscriptの登録解除メソッドを使用して、スクリプトが既に登録されているかどうかを確認します。 これにより、スクリプトの再登録が試行されないようにすることができます。

## <a name="registerstartupscript"></a>RegisterStartupScript

RegisterStartupScript メソッドは、RegisterClientScriptBlock メソッドと同じ引数を受け取ります。 RegisterStartupScript に登録されているスクリプトは、ページが読み込まれた後、OnLoad クライアント側のイベントの前に実行されます。 1\.x では、RegisterStartupScript に登録されているスクリプトは、RegisterClientScriptBlock に登録されているスクリプトが、開始 &lt;フォーム&gt; タグの直後に配置されている間に、終了 &lt;/&gt; タグの直前に配置されました。 ASP.NET 2.0 では、両方とも、終了 &lt;/&gt; タグの直前に配置されます。

> [!NOTE]
> RegisterStartupScript に関数を登録すると、その関数は、クライアント側のコードで明示的に呼び出されるまで実行されません。

IsStartupScriptRegistered メソッドを使用して、スクリプトが既に登録されているかどうかを確認し、スクリプトの再登録を試行しないようにします。

## <a name="other-clientscriptmanager-methods"></a>その他の ClientScriptManager メソッド

ClientScriptManager クラスのその他の便利なメソッドの一部を次に示します。

|  <strong>GetCallbackEventReference</strong>   |                                                 このモジュールの「スクリプトコールバック」を参照してください。                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>GetPostBackClientHyperlink</strong>  |                クライアント側のイベントからポストバックするために使用できる JavaScript 参照 (javascript:&lt;呼び出し&gt;) を取得します。                 |
|  <strong>System.web.ui.clientscriptmanager.getpostbackeventreference</strong>   |                                   クライアントからポストバックを開始するために使用できる文字列を取得します。                                    |
|      <strong>GetWebResourceUrl</strong>       | アセンブリに埋め込まれているリソースへの URL を返します。 <strong>RegisterClientScriptResource</strong>と組み合わせて使用する必要があります。 |
| <strong>RegisterClientScriptResource</strong> |     Web リソースをページに登録します。 これらは、アセンブリに埋め込まれ、新しい Webresource.axd ハンドラーによって処理されるリソースです。      |
|     <strong>RegisterHiddenField</strong>      |                                                 非表示のフォームフィールドをページに登録します。                                                 |
|  <strong>RegisterOnSubmitStatement</strong>   |                                  HTML フォームの送信時に実行されるクライアント側のコードを登録します。                                   |

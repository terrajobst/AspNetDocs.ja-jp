---
uid: web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
title: フォーム認証の概要 (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、単なるディスカッションから実装について説明します。特に、フォーム認証の実装について説明します。 Web アプリケーション w...
ms.author: riande
ms.date: 01/14/2008
ms.assetid: 83267f7d-64d9-41ee-82cf-da91b1bf534d
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: d8ceb6b5290300992e52199caa9314c573de1942
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514630"
---
# <a name="an-overview-of-forms-authentication-vb"></a>フォーム認証の概要 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_02_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial02_FormsAuth_vb.pdf)

> このチュートリアルでは、単なるディスカッションから実装について説明します。特に、フォーム認証の実装について説明します。 このチュートリアルで作成する web アプリケーションは、単純なフォーム認証からメンバーシップとロールに移行するときに、以降のチュートリアルでも引き続きビルドされます。
> 
> このトピックの詳細については、「 [ASP.NET での基本フォーム認証の使用](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)」を参照してください。

## <a name="introduction"></a>はじめに

前の[チュートリアル](security-basics-and-asp-net-support-vb.md)では、ASP.NET によって提供されるさまざまな認証、承認、ユーザーアカウントのオプションについて説明しました。 このチュートリアルでは、単なるディスカッションから実装について説明します。特に、フォーム認証の実装について説明します。 このチュートリアルで作成する web アプリケーションは、単純なフォーム認証からメンバーシップとロールに移行するときに、以降のチュートリアルでも引き続きビルドされます。

このチュートリアルでは、まず、フォーム認証ワークフロー (前のチュートリアルで触れたトピック) について詳しく説明します。 次に、フォーム認証の概念をデモするための ASP.NET web サイトを作成します。 次に、フォーム認証を使用するようにサイトを構成し、単純なログインページを作成します。また、ユーザーが認証されているかどうかをコードで確認する方法、およびユーザーがログインしたユーザー名を確認する方法についても説明します。

フォーム認証ワークフローについて理解し、web アプリケーションで有効にし、ログインページとログオフページを作成することは、ユーザーアカウントをサポートし、web ページを介してユーザーを認証する ASP.NET アプリケーションを構築するためのすべての重要な手順です。 このため、これらのチュートリアルは相互に構築されるため、以前のプロジェクトでフォーム認証を構成している経験がある場合でも、次のチュートリアルに進む前に、このチュートリアルを完全に実行することをお勧めします。

## <a name="understanding-the-forms-authentication-workflow"></a>フォーム認証ワークフローについて

ASP.NET ランタイムが ASP.NET page や ASP.NET Web service などの ASP.NET リソースの要求を処理すると、その要求によって、そのライフサイクル中に多数のイベントが発生します。 要求の最初と最後にイベントが発生し、要求が認証され、承認されたときに発生したイベント、未処理の例外が発生した場合に発生するイベントなどがあります。 イベントの完全な一覧を表示するには、 [HttpApplication オブジェクトのイベント](https://msdn.microsoft.com/library/system.web.httpapplication_events.aspx)を参照してください。

*HTTP モジュール*は、要求ライフサイクル内の特定のイベントに応答して実行されるコードを持つマネージクラスです。 ASP.NET には、バックグラウンドで重要なタスクを実行する多数の HTTP モジュールが付属しています。 ここで説明するために特に関連する2つの組み込み HTTP モジュールは、次のとおりです。

- **[FormsAuthenticationModule](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)** -フォーム認証チケットを調べることによってユーザーを認証します。これは通常、ユーザーの cookies コレクションに含まれています。 フォーム認証チケットが存在しない場合、ユーザーは匿名です。
- **[Urlauthorizationmodule](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)** -要求された URL へのアクセスが現在のユーザーに許可されているかどうかを判断します。 このモジュールは、アプリケーションの構成ファイルで指定されている承認規則を確認することによって、権限を決定します。 また、ASP.NET には、要求されたファイルの Acl をコンサルティングして機関を決定する[Fileauthorizationmodule](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx)も含まれています。

FormsAuthenticationModule は、UrlAuthorizationModule (および FileAuthorizationModule) を実行する前に、ユーザーの認証を試みます。 要求を行っているユーザーが要求されたリソースへのアクセスを承認されていない場合、承認モジュールは要求を終了し、 [HTTP 401 の許可](http://www.checkupdown.com/status/E401.html)されていない状態を返します。 Windows 認証シナリオでは、HTTP 401 状態がブラウザーに返されます。 この状態コードにより、ブラウザーはモーダルダイアログボックスを使用して資格情報の入力を求めます。 ただし、フォーム認証では、HTTP 401 の未承認ステータスがブラウザーに送信されることはありません。これは、FormsAuthenticationModule がこの状態を検出し、代わりに、( [http 302 リダイレクト](http://www.checkupdown.com/status/E302.html)ステータスを使用して) ユーザーをログインページにリダイレクトするように変更するためです。

ログインページの役割は、ユーザーの資格情報が有効であるかどうかを判断し、その場合はフォーム認証チケットを作成して、アクセスしようとしていたページにユーザーをリダイレクトすることです。 認証チケットは、web サイト上のページへの後続の要求に含まれます。この要求は、FormsAuthenticationModule がユーザーを識別するために使用します。

[フォーム認証ワークフローの ![](an-overview-of-forms-authentication-vb/_static/image2.png)](an-overview-of-forms-authentication-vb/_static/image1.png)

**図 01**: フォーム認証ワークフロー ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image3.png)されます)

### <a name="remembering-the-authentication-ticket-across-page-visits"></a>ページアクセス全体で認証チケットを記憶する

ログイン後、各要求でフォーム認証チケットを web サーバーに送り返す必要があります。これにより、ユーザーはサイトを参照するときにログインしたままになります。 通常、これはユーザーの cookies コレクションに認証チケットを配置することで実現されます。 [Cookie](http://en.wikipedia.org/wiki/HTTP_cookie)は、ユーザーのコンピューター上に存在し、cookie を作成した web サイトへの各要求の HTTP ヘッダーで送信される小さなテキストファイルです。 したがって、フォーム認証チケットが作成され、ブラウザーの cookie に格納されると、そのサイトにアクセスするたびに、要求と共に認証チケットが送信され、それによってユーザーが識別されます。

> [!NOTE]
> 各チュートリアルで使用されているデモ web アプリケーションは、ダウンロードとして入手できます。 このダウンロード可能なアプリケーションは、.NET Framework バージョン3.5 を対象とした Visual Web Developer 2008 で作成されました。 アプリケーションは .NET 3.5 を対象としているため、その web.config ファイルには、3.5 固有の追加の構成要素が含まれています。 長期的には、コンピューターに .NET 3.5 をまだインストールしていない場合は、まず、web.config から3.5 固有のマークアップを削除しなくても、ダウンロード可能な web アプリケーションは機能しません。

Cookie の1つの側面は、ブラウザーが cookie を破棄する日付と時刻である、有効期限です。 フォーム認証クッキーの有効期限が切れると、ユーザーは認証されなくなり、匿名になります。 ユーザーが公共のターミナルからアクセスしているときは、ブラウザーを閉じるときに認証チケットが期限切れになる可能性があります。 ただし、自宅からアクセスする場合、同じユーザーは、サイトにアクセスするたびに再ログインする必要がないように、ブラウザーの再起動を通じて認証チケットを記憶する必要があります。 この決定は、多くの場合、ログインページの [ユーザーに記憶する] チェックボックスの形式で行います。 手順3では、ログインページで [保存] チェックボックスを実装する方法を確認します。 次のチュートリアルでは、認証チケットのタイムアウト設定について詳しく説明します。

> [!NOTE]
> Web サイトへのログオンに使用したユーザーエージェントが cookie をサポートしていない可能性があります。 このような場合、ASP.NET では、cookie なしのフォーム認証チケットを使用できます。 このモードでは、認証チケットは URL にエンコードされます。 ここでは、クッキーレス認証チケットが使用される場合と、次のチュートリアルで作成および管理される方法について説明します。

### <a name="the-scope-of-forms-authentication"></a>フォーム認証のスコープ

FormsAuthenticationModule は、ASP.NET ランタイムの一部であるマネージコードです。 Microsoft の[インターネットインフォメーションサービス (iis)](https://www.iis.net/) web サーバーのバージョン7より前では、IIS の HTTP パイプラインと ASP.NET ランタイムのパイプラインの間には個別のバリアがありました。 つまり、IIS 6 以前では、FormsAuthenticationModule は、IIS から ASP.NET ランタイムに要求が委任された場合にのみ実行されます。 既定では、IIS は静的なコンテンツ自体 (HTML ページ、CSS、イメージファイルなど) を処理します。また、.aspx、.asmx、または .ashx の拡張子を持つページが要求された場合にのみ、ASP.NET ランタイムに要求を渡します。

ただし、IIS 7 では、IIS と ASP.NET の統合パイプラインを使用できます。 いくつかの構成設定を使用して、IIS 7 をセットアップして、*すべて*の要求に対して FormsAuthenticationModule を呼び出すことができます。 さらに、IIS 7 では、任意の種類のファイルの URL 承認規則を定義できます。 詳細については、「 [IIS6 と iis7 のセキュリティ間の変更](https://www.iis.net/learn/get-started/whats-new-in-iis-7/changes-in-security-between-iis-60-and-iis-7-and-above)」、「 [Web Platform security](https://www.iis.net/learn/get-started/whats-new-in-iis-7/iis7-and-above-security-improvements)」、および「 [iis7 URL Authorization](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)」を参照してください。

長期的に言えば、IIS 7 より前のバージョンでは、フォーム認証のみを使用して、ASP.NET ランタイムによって処理されるリソースを保護できます。 同様に、URL 承認規則は ASP.NET ランタイムによって処理されるリソースにのみ適用されます。 ただし、IIS 7 では、FormsAuthenticationModule と UrlAuthorizationModule を IIS の HTTP パイプラインに統合して、この機能をすべての要求に拡張することができます。

## <a name="step-1-creating-an-aspnet-website-for-this-tutorial-series"></a>手順 1: このチュートリアルシリーズの ASP.NET Web サイトを作成する

最も多くのユーザーにリーチするために、このシリーズで作成する ASP.NET web サイトは、Microsoft の無料版の Visual Studio 2008、 [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)を使用して作成されます。 [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx)データベースに SqlMembershipProvider ユーザーストアを実装します。 Visual studio 2005 を使用している場合、または Visual Studio 2008 または SQL Server の別のエディションを使用している場合は、心配する必要はありません。手順はほぼ同じであり、重要ではない違いが指摘されます。

フォーム認証を構成する前に、まず ASP.NET web サイトが必要です。 まず、新しいファイルシステムベースの ASP.NET web サイトを作成します。 これを行うには、Visual Web Developer を起動し、[ファイル] メニューの [新しい Web サイト] をクリックして、[新しい Web サイト] ダイアログボックスを表示します。 ASP.NET Web サイトテンプレートを選択し、[場所] ドロップダウンリストを [ファイルシステム] に設定し、Web サイトを配置するフォルダーを選択して、その言語を VB に設定します。 これにより、default.aspx ASP.NET ページ、App\_Data フォルダー、および web.config ファイルを使用して、新しい web サイトが作成されます。

> [!NOTE]
> Visual Studio では、2つのプロジェクト管理モード (Web サイトプロジェクトと Web アプリケーションプロジェクト) がサポートされています。 Web サイトプロジェクトにはプロジェクトファイルがありませんが、Web アプリケーションプロジェクトは Visual Studio .NET 2002/2003 のプロジェクトアーキテクチャに似ています。プロジェクトファイルが含まれ、プロジェクトのソースコードが1つのアセンブリにコンパイルされ、/bin フォルダーに配置されます。 Visual Studio 2005 は、web アプリケーションプロジェクトモデルが Service Pack 1 で導入されましたが、最初はサポートされている Web サイトプロジェクトのみです。Visual Studio 2008 では、両方のプロジェクトモデルが提供されます。 ただし、Visual Web Developer 2005 と2008の各エディションでは、Web サイトプロジェクトのみがサポートされます。 ここでは、Web サイトプロジェクトモデルを使用します。 Express 以外のエディションを使用していて、代わりに[Web アプリケーションプロジェクトモデル](https://msdn.microsoft.com/library/aa730880(vs.80).aspx)を使用する場合は、自由に選択してください。ただし、画面に表示される内容と、このチュートリアルで説明されているスクリーンショットや手順との間には、いくつかの違いがある可能性があることに注意してください。

[新しいファイルシステムベースの Web サイトを作成 ![には](an-overview-of-forms-authentication-vb/_static/image5.png)](an-overview-of-forms-authentication-vb/_static/image4.png)

**図 02**: 新しいファイルシステムベースの Web サイトを作成[する (クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image6.png)されます)

### <a name="adding-a-master-page"></a>マスターページの追加

次に、Site. master という名前のルートディレクトリ内のサイトに新しいマスターページを追加します。 [マスターページ](https://msdn.microsoft.com/library/wtxbf3hh.aspx)を使用すると、ページの開発者は、ASP.NET ページに適用できるサイト全体のテンプレートを定義できます。 マスターページの主な利点は、サイトの全体的な外観を1つの場所に定義できるため、サイトのレイアウトを簡単に更新または調整できることです。

[Website という名前のマスターページを Web サイトに追加 ![には](an-overview-of-forms-authentication-vb/_static/image8.png)](an-overview-of-forms-authentication-vb/_static/image7.png)

**図 03**: websites. Master という名前のマスターページを web サイトに追加する ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image9.png)されます)

ここでは、マスターページでサイト全体のページレイアウトを定義します。 デザインビューを使用して、必要なレイアウトや Web コントロールを追加したり、手動でソースビューにマークアップを手動で追加したりすることができます。 マスターページのレイアウトを構成し、 *[ASP.NET 2.0 チュートリアルシリーズのデータを操作](../../data-access/index.md)* するときに使用するレイアウトを模倣しました (図4を参照)。 マスターページでは、ファイルスタイル .css (このチュートリアルに関連するダウンロードに含まれています) に定義されている CSS 設定を使用して、配置とスタイルに[カスケードスタイルシート](http://www.w3schools.com/css/default.asp)を使用します。 次に示すマークアップからはわかりませんが、CSS 規則は、ナビゲーション &lt;div&gt;の内容が、左側に表示されるように絶対配置され、200ピクセルの固定幅であるように定義されています。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample1.aspx)]

マスターページでは、静的ページレイアウトと、マスターページを使用する ASP.NET ページで編集できる領域の両方が定義されています。 これらのコンテンツ編集可能な領域は、ContentPlaceHolder コントロールによって示されます。これは、コンテンツ &lt;div&gt;に表示されます。 マスターページには ContentPlaceHolder (MainContent) が1つありますが、マスターページには複数の ContentPlaceHolders がある場合があります。

上で入力したマークアップで、デザインビューに切り替えると、マスターページのレイアウトが表示されます。 このマスターページを使用するすべての ASP.NET ページでは、この統一レイアウトが使用され、MainContent 領域のマークアップを指定することができます。

[デザインビューで表示したときにマスターページを ![する](an-overview-of-forms-authentication-vb/_static/image11.png)](an-overview-of-forms-authentication-vb/_static/image10.png)

**図 04**: デザインビューで表示したときのマスターページ ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image12.png)されます)

### <a name="creating-content-pages"></a>コンテンツページの作成

この時点では、web サイトに default.aspx ページがありますが、先ほど作成したマスターページは使用しません。 Web ページの宣言型マークアップを操作してマスターページを使用することは可能ですが、ページにコンテンツがまだ含まれていない場合は、ページを削除してプロジェクトに再度追加するだけで、使用するマスターページを指定できます。 そのため、最初にプロジェクトから default.aspx を削除します。

次に、ソリューションエクスプローラーでプロジェクト名を右クリックし、default.aspx という名前の新しい Web フォームを追加することを選択します。 ここでは、[マスターページの選択] チェックボックスをオンにし、一覧から [.master] マスターページを選択します。

[新しい default.aspx ページを追加 ![マスターページの選択を選択します。](an-overview-of-forms-authentication-vb/_static/image14.png)](an-overview-of-forms-authentication-vb/_static/image13.png)

**図 05**: 新しい default.aspx ページを追加するマスターページの選択を選択する ([クリックしてフルサイズのイメージを表示](an-overview-of-forms-authentication-vb/_static/image15.png))

[![のマスターページを使用する](an-overview-of-forms-authentication-vb/_static/image17.png)](an-overview-of-forms-authentication-vb/_static/image16.png)

**図 06**: .Master マスターページを使用[する (クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image18.png)されます)

> [!NOTE]
> Web アプリケーションプロジェクトモデルを使用している場合は、[新しい項目の追加] ダイアログボックスに [マスターページの選択] チェックボックスは表示されません。 代わりに、種類が Web コンテンツフォームの項目を追加する必要があります。 [Web コンテンツフォーム] オプションを選択して [追加] をクリックすると、図6に示されているのと同じ [マスターの選択] ダイアログボックスが表示されます。

新しい default.aspx ページの宣言型マークアップには、マスターページファイルへのパス、およびマスターページの MainContent ContentPlaceHolder のコンテンツコントロールを指定する @Page ディレクティブだけが含まれています。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample2.aspx)]

ここでは、default.aspx を空のままにします。 コンテンツを追加するには、このチュートリアルで後ほど説明します。

> [!NOTE]
> マスターページには、メニューまたはその他のナビゲーションインターフェイスのセクションが含まれています。 このようなインターフェイスは、今後のチュートリアルで作成します。

## <a name="step-2-enabling-forms-authentication"></a>手順 2: フォーム認証を有効にする

ASP.NET web サイトを作成したので、次のタスクはフォーム認証を有効にすることです。 アプリケーションの認証構成は、web.config の[&lt;authentication&gt; 要素](https://msdn.microsoft.com/library/532aee0e.aspx)によって指定されます。&lt;authentication&gt; 要素には、アプリケーションで使用される認証モデルを指定する mode という名前の1つの属性が含まれています。 この属性には、次の4つの値のいずれかを指定できます。

- **Windows** -前のチュートリアルで説明したように、アプリケーションで Windows 認証を使用する場合は、web サーバーがビジターを認証する必要があり、通常は基本認証、ダイジェスト認証、または統合 Windows 認証を使用して行われます。
- **フォーム**-ユーザーは、web ページ上のフォームを使用して認証されます。
- **Passport**-ユーザーは、Microsoft の passport ネットワークを使用して認証されます。
- **なし**-認証モデルは使用されません。すべての訪問者は匿名です。

既定では、ASP.NET アプリケーションは Windows 認証を使用します。 認証の種類をフォーム認証に変更するには、&lt;認証の&gt; 要素のモード属性をフォームに変更する必要があります。

プロジェクトに web.config ファイルがまだ含まれていない場合は、ソリューションエクスプローラーでプロジェクト名を右クリックし、[新しい項目の追加] をクリックして、Web 構成ファイルを追加することで、もう1つ追加します。

[![プロジェクトに web.config がまだ含まれていない場合は、ここで追加します。](an-overview-of-forms-authentication-vb/_static/image20.png)](an-overview-of-forms-authentication-vb/_static/image19.png)

**図 07**: プロジェクトにまだ Web.config が含まれていない場合は、ここで追加します ([クリックすると、フルサイズのイメージが表示](an-overview-of-forms-authentication-vb/_static/image21.png)されます)

次に、&lt;authentication&gt; 要素を見つけて、フォーム認証を使用するように更新します。 この変更を行うと、web.config ファイルのマークアップは次のようになります。

[!code-xml[Main](an-overview-of-forms-authentication-vb/samples/sample3.xml)]

> [!NOTE]
> Web.config は XML ファイルであるため、大文字と小文字の区別が重要になります。 Mode 属性が、大文字 F のフォームに設定されていることを確認します。フォームなどの異なる大文字小文字を使用すると、ブラウザーからサイトにアクセスしたときに構成エラーが表示されます。

&lt;authentication&gt; 要素には、フォーム認証固有の設定を含む &lt;フォーム&gt; 子要素をオプションで含めることができます。 ここでは、既定のフォーム認証設定を使用してみましょう。 &lt;forms&gt; 子要素については、次のチュートリアルで詳しく説明します。

## <a name="step-3-building-the-login-page"></a>手順 3: ログインページを作成する

フォーム認証をサポートするために、web サイトにはログインページが必要です。 「フォーム認証ワークフローについて」セクションで説明したように、FormsAuthenticationModule は、表示を許可されていないページにアクセスしようとすると、ユーザーをログインページに自動的にリダイレクトします。 また、匿名ユーザーへのログインページへのリンクを表示する ASP.NET Web コントロールもあります。 この質問は、ログインページの URL をそことしています。

既定では、フォーム認証システムはログインページに login.aspx という名前を付け、web アプリケーションのルートディレクトリに配置することを想定しています。 別のログインページの URL を使用する場合は、web.config で指定します。これを行う方法については、以降のチュートリアルで説明します。

ログインページには、次の3つの役割があります。

1. ビジターが資格情報を入力できるようにするインターフェイスを提供します。
2. 送信された資格情報が有効かどうかを確認します。
3. フォーム認証チケットを作成して、ユーザーにログインします。

### <a name="creating-the-login-pages-user-interface"></a>ログインページのユーザーインターフェイスを作成する

最初のタスクを開始してみましょう。 新しい ASP.NET ページを login.aspx という名前のサイトのルートディレクトリに追加し、それを .master マスターページに関連付けます。

[![、login.aspx という名前の新しい ASP.NET ページを追加します。](an-overview-of-forms-authentication-vb/_static/image23.png)](an-overview-of-forms-authentication-vb/_static/image22.png)

**図 08**: Login.aspx という名前の新しい ASP.NET ページを追加[する (クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image24.png)されます)

一般的なログインページインターフェイスは、2つのテキストボックスで構成されています。1つはユーザー名用で、もう1つはパスワード用で、もう1つはフォームを送信するためのボタンです。 多くの場合、web サイトには [覚えておく] チェックボックスが含まれています

Login.aspx に2つのテキストボックスを追加し、それぞれの ID プロパティをユーザー名とパスワードに設定します。 また、パスワードの TextMode プロパティを Password に設定します。 次に、CheckBox コントロールを追加し、その ID プロパティを RememberMe に設定し、その Text プロパティを記憶するように設定します。 その後、LoginButton という名前のボタンを追加し、そのテキストプロパティが Login に設定されていることを示します。 最後に、ラベル Web コントロールを追加し、その ID プロパティを InvalidCredentialsMessage に設定します。 Text プロパティは、ユーザー名またはパスワードに対して無効です。 もう一度やり直してください。 ForeColor プロパティは赤、Visible プロパティは False になります。

この時点で、画面は図9のスクリーンショットのようになります。ページの宣言構文は次のようになります。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample4.aspx)]

[ログインページに、チェックボックス、ボタン、ラベルの2つのテキストボックスが含まれて ![](an-overview-of-forms-authentication-vb/_static/image26.png)](an-overview-of-forms-authentication-vb/_static/image25.png)

**図 09**: ログインページには、2つのテキストボックス、チェックボックス、ボタン、およびラベルがあります ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image27.png)されます)

最後に、LoginButton の Click イベントのイベントハンドラーを作成します。 デザイナーからボタンコントロールをダブルクリックするだけで、このイベントハンドラーが作成されます。

### <a name="determining-if-the-supplied-credentials-are-valid"></a>指定された資格情報が有効かどうかを確認しています

次に、ボタンの Click イベントハンドラーでタスク2を実装する必要があります。指定された資格情報が有効かどうかを判断します。 これを行うには、指定された資格情報が既知の資格情報と一致するかどうかを判断できるように、ユーザーの資格情報をすべて保持するユーザーストアが必要です。

ASP.NET 2.0 より前の開発者は、独自のユーザーストアを実装し、ストアに対して指定された資格情報を検証するコードを記述する責任がありました。 ほとんどの開発者は、ユーザー名、パスワード、電子メール、LastLoginDate などの列を使用して、データベースにユーザーストアを実装し、ユーザーという名前のテーブルを作成します。 このテーブルでは、ユーザーアカウントごとに1つのレコードが作成されます。 ユーザーが指定した資格情報を確認するには、データベースに対して一致するユーザー名のクエリを実行し、データベース内のパスワードが指定されたパスワードにこれていることを確認する必要があります。

ASP.NET 2.0 では、開発者はメンバーシッププロバイダーの1つを使用してユーザーストアを管理する必要があります。 このチュートリアルシリーズでは、ユーザーストアに SQL Server データベースを使用する SqlMembershipProvider を使用します。 SqlMembershipProvider を使用する場合は、プロバイダーが想定するテーブル、ビュー、ストアドプロシージャを含む特定のデータベーススキーマを実装する必要があります。 このスキーマの実装方法については、SQL Server チュートリアルの「 *[メンバーシップスキーマの作成](../membership/creating-the-membership-schema-in-sql-server-vb.md)* 」を確認します。 メンバーシッププロバイダーが設定されているので、ユーザーの資格情報を検証することは、[メンバーシップクラス](https://msdn.microsoft.com/library/system.web.security.membership.aspx)の[validateuser (*ユーザー名*,*パスワード*) メソッド](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)を呼び出すのと同じように簡単です。これは、ユーザー*名*と*パスワード*の組み合わせが有効かどうかを示すブール値を返します。 SqlMembershipProvider のユーザーストアをまだ実装していないので、この時点ではメンバーシップクラスの ValidateUser メソッドを使用できません。

独自のカスタムユーザーデータベーステーブル (SqlMembershipProvider を実装した後は廃止される可能性があります) を作成するのではなく、代わりにログインページ内に有効な資格情報をハードコーディングしてみましょう。 LoginButton の Click イベントハンドラーに、次のコードを追加します。

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample5.vb)]

ご覧のとおり、3つの有効なユーザーアカウント (Scott、Jisun、および Sam) と、3つすべてのパスワード (パスワード) は同じです。 このコードでは、ユーザーとパスワードの配列をループ処理して、有効なユーザー名とパスワードの一致を探します。 ユーザー名とパスワードの両方が有効な場合は、ユーザーをログインさせて、適切なページにリダイレクトする必要があります。 資格情報が無効な場合は、InvalidCredentialsMessage ラベルが表示されます。

ユーザーが有効な資格情報を入力すると、それが適切なページにリダイレクトされることを説明しました。 適切なページは何ですか。 ユーザーが表示を許可されていないページにアクセスすると、FormsAuthenticationModule によって自動的にログインページにリダイレクトされることを思い出してください。 その場合、ReturnUrl パラメーターを使用して、要求された URL を querystring に含めます。 つまり、ユーザーが ProtectedPage にアクセスしようとしたときに、ユーザーがその操作を許可されていない場合、FormsAuthenticationModule は次のようにリダイレクトします。

Login.aspx?ReturnUrl=ProtectedPage.aspx

ログインに成功すると、ユーザーは ProtectedPage にリダイレクトされます。 または、ユーザーが自分の volition のログインページにアクセスすることもできます。 この場合、ユーザーをログインした後、ルートフォルダーの default.aspx ページに送信する必要があります。

### <a name="logging-in-the-user"></a>ユーザーのログイン

指定された資格情報が有効であることを前提として、フォーム認証チケットを作成し、その結果、サイトにユーザーをログインさせる必要があります。 FormsAuthentication[名前空間](https://msdn.microsoft.com/library/system.web.security.aspx)の[クラス](https://msdn.microsoft.com/library/system.web.security.formsauthentication.aspx)には、フォーム認証システムを使用してユーザーのログインとログアウトを行うためのさまざまなメソッドが用意されています。 FormsAuthentication クラスにはいくつかのメソッドがありますが、この時点の3つの目的は次のとおりです。

- [GetAuthCookie (*username*、 *persistcookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.getauthcookie.aspx) -指定された名前の*ユーザー*名のフォーム認証チケットを作成します。 次に、このメソッドは、認証チケットの内容を保持する HttpCookie オブジェクトを作成して返します。 *Persistcookie*が True の場合は、永続的なクッキーが作成されます。
- [SetAuthCookie (*username*、 *persistcookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) -getauthcookie (*username*、 *persistcookie*) メソッドを呼び出して、フォーム認証 cookie を生成します。 次に、このメソッドは、GetAuthCookie によって返されたクッキーを Cookies コレクションに追加します (cookie ベースのフォーム認証が使用されていることを前提としています。それ以外の場合、このメソッドはクッキーレスチケットロジックを処理する内部クラスを呼び出します)。
- [RedirectFromLoginPage (*username*、 *persistcookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.redirectfromloginpage.aspx) -このメソッドは setauthcookie (*username*、 *persistcookie*) を呼び出し、適切なページにユーザーをリダイレクトします。

GetAuthCookie は、cookie を Cookie コレクションに書き込む前に認証チケットを変更する必要がある場合に便利です。 SetAuthCookie は、フォーム認証チケットを作成して Cookie コレクションに追加する必要がありますが、ユーザーを適切なページにリダイレクトしない場合に便利です。 ログインページに保存することも、別のページに送信することもできます。

ユーザーをログインし、適切なページにリダイレクトするため、RedirectFromLoginPage を使用してみましょう。 LoginButton の Click イベントハンドラーを更新して、2つのコメントが付いた TODO 行を次のコード行に置き換えます。

FormsAuthentication.RedirectFromLoginPage(UserName.Text, RememberMe.Checked)

フォーム認証チケットを作成するときは、フォーム認証チケットの*username*パラメーターに Username テキストボックスの Text プロパティを使用し、 *persistcookie*パラメーターの [Rememberme] チェックボックスのチェック状態を使用します。

ログインページをテストするには、ブラウザーでアクセスします。 ユーザー名が "いいえ"、パスワードが間違っているなど、無効な資格情報を入力して開始します。 ログインボタンをクリックすると、ポストバックが発生し、InvalidCredentialsMessage ラベルが表示されます。

[無効な資格情報を入力したときに InvalidCredentialsMessage ラベルが表示される ![](an-overview-of-forms-authentication-vb/_static/image29.png)](an-overview-of-forms-authentication-vb/_static/image28.png)

**図 10**: 無効な資格情報を入力したときに InvalidCredentialsMessage ラベルが表示される ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image30.png)されます)

次に、有効な資格情報を入力し、[ログイン] ボタンをクリックします。 この時点で、ポストバックが発生するとフォーム認証チケットが作成され、default.aspx に自動的にリダイレクトされます。 この時点で、web サイトにログインしましたが、現在ログインしていることを示す視覚的な手掛かりはありません。 手順4では、ユーザーがログインしているかどうかをプログラムで判断する方法、およびページにアクセスするユーザーを識別する方法について説明します。

手順5では、web サイトからユーザーをログアウトする方法について説明します。

### <a name="securing-the-login-page"></a>ログインページのセキュリティ保護

ユーザーが資格情報を入力し、ログインページフォームを送信すると、パスワードを含む資格情報が、インターネットを介して*プレーンテキスト*で web サーバーに送信されます。 つまり、ハッカーがネットワークトラフィックをスニッフィングすると、ユーザー名とパスワードが表示されます。 これを回避するには、 [SSL (Secure Socket layer)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)を使用してネットワークトラフィックを暗号化することが不可欠です。 これにより、資格情報 (ページ全体の HTML マークアップ) が web サーバーによって受信されるまでブラウザーを離れた時点から暗号化されるようになります。

Web サイトに機密情報が含まれていない場合は、ログインページと、ユーザーのパスワードがプレーンテキストでネットワーク経由で送信されるその他のページでのみ SSL を使用する必要があります。 フォーム認証チケットのセキュリティ保護について心配する必要はありません。既定では、暗号化とデジタル署名が行われます (改ざんを防ぐため)。 フォーム認証チケットのセキュリティについて詳しくは、次のチュートリアルで説明します。

> [!NOTE]
> 多くの金融および医療 web サイトは、認証されたユーザーがアクセスできる*すべて*のページで SSL を使用するように構成されています。 このような web サイトを構築する場合は、フォーム認証チケットがセキュリティで保護された接続でのみ送信されるように、フォーム認証システムを構成できます。 次のチュートリアル「 *[フォーム認証構成」および「高度なトピック](../membership/creating-the-membership-schema-in-sql-server-vb.md)* 」では、さまざまなフォーム認証構成オプションについて説明します。

## <a name="step-4-detecting-authenticated-visitors-and-determining-their-identity"></a>手順 4: 認証された訪問者の検出と Id の確認

この時点で、フォーム認証が有効になり、基本的なログインページが作成されましたが、ユーザーが認証されているか匿名であるかを判断する方法はまだ確認していません。 場合によっては、認証されたユーザーまたは匿名ユーザーがページにアクセスしているかどうかに応じて、異なるデータまたは情報を表示したい場合があります。 さらに、多くの場合、認証されたユーザーの id を把握しておく必要があります。

これらの手法を説明するために、既存の default.aspx ページを拡張してみましょう。 Default.aspx で、2つのパネルコントロールを追加します。1つは認証 Atedmessagepanel、もう1つは AnonymousMessagePanel という名前です。 最初のパネルで、WelcomeBackMessage という名前のラベルコントロールを追加します。 2番目のパネルでハイパーリンクコントロールを追加し、[Text] プロパティを [Log In] に設定し、[NavigateUrl] プロパティを「~/login」に設定します。 この時点で、default.aspx の宣言型マークアップは次のようになります。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample6.aspx)]

ここで推測しているように、認証された訪問者に対してのみ認証の Atedmessagepanel を表示し、匿名訪問者に AnonymousMessagePanel することをお勧めします。 これを実現するには、ユーザーがログインしているかどうかに応じて、これらのパネルの表示プロパティを設定する必要があります。

[要求の IsAuthenticated プロパティ](https://msdn.microsoft.com/library/system.web.httprequest.isauthenticated.aspx)は、要求が認証されているかどうかを示すブール値を返します。 次のコードをページ\_読み込みイベントハンドラーコードに入力します。

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample7.vb)]

このコードを使用して、ブラウザーから default.aspx にアクセスします。 まだログインしていない場合は、ログインページへのリンクが表示されます (図11を参照)。 このリンクをクリックして、サイトにログインします。 手順 3. で見たように、資格情報を入力した後、default.aspx に返されますが、今回はページがようこそを示しています。 メッセージ (図12を参照)。

[匿名でアクセスすると ![[ログイン] リンクが表示されます。](an-overview-of-forms-authentication-vb/_static/image32.png)](an-overview-of-forms-authentication-vb/_static/image31.png)

**図 11**: 匿名でアクセスすると、[ログイン] リンクが表示されます ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image33.png)されます)

[認証されたユーザーを ![に歓迎します。メッセージ](an-overview-of-forms-authentication-vb/_static/image35.png)](an-overview-of-forms-authentication-vb/_static/image34.png)

**図 12**: 認証されたユーザーがようこそを表示する メッセージ ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image36.png)される)

[HttpContext オブジェクト](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)の[user プロパティ](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)を使用して、現在ログオンしているユーザーの id を確認できます。 HttpContext オブジェクトは、現在の要求に関する情報を表します。このオブジェクトは、応答、要求、セッションなどの一般的な ASP.NET オブジェクトのホームです。 User プロパティは、現在の HTTP 要求のセキュリティコンテキストを表し、 [IPrincipal インターフェイス](https://msdn.microsoft.com/library/system.security.principal.iprincipal.aspx)を実装します。

User プロパティは、FormsAuthenticationModule によって設定されます。 具体的には、FormsAuthenticationModule が受信要求でフォーム認証チケットを検出すると、新しい GenericPrincipal オブジェクトを作成し、それを User プロパティに割り当てます。

プリンシパルオブジェクト (GenericPrincipal など) は、ユーザーの id と所属するロールに関する情報を提供します。 IPrincipal インターフェイスは、次の2つのメンバーを定義します。

- [IsInRole (*roleName*)](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole.aspx) -プリンシパルが指定されたロールに属しているかどうかを示すブール値を返すメソッド。
- [Identity](https://msdn.microsoft.com/library/system.security.principal.iprincipal.identity.aspx) - [IIdentity インターフェイス](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx)を実装するオブジェクトを返すプロパティです。 IIdentity インターフェイスは、 [AuthenticationType](https://msdn.microsoft.com/library/system.security.principal.iidentity.authenticationtype.aspx)、 [Isauthenticated](https://msdn.microsoft.com/library/system.security.principal.iidentity.isauthenticated.aspx)、および[Name](https://msdn.microsoft.com/library/system.security.principal.iidentity.name.aspx)という3つのプロパティを定義します。

現在の訪問者の名前を確認するには、次のコードを使用します。

Dim Currentの名前を String = User.Identity.Name として指定します。

フォーム認証を使用する場合、GenericPrincipal の Identity プロパティに対して[FormsIdentity オブジェクト](https://msdn.microsoft.com/library/system.web.security.formsidentity.aspx)が作成されます。 FormsIdentity クラスは、常に AuthenticationType プロパティの文字列形式を返し、IsAuthenticated プロパティの場合は True を返します。 Name プロパティは、フォーム認証チケットを作成するときに指定されたユーザー名を返します。 これら3つのプロパティに加えて、FormsIdentity には、[チケットプロパティ](https://msdn.microsoft.com/library/system.web.security.formsidentity.ticket.aspx)を使用して基になる認証チケットへのアクセスが含まれます。 Ticket プロパティは、種類が[フォーム Authenticationticket](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)のオブジェクトを返します。このオブジェクトには、有効期限、Ispersistent、IssueDate、Name などのプロパティが含まれています。

ここで重要な点は、FormsAuthentication (*username*, *Persistcookie*)、FormsAuthentication (*ユーザー名、* *persistcookie*)、および FormsAuthentication (*username*、 *persistcookie*) の各メソッドに指定されている*username*パラメーターが User.Identity.Name によって返される値と同じであることです。 さらに、これらのメソッドによって作成される認証チケットは、FormsIdentity オブジェクトにユーザー Id をキャストして、Ticket プロパティにアクセスすることによって利用できます。

Dim ident As FormsIdentity = CType(User.Identity, FormsIdentity)

Dim authTicket As フォーム Authenticationticket = ident。チケット

Default.aspx でよりパーソナライズされたメッセージを提供してみましょう。 WelcomeBackMessage ラベルの Text プロパティに "Welcome back, *Username*" という文字列が割り当てられるように、ページ\_読み込みイベントハンドラーを更新します。

WelcomeBackMessage = "Welcome back," &amp; User.Identity.Name &amp; "!"

図13は、この変更の影響を示しています (ユーザー Scott としてログインしている場合)。

[ウェルカムメッセージに、現在ログインしているユーザーの名前が含まれて ![](an-overview-of-forms-authentication-vb/_static/image38.png)](an-overview-of-forms-authentication-vb/_static/image37.png)

**図 13**: ウェルカムメッセージには、現在ログインしているユーザーの名前が含まれます ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image39.png)されます)

### <a name="using-the-loginview-and-loginname-controls"></a>LoginView および Logincontrols の使用

認証されたユーザーと匿名ユーザーに異なるコンテンツを表示することは、一般的な要件です。では、現在ログオンしているユーザーの名前が表示されます。 このため、ASP.NET には、図13と同じ機能を提供する2つの Web コントロールが含まれていますが、1行のコードを記述する必要はありません。

[LoginView コントロール](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx)は、認証されたユーザーと匿名ユーザーに対してさまざまなデータを簡単に表示できるようにする、テンプレートベースの Web コントロールです。 LoginView には、次の2つの定義済みテンプレートが含まれます。

- AnonymousTemplate-このテンプレートに追加されたすべてのマークアップは、匿名の訪問者にのみ表示されます。
- LoggedInTemplate-このテンプレートのマークアップは、認証されたユーザーにのみ表示されます。

ここでは、LoginView コントロールをサイトのマスターページ (.master) に追加します。 ただし、LoginView コントロールだけを追加するのではなく、新しい ContentPlaceHolder コントロールを追加し、その新しい ContentPlaceHolder 内に LoginView コントロールを配置してみましょう。 この決定の根拠は、すぐに明らかになります。

> [!NOTE]
> AnonymousTemplate と LoggedInTemplate に加えて、LoginView コントロールには、ロール固有のテンプレートを含めることができます。 ロール固有のテンプレートは、指定されたロールに属しているユーザーのみにマークアップを表示します。 この後のチュートリアルでは、LoginView コントロールのロールベースの機能について説明します。

まず、LoginContent という名前の ContentPlaceHolder を、ナビゲーション &lt;div&gt; 要素内のマスターページに追加します。 ContentPlaceHolder コントロールをツールボックスからソースビューにドラッグするだけで、結果として得られるマークアップを TODO: Menu のすぐ上に配置することができます。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample8.aspx)]

次に、LoginContent ContentPlaceHolder 内に LoginView コントロールを追加します。 マスターページの ContentPlaceHolder コントロールに配置されたコンテンツは、ContentPlaceHolder の*既定のコンテンツ*と見なされます。 つまり、このマスターページを使用する ASP.NET ページでは、ContentPlaceHolder ごとに独自のコンテンツを指定することも、マスターページの既定のコンテンツを使用することもできます。

LoginView およびその他のログイン関連のコントロールは、ツールボックスの [ログイン] タブにあります。

[ツールボックスの LoginView コントロールの ![](an-overview-of-forms-authentication-vb/_static/image41.png)](an-overview-of-forms-authentication-vb/_static/image40.png)

**図 14**: ツールボックスの LoginView コントロール ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image42.png)されます)

次に、LoginView コントロールの直後に ContentPlaceHolder 内にある2つの &lt;br/&gt; 要素を追加します。 この時点で、ナビゲーション &lt;div&gt; 要素のマークアップは次のようになります。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample9.aspx)]

LoginView のテンプレートは、デザイナーまたは宣言型マークアップから定義できます。 Visual Studio のデザイナーから、LoginView のスマートタグを展開します。このタグには、構成されているテンプレートがドロップダウンリストに表示されます。 「Hello, AnonymousTemplate」というテキストを入力します。次に、HyperLink コントロールを追加し、その Text プロパティと NavigateUrl プロパティをそれぞれ設定します。

AnonymousTemplate を構成した後、LoggedInTemplate に切り替え、"Welcome back" というテキストを入力します。 次に、[ツールボックス] から [LoggedInTemplate] コントロールを [戻る] テキストの直後に配置します。 その名前が示すように、ログイン[コントロール](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginname.aspx)は、現在ログインしているユーザーの名前を表示します。 内部的には、Logincontrol は User.Identity.Name プロパティを単に出力します。

これらを LoginView のテンプレートに追加すると、マークアップは次のようになります。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample10.aspx)]

このマスターページに追加すると、ユーザーが認証されているかどうかに応じて、web サイトの各ページに異なるメッセージが表示されます。 図15は、ブラウザーでユーザー Jisun によってアクセスされたときの default.aspx ページを示しています。 "ようこそ"、"Jisun" メッセージは2回繰り返されます。1回目は、(追加した LoginView コントロールを使用して) 左側にあるマスターページのナビゲーションセクションで、もう1回は default.aspx のコンテンツ領域 (パネルコントロールとプログラムロジックを使用) で1回です。

[LoginView コントロールに ![、[ようこそ]、[Jisun] が表示されます。](an-overview-of-forms-authentication-vb/_static/image44.png)](an-overview-of-forms-authentication-vb/_static/image43.png)

**図 15**: LoginView コントロールには、[ようこそ]、[Jisun] が表示されます。 ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image45.png)される)

LoginView をマスターページに追加したので、サイトのすべてのページに表示できます。 ただし、このメッセージを表示しない web ページが存在する場合があります。 ログインページへのリンクは存在しないと思われるため、このようなページはログインページです。 LoginView コントロールをマスターページの ContentPlaceHolder に配置したため、コンテンツページでこの既定のマークアップをオーバーライドできます。 Login.aspx を開き、デザイナーにアクセスします。 マスターページの LoginContent ContentPlaceHolder に対して login.aspx でコンテンツコントロールが明示的に定義されていないため、ログインページには、この ContentPlaceHolder のマスターページの既定のマークアップが表示されます。 これはデザイナーで確認できます。 LoginContent ContentPlaceHolder は、既定のマークアップ (LoginView コントロール) を示しています。

[![ログインページに、マスターページの LoginContent ContentPlaceHolder の既定のコンテンツが表示されます。](an-overview-of-forms-authentication-vb/_static/image47.png)](an-overview-of-forms-authentication-vb/_static/image46.png)

**図 16**: ログインページには、マスターページの Logincontent ContentPlaceHolder の既定のコンテンツが表示されます ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image48.png)されます)

LoginContent ContentPlaceHolder の既定のマークアップをオーバーライドするには、デザイナーで領域を右クリックし、コンテキストメニューから [カスタムコンテンツの作成] オプションを選択します。 (Visual Studio 2008 を使用している場合、ContentPlaceHolder にはスマートタグが含まれています。このタグを選択すると、同じオプションが提供されます)。これにより、ページのマークアップに新しいコンテンツコントロールが追加され、このページのカスタムコンテンツを定義できるようになります。 ここにカスタムメッセージ (ログインしてみてください) を追加できますが、空白のままにしておきます。

> [!NOTE]
> Visual Studio 2005 では、カスタムコンテンツを作成すると、ASP.NET ページに空のコンテンツコントロールが作成されます。 ただし、Visual Studio 2008 では、カスタムコンテンツを作成すると、マスターページの既定のコンテンツが新しく作成されたコンテンツコントロールにコピーされます。 Visual Studio 2008 を使用している場合は、新しいコンテンツコントロールを作成した後で、マスターページからコピーしたコンテンツをクリアするようにしてください。

図17は、この変更を行った後にブラウザーからアクセスしたときの login.aspx ページを示しています。 Default.aspx にアクセスするときと同じように、左側のナビゲーション &lt;div&gt; には、Hello、*人、また*は歓迎がないことに注意してください。

[ログインページを ![と、既定の LoginContent ContentPlaceHolder のマークアップが非表示になります。](an-overview-of-forms-authentication-vb/_static/image50.png)](an-overview-of-forms-authentication-vb/_static/image49.png)

**図 17**: ログインページで既定の Logincontent ContentPlaceHolder のマークアップが非表示になる ([クリックしてフルサイズの画像を表示する](an-overview-of-forms-authentication-vb/_static/image51.png))

## <a name="step-5-logging-out"></a>手順 5: ログアウト

手順3では、ユーザーをサイトにログインするためのログインページの構築について説明しましたが、ユーザーをログアウトする方法についてはまだ説明していません。FormsAuthentication クラスには、でユーザーをログに記録するメソッドに加えて、[サインアウトメソッド](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)も用意されています。 サインアウトメソッドは、単にフォーム認証チケットを破棄し、その結果、サイトからユーザーをログアウトします。

Log out リンクを提供することは、ユーザーをログアウトするために特別に設計されたコントロールを ASP.NET に含む一般的な機能です。[LoginStatus コントロール](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginstatus.aspx)は、ユーザーの認証状態に応じて、Login linkbutton または Logout linkbutton のいずれかを表示します。 ログイン LinkButton は匿名ユーザーに対してレンダリングされますが、ログアウト LinkButton は認証されたユーザーに表示されます。 Login および Logout LinkButtons のテキストは、LoginStatus の LoginText プロパティと LogoutText プロパティを使用して構成できます。

Login LinkButton をクリックすると、ポストバックが発生し、ログインページにリダイレクトが発行されます。 Logout LinkButton をクリックすると、LoginStatus コントロールは FormsAuthentication メソッドを呼び出し、ページにユーザーをリダイレクトします。 ログオフしたユーザーがリダイレクトされるページは、LogoutAction プロパティによって異なります。このプロパティは、次の3つの値のいずれかに割り当てることができます。

- Refresh-既定値。アクセスしたばかりのページにユーザーをリダイレクトします。 アクセスしたばかりのページで匿名ユーザーが許可されていない場合、FormsAuthenticationModule はユーザーをログインページに自動的にリダイレクトします。

ここでリダイレクトが実行される理由を知りたい場合があります。 ユーザーが同じページにとどまる場合は、明示的なリダイレクトが必要になるのはなぜですか。 その理由は、ログオフ LinkButton がクリックされたときに、ユーザーの cookie コレクションにフォーム認証チケットがまだあるためです。 その結果、ポストバック要求は認証された要求になります。 LoginStatus コントロールはサインアウトメソッドを呼び出しますが、これは FormsAuthenticationModule がユーザーを認証した後に発生します。 したがって、明示的なリダイレクトによって、ブラウザーはページを再要求します。 ブラウザーがページを再要求したときに、フォーム認証チケットが削除されたため、受信要求は匿名になります。

- リダイレクト-ユーザーは、LoginStatus の LogoutPageUrl プロパティによって指定された URL にリダイレクトされます。
- RedirectToLoginPage-ユーザーはログインページにリダイレクトされます。

マスターページに LoginStatus コントロールを追加し、リダイレクトオプションを使用して、サインアウトしたことを確認するメッセージを表示するページにユーザーを送信するように構成してみましょう。まず、Logout という名前のルートディレクトリにページを作成します。 このページを必ず、このページを使用してください。 次に、ページのマークアップに、ログアウトしたことを示すメッセージを入力します。

次に、LoginStatus マスターページに戻り、LoginContent ContentPlaceHolder の LoginView の下に、[] コントロールを追加します。 LoginStatus コントロールの LogoutAction プロパティを Redirect に、LogoutPageUrl プロパティを ~/logoutaction に設定します。

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample11.aspx)]

LoginStatus は LoginView コントロールの外部にあるため、匿名ユーザーと認証済みユーザーの両方に対して表示されますが、これは問題ありません。これは、LoginStatus で Login または Logout LinkButton が正しく表示されるためです。 LoginStatus コントロールを追加すると、AnonymousTemplate のログインハイパーリンクは不要になり、削除されます。

図18は、Jisun がアクセスしたときの default.aspx を示しています。 左の列には、メッセージが表示されます。「ようこそ」と「Jisun」というメッセージが、ログアウト用のリンクと共に表示されます。Log out LinkButton をクリックすると、ポストバックが発生し、システムから Jisun に署名された後、Logout にリダイレクトされます。 図19に示すように、Jisun が Logout に到達すると、既にサインアウトされているため、匿名になります。 その結果、左側の列には、[ようこそ]、[人]、ログインページへのリンクが表示されます。

[default.aspx ![、Logout LinkButton と共に、ようこそ、Jisun、](an-overview-of-forms-authentication-vb/_static/image53.png)](an-overview-of-forms-authentication-vb/_static/image52.png)

**図 18**: default.aspx は、既定では、[ようこそ] が表示され、Logout LinkButton と共に Jisun が表示されます ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image54.png)されます)

[![Logout は Login LinkButton と共に歓迎を表示します](an-overview-of-forms-authentication-vb/_static/image56.png)](an-overview-of-forms-authentication-vb/_static/image55.png)

**図 19**: Logout はログイン LinkButton と共に歓迎を示します ([クリックすると、フルサイズの画像が表示](an-overview-of-forms-authentication-vb/_static/image57.png)されます)

> [!NOTE]
> Logout ページをカスタマイズして、マスターページの LoginContent ContentPlaceHolder を非表示にすることをお勧めします (手順4の login.aspx の場合と同様)。 その理由は、LoginStatus コントロールによってレンダリングされたログイン LinkButton (Hello, こんにちはの下にある) が、ReturnUrl querystring パラメーターの現在の URL を渡してログインページにユーザーを送信するためです。 つまり、ログアウトしたユーザーがこの LoginStatus の Login LinkButton をクリックし、ログインすると、ユーザーが簡単に混乱する可能性がある Logout にリダイレクトされます。

## <a name="summary"></a>まとめ

このチュートリアルでは、フォーム認証ワークフローの調査を開始し、ASP.NET アプリケーションでフォーム認証を実装しました。 フォーム認証は FormsAuthenticationModule を利用しています。これには、フォーム認証チケットに基づいてユーザーを識別し、承認されていないユーザーをログインページにリダイレクトするという2つの役割があります。

.NET Framework の FormsAuthentication クラスには、フォーム認証チケットを作成、検査、および削除するメソッドが含まれています。 要求が認証されているかどうかを判断するための追加のプログラムサポートと、ユーザーの id に関する情報が提供されます。 また、LoginView、LoginStatus、および Loginweb コントロールもあります。これにより、開発者は、多くの一般的なログイン関連タスクを簡単に、コードを自由に実行できるようになります。 今後のチュートリアルでは、これらおよび他のログイン関連 Web コントロールについてさらに詳しく説明します。

このチュートリアルでは、フォーム認証の概要を大まかに説明しました。 さまざまな構成オプションについては説明しませんでした。クッキーレスフォーム認証チケットがどのように機能するかを確認するか、ASP.NET がフォーム認証チケットの内容を保護する方法を調べてください。 これらのトピックについては、[次のチュートリアル](forms-authentication-configuration-and-advanced-topics-vb.md)で説明します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [IIS6 と IIS7 のセキュリティ間の変更](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [Login ASP.NET コントロール](https://msdn.microsoft.com/library/d51ttbhx.aspx)
- [Professional ASP.NET 2.0 のセキュリティ、メンバーシップ、およびロール管理](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html)(ISBN: 978-0-7645-9698-8)
- [&lt;authentication&gt; 要素](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;認証用の &lt;フォーム&gt; 要素&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>このチュートリアルに含まれるトピックのビデオトレーニング

- [ASP.NET で基本フォーム認証を使用する](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者には、Alicja Maziarz、John 加藤 u、Teresa Murphy が含まれています。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](security-basics-and-asp-net-support-vb.md)
> [次へ](forms-authentication-configuration-and-advanced-topics-vb.md)

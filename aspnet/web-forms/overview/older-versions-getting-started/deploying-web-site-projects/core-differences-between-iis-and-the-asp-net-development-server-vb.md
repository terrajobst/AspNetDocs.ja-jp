---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-vb
title: IIS と ASP.NET 開発サーバーの主な相違点 (VB) |Microsoft Docs
author: rick-anderson
description: ASP.NET アプリケーションをローカルでテストする場合、ASP.NET Development Web サーバーを使用している可能性があります。 ただし、実稼働 web サイトはおそらく pow...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 090e9205-52f3-4d72-ae31-44775b8b8421
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-vb
msc.type: authoredcontent
ms.openlocfilehash: 880bb403e671446a77d7eebccf578a1dc714d1f9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586523"
---
# <a name="core-differences-between-iis-and-the-aspnet-development-server-vb"></a>IIS と ASP.NET 開発サーバーの間の中心的違い (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_06_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial06_WebServerDiff_vb.pdf)

> ASP.NET アプリケーションをローカルでテストする場合、ASP.NET Development Web サーバーを使用している可能性があります。 ただし、運用 web サイトは、最も多くの場合、IIS を利用しています。 これらの web サーバーが要求を処理する方法にはいくつかの違いがあり、これらの違いによって重要な結果が得られる可能性があります。 このチュートリアルでは、連動のさまざまな相違点について説明します。

## <a name="introduction"></a>はじめに

ユーザーが ASP.NET アプリケーションにアクセスするたびに、ブラウザーは web サイトに要求を送信します。 この要求は web サーバーソフトウェアによって取得され、要求されたリソースのコンテンツを生成して返すように ASP.NET ランタイムと連携します。 [**I** n **i**は、( IIS)](http://en.wikipedia.org/wiki/Internet_Information_Services)は、Windows サーバーに共通のインターネットベースの機能を提供する一連のサービスです。 IIS は、運用環境で ASP.NET アプリケーションを実行するために最も一般的に使用される web サーバーです。ほとんどの場合、web ホストプロバイダーが ASP.NET アプリケーションを提供するために使用している web サーバーソフトウェアです。 Iis は、IIS をインストールして適切に構成する必要がありますが、開発環境で web サーバーソフトウェアとして使用することもできます。

ASP.NET 開発サーバーは、開発環境用の別の web サーバーオプションです。に付属しており、Visual Studio に統合されています。 IIS を使用するように web アプリケーションが構成されていない限り、Visual Studio 内から web ページに初めてアクセスしたときに、ASP.NET 開発サーバーが自動的に開始され、web サーバーとして使用されます。 「[*配置する必要があるファイルの決定*](determining-what-files-need-to-be-deployed-vb.md)」で作成したデモ web アプリケーションは、IIS を使用するように構成されていないファイルシステムベースの web アプリケーションです。 このため、Visual Studio 内からこれらの web サイトのいずれかを閲覧すると、ASP.NET 開発サーバーが使用されます。

完璧な世界では、開発環境と運用環境は同じになります。 ただし、前のチュートリアルで説明したように、環境に異なる構成設定があることは珍しくありません。 環境内で異なる web サーバーソフトウェアを使用すると、アプリケーションを展開するときに考慮する必要がある別の変数が追加されます。 このチュートリアルでは、IIS と ASP.NET 開発サーバーの主な違いについて説明します。 これらの違いにより、開発環境で問題が発生したコードが例外をスローしたり、運用環境で実行されたときに動作が異なる場合があります。

## <a name="security-context-differences"></a>セキュリティコンテキストの違い

Web サーバーソフトウェアが受信要求を処理するたびに、その要求が特定のセキュリティコンテキストに関連付けられます。 このセキュリティコンテキスト情報は、要求で許容されるアクションを決定するためにオペレーティングシステムによって使用されます。 たとえば、ASP.NET ページには、ディスク上のファイルにメッセージを記録するコードが含まれている場合があります。 この ASP.NET ページがエラーなしで実行されるようにするには、セキュリティコンテキストにファイルシステムレベルの適切なアクセス許可、つまりそのファイルに対する書き込みアクセス許可が必要です。

ASP.NET 開発サーバーは、現在ログオンしているユーザーのセキュリティコンテキストに着信要求を関連付けます。 管理者としてデスクトップにログオンしている場合、ASP.NET 開発サーバーによって提供される ASP.NET ページには、管理者と同じアクセス権が与えられます。 ただし、IIS によって処理される ASP.NET 要求は、特定のコンピューターアカウントに関連付けられています。 既定では、ネットワークサービスコンピューターアカウントは IIS バージョン6および7によって使用されます。ただし、web ホストプロバイダーでは、顧客ごとに一意のアカウントが構成されている場合があります。 さらに、web ホストプロバイダーには、このコンピューターアカウントに対する制限されたアクセス許可が与えられる可能性があります。 結果として、開発環境ではエラーなしで実行される web ページが存在する可能性がありますが、運用環境でホストされている場合は承認関連の例外が生成されます。

この種のエラーを表示するには、書籍のレビュー web サイトにページを作成して、最新の日時を格納するファイルをディスク上に作成します。これにより、 *ASP.NET は24時間のレビューで 3.5*が表示されます。 先に進むには、[`~/Tech/TYASP35.aspx`] ページを開き、次のコードを `Page_Load` イベントハンドラーに追加します。

[!code-vb[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample1.vb)]

> [!NOTE]
> [`File.WriteAllText` メソッド](https://msdn.microsoft.com/library/system.io.file.writealltext.aspx)は、新しいファイルが存在しない場合は作成し、指定された内容をそのファイルに書き込みます。 ファイルが既に存在する場合は、既存の内容が上書きされます。

次に、ASP.NET 開発サーバーを使用して、開発環境の [ *ASP.NET 3.5 In the 24 Hours* book review] \ (24 時間の自己学習 \) ページにアクセスします。 Web アプリケーションのルートディレクトリ内のテキストファイルを作成および変更するための適切なアクセス許可を持つアカウントを使用してコンピューターにログオンしていると仮定した場合、ブックのレビューは以前と同じように見えますが、ページに日付と時刻が表示されるたびに、ユーザーの IP アドレスが `LastTYASP35Access.txt` ファイルに格納されます。 ブラウザーでこのファイルを参照します。図1に示すようなメッセージが表示されます。

[このテキストファイルには、ブックのレビューが最後に閲覧された日時が含まれて ![&lt;](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image2.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image1.png)

**図 1**: このテキストファイルには、ブックのレビューが最後に閲覧された日時が含まれています ([クリックすると、フルサイズの画像が表示](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image3.png)されます)

Web アプリケーションを運用環境にデプロイした後、 *24 時間の*書籍のレビューページで、ホストされている ASP.NET 3.5 にアクセスします。 この時点で、[book review] ページが通常として表示されるか、図2のようなエラーメッセージが表示されます。 一部の web ホストプロバイダーは、匿名 ASP.NET コンピューターアカウントに書き込みアクセス許可を付与します。この場合、ページはエラーなしで動作します。 ただし、web ホストプロバイダーが匿名アカウントへの書き込みアクセスを禁止している場合は、`TYASP35.aspx` ページが `LastTYASP35Access.txt` ファイルに現在の日付と時刻を書き込もうとしたときに、 [`UnauthorizedAccessException` 例外](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx)が発生します。

[IIS によって使用される既定のコンピューターアカウントに、ファイルシステムへの書き込みアクセス許可がない ![](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image5.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image4.png)

**図 2**: IIS で使用される既定のコンピューターアカウントに、ファイルシステムへの書き込みアクセス許可がない ([クリックしてフルサイズのイメージを表示する](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image6.png))

ほとんどの web ホストプロバイダーには、web サイトでファイルシステムのアクセス許可を指定できるようにするアクセス許可ツールがいくつか用意されています。 ルートディレクトリへの書き込みアクセス権を匿名 ASP.NET アカウントに付与してから、[book review] ページに戻ります。 (必要に応じて、既定の ASP.NET アカウントに書き込みアクセス許可を付与する方法については、web ホストプロバイダーに問い合わせてください。)今回は、ページがエラーなしで読み込まれ、`LastTYASP35Access.txt` ファイルが正常に作成されます。

ここでは、ASP.NET 開発サーバーが IIS とは異なるセキュリティコンテキストで動作するため、ファイルシステムに対して読み取りまたは書き込みを行う ASP.NET ページ、Windows イベントログの読み取りまたは書き込み、または Windows への読み取りまたは書き込みを行うことができます。 レジストリは開発時に予想どおりに機能しますが、運用時には例外を生成します。 共有 web ホスティング環境に配置される web アプリケーションを構築する場合は、イベントログまたは Windows レジストリに対して読み取りまたは書き込みを行わないでください。 また、運用環境の適切なフォルダーに対する読み取り権限と書き込み権限を付与する必要がある場合があるため、ファイルシステムに対して読み取りまたは書き込みを行うすべての ASP.NET ページをメモしておきます。

## <a name="differences-on-serving-static-content"></a>静的コンテンツの提供に関する相違点

IIS と ASP.NET 開発サーバーにおけるもう1つの重要な違いは、静的コンテンツの要求を処理する方法です。 ASP.NET 開発サーバーに含まれるすべての要求は、ASP.NET ページ、イメージ、または JavaScript ファイルのいずれであるかにかかわらず、ASP.NET ランタイムによって処理されます。 既定では、ASP.NET リソース (ASP.NET web ページ、Web サービスなど) に対して要求が送られた場合にのみ、IIS は ASP.NET ランタイムを呼び出します。 静的コンテンツ (画像、CSS ファイル、JavaScript ファイル、PDF ファイル、ZIP ファイルなど) の要求は、ASP.NET ランタイムを介さずに IIS によって取得されます。 (静的コンテンツを提供する場合は、ASP.NET ランタイムで動作するように IIS に指示することができます。詳細については、このチュートリアルの「IIS 7 を使用した静的ファイルでのフォームベース認証と URL 認証の実行」を参照してください)。

ASP.NET ランタイムは、要求されたコンテンツを生成するためのいくつかの手順を実行します。これには、認証 (要求元の識別) と承認 (要求されたコンテンツを表示するアクセス許可が要求元にあるかどうかの確認) が含まれます。 一般的な形式の認証は、*フォームベースの認証*です。この認証では、資格情報を入力してユーザーを識別します。通常は、web ページ上のテキストボックスにユーザー名とパスワードを入力します。 資格情報を検証すると、web サイトはユーザーのブラウザーに*認証チケット*cookie を保存します。これは、web サイトへの後続のすべての要求と共に送信され、ユーザーの認証に使用されます。 さらに、ユーザーが特定のフォルダーにアクセスできるかどうかを指定する*URL 承認*規則を指定することもできます。 多くの ASP.NET websites は、フォームベースの認証と URL 承認を使用してユーザーアカウントをサポートし、特定のロールに属している認証済みのユーザーまたはユーザーのみがアクセスできるサイトの一部を定義します。

> [!NOTE]
> ASP の詳細な調査を行う場合。ネットワークのフォームベース認証、URL 認証、およびその他のユーザーアカウント関連機能については、「 [Web サイトのセキュリティ](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)に関するチュートリアル」をご覧ください。

フォームベースの承認を使用するユーザーアカウントをサポートする web サイトがあり、URL 承認を使用するフォルダーがあり、認証されたユーザーのみを許可するように構成されているとします。 このフォルダーには、ASP.NET ページと PDF ファイルが含まれており、認証されたユーザーのみがこれらの PDF ファイルを表示できることを意図しています。

ビジターがブラウザーのアドレスバーに直接 URL を入力して、これらの PDF ファイルの1つを表示しようとするとどうなりますか。 まず、書籍のレビューサイトに新しいフォルダーを作成して PDF ファイルを追加し、匿名ユーザーがこのフォルダーにアクセスできないように URL 認証を使用するようにサイトを構成します。 デモアプリケーションをダウンロードすると、`PrivateDocs` という名前のフォルダーが作成され、 [Web サイトのセキュリティチュートリアル](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)(「方法」) から PDF が追加されたことがわかります。 `PrivateDocs` フォルダーには、匿名ユーザーを拒否する URL 承認規則を指定する `Web.config` ファイルも含まれています。

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample2.xml)]

最後に、ルートディレクトリの web.config ファイルを更新することによって、フォームベースの認証を使用するように web アプリケーションを構成しました。これは、次のように置き換えます。

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample3.xml)]

この文を、次の文に置き換えます。

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample4.xml)]

ASP.NET 開発サーバーを使用して、サイトにアクセスし、ブラウザーのアドレスバーにある PDF ファイルの1つに直接 URL を入力します。 このチュートリアルに関連付けられている web サイトをダウンロードした場合、URL は次のようになります: `http://localhost:portNumber/PrivateDocs/aspnet_tutorial01_Basics_vb.pdf`

この URL をアドレスバーに入力すると、ブラウザーはファイルの ASP.NET 開発サーバーに要求を送信します。 ASP.NET 開発サーバーは、ASP.NET ランタイムに要求を渡して処理を行います。 まだログインしていないため、`PrivateDocs` フォルダー内の `Web.config` は匿名アクセスを拒否するように構成されているため、ASP.NET ランタイムはログイン `Login.aspx` ページに自動的にリダイレクトします (図3を参照)。 ユーザーをログインページにリダイレクトする場合、ASP.NET には、ユーザーが表示しようとしていたページを示す `ReturnUrl` querystring パラメーターが含まれています。 正常にログインした後、ユーザーはこのページに戻ることができます。

[承認されていないユーザーがログインページに自動的にリダイレクト ![](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image8.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image7.png)

**図 3**: 許可されていないユーザーがログインページに自動的にリダイレクトされる ([クリックしてフルサイズの画像を表示する](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image9.png))

次に、この動作が運用環境でどのように動作するかを見てみましょう。 アプリケーションをデプロイし、運用環境の `PrivateDocs` フォルダー内のいずれかの Pdf に直接 URL を入力します。 これにより、ブラウザーでファイルの要求 IIS を送信するように求められます。 静的ファイルが要求されるため、IIS は ASP.NET ランタイムを呼び出さずにファイルを取得して返します。 その結果、URL 承認チェックは実行されませんでした。このプライベート PDF の内容は、ファイルへの直接 URL を知っているすべてのユーザーがアクセスできます。

[匿名ユーザーは、ファイルへの直接 URL を入力することによって、プライベート PDF ファイルをダウンロード ![ます。](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image11.png)](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image10.png)

**図 4**: 匿名ユーザーは、ファイルへの直接 URL を入力してプライベート PDF ファイルをダウンロードできます ([クリックすると、フルサイズの画像が表示](core-differences-between-iis-and-the-asp-net-development-server-vb/_static/image12.png)されます)。

### <a name="performing-forms-based-authentication-and-url-authentication-on-static-files-with-iis-7"></a>IIS 7 を使用した静的ファイルでのフォームベース認証と URL 認証の実行

承認されていないユーザーから静的コンテンツを保護するには、いくつかの手法を使用できます。 IIS 7 では、統合された*パイプライン*が導入されました。これにより、iis のワークフローが ASP.NET ランタイムのワークフローと共に使用されます。 簡単に言うと、ASP.NET ランタイムの認証および承認モジュールがすべての受信要求 (PDF ファイルなどの静的コンテンツを含む) を呼び出すように IIS に指示できます。 Web ホストプロバイダーに問い合わせて、統合パイプラインを使用するように web サイトを構成する方法を確認してください。

統合パイプラインを使用するように IIS を構成したら、次のマークアップをルートディレクトリの `Web.config` ファイルに追加します。

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-vb/samples/sample5.xml)]

このマークアップは、ASP.NET ベースの認証および承認モジュールを使用するように IIS 7 に指示します。 アプリケーションを再配置し、PDF ファイルに再度アクセスします。 このとき、IIS が要求を処理するときに、ASP.NET ランタイムの認証と承認ロジックに要求を検査する機会が与えられます。 認証されたユーザーのみが `PrivateDocs` フォルダーの内容を表示する権限を持っているため、匿名ビジターは自動的にログインページにリダイレクトされます (図3を参照)。

> [!NOTE]
> Web ホストプロバイダーがまだ IIS 6 を使用している場合は、統合パイプライン機能を使用できません。 回避策の1つは、HTTP アクセスを禁止するフォルダー (`App_Data`など) にプライベートドキュメントを配置し、これらのドキュメントを提供するページを作成することです。 このページは `GetPDF.aspx`と呼ばれる場合があります。また、クエリ文字列パラメーターを使用して PDF の名前が渡されます。 `GetPDF.aspx` のページでは、まず、ユーザーがファイルを表示するアクセス許可を持っていることを確認し、存在する場合は、 [`Response.WriteFile(filePath)`](https://msdn.microsoft.com/library/system.web.httpresponse.writefile.aspx)メソッドを使用して、要求された PDF ファイルの内容を要求元のクライアントに送り返します。 この手法は、統合パイプラインを有効にしたくない場合に、IIS 7 でも機能します。

## <a name="summary"></a>要約

運用環境の web アプリケーションは、Microsoft の IIS web サーバーソフトウェアを使用してホストされます。 ただし、開発環境では、アプリケーションは IIS または ASP.NET 開発サーバーを使用してホストされる場合があります。 異なるソフトウェアを使用すると、混合に別の変数が追加されるため、同じ web サーバーソフトウェアを両方の環境で使用するのが理想的です。 ただし、ASP.NET 開発サーバーを使いやすくすることで、開発環境での選択が魅力的になります。 IIS と ASP.NET 開発サーバーにはいくつかの基本的な違いがありますが、これらの違いを認識している場合は、アプリケーションの動作と機能に関係なく同じ方法で動作し、機能するようにするための対策を講じることができます。environment.

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET と IIS 7.0 の統合](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)
- [IIS 7 のすべての種類のコンテンツで ASP.NET フォーラム認証を使用する](https://blogs.iis.net/bills/archive/2007/05/19/using-asp-net-forms-authentication-with-all-types-of-content-with-iis7-video.aspx)(ビデオ)
- [Visual Web Developer の web サーバー](https://msdn.microsoft.com/library/58wxa9w5.aspx)

> [!div class="step-by-step"]
> [前へ](common-configuration-differences-between-development-and-production-vb.md)
> [次へ](deploying-a-database-vb.md)

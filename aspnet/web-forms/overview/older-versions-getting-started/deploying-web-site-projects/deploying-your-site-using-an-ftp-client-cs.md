---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-cs
title: FTP クライアントを使用してサイトをC#展開する () |Microsoft Docs
author: rick-anderson
description: ASP.NET アプリケーションを配置する最も簡単な方法は、開発環境から運用環境に必要なファイルを手動でコピーすることです。 Thi...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: a3599cf7-8474-4006-954a-3bc693736b66
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-cs
msc.type: authoredcontent
ms.openlocfilehash: a3474650939ee220b3fd712e9f5a6cf3db11db09
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621137"
---
# <a name="deploying-your-site-using-an-ftp-client-c"></a>FTP クライアントを使用してサイトを配置する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_03_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial03_DeployingViaFTP_cs.pdf)

> ASP.NET アプリケーションを配置する最も簡単な方法は、開発環境から運用環境に必要なファイルを手動でコピーすることです。 このチュートリアルでは、FTP クライアントを使用してデスクトップから web ホストプロバイダーにファイルを取得する方法について説明します。

## <a name="introduction"></a>はじめに

前のチュートリアルでは、単純な Book Review ASP.NET web アプリケーションを導入しました。これは、いくつかの ASP.NET ページ、マスターページ、カスタム基本 `Page` クラス、多数のイメージ、3つの CSS スタイルシートで構成されています。 これで、このアプリケーションを web ホストプロバイダーにデプロイする準備が整いました。この時点で、インターネットに接続しているすべてのユーザーがアプリケーションにアクセスできるようになります。

「[*デプロイする必要があるファイルの決定*](determining-what-files-need-to-be-deployed-cs.md)」のチュートリアルでは、web ホストプロバイダーにどのファイルをコピーする必要があるかを説明します。 (コピーされるファイルは、アプリケーションが明示的にコンパイルされているか自動的にコンパイルされているかによって異なります)。しかし、運用環境 (web ホストプロバイダーによって管理される web サーバー) までの開発環境 (デスクトップ) からファイルを取得するにはどうすればよいでしょうか。 [ **F**ファイル**T** ransfer **P** rotocol (FTP)](http://en.wikipedia.org/wiki/File_Transfer_Protocol)は、ネットワーク経由でコンピューター間でファイルをコピーするために一般的に使用されるプロトコルです。 もう1つのオプションは FrontPage Server Extensions (FPSE) です。 このチュートリアルでは、スタンドアロン FTP クライアントソフトウェアを使用して、開発環境から運用環境に必要なファイルを展開する方法について説明します。

> [!NOTE]
> Visual Studio には、FTP 経由で web サイトを公開するためのツールが含まれています。これらのツール、および FPSE を使用するツールについては、次のチュートリアルで説明します。

FTP を使用してファイルをコピーするには、開発環境で*ftp クライアント*が必要です。 FTP クライアントは、インストールされているコンピューターから*ftp サーバー*を実行しているコンピューターにファイルをコピーするように設計されたアプリケーションです。 (Web ホストプロバイダーで FTP を使用したファイル転送がサポートされている場合は、web サーバーで FTP サーバーが実行されています)。多数の FTP クライアントアプリケーションを使用できます。 Web ブラウザーは FTP クライアントとしても二重に使用できます。 お気に入りの FTP クライアントと、このチュートリアルで使用するものは、 [FileZilla](http://filezilla-project.org/)であり、Windows、Linux、および mac で利用できる無料のオープンソースの ftp クライアントです。 ただし、すべての FTP クライアントは動作します。そのため、最も使いやすいクライアントを自由に使用できます。

このチュートリアルを実行する前に、web ホストプロバイダーでアカウントを作成しておく必要があります。 前のチュートリアルで説明したように、gaggle の web ホストプロバイダー企業は、さまざまな価格、機能、サービス品質を備えています。 このチュートリアルシリーズでは、web ホストプロバイダーとして[ディスカウント ASP.NET](http://discountasp.net)を使用しますが、サイトが開発されている ASP.NET バージョンがサポートされていれば、どの web ホストプロバイダーでも従うことができます。 (これらのチュートリアルは、ASP.NET 3.5 を使用して作成されています)。また、このチュートリアルでは FTP を使用して web ホストプロバイダーにファイルをコピーするため、今後は web ホストプロバイダーが web サーバーへの FTP アクセスをサポートしている必要があります。 ほぼすべての web ホストプロバイダーがこの機能を提供しますが、サインアップする前に再確認する必要があります。

## <a name="deploying-the-book-review-web-application-project"></a>Book Review Web アプリケーションプロジェクトの配置

書籍レビュー web アプリケーションの2つのバージョンがあることを思い出してください。1つは Web アプリケーションプロジェクトモデル (BookReviewsWAP) を使用して実装され、もう1つは Web サイトプロジェクトモデル (BookReviewsWSP) を使用します。 このプロジェクトの種類は、サイトが自動または明示的にコンパイルされているかどうかに影響し、そのコンパイルモデルによって配置する必要があるファイルが決まります。 そのため、BookReviewsWAP プロジェクトと BookReviewsWSP プロジェクトを個別にデプロイし、BookReviewsWAP から開始します。 まだ行っていない場合は、この2つの ASP.NET アプリケーションをダウンロードしてください。

`BookReviewsWAP` フォルダーに移動し、`BookReviewsWAP.sln` ファイルをダブルクリックして、BookReviewsWAP プロジェクトを起動します。 プロジェクトを配置する前に、プロジェクトをビルドして、ソースコードに対する変更がコンパイル済みアセンブリに含まれていることを確認することが重要です。 プロジェクトをビルドするには、[ビルド] メニューの [BookReviewsWAP のビルド] をクリックします。 これにより、プロジェクト内のソースコードが1つのアセンブリ `BookReviewsWAP.dll`にコンパイルされ、`Bin` フォルダーに配置されます。

これで、必要なファイルをデプロイする準備ができました。 FTP クライアントを起動し、web ホストプロバイダーの web サーバーに接続します。 (Web ホスティング会社にサインアップすると、FTP サーバーへの接続方法に関する情報が電子メールで送信されます。これには、FTP サーバーのアドレスだけでなく、ユーザー名とパスワードも含まれます)。

次のファイルをデスクトップから web ホストプロバイダーのルート web サイトフォルダーにコピーします。 Web ホストプロバイダーで web サーバーに FTP を行うと、ルート web サイトのディレクトリになる可能性が高くなります。 ただし、一部の web ホストプロバイダーには、web サイトファイルのルートフォルダーとして機能する `www` または `wwwroot` という名前のサブフォルダーがあります。 最後に、ファイルに対して FTPing を実行するときに、運用環境 (`Bin` フォルダー、`Fiction` フォルダー、`Images` フォルダーなど) に対応するフォルダー構造を作成することが必要になる場合があります。

- `~/Default.aspx`
- `~/About.aspx`
- `~/Site.master`
- `~/Web.config`
- `~/Web.sitemap`
- `Styles` フォルダーの完全な内容
- `Images` フォルダーの完全な内容 (およびそのサブフォルダー、`BookCovers`)
- `~/Fiction/Default.aspx`
- `~/Fiction/Blaze.aspx`
- `~/Tech/Default.aspx`
- `~/Tech/CYOW.aspx`
- `~/Tech/TYASP35.aspx`
- `~/Bin/BookReviewsWAP.dll`

図1は、必要なファイルがコピーされた後の FileZilla を示しています。 FileZilla は、左側のローカルコンピューター上のファイルと、右側のリモートコンピューター上のファイルを表示します。 図1に示すように、`About.aspx.cs`などの ASP.NET ソースコードファイルはローカルコンピューター (開発環境) 上にありますが、明示的なコンパイルを使用するときにコードファイルを配置する必要がないため、web ホストプロバイダー (運用環境) にコピーされませんでした。

> [!NOTE]
> ソースコードファイルが運用サーバーに存在しても、無視されるため、問題はありません。 ASP.NET は、ソースコードファイルが実稼働サーバー上に存在する場合でも、web サイトの訪問者がアクセスできないように、ソースコードファイルに対する HTTP 要求を既定では禁止します。 (つまり、ユーザーが `http://www.yoursite.com/Default.aspx.cs` にアクセスしようとすると、これらの種類のファイル `.cs` ファイルが禁止されていることを説明するエラーページが表示されます)。

[FTP クライアントを使用して、必要なファイルをデスクトップから Web ホストプロバイダーの Web サーバーにコピー ![](deploying-your-site-using-an-ftp-client-cs/_static/image2.png)](deploying-your-site-using-an-ftp-client-cs/_static/image1.png)

**図 1**: FTP クライアントを使用して、必要なファイルをデスクトップから Web ホストプロバイダーの web サーバーにコピーする ([クリックすると、フルサイズの画像が表示](deploying-your-site-using-an-ftp-client-cs/_static/image3.png)されます)

サイトをデプロイしたら、しばらく時間をおいてサイトをテストしてください。 ドメイン名を購入し、DNS 設定を適切に構成した場合は、ドメイン名を入力してサイトにアクセスできます。 または、web ホストプロバイダーからサイトの URL を指定する必要があります。これは*accountname*のようになります。*webhostprovider*.com または*webhostprovider*.com/*accountname*。 たとえば、割引 ASP.NET のアカウントの URL は次のようになります。 `http://httpruntime.web703.discountasp.net`。

図2は、デプロイされた書籍レビューサイトを示しています。 これは、割引 ASP で表示されていることに注意してください。NET のサーバー (`http://httpruntime.web703.discountasp.net`)。 この時点で、インターネットに接続しているすべてのユーザーが自分の web サイトを表示できます。 予想したとおり、サイトは、開発環境でテストする場合と同じように表示および動作します。

> [!NOTE]
> アプリケーションの表示中にエラーが発生した場合は、正しいファイルセットを展開したことを確認するためにしばらく時間がかかります。 次に、エラーメッセージを調べて、問題に関する手掛かりが表示されているかどうかを確認します。 その後、web ホスト会社のヘルプデスクに連絡するか、 [ASP.NET フォーラム](https://forums.asp.net/)で適切なフォーラムに質問を投稿することができます。

[ブックのレビューサイトにインターネット接続を使用しているユーザーがアクセスできるようになり ![](deploying-your-site-using-an-ftp-client-cs/_static/image5.png)](deploying-your-site-using-an-ftp-client-cs/_static/image4.png)

**図 2**: 書籍のレビューサイトにインターネット接続を使用しているすべてのユーザーがアクセスできるようになりました ([クリックしてフルサイズの画像を表示](deploying-your-site-using-an-ftp-client-cs/_static/image6.png))

## <a name="deploying-the-book-review-web-site-project"></a>書籍レビュー Web サイトプロジェクトを展開する

BookReviewsWSP Web サイトプロジェクトなどの自動コンパイルを使用する ASP.NET アプリケーションを配置する場合、`Bin` フォルダーにコンパイル済みのアセンブリはありません。 そのため、web アプリケーションのソースコードファイルを運用環境に配置する必要があります。 では、このプロセスについて説明します。

Web アプリケーションプロジェクトと同様に、最初にアプリケーションを配置する前にビルドすることをお勧めします。 Web サイトプロジェクトをビルドしてもアセンブリは作成されませんが、ページにコンパイル時エラーがあるかどうかがチェックされます。 これらのエラーは、サイトへの訪問者によって検出されるのではなく、今すぐに見つけることをお勧めします。

プロジェクトが正常にビルドされたら、FTP クライアントを使用して、web ホストプロバイダーのルート web サイトフォルダーに次のファイルをコピーします。 場合によっては、運用環境で対応するフォルダー構造を作成する必要があります。

> [!NOTE]
> BookReviewsWAP プロジェクトを既に展開している場合でも、BookReviewsWSP プロジェクトを配置しようとする場合は、まず BookReviewsWAP を展開するときにアップロードされた web サーバー上のすべてのファイルを削除し、次に BookReviewsWSP のファイルを配置します。

- `~/Default.aspx`
- `~/Default.aspx.cs`
- `~/About.aspx`
- `~/About.aspx.cs`
- `~/Site.master`
- `~/Site.master.cs`
- `~/Web.config`
- `~/Web.sitemap`
- `Styles` フォルダーの完全な内容
- `Images` フォルダーの完全な内容 (およびそのサブフォルダー、`BookCovers`)
- `~/App_Code/BasePage.cs`
- `~/Fiction/Default.aspx`
- `~/Fiction/Default.aspx.cs`
- `~/Fiction/Blaze.aspx`
- `~/Fiction/Blaze.aspx.cs`
- `~/Tech/Default.aspx`
- `~/Tech/Default.aspx.cs`
- `~/Tech/CYOW.aspx`
- `~/Tech/CYOW.aspx.cs`
- `~/Tech/TYASP35.aspx`
- `~/Tech/TYASP35.aspx.cs`

図3は、必要なファイルをコピーした後の FileZilla を示しています。 ご覧のように、`About.aspx.cs`などの ASP.NET ソースコードファイルは、自動コンパイルを使用するときにコードファイルを配置する必要があるため、ローカルコンピューター (開発環境) と web ホストプロバイダー (運用環境) の両方に存在します。

[FTP クライアントを使用して、必要なファイルをデスクトップから Web ホストプロバイダーの Web サーバーにコピー ![](deploying-your-site-using-an-ftp-client-cs/_static/image8.png)](deploying-your-site-using-an-ftp-client-cs/_static/image7.png)

**図 3**: FTP クライアントを使用して、必要なファイルをデスクトップから Web ホストプロバイダーの web サーバーにコピーする ([クリックすると、フルサイズの画像が表示](deploying-your-site-using-an-ftp-client-cs/_static/image9.png)されます)

ユーザーエクスペリエンスは、アプリケーションのコンパイルモデルの影響を受けません。 同じ ASP.NET ページにアクセスでき、Web サイトが Web アプリケーションプロジェクトモデルと Web サイトプロジェクトモデルのどちらを使用して作成されたかにかかわらず、同じ外観と動作が表示されます。

### <a name="updating-a-web-application-on-production"></a>運用環境での Web アプリケーションの更新

Web アプリケーションの開発と配置は、1回限りのプロセスではありません。 たとえば、Book Review web サイトを作成するときに、さまざまなページを作成し、そのコードをパーソナルコンピューター (開発環境) に記述しました。 特定の安定した状態に達した後、他のユーザーがサイトにアクセスしてレビューを読むことができるように、アプリケーションをデプロイしました。 しかし、デプロイでは、このサイトでの開発の終了がマークされていません。 書籍のレビューを追加したり、新しい機能を実装したりすることがあります。たとえば、訪問者が書籍を評価したり、自分のコメントを残したりすることができます。 このような機能強化は開発環境で開発され、完了したらデプロイする必要があります。 このため、開発とデプロイは循環しています。 アプリケーションを開発してから展開します。 サイトが稼働していて、運用環境では、新しい機能が追加され、バグは時間の経過と共に修正されるため、アプリケーションを再デプロイすることができます。 などです。

ご想像のとおり、web アプリケーションを再配置する場合は、新しいファイルと変更されたファイルのみをコピーする必要があります。 変更されていないページまたはサーバーまたはクライアント側のサポートファイルを再配置する必要はありません (ただし、このような問題はありません)。

> [!NOTE]
> 明示的なコンパイルを使用する場合は、プロジェクトに新しい ASP.NET ページを追加したり、コードに関連する変更を加えたりするたびに、プロジェクトをリビルドする必要があります。これにより、`Bin` フォルダー内のアセンブリが更新されます。 そのため、運用環境で web アプリケーションを更新する場合は、この更新されたアセンブリを運用環境にコピーする必要があります (その他の新規および更新されたコンテンツと共に)。

また、`Bin` ディレクトリ内の `Web.config` またはファイルに対する変更によって、web サイトのアプリケーションプールが停止し、再起動されることも理解しておいてください。 セッション状態が `InProc` モード (既定値) を使用して格納されている場合、これらのキーファイルが変更されるたびに、サイトの訪問者がセッション状態を失うことになります。 この落とし穴を回避するには、`StateServer` または `SQLServer` モードを使用してセッションを保存することを検討してください。 このトピックの詳細については[、「セッション状態モード](https://msdn.microsoft.com/library/ms178586.aspx)の読み取り」を参照してください。

最後に、運用環境にコピーする必要があるファイルの数とサイズによっては、アプリケーションの再デプロイに数秒から数分かかる場合があることに注意してください。 この期間中、サイトにアクセスしているユーザーには、エラーまたは異常な動作が発生する可能性があります。 アプリケーション全体を "オフ" にするには、アプリケーションのルートディレクトリに `App_Offline.htm` という名前のページを追加します。これにより、サイトがメンテナンスのためにダウンしていることをユーザーに説明すると共に、すぐにバックアップが実行されます。 `App_Offline.htm` ファイルが存在する場合、ASP.NET ランタイムはすべての受信要求をそのページにリダイレクトします。

## <a name="summary"></a>要約

Web アプリケーションを配置するには、開発環境から運用環境に必要なファイルをコピーする必要があります。 ネットワーク経由でファイルを転送する最も一般的な方法はファイル転送プロトコル (FTP) であり、ほとんどの web ホストプロバイダーは web サーバーへの FTP アクセスをサポートしています。 このチュートリアルでは、FTP クライアントを使用して、必要なファイルを web サーバーに展開する方法を説明しました。 デプロイされると、インターネットに接続しているすべてのユーザーが web サイトにアクセスできるようになります。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [App\_Offline .htm を表示し、"IE のわかりやすいエラー" 機能を回避する](https://weblogs.asp.net/scottgu/App_5F00_Offline.htm-and-working-around-the-_2200_IE-Friendly-Errors_2200_-feature)
- [セッション状態モード](https://msdn.microsoft.com/library/ms178586.aspx)

> [!div class="step-by-step"]
> [前へ](determining-what-files-need-to-be-deployed-cs.md)
> [次へ](deploying-your-site-using-visual-studio-cs.md)

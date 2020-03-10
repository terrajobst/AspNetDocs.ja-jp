---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-cs
title: Visual Studio を使用してサイトC#をデプロイする () |Microsoft Docs
author: rick-anderson
description: Visual Studio には、web サイトを配置するためのツールが含まれています。 これらのツールの詳細については、このチュートリアルを参照してください。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: cde4ee53-a5d0-4937-a54b-67877e8266c3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-cs
msc.type: authoredcontent
ms.openlocfilehash: 4259e51f5a3e6a97bae2aa27b76cbd56ca3449d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522796"
---
# <a name="deploying-your-site-using-visual-studio-c"></a>Visual Studio を使用してサイトを配置する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_04_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial04_DeployingViaVS_cs.pdf)

> Visual Studio には、web サイトを配置するためのツールが含まれています。 これらのツールの詳細については、このチュートリアルを参照してください。

## <a name="introduction"></a>はじめに

前のチュートリアルでは、単純な ASP.NET web アプリケーションを web ホストプロバイダーに展開する方法について説明しました。 具体的には、FileZilla のような FTP クライアントを使用して、開発環境から運用環境に必要なファイルを転送する方法を説明しました。 また、Visual Studio には、web ホストプロバイダーへの配置を容易にする組み込みのツールも用意されています。 このチュートリアルでは、Web サイトのコピーツールの2つについて検討します。このツールでは、FTP または FrontPage Server Extensions を使用してリモート web サーバーとの間でファイルを移動できます。発行ツール。 web サイト全体を指定した場所にコピーします。

> [!NOTE]
> Visual Studio で提供されるその他の配置関連ツールには、 [Web セットアッププロジェクト](https://msdn.microsoft.com/library/wx3b589t.aspx)および[web 配置プロジェクト](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en)アドインが含まれます。 Web セットアッププロジェクトでは、web サイトのコンテンツと構成情報を1つの MSI ファイルにパッケージ化します。 このオプションは、イントラネット内に展開されている web サイトや、お客様が独自の web サーバーにインストールした事前パッケージ web アプリケーションを販売する企業にとって最も役立ちます。 Web 配置プロジェクトアドインは、開発環境と運用環境のビルド間の構成の違いを簡単に指定できる Visual Studio アドインです。 このチュートリアルシリーズでは、Web セットアッププロジェクトについては説明しません。Web 配置プロジェクトの概要については、「[*開発と運用のチュートリアルの間の一般的な構成の違い*](common-configuration-differences-between-development-and-production-cs.md)」をお寄せください。

## <a name="deploying-your-site-using-the-copy-web-site-tool"></a>Web サイトのコピーツールを使用したサイトのデプロイ

Visual Studio の Web サイトのコピーツールは、スタンドアロン FTP クライアントの機能に似ています。 簡単に言うと、Web サイトのコピーツールを使用すると、FTP または FrontPage Server Extensions 経由でリモート web サイトに接続できます。 FileZilla のユーザーインターフェイスと同様に、Web サイトのコピーのユーザーインターフェイスは2つのペインで構成されます。左側のウィンドウにはローカルファイルが一覧表示され、右側のペインには移行先サーバー上のファイルが一覧表示されます。

> [!NOTE]
> Web サイトのコピーツールは、Web サイトプロジェクトでのみ使用できます。 Web アプリケーションプロジェクトを使用する場合、Visual Studio はこのツールを提供します。

Web サイトのコピーツールを使用して、本レビューアプリケーションを運用環境に発行する方法を見てみましょう。 Web サイトのコピーツールは、Web サイトプロジェクトモデルを使用するプロジェクトでのみ機能するので、BookReviewsWSP プロジェクトでこのツールを使用してのみ調べることができます。 そのプロジェクトを開きます。

ソリューションエクスプローラーの [Web サイトのコピー] アイコンをクリックして、Web サイトのコピーツールプロジェクトを起動します (このアイコンは図1で丸で囲まれています)。または、[Web サイト] メニューの [Web サイトのコピー] オプションを選択することもできます。 どちらの方法でも、図1に示す Web サイトのコピーのユーザーインターフェイスが起動されます。リモートサーバーにまだ接続していないため、図1の左側のウィンドウだけが設定されます。

[Web サイトのコピーツールのユーザーインターフェイスの ![は、2つのペインに分割されています。](deploying-your-site-using-visual-studio-cs/_static/image2.png)](deploying-your-site-using-visual-studio-cs/_static/image1.png)

**図 1**: Web サイトのコピーツールのユーザーインターフェイスが2つのペインに分割されている ([クリックしてフルサイズのイメージを表示する](deploying-your-site-using-visual-studio-cs/_static/image3.png))

サイトをデプロイするには、最初に web ホストプロバイダーに接続する必要があります。 Web サイトのコピーのユーザーインターフェイスの上部にある [接続] ボタンをクリックします。 これにより、図2に示す [Web サイトを開く] ダイアログボックスが表示されます。

左の4つのオプションのいずれかを選択して、目的の web サイトに接続できます。

- **[ファイルシステム]** -コンピューターからアクセスできるフォルダーまたはネットワーク共有にサイトを展開するには、このチェックボックスをオンにします。
- **[ローカル iis]** : コンピューターにインストールされている IIS web サーバーにサイトを展開する場合に、このオプションを使用します。
- **Ftp サイト**-ftp を使用してリモート web サイトに接続します。
- **リモートサイト**-FrontPage Server Extensions を使用してリモート web サイトに接続します。

ほとんどの web ホストプロバイダーは FTP をサポートしますが、FrontPage Server 拡張機能のサポートはあまりありません。 そのため、[FTP サイト] オプションを選択し、図2に示すように接続情報を入力しました。

[送信先 Web サイトを指定 ![には](deploying-your-site-using-visual-studio-cs/_static/image5.png)](deploying-your-site-using-visual-studio-cs/_static/image4.png)

**図 2**: 接続先の web サイトを指定[する (クリックすると、フルサイズの画像が表示](deploying-your-site-using-visual-studio-cs/_static/image6.png)されます)

接続後、Web サイトのコピーツールでは、リモートサイトのファイルが右ペインに読み込まれ、各ファイルの状態 (新規、削除済み、変更済み、または変更されていない) が示されます。 ローカルサイトからリモートサイトにファイルをコピーしたり、その逆をコピーしたりできます。

BookReviewsWSP プロジェクトに新しいページを追加し、それをデプロイして、Web サイトのコピーツールが動作することを確認しましょう。 `Privacy.aspx`という名前のルートディレクトリで、Visual Studio で新しい ASP.NET ページを作成します。 ページで `Site.master` マスターページを使用し、サイトのプライバシーポリシーをこのページに追加します。 図3は、このページが作成された後の Visual Studio を示しています。

[&gt;&lt;コードという名前の新しいページを Web サイトのルートフォルダーに追加 ![ます&gt;&lt;。](deploying-your-site-using-visual-studio-cs/_static/image8.png)](deploying-your-site-using-visual-studio-cs/_static/image7.png)

**図 3**: `Privacy.aspx` という名前の新しいページを web サイトのルートフォルダーに追加する ([クリックすると、フルサイズの画像が表示](deploying-your-site-using-visual-studio-cs/_static/image9.png)されます)

次に、[Web サイトのコピー] ユーザーインターフェイスに戻ります。 図4に示すように、左側のウィンドウに新しいファイル `Policy.aspx` と `Policy.aspx.cs`が含まれるようになりました。 さらに、これらのファイルは矢印アイコンでマークされ、[新規] の状態になっています。これは、これらがローカルサイトに存在するがリモートサイトには存在しないことを示しています。

[![Web サイトのコピーツールには、新しい &lt;コード&gt;のプライバシーに関する情報が含まれています。このページの左側のウィンドウには、コードが含まれて&gt;&lt;います。](deploying-your-site-using-visual-studio-cs/_static/image11.png)](deploying-your-site-using-visual-studio-cs/_static/image10.png)

**図 4**: Web サイトのコピーツールでは、新しい `Privacy.aspx` ページが左側のウィンドウに表示されます ([クリックすると、フルサイズの画像が表示](deploying-your-site-using-visual-studio-cs/_static/image12.png)されます)

新しいファイルを展開するには、それらを選択し、矢印アイコンをクリックしてリモートサイトに転送します。 転送が完了すると `Policy.aspx` と、状態が変更されていないローカルとリモートの両方のサイトに `Policy.aspx.cs` ファイルが存在します。

Web サイトのコピーツールでは、新しいファイルの一覧表示と共に、ローカルサイトとリモートサイトで異なるファイルが強調表示されます。 実際の動作を確認するには、[`Privacy.aspx`] ページに戻り、プライバシーポリシーにいくつかの単語を追加します。 ページを保存し、Web サイトのコピーツールに戻ります。 図5に示すように、左側のウィンドウの [`Privacy.aspx`] ページには、リモートサイトと同期していないことを示す [変更] という状態があります。

[Web サイトのコピーツールを ![と、&lt;コード&gt;のコード&gt; ページが変更されたことを示し&lt;ます。](deploying-your-site-using-visual-studio-cs/_static/image14.png)](deploying-your-site-using-visual-studio-cs/_static/image13.png)

**図 5**: Web サイトのコピーツールは、`Privacy.aspx` ページが変更されたことを示します ([クリックすると、フルサイズの画像が表示](deploying-your-site-using-visual-studio-cs/_static/image15.png)されます)

Web サイトのコピーツールは、最後のコピー操作以降にファイルが削除されたかどうかも示します。 ローカルプロジェクトから `Privacy.aspx` を削除し、Web サイトのコピーツールを更新します。 `Privacy.aspx` および `Privacy.aspx.cs` ファイルは左側のウィンドウに表示されたままですが、最後のコピー操作以降に削除されたことを示す状態が削除されています。

## <a name="publishing-a-web-application"></a>Web アプリケーションの発行

Visual Studio 内から web アプリケーションを配置するもう1つの方法は、[ビルド] メニューからアクセスできる [発行] オプションを使用することです。 Publish オプションは、アプリケーションを明示的にコンパイルし、必要なすべてのファイルを指定されたリモートサイトにコピーします。 後で説明するように、Publish オプションは Web サイトのコピーツールよりも無愛想です。 Web サイトのコピーツールを使用すると、ローカルサイトおよびリモートサイト上のファイルを確認し、必要に応じて個々のファイルをアップロードまたはダウンロードできるようになります。また、[発行] オプションを使用すると、web アプリケーション全体がデプロイされます。

必要なすべてのファイルを指定されたリモートサイトにコピーするだけでなく、[発行] オプションを選択すると、アプリケーションも明示的にコンパイルされます。 Web アプリケーションプロジェクトを明示的にコンパイルする必要がある場合は、Web アプリケーションプロジェクトで [発行] オプションが使用可能であることを意外に考える必要があります。 少し驚くかもしれませんが、Web サイトプロジェクトで [発行] オプションを使用することもできます。 「[*配置する必要があるファイルの決定*](determining-what-files-need-to-be-deployed-cs.md)」チュートリアルで説明したように、Web サイトプロジェクトは、*事前コンパイル*と呼ばれるプロセスを使用して明示的にコンパイルできます。 このチュートリアルでは、Web アプリケーションプロジェクトで発行オプションを使用する方法について説明します。今後のチュートリアルでは、事前コンパイルについて説明します。この時点で、Web サイトプロジェクトで発行オプションを使用する方法を確認します。

> [!NOTE]
> [発行] オプションは、Web サイトプロジェクトと Web アプリケーションプロジェクトの両方で Visual Studio で使用できますが、Visual Web Developer では、Web アプリケーションプロジェクトの [発行] オプションのみが提供されます。

Publish オプションを使用して、書籍レビューアプリケーションをデプロイする方法を見てみましょう。 まず、Visual Studio で BookReviewsWAP (Web アプリケーションプロジェクト) を開きます。 [発行] メニューで、[Build BookReviewsWAP] プロジェクトを選択します。 これにより、他の構成オプションのように、ターゲットの場所を入力するよう求めるダイアログボックスが表示されます (図6を参照)。 Web サイトのコピーツールと同様に、ローカルフォルダー、IIS 上のローカル web サイト、FrontPage Server Extensions をサポートするリモート web サイト、または FTP サーバーのアドレスを指す場所を入力できます。 リモート web サーバー上のファイルを、展開されたファイルに置き換えるか、または発行前にリモートサイト上のすべてのコンテンツを削除するかを選択できます。 また、次の項目をコピーするかどうかを指定することもできます。

- プロジェクト内のファイルだけがアプリケーションを実行する必要があります。これにより、不要なソースコードおよびプロジェクト関連ファイルが除外されます。
- すべてのプロジェクトファイル。ソースコードファイルと、ソリューションファイルのような Visual Studio プロジェクトファイルが含まれます。
- ソースプロジェクトフォルダー内のすべてのファイル。ソースプロジェクトフォルダー内のすべてのファイルが、プロジェクトに含まれているかどうかに関係なくコピーされます。

`App_Data` フォルダーの内容をアップロードするオプションもあります。

[送信先 Web サイトを指定 ![には](deploying-your-site-using-visual-studio-cs/_static/image17.png)](deploying-your-site-using-visual-studio-cs/_static/image16.png)

**図 6**: 接続先の web サイトを指定[する (クリックすると、フルサイズの画像が表示](deploying-your-site-using-visual-studio-cs/_static/image18.png)されます)

Book Review アプリケーションの場合、リモートサイトには、Web サイトのコピーツールを使用して BookReviewsWSP プロジェクトをコピーするときに配置されたファイルが含まれています。 そのため、既存のコンテンツをすべて削除して、Publish オプションを開始してみましょう。 また、不要なソースコードやプロジェクトファイルを使用して運用環境を乱雑にするのではなく、必要なファイルをコピーするだけです。 これらのオプションを指定したら、[発行] ボタンをクリックします。 次の数秒で、Visual Studio は必要なファイルを変換先サイトに配置し、進行状況を出力ウィンドウに表示します。

図7に、発行操作が完了した後の FTP サイト上のファイルを示します。 マークアップページと、必要なサーバー側およびクライアント側のサポートファイルのみがアップロードされていることに注意してください。

[必要なファイルのみが運用環境に発行された ![](deploying-your-site-using-visual-studio-cs/_static/image20.png)](deploying-your-site-using-visual-studio-cs/_static/image19.png)

**図 7**: 必要なファイルのみが運用環境に発行された ([クリックしてフルサイズのイメージを表示する](deploying-your-site-using-visual-studio-cs/_static/image21.png))

Publish オプションは、Web サイトのコピーツールよりも微妙なツールです。 Web サイトのコピーツールを使用すると、ローカルサイトおよびリモートサイト上のファイルを検査し、それらがどのように異なるかを確認することができます。発行オプションでは、そのようなインターフェイスは提供されません。 さらに、Web サイトのコピーツールを使用すると、個々のファイルをアップロードまたは削除することができます。 Publish オプションでは、このような細かい制御が許可されていません。代わりに、アプリケーション*全体*が発行されます。 この動作には長所と短所があります。 プラス側では、発行オプションを使用するときに、重要なファイルのアップロードを忘れることはありません。 ただし、非常に大規模な web サイトに小さな変更を加えた場合、発行オプションを使用すると、変更されたページを更新することはできず、Visual Studio によってサイト全体が展開されるまで待機する必要があります。

運用環境と開発環境でコンテンツが異なる特定のファイルが存在することは珍しくありません。 キーの例としては、アプリケーションの構成ファイル `Web.config`があります。 発行オプションによって web アプリケーションファイルが無条件にコピーされるため、運用環境のカスタマイズされた構成ファイルは開発環境のバージョンで上書きされます。 以降のチュートリアルでは、このトピックについて詳しく説明し、このような違いが存在する場合に web アプリケーションをデプロイするためのヒントを提供します。

## <a name="summary"></a>まとめ

Web サイトを配置するには、必要なファイルを開発環境から運用環境にコピーする必要があります。 前のチュートリアルでは、FileZilla のような FTP クライアントを使用してファイルを転送する方法を説明しました。 このチュートリアルでは、Visual Studio の2つの配置ツール (Web サイトのコピーツールと [発行] オプション) を確認しています。 Web サイトのコピーツールは、FTP クライアントに似ています。これは、ローカルコンピューター上のファイルと、2つのコンピューター間でファイルを簡単にアップロードまたはダウンロードできるように指定されたリモートコンピューターの2つのペインからなるインターフェイスがあることです。 Publish オプションは、プロジェクトを明示的にコンパイルし、指定された変換先にアプリケーション全体を配置する、より無愛想ツールです。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [Web サイトのコピーツールを使用した Web サイトのコピー](https://msdn.microsoft.com/library/1cc82atw.aspx)
- [操作方法: Web サイトのコピーツールを使用して Web サイトをデプロイ](../../../videos/how-do-i/how-do-i-deploy-a-web-site-using-the-copy-web-site-tool.md)する (ビデオ)
- [方法: Web アプリケーションプロジェクトを発行する](https://msdn.microsoft.com/library/aa983453.aspx)
- [方法: Web サイトを発行する](https://msdn.microsoft.com/library/20yh9f1b.aspx)
- [Visual Studio でのセットアッププロジェクトと配置プロジェクト](https://msdn.microsoft.com/library/wx3b589t.aspx)

> [!div class="step-by-step"]
> [前へ](deploying-your-site-using-an-ftp-client-cs.md)
> [次へ](common-configuration-differences-between-development-and-production-cs.md)

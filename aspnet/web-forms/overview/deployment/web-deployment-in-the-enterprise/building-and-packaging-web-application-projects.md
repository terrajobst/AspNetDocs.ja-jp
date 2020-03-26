---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
title: Web アプリケーションプロジェクトのビルドとパッケージ化 |Microsoft Docs
author: jrjlee
description: Web アプリケーションプロジェクトをリモートサーバー環境に配置する場合、最初のタスクは、プロジェクトをビルドし、web 配置パッケージを生成することです。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 94e92f80-a7e3-4d18-9375-ff8be5d666ac
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
msc.type: authoredcontent
ms.openlocfilehash: 1d0ee0264ce6461d7b0159f1a44de4de31e2d079
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463228"
---
# <a name="building-and-packaging-web-application-projects"></a>Web アプリケーション プロジェクトのビルドとパッケージ化

[Jason Lee](https://github.com/jrjlee)

[PDF のダウンロード](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Web アプリケーションプロジェクトをリモートサーバー環境に配置する場合、最初のタスクは、プロジェクトをビルドし、web 配置パッケージを生成することです。 このトピックでは、web アプリケーションプロジェクトのビルドプロセスのしくみについて説明します。 特に、次のことについて説明します。
> 
> - Web 発行パイプライン (WPP) が、配置機能を含むようにビルドプロセスを拡張する方法。
> - インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を使用して、web アプリケーションを展開パッケージに変換する方法について説明します。
> - ビルドとパッケージ化のプロセスのしくみと、作成されるファイルについて説明します。

Visual Studio 2010 では、web アプリケーションプロジェクトのビルドと配置のプロセスは、WPP によってサポートされています。 WPP には、MSBuild の機能を拡張し Web 配置と統合できるようにする一連の Microsoft Build Engine (MSBuild) のターゲットが用意されています。 この拡張機能は、Visual Studio 内で web アプリケーションプロジェクトのプロパティページで確認できます。 パッケージ/ **[発行]** ページでは、 **[SQL のパッケージ化/発行]** ページを使用して、ビルドプロセスが完了したときに web アプリケーションプロジェクトを配置用にパッケージ化する方法を構成できます。

![](building-and-packaging-web-application-projects/_static/image1.png)

## <a name="how-does-the-wpp-work"></a>WPP はどのように動作しますか。

ベースの web アプリケーションプロジェクトのC#プロジェクトファイルを見ると、2つの .targets ファイルがインポートされていることがわかります。

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample1.xml)]

最初の**インポート**ステートメントは、すべてのビジュアルC#プロジェクトに共通です。 このファイル ( *Microsoft. CSharp. targets*) には、ビジュアルC#に固有のターゲットとタスクが含まれています。 たとえば、 C#コンパイラ (**Csc**) タスクはここで呼び出されます。 その後、 *microsoft*の .targets ファイルに*よって、ファイルが*インポートされます。 これにより、**ビルド**、**リビルド**、**実行**、**コンパイル**、**クリーン**など、すべてのプロジェクトに共通するターゲットが定義されます。 2番目の**インポート**ステートメントは、web アプリケーションプロジェクトに固有のものです。 その後、 *microsoft の WebApplication*ファイルに*よって、ファイルが*インポートされます。 この*ファイルは基本的に、WPP* *です。* これは、さまざまな展開タスクを完了するために Web 配置を呼び出すターゲット ( **Package**や**MSDeployPublish**など) を定義します。

これらの追加のターゲットの使用方法を理解するには、Contact Manager サンプルソリューションで、 *Publish*ファイルを開き、 **buildprojects**ターゲットを確認します。

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample2.xml)]

このターゲットでは、 **MSBuild**タスクを使用してさまざまなプロジェクトをビルドします。 **Deployonbuild**プロパティと**deploytarget**プロパティに注目してください。

- **Deployonbuild = true**プロパティは、基本的に "ビルドが正常に完了したときに追加のターゲットを実行します。" という意味になります。
- **Deploytarget**プロパティは、 **deployonbuild**プロパティが**true**と等しい場合に実行するターゲットの名前を指定します。 この場合、プロジェクトをビルドした後、MSBuild で**パッケージ**ターゲットを実行するように指定します。

**パッケージ**ターゲットは、 *Microsoft. Publishing. .targets*ファイルで定義されています。 基本的に、このターゲットは web アプリケーションプロジェクトのビルド出力を取得し、IIS web サーバーに発行できる web 配置パッケージに変換します。

> [!NOTE]
> Visual Studio 2010 でプロジェクトファイル (たとえば、 <em>Contactmanager. .csproj</em>) を表示するには、最初にソリューションからプロジェクトをアンロードする必要があります。 [<strong>ソリューションエクスプローラー</strong> ] ウィンドウで、プロジェクトノードを右クリックし、[<strong>プロジェクトのアンロード</strong>] をクリックします。 もう一度プロジェクトノードを右クリックし、[<em>プロジェクトファイル</em>の<strong>編集</strong>] をクリックします。 プロジェクトファイルは、未加工の XML 形式で開かれます。 完了したらプロジェクトを再度読み込んでください。  
> MSBuild のターゲット、タスク、および<strong>インポート</strong>ステートメントの詳細については、「[プロジェクトファイルに](understanding-the-project-file.md)ついて」を参照してください。 プロジェクトファイルと WPP の詳細については、Microsoft Build Engine 内の [を参照してください。MSBuild と Team Foundation ビルド](http://amzn.com/0735645248) を使用して、作成者 Iロウ Hashimi とウィリアム Bartholomew、ISBN:978-0-7356-4524-0。

## <a name="what-is-a-web-deployment-package"></a>Web 展開パッケージとは

Visual Studio 2010 を使用するか MSBuild を直接使用して、web アプリケーションプロジェクトをビルドして配置すると、通常は*web 配置パッケージ*になります。 Web 配置パッケージは .zip ファイルです。 これには、Web アプリケーションを再作成するために IIS と Web 配置が必要とするすべてのものが含まれます。次のようなものがあります。

- コンテンツ、リソースファイル、構成ファイル、JavaScript とカスケードスタイルシート (CSS) リソースなど、web アプリケーションのコンパイル済み出力。
- Web アプリケーションプロジェクトのアセンブリと、ソリューション内の参照されるプロジェクトのアセンブリ。
- Web アプリケーションと共に配置しているデータベースを生成する SQL スクリプト。

Web 配置パッケージが生成されたら、さまざまな方法で IIS web サーバーに発行できます。 たとえば、リモートエージェントサービスを対象にするか、送信先 web サーバーの Web 配置ハンドラーをターゲットにして、リモートで展開することができます。または、IIS マネージャーを使用して、移行先の web サーバーにパッケージを手動でインポートすることもでき Web 配置ます。 これらの展開方法の詳細については、「 [Web 配置に適切なアプローチを選択する](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)」を参照してください。

## <a name="how-does-the-build-process-work"></a>ビルドプロセスはどのように機能しますか。

これは、web アプリケーションプロジェクトをビルドしてパッケージ化した場合の動作を示しています。

![](building-and-packaging-web-application-projects/_static/image2.png)

Web アプリケーションプロジェクトをビルドすると、ビルドプロセスによって [プロジェクト名] という名前のファイルが生成され*ます。SourceManifest*。 このは、プロジェクトファイルとビルド出力と共に使用さ*れます。SourceManifest*ファイルには、Web 配置パッケージに含める必要がある Web 配置が示されています。 これらの入力を使用して、Web 配置によって、 *[project name] .zip*という名前の Web 配置パッケージが生成されます。

ビルドプロセスでは、web 配置パッケージと共に、パッケージの使用に役立つ2つのファイルが生成されます。

- *.Deploy*ファイルには、web 配置パッケージをリモート IIS web サーバーに発行するパラメーター化された Web 配置 (msdeploy.exe) コマンドのセットが含まれています。 適切なパラメーターを使用して *.deploy*ファイルを実行すると、通常、msdeploy.exe コマンドを手動で作成する代わりに、より迅速かつ簡単に使用できます。
- *Setparameters .xml*ファイルは、msdeploy.exe コマンドにパラメーター値のセットを提供します。 これらの値には、パッケージを配置する IIS web アプリケーションの名前、 *web.config*ファイルで定義されているサービスエンドポイントと接続文字列の値、プロジェクトのプロパティページで定義されている配置プロパティの値などのプロパティが含まれます。

*Setparameters .xml*ファイルは、デプロイプロセスを管理するための鍵です。 このファイルは、web アプリケーションプロジェクトの内容に応じて動的に生成されます。 たとえば、 *web.config ファイルに*接続文字列を追加すると、ビルドプロセスによって接続文字列が自動的に検出され、それに従って配置がパラメーター化され、 *setparameters .xml*ファイルにエントリが作成され、デプロイプロセスの一部として接続文字列を変更できるようになります。 次のトピック「 [Web パッケージ配置のパラメーターの構成](configuring-parameters-for-web-package-deployment.md)」では、このファイルの役割について詳しく説明し、ビルド時および配置時に変更できるさまざまな方法について説明します。

> [!NOTE]
> Visual Studio 2010 では、パッケージ化する前に、WPP は web アプリケーションでのページのプリコンパイルをサポートしていません。 次のバージョンの Visual Studio および WPP には、パッケージ化オプションとして web アプリケーションをプリコンパイルする機能が含まれています。

## <a name="conclusion"></a>まとめ

このトピックでは、Visual Studio 2010 での web アプリケーションプロジェクトのビルドおよびパッケージ化プロセスの概要について説明しました。 この記事では、WPP での Web 配置コマンドの呼び出し方法について説明し、ビルドとパッケージ化のプロセスのしくみについて説明しました。

Web 配置パッケージを作成したら、次の手順としてデプロイします。 詳細については、「 [Web パッケージ配置のパラメーターの構成](configuring-parameters-for-web-package-deployment.md)」および「 [Web パッケージの配置](deploying-web-packages.md)」を参照してください。

## <a name="further-reading"></a>関連項目

このチュートリアルの次のトピック「[Web パッケージの配置](deploying-web-packages.md)と [web パッケージの配置のためのパラメーターの構成](configuring-parameters-for-web-package-deployment.md)」では、作成した web パッケージの使用方法についてのガイダンスを提供しています。 このシリーズの[「高度なエンタープライズ Web 展開](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)」の最後のチュートリアルでは、パッケージ化プロセスをカスタマイズおよびトラブルシューティングする方法についてのガイダンスを提供します。

プロジェクトファイルと WPP の詳細については、Microsoft Build Engine 内の [を参照してください。MSBuild と Team Foundation ビルド](http://amzn.com/0735645248) を使用して、作成者 Iロウ Hashimi とウィリアム Bartholomew、ISBN:978-0-7356-4524-0。

> [!div class="step-by-step"]
> [前へ](understanding-the-build-process.md)
> [次へ](configuring-parameters-for-web-package-deployment.md)

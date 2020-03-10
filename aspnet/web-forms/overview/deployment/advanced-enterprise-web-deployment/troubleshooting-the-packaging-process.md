---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: パッケージ化プロセスのトラブルシューティング |Microsoft Docs
author: jrjlee
description: このトピックでは、M... で Enablepackageprocessの Andassert プロパティを使用して、パッケージ化プロセスに関する詳細情報を収集する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 8ad649dfff085a8774cc13c11d8a3e3d48277d66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509752"
---
# <a name="troubleshooting-the-packaging-process"></a>パッケージ化処理のトラブルシューティング

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、Microsoft Build Engine (MSBuild) で**Enablepackageprocessの Andassert**プロパティを使用して、パッケージ化プロセスに関する詳細情報を収集する方法について説明します。
> 
> **Enablepackageprocessの Andassert**プロパティを**true**に設定すると、MSBuild は次のことを行います。
> 
> - ビルドログにパッケージ化プロセスに関する追加情報を追加します。
> - 特定の条件下でエラーをログに記録します。たとえば、パッケージ化の一覧に重複するファイルがある場合などです。
> - *ProjectName*\_パッケージフォルダーにログディレクトリを作成し、パッケージ化するファイルに関する情報を記録するために使用します。
> 
> パッケージ化処理が失敗した場合、または web 配置パッケージに予期したファイルが含まれていない場合は、この情報を使用してプロセスのトラブルシューティングを行い、問題が発生している場所を特定することができます。
> 
> > [!NOTE]
> > **Enablepackageprocessの Andassert**プロパティは、**デバッグ**構成を使用してプロジェクトをビルドする場合にのみ機能します。 他の構成では、プロパティは無視されます。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a>Enablepackageprocessの Andassert プロパティについて

[Web アプリケーションプロジェクトのビルドおよびパッケージ化](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)Web 発行パイプライン (WPP) が msbuild ターゲットのセットを提供する方法について説明します。これにより、msbuild の機能が拡張され、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) と統合できるようになります。 Web アプリケーションプロジェクトをパッケージ化する場合は、WPP ターゲットを呼び出します。

これらの WPP ターゲットの多くには、 **Enablepackageprocesslogs Andassert**プロパティが**true**に設定されている場合に追加情報をログに記録する条件付きロジックが含まれます。 たとえば、**パッケージ**ターゲットを確認すると、追加のログディレクトリが作成され、 **enablepackageprocessの andassert**が**true**の場合は、ファイルの一覧がテキストファイルに書き込まれることがわかります。

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]

> [!NOTE]
> WPP ターゲットは、% PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web フォルダーの*Microsoft. Publishing. .targets*ファイルで定義されています。 このファイルを開き、Visual Studio 2010 または任意の XML エディターでターゲットを確認することができます。 ファイルの内容を変更しないように注意してください。

## <a name="enabling-the-additional-logging"></a>追加のログ記録を有効にする

**Enablepackageprocessの Andassert**プロパティの値は、プロジェクトのビルド方法に応じてさまざまな方法で指定できます。

コマンドラインからプロジェクトをビルドする場合は、コマンドライン引数として**Enablepackageprocessの Andassert**プロパティの値を指定できます。

[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]

カスタムプロジェクトファイルを使用してプロジェクトをビルドしている場合は、 **MSBuild**タスクの**Properties**属性に**Enablepackageprocessの andassert**値を含めることができます。

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]

Team Foundation Server (TFS) のビルド定義を使用してプロジェクトをビルドしている場合は、 **MSBuild の Arguments**行で**enablepackageprocessの andassert**プロパティの値を指定できます。![](troubleshooting-the-packaging-process/_static/image1.png)

> [!NOTE]
> ビルド定義の作成と構成の詳細については、「[配置をサポートするビルド定義の作成](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)」を参照してください。

または、すべてのビルドにパッケージを含める場合は、web アプリケーションプロジェクトのプロジェクトファイルを変更して、 **Enablepackageprocessの Andassert**プロパティを**true**に設定します。 .Csproj ファイルまたは .vbproj ファイル内の最初の**PropertyGroup**要素にプロパティを追加する必要があります。

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]

## <a name="reviewing-the-log-files"></a>ログファイルの確認

**Enablepackageprocessの Andassert**が**true**に設定された web アプリケーションプロジェクトをビルドしてパッケージ化すると、MSBuild は*ProjectName*\_package フォルダーに Log という名前の追加のフォルダーを作成します。 ログフォルダーには、さまざまなファイルが含まれています。

![](troubleshooting-the-packaging-process/_static/image2.png)

表示されるファイルの一覧は、プロジェクトの内容とビルドプロセスによって異なります。 ただし、通常、これらのファイルは、処理のさまざまな段階で、パッケージ化のために WPP が収集しているファイルの一覧を記録するために使用されます。

- *PreExcludePipelineCollectFilesPhaseFileList*ファイルには、除外対象として指定されたファイルがすべて削除される前に、MSBuild によってパッケージ化のために収集されるファイルが一覧表示されます。
- *AfterExcludeFilesFilesList*ファイルには、除外対象として指定されたファイルがすべて削除された後に、変更されたファイルの一覧が含まれています。

    > [!NOTE]
    > パッケージ化プロセスからファイルとフォルダーを除外する方法の詳細については、「[展開からのファイルとフォルダーの除外](excluding-files-and-folders-from-deployment.md)」を参照してください。
- *Aftertransformwebconfig .txt*ファイルには *、任意の web.config 変換*が実行された後にパッケージ化のために収集されたファイルが一覧表示されます。 この一覧では、構成固有の*web.config 変換ファイル*( *web.config や web.config など)* *は、パッケージ*化のためにファイルの一覧から除外されます。 変換された1つの*web.config*がその場所に含まれています。
- *PostAutoParameterizationWebConfigConnectionStrings*ファイルには、 *web.config ファイル内*の接続文字列がパラメーター化された後のファイルの一覧が含まれています。 これは、パッケージを配置するときに、接続文字列をターゲット環境の適切な設定に置き換えることができるプロセスです。
- *Prepackage .txt*ファイルには、パッケージに含めるファイルの完成したビルド前の一覧が含まれています。

> [!NOTE]
> 追加のログファイルの名前は、通常、WPP ターゲットに対応します。 これらのターゲットを確認するには *、%* PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web フォルダー内のファイルを調べます。

Web パッケージの内容が期待どおりでない場合は、これらのファイルを確認することで、プロセスがどの時点で問題になったかを特定するのに便利です。

## <a name="conclusion"></a>まとめ

このトピックでは、MSBuild で**Enablepackageprocessの Andassert**プロパティを使用して、パッケージ化プロセスのトラブルシューティングを行う方法について説明します。 この記事では、ビルドプロセスにプロパティ値を提供するさまざまな方法について説明し、プロパティを**true**に設定した場合に記録される追加情報について説明しました。

## <a name="further-reading"></a>参考資料

カスタム MSBuild プロジェクトファイルを使用した配置プロセスの制御の詳細については、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」および「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。 WPP と、それがパッケージ化プロセスを管理する方法の詳細については、「 [Web アプリケーションプロジェクトのビルドおよびパッケージ化](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)」を参照してください。 Web 配置パッケージから特定のファイルとフォルダーを除外する方法のガイダンスについては、「[展開からのファイルとフォルダーの除外](excluding-files-and-folders-from-deployment.md)」を参照してください。

> [!div class="step-by-step"]
> [[戻る]](running-windows-powershell-scripts-from-msbuild-project-files.md)

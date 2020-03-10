---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: ファイルとフォルダーを配置から除外する |Microsoft Docs
author: jrjlee
description: このトピックでは、web アプリケーションプロジェクトをビルドしてパッケージ化するときに、web 配置パッケージからファイルとフォルダーを除外する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: a262ce43d7199fb1015d54d0b7c213857c360946
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438418"
---
# <a name="excluding-files-and-folders-from-deployment"></a>配置からファイルとフォルダーを除外する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、web アプリケーションプロジェクトをビルドしてパッケージ化するときに、web 配置パッケージからファイルとフォルダーを除外する方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="overview"></a>概要

Visual Studio 2010 で web アプリケーションプロジェクトをビルドする場合、Web 発行パイプライン (WPP) を使用すると、コンパイルされた web アプリケーションを展開可能な web パッケージにパッケージ化することによって、このビルドプロセスを拡張できます。 その後、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を使用して、この web パッケージをリモート IIS web サーバーに展開したり、IIS マネージャーを使用して手動でインポートしたりできます。 このパッケージ化プロセスについ[ては、「Web アプリケーションプロジェクトのビルドおよびパッケージ化](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)」で説明されています。

では、どのようにして web パッケージに含まれるのかを制御するにはどうすればよいでしょうか。 Visual Studio のプロジェクト設定は、基になるプロジェクトファイルを通じて、多数のシナリオに十分な制御を提供します。 ただし、場合によっては、web パッケージのコンテンツを特定の配置先環境に合わせて調整する必要があります。 たとえば、アプリケーションをテスト環境に配置するときにログファイルのフォルダーを含め、ステージング環境または運用環境にアプリケーションを配置するときにそのフォルダーを除外することができます。 このトピックでは、その方法について説明します。

## <a name="what-gets-included-by-default"></a>既定では何が含まれますか。

Visual Studio で web アプリケーションプロジェクトのプロパティを構成すると、 **[パッケージ/発行]** ページの **[配置する項目]** の一覧で、web 配置パッケージに含める内容を指定できます。 既定では、このアプリケーションを**実行するために必要なファイルのみ**に設定されます。

![](excluding-files-and-folders-from-deployment/_static/image1.png)

**このアプリケーションの実行に必要なファイルのみ**を選択した場合、WPP は web パッケージに追加するファイルを決定しようとします。 これには次のものが含まれます

- プロジェクトのすべてのビルド出力。
- **コンテンツ**のビルドアクションでマークされたファイル。

> [!NOTE]
> このファイルには、含めるファイルを決定するロジックが含まれています。   
> *%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\.........*

## <a name="excluding-specific-files-and-folders"></a>特定のファイルとフォルダーを除外する

場合によっては、どのファイルとフォルダーを展開するかをきめ細かく制御する必要があります。 事前に除外するファイルがわかっていて、その除外がすべての変換先環境に適用される場合は、各ファイルの**ビルドアクション**を**None**に設定するだけで済みます。

**特定のファイルを配置から除外するには**

1. **[ソリューションエクスプローラー]** ウィンドウで、ファイルを右クリックし、 **[プロパティ]** をクリックします。
2. **[プロパティ]** ウィンドウの **[ビルドアクション]** 行で、 **[なし]** を選択します。

ただし、この方法は常に便利であるとは限りません。 たとえば、配置先の環境に応じて、または Visual Studio の外部から、どのファイルとフォルダーを含めるかを変更することができます。 たとえば、Contact Manager サンプルソリューションで、ContactManager. Mvc プロジェクトの内容を確認します。

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- 内部フォルダーには、開発者が開発目的でローカルデータベースを作成、削除、および設定するために使用する SQL スクリプトが含まれています。 このフォルダー内の何も、ステージング環境または運用環境に配置することはできません。
- Scripts フォルダーには、いくつかの JavaScript ファイルが含まれています。 これらのファイルの大部分は、Visual Studio でのデバッグまたは IntelliSense の提供をサポートするためにのみ含まれています。 これらのファイルの一部は、ステージング環境または運用環境に配置しないでください。 ただし、トラブルシューティングを容易にするために、開発者向けテスト環境に配置することもできます。

プロジェクトファイルを操作して特定のファイルやフォルダーを除外することもできますが、簡単な方法があります。 WPP には、 **ExcludeFromPackageFolders**および**ExcludeFromPackageFiles**という名前の項目リストを作成してファイルとフォルダーを除外する機構が含まれています。 これらのリストに独自の項目を追加することで、この機構を拡張できます。 これを行うには、次の大まかな手順を実行する必要があります。

1. プロジェクトファイルと同じフォルダーに、 *[project name] wpp*という名前のカスタムプロジェクトファイルを作成します。

    > [!NOTE]
    > *.Targets*ファイルは、web アプリケーションプロジェクトファイル&#x2014;と同じフォルダーに配置する必要があります。たとえば、ビルドと配置のプロセスを制御するために使用するカスタムプロジェクトファイルと同じフォルダーではなく、 *contactmanager. .csproj*&#x2014;というフォルダーにする必要があります。
2. **ItemGroup**ファイル*で*、要素を追加します。
3. **ItemGroup**要素で、必要に応じて特定のファイルとフォルダーを除外するために、 **ExcludeFromPackageFolders**と**ExcludeFromPackageFiles**の項目を追加します。

*このファイルの*基本的な構造は次のとおりです。

[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]

各項目には、 **Fromtarget**という名前の項目メタデータ要素が含まれていることに注意してください。 これは、ビルドプロセスに影響しない省略可能な値です。これは、他のユーザーがビルドログをレビューしたときに特定のファイルやフォルダーが省略された理由を示すためにのみ機能します。

## <a name="excluding-files-and-folders-from-a-web-package"></a>Web パッケージからのファイルとフォルダーの除外

次の手順では、web アプリケーションプロジェクトに*wpp*ファイルを追加する方法と、プロジェクトをビルドするときにファイルを使用して web パッケージから特定のファイルとフォルダーを除外する方法について説明します。

**ファイルとフォルダーを web 配置パッケージから除外するには**

1. Visual Studio 2010 でソリューションを開きます。
2. **[ソリューションエクスプローラー]** ウィンドウで、web アプリケーションプロジェクトノード ( **contactmanager**など) を右クリックし、 **[追加]** をポイントして、 **[新しい項目]** をクリックします。
3. **[新しい項目の追加]** ダイアログボックスで、 **[XML ファイル]** テンプレートを選択します。
4. **[名前]** ボックスに「 *[project Name] * * ** を使用します。」と入力し (たとえば、 **contactmanager. Mvc. wpp**)、 **[追加]** をクリックします。

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > プロジェクトのルートノードに新しい項目を追加すると、そのファイルはプロジェクトファイルと同じフォルダーに作成されます。 これを確認するには、エクスプローラーでフォルダーを開きます。
5. ファイルで、**プロジェクト**要素と**ItemGroup**要素を追加します。

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. Web パッケージからフォルダーを除外する場合は、 **ItemGroup**要素に**ExcludeFromPackageFolders**要素を追加します。

   1. **Include**属性に、除外するフォルダーのセミコロン区切りのリストを指定します。
   2. **Fromtarget**メタデータ要素で、フォルダーが除外される理由を示す意味のある値を指定します。これは *、ファイルの*名前のようになります。

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. Web パッケージからファイルを除外する場合は、 **ItemGroup**要素に**ExcludeFromPackageFiles**要素を追加します。

   1. **Include**属性に、除外するファイルのセミコロン区切りのリストを指定します。
   2. **Fromtarget**メタデータ要素で、ファイルが除外される理由を示す意味のある値を*指定します*。これは、ファイルの名前のようになります。

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. *[プロジェクト名] の .targets*ファイルは次のようになります。

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. *[Project name]. wpp. .targets*ファイルを保存して閉じます。

次に web アプリケーションプロジェクトをビルドしてパッケージ化すると、WPP によって自動的に*wpp*ファイルが検出されます。 指定したファイルとフォルダーは、web パッケージに含まれません。

## <a name="conclusion"></a>まとめ

このトピックでは、web アプリケーションプロジェクトファイルと同じフォルダーにカスタムの*wpp*ファイルを作成することによって、web パッケージのビルド時に特定のファイルとフォルダーを除外する方法について説明します。

## <a name="further-reading"></a>参考資料

カスタム Microsoft Build Engine (MSBuild) プロジェクトファイルを使用した配置プロセスの制御の詳細については、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」および「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」を参照してください。 パッケージ化と配置のプロセスの詳細については、「 [Web アプリケーションプロジェクトのビルドとパッケージ化](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)」、「Web[パッケージ配置のパラメーターの構成](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)」、および「 [web パッケージの配置](../web-deployment-in-the-enterprise/deploying-web-packages.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](deploying-membership-databases-to-enterprise-environments.md)
> [次へ](taking-web-applications-offline-with-web-deploy.md)

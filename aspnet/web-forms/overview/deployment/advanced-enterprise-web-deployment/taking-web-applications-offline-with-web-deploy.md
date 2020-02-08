---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
title: Web 配置を使用して Web アプリケーションをオフラインにする |Microsoft Docs
author: jrjlee
description: このトピックでは、インターネットインフォメーションサービス (IIS) Web 展開を使用して、自動展開の間に web アプリケーションをオフラインにする方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3e9f6e7d-8967-4586-94d5-d3a122f12529
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
msc.type: authoredcontent
ms.openlocfilehash: ba60664a0c3daa0650cd7e7cfc4ab9da08df3440
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075139"
---
# <a name="taking-web-applications-offline-with-web-deploy"></a>Web 配置の際、Web アプリをオフラインにする

[Jason Lee](https://github.com/jrjlee)

[PDF のダウンロード](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、インターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を使用して、自動展開の間に web アプリケーションをオフラインにする方法について説明します。 Web アプリケーションを参照するユーザーは、デプロイが完了するまで、*オフライン .htm ファイル\_アプリ*にリダイレクトされます。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この&#x2014;プロジェクトファイルには、ビルドプロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドおよび配置設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="task-overview"></a>タスクの概要

さまざまなシナリオでは、データベースや web サービスなどの関連コンポーネントに変更を加えるときに、web アプリケーションをオフラインにする必要があります。 通常、IIS と ASP.NET では、 *App\_* という名前のファイルを iis web サイトまたは web アプリケーションのルートフォルダーに配置することによってこれを実現します。 *\_のオフライン .htm*ファイルは標準の HTML ファイルであり、通常、メンテナンスのためにサイトが一時的に使用できないことを通知する単純なメッセージが含まれています。 *アプリ\_オフライン .htm*ファイルが web サイトのルートフォルダーに存在している間、IIS は自動的にすべての要求をファイルにリダイレクトします。 更新が完了したら、*アプリ\_offline .htm*ファイルを削除すると、web サイトは通常どおりに要求の処理を再開します。

Web 配置を使用して、対象の環境に対して自動または単一ステップの配置を実行する場合は、*アプリ\_のオフライン .htm*ファイルの追加と削除を展開プロセスに組み込むことをお勧めします。 これを行うには、次のような高レベルのタスクを実行する必要があります。

- 配置プロセスの制御に使用する Microsoft Build Engine (MSBuild) プロジェクトファイルで、配置タスクを開始する前に、移行先サーバーに*アプリ\_オフライン .htm*ファイルをコピーする MSBuild ターゲットを作成します。
- すべての展開タスクが完了したら、移行先サーバーから*アプリ\_offline .htm*ファイルを削除する別の MSBuild ターゲットを追加します。
- Web アプリケーションプロジェクトで、Web 配置が呼び出されたときに、*アプリ\_オフライン .htm*ファイルが配置パッケージに追加されるようにするための、 *.targets*ファイルを作成します。

このトピックでは、これらの手順を実行する方法について説明します。 このトピックのタスクとチュートリアルでは、少なくとも1つの web アプリケーションプロジェクトを含むソリューションが既に作成されていることを前提としています。また、「[エンタープライズでの Web 配置](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)」で説明されているように、カスタムプロジェクトファイルを使用してデプロイプロセスを制御します。 または、 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)サンプルソリューションを使用して、「」の例に従ってください。

## <a name="adding-an-app_offline-file-to-a-web-application-project"></a>アプリ\_オフラインファイルを Web アプリケーションプロジェクトに追加する

最初に完了する必要がある作業は、*アプリ\_オフライン*ファイルを web アプリケーションプロジェクトに追加することです。

- ファイルが開発プロセスに干渉しないようにするには (アプリケーションを完全にオフラインにしないようにする場合)、 *App\_offline. .htm*以外のものを呼び出す必要があります。 たとえば、ファイルに*offline-template\_* という名前を指定できます。
- ファイルがそのように配置されないようにするには、[ビルド] アクションを **[なし**] に設定する必要があります。

**アプリ\_オフラインファイルを web アプリケーションプロジェクトに追加するには**

1. Visual Studio 2010 でソリューションを開きます。
2. **[ソリューションエクスプローラー]** ウィンドウで、web アプリケーションプロジェクトを右クリックし、 **[追加]** をポイントして、 **[新しい項目]** をクリックします。
3. **[新しい項目の追加]** ダイアログボックスで、 **[HTML ページ]** を選択します。
4. **[名前]** ボックスに「 **App\_offline-template**」と入力し、 **[追加]** をクリックします。

    ![](taking-web-applications-offline-with-web-deploy/_static/image1.png)
5. 単純な HTML を追加して、アプリケーションが使用できないことをユーザーに通知し、ファイルを保存します。 サーバー側のタグを含めないでください (たとえば、"asp:" というプレフィックスが付いたタグなど)。 

    ![](taking-web-applications-offline-with-web-deploy/_static/image2.png)
6. **[ソリューションエクスプローラー]** ウィンドウで、新しいファイルを右クリックし、 **[プロパティ]** をクリックします。
7. **[プロパティ]** ウィンドウの **[ビルドアクション]** 行で、 **[なし]** を選択します。

    ![](taking-web-applications-offline-with-web-deploy/_static/image3.png)

## <a name="deploying-and-deleting-an-app_offline-file"></a>アプリ\_オフラインファイルの展開と削除

次の手順では、デプロイロジックを変更して、デプロイプロセスの開始時に移行先サーバーにファイルをコピーし、最後にファイルを削除します。

> [!NOTE]
> 次の手順では、「[プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されているように、カスタム MSBuild プロジェクトファイルを使用して配置プロセスを制御していることを前提としています。 Visual Studio から直接デプロイする場合は、別の方法を使用する必要があります。 作成者は、[発行中に Web アプリをオフラインにする方法](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx)について説明します。

*アプリ\_オフライン*ファイルを移行先の IIS web サイトに展開するには、 [Web 配置**contentpath**プロバイダー](https://technet.microsoft.com/library/dd569034(WS.10).aspx)を使用して msdeploy.exe を呼び出す必要があります。 **Contentpath**プロバイダーは、物理ディレクトリパスと iis web サイトまたはアプリケーションパスの両方をサポートしています。これにより、Visual Studio プロジェクトフォルダーと iis web アプリケーションの間でファイルを同期するための最適な選択肢となります。 ファイルを配置するために、Msdeploy.exe コマンドは次のようになります。

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample1.cmd)]

デプロイプロセスの最後に、転送先サイトからファイルを削除するために、Msdeploy.exe コマンドは次のようになります。

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample2.cmd)]

ビルドと配置のプロセスの一部としてこれらのコマンドを自動化するには、それらをカスタム MSBuild プロジェクトファイルに統合する必要があります。 次の手順では、これを行う方法について説明します。

**オフラインファイル\_アプリを展開および削除するには**

1. Visual Studio 2010 で、配置プロセスを制御する MSBuild プロジェクトファイルを開きます。 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)サンプルソリューションでは、これは、 *Publish*ファイルです。
2. ルート**プロジェクト**要素に、*アプリ\_のオフライン*展開の変数を格納する新しい**PropertyGroup**要素を作成します。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample3.xml)]
3. **SourceRoot**プロパティは、 *Publish*ファイル内の他の場所で定義されています。 これは、ソースコンテンツのルートフォルダーの場所を、現在のパス&#x2014;を基準とした、 *Publish. proj*ファイルの場所を基準とした相対的な位置を示します。
4. **Contentpath**プロバイダーは、相対ファイルパスを受け入れません。そのため、ソースファイルの絶対パスを取得してから、デプロイする必要があります。 これを行うには、 [ConvertToAbsolutePath](https://msdn.microsoft.com/library/bb882668.aspx)タスクを使用します。
5. **GetAppOfflineAbsolutePath**という名前の新しい**Target**要素を追加します。 このターゲット内で、 **ConvertToAbsolutePath**タスクを使用して、プロジェクトフォルダー内の*アプリ\_オフラインテンプレート*ファイルへの絶対パスを取得します。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample4.xml)]
6. このターゲットは、プロジェクトフォルダー内の*アプリ\_オフラインテンプレート*ファイルへの相対パスを取得し、絶対ファイルパスとして新しいプロパティに保存します。 **Beforetargets**属性は、このターゲットを**DeployAppOffline**ターゲットの前に実行することを指定します。これは、次の手順で作成します。
7. **DeployAppOffline**という名前の新しいターゲットを追加します。 このターゲット内で、アプリを移行先の web サーバーに *\_オフライン*ファイルをデプロイする msdeploy.exe コマンドを呼び出します。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample5.xml)]
8. この例では、 **ContactManagerIisPath**プロパティはプロジェクトファイル内の他の場所で定義されています。 これは、単に *[Iis Web サイト名]/[アプリケーション名]* という形式の iis アプリケーションパスです。 ターゲットに条件を含めることで、ユーザーはプロパティ値を変更するかコマンドラインパラメーターを指定することによって、*アプリ\_オフライン*展開のオンとオフを切り替えることができます。
9. **DeleteAppOffline**という名前の新しいターゲットを追加します。 このターゲット内で、保存先の web サーバーから*アプリ\_オフライン*ファイルを削除する msdeploy.exe コマンドを呼び出します。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample6.xml)]
10. 最後のタスクは、プロジェクトファイルの実行中に、これらの新しいターゲットを適切な時点で呼び出します。 これはさまざまな方法で行うことができます。 たとえば、 **FullPublishDependsOn**プロパティでは、 **fullpublish**の既定のターゲットが呼び出されたときに実行する必要があるターゲットのリストを指定し*ます*。
11. MSBuild プロジェクトファイルを変更して、発行プロセスの適切なポイントで**DeployAppOffline**および**DeleteAppOffline**ターゲットを呼び出すようにします。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample7.xml)]

カスタム MSBuild プロジェクトファイルを実行すると、ビルドが正常に完了した直後に、*アプリ\_オフライン*ファイルがサーバーに配置されます。 その後、すべてのデプロイタスクが完了すると、サーバーから削除されます。

## <a name="adding-an-app_offline-file-to-deployment-packages"></a>アプリ\_オフラインファイルを展開パッケージに追加する

展開を構成する方法によっては、移行先に web パッケージを配置&#x2014;するときに、*アプリ\_オフライン .htm*ファイル&#x2014;のように、移行先 IIS web アプリケーションの既存のコンテンツが自動的に削除されることがあります。 デプロイ中に*アプリ\_オフライン .htm*ファイルが配置されるようにするには、デプロイプロセスの開始時に直接ファイルを配置するだけでなく、web 配置パッケージ内にファイルを含める必要があります。

- このトピックの前のタスクを実行したことがある場合は、*アプリ\_オフライン .htm*ファイルを別のファイル名 (*アプリ\_offline-template*を使用しました) の下に web アプリケーションプロジェクトに追加し、ビルドアクションを **[なし**] に設定します。 これらの変更は、ファイルが開発やデバッグに干渉するのを防ぐために必要です。 そのため、パッケージ化プロセスをカスタマイズして、*アプリ\_オフライン .htm*ファイルが web 配置パッケージに含まれるようにする必要があります。

Web 発行パイプライン (WPP) は、 **Filesforの Ingfromproject**という名前の項目リストを使用して、web 配置パッケージに含める必要があるファイルのリストを作成します。 独自の項目をこの一覧に追加することで、web パッケージの内容をカスタマイズできます。 これを行うには、次の大まかな手順を実行する必要があります。

1. プロジェクトファイルと同じフォルダーに、 *[project name] wpp*という名前のカスタムプロジェクトファイルを作成します。

    > [!NOTE]
    > *.Targets*ファイルは、web アプリケーションプロジェクトファイル&#x2014;と同じフォルダーに配置する必要があります。たとえば、ビルドと配置のプロセスを制御するために使用するカスタムプロジェクトファイルと同じフォルダーではなく、 *contactmanager. .csproj*&#x2014;というフォルダーにする必要があります。
2. *Wpp*ファイルで、 **CopyAllFilesToSingleFolderForPackage**ターゲットの*前に*実行する新しい MSBuild ターゲットを作成します。 これは、パッケージに含める項目の一覧を作成する WPP ターゲットです。
3. 新しいターゲットで、 **ItemGroup**要素を作成します。
4. **ItemGroup**要素で、 **Filesfor ingfromプロジェクト**項目を追加し、 *\_アプリをオフライン .htm*ファイルとして指定します。

*. .Targets*ファイルは次のようになります。

[!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample8.xml)]

この例の重要な点を次に示します。

- **Beforetargets**属性は、 **CopyAllFilesToSingleFolderForPackage**ターゲットの直前に実行されることを指定することによって、このターゲットを WPP に挿入します。
- **FilesforDestinationRelativePath Ingfromproject**項目では、ファイルの名前を*app\_offline-template*から*app\_* に変更するために、リストに追加されたときに、このメタデータ値を使用します。

次の手順では、この*wpp*ファイルを web アプリケーションプロジェクトに追加する方法について説明します。

**Web 配置パッケージに wpp ファイルを追加するには**

1. Visual Studio 2010 でソリューションを開きます。
2. **[ソリューションエクスプローラー]** ウィンドウで、web アプリケーションプロジェクトノード ( **contactmanager**など) を右クリックし、 **[追加]** をポイントして、 **[新しい項目]** をクリックします。
3. **[新しい項目の追加]** ダイアログボックスで、 **[XML ファイル]** テンプレートを選択します。
4. **[名前]** ボックスに「 *[project Name] * * ** を使用します。」と入力し (たとえば、 **contactmanager. Mvc. wpp**)、 **[追加]** をクリックします。

    ![](taking-web-applications-offline-with-web-deploy/_static/image4.png)

    > [!NOTE]
    > プロジェクトのルートノードに新しい項目を追加すると、そのファイルはプロジェクトファイルと同じフォルダーに作成されます。 これを確認するには、エクスプローラーでフォルダーを開きます。
5. ファイルで、前に説明した MSBuild マークアップを追加します。

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample9.xml)]
6. *[Project name]. wpp. .targets*ファイルを保存して閉じます。

次に web アプリケーションプロジェクトをビルドしてパッケージ化すると、WPP によって自動的に*wpp*ファイルが検出されます。 アプリ *\_offline-template*ファイルは、*アプリ\_offline. .htm*として生成される web 展開パッケージに含まれます。

> [!NOTE]
> 配置に失敗した場合、*アプリ\_オフライン .htm*ファイルはそのまま残り、アプリケーションはオフラインのままになります。 これは通常、望ましい動作です。 アプリケーションをオンラインに戻すには、web サーバーから*オフラインの .htm ファイル\_アプリ*を削除します。 または、エラーを修正して正常な配置を実行すると、*アプリ\_のオフライン .htm*ファイルが削除されます。

## <a name="conclusion"></a>まとめ

このトピックでは、デプロイ中に web アプリケーションをオフラインにする方法について説明します。そのためには、展開プロセスの開始時に移行先サーバーに*アプリ\_オフライン .htm*ファイルを発行し、最後にそのサーバーを削除します。 また、web 配置パッケージに*アプリ\_offline .htm*ファイルを組み込む方法についても説明します。

## <a name="further-reading"></a>関連項目

パッケージ化と配置のプロセスの詳細については、「 [Web アプリケーションプロジェクトのビルドとパッケージ化](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)」、「Web[パッケージ配置のパラメーターの構成](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)」、および「 [web パッケージの配置](../web-deployment-in-the-enterprise/deploying-web-packages.md)」を参照してください。

Web アプリケーションを Visual Studio から直接発行する場合は、これらのチュートリアルで説明されているカスタム MSBuild プロジェクトファイルの方法を使用するのではなく、発行中にアプリケーションをオフラインにするために、若干異なる方法を使用する必要があります。process.

> [!div class="step-by-step"]
> [前へ](excluding-files-and-folders-from-deployment.md)
> [次へ](running-windows-powershell-scripts-from-msbuild-project-files.md)

---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: 配置をサポートするビルド定義を作成する |Microsoft Docs
author: jrjlee
description: Team Foundation Server (TFS) 2010 で任意の種類のビルドを実行する場合は、チームプロジェクト内にビルド定義を作成する必要があります。 このトピックの内容
ms.author: riande
ms.date: 05/04/2012
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: e11c91a824446572aaf0b3bc6954b9b8ffb4eaff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78489010"
---
# <a name="creating-a-build-definition-that-supports-deployment"></a>配置をサポートするビルド定義を作成する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Team Foundation Server (TFS) 2010 で任意の種類のビルドを実行する場合は、チームプロジェクト内にビルド定義を作成する必要があります。 このトピックでは、TFS で新しいビルド定義を作成する方法と、チームビルドでビルドプロセスの一部として web 配置を制御する方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「プロジェクト[ファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この方法で&#x2014;は、ビルドおよび配置プロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドと配置の設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="task-overview"></a>タスクの概要

ビルド定義は、TFS のチームプロジェクトに対してビルドを実行する方法とタイミングを制御するメカニズムです。 各ビルド定義は次を指定します。

- ビルドする項目。 Visual Studio ソリューションファイルやカスタム Microsoft Build Engine (MSBuild) プロジェクトファイルなどです。
- 手動トリガー、継続的インテグレーション (CI)、ゲートチェックインなど、ビルドを実行するタイミングを決定する条件。
- チームビルドがビルド出力を送信する場所 (web パッケージやデータベーススクリプトなどの配置成果物を含む)。
- 各ビルドが保持される時間の長さ。
- ビルドプロセスの他のさまざまなパラメーター。

> [!NOTE]
> ビルド定義の詳細については、「[ビルドプロセスの定義](https://msdn.microsoft.com/library/ms181715.aspx)」を参照してください。

このトピックでは、開発者が新しいコンテンツをチェックインしたときにビルドがトリガーされるように、CI を使用するビルド定義を作成する方法について説明します。 ビルドが成功した場合、ビルドサービスはカスタムプロジェクトファイルを実行して、ソリューションをテスト環境に配置します。

ビルドをトリガーするときは、次の操作を行う必要があります。

- まず、チームビルドによってソリューションがビルドされます。 このプロセスの一部として、チームビルドは Web 発行パイプライン (WPP) を呼び出して、ソリューション内の各 web アプリケーションプロジェクトの web 配置パッケージを生成します。 チームビルドでは、ソリューションに関連付けられている単体テストも実行されます。
- ソリューションのビルドに失敗した場合、チームビルドはそれ以上の操作を行う必要はありません。 単体テストの失敗は、ビルドの失敗として扱う必要があります。
- ソリューションのビルドが成功した場合は、ソリューションの配置を制御するカスタムプロジェクトファイルをチームビルドで実行する必要があります。 このプロセスの一部として、チームビルドはインターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) を呼び出して、パッケージ化された web アプリケーションを対象の web サーバーにインストールします。また、VSDBCMD ユーティリティを呼び出してデータベースの作成を実行します。転送先データベースサーバー上のスクリプト。

このプロセスを次に示します。

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)サンプルソリューションには、msbuild またはチームビルドから実行できるカスタム msbuild プロジェクトファイル ( *Publish. proj*) が含まれています。 「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」で説明されているように、このプロジェクトファイルは、web パッケージとデータベースをターゲット環境に配置するロジックを定義します。 このファイルには、チームビルドで実行されている場合にビルドおよびパッケージ化のプロセスを省略するロジックが含まれており、実行する配置タスクだけが残ります。 これは、この方法で配置を自動化する場合、通常、ソリューションが正常にビルドされ、配置プロセスが開始される前に単体テストが合格することを確認する必要があるためです。

次のセクションでは、新しいビルド定義を作成することによって、このプロセスを実装する方法について説明します。

> [!NOTE]
> この手順&#x2014;では、ソリューション&#x2014;をビルド、テスト、および配置するための単一の自動化されたプロセスが、テスト環境への配置に最も適している可能性があります。 ステージング環境と運用環境では、テスト環境で既に検証および検証済みのコンテンツを以前のビルドから配置する方がはるかに多い場合があります。 この方法については、次のトピック「[特定のビルドの配置](deploying-a-specific-build.md)」を参照してください。

### <a name="who-performs-this-procedure"></a>だれがこの手順を実行しますか?

通常、TFS 管理者がこの手順を実行します。 場合によっては、開発者チームリーダーが TFS のチームプロジェクトコレクションに対して責任を負うことがあります。 新しいビルド定義を作成するには、ソリューションを含むチームプロジェクトコレクションの**プロジェクトコレクションビルド管理者**グループのメンバーである必要があります。

## <a name="create-a-build-definition-for-ci-and-deployment"></a>CI とデプロイのビルド定義を作成する

次の手順では、CI によってトリガーされるビルド定義を作成する方法について説明します。 ビルドが成功すると、カスタム MSBuild プロジェクトファイルのロジックを使用してソリューションが配置されます。

**CI およびデプロイのビルド定義を作成するには**

1. Visual Studio 2010 の **[チームエクスプローラー]** ウィンドウで、チームプロジェクトノードを展開し、 **[ビルド]** を右クリックして、 **[新しいビルド定義]** をクリックします。

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. **[全般]** タブで、ビルド定義に名前 ( **deploytotest**など) とオプションの説明を指定します。
3. **[トリガー]** タブで、新しいビルドをトリガーする条件を選択します。 たとえば、開発者が新しいコードをチェックインするたびにソリューションをビルドしてテスト環境に配置する場合は、 **[継続的インテグレーション]** を選択します。
4. **[ビルドの既定値]** タブで、 **[ビルド出力を次の格納フォルダーにコピーする]** ボックスに、格納フォルダーの汎用名前付け規則 (UNC) パス (たとえば、 **\\TFSBUILD\Drops**) を入力します。

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > この格納場所には、構成する保持ポリシーに応じて複数のビルドが格納されます。 特定のビルドからステージング環境または運用環境に配置アーティファクトを発行する場合は、ここで確認できます。
5. **[プロセス]** タブの **[ビルドプロセスファイル]** ドロップダウンリストで、 **[defaulttemplate .xaml]** を選択したままにします。 これは、すべての新しいチームプロジェクトに追加される既定のビルドプロセステンプレートの1つです。
6. **[ビルドプロセスパラメーター]** テーブルで、 **[ビルドする項目]** 行をクリックし、**省略記号**ボタンをクリックします。

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. **[ビルドする項目]** ダイアログボックスで、 **[追加]** をクリックします。
8. ソリューションファイルの場所を参照し、[ **OK]** をクリックします。

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. **[ビルドする項目]** ダイアログボックスで、 **[追加]** をクリックします。
10. **[項目の種類]** ボックスの一覧で、 **[MSBuild プロジェクトファイル]** を選択します。
11. デプロイプロセスを制御するカスタムプロジェクトファイルの場所を参照し、ファイルを選択して、[ **OK]** をクリックします。

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. **[ビルドする項目]** ダイアログボックスに2つの項目が表示されるようになりました。 **[OK]** をクリックします。

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. **[プロセス]** タブの **[ビルドプロセスパラメーター]** テーブルで、 **[詳細設定**] セクションを展開します。
14. **[Msbuild 引数]** 行に、ビルドする項目の*いずれか*に必要な msbuild コマンドライン引数を追加します。 Contact Manager ソリューションのシナリオでは、次の引数が必要です。

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. 次の点に注意してください。

    1. Contact Manager ソリューションをビルドする場合は、 **Deployonbuild = true**および**deploytarget = package**引数が必要です。 これにより、「 [Web アプリケーションプロジェクトのビルドおよびパッケージ化](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)」で説明されているように、各 web アプリケーションプロジェクトをビルドした後に、web 配置パッケージを作成するよう MSBuild に指示します。
    2. **TargetEnvPropsFile**引数は、 *Publish*ファイルをビルドするときに必要です。 このプロパティは、「[ビルドプロセスについ](../web-deployment-in-the-enterprise/understanding-the-build-process.md)て」で説明されているように、環境固有の構成ファイルの場所を示します。
16. **[保持ポリシー]** タブで、必要に応じて保持する各種類のビルド数を構成します。
17. **[保存]** をクリックします。

## <a name="queue-a-build"></a>ビルドをキューに配置する

この時点で、少なくとも1つの新しいビルド定義が作成されています。 これで、定義したビルドプロセスが、ビルド定義で指定したトリガーに従って実行されるようになります。

CI を使用するようにビルド定義を構成した場合は、次の2つの方法でビルド定義をテストできます。

- 一部のコンテンツをチームプロジェクトにチェックインして、自動ビルドをトリガーします。
- ビルドを手動でキューに置いてください。

**ビルドを手動でキューに作成するには**

1. **[チームエクスプローラー]** ウィンドウで、ビルド定義を右クリックし、 **[新しいビルドをキューに追加]** をクリックします。

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. **[ビルドのキュー]** ダイアログボックスで、ビルドのプロパティを確認し、 **[キュー]** をクリックします。

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

手動でトリガーされたかどうかに&#x2014;関係なく、ビルドの進行状況と結果&#x2014;を確認するには、 **[チームエクスプローラー]** ウィンドウでビルド定義をダブルクリックします。 これにより、 **[ビルドエクスプローラー]** タブが開きます。

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

ここから、失敗したビルドのトラブルシューティングを行うことができます。 個々のビルドをダブルクリックすると、概要情報を表示したり、詳細なログファイルまでクリックしたりできます。

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

この情報を使用して、失敗したビルドをトラブルシューティングし、問題が解決されてから別のビルドを試みることができます。

> [!NOTE]
> 配置ロジックを実行するビルドは、対象となる環境で必要なアクセス許可をビルドサーバーに付与するまで、失敗する可能性があります。 詳細については、「[チームビルドの配置のアクセス許可を構成する](configuring-permissions-for-team-build-deployment.md)」を参照してください。

## <a name="monitor-the-build-process"></a>ビルドプロセスを監視する

TFS には、ビルドプロセスを監視するのに役立つさまざまな機能が用意されています。 たとえば、TFS は、ビルドが完了すると、タスクバーの通知領域に電子メールを送信したり、警告を表示したりできます。 詳細については、「[ビルドの実行と監視](https://msdn.microsoft.com/library/ms181721.aspx)」を参照してください。

## <a name="conclusion"></a>まとめ

このトピックでは、TFS でビルド定義を作成する方法について説明します。 ビルド定義は CI 用に構成されているため、開発者がチームプロジェクトにコンテンツをチェックインするたびにビルドプロセスが実行されます。 ビルド定義により、カスタム MSBuild プロジェクトファイルが実行され、web パッケージとデータベーススクリプトが対象サーバー環境に配置されます。

自動配置をビルドプロセスの一部として成功させるには、ターゲット web サーバーとターゲットデータベースサーバーのビルドサービスアカウントに適切なアクセス許可を付与する必要があります。 このチュートリアルの最後のトピック「[チームビルドの配置に対するアクセス許可の構成](configuring-permissions-for-team-build-deployment.md)」では、チームビルドサーバーからの自動配置に必要なアクセス許可を識別および構成する方法について説明します。

## <a name="further-reading"></a>参考資料

ビルド定義の作成の詳細については、「[基本的なビルド定義の作成](https://msdn.microsoft.com/library/ms181716.aspx)」および「[ビルドプロセスの定義](https://msdn.microsoft.com/library/ms181715.aspx)」を参照してください。 ビルドをキューに追加する方法の詳細については、「[ビルドをキュー](https://msdn.microsoft.com/library/ms181722.aspx)に入れ」を参照してください。

> [!div class="step-by-step"]
> [前へ](configuring-a-tfs-build-server-for-web-deployment.md)
> [次へ](deploying-a-specific-build.md)

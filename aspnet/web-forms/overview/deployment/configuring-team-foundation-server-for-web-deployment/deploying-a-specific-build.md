---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: 特定のビルドを配置する |Microsoft Docs
author: jrjlee
description: このトピックでは、ステージングまたは実稼働 enviro など、特定の以前のビルドから新しい変換先に web パッケージとデータベーススクリプトを配置する方法について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: 6bede6b36c24ade928ab052e14daec1e017bd0b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519574"
---
# <a name="deploying-a-specific-build"></a>特定のビルドを配置する

[Jason Lee](https://github.com/jrjlee)

[[Download PDF]\(PDF をダウンロード\)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> このトピックでは、ステージング環境や運用環境など、特定の以前のビルドから新しい変換先に web パッケージとデータベーススクリプトを配置する方法について説明します。

このトピックでは、Fabrikam, Inc. という架空の企業のエンタープライズ展開要件に基づいて、一連のチュートリアルの一部を説明します。このチュートリアルシリーズでは、&#x2014; [Contact Manager ソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;のサンプルソリューションを使用して、ASP.NET MVC 3 アプリケーション、Windows Communication Foundation (WCF) サービス、データベースプロジェクトなど、現実的なレベルの複雑さを持つ web アプリケーションを表します。

これらのチュートリアルの中核となる配置方法は、「プロジェクト[ファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」で説明されている分割プロジェクトファイルアプローチに基づいています。この方法で&#x2014;は、ビルドおよび配置プロセスは、すべての変換先環境に適用されるビルド命令を含む2つのプロジェクトファイルと、環境固有のビルドと配置の設定を含んでいます。 ビルド時に、環境固有のプロジェクトファイルが環境に依存しないプロジェクトファイルにマージされ、ビルド命令の完全なセットが形成されます。

## <a name="task-overview"></a>タスクの概要

これまでは、このチュートリアルでは、シングルステップまたは自動化されたプロセスの一部として、web アプリケーションとデータベースを構築、パッケージ化、および配置する方法に重点を置いています。 ただし、いくつかの一般的なシナリオでは、ドロップフォルダー内のビルドの一覧から配置するリソースを選択する必要があります。 つまり、最新のビルドが配置するビルドではない可能性があります。

前のトピック「[配置をサポートするビルド定義の作成](creating-a-build-definition-that-supports-deployment.md)」で説明した継続的インテグレーション (CI) シナリオを検討してください。 Team Foundation Server (TFS) 2010 でビルド定義を作成しました。 開発者がコードを TFS にチェックインするたびに、チームビルドはコードをビルドし、ビルドプロセスの一部として web パッケージとデータベーススクリプトを作成し、単体テストを実行して、リソースをテスト環境に配置します。 ビルド定義の作成時に構成した保持ポリシーに応じて、TFS は以前のビルドの数を保持します。

![](deploying-a-specific-build/_static/image1.png)

ここで、テスト環境でこれらのビルドのいずれかに対して検証と検証のテストを実行し、アプリケーションをステージング環境に配置する準備ができたとします。 それまでの間、開発者は新しいコードをチェックインした可能性があります。 ソリューションをリビルドしてステージング環境に配置する必要はなく、ステージング環境に最新のビルドを配置する必要もありません。 代わりに、テストサーバーで検証および検証した特定のビルドを配置します。

これを実現するには、Microsoft Build Engine (MSBuild) に対して、特定のビルドが生成した web パッケージとデータベーススクリプトの検索先を指定する必要があります。

## <a name="overriding-the-outputroot-property"></a>OutputRoot プロパティのオーバーライド

[サンプルソリューション](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)では、 *Publish*ファイルは**outputroot**という名前のプロパティを宣言します。 名前が示すように、これは、ビルドプロセスが生成するすべてのものを含むルートフォルダーです。 *Publish*ファイルで、 **outputroot**プロパティがすべてのデプロイリソースのルートの場所を参照していることを確認できます。

> [!NOTE]
> **Outputroot**は、一般的に使用されるプロパティ名です。 またC# 、ビジュアルおよび Visual Basic プロジェクトファイルは、すべてのビルド出力のルートの場所を格納するために、このプロパティを宣言します。

[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]

プロジェクトファイルで、以前の TFS ビルド&#x2014;&#x2014;の出力のように、別の場所から web パッケージとデータベーススクリプトを配置する場合は、単に**outputroot**プロパティをオーバーライドする必要があります。 プロパティ値は、チームビルドサーバーの関連するビルドフォルダーに設定する必要があります。 コマンドラインから MSBuild を実行していた場合は、コマンドライン引数として**Outputroot**の値を指定できます。

[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]

ただし、実際には、ビルド出力を使用する予定がない&#x2014;場合は、ビルドターゲットをスキップするだけで、ソリューションをビルドすることはできません。 これを行うには、コマンドラインから実行するターゲットを指定します。

[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]

ただし、ほとんどの場合は、TFS ビルド定義に配置ロジックをビルドします。 これにより、**キュービルド**アクセス許可を持つユーザーは、TFS サーバーへの接続を使用して Visual Studio のインストールから配置をトリガーできます。

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a>特定のビルドを配置するためのビルド定義の作成

次の手順では、ユーザーが1つのコマンドでステージング環境への配置をトリガーできるようにするビルド定義を作成する方法について説明します。

この場合、カスタムプロジェクトファイルで配置ロジックを実行するために&#x2014;必要なものをビルド定義に実際に作成する必要はありません。 *Publish*ファイルには、ファイルがチームビルドで実行されている場合に**ビルド**ターゲットをスキップする条件付きロジックが含まれています。 これを行うには、組み込みの**BuildingInTeamBuild**プロパティを評価します。これは、チームビルドでプロジェクトファイルを実行すると、自動的に**true**に設定されます。 その結果、ビルドプロセスをスキップし、単にプロジェクトファイルを実行して既存のビルドを配置することができます。

**手動で配置をトリガーするビルド定義を作成するには**

1. Visual Studio 2010 の **[チームエクスプローラー]** ウィンドウで、チームプロジェクトノードを展開し、 **[ビルド]** を右クリックして、 **[新しいビルド定義]** をクリックします。

    ![](deploying-a-specific-build/_static/image2.png)
2. **[全般]** タブで、ビルド定義に名前 ( **deploytostaging**など) とオプションの説明を指定します。
3. **[トリガー]** タブで、 **[手動-チェックインで新しいビルドをトリガーしない]** を選択します。
4. **[ビルドの既定値]** タブで、 **[ビルド出力を次の格納フォルダーにコピーする]** ボックスに、格納フォルダーの汎用名前付け規則 (UNC) パス (たとえば、 **\\TFSBUILD\Drops**) を入力します。

    ![](deploying-a-specific-build/_static/image3.png)
5. **[プロセス]** タブの **[ビルドプロセスファイル]** ドロップダウンリストで、 **[defaulttemplate .xaml]** を選択したままにします。 これは、すべての新しいチームプロジェクトに追加される既定のビルドプロセステンプレートの1つです。
6. **[ビルドプロセスパラメーター]** テーブルで、 **[ビルドする項目]** 行をクリックし、**省略記号**ボタンをクリックします。

    ![](deploying-a-specific-build/_static/image4.png)
7. **[ビルドする項目]** ダイアログボックスで、 **[追加]** をクリックします。
8. **[項目の種類]** ボックスの一覧で、 **[MSBuild プロジェクトファイル]** を選択します。
9. デプロイプロセスを制御するカスタムプロジェクトファイルの場所を参照し、ファイルを選択して、[ **OK]** をクリックします。

    ![](deploying-a-specific-build/_static/image5.png)
10. **[ビルドする項目]** ダイアログボックスで、[ **OK]** をクリックします。
11. **[ビルドプロセスパラメーター]** テーブルで、 **[詳細設定**] セクションを展開します。
12. **[MSBuild 引数]** 行で、環境固有のプロジェクトファイルの場所を指定し、ビルドフォルダーの場所のプレースホルダーを追加します。

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > ビルドをキューに置きたびに、 **Outputroot**値をオーバーライドする必要があります。 これについては、次の手順で説明します。
13. **[保存]** をクリックします。

ビルドをトリガーするときに、配置するビルドを指すように**Outputroot**プロパティを更新する必要があります。

**ビルド定義から特定のビルドを配置するには**

1. **[チームエクスプローラー]** ウィンドウで、ビルド定義を右クリックし、 **[新しいビルドをキューに追加]** をクリックします。

    ![](deploying-a-specific-build/_static/image7.png)
2. **[キュービルド]** ダイアログボックスの **[パラメーター]** タブで、 **[詳細設定]** セクションを展開します。
3. **[MSBuild 引数]** 行で、 **outputroot**プロパティの値をビルドフォルダーの場所に置き換えます。 次に例を示します。

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > ビルドフォルダーへのパスの末尾には、末尾にスラッシュを含めてください。
4. **[キュー]** をクリックします。

ビルドをキューに配置すると、プロジェクトファイルによって、 **Outputroot**プロパティに指定したビルド格納フォルダーからデータベーススクリプトと web パッケージが配置されます。

## <a name="conclusion"></a>まとめ

このトピックでは、split project file デプロイモデルを使用して、特定の以前のビルドから web パッケージやデータベーススクリプトなどのデプロイリソースを発行する方法について説明します。 ここでは、 **Outputroot**プロパティをオーバーライドする方法と、配置ロジックを TFS ビルド定義に組み込む方法について説明しました。

## <a name="further-reading"></a>参考資料

ビルド定義の作成の詳細については、「[基本的なビルド定義の作成](https://msdn.microsoft.com/library/ms181716.aspx)」および「[ビルドプロセスの定義](https://msdn.microsoft.com/library/ms181715.aspx)」を参照してください。 ビルドをキューに追加する方法の詳細については、「[ビルドをキュー](https://msdn.microsoft.com/library/ms181722.aspx)に入れ」を参照してください。

> [!div class="step-by-step"]
> [前へ](creating-a-build-definition-that-supports-deployment.md)
> [次へ](configuring-permissions-for-team-build-deployment.md)

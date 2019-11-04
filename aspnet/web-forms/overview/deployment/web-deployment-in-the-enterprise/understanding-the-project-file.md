---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: プロジェクトファイルについてMicrosoft Docs
author: jrjlee
description: ビルドと配置のプロセスの中核となるのは、Microsoft Build Engine (MSBuild) プロジェクトファイルです。 このトピックでは、まず MSBuild の概要について説明します。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 419fe51aaf65bddcc2c50380f099f842a8d9439c
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445691"
---
# <a name="understanding-the-project-file"></a>プロジェクトファイルについて

[Jason Lee](https://github.com/jrjlee)

[PDF のダウンロード](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> ビルドと配置のプロセスの中核となるのは、Microsoft Build Engine (MSBuild) プロジェクトファイルです。 このトピックでは、まず MSBuild とプロジェクトファイルの概念的な概要について説明します。 ここでは、プロジェクトファイルを操作するときに使用する主要なコンポーネントについて説明します。また、プロジェクトファイルを使用して実際のアプリケーションを配置する方法の例を示します。
> 
> 学習内容:
> 
> - MSBuild が MSBuild プロジェクトファイルを使用してプロジェクトをビルドする方法。
> - MSBuild をインターネットインフォメーションサービス (IIS) Web 配置ツール (Web 配置) などの展開テクノロジと統合する方法について説明します。
> - プロジェクトファイルの主要なコンポーネントを理解する方法。
> - プロジェクトファイルを使用して複雑なアプリケーションをビルドおよび配置する方法について説明します。

## <a name="msbuild-and-the-project-file"></a>MSBuild とプロジェクトファイル

Visual Studio でソリューションを作成してビルドすると、Visual Studio は MSBuild を使用してソリューション内の各プロジェクトをビルドします。 すべてのC# Visual Studio プロジェクトには、MSBuild プロジェクトファイルが含まれています。ファイル拡張子&#x2014;は、プロジェクト (.csproj)、Visual Basic.NET プロジェクト (.vbproj)、またはデータベースプロジェクト (.dbproj) などのプロジェクトの種類を反映しています。 プロジェクトをビルドするには、MSBuild がプロジェクトに関連付けられているプロジェクトファイルを処理する必要があります。 プロジェクトファイルは、MSBuild がプロジェクトをビルドするために必要なすべての情報と手順を含む XML ドキュメントです。これには、含めるコンテンツ、プラットフォーム要件、バージョン管理情報、web サーバーまたはデータベースサーバーの設定、実行する必要があるタスク。

MSBuild プロジェクトファイルは[MSBUILD XML スキーマ](/visualstudio/msbuild/msbuild-project-file-schema-reference)に基づいており、その結果、ビルドプロセスは完全にオープンで透過的になります。 また、msbuild エンジン&#x2014;を使用するために Visual Studio をインストールする必要はありません。 msbuild.exe 実行可能ファイルは .NET Framework に含まれており、コマンドプロンプトから実行できます。 開発者は、MSBuild XML スキーマを使用して独自の MSBuild プロジェクトファイルを作成し、プロジェクトのビルドと配置の方法を洗練された詳細な制御を行うことができます。 これらのカスタムプロジェクトファイルは、Visual Studio によって自動的に生成されるプロジェクトファイルとまったく同じ方法で動作します。

> [!NOTE]
> MSBuild プロジェクトファイルは、Team Foundation Server (TFS) のチームビルドサービスと共に使用することもできます。 たとえば、継続的インテグレーション (CI) シナリオでプロジェクトファイルを使用すると、新しいコードがチェックインされたときにテスト環境への配置を自動化できます。 詳細については、「[自動 Web 展開の Team Foundation Server の構成](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)」を参照してください。

### <a name="project-file-naming-conventions"></a>プロジェクトファイルの名前付け規則

独自のプロジェクトファイルを作成する場合は、任意のファイル拡張子を使用できます。 ただし、ソリューションを他のユーザーが理解しやすいようにするには、次の一般的な規則を使用する必要があります。

- プロジェクトをビルドするプロジェクトファイルを作成する場合は、proj 拡張子を使用します。
- 他のプロジェクトファイルにインポートする再利用可能なプロジェクトファイルを作成する場合は、.targets 拡張子を使用します。 .Targets 拡張子の付いたファイルは、通常は何もビルドしません。これには、proj ファイルにインポートできる指示が含まれているだけです。

### <a name="integration-with-deployment-technologies"></a>展開テクノロジとの統合

ASP.NET web applications や ASP.NET MVC web アプリケーションのように、Visual Studio 2010 で web アプリケーションプロジェクトを操作したことがある場合、これらのプロジェクトには、web アプリケーションをパッケージ化してターゲット環境に配置するための組み込みサポートが含まれていることがわかります。 これらのプロジェクトの**プロパティ**ページには、アプリケーションのコンポーネントのパッケージ化と配置の方法を構成するために使用できる **[Web のパッケージ化/発行]** タブと **[SQL のパッケージ化/発行]** タブがあります。 [Web の**パッケージ化/発行**] タブが表示されます。

![](understanding-the-project-file/_static/image1.png)

これらの機能の背後にある基になるテクノロジは、Web 発行パイプライン (WPP) と呼ばれます。 WPP は基本的に、MSBuild と[Web 配置](https://go.microsoft.com/?linkid=9805122)を統合して、Web アプリケーションの完全なビルド、パッケージ、および配置プロセスを提供します。

Web プロジェクト用のカスタムプロジェクトファイルを作成するときに、WPP によって提供される統合ポイントを利用できるという素晴らしいニュースがあります。 プロジェクトファイルに配置手順を含めることができます。これにより、プロジェクトのビルド、web 配置パッケージの作成、およびこれらのパッケージのリモートサーバーへのインストールを、1つのプロジェクトファイルと MSBuild の1回の呼び出しで行うことができます。 ビルドプロセスの一部として、他の実行可能ファイルを呼び出すこともできます。 たとえば、VSDBCMD コマンドラインツールを実行して、スキーマファイルからデータベースを配置できます。 このトピックでは、これらの機能を利用して、エンタープライズ展開シナリオの要件を満たす方法について説明します。

> [!NOTE]
> Web アプリケーションの配置プロセスのしくみの詳細については、「 [ASP.NET Web アプリケーションプロジェクトの配置の概要](https://msdn.microsoft.com/library/dd394698.aspx)」を参照してください。

## <a name="the-anatomy-of-a-project-file"></a>プロジェクトファイルの構造

ビルドプロセスの詳細を確認する前に、MSBuild プロジェクトファイルの基本的な構造について理解しておく必要があります。 このセクションでは、プロジェクトファイルを確認、編集、または作成するときに発生する一般的な要素の概要について説明します。 具体的には、次のことについて説明します。

- *プロパティ*を使用してビルド処理の変数を管理する方法。
- *項目*を使用してビルド処理の入力を識別する方法 (コードファイルなど)。
- *ターゲット*と*タスク*を使用して、プロジェクトファイル内の他の場所で定義された*プロパティ*と*項目*を使用して、MSBuild に実行命令を提供する方法。

これは、MSBuild プロジェクトファイル内のキー要素間の関係を示しています。

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a>Project 要素

[Project](https://msdn.microsoft.com/library/bcxfsh87.aspx)要素は、すべてのプロジェクトファイルのルート要素です。 **プロジェクト要素に**は、プロジェクトファイルの XML スキーマを識別するだけでなく、ビルドプロセスのエントリポイントを指定するための属性を含めることができます。 たとえば、 [Contact Manager サンプルソリューション](the-contact-manager-solution.md)では、" **fullpublish**" という名前のターゲットを呼び出すことによって、ビルドを開始する必要があることを指定し*ます。*

[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]

### <a name="properties-and-conditions"></a>プロパティと条件

プロジェクトファイルは、通常、プロジェクトを正常にビルドおよび配置するためにさまざまな情報を提供する必要があります。 これらの情報には、サーバー名、接続文字列、資格情報、ビルド構成、ソースとターゲットのファイルパス、およびカスタマイズをサポートするために必要なその他の情報が含まれます。 プロジェクトファイルでは、 [PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx)要素内でプロパティを定義する必要があります。 MSBuild プロパティは、キーと値のペアで構成されます。 **PropertyGroup**要素内では、要素名によってプロパティキーが定義され、要素の内容によってプロパティ値が定義されます。 たとえば、 **ServerName**および**ConnectionString**という名前のプロパティを定義して、静的サーバー名と接続文字列を格納できます。

[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]

プロパティ値を取得するには、 *$ (PropertyName)* という形式を使用します。 たとえば、 **ServerName**プロパティの値を取得するには、次のように入力します。

[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]

> [!NOTE]
> このトピックの後半で、プロパティ値を使用する方法とタイミングの例を紹介します。

プロジェクトファイルに静的なプロパティとして情報を埋め込むことは、常にビルドプロセスを管理するための理想的な方法ではありません。 さまざまなシナリオでは、他のソースから情報を取得したり、ユーザーがコマンドプロンプトから情報を提供できるようにしたりすることができます。 MSBuild では、コマンドラインパラメーターとして任意のプロパティ値を指定できます。 たとえば、ユーザーがコマンドラインから Msbuild.exe を実行するときに、 **ServerName**の値を指定できます。

[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]

> [!NOTE]
> Msbuild.exe で使用できる引数とスイッチの詳細については、「 [Msbuild コマンドラインリファレンス](https://msdn.microsoft.com/library/ms164311.aspx)」を参照してください。

同じプロパティ構文を使用して、環境変数と組み込みプロジェクトプロパティの値を取得できます。 よく使用される多くのプロパティが定義されており、関連するパラメーター名を含めることによってプロジェクトファイルで使用できます。 たとえば、&#x2014;現在のプロジェクトプラットフォーム ( **x86**や**AnyCpu**&#x2014;など) を取得するには、プロジェクトファイルに **$ (platform)** プロパティの参照を含めることができます。 詳細については、「[ビルドコマンドとプロパティのマクロ](https://msdn.microsoft.com/library/c02as0cs.aspx)」、「 [MSBuild プロジェクトの共通プロパティ](https://msdn.microsoft.com/library/bb629394.aspx)」、および「[予約済みのプロパティ](https://msdn.microsoft.com/library/ms164309.aspx)」を参照してください。

プロパティは、多くの場合、*条件*と組み合わせて使用されます。 ほとんどの MSBuild 要素は**Condition**属性をサポートしています。これにより、msbuild が要素を評価する条件を指定できます。 たとえば、次のプロパティ定義について考えてみます。

[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]

MSBuild がこのプロパティ定義を処理するときに、 **$ (Outputroot)** プロパティ値が使用可能かどうかを最初に確認します。 プロパティ値が空白&#x2014;の場合、ユーザーはこのプロパティ&#x2014;の値を指定していません。条件が**true**に評価され、プロパティ値がに設定され**ます。\** 発行します。ユーザーがこのプロパティの値を指定した場合、条件は**false**と評価され、静的なプロパティ値は使用されません。

条件を指定するさまざまな方法の詳細については、「 [MSBuild の条件](https://msdn.microsoft.com/library/7szfhaft.aspx)」を参照してください。

### <a name="items-and-item-groups"></a>項目と項目グループ

プロジェクトファイルの重要な役割の1つは、ビルドプロセスへの入力を定義することです。 通常、これらの入力は&#x2014;、ビルド処理の一部として処理またはコピーする必要があるファイルコードファイル、構成ファイル、コマンドファイル、およびその他のファイルです。 MSBuild プロジェクトスキーマでは、これらの入力は[項目](https://msdn.microsoft.com/library/ms164283.aspx)要素によって表されます。 プロジェクトファイルでは、 [ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx)要素内に項目を定義する必要があります。 **プロパティ**要素と同様に、**項目**要素には名前を自由に指定できます。 ただし、項目が表すファイルまたはワイルドカードを識別するには、 **Include**属性を指定する必要があります。

[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]

同じ名前の複数の**Item**要素を指定することで、リソースの名前付きリストを効果的に作成できます。 これを実際に確認するには、Visual Studio によって作成されたプロジェクトファイルの中から1つを見てみます。 たとえば、サンプルソリューションの*Contactmanager. .csproj*ファイルには、多数の項目グループが含まれており、それぞれに同じ名前の**項目**要素が複数あります。

[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]

このようにして、プロジェクトファイルは、ビルドを成功させるために必要なアセンブリが**参照**リストに&#x2014;含まれているのと同じ方法で処理する必要があるファイルのリストを構築するように MSBuild に指示します。 **[コンパイル]** の一覧にコードが含まれています。コンパイルが必要なファイルと**コンテンツ**の一覧には、変更せずにコピーする必要があるリソースが含まれます。 このトピックの後の方で、ビルドプロセスがこれらの項目を参照して使用する方法について説明します。

Item 要素には、 [Itemmetadata](https://msdn.microsoft.com/library/ms164284.aspx)子要素を含めることもできます。 これらは、ユーザー定義のキーと値のペアであり、基本的にその項目に固有のプロパティを表します。 たとえば、プロジェクトファイル内の**コンパイル**項目要素の大部分には、子要素の**依存**関係が含まれます。

[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]

> [!NOTE]
> ユーザーが作成したアイテムメタデータに加え、すべてのアイテムには、作成時にさまざまな共通メタデータが割り当てられます。 詳細については、「[既知の項目メタデータ](https://msdn.microsoft.com/library/ms164313.aspx)」を参照してください。

ルートレベルの**プロジェクト**要素内または特定の**ターゲット**要素内に**ItemGroup**要素を作成できます。 **ItemGroup**要素は**Condition**属性もサポートします。これにより、プロジェクト構成やプラットフォームなどの条件に従って、ビルドプロセスへの入力を調整できます。

### <a name="targets-and-tasks"></a>ターゲットとタスク

MSBuild スキーマでは、 [task](https://msdn.microsoft.com/library/77f2hx1s.aspx)要素は個々のビルド命令 (またはタスク) を表します。 MSBuild には、多数の定義済みタスクが含まれています。 (例:

- **コピー**タスクは、ファイルを新しい場所にコピーします。
- **Csc**タスクは、Visual C#コンパイラを呼び出します。
- **Vbc.exe**タスクは、Visual Basic コンパイラを呼び出します。
- **Exec**タスクは、指定されたプログラムを実行します。
- **メッセージ**タスクは、メッセージを logger に書き込みます。

> [!NOTE]
> すぐに使用できるタスクの詳細については、「 [MSBuild タスクリファレンス](https://msdn.microsoft.com/library/7z253716.aspx)」を参照してください。 独自のカスタムタスクを作成する方法など、タスクの詳細については、「 [MSBuild タスク](https://msdn.microsoft.com/library/ms171466.aspx)」を参照してください。

タスクは、常に[ターゲット](https://msdn.microsoft.com/library/t50z2hka.aspx)要素内に含まれている必要があります。 **Target**要素は、順番に実行される1つ以上のタスクのセットであり、プロジェクトファイルには複数のターゲットを含めることができます。 タスクまたは一連のタスクを実行する場合は、タスクを含むターゲットを呼び出します。 たとえば、メッセージをログに記録する単純なプロジェクトファイルがあるとします。

[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]

**/T**スイッチを使用してターゲットを指定することで、コマンドラインからターゲットを呼び出すことができます。

[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]

または、 **defaulttargets**属性を**Project**要素に追加して、呼び出すターゲットを指定することもできます。

[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]

この場合、コマンドラインからターゲットを指定する必要はありません。 プロジェクトファイルを指定するだけで、MSBuild は**Fullpublish**ターゲットを呼び出すことができます。

[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]

ターゲットとタスクには両方とも**条件**属性を含めることができます。 そのため、特定の条件が満たされた場合に、ターゲット全体または個々のタスクを除外することを選択できます。

一般に、便利なタスクとターゲットを作成する場合は、プロジェクトファイルの他の場所で定義したプロパティと項目を参照する必要があります。

- プロパティ値を使用するには、「 **$ (***propertyname***)** 」と入力します。ここで、 *propertyname*は**プロパティ**要素の名前、またはパラメーターの名前です。
- 項目を使用するには、「 **@ (***itemname***)** 」と入力します。ここで、 *itemname*は**item**要素の名前です。

> [!NOTE]
> 同じ名前で複数の項目を作成する場合は、リストを作成していることに注意してください。 これに対して、同じ名前で複数のプロパティを作成した場合、指定した最後のプロパティ値によって、&#x2014;同じ名前を持つ以前のプロパティが上書きされます。プロパティには、1つの値のみを含めることができます。

たとえば、サンプルソリューションの*Publish*ファイルで、 **buildprojects**ターゲットを見てみましょう。

[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]

このサンプルでは、次の重要なポイントを確認できます。

- **BuildingInTeamBuild**パラメーターが指定され、値が**true**の場合、このターゲット内のタスクは実行されません。
- ターゲットには、 [MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx)タスクの1つのインスタンスが含まれています。 このタスクを使用すると、他の MSBuild プロジェクトをビルドできます。
- **Projectstobuild**項目がタスクに渡されます。 この項目は、プロジェクトファイルまたはソリューションファイルの一覧を表すことができます。これは、項目グループ内の**Projectstobuild** item 要素によって定義されます。 この場合、 **Projectstobuild**項目は1つのソリューションファイルを参照します。

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- **MSBuild**タスクに渡されるプロパティ値には、 **Outputroot**および**Configuration**という名前のパラメーターが含まれます。 これらは、指定されている場合はパラメーター値に設定され、それ以外の場合は静的なプロパティ値に設定されます。

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

**MSBuild**タスクによって**ビルド**という名前のターゲットが呼び出されることもわかります。 これは、Visual Studio プロジェクトファイルで広く使用されているいくつかの組み込みターゲットの1つであり、**ビルド**、**クリーン**、**リビルド**、**発行**などのカスタムプロジェクトファイルで使用できます。 ターゲットとタスクを使用してビルドプロセスを制御する方法、特に**MSBuild**タスクについては、このトピックの後半で説明します。

> [!NOTE]
> ターゲットの詳細については、「 [MSBuild ターゲット](https://msdn.microsoft.com/library/ms171462.aspx)」を参照してください。

## <a name="splitting-project-files-to-support-multiple-environments"></a>複数の環境をサポートするためのプロジェクトファイルの分割

テストサーバー、ステージングプラットフォーム、運用環境などの複数の環境にソリューションを配置できるようにするとします。 構成は、サーバー名や接続文字列&#x2014;などの点だけでなく、資格情報、セキュリティ設定、およびその他の多くの要因の観点からも、非常に異なる場合があります。 これを定期的に実行する必要がある場合は、ターゲット環境を切り替えるたびにプロジェクトファイル内の複数のプロパティを編集するのは現実的ではありません。 また、ビルドプロセスに提供されるプロパティ値の無限のリストを必要とする理想的なソリューションでもありません。

幸いにも、別の方法があります。 MSBuild では、ビルド構成を複数のプロジェクトファイルに分割できます。 このしくみを確認するために、サンプルソリューションでは、次の2つのカスタムプロジェクトファイルがあることに注意してください。

- *Publish. proj*には、すべての環境に共通のプロパティ、項目、およびターゲットが含まれています。
- *Env-* 開発環境に固有のプロパティが含まれています。

次に、 *Publish*ファイルに[Import](https://msdn.microsoft.com/library/92x05xfs.aspx)要素が含まれていることを確認します。これは、**プロジェクト**の開始タグのすぐ下にあります。

[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]

**Import**要素は、現在の msbuild プロジェクトファイルに別の msbuild プロジェクトファイルの内容をインポートするために使用されます。 この場合、 **TargetEnvPropsFile**パラメーターを使用して、インポートするプロジェクトファイルのファイル名を指定します。 MSBuild を実行するときに、このパラメーターの値を指定できます。

[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]

これにより、2つのファイルの内容が効率的に1つのプロジェクトファイルにマージされます。 この方法を使用すると、ユニバーサルビルド構成を含む1つのプロジェクトファイルと、環境固有のプロパティを含む複数の補助プロジェクトファイルを作成できます。 その結果、別のパラメーター値を指定してコマンドを実行するだけで、ソリューションを別の環境に配置できます。

![](understanding-the-project-file/_static/image3.png)

この方法でプロジェクトファイルを分割することをお勧めします。 これにより、開発者は1つのコマンドを実行して複数の環境に配置できます。一方で、複数のプロジェクトファイル間でのユニバーサルビルドプロパティの重複を回避できます。

> [!NOTE]
> 独自のサーバー環境に合わせて環境固有のプロジェクトファイルをカスタマイズする方法については、「[ターゲット環境の配置プロパティの構成](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)」を参照してください。

## <a name="conclusion"></a>まとめ

このトピックでは、MSBuild プロジェクトファイルの概要について説明し、独自のカスタムプロジェクトファイルを作成してビルドプロセスを制御する方法について説明しました。 また、プロジェクトファイルをユニバーサルビルド命令と環境固有のビルドプロパティに分割するという概念が導入されました。これにより、複数の変換先にプロジェクトを簡単にビルドして配置することができます。

次のトピック「[ビルドプロセスについ](understanding-the-build-process.md)て」では、プロジェクトファイルを使用してビルドと配置を制御する方法について詳しく説明しています。これは、現実的なレベルの複雑さでソリューションをデプロイする方法を説明することによって行われます。

## <a name="further-reading"></a>関連項目

プロジェクトファイルと WPP の詳細については、「Microsoft Build Engine の内部」を参照してください[。: MSBuild と Team Foundation Build](http://amzn.com/0735645248) By 作成者 Iロウ Hashimi およびウィリアム Bartholomew、ISBN: 978-0-7356-4524-0。

> [!div class="step-by-step"]
> [前へ](setting-up-the-contact-manager-solution.md)
> [次へ](understanding-the-build-process.md)

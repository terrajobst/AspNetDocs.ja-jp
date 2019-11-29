---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
title: 'Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: プロジェクトプロパティの構成-4/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 8b013630-842c-4d44-a6fc-c6be43e7210f
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
msc.type: authoredcontent
ms.openlocfilehash: 6e63e75dca3d776fb9a1bd7e420ef48891daac69
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74569805"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-configuring-project-properties---4-of-12"></a>Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションの配置: プロジェクトプロパティの構成-4/12

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。 シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。

## <a name="overview"></a>の概要

一部の配置オプションは、プロジェクトファイル ( *.csproj*または *.vbproj*ファイル) に格納されているプロジェクトプロパティで構成されます。 ほとんどの場合、これらの設定の既定値は必要ですが、Visual Studio に組み込まれている**プロジェクトプロパティ**の UI を使用すると、これらの設定を変更する必要がある場合に、これらの設定を操作できます。 このチュートリアルでは、 **[プロジェクトのプロパティ]** で配置設定を確認します。 また、空のフォルダーを配置するプレースホルダーファイルも作成します。

## <a name="configuring-deployment-settings-in-the-project-properties-window"></a>プロジェクトの [プロパティ] ウィンドウでの配置設定の構成

次のチュートリアルで説明するように、デプロイ時の動作に影響するほとんどの設定が発行プロファイルに含まれています。 注意すべきいくつかの設定は、プロジェクトの **[プロパティ]** ウィンドウの [**パッケージ]/[発行**] タブにあります。 これらの設定は、各ビルド構成に対して指定されます。つまり、デバッグビルドの場合とは異なる設定をリリースビルドに対して使用できます。

**ソリューションエクスプローラー**で、 **ContosoUniversity**プロジェクトを右クリックし、 **[プロパティ]** をクリックして、 **[Web のパッケージ化/発行]** タブを選択します。

![Package_Publish_Web_tab](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image1.png)

ウィンドウが表示されると、既定では、ソリューションで現在アクティブになっているビルド構成の設定が表示されます。 **構成**ボックスが**アクティブ (リリース)** を示していない場合は、リリースビルド構成の設定を表示するために **[リリース]** を選択します。 テスト環境と運用環境の両方にリリースビルドを配置します。

![Package_Publish_Web_tab_selecting_Release](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image2.png)

**[アクティブ (リリース)]** または **[リリース]** を選択すると、リリースビルド構成を使用して配置するときに有効な値が表示されます。

- **[展開する項目]** ボックスで、**アプリケーションの実行に必要なファイルのみ**が選択されます。 その他のオプションとして、**このプロジェクトのすべてのファイル**または**このプロジェクトフォルダー内のすべてのファイル**があります。 既定の選択をそのままにしておくことで、ソースコードファイルを配置しないようにします (など)。 この設定は、SQL Server Compact バイナリファイルを含むフォルダーをプロジェクトに含める必要がある理由です。 この設定の詳細については、「 [ASP.NET Web アプリケーションプロジェクトの配置](https://msdn.microsoft.com/library/ee942158.aspx)に関する FAQ」の「**プロジェクトフォルダー内のすべてのファイルが配置されない理由**」を参照してください。
- 生成された**デバッグシンボルを除外**します。 このビルド構成を使用すると、デバッグは行われません。
- **[アプリ\_データフォルダーからファイルを除外する**] が選択されていません。 メンバーシップデータベースの SQL Server Compact ファイルはそのフォルダーにあり、配置する必要があります。 データベースの変更を含まない更新プログラムを展開する場合は、このチェックボックスをオンにします。
- **発行前にこのアプリケーションをプリコンパイル**します。 ほとんどのシナリオでは、web アプリケーションプロジェクトをプリコンパイルする必要はありません。 このオプションの詳細については、「[ [Web のパッケージ化/発行] タブ」、「プロジェクトのプロパティ」、](https://msdn.microsoft.com/library/dd410108(v=vs.110).aspx)および「[プリコンパイルの詳細設定」](https://msdn.microsoft.com/library/hh475319(v=vs.110).aspx)を参照してください。
- [ **Sql のパッケージ化/発行] タブで構成されているすべてのデータベースを含める**ことはできますが、このオプションは、[Sql の**パッケージ化/発行**] タブを構成していないため、無効になります。このタブは、SQL Server データベースを配置するための唯一のオプションとして使用されていた従来のデータベース配置方法を対象としています。 「 [SQL Server への移行](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)」チュートリアルの「 **SQL のパッケージ化/発行**」タブを使用します。
- これらのチュートリアルでワンクリック発行を使用しているため、 **[Web デプロイパッケージの設定]** セクションは適用されません。

**構成** ドロップダウンボックスを デバッグ に変更して、デバッグビルドの既定の設定を確認します。 値は同じです。ただし、[**生成されたデバッグシンボルを除外**する] をオフにすると、デバッグビルドを配置するときにデバッグできるようになります。

## <a name="making-sure-that-the-elmah-folder-gets-deployed"></a>Elmah フォルダーが展開されていることを確認する

前のチュートリアルで見たように、 [Elmah NuGet パッケージ](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)は、エラーのログ記録とレポートの機能を提供します。 Contoso 大学アプリケーションの Elmah は *、elmah という名前*のフォルダーにエラーの詳細を格納するように構成されています。

![Elmah フォルダー](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image3.png)

特定のファイルやフォルダーを展開から除外することは、一般的な要件です。別の例として、ユーザーがファイルをアップロードできるフォルダーがあります。 開発環境で作成されたログファイルやアップロードされたファイルを運用環境に配置する必要はありません。 また、運用環境に更新プログラムを展開する場合は、運用環境に存在するファイルを展開プロセスで削除する必要がありません。 (展開オプションの設定方法によっては、展開時に移行先サイトにファイルが存在し、ソースサイトには存在しない場合、Web 配置によって移行先から削除されます)。

このチュートリアルで既に説明したように、 **[パッケージ化/発行]** タブの **[配置する項目]** オプションは、**このアプリケーションを実行するために必要なファイルのみ**に設定されています。 その結果、Elmah によって開発されたログファイルは配置されません。これは、このような状況で発生します。 (配置するには、プロジェクトに含める必要があります。また、**ビルドアクション**プロパティを **[コンテンツ]** に設定する必要があります。 詳細については、「 [ASP.NET Web アプリケーションプロジェクトの配置](https://msdn.microsoft.com/library/ee942158.aspx)に関する FAQ」の「**プロジェクトフォルダー内のすべてのファイルが配置されない理由**」を参照してください。 ただし、コピーするファイルが少なくとも1つある場合を除き、Web 配置では、移行先サイトにフォルダーは作成されません。 そのため、フォルダーに *.txt*ファイルを追加して、フォルダーをコピーするようにプレースホルダーとして機能させることができます。

**ソリューションエクスプローラー**で、[ *Elmah* ] フォルダーを右クリックし、 **[新しい項目の追加]** を選択して、" *file.txt*" という名前のファイルを作成します。 "これはプレースホルダーファイルで、フォルダーが展開されることを確認します。" というテキストを入力します。 ファイルを保存します。 これで、Visual Studio でこのファイルとフォルダーが配置されていることを確認する必要があります。これは、 *.txt*ファイルの "**ビルドアクション**" プロパティが既定で **[コンテンツ]** に設定されているためです。

これで、すべてのデプロイのセットアップタスクが完了しました。 次のチュートリアルでは、Contoso 大学サイトをテスト環境にデプロイしてテストします。

> [!div class="step-by-step"]
> [前へ](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
> [次へ](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)

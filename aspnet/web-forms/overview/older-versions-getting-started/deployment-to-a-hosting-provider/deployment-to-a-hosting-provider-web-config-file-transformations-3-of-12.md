---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
title: 'Visual Studio または Visual Web Developer を使用して SQL Server Compact で ASP.NET Web アプリケーションをデプロイする: web.config ファイルの変換-3/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 2b0df3d9-450b-4ea6-b315-4c9650722cad
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
msc.type: authoredcontent
ms.openlocfilehash: fe71e6cfb0f4c5f1d99b326e9d90edb6c8c5feee
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600522"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-webconfig-file-transformations---3-of-12"></a>Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: web.config ファイルの変換-3/12

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。 シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。

## <a name="overview"></a>の概要

このチュートリアルでは、別の移行先環境に配置するときに web.config ファイルを変更するプロセスを自動化する方法について説明*します。* ほとんどのアプリケーションでは、アプリケーションの配置時に異なる必要がある設定が*web.config ファイルに*あります。 これらの変更を行うプロセスを自動化すると、を展開するたびに手動で行う必要がなくなります。これは面倒でエラーが発生しやすくなります。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config の変換と Web 配置パラメーター

*Web.config ファイル設定*の変更プロセスを自動化するには、web.config[変換](https://msdn.microsoft.com/library/dd465326.aspx)と[Web 配置パラメーター](https://msdn.microsoft.com/library/ff398068.aspx)の2つの方法があります。 Web.config*変換ファイル*には、配置時に*web.config ファイルを*変更する方法を指定する XML マークアップが含まれています。 特定のビルド構成および特定の発行プロファイルに対して異なる変更を指定できます。 既定のビルド構成はデバッグとリリースであり、カスタムビルド構成を作成できます。 通常、発行プロファイルは、配置先の環境に対応します。 (「[テスト環境として IIS に配置](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)する」チュートリアルの発行プロファイルの詳細については、「」を参照してください)。

Web 配置パラメーターを使用すると、 *web.config ファイルにある設定*を含め、配置時に構成する必要があるさまざまな種類の設定を指定できます。 *Web.config ファイルの*変更を指定するために使用する場合、Web 配置のパラメーターはより複雑になりますが、を配置するまで設定する値がわからない場合に便利です。 たとえば、エンタープライズ環境では、*展開パッケージ*を作成して、運用環境にインストールする it 部門のユーザーに付与することができます。また、そのユーザーは、不明な接続文字列またはパスワードを入力できる必要があります。

このチュートリアルで説明するシナリオで*は、web.config ファイルに*対して実行する必要があることがすべてわかっているので、Web 配置パラメーターを使用する必要はありません。 使用するビルド構成に応じて異なる変換をいくつか構成します。また、使用する発行プロファイルによって異なるものもあります。

## <a name="creating-transformation-files-for-publish-profiles"></a>発行プロファイルの変換ファイルの作成

**ソリューションエクスプローラー**で、[ *web.config] を展開し*て、2つの既定のビルド構成に対して既定で作成さ*れる、web.config および web.config* *の変換ファイル*を表示します。

![Config_transform_files](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image1.png)

カスタムビルド構成の変換ファイルを作成するには、web.config ファイルを右クリックし、コンテキストメニューから **[構成変換の追加]** を選択します。ただし、このチュートリアルでは、これを行う必要はありません。

ビルド構成ではなく、配置先に関連付けられた変更を構成するには、さらに2つの変換ファイルが必要です。 この種類の設定の典型的な例は、テストと運用環境で異なる WCF エンドポイントです。 後のチュートリアルでは、Test および Production という名前の発行プロファイルを作成し*ます。その*ため、web.config ファイルと*web.config ファイルが*必要です。

発行プロファイルに関連付けられている変換ファイルは、手動で作成する必要があります。 **ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[エクスプローラーでフォルダーを開く]** を選択します。

![Open_folder_in_Windows_Explorer](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image2.png)

**Windows エクスプローラー***で、web.config ファイルを*選択し、ファイルをコピーして、2つのコピーを貼り付けます。 これら*のコピーの名前を「web.config* 」*と「web.config*」に変更し、 **Windows エクスプローラー**を閉じます。

**ソリューションエクスプローラー**で、[**最新**の状態に更新] をクリックして新しいファイルを表示します。

新しいファイルを選択し、右クリックして、コンテキストメニューの **[プロジェクトに含める]** をクリックします。

![テストおよび運用構成ファイルをプロジェクトに含める](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image3.png)

これらのファイルが展開されないようにするには、**ソリューションエクスプローラー**でそれらを選択し、 **[プロパティ]** ウィンドウで、 **[ビルドアクション]** プロパティを **[コンテンツ]** から **[なし]** に変更します。 (ビルド構成に基づく変換ファイルは、自動的には配置されません)。

これ*で、* web.config 変換ファイルに web.config*を入力する*準備が整いました。

## <a name="limiting-error-log-access-to-administrators"></a>管理者へのエラーログアクセスの制限

アプリケーションの実行中にエラーが発生した場合は、システムによって生成されたエラーページの代わりに一般的なエラーページが表示され、エラーのログ記録とレポートには[Elmah NuGet パッケージ](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)が使用されます。 *Web.config ファイルの*`customErrors` 要素は、次のエラーページを指定します。

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample1.xml)]

エラーページを表示するには、`customErrors` 要素の `mode` 属性を一時的に "RemoteOnly" から "On" に変更し、Visual Studio からアプリケーションを実行します。 無効な URL ( *Studentsxxx*など) を要求することでエラーが発生します。 IIS によって生成された "ページが見つかりません" エラーページの代わりに、 *Genericerrorpage .aspx*ページが表示されます。

[![Error_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image5.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image4.png)

エラーログを表示するには、ポート番号の後の URL のすべてを、 *elmah* (スクリーンショットの例: `http://localhost:51130/elmah.axd`) に置き換えて、enter キーを押します。

[![Elmah_log_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image7.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image6.png)

完了したら、忘れずに `customErrors` 要素を "RemoteOnly" モードに戻してください。

開発用コンピューターでは、[エラーログ] ページに無料でアクセスできるようにすると便利ですが、運用環境ではセキュリティ上のリスクになります。 実稼働サイトでは、 *web.config ファイルに*変換を構成することによって、エラーログへのアクセスを管理者だけに制限する承認規則を追加できます。

Web.config*を開き、* 次に示すように、開始 `configuration` タグの直後に新しい `location` 要素を追加します。 (ここに示すように、コンテキストを提供するためだけに表示されている、`location` 要素だけを追加してください)。

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample2.xml?highlight=2-9)]

`Transform` 属性値 "Insert" により、この `location` 要素*は、web.config ファイル内*の既存の `location` 要素に兄弟として追加されます。 ( **[更新プログラムのクレジット]** ページの承認規則を指定する `location` 要素が既に1つあります)。デプロイ後に実稼働サイトをテストする場合は、この承認規則が有効であるかどうかをテストします。

テスト環境ではエラーログへのアクセスを制限する必要がないため、このコードを*web.config ファイルに*追加する必要はありません。

> [!NOTE] 
> 
> **セキュリティ**に関する注意実稼働アプリケーションのパブリックにエラーの詳細を表示しないようにするか、その情報をパブリックな場所に格納してください。 攻撃者は、エラー情報を使用してサイトの脆弱性を検出することができます。 独自のアプリケーションで ELMAH を使用する場合は、セキュリティリスクを最小限に抑えるために、ELMAH をどのように構成できるかを必ず調べてください。 このチュートリアルの ELMAH の例は、推奨される構成とは見なさないでください。 これは、アプリケーションがファイルを作成するために必要なフォルダーの処理方法を示すために選択された例です。

## <a name="setting-an-environment-indicator"></a>環境インジケーターの設定

一般的なシナリオと*して、web.config ファイルの*設定は、配置する環境ごとに異なる必要があります。 たとえば、WCF サービスを呼び出すアプリケーションでは、テスト環境と運用環境で異なるエンドポイントが必要になる場合があります。 Contoso 大学のアプリケーションにも、この種類の設定が含まれています。 この設定では、開発、テスト、運用など、どの環境が使用されているかを示す、サイトのページに表示されるインジケーターを制御します。 設定値は、アプリケーションが "(Dev)" または "(Test)" を、サイトのメインの見出しに追加するかどうかを決定し*ます。* マスターページ:

[![Environment_indicator](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image9.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image8.png)

アプリケーションが運用環境で実行されている場合、環境インジケーターは省略されます。

Contoso 大学の web ページでは、アプリケーションが実行されている環境を確認するため*に、web.config ファイルの*`appSettings` に設定されている値を読み取ります。

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample3.xml)]

この値は、テスト環境では "Test"、運用環境では "production" にする必要があります。

Web.config*を開き、* 前の手順で追加した `location` 要素の開始タグの直前に `appSettings` 要素を追加します。

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample4.xml)]

属性値 "SetAttributes" `xdt:Transform` は、この変換の目的が、 *web.config*ファイル内の既存の要素の属性値を変更することを示します。 `xdt:Locator` 属性値 "Match (キー)" は、変更される要素が、ここで指定された `key` 属性と一致する `key` 属性を持つ要素であることを示します。 `add` 要素の唯一の属性は `value`です。これは、配置された*web.config*ファイルで変更されます。 このコードにより、`Environment` `appSettings` 要素の `value` 属性が、実稼働環境に配置されている web.config ファイルで "production" に設定さ*れます。*

次に、同じ*変更を web.config ファイルに*適用します。ただし、`value` を "製品" ではなく "Test" に設定します。 完了すると、 *web.config*の `appSettings` セクションは次の例のようになります。

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample5.xml)]

## <a name="disabling-debug-mode"></a>無効化 (デバッグモードを)

リリースビルドでは、配置先の環境に関係なくデバッグを有効にしないようにします。 既定では *、web.config 変換ファイル*は、`compilation` 要素から `debug` 属性を削除するコードを使用して自動的に作成されます。

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample6.xml)]

`Transform` 属性を指定すると、リリースビルドを配置するたびに、配置された*web.config*ファイルの `debug` 属性が省略されます。

この変換は、リリース変換ファイルをコピーして作成したものであるため、テストおよび実稼働の変換ファイルにもあります。 このファイルを複製する必要はありません。そのため、各ファイルを開き、**コンパイル**要素を削除して、各ファイルを保存して閉じます。

## <a name="setting-connection-strings"></a>接続文字列の設定

ほとんどの場合、接続文字列の変換を設定する必要はありません。これは、発行プロファイルで接続文字列を指定できるためです。 ただし、SQL Server Compact データベースを配置するときに、Entity Framework Code First Migrations を使用して移行先サーバー上のデータベースを更新すると、例外が発生します。 このシナリオでは、データベーススキーマを更新するためにサーバーで使用される追加の接続文字列を指定する必要があります。 この変換を設定するには、 *web.config と web.config の両方の変換*ファイルで、 **&lt;構成**の開始&gt;タグの直後に **&lt;connectionStrings&gt;** 要素を追加します。

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample7.xml)]

`Transform` 属性は、配置された*web.config*ファイルの*connectionStrings*要素にこの接続文字列を追加することを指定します。 (発行プロセスでは、この追加の接続文字列が存在しない場合は自動的に作成されますが、既定では、 **providerName**属性は `System.Data.SqlClient`に設定されます。これは、SQL Server Compact に対しては機能しません。 接続文字列を手動で追加することによって、不適切なプロバイダー名を持つ接続文字列要素を作成しないようにすることができます。

これで、テストと運用のために Contoso 大学アプリケーションを展開するために必要なすべての*web.config 変換が*指定されました。 次のチュートリアルでは、プロジェクトのプロパティの設定を必要とする配置のセットアップタスクについて説明します。

## <a name="more-information"></a>その他の情報

このチュートリアルで説明しているトピックの詳細については、「 [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx)」の web.config 変換シナリオを参照してください。

> [!div class="step-by-step"]
> [前へ](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
> [次へ](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)

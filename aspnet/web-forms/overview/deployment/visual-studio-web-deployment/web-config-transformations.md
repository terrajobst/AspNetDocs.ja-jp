---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 'Visual Studio を使用した ASP.NET Web 配置: web.config ファイルの変換 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513712"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>Visual Studio を使用した ASP.NET Web 配置: web.config ファイル変換

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。 シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。

## <a name="overview"></a>概要

このチュートリアルでは、別の移行先環境に配置するときに web.config ファイルを変更するプロセスを自動化する方法について説明*します。* ほとんどのアプリケーションでは、アプリケーションの配置時に異なる必要がある設定が*web.config ファイルに*あります。 これらの変更を行うプロセスを自動化すると、を展開するたびに手動で行う必要がなくなります。これは面倒でエラーが発生しやすくなります。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](troubleshooting.md)を確認してください。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config の変換と Web 配置パラメーター

*Web.config ファイル設定*の変更プロセスを自動化するには、web.config[変換](https://msdn.microsoft.com/library/dd465326.aspx)と[Web 配置パラメーター](https://msdn.microsoft.com/library/ff398068.aspx)の2つの方法があります。 Web.config*変換ファイル*には、配置時に*web.config ファイルを*変更する方法を指定する XML マークアップが含まれています。 特定のビルド構成および特定の発行プロファイルに対して異なる変更を指定できます。 既定のビルド構成はデバッグとリリースであり、カスタムビルド構成を作成できます。 通常、発行プロファイルは、配置先の環境に対応します。 (「[テスト環境として IIS に配置](deploying-to-iis.md)する」チュートリアルの発行プロファイルの詳細については、「」を参照してください)。

Web 配置パラメーターを使用すると、 *web.config ファイルにある設定*を含め、配置時に構成する必要があるさまざまな種類の設定を指定できます。 *Web.config ファイルの*変更を指定するために使用する場合、Web 配置のパラメーターはより複雑になりますが、を配置するまで設定する値がわからない場合に便利です。 たとえば、エンタープライズ環境では、*展開パッケージ*を作成して、運用環境にインストールする it 部門のユーザーに付与することができます。また、そのユーザーは、不明な接続文字列またはパスワードを入力できる必要があります。

このチュートリアルシリーズで説明するシナリオで*は、web.config ファイルに*対して実行する必要があるすべてのことを事前に把握しているので、Web 配置パラメーターを使用する必要はありません。 使用するビルド構成に応じて異なる変換をいくつか構成します。また、使用する発行プロファイルによって異なるものもあります。

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>Azure での web.config 設定の指定

変更する*web.config ファイルの*設定が `<connectionStrings>` または `<appSettings>` 要素に含まれていて、Azure App Service で Web Apps するように配置している場合は、配置時に変更を自動化するためのもう1つのオプションがあります。 Web アプリの管理ポータルページの **[構成]** タブで、Azure で有効にする設定を入力できます ( **[アプリの設定]** セクションと **[接続文字列]** セクションまで下にスクロールします)。 プロジェクトをデプロイすると、Azure によって自動的に変更が適用されます。 詳細については、「 [Windows Azure websites: アプリケーション文字列と接続文字列のしくみ](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)」を参照してください。

## <a name="default-transformation-files"></a>既定の変換ファイル

**ソリューションエクスプローラー**で、[ *web.config] を展開し*て、2つの既定のビルド構成に対して既定で作成さ*れる、web.config および web.config* *の変換ファイル*を表示します。

![Config_transform_files](web-config-transformations/_static/image1.png)

カスタムビルド構成の変換ファイルを作成するには、web.config ファイルを右クリックし、コンテキストメニューの **[構成変換の追加]** をクリックします。 このチュートリアルでは、カスタムビルド構成を作成していないため、これを行う必要はありません。メニューオプションは無効になっています。

後で、3つの変換ファイルを作成します。1つはテスト、ステージング、および実稼働の各発行プロファイル用です。 発行プロファイル変換ファイルで処理する設定の典型的な例としては、移行先の環境によっては、テストと運用で異なる WCF エンドポイントがあります。 発行プロファイル変換ファイルは、後のチュートリアルで使用する発行プロファイルを作成した後で作成します。

## <a name="disable-debug-mode"></a>デバッグモードを無効にする

ターゲット環境ではなくビルド構成に依存する設定の例として、`debug` 属性があります。 リリースビルドでは、通常、デプロイ先の環境に関係なくデバッグを無効にする必要があります。 したがって、既定では、Visual Studio プロジェクトテンプレートは、`compilation` 要素から `debug` 属性を削除するコードを使用して、 *web.config 変換ファイルを作成します*。 既定の*web.config*は次のようになります。コメントアウトされたサンプル変換コードに加え、`debug` 属性を削除するコードが `compilation` 要素に含まれています。

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

`xdt:Transform="RemoveAttributes(debug)"` 属性は、配置された*web.config*ファイルの `system.web/compilation` 要素から `debug` 属性を削除することを指定します。 これは、リリースビルドを配置するたびに実行されます。

## <a name="limit-error-log-access-to-administrators"></a>管理者へのエラーログアクセスを制限する

アプリケーションの実行中にエラーが発生した場合、アプリケーションはシステムによって生成されたエラーページの代わりに一般的なエラーページを表示し、エラーのログ記録とレポートには[Elmah NuGet パッケージ](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)を使用します。 アプリケーションの*web.config*ファイルの `customErrors` 要素は、次のエラーページを指定します。

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

エラーページを表示するには、`customErrors` 要素の `mode` 属性を一時的に "RemoteOnly" から "On" に変更し、Visual Studio からアプリケーションを実行します。 無効な URL ( *Studentsxxx*など) を要求することでエラーが発生します。 IIS によって生成された "リソースが見つかりません" というエラーページが表示され、 *Genericerrorpage .aspx*ページが表示されます。

![[エラー] ページ](web-config-transformations/_static/image2.png)

エラーログを表示するには、ポート番号の後の URL のすべてを*elmah* (たとえば `http://localhost:51130/elmah.axd`) に置き換え、enter キーを押します。

![ELMAH ページ](web-config-transformations/_static/image3.png)

完了したら、忘れずに `customErrors` 要素を "RemoteOnly" モードに戻してください。

開発用コンピューターでは、[エラーログ] ページに無料でアクセスできるようにすると便利ですが、運用環境ではセキュリティ上のリスクになります。 運用サイトでは、管理者へのエラーログアクセスを制限する承認規則を追加し、その制限がテストとステージングにも必要であることを確認します。 このため、リリースビルドを配置するたびに実装する必要があるもう1つの変更があり、これ*は、web.config ファイルに*属しています。

次に示すように *、web.config を開き、* 終了 `configuration` タグの直前に新しい `location` 要素を追加します。

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

`Transform` 属性値 "Insert" により、この `location` 要素*は、web.config ファイル内*の既存の `location` 要素に兄弟として追加されます。 ( **[更新プログラムのクレジット]** ページの承認規則を指定する `location` 要素が既に1つあります)。

これで、変換をプレビューして、正しくコーディングされていることを確認できます。

**ソリューションエクスプローラー**で、 *[web.config] を右クリックし*、[変換の**プレビュー**] をクリックします。

![[変換のプレビュー] メニュー](web-config-transformations/_static/image4.png)

左側*に開発用の web.config ファイル*を表示するページが開き、変更が強調表示された状態で、配置された*web.config*ファイルが右側に表示されます。

![デバッグ変換のプレビュー](web-config-transformations/_static/image5.png)

![場所変換のプレビュー](web-config-transformations/_static/image6.png)

(プレビューでは、変換を記述しなかった追加の変更が発生する可能性があります。通常は、機能に影響しない空白を削除する必要があります)。

配置後にサイトをテストする場合は、承認規則が有効であることを確認するテストも行います。

> [!NOTE] 
> 
> **セキュリティ**に関する注意実稼働アプリケーションのパブリックにエラーの詳細を表示しないようにするか、その情報をパブリックな場所に格納してください。 攻撃者は、エラー情報を使用してサイトの脆弱性を検出することができます。 独自のアプリケーションで ELMAH を使用する場合は、セキュリティ上のリスクを最小限に抑えるように ELMAH を構成します。 このチュートリアルの ELMAH の例は、推奨される構成とは見なさないでください。 これは、アプリケーションがファイルを作成するために必要なフォルダーの処理方法を示すために選択された例です。 詳細については、「 [ELMAH エンドポイントのセキュリティ保護](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)」を参照してください。

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>発行プロファイル変換ファイルで処理する設定

一般的なシナリオと*して、web.config ファイルの*設定は、配置する環境ごとに異なる必要があります。 たとえば、WCF サービスを呼び出すアプリケーションでは、テスト環境と運用環境で異なるエンドポイントが必要になる場合があります。 Contoso 大学のアプリケーションにも、この種類の設定が含まれています。 この設定では、開発、テスト、運用など、どの環境が使用されているかを示す、サイトのページに表示されるインジケーターを制御します。 設定値は、アプリケーションが "(Dev)" または "(Test)" を、サイトのメインの見出しに追加するかどうかを決定し*ます。* マスターページ:

![環境インジケーター](web-config-transformations/_static/image7.png)

アプリケーションがステージング環境または運用環境で実行されている場合、環境インジケーターは省略されます。

Contoso 大学の web ページでは、アプリケーションが実行されている環境を確認するため*に、web.config ファイルの*`appSettings` に設定されている値を読み取ります。

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

この値は、テスト環境では "Test"、ステージング環境と運用環境では "運用" にする必要があります。

変換ファイルの次のコードは、この変換を実装します。

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

属性値 "SetAttributes" `xdt:Transform` は、この変換の目的が、 *web.config*ファイル内の既存の要素の属性値を変更することを示します。 `xdt:Locator` 属性値 "Match (キー)" は、変更される要素が、ここで指定された `key` 属性と一致する `key` 属性を持つ要素であることを示します。 `add` 要素の唯一の属性は `value`です。これは、配置された*web.config*ファイルで変更されます。 次に示すコードでは、`Environment` `appSettings` 要素の `value` 属性が、配置されている*web.config ファイルで*"Test" に設定されています。

この変換は、まだ作成していない発行プロファイル変換ファイルに属しています。 テスト環境、ステージング環境、および運用環境の発行プロファイルを作成するときに、この変更を実装する変換ファイルを作成および更新します。 これを行うには、[ [IIS に配置](deploying-to-iis.md)] および [[運用環境への配置](deploying-to-production.md)] チュートリアルを実行します。

> [!NOTE]
> この設定は `<appSettings>` 要素内にあるため、Azure App Service Web Apps をデプロイするときに変換を指定する別の方法として、このトピックで前述した「 [Azure での web.config 設定の指定](#watransforms)」を参照してください。

## <a name="setting-connection-strings"></a>接続文字列の設定

既定の変換ファイルには、接続文字列の更新方法を示す例が含まれていますが、ほとんどの場合、接続文字列の変換を設定する必要はありません。これは、発行プロファイルで接続文字列を指定できるためです。 これを行うには、[ [IIS に配置](deploying-to-iis.md)] および [[運用環境への配置](deploying-to-production.md)] チュートリアルを実行します。

## <a name="summary"></a>まとめ

これで、発行プロファイルを作成する前に*web.config の変換を*実行できるようになりました。また、配置した web.config ファイルに含まれる内容のプレビューが表示されました。

![場所変換のプレビュー](web-config-transformations/_static/image8.png)

次のチュートリアルでは、プロジェクトのプロパティの設定を必要とする配置のセットアップタスクについて説明します。

## <a name="more-information"></a>詳細情報

このチュートリアルで説明しているトピックの詳細については、「web.config の変換を使用して、[配置中に変換先の web.config ファイルまたは app.config ファイルの設定を変更する](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms)」を参照してください。

> [!div class="step-by-step"]
> [前へ](preparing-databases.md)
> [次へ](project-properties.md)

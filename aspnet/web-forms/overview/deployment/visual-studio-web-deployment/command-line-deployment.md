---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Visual Studio を使用した ASP.NET Web デプロイ: コマンドラインデプロイ |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512074"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a>Visual Studio を使用した ASP.NET Web デプロイ: コマンドライン展開

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。 シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。

## <a name="overview"></a>概要

このチュートリアルでは、コマンドラインから Visual Studio web 発行パイプラインを呼び出す方法について説明します。 これは、Visual Studio で手動ではなく、[ソースコードのバージョン管理システム](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)を使用して、[配置プロセスを自動化](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)する場合に便利です。

## <a name="make-a-change-to-deploy"></a>デプロイを変更する

現在、[バージョン情報] ページには、テンプレートコードが表示されます。

![テンプレートコードを使用したページの概要](command-line-deployment/_static/image1.png)

これを、学生登録の概要を表示するコードに置き換えます。

*About .aspx*ページを開き、`MainContent` `Content` 要素内のすべてのマークアップを削除し、その場所に次のマークアップを挿入します。

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

プロジェクトを実行し、 **[バージョン情報]** ページを選択します。

![About ページ](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a>コマンドラインを使用してテストに配置する

別のデータベースの変更を配置しないので、ContosoUniversity データベースの dbDacFx データベースの配置を無効にしてください。 Web の**発行**ウィザードを開き、3つの発行プロファイルのそれぞれで、 **[設定]** タブの **[データベースの更新]** チェックボックスをオフにします。

Windows 8 のスタートページで、 **VS2012 の開発者コマンドプロンプト**を検索します。

**VS2012 の [開発者コマンドプロンプト**] のアイコンを右クリックし、 **[管理者として実行]** をクリックします。

コマンドプロンプトで次のコマンドを入力し、ソリューションファイルへのパスをソリューションファイルへのパスに置き換えます。

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

MSBuild によってソリューションがビルドされ、テスト環境に配置されます。

![コマンド ライン出力](command-line-deployment/_static/image3.png)

ブラウザーを開き、`http://localhost/ContosoUniversity`にアクセスし、 **[バージョン情報]** ページをクリックして、展開が成功したことを確認します。

テストで学生を作成していない場合は、 **[Student Body Statistics]** \ (学生の本文 \) の見出しの下に空のページが表示されます。 **学生**のページにアクセスして、 **[学生の追加]** をクリックし、いくつかの学生を追加してから、 **[バージョン情報]** ページに戻って学生の統計情報を表示します。

![テスト環境のページについて](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a>キーのコマンドラインオプション

入力したコマンドによって、ソリューションファイルのパスと2つのプロパティが MSBuild に渡されました。

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a>ソリューションの配置と個々のプロジェクトの配置

ソリューションファイルを指定すると、ソリューション内のすべてのプロジェクトがビルドされます。 ソリューションに複数の web プロジェクトがある場合は、次の MSBuild 動作が適用されます。

- コマンドラインで指定したプロパティは、すべてのプロジェクトに渡されます。 したがって、各 web プロジェクトには、指定した名前の発行プロファイルが必要です。 `/p:PublishProfile=Test`を指定する場合、各 web プロジェクトには*Test*という名前の発行プロファイルが必要です。
- 1つのプロジェクトがビルドされない場合は、そのプロジェクトが正常に発行される可能性があります。 詳細については、「stackoverflow スレッド[MSBuild が2つのパッケージで失敗](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)する」を参照してください。

ソリューションではなく個々のプロジェクトを指定する場合は、Visual Studio のバージョンを指定するパラメーターを追加する必要があります。 Visual Studio 2012 を使用している場合、コマンドラインは次の例のようになります。

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

Visual Studio 2010 のバージョン番号は10.0 です。 詳細については、作成者 Hashimi のブログの「 [Visual Studio プロジェクトの互換性と VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) 」を参照してください。

### <a name="specifying-the-publish-profile"></a>発行プロファイルの指定

発行プロファイルは、次の例に示すように、名前または*pubxml*ファイルへの完全パスを使用して指定できます。

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a>コマンドライン発行でサポートされている Web 発行方法

コマンドライン発行では、次の3つの発行方法がサポートされています。

- `MSDeploy`-Web 配置を使用して発行します。
- `Package`-Web 配置パッケージを作成して発行します。 パッケージを作成する MSBuild コマンドとは別にパッケージをインストールする必要があります。
- `FileSystem`-指定したフォルダーにファイルをコピーして発行します。

### <a name="specifying-the-build-configuration-and-platform"></a>ビルド構成とプラットフォームの指定

ビルド構成とプラットフォームは、Visual Studio またはコマンドラインで設定する必要があります。 発行プロファイルには `LastUsedBuildConfiguration` と `LastUsedPlatform`という名前のプロパティが含まれますが、プロジェクトのビルド方法を決定するためにこれらのプロパティを設定することはできません。 詳細については、「MSBuild: 作成者 Hashimi のブログで[構成プロパティを設定する方法](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)」を参照してください。

## <a name="deploy-to-staging"></a>ステージングへのデプロイ

Azure にデプロイするには、コマンドラインにパスワードを追加する必要があります。 Visual Studio の発行プロファイルにパスワードを保存した場合、パスワードは暗号化された形式で*pubxml. user*ファイルに格納されていました。 このファイルは、コマンドラインの展開を行うときに MSBuild によってアクセスされることはないため、コマンドラインパラメーターでパスワードを渡す必要があります。

1. 以前にステージング web サイト用にダウンロードした *.publishsettings*ファイルから必要なパスワードをコピーします。 パスワードは、Web 配置 `publishProfile` 要素の `userPWD` 属性の値です。

    ![Web 配置パスワード](command-line-deployment/_static/image5.png)
2. Windows 8 のスタートページで、 **VS2012 の開発者コマンドプロンプト**を検索し、アイコンをクリックしてコマンドプロンプトを開きます。 (ローカルコンピューター上の IIS には展開されないため、この時点で管理者として開く必要はありません)。
3. コマンドプロンプトで次のコマンドを入力します。ソリューションファイルへのパスは、ソリューションファイルへのパスとパスワードで置き換えます。

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    このコマンドラインには、追加のパラメーターとして `/p:AllowUntrustedCertificate=true`が含まれていることに注意してください。 このチュートリアルの執筆中は、コマンドラインから Azure に発行するときに、`AllowUntrustedCertificate` のプロパティを設定する必要があります。 このバグの修正がリリースされた場合、そのパラメーターは必要ありません。
4. ブラウザーを開き、ステージングサイトの URL にアクセスし、 **[バージョン情報]** ページをクリックして、デプロイが成功したことを確認します。

    テスト環境で既に説明したように、 **[バージョン情報]** ページで統計を表示するには、いくつかの学生を作成する必要がある場合があります。

## <a name="deploy-to-production"></a>運用環境への配置

運用環境にデプロイするプロセスは、ステージングのプロセスに似ています。

1. 前の手順でダウンロードした *.publishsettings*ファイルから必要なパスワードをコピーします。
2. **VS2012 の開発者コマンドプロンプトを**開きます。
3. コマンドプロンプトで次のコマンドを入力します。ソリューションファイルへのパスは、ソリューションファイルへのパスとパスワードで置き換えます。

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    実際の運用サイトでも、データベースの変更があった場合は、通常、展開の前に*アプリ\_offline .htm*ファイルをサイトにコピーし、展開が正常に完了した後に削除します。
4. ブラウザーを開き、ステージングサイトの URL にアクセスし、 **[バージョン情報]** ページをクリックして、デプロイが成功したことを確認します。

## <a name="summary"></a>まとめ

これで、コマンドラインを使用してアプリケーションの更新プログラムが展開されました。

![テスト環境のページについて](command-line-deployment/_static/image6.png)

次のチュートリアルでは、web 発行パイプラインを拡張する方法の例を紹介します。 この例では、プロジェクトに含まれていないファイルを配置する方法を示します。

> [!div class="step-by-step"]
> [前へ](deploying-a-database-update.md)
> [次へ](deploying-extra-files.md)

---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 'Visual Studio を使用した ASP.NET Web デプロイ: 運用環境へのデプロイ |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: ddc3d15f0436c4c3a24491cf0377111768da67df
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74617643"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a>Visual Studio を使用した ASP.NET Web 配置: 運用環境への配置

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。 シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。

## <a name="overview"></a>の概要

このチュートリアルでは、Microsoft Azure アカウントを設定し、ステージング環境と運用環境を作成します。次に、Visual Studio のワンクリック発行機能を使用して、ステージング環境と運用環境に ASP.NET web アプリケーションをデプロイします。

必要に応じて、サードパーティのホスティングプロバイダーにデプロイすることもできます。 このチュートリアルで説明する手順のほとんどは、ホスティングプロバイダーまたは Azure の場合と同じですが、各プロバイダーには、アカウントと web サイト管理のための独自のユーザーインターフェイスが用意されています。 ホスティングプロバイダーは、Microsoft.com web サイトの[プロバイダーのギャラリー](https://www.microsoft.com/web/hosting)にあります。

リマインダー: チュートリアルを実行するときにエラーメッセージが表示されたり、機能しない場合は、このチュートリアルシリーズのトラブルシューティングのページを確認してください。

## <a name="get-a-microsoft-azure-account"></a>Microsoft Azure アカウントを取得する

まだ Azure アカウントを持っていない場合は、無料試用版アカウントを数分で作成できます。 詳細については、「 [Azure 無料試用版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)」を参照してください。

## <a name="create-a-staging-environment"></a>ステージング環境を作成する

> [!NOTE]
> このチュートリアルの執筆以来、ステージング環境と運用環境を作成するための多くのプロセスを自動化する新しい機能が追加されました Azure App Service。 「 [Azure App Service で web アプリのステージング環境を設定する](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/)」を参照してください。

「[テスト環境にデプロイする」チュートリアル](deploying-to-iis.md)で説明したように、最も信頼性の高いテスト環境は、実稼働 web サイトと同様に、ホスティングプロバイダーの web サイトです。 多くのホスティングプロバイダーでは、この利点と大幅な追加コストを比較する必要がありますが、Azure では、追加の無料 web アプリをステージングアプリとして作成できます。 また、データベースが必要であり、実稼働データベースを犠牲にした場合の追加費用は、[なし] または [最小] のどちらかになります。 Azure では、各データベースではなく、使用するデータベースストレージの量に対して課金されます。ステージングで使用する追加のストレージの量は最小限に抑えられます。

「[テスト環境にデプロイする」チュートリアル](deploying-to-iis.md)で説明したように、ステージング環境と運用環境では、2つのデータベースを1つのデータベースに配置します。 個別に保持する場合、プロセスは同じです。ただし、環境ごとに追加のデータベースを作成し、発行プロファイルを作成するときに、各データベースに対して正しい宛先文字列を選択する点が異なります。

チュートリアルのこのセクションでは、ステージング環境に使用する web アプリとデータベースを作成し、ステージング環境にデプロイしてテストしてから、運用環境にデプロイします。

> [!NOTE]
> 次の手順では、Azure 管理ポータルを使用して Azure App Service で web アプリを作成する方法について説明します。 Azure SDK の最新バージョンでは、サーバーエクスプローラーを使用して、Visual Studio を離れることなくこの操作を行うこともできます。 Visual Studio 2013 では、[発行] ダイアログから直接 web アプリを作成することもできます。 詳細については、「 [Azure App Service での ASP.NET web アプリの作成](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)」を参照してください。

1. [Azure 管理ポータル](https://manage.windowsazure.com/)で **[Websites]** をクリックし、 **[New]** をクリックします。
2. **[Web サイト]** をクリックし、 **[カスタム作成]** をクリックします。

    **新しい Web サイト-カスタム作成**ウィザードが開きます。 **カスタム作成**ウィザードを使用すると、web サイトとデータベースを同時に作成できます。
3. ウィザードの **[Web サイトの作成]** 手順で、アプリケーションのステージング環境の一意の url として使用する文字列を **[url]** ボックスに入力します。 たとえば、「ContosoUniversity-staging123」と入力します (ContosoUniversity の場合に一意になるように、末尾に乱数を含めます)。

    完全な URL は、ここで入力した内容に、テキストボックスの横に表示されるサフィックスを加えたものになります。
4. **[リージョン]** ドロップダウンリストで、ユーザーに最も近いリージョンを選択します。

    この設定では、web アプリが実行されるデータセンターを指定します。
5. **[データベース]** ドロップダウンリストで、 **[新しい SQL データベースの作成]** を選択します。
6. **[DB 接続文字列名]** ボックスに、既定値の*defaultconnection*をそのまま使用します。
7. ボックスの下部にある右矢印をクリックします。

    次の図は、サンプルの値を含む **[Web サイトの作成]** ダイアログを示しています。 入力した URL とリージョンは異なります。

    ![Web サイトの作成手順](deploying-to-production/_static/image1.png)

    ウィザードは、 **[データベースの設定の指定]** 手順に進みます。
8. **[名前]** ボックスに「 *ContosoUniversity* 」と入力し、たとえば「 *ContosoUniversity123*」と入力します。
9. **[サーバー]** ボックスで、 **[新しい SQL Database サーバー]** を選択します。
10. 管理者の名前とパスワードを入力します。

    ここには既存の名前とパスワードを入力していません。 後でデータベースにアクセスするときに使用するために定義する新しい名前とパスワードを入力します。
11. **[リージョン]** ボックスで、web アプリ用に選択したのと同じリージョンを選択します。

    Web サーバーとデータベースサーバーを同じリージョンに保持することで、最高のパフォーマンスが得られ、コストを最小限に抑えることができます。
12. 終了したことを示すには、ボックスの下部にあるチェックマークをクリックします。

    次の図は、 **[データベースの設定の指定]** ダイアログを示しています。 入力した値が異なる場合があります。

    ![新しい Web サイト-データベースを使用した作成ウィザードの [データベースの設定] 手順](deploying-to-production/_static/image2.png)

    管理ポータルが Websites ページに戻り、 **[状態]** 列に web アプリが作成されていることが示されます。 しばらくすると (通常は1分未満)、web アプリが正常に作成されたことが **[状態]** 列に表示されます。 左側のナビゲーションバーで、アカウントにある web アプリの数が**Websites**アイコンの横に表示され、 **[SQL データベース]** アイコンの横にデータベースの数が表示されます。

    ![管理ポータルの web サイトページ、作成された web サイト](deploying-to-production/_static/image3.png)

    Web アプリ名は、この図のサンプルアプリとは異なります。

## <a name="deploy-the-application-to-staging"></a>アプリケーションをステージングにデプロイする

ステージング環境用の web アプリとデータベースを作成したので、プロジェクトを配置できます。

> [!NOTE]
> 次の手順では、.publishsettings ファイルをダウンロードして発行プロファイルを作成する方法を説明*します。* このファイルは、Azure だけでなく、サードパーティのホスティングプロバイダーでも機能します。 最新の Azure SDK では、Visual Studio から Azure に直接接続し、Azure アカウントにある web アプリの一覧から選択することもできます。 Visual Studio 2013 では、 **[Web 発行]** ダイアログボックスまたは **[サーバーエクスプローラー]** ウィンドウから Azure にサインインできます。 詳細については、「 [Azure App Service での ASP.NET web アプリの作成](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)」を参照してください。

### <a name="download-the-publishsettings-file"></a>.Publishsettings ファイルをダウンロードします。

1. 先ほど作成した web アプリの名前をクリックします。

    ![ダッシュボードにアクセスするには、サイトをクリックします](deploying-to-production/_static/image4.png)
2. **[ダッシュボード]** タブの **[概要]** で、 **[発行プロファイルのダウンロード]** をクリックします。

    ![発行プロファイルのダウンロードのリンク](deploying-to-production/_static/image5.png)

    この手順では、web アプリにアプリケーションを配置するために必要なすべての設定を含むファイルをダウンロードします。 このファイルを Visual Studio にインポートすると、この情報を手動で入力する必要がなくなります。
3. Visual Studio からアクセスできるフォルダーに *.publishsettings*ファイルを保存します。

    ![.publishsettings ファイルを保存しています](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > セキュリティ- *.publishsettings*ファイルには、Azure サブスクリプションとサービスの管理に使用される資格情報 (エンコードされていない) が含まれています。 このファイルのセキュリティのベストプラクティスは、ソースディレクトリの外部 (たとえば、[ライブラリ] フォルダー内) に一時的に保存し、インポートが完了した後に削除することです。 悪意のあるユーザーが *.publishsettings*ファイルにアクセスすると、Azure サービスを編集、作成、削除できます。

### <a name="create-a-publish-profile"></a>発行プロファイルを作成する

1. Visual Studio で**ソリューションエクスプローラー**で ContosoUniversity プロジェクトを右クリックし、コンテキストメニューから **[発行]** を選択します。

    **Web の発行**ウィザードが開きます。
2. **[プロファイル]** タブをクリックします。
3. **[インポート]** をクリックします。
4. 前の手順でダウンロードした *.publishsettings*ファイルに移動し、 **[開く]** をクリックします。

    ![[発行設定のインポート] ダイアログボックス](deploying-to-production/_static/image7.png)
5. **[接続]** タブで、 **[接続の検証]** をクリックして、設定が正しいことを確認します。

    接続が検証されると、 **[接続の検証]** ボタンの横に緑色のチェックマークが表示されます。

    一部のホスティングプロバイダーでは、 **[接続の検証]** をクリックすると、 **[証明書のエラー]** ダイアログボックスが表示する場合があります。 その場合は、サーバー名が予期したとおりであることを確認します。 サーバー名が正しい場合は、 **[この証明書を Visual Studio の今後のセッション用に保存する]** を選択し、 **[同意]** する をクリックします。 (このエラーは、デプロイ先の URL に対して SSL 証明書を購入する費用が発生しないように、ホスティングプロバイダーによって選択されたことを意味します。 有効な証明書を使用してセキュリティで保護された接続を確立する場合は、ホスティングプロバイダーに問い合わせてください。)
6. [次へ] をクリックします。

    ![[接続] タブの [接続成功] アイコンと [次へ] ボタン](deploying-to-production/_static/image8.png)
7. **[設定]** タブで、 **[ファイル発行オプション]** を展開し、[**アプリ\_データフォルダーからファイルを除外する**] を選択します。

    **[ファイル発行オプション]** の他のオプションの詳細については、「 [IIS への展開](deploying-to-iis.md)」チュートリアルを参照してください。 この手順の結果と次のデータベース構成手順を示すスクリーンショットは、データベースの構成手順の最後にあります。
8. **[データベース]** セクションの **[defaultconnection]** で、メンバーシップデータベースのデータベースの配置を構成します。
9. 1. **[データベースの更新]** を選択します。

        **Defaultconnection**のすぐ下にある **[リモート接続文字列]** ボックスに、.publishsettings ファイルの接続文字列が入力されます。接続文字列には SQL Server 資格情報が含まれています。これは、 *pubxml*ファイルにプレーンテキストで格納されます。 完全に保存しない場合は、データベースをデプロイした後に発行プロファイルからそれらを削除し、代わりに Azure に保存することができます。 詳細については、Scott マン Selman のブログの[ソースから Azure へのデプロイ時に ASP.NET database 接続文字列を安全に保つ方法に](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx)関する記事をご覧ください。
      2. **[データベースの更新の構成]** をクリックします。
      3. **[データベースの更新の構成]** ダイアログボックスで、 **[SQL スクリプトの追加]** をクリックします。
      4. **[SQL スクリプトの追加]** ボックスで、ソリューションフォルダーの前の手順で保存した*aspnet-data-prod*スクリプトに移動し、 **[開く]** をクリックします。
      5. **[データベースの更新の構成]** ダイアログボックスを閉じます。
10. **[データベース]** セクションの **[schoolcontext.cs]** で、 **[Code First Migrations の実行 (アプリケーションの起動時に実行)]** を選択します。

    Visual Studio では、`DbContext` クラスの**更新データベース**ではなく**Execute Code First Migrations**が表示されます。 移行ではなく dbDacFx プロバイダーを使用して、`DbContext` クラスを使用してアクセスするデータベースを配置する場合は、「Visual Studio の Web 配置に関する FAQ」と MSDN の ASP.NET を参照し[Code First 操作方法](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations)てください。

    **[設定]** タブは、次の例のようになります。

    ![ステージングの [設定] タブ](deploying-to-production/_static/image9.png)
11. 次の手順を実行して、プロファイルを保存し、名前を「*ステージング*」に変更します。

    1. **[プロファイル]** タブをクリックし、 **[プロファイルの管理]** をクリックします。
    2. インポートによって、FTP 用と Web 配置用の2つの新しいプロファイルが作成されました。 Web 配置プロファイルを構成しました: このプロファイルの名前を*ステージング*に変更します。

        ![プロファイル名をステージングに変更](deploying-to-production/_static/image10.png)
    3. **[Web 発行プロファイルの編集]** ダイアログボックスを閉じます。
    4. Web の**発行**ウィザードを閉じます。

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a>環境インジケーターの発行プロファイルの変換を構成する

> [!NOTE]
> このセクションでは、環境インジケーターの web.config 変換を設定する方法について説明します。 インジケーターは `<appSettings>` 要素内にあるため、Azure App Service を配置するときに変換を指定する別の方法があります。 詳細については、「 [Azure での web.config 設定の指定](web-config-transformations.md#watransforms)」を参照してください。

1. **ソリューションエクスプローラー**で、 **[プロパティ]** 、 **[publishprofiles]** の順に展開します。
2. [ *Pubxml*] を右クリックし、 **[構成の変換の追加]** をクリックします。

    ![ステージング用の構成変換の追加](deploying-to-production/_static/image11.png)

    Visual *Studio によって、web.config 変換*ファイルが作成されて開きます。
3. *Web.config 変換ファイル*で、開始 `configuration` タグの直後に次のコードを挿入します。

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    ステージング発行プロファイルを使用すると、この変換によって環境インジケーターが "運用" に設定されます。 デプロイされた web アプリでは、"(Dev)" や "(Test)" などのサフィックスは "Contoso 大学" H1 見出しの後には表示されません。
4. *Web.config ファイルを*右クリックし、 **[変換のプレビュー]** をクリックして、コード化された変換によって予想される変更が生成されることを確認します。

    Web.config の**プレビュー**ウィンドウには、 *web.config 変換と* *web.config 変換の*両方を適用した結果が表示されます。

### <a name="prevent-public-use-of-the-test-app"></a>テストアプリが一般に使用されないようにする

ステージングアプリに関する重要な考慮事項は、インターネット上で公開されていても、パブリックに使用しないようにすることです。 ユーザーが見つけて使用する可能性を最小限に抑えるには、次の方法のうち1つ以上を使用します。

- ステージングアプリへのアクセスを許可するファイアウォール規則を、ステージングのテストに使用する IP アドレスからのみ設定します。
- 推測が不可能な難読化された URL を使用します。
- *Robots.txt*ファイルを作成して、検索エンジンがテストアプリとレポートリンクを検索結果にクロールしないようにします。

これらの方法のうちの1つは最も効果的ですが、このチュートリアルでは説明しません。 Azure App Service ではなく Azure クラウドサービスにデプロイする必要があるためです。 Azure での Cloud Services と IP の制限の詳細については、「 [azure によって提供されるコンピューティングホスティングオプション](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me)」を参照してください。また、[特定の Ip アドレスから Web ロールへのアクセスをブロックする](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx)ことができます。 サードパーティのホスティングプロバイダーにデプロイする場合は、プロバイダーに問い合わせて、IP 制限を実装する方法を確認してください。

このチュートリアルでは、 *robots.txt*ファイルを作成します。

1. **ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[新しい項目の追加]** をクリックします。
2. *Robots.txt*という名前の新しい**テキストファイル**を作成し、次のテキストを入力します。

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    `User-agent` 行は、ファイル内のルールがすべての検索エンジン web クローラー (ロボット) に適用されることを検索エンジンに通知します。また、`Disallow` 行は、サイトのページをクロールする必要がないことを指定します。

    検索エンジンで運用アプリのカタログを作成する場合は、このファイルを運用環境のデプロイから除外する必要があります。 これを行うには、作成時に実稼働発行プロファイルに設定を構成します。

### <a name="deploy-to-staging"></a>ステージング環境へのデプロイ

1. Contoso 大学プロジェクトを右クリックし、 **[発行]** をクリックして、 **Web の発行**ウィザードを開きます。
2. **ステージング**プロファイルが選択されていることを確認します。
3. **[発行]** をクリックします。

    **[出力]** ウィンドウには、実行された配置アクションが表示され、デプロイが正常に完了したことがレポートされます。 既定のブラウザーが自動的に開き、デプロイされた web アプリの URL が表示されます。

## <a name="test-in-the-staging-environment"></a>ステージング環境でのテスト

環境インジケーターが存在しないことに注意してください ("(テスト)" または "(Dev)" は H1 見出しの後にあります。これは、環境インジケーターの*web.config 変換が*成功したことを示しています。

![ホームページのステージング](deploying-to-production/_static/image12.png)

**[Students]** ページを実行して、デプロイされたデータベースに学生がいないことを確認します。

**インストラクターページを**実行して、Code First がインストラクターのデータでデータベースをシード処理したことを確認します。

[**学生] メニュー**から 学生の **[追加]** を選択し、学生を追加します。次に、 **[学生]** ページで新しい学生を表示して、データベースへの書き込みが正常に完了したことを確認します。

**[コース]** ページで、 **[クレジットの更新]** をクリックします。 **[更新プログラムのクレジット]** ページには管理者権限が必要であるため、 **[ログイン]** ページが表示されます。 前の手順で作成した管理者アカウントの資格情報を入力します ("admin" と "prodpwd")。 **[更新プログラムのクレジット]** ページが表示され、前のチュートリアルで作成した管理者アカウントがテスト環境に正しく配置されていることを確認します。

無効な URL を要求して、ELMAH が追跡するエラーを発生させ、ELMAH エラー報告を要求します。 サードパーティのホスティングプロバイダーに配置している場合は、前のチュートリアルで空だったのと同じ理由でレポートが空であることがわかります。 フォルダーのアクセス許可を構成するには、ホスティングプロバイダーのアカウント管理ツールを使用して、ELMAH がログフォルダーに書き込むことができるようにする必要があります。

これで、作成したアプリケーションは、運用環境で使用するものと同じように、web アプリのクラウドで実行されます。 すべてが正常に動作しているため、次の手順は運用環境にデプロイすることです。

## <a name="deploy-to-production"></a>運用環境へのデプロイ

運用 web アプリを作成し、運用環境にデプロイするプロセスは、ステージングの場合と同じですが、配置から*robots.txt*を除外する必要がある点が異なります。 これを行うには、発行プロファイルファイルを編集します。

### <a name="create-the-production-environment-and-the-production-publish-profile"></a>運用環境と実稼働発行プロファイルを作成する

1. ステージングに使用したのと同じ手順に従って、運用 web アプリとデータベースを Azure に作成します。

    データベースを作成するときに、以前に作成したのと同じサーバーに配置するか、新しいサーバーを作成するかを選択できます。
2. *.Publishsettings*ファイルをダウンロードします。
3. ステージングに使用したのと同じ手順に従って、 *.publishsettings*ファイルをインポートして発行プロファイルを作成します。

    **[設定]** タブの **[データベース]** セクションで、 **[defaultconnection]** の下にあるデータ配置スクリプトを必ず構成してください。
4. 発行プロファイルの名前を*運用環境*に変更します。
5. ステージングに使用したのと同じ手順に従って、環境インジケーターの発行プロファイルの変換を構成します。

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a>Pubxml ファイルを編集して robots.txt を除外する

発行プロファイルファイルには &lt;*profilename&gt;と*いう名前が付けられ、 *publishprofiles*フォルダーにあります。 *Publishprofiles* C#フォルダーは、web アプリケーションプロジェクトの [*プロパティ*] フォルダーの下、VB Web アプリケーションプロジェクトの [ *My project* ] フォルダーの下、または web アプリプロジェクトの [ *App\_Data* ] フォルダーの下にあります。 各*pubxml*ファイルには、1つの発行プロファイルに適用される設定が含まれています。 Web の発行ウィザードで入力した値はこれらのファイルに格納され、Visual Studio UI では使用できない設定を作成または変更するために編集できます。

既定では、発行プロファイルを作成するときに、 *pubxml*ファイルはプロジェクトに含まれますが、プロジェクトから除外することができ、Visual Studio では引き続き使用されます。 Visual Studio では、プロジェクトに含まれているかどうかに関係なく、pubxml ファイルの*Publishprofiles*フォルダーが検索され*ます。*

各*pubxml*ファイルには、 *pubxml. user*ファイルがあります。 *Pubxml. user*ファイルには、[**パスワードを保存**する] オプションを選択した場合に暗号化されたパスワードが含まれ、既定ではプロジェクトから除外されます。

*Pubxml*ファイルには、特定の発行プロファイルに関連する設定が含まれています。 すべてのプロファイルに適用する設定を構成する場合は、 *. .targets*ファイルを作成できます。 ビルドプロセスでは、これらのファイルが *.csproj*または *.vbproj*プロジェクトファイルにインポートされるため、プロジェクトファイルで構成できるほとんどの設定はこれらのファイルで構成できます。 *Pubxml*ファイルおよび*wpp*ファイルの詳細については、「[方法: 発行プロファイル (Pubxml) ファイルの配置設定を編集する」および「Visual Studio Web プロジェクトの wpp ファイル](https://msdn.microsoft.com/library/ff398069.aspx)」を参照してください。

1. **ソリューションエクスプローラー**で、 **[プロパティ]** を展開し、 **[publishprofiles]** を展開します。
2. [ *Production. pubxml* ] を右クリックし、 **[開く]** をクリックします。

    ![Pubxml ファイルを開きます。](deploying-to-production/_static/image13.png)
3. [ *Production. pubxml* ] を右クリックし、 **[開く]** をクリックします。
4. 終了 `PropertyGroup` 要素の直前に、次の行を追加します。

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    Pubxml ファイルは、次の例のようになります。

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    ファイルとフォルダーを除外する方法の詳細については、MSDN の「 **Visual Studio と ASP.NET の Web 配置に関してよく寄せ**られる質問」の「[特定のファイルまたはフォルダーをデプロイから除外](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment)する方法」を参照してください。

### <a name="deploy-to-production"></a>運用環境へのデプロイ

1. Web の**発行**ウィザードを開き、 **[実稼働]** 発行プロファイル が選択されていることを確認し、 **[プレビュー]** タブの **[プレビューの開始]** をクリックして、 *robots.txt*ファイルが運用アプリにコピーされないことを確認します。

    ![運用環境に発行するファイルのプレビュー](deploying-to-production/_static/image14.png)

    コピーされるファイルの一覧を確認します。 *Aspx.cs*、 *aspx.designer.cs*、 *Master.cs*、 *Master.designer.cs*の各ファイルを含むすべての *.cs*ファイルが省略されていることがわかります。 このコードはすべて、 *bin*フォルダーにある*ContosoUniversity*ファイルと*ContosoUniversity*ファイルにコンパイルされています。 アプリケーションを実行するために必要なのは *.dll*だけであり、アプリケーションの実行に必要なファイルのみを配置する必要があることを指定した場合、配布先の環境に *.cs*ファイルはコピーされません。 *Obj*フォルダーと*ContosoUniversity*ファイルと *.csproj*ファイルは、同じ理由で省略されています。

    **[発行]** をクリックして、運用環境にデプロイします。
2. ステージングに使用したのと同じ手順に従って、運用環境でテストします。

    すべてのものは、URL と*robots.txt*ファイルがない場合を除き、ステージングと同じです。

## <a name="summary"></a>要約

これで、web アプリのデプロイとテストが正常に完了し、インターネット経由で公開されるようになりました。

![ホームページの運用](deploying-to-production/_static/image15.png)

次のチュートリアルでは、アプリケーションコードを更新し、テスト環境、ステージング環境、および運用環境に変更をデプロイします。

> [!NOTE]
> アプリケーションが運用環境で使用されている間は、復旧計画を実装する必要があります。 つまり、データベースを運用アプリからセキュリティで保護されたストレージの場所に定期的にバックアップする必要があります。また、このようなバックアップの複数の世代を維持する必要があります。 データベースを更新するときは、変更の直前にからバックアップコピーを作成する必要があります。 これにより、間違いを犯しても、運用環境にデプロイするまで検出されない場合でも、データベースを破損する前の状態に復旧できます。 詳細については、「 [Azure SQL Database のバックアップと復元](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx)」を参照してください。
> 
> 
> [!NOTE]
> このチュートリアルでは、デプロイ先の SQL Server エディションが Azure SQL Database ます。 デプロイプロセスは SQL Server の他のエディションに似ていますが、実際の運用アプリケーションでは、一部のシナリオで Azure SQL Database に特別なコードが必要になる場合があります。 詳細については、「 [Azure SQL Database の操作](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb)」および「 [SQL Server と Azure SQL Database の選択](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing)」を参照してください。
> 
> [!div class="step-by-step"]
> [前へ](setting-folder-permissions.md)
> [次へ](deploying-a-code-update.md)

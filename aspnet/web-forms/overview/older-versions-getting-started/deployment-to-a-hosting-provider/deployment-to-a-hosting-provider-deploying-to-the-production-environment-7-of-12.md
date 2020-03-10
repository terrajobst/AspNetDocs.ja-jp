---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
title: 'Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: 運用環境への配置-7/12 |Microsoft Docs'
author: tdykstra
description: この一連のチュートリアルでは、Visual Stu... を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: b83ab819-2b05-4776-b7b4-79ef78d457a5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
msc.type: authoredcontent
ms.openlocfilehash: db838633accdedd7c0693b126a007e254ca681e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458170"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-the-production-environment---7-of-12"></a>Visual Studio または Visual Web Developer を使用した SQL Server Compact を使用した ASP.NET Web アプリケーションのデプロイ: 運用環境へのデプロイ-12/12

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> この一連のチュートリアルでは、Visual Studio 2012 RC または Visual Studio Express 2012 RC for Web を使用して SQL Server Compact データベースを含む ASP.NET web アプリケーションプロジェクトをデプロイ (発行) する方法について説明します。 Web 発行の更新をインストールする場合は、Visual Studio 2010 を使用することもできます。 シリーズの概要については、[シリーズの最初のチュートリアル](deployment-to-a-hosting-provider-introduction-1-of-12.md)を参照してください。
> 
> Visual Studio 2012 の RC リリース後に導入された配置機能を示すチュートリアルについては、SQL Server Compact 以外の SQL Server のエディションをデプロイする方法、Azure App Service Web Apps にデプロイする方法については、「 [ASP.NET Web deployment Using Visual studio (Visual studio を使用した Web デプロイ](../../deployment/visual-studio-web-deployment/introduction.md)のデプロイ)」を参照してください。

## <a name="overview"></a>概要

このチュートリアルでは、ホスティングプロバイダーを使用してアカウントを設定し、Visual Studio のワンクリック発行機能を使用して ASP.NET web アプリケーションを運用環境にデプロイします。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)を確認してください。

## <a name="selecting-a-hosting-provider"></a>ホスティングプロバイダーの選択

Contoso 大学アプリケーションとこのチュートリアルシリーズでは、ASP.NET 4 と Web 配置をサポートするプロバイダーが必要です。 このチュートリアルでは、ライブ web サイトへのデプロイの完全なエクスペリエンスを示すために、特定のホスティング会社を選択しました。 各ホスティング会社はさまざまな機能を提供しており、サーバーへの展開の経験は多少異なります。 ただし、このチュートリアルで説明するプロセスは、全体的なプロセスにおいて一般的です。 このチュートリアルで使用されているホスティングプロバイダー (Cytanium.com) は、使用可能な多くのうちの1つであり、このチュートリアルでの使用は、保証や推奨事項を構成するものではありません。

独自のホスティングプロバイダーを選択する準備ができたら、Microsoft.com/web サイトの[プロバイダーのギャラリー](https://www.microsoft.com/web/hosting)にある機能と価格を比較できます。

## <a name="creating-an-account"></a>アカウントの作成

選択したプロバイダーでアカウントを作成します。 完全な SQL Server データベースのサポートが追加されている場合は、このチュートリアル用に選択する必要はありませんが、このシリーズの後の[SQL Server チュートリアルに移行](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)するために必要になります。

これらのチュートリアルでは、新しいドメイン名を登録する必要はありません。 プロバイダーによってサイトに割り当てられた一時的な URL を使用して、正常に配置されたことを確認できます。

アカウントが作成されると、通常は、サイトを展開して管理するために必要なすべての情報が記載されたウェルカムメールが届きます。 ホスティングプロバイダーから送信された情報は、ここに表示されているものと似ています。 新しいアカウント所有者に送信される Cytanium ウェルカムメールには、次の情報が含まれています。

- プロバイダーのコントロールパネルサイトの URL。サイトの設定を管理できます。 指定した ID とパスワードは、簡単に参照できるように、ウェルカムメールのこの部分に含まれています。 (両方ともこの図のデモ値に変更されています)。

    [![Welcome_Email_Control_Panel_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image1.png)
- 既定の .NET Framework バージョンとその変更方法に関する情報です。 多くのホストサイトは、既定で2.0 に設定されています。これは、.NET Framework 2.0、3.0、または3.5 を対象とする ASP.NET アプリケーションで動作します。 ただし、Contoso 大学は .NET Framework 4 アプリケーションであるため、この設定を変更する必要があります。 (ASP.NET 4.5 アプリケーションの場合は、.NET 4.0 設定を使用します)。

    [![Welcome_Email_Framework_Version](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image3.png)
- Web サイトへのアクセスに使用できる一時的な URL。 このアカウントが作成されたときに、既存のドメイン名として "contosouniversity.com" が入力されました。 そのため、一時 URL は `http://contosouniversity.com.vserver01.cytanium.com`ます。

    [![Welcome_Email_Temporary_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image5.png)
- データベースを設定する方法と、それらにアクセスするために必要な接続文字列について説明します。

    [![Welcome_Email_Database_Info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image7.png)
- サイトを展開するためのツールと設定について説明します。 (Cytanium からの電子メールには WebMatrix も記載されていますが、ここでは省略しています)。

    [![Welcome_Email_Deploy_info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image10.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image9.png)

## <a name="setting-the-net-framework-version"></a>.NET Framework のバージョンの設定

Cytanium のウェルカムメールには、.NET Framework のバージョンを変更する手順へのリンクが記載されています。 この手順では、Cytanium コントロールパネルを使用してこれを行うことができます。 他のプロバイダーには、外観が異なるコントロールパネルサイトがあります。また、別の方法でこれを行うように指示することもできます。

コントロールパネルの URL にアクセスします。 ユーザー名とパスワードを使用してログインすると、コントロールパネルが表示されます。

[![Cytanium_Control_Panel](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image11.png)

**[ホストスペース]** ボックスで、web アイコンの上にポインターを置き、メニューから **[web サイト]** を選択します。

[![Cytanium_Control_Panel_selecting_Web_Sites](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image13.png)

**[Web サイト]** ボックスで、 **[contosouniversity.com]** (アカウントの作成時に使用したサイトの名前) をクリックします。

[![Cytanium_Control_Panel_selecting_contosouniversity](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image15.png)

**[Web サイトのプロパティ]** ボックスで、 **[拡張機能]** タブを選択します。

[![Cytanium_Control_Panel_Extensions_tab](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image17.png)

ASP.NET を**2.0 統合パイプライン**から**4.0 (統合パイプライン)** に変更し、 **[更新]** をクリックします。

## <a name="publishing-to-the-hosting-provider"></a>ホスティングプロバイダーへの発行

ホスティングプロバイダーからのウェルカムメールには、プロジェクトを発行するために必要なすべての設定が含まれており、その情報を発行プロファイルに手動で入力できます。 しかし、より簡単でエラーが発生しやすい方法を使用して、プロバイダーへのデプロイを構成します。 *.publishsettings*ファイルをダウンロードし、発行プロファイルにインポートします。

ブラウザーで、Cytanium コントロールパネルにアクセスし、 **[web]** を選択して、[web サイト] を選択し**ます。**

![コントロールパネルの Web サイトの選択](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image19.png)

**Contosouniversity.com** web サイトを選択します。

![コントロールパネルの contosouniversity.com の選択](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image20.png)

**[Web 発行]** タブを選択します。

![コントロールパネルの [Web 発行] タブ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image21.png)

ユーザー名とパスワードを入力して、web 発行に使用する資格情報を作成します。 コントロールパネルへのログオンに使用するのと同じ資格情報を入力できます。 **[有効]** をクリックします。

![コントロールパネルの発行資格情報の作成](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image22.png)

[**この web サイトの発行プロファイルのダウンロード] を**クリックします。

![コントロールパネルの発行プロファイルのダウンロード](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image23.png)

ファイルを開くか保存するかを確認するメッセージが表示されたら、保存します。

![発行プロファイルファイルの保存](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image24.png)

Visual Studio の**ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを右クリックし、 **[発行]** を選択します。 **[Web の発行]** ダイアログボックスは、 **[プレビュー]** タブに表示されます。これは、使用した最後のプロファイルであるため、**テスト**プロファイルが選択されています。

**[プロファイル]** タブを選択し、 **[インポート]** をクリックします。

![Web の発行ウィザードの [インポート] ボタン](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image25.png)

**[発行設定のインポート]** ダイアログボックスで、ダウンロードした *.publishsettings*ファイルを選択し、 **[開く]** をクリックします。 ウィザードは、すべてのフィールドが入力された [接続] タブに進みます。

![Web の発行ウィザードの [接続] タブ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image26.png)

.Publishsettings ファイルは、サイトの計画された永続的な URL を [宛先 URL] ボックスに配置しますが、そのドメインをまだ購入していない場合は、値を一時的な URL に置き換えます。 この例では、URL は *[http://contosouniversity.com.vserver01.cytanium.com](http://contosouniversity.com.vserver01.cytanium.com)です。* このボックスの唯一の目的は、配置後にブラウザーが自動的に開く URL を指定することです。 空白のままにしておくと、配置後にブラウザーが自動的に起動しないことが唯一の結果となります。

**[接続の検証]** をクリックして設定が正しいことを確認し、サーバーに接続できることを確認します。 前に見たように、緑色のチェックマークは接続が成功したことを確認します。

接続の検証 をクリックすると、**証明書のエラー** ダイアログボックスが表示することがあります。 その場合は、サーバー名が予期したとおりであることを確認します。 表示されている場合は、 **[今後、Visual Studio のセッションにこの証明書を保存する]** を選択し、 **[同意]** する をクリックします。 (このエラーは、デプロイ先の URL に対して SSL 証明書を購入する費用が発生しないように、ホスティングプロバイダーによって選択されたことを意味します。 有効な証明書を使用してセキュリティで保護された接続を確立する場合は、ホスティングプロバイダーに問い合わせてください。)

![証明書のエラー](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image27.png)

**[次へ]** をクリックします。

**[設定]** タブの **[データベース]** セクションで、テスト発行プロファイルに入力したものと同じ値を入力します。 必要な接続文字列がドロップダウンリストに表示されます。

- Schoolcontext.cs の [接続文字列] ボックスで **、** [`Data Source=|DataDirectory|School-Prod.sdf`] を選択します。
- **[Schoolcontext.cs]** で、 **[Code First Migrations の適用]** を選択します。
- **Defaultconnection**の [接続文字列] ボックスで、[`Data Source=|DataDirectory|aspnet-Prod.sdf`] を選択します。
- **[Defaultconnection]** で、 **[Update database]** をオフのままにします。

![Web の発行ウィザードの [設定] タブ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image28.png)

**[次へ]** をクリックします。

**[プレビュー]** タブで、 **[プレビューの開始]** をクリックして、コピーされるファイルの一覧を表示します。 ローカルコンピューターの IIS に展開したときと同じ一覧が表示されます。

発行する前に、プロファイルの名前を変更して、web.config 変換ファイルが適用されるようにします。 **[プロファイル]** タブを選択し、 **[プロファイルの管理]** をクリックします。

![Web の発行ウィザードのプロファイルの管理](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image29.png)

**[Web 発行プロファイルの編集]** ダイアログボックスで、実稼働プロファイルを選択し、 **[名前の変更]** をクリックして、プロファイル名を「production」に変更します。 次に、 **[閉じる]** をクリックします。

![[Web 発行プロファイルの編集] ダイアログボックス](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image30.png)

**[発行]** をクリックします。

アプリケーションはホスティングプロバイダーに発行されます。 結果が**出力**ウィンドウに表示されます。

![配置後の出力ウィンドウ](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image31.png)

**Web の発行**ウィザードの **[接続]** タブの **[宛先 url]** ボックスに入力した url がブラウザーによって自動的に開きます。 Visual Studio でサイトを実行したときと同じホームページが表示されます。ただし、タイトルバーに "(テスト)" または "(Dev)" の環境インジケーターはありません。 これは、環境インジケーターの*web.config*変換が正常に動作したことを示します。

> [!NOTE]
> 見出しに "(Test)" と表示されている場合は、ContosoUniversity プロジェクトから*obj*フォルダーを削除して再デプロイします。 プレリリース版のソフトウェアでは、運用プロファイルを使用していても、以前に適用された変換ファイル (web.config) が再度適用される可能性があります。

[![Home_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image33.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image32.png)

データベースにアクセスするページを実行する前に、Elmah が発生したすべてのエラーをログに記録できることを確認してください。

## <a name="setting-folder-permissions-for-elmah"></a>Elmah のフォルダー権限を設定しています

このシリーズの前のチュートリアルで覚えているように、アプリケーションには、Elmah がエラーログファイルを格納するアプリケーションのフォルダーに対する書き込みアクセス許可があることを確認する必要があります。 コンピューターのローカルに IIS に配置した場合は、これらのアクセス許可を手動で設定します。 このセクションでは、Cytanium でアクセス許可を設定する方法について説明します。 (一部のホスティングプロバイダーでは、この操作を実行できない場合があります。書き込みアクセス許可を持つ1つ以上の定義済みフォルダーが提供される場合があります。 その場合は、指定されたフォルダーを使用するようにアプリケーションを変更する必要があります)。

フォルダーのアクセス許可は、Cytanium コントロールパネルで設定できます。 コントロールパネルの URL にアクセスし、 **[ファイルマネージャー]** を選択します。

[![Cytanium_Control_Panel_with_File_Manager_selected](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image35.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image34.png)

**[ファイルマネージャー]** ボックスで、 **[contosouniversity.com]** 、 **[wwwroot]** の順に選択して、アプリケーションのルートフォルダーを表示します。 **[Elmah]** の横にある南京錠アイコンをクリックします。

[![Cytanium_Control_Panel_File_Manager_at_root_folder](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image37.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image36.png)

[**ファイル**/**フォルダーのアクセス許可**] ウィンドウで、 **contosouniversity.com**の **[読み取り]** および **[書き込み]** チェックボックスをオンにし、 **[アクセス許可の設定]** をクリックします。

[![Cytanium_Control_Panel_File_Folder_Permissions_Elmah](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image39.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image38.png)

エラーを発生させて、Elmah エラーレポートを表示することで、elmah に*elmah*フォルダーへの書き込みアクセス権があることを確認してください。 *Studentsxxx*のような無効な URL を要求します。 以前と同様に、 *Genericerrorpage .aspx*ページが表示されます。 **[ログアウト]** リンクをクリックし、次に*Elmah*を実行します。 最初に **[ログイン]** ページが表示されます。これにより、 *Web.config*変換が Elmah 承認を正常に追加したことが検証されます。 ログインすると、発生したエラーを示すレポートが表示されます。

[![Elmah. axd_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image41.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image40.png)

## <a name="testing-in-the-production-environment"></a>運用環境でのテスト

**[Students]** ページを実行します。 アプリケーションは、初めて School データベースにアクセスしようとします。これにより、データベースを作成するために Code First Migrations がトリガーされます。 しばらくしてからページが表示されている場合は、学生がいないことを示しています。

[![Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image43.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image42.png)

**インストラクターページを**実行して、シードデータによってインストラクターデータがデータベースに正常に挿入されたことを確認します。

[![Instructors_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image45.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image44.png)

テスト環境で行ったように、運用環境でデータベースの更新が機能していることを確認する必要がありますが、通常はテストデータを運用データベースに入力する必要はありません。 このチュートリアルでは、テストで行ったのと同じ方法を使用します。 実際のアプリケーションでは、実稼働データベースにテストデータを導入しなくても、データベースの更新が成功したことを検証するメソッドを見つけることができます。 アプリケーションによっては、何かを追加してから削除するのが実用的な場合があります。

学生を追加し、 **[Students]** ページで入力したデータを表示して、データベースのデータを更新できることを確認します。

[![Add_Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image47.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image46.png)

[![Students_page_with_new_student_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image49.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image48.png)

**[コース]** メニューの **[クレジットの更新]** を選択して、承認規則が正しく機能していることを確認します。 **[ログイン]** ページが表示されます。 管理者アカウントの資格情報を入力し、 **[ログイン]** をクリックすると、**クレジットの更新**ページが表示されます。

[![Log_In_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image51.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image50.png)

ログインに成功すると、 **[更新プログラムのクレジット]** ページが表示されます。 これは、(管理者アカウントが1つの) ASP.NET メンバーシップデータベースが正常に展開されたことを示します。

[![Update_Credits_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image53.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image52.png)

これで、サイトの展開とテストが正常に完了し、インターネット経由で公開されるようになりました。

## <a name="creating-a-more-reliable-test-environment"></a>より信頼性の高いテスト環境の作成

「[テスト環境へのデプロイ](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)」チュートリアルで説明したように、最も信頼性の高いテスト環境は、運用アカウントと同じように、ホスティングプロバイダーの2番目のアカウントになります。 これは、ローカル IIS をテスト環境として使用するよりもコストが高くなります。これは、2番目のホスティングアカウントにサインアップする必要があるためです。 しかし、運用サイトのエラーや障害が発生しないようにする場合は、コストの価値があると判断します。

テストアカウントを作成してデプロイするプロセスのほとんどは、実稼働環境にデプロイするために既に行っているものと似ています。

- *Web.config 変換ファイル*を作成します。
- ホスティングプロバイダーでアカウントを作成します。
- 新しい発行プロファイルを作成し、テストアカウントにデプロイします。

### <a name="preventing-public-access-to-the-test-site"></a>テストサイトへのパブリックアクセスの防止

テストアカウントにとって重要な考慮事項は、インターネット上で公開されることですが、パブリックで使用することは望ましくありません。 サイトをプライベートに保つには、次の方法のうち1つ以上を使用します。

- テスト用に使用している IP アドレスからのみテストサイトへのアクセスを許可するファイアウォール規則を設定するには、ホスティングプロバイダーに問い合わせてください。
- パブリックサイトの URL と類似していないように URL を偽装します。
- *Robots.txt*ファイルを使用して、検索エンジンがテストサイトをクロールしないようにし、検索結果でそのサイトへのリンクを報告しないようにします。

これらの方法の1つは、明らかに最も安全ですが、の手順は、各ホスティングプロバイダーに固有であり、このチュートリアルでは説明しません。 テストアカウントの URL への参照を自分の IP アドレスのみに許可するようにホスティングプロバイダーに設定すると、理論的には検索エンジンのクロールを気にする必要がありません。 ただし、その場合でも、ファイアウォールルールが誤ってオフになった場合のバックアップとして、 *robots.txt*ファイルを展開することをお勧めします。

*Robots.txt*ファイルがプロジェクトフォルダーに移動し、次のテキストが含まれている必要があります。

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/samples/sample1.cmd)]

`User-agent` 行は、ファイル内のルールがすべての検索エンジン web クローラー (ロボット) に適用されることを検索エンジンに通知します。また、`Disallow` 行は、サイトのページをクロールする必要がないことを指定します。

場合によっては、検索エンジンで運用サイトのカタログを作成する必要があるため、このファイルを運用環境のデプロイから除外する必要があります。 これを行うには、「 [ASP.NET Web アプリケーションプロジェクトの配置](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment)に関する FAQ」の「**特定のファイルまたはフォルダーをデプロイから除外することはできますか**」を参照してください。 必ず、実稼働発行プロファイルにのみ除外を指定してください。

2番目のホスティングアカウントの作成は、必要のないテスト環境を操作するためのアプローチですが、追加費用がかかる場合があります。 次のチュートリアルでは、引き続き IIS をテスト環境として使用します。

次のチュートリアルでは、アプリケーションコードを更新し、テスト環境と運用環境に変更を配置します。

> [!div class="step-by-step"]
> [前へ](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
> [次へ](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)

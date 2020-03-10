---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 'Visual Studio を使用した ASP.NET Web 配置: コード更新の配置 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457642"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a>Visual Studio を使用した ASP.NET Web 配置: コード更新の配置

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。 シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。

## <a name="overview"></a>概要

最初のデプロイの後、web サイトの保守と開発の作業が継続し、その前に更新プログラムを展開する必要があります。 このチュートリアルでは、アプリケーションコードに更新プログラムをデプロイするプロセスについて順を追って紹介します。 このチュートリアルで実装およびデプロイする更新プログラムには、データベースの変更は含まれません。次のチュートリアルでは、データベースの変更を配置する場合の違いについて説明します。

リマインダー: チュートリアルを実行しているときにエラーメッセージが表示されたり機能しない場合は、必ず[トラブルシューティングのページ](troubleshooting.md)を確認してください。

## <a name="make-a-code-change"></a>コードに変更を加える

アプリケーションの更新の簡単な例として **、インストラクターのページに**、選択したインストラクターが担当するコースの一覧を追加します。

**インストラクター**ページを実行すると、グリッドに**選択**リンクがあることがわかりますが、行の背景を灰色にする以外には何も行われません。

![選択したインストラクターページ](deploying-a-code-update/_static/image1.png)

次に、 **[選択]** リンクがクリックされたときに実行されるコードを追加します。選択したインストラクターによって担当されるコースの一覧が表示されます。

1. *講師*の**ErrorMessageLabel** `Label` コントロールの直後に、次のマークアップを追加します。

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. ページを実行し、インストラクターを選択します。 インストラクターがトレーニングしたコースの一覧が表示されます。

    ![コースが講義されるインストラクターページ](deploying-a-code-update/_static/image2.png)
3. ブラウザーを閉じます。

## <a name="deploy-the-code-update-to-the-test-environment"></a>コードの更新をテスト環境に配置する

発行プロファイルを使用してテスト、ステージング、および運用環境への配置を行う前に、データベースのパブリッシュオプションを変更する必要があります。 メンバーシップデータベースの grant および data deployment スクリプトを実行する必要がなくなりました。

1. ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックして、 **Web の発行**ウィザードを開きます。
2. **[プロファイル]** ボックスの一覧で、**テスト**プロファイルをクリックします。
3. **[設定]** タブをクリックします。
4. **[データベース]** セクションの **[defaultconnection]** で、 **[データベースの更新]** チェックボックスをオフにします。
5. **[プロファイル]** タブをクリックし、 **[プロファイル]** ドロップダウンリストで**ステージング**プロファイルをクリックします。
6. **テスト**プロファイルに加えられた変更を保存するかどうかを確認するメッセージが表示されたら、[**はい]** をクリックします。
7. ステージングプロファイルで同じ変更を行います。
8. 運用プロファイルで同じ変更を行うには、この手順を繰り返します。
9. Web の**発行**ウィザードを閉じます。

テスト環境への配置は、ワンクリックでの発行を再実行するだけの簡単な方法です。 この処理をより迅速に行うために、 **Web One の [発行**] ツールバーを使用できます。

1. **[表示]** メニューの **[ツールバー]** をクリックし、[ **Web One] をクリック**します。

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. **ソリューションエクスプローラー**で、ContosoUniversity プロジェクトを選択します。
3. **web で [発行**] ツールバーをクリックし、**テスト**発行プロファイルを選択して、 **[web の発行]** をクリックします (矢印が左と右にあるアイコン)。

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. Visual Studio によって更新されたアプリケーションが配置され、ブラウザーが自動的にホームページに表示されます。
5. インストラクターページを実行し、インストラクターを選択して、更新が正常に展開されたことを確認します。

通常は回帰テストも行います (つまり、サイトの他の部分をテストして、新しい変更によって既存の機能が破壊されていないことを確認します)。 ただし、このチュートリアルでは、この手順を省略し、ステージング環境と運用環境への更新プログラムのデプロイに進みます。

を再展開すると、変更されたファイルが Web 配置によって自動的に判断され、変更されたファイルのみがサーバーにコピーされます。 既定では、Web 配置は、ファイルの最終変更日を使用して、変更された日付を特定します。 ソース管理システムによっては、ファイルの内容を変更しない場合でもファイルの日付が変更されることがあります。 その場合は、ファイルのチェックサムを使用して変更されたファイルを特定するように Web 配置を構成することができます。 詳細については、「ASP.NET の展開に関する FAQ」で、[すべてのファイルが再展開](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum)される理由に関するページを参照してください。

## <a name="take-the-application-offline-during-deployment"></a>デプロイ中にアプリケーションをオフラインにする

ここでデプロイしている変更は、1つのページに単純に変更されます。 ただし、大規模な変更を配置する場合や、コードとデータベースの両方の変更を配置する場合があります。配置が完了する前にユーザーがページを要求すると、サイトが正しく動作しなくなることがあります。 配置の進行中にユーザーがサイトにアクセスできないようにするには、*アプリ\_のオフライン .htm*ファイルを使用します。 アプリケーションのルートフォルダーに*app\_offline .htm*という名前のファイルを配置すると、アプリケーションを実行する代わりに IIS によってそのファイルが自動的に表示されます。 そのため、デプロイ中にアクセスできないようにするには、*アプリ\_* をルートフォルダーに置き、デプロイプロセスを実行してから、展開が正常に完了した後で、*アプリ\_offline .htm*を削除します。

配置を開始するときに既定の*アプリ\_オフライン .htm*ファイルを自動的に配置し、終了時に削除するように Web 配置を構成することができます。 これを行うには、次の XML 要素を発行プロファイル (pubxml) ファイルに追加するだけです。

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

このチュートリアルでは、カスタム*アプリ\_オフライン .htm*ファイルを作成して使用する方法について説明します。

ステージングサイトにアクセスするユーザーがいないため、ステージングサイトで*アプリ\_offline .htm*を使用する必要はありません。 ただし、ステージングを使用して、運用環境でのデプロイを計画しているすべてのことをテストすることをお勧めします。

### <a name="create-app_offlinehtm"></a>アプリ\_offline .htm を作成する

1. **ソリューションエクスプローラー**で、ソリューションを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** をクリックします。
2. *App\_offline .htm*という名前の**html ページ**を作成します (Visual Studio で既定で作成される *.html*拡張子の最後の "l" を削除します)。
3. テンプレートマークアップを次のマークアップに置き換えます。

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. ファイルを保存して閉じます。

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a>アプリ\_offline .htm を web サイトのルートフォルダーにコピーします。

任意の FTP ツールを使用して、web サイトにファイルをコピーできます。 [FileZilla](http://filezilla-project.org/)は一般的な FTP ツールであり、スクリーンショットに示されています。

FTP ツールを使用するには、FTP URL、ユーザー名、およびパスワードの3つが必要です。

URL は、Azure 管理ポータルの web サイトの [ダッシュボード] ページに表示されます。 FTP のユーザー名とパスワードは、先ほどダウンロードした *.publishsettings*ファイルにあります。 次の手順は、これらの値を取得する方法を示しています。

1. Azure 管理ポータルで、**Web サイト** タブをクリックし、ステージング web サイトをクリックします。
2. **[ダッシュボード]** ページで下に**スクロールし、[概要] セクション**で FTP ホスト名を見つけます。

    ![FTP ホスト名](deploying-a-code-update/_static/image5.png)
3. メモ帳などのテキストエディターで *.publishsettings*ファイルを開きます。
4. FTP プロファイルの `publishProfile` 要素を見つけます。
5. `userName` と `userPWD` の値をコピーします。

    ![FTP 資格情報](deploying-a-code-update/_static/image6.png)
6. FTP ツールを開き、FTP URL にログオンします。
7. *App\_offline .htm*をソリューションフォルダーからステージングサイトの */siteフォルダー*にコピーします。

    ![App_offline のコピー](deploying-a-code-update/_static/image7.png)
8. ステージングサイトの URL を参照します。 ホームページの代わりに、*アプリ\_offline .htm*ページが表示されるようになります。

    ![ブラウザーウィンドウの app_offline .htm](deploying-a-code-update/_static/image8.png)

これで、ステージングにデプロイする準備ができました。

## <a name="deploy-the-code-update-to-staging-and-production"></a>ステージング環境と運用環境にコードの更新をデプロイする

1. **Web One の [発行**] ツールバーで、 **[ステージング]** 発行プロファイル を選択し、 **[web の発行]** をクリックします。

    更新されたアプリケーションが Visual Studio によって展開され、ブラウザーが開き、サイトのホームページが表示されます。 *アプリ\_のオフライン .htm*ファイルが表示されます。 展開が成功したことを確認するためにテストする前に、*アプリ\_のオフライン .htm*ファイルを削除する必要があります。
2. FTP ツールに戻り、**アプリ\_offline .htm**をステージングサイトから削除します。
3. ブラウザーで、ステージングサイトの [インストラクター] ページを開き、更新プログラムが正常に展開されたことを確認するインストラクターを選択します。
4. ステージングの場合と同じ手順に従います。

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a>変更の確認と特定のファイルの展開

また、Visual Studio 2012 では、個々のファイルを配置することもできます。 選択したファイルについて、ローカルバージョンと配置されたバージョンの相違点を表示したり、ファイルを移行先環境に配置したり、コピー先の環境からローカルプロジェクトにファイルをコピーしたりできます。 チュートリアルのこのセクションでは、これらの機能を使用する方法について説明します。

### <a name="make-a-change-to-deploy"></a>デプロイを変更する

1. *コンテンツ/サイト .css*を開き、`body` タグのブロックを見つけます。
2. `background-color` の値を `#fff` から `darkblue`に変更します。

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a>[発行のプレビュー] ウィンドウでの変更の表示

**Web の発行**ウィザードを使用してプロジェクトを発行するときに、**プレビュー**ウィンドウでファイルをダブルクリックすると、発行される変更内容を確認できます。

1. ContosoUniversity プロジェクトを右クリックし、 **[発行]** をクリックします。
2. **[プロファイル]** ドロップダウンリストから、**テスト**発行プロファイルを選択します。
3. **[プレビュー]** をクリックし、 **[プレビューの開始]** をクリックします。
4. **プレビュー**ウィンドウで、 **[.css]** をダブルクリックします。

    ![[.Css] をダブルクリックします。](deploying-a-code-update/_static/image9.png)

    **[変更のプレビュー]** ダイアログに、デプロイされる変更のプレビューが表示されます。

    ![サイト .css に対する変更のプレビュー](deploying-a-code-update/_static/image10.png)

    *Web.config*ファイルをダブルクリックすると、 **[変更のプレビュー]** ダイアログボックスに、ビルド構成の変換と発行プロファイルの変換の影響が表示されます。 この時点で、サーバー*上の web.config ファイルが*変更されることは何も行われていないため、変更がないことが予想されます。 ただし、 **[変更のプレビュー]** ウィンドウでは、2つの変更が誤って表示されます。 2つの XML 要素が削除されるように見えます。 これらの要素は、発行プロセスによって追加されます。この場合、Code First コンテキストクラスの**アプリケーション開始時に [Code First Migrations の実行**] を選択します。 この比較は、発行プロセスによってこれらの要素が追加される前に行われます。そのため、削除されるのではなく、削除されているように見えます。 このエラーは、今後のリリースで修正される予定です。
5. **[閉じる]** をクリックします。
6. **[発行]** をクリックします。
7. ブラウザーが開き、テストサイトのホームページが表示されたら、CTRL キーを押しながら F5 キーを押して、CSS の変更の効果を確認します。

    ![CSS の変更の影響](deploying-a-code-update/_static/image11.png)
8. ブラウザーを閉じます。

### <a name="publish-specific-files-from-solution-explorer"></a>ソリューションエクスプローラーから特定のファイルを発行する

青の背景に気がなく、元の色に戻す必要があるとします。 このセクションでは、**ソリューションエクスプローラー**から直接特定のファイルを発行することによって、元の設定を復元します。

1. *コンテンツ/サイト .css*を開き、`background-color` 設定を `#fff`に復元します。
2. **ソリューションエクスプローラー**で、*コンテンツ/サイトの .css*ファイルを右クリックします。

    コンテキストメニューには、3つの発行オプションが表示されます。

    ![ソリューションエクスプローラーからの発行オプション](deploying-a-code-update/_static/image12.png)
3. [変更のプレビュー] をクリックして **、.css に**します。

    ウィンドウが開き、ローカルファイルと移行先の環境でのバージョンの相違点が表示されます。

    ![Diff-Content/.css](deploying-a-code-update/_static/image13.png)
4. **ソリューションエクスプローラー**で、もう一度 **[.css]** を右クリックし、 **[Publish site .css]** をクリックします。

    **[Web 発行アクティビティ]** ウィンドウに、ファイルが発行されたことが表示されます。

    ![Web 発行アクティビティウィンドウ](deploying-a-code-update/_static/image14.png)
5. ブラウザーで `http://localhost/contosouniversity` URL を開き、CTRL キーを押しながら F5 キーを押すと、CSS の変更の効果を確認するために、ハード更新が行われます。

    ![通常の CSS を使用したホームページ](deploying-a-code-update/_static/image15.png)
6. ブラウザーを閉じます。

## <a name="summary"></a>まとめ

ここでは、データベースの変更を伴わないアプリケーションの更新を展開するいくつかの方法を説明しました。また、変更をプレビューして、更新対象が期待どおりであることを確認する方法についても説明しました。 これで、インストラクターのページに、**コース**のセクションがあります。

![コースが講義されるインストラクターページ](deploying-a-code-update/_static/image16.png)

次のチュートリアルでは、データベースの変更を配置する方法について説明します。誕生日フィールドをデータベースとインストラクターページに追加します。

> [!div class="step-by-step"]
> [前へ](deploying-to-production.md)
> [次へ](deploying-a-database-update.md)

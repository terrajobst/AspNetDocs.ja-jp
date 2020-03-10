---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-vb
title: 実稼働データベースを使用するように運用 Web アプリケーションを構成する (VB) |Microsoft Docs
author: rick-anderson
description: 前のチュートリアルで説明したように、開発環境と運用環境で構成情報が異なることは珍しくありません。 これは...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: a64a7aa0-6608-449e-83bf-1ef8cceee504
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-the-production-web-application-to-use-the-production-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 7fe4f545a76992ad687827af447d9a9e95bea73f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516622"
---
# <a name="configuring-the-production-web-application-to-use-the-production-database-vb"></a>実稼働データベースを使用するように Web アプリケーションを構成する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_08_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial08_DBConfig_vb.pdf)

> 前のチュートリアルで説明したように、開発環境と運用環境で構成情報が異なることは珍しくありません。 これは、データドリブン web アプリケーションの場合に特に当てはまります。これは、開発環境と運用環境でデータベース接続文字列が異なるためです。 このチュートリアルでは、適切な接続文字列を追加するように運用環境を構成する方法について説明します。

## <a name="introduction"></a>はじめに

データドリブンの web アプリケーションは、通常、運用環境の場合よりも、開発時に異なるデータベースを使用します。 Web ホストプロバイダーによってホストされ、ローカルで開発されたアプリケーションの場合、開発データベースは通常、開発者のコンピューターに配置されます。運用データベースは、web ホスティング会社の施設にあるデータベースサーバーでホストされます。 データドリブン web アプリケーションを配置するには、運用データベースサーバーに開発データベースをコピーすることがあります。 前のチュートリアルでは、この手順を実行する方法を見てきました。

Web アプリケーションは、*接続文字列*内の情報を使用して、データベースとの接続を確立します。 通常 `Web.config`に格納されている接続文字列は、データベースサーバー名、データベース名、セキュリティコンテキスト、およびその他の情報を指定します。 Web アプリケーションで使用されるデータベースは、web アプリケーションが開発環境と運用環境のどちらで実行されているかによって異なります。そのため、2つの環境で接続文字列が異なる必要があります。

開発環境と運用環境で構成情報が異なることは珍しくありません。 *開発と運用のチュートリアルの一般的な構成の違い*については、これら2つの環境間で個別の構成情報を保持するための手法と、データベース接続文字列についての簡単な説明を説明しました。 このチュートリアルでは、適切な接続文字列を追加するように運用環境を構成する方法について説明します。

## <a name="examining-the-connection-string-information"></a>接続文字列情報を調べています

Book review web アプリケーションで使用される接続文字列は、アプリケーションの構成ファイル `Web.config`に格納されます。 `Web.config` には、接続文字列を格納するための特別なセクション[&lt;connectionStrings&gt;](https://msdn.microsoft.com/library/bf7sd233.aspx)という名前のこのが含まれています。 本書レビュー web サイトの `Web.config` ファイルには、このセクションで `ReviewsConnectionString`という1つの接続文字列が定義されています。

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample1.xml)]

接続文字列-Data Source = .\SQLEXPRESS;AttachDbFilename = |DataDirectory | \Reviews.mdf; Integrated Security = True;User Instance = True-複数のオプションと値で構成されます。オプションと値のペアはセミコロンで区切られ、各オプションと値は等号で区切られます。 この接続文字列で使用される4つのオプションは次のとおりです。

- `Data Source`-データベースサーバーの場所とデータベースサーバーのインスタンス名 (存在する場合) を指定します。 `.\SQLEXPRESS`の値は、データベースサーバーとインスタンス名が存在する例です。 この期間は、データベースサーバーがアプリケーションと同じコンピューター上にあることを指定します。インスタンス名が `SQLEXPRESS`。
- `AttachDbFilename`-データベースファイルの場所を指定します。 この値には `|DataDirectory|`プレースホルダーが含まれています。これは、実行時にアプリケーションの `App_Data` フォルダーの完全パスに解決されます。
- `Integrated Security`-データベースへの接続時に指定したユーザー名/パスワードを使用するか (false)、現在の Windows アカウントの資格情報 (true) を使用するかを示すブール値です。
- `User Instance`-ローカルコンピューターの管理者以外のユーザーが接続して SQL Server Express Edition データベースに接続できるかどうかを示す、SQL Server Express のエディションに固有の構成オプション。 この設定の詳細については、「 [SQL Server Express ユーザーインスタンス](https://msdn.microsoft.com/library/ms254504.aspx)」を参照してください。

使用できる接続文字列のオプションは、接続先のデータベースと使用されている[ADO.NET](http://ADO.NET)データベースプロバイダーによって異なります。 たとえば、Microsoft SQL Server データベースに接続するための接続文字列は、Oracle データベースへの接続に使用される接続文字列とは異なります。 同様に、SqlClient プロバイダーを使用して Microsoft SQL Server データベースに接続する場合は、OLE DB プロバイダーを使用する場合とは異なる接続文字列が使用されます。

データベース接続文字列は、使用可能なオプションのリソースとして[ConnectionStrings.com](http://www.connectionstrings.com/)のようなサイトを使用して手動で作成できます。 ただし、簡単な方法は、Visual Studio のサーバーエクスプローラーにデータベースを追加し、次にプロパティウィンドウから接続文字列を取得することです。 この後者の手法を使用して、実稼働データベースサーバーへの接続文字列を構築します。

Visual Studio を開き、[サーバーエクスプローラー] ウィンドウに移動します (Visual Web Developer では、このウィンドウはデータベースエクスプローラーと呼ばれます)。 [データ接続] オプションを右クリックし、コンテキストメニューの [接続の追加] オプションを選択します。 これにより、図1に示すウィザードが表示されます。 適切なデータソースを選択し、[続行] をクリックします。

[![新しいデータベースをサーバーエクスプローラーに追加することを選択します。](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image2.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image1.jpg) 

**図 1**: サーバーエクスプローラーに新しいデータベースを追加することを選択する ([クリックすると、フルサイズの画像が表示](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image3.jpg)されます)

次に、さまざまなデータベース接続情報を指定します (図2を参照)。 Web ホスティング会社にサインアップした場合は、データベースへの接続方法に関する情報 (データベースサーバー名、データベース名、データベースへの接続に使用するユーザー名とパスワードなど) を提供する必要があります。 この情報を入力したら、[OK] をクリックしてこのウィザードを完了し、データベースをサーバーエクスプローラーに追加します。

[データベース接続情報を指定 ![には](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image5.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image4.jpg) 

**図 2**: データベース接続情報を指定[する (クリックすると、フルサイズの画像が表示](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image6.jpg)されます)

これで、運用環境のデータベースがサーバーエクスプローラーに一覧表示されます。 サーバーエクスプローラーからデータベースを選択し、プロパティウィンドウにアクセスします。 ここには、Connection String という名前のプロパティがあり、データベースの接続文字列が表示されます。 実稼働環境と SqlClient プロバイダーで Microsoft SQL Server データベースを使用していると仮定した場合、接続文字列は次のようになります。

<strong>データソース =<em>serverName</em>;初期カタログ =<em>databaseName</em>;Persist Security Info = True;ユーザー ID =<em>username</em>;パスワード =*パスワード</strong>*

ここで、 *serverName*、 *databaseName*、 *username*、および*password*は、データベースサーバー名、データベース名、web ホスト会社によって指定されたユーザー名とパスワードの値です。

## <a name="deploying-the-book-reviews-web-application"></a>書籍レビュー Web アプリケーションを展開する

前のチュートリアルでは、開発データベースを運用環境にコピーする手順について説明しましたが、データドリブンアプリケーションの配置については説明しませんでした。 この時点で、運用環境にはデータベースが含まれていますが、静的なレビューを含む書籍レビューアプリケーションのバージョンが使用されています。 更新された構成情報と共に、新しいデータドリブンアプリケーションを実稼働サーバーに配置する必要があります。

開発環境から運用環境にデータドリブンアプリケーションをデプロイします。 このプロセスの詳細については、前のチュートリアルで説明しました。 リフレッシャーが必要な場合は、「 *FTP クライアントを使用した Web サイトのデプロイ*」または「 *Visual Studio を使用した Web サイトのデプロイ*」チュートリアルを参照してください。 運用データベースの接続文字列が運用環境で使用されているものであることを確認する必要があります。つまり、代替の `Web.config` ファイルを配置する必要があります。 具体的には、このように変更された `Web.config` ファイル `<connectionStrings>` 要素には、実稼働データベース接続文字列が含まれている必要があり、次のようになります。

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample2.xml)]

`<connectionStrings>` 要素の接続文字列の名前は同じであることに注意してください (`ReviewsConnectionString`)。ただし、ここでは、開発データベース接続文字列ではなく、実稼働データベース接続文字列が含まれています。

より形式化された展開ワークフローがない場合は、配置前に実稼働データベース接続文字列を使用するように `Web.config` ファイルを手動で変更します (後で開発データベース接続文字列を使用するようにしてください)。または、デプロイプロセスの一部として運用環境にアップロードされる運用環境の構成情報を使用して別の `Web.config` ファイルを

> [!NOTE]
> 開発データベース接続文字列を含む `Web.config` ファイルを誤って配置した場合、運用環境でアプリケーションがデータベースに接続しようとするとエラーが発生します。 このエラーは、サーバーが見つからなかったかアクセスできなかったことを示すメッセージが表示された `SqlException` として報告されます。

サイトが運用環境にデプロイされたら、ブラウザーで運用サイトにアクセスします。 データドリブンアプリケーションをローカルで実行する場合と同じユーザーエクスペリエンスが表示されます。 実稼働環境で web サイトにアクセスした場合、サイトは実稼働データベースサーバーを使用しますが、開発環境の web サイトにアクセスするときは、開発時にデータベースを使用します。 図3に、運用環境の web サイトの「 *ASP.NET 3.5 In the 24 Hours review」 (24 時間のレビューを自分で*確認する) ページを示します (ブラウザーのアドレスバーの URL に注意してください)。

[これで、データドリブンアプリケーションを運用環境で使用できるようになり ![ます。](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image8.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image7.jpg) 

**図 3**: データドリブンアプリケーションを運用環境で使用できるようになりました。 ([クリックすると、フルサイズの画像が表示](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image9.jpg)される)

### <a name="storing-connection-strings-in-a-separate-configuration-file"></a>接続文字列を別の構成ファイルに格納する

開発環境と運用環境で個別の構成情報を保持するための一般的な手法として、`Web.config`の2つのバージョンがあります。1つは開発環境用で、もう1つは運用用です。 デプロイ時に、適切な `Web.config` バージョンを運用環境にコピーできます。 このプロセスは、展開ワークフローの一部として自動化されるのが理想的です。

2つの個別の `Web.config` ファイルを保持するのではなく、必要に応じてより細かい違いを提供できます。 `Web.config` ファイルを構成する要素は、`Web.config` ファイルで参照される外部構成ファイルで定義できます。 簡単に言うと、1つの `Web.config` ファイルを使用できます。このファイルには、アプリケーションで使用される接続文字列が含まれ、各環境で一意である、databaseConnectionStrings .config ファイルを参照します。 さまざまな構成情報を別々のファイルに分割すると、より単純な `Web.config` ファイルが提供され、開発環境と運用環境の構成の違いをより明確に把握できます。

この手法を使用するには、まず、`ConfigSections`という名前の web アプリケーションに新しいフォルダーを作成します。 次に、databaseConnectionStrings という名前の新しいフォルダーに2つのファイルを追加します。次に、`Web.config` の `<connectionStrings>` 要素を databaseConnectionStrings. dev. .config ファイルにコピーします。次に、実稼働データベース接続文字列を指定するように、databaseConnectionStrings. machine.config ファイル内の接続文字列を変更します。 たとえば、databaseConnectionStrings. dev. .config ファイルには、開発データベースを参照する接続文字列を含む `<connectionStrings>` 要素だけを含める必要があります。

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample3.xml)]

同様に、databaseConnectionStrings. .config ファイルには、`<connectionStrings>` 要素だけを含める必要がありますが、実稼働データベース接続文字列が含まれている必要があります。

DatabaseConnectionStrings. dev. .config ファイルのコピーを作成し、その名前を「databaseConnectionStrings .config」にします。

> [!NOTE]
> 構成ファイルには、`connectionStrings.config` や `dbInfo.config`など、必要に応じて、databaseConnectionStrings .config 以外の名前を指定できます。 ただし、既定では ASP.NET エンジンによって処理されない `.config` ファイルを `.config` 拡張子でファイルに名前を付けてください。 `connectionStrings.txt`のように、ファイルに別の名前を指定すると、ユーザーはブラウザーで[www.yoursite.com/ConfigSettings/connectionStrings.txt](http://www.yoursite.com/ConfigSettings/connectionStrings.txt)をポイントし、ファイルの内容を表示することができます。

この時点で、`ConfigSections` フォルダーには3つのファイルが含まれている必要があります (図4を参照)。 DatabaseConnectionStrings. dev. .config ファイルと databaseConnectionStrings. app.config ファイルには、それぞれ開発環境と運用環境の接続文字列が含まれています。 DatabaseConnectionStrings .config ファイルには、実行時に web アプリケーションによって使用される接続文字列情報が含まれています。 そのため、databaseConnectionStrings .config ファイルは開発環境の databaseConnectionStrings. dev. .config ファイルと同じである必要がありますが、運用環境では、databaseConnectionStrings .config ファイルはと同じである必要があります。databaseConnectionStrings. machine.config.

[![ConfigSections](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image11.jpg)](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image10.jpg) 

**図 4**: configsections ([クリックしてフルサイズのイメージを表示する](configuring-the-production-web-application-to-use-the-production-database-vb/_static/image12.jpg))

次に、接続文字列ストアに databaseConnectionStrings .config ファイルを使用するように `Web.config` に指示する必要があります。 `Web.config`を開いて、既存の `<connectionStrings>` 要素を次の XAML に置き換えます。

[!code-xml[Main](configuring-the-production-web-application-to-use-the-production-database-vb/samples/sample4.xml)]

`configSource` 属性は、`Web.config` ファイルを基準とした物理パスを指定します。 外部 `.config` ファイルが `Web.config` と同じディレクトリにある場合は、この属性に `.config` ファイルのファイル名を設定します。 ConfigSections\databaseConnectionStrings.config. の場合と同様に、サブディレクトリ内にある場合は、フォルダー名とファイル名を区切るために円記号を使用してサブフォルダーを指定します。

この変更により、開発環境と運用環境に同じ `Web.config` ファイルが含まれるようになります。 ここで、唯一の違いは、databaseConnectionStrings .config ファイルです。 DatabaseConnectionStrings. .config ファイルを運用環境にコピーし、その名前を databaseConnectionStrings .config に変更します。将来、実稼働データベース接続文字列に変更が加えられた場合は、それを databaseConnectionStrings. .config ファイルに変更し、そのファイルを運用環境にアップロードして、その名前を databaseConnectionStrings .config に変更する必要があります。

> [!NOTE]
> `Web.config` 要素の情報を別のファイルに指定し、`configSource` 属性を使用して `Web.config`内からそのファイルを参照することができます。

## <a name="summary"></a>まとめ

通常、データドリブンアプリケーションでは、開発環境と運用環境で異なるデータベースを使用します。 そのため、web アプリケーションの構成に格納されているデータベース接続文字列は、環境ごとに一意である必要があります。 このチュートリアルでは、運用データベースの接続文字列を決定する方法と、2つの環境で一意の接続文字列情報を維持する方法について説明しました。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [接続文字列と構成ファイル](https://msdn.microsoft.com/library/ms254494.aspx)
- [データベース構成文字列情報 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [設定を Web.config ファイルの外に移動する](http://www.asp101.com/tips/index.asp?id=154)
- [&lt;connectionStrings&gt; 要素の技術ドキュメント](https://msdn.microsoft.com/library/bf7sd233.aspx)

> [!div class="step-by-step"]
> [前へ](deploying-a-database-vb.md)
> [次へ](configuring-a-website-that-uses-application-services-vb.md)

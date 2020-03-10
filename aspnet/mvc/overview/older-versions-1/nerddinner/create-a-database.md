---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: データベースの作成 | Microsoft Docs
author: microsoft
description: 手順 2. では、データベースを作成する手順を示します。この手順では、すべてのディナーデータと、このアプリケーションのすべてのデータを保持します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469300"
---
# <a name="create-a-database"></a>データベースの作成

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法について説明する無料の["" アプリケーションチュートリアル](introducing-the-nerddinner-tutorial.md)の手順2です。
> 
> 手順 2. では、データベースを作成する手順を示します。この手順では、すべてのディナーデータと、このアプリケーションのすべてのデータを保持します。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-2-creating-the-database"></a>手順 2: データベースを作成する

ここでは、データベースを使用して、世界中のアプリケーションのディナーと RSVP のすべてのデータを格納します。

次の手順では、free SQL Server Express edition ( [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)の V2 を使用して簡単にインストールできる) を使用してデータベースを作成する方法を示します。 記述するすべてのコードは、SQL Server Express と完全 SQL Server の両方で動作します。

### <a name="creating-a-new-sql-server-express-database"></a>新しい SQL Server Express データベースの作成

まず、web プロジェクトを右クリックし、 **[新しい項目の追加]** メニューコマンド&gt;選択します。

![](create-a-database/_static/image1.png)

これにより、Visual Studio の [新しい項目の追加] ダイアログが表示されます。 "データ" カテゴリでフィルター処理し、"SQL Server データベース" 項目テンプレートを選択します。

![](create-a-database/_static/image2.png)

ここでは、"" を作成する SQL Server Express データベースに名前を指定し、[ok] をクリックします。 次に、このファイルをアプリの\_データディレクトリ (読み取りと書き込みの両方のセキュリティ Acl が既に設定されているディレクトリ) に追加するかどうかを確認するメッセージが表示されます。

![](create-a-database/_static/image3.png)

[はい] をクリックすると、新しいデータベースが作成され、ソリューションエクスプローラーに追加されます。

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>データベース内にテーブルを作成する

これで、新しい空のデータベースが作成されました。 いくつかのテーブルを追加してみましょう。

これを行うには、Visual Studio 内の [サーバーエクスプローラー] タブウィンドウに移動します。これにより、データベースとサーバーを管理できるようになります。 アプリケーションの \ App\_Data フォルダーに格納されている SQL Server Express データベースは、サーバーエクスプローラー内に自動的に表示されます。 必要に応じて、[サーバーエクスプローラー] ウィンドウの上部にある [データベースに接続] アイコンを使用して、一覧に SQL Server データベース (ローカルとリモートの両方) を追加することもできます。

![](create-a-database/_static/image5.png)

このデータベースに2つのテーブルを追加します。1つはディナーを格納するテーブル、もう1つは RSVP acceptances を追跡するためのテーブルです。 新しいテーブルを作成するには、データベース内の "Tables" フォルダーを右クリックし、[新しいテーブルの追加] メニューコマンドを選択します。

![](create-a-database/_static/image6.png)

テーブルデザイナーが開き、テーブルのスキーマを構成することができます。 "ディナー" テーブルでは、次の10列のデータが追加されます。

![](create-a-database/_static/image7.png)

"Dinid" 列をテーブルの一意の主キーにする必要があります。 これを構成するには、[Dinid] 列を右クリックし、[主キーの設定] メニュー項目を選択します。

![](create-a-database/_static/image8.png)

Dinare Id を主キーにするだけでなく、新しいデータ行がテーブルに追加されたときに自動的に値がインクリメントされる "identity" 列として構成する必要もあります (つまり、挿入された最初のディナー行の Dinは1、2番目に挿入された行になります)。には、2のような Dinid が割り当てられます。

これを行うには、[Dinid] 列を選択し、[列のプロパティ] エディターを使用して、列の "(Is Id)" プロパティを "Yes" に設定します。 標準の id の既定値を使用します (新しいディナー行ごとに1から増分1を開始します)。

![](create-a-database/_static/image9.png)

次に、Ctrl + S キーを押すか、または [**ファイル&gt;保存**] メニューコマンドを使用して、テーブルを保存します。 これにより、テーブルに名前を指定するように求められます。 "ディナー" という名前を指定します。

![](create-a-database/_static/image10.png)

新しいディナーテーブルは、サーバーエクスプローラーのデータベース内に表示されます。

次に、上記の手順を繰り返し、"RSVP" テーブルを作成します。 このテーブルには3つの列があります。 RsvpID 列を主キーとして設定し、さらに id 列にします。

![](create-a-database/_static/image11.png)

このファイルを保存し、"RSVP" という名前を付けます。

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>テーブル間の外部キーリレーションシップの設定

これで、データベース内に2つのテーブルが作成されました。 スキーマデザインの最後の手順では、これら2つのテーブル間に "一対多" リレーションシップを設定します。これにより、各ディナー行を、それに適用される0個以上の RSVP 行に関連付けることができます。 これを行うには、"ディナー" テーブルの "Din Id" 列との外部キーリレーションシップを持つように、RSVP テーブルの "Dinの Id" 列を構成します。

これを行うには、サーバーエクスプローラーでテーブルデザイナー内の RSVP テーブルをダブルクリックして、そのテーブルを開きます。 次に、その中の "Dinの Id" 列を選択し、右クリックして、[リレーションシップ...] を選択します。コンテキストメニューコマンド:

![](create-a-database/_static/image12.png)

これにより、テーブル間のリレーションシップを設定するために使用できるダイアログが表示されます。

![](create-a-database/_static/image13.png)

[追加] ボタンをクリックして、ダイアログに新しいリレーションシップを追加します。 リレーションシップを追加したら、ダイアログの右側にあるプロパティグリッド内の [テーブルと列の指定] ツリービューノードを展開し、[...] をクリックします。右側のボタンをクリックします。

![](create-a-database/_static/image14.png)

[...] をクリックすると、ボタンをクリックすると、リレーションシップに関係するテーブルと列を指定したり、リレーションシップに名前を付けたりできるようにするためのダイアログボックスが表示されます。

主キーテーブルを "ディナー" に変更し、ディナーテーブル内の "Din Id" 列を主キーとして選択します。 RSVP テーブルは外部キーテーブル、および RSVP です。Dinの Id 列は、外部キーとして関連付けられます。

![](create-a-database/_static/image15.png)

これで、RSVP テーブルの各行が、ディナーテーブルの行に関連付けられます。 SQL Server は参照整合性を維持し、有効なディナー行を指していない場合は新しい RSVP 行を追加しないようにします。 また、これを参照している予約行がある場合は、ディナー行を削除できなくなります。

### <a name="adding-data-to-our-tables"></a>テーブルへのデータの追加

それでは、いくつかのサンプルデータをディナーテーブルに追加してみましょう。 テーブルにデータを追加するには、サーバーエクスプローラー内で右クリックし、[テーブルデータの表示] コマンドを選択します。

![](create-a-database/_static/image16.png)

ここでは、アプリケーションの実装を開始するときに使用できるディナーデータを数行追加します。

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>次の手順

これで、データベースの作成が完了しました。 クエリと更新に使用できるモデルクラスを作成しましょう。

> [!div class="step-by-step"]
> [前へ](create-a-new-aspnet-mvc-project.md)
> [次へ](build-a-model-with-business-rule-validations.md)

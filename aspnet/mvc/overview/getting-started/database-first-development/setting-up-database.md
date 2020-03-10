---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: 'チュートリアル: MVC 5 を使用した EF Database First の概要'
description: このチュートリアルでは、既存のデータベースを使用して作業を開始し、ユーザーがデータと対話できるようにする web アプリケーションをすばやく作成する方法について説明します。
author: Rick-Anderson
ms.author: riande
ms.date: 01/15/2019
ms.topic: tutorial
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: a760767839a834a9c7e9fe358a3fd806a833261f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471460"
---
# <a name="tutorial-get-started-with-ef-database-first-using-mvc-5"></a>チュートリアル: MVC 5 を使用した EF Database First の概要

MVC、Entity Framework、ASP.NET のスキャフォールディングを使用して、既存のデータベースへのインターフェイスを提供する web アプリケーションを作成できます。 このチュートリアルシリーズでは、ユーザーがデータベーステーブルに格納されているデータを表示、編集、作成、および削除できるようにするコードを自動的に生成する方法について説明します。 生成されたコードは、データベーステーブルの列に対応しています。 シリーズの最後の部分では、データの注釈をデータモデルに追加して検証要件を指定し、書式設定を表示する方法について説明します。 完了したら、Azure の記事に進んで、Azure App Service に .NET アプリと SQL データベースをデプロイする方法を学習できます。

このチュートリアルでは、既存のデータベースを使用して作業を開始し、ユーザーがデータと対話できるようにする web アプリケーションをすばやく作成する方法について説明します。 Entity Framework 6 と MVC 5 を使用して、web アプリケーションをビルドします。 ASP.NET スキャフォールディング機能を使用すると、データの表示、更新、作成、および削除のためのコードを自動的に生成できます。 Visual Studio 内で発行ツールを使用すると、サイトとデータベースを Azure に簡単にデプロイできます。

シリーズのこの部分では、データベースを作成し、データを読み込む方法について説明します。

このシリーズでは、Tom Dykstra と Rick Anderson からの投稿を執筆しました。 コメントセクションのユーザーからのフィードバックに基づいて改善されました。

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * データベースを設定する

## <a name="prerequisites"></a>前提条件

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="set-up-the-database"></a>データベースを設定する

既存のデータベースを使用する環境を模倣するには、まず、事前に入力されたデータを含むデータベースを作成し、次にデータベースに接続する web アプリケーションを作成します。

このチュートリアルは、Visual Studio 2017 で LocalDB を使用して開発されました。 LocalDB ではなく既存のデータベースサーバーを使用できますが、Visual studio のバージョンとデータベースの種類によっては、Visual Studio のすべてのデータツールがサポートされていない場合があります。 データベースでツールを使用できない場合は、データベースの管理スイート内でデータベース固有の手順の一部を実行することが必要になる場合があります。

お使いのバージョンの Visual Studio のデータベースツールに問題がある場合は、最新バージョンのデータベースツールがインストールされていることを確認してください。 データベースツールの更新またはインストールの詳細については、「 [Microsoft SQL Server Data tools](https://msdn.microsoft.com/data/hh297027)」を参照してください。

Visual Studio を起動し、 **SQL Server データベースプロジェクト**を作成します。 **プロジェクトに名前を指定**します。

![データベースプロジェクトの作成](setting-up-database/_static/image1.png)

これで、空のデータベースプロジェクトが作成されました。 このデータベースを Azure にデプロイできるようにするには、プロジェクトのターゲットプラットフォームとして Azure SQL Database を設定します。 ターゲットプラットフォームを設定しても、実際にはデータベースはデプロイされません。これは、データベースプロジェクトが、データベースの設計がターゲットプラットフォームと互換性があることを確認することのみを意味します。 ターゲットプラットフォームを設定するには、プロジェクトの**プロパティ**を開き、ターゲットプラットフォームの **[Microsoft Azure SQL Database]** を選択します。

このチュートリアルに必要なテーブルを作成するには、テーブルを定義する SQL スクリプトを追加します。 プロジェクトを右クリックし、新しい項目を追加します。 テーブル**とビュー** > **テーブル**を選択し、「 *Student*」という名前を指定します。

テーブルファイルで、T-sql コマンドを次のコードに置き換えて、テーブルを作成します。

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

デザインウィンドウがコードと自動的に同期することに注意してください。 コードまたはデザイナーを使用して作業することができます。

![コードとデザインを表示する](setting-up-database/_static/image5.png)

別のテーブルを追加します。 今回は、Course という名前を使用して、次の T-sql コマンドを使用します。

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

さらにもう一度繰り返して、登録という名前のテーブルを作成します。

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

データベースを配置した後に実行されるスクリプトを使用して、データベースにデータを読み込むことができます。 配置後スクリプトをプロジェクトに追加します。 プロジェクトを右クリックし、新しい項目を追加します。 **配置後スクリプト** > **ユーザースクリプト**を選択します。 既定の名前を使用できます。

次の T-sql コードを配置後スクリプトに追加します。 このスクリプトは、一致するレコードが見つからない場合に、単にデータベースにデータを追加します。 データベースに入力したデータを上書きしたり削除したりすることはありません。

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

配置後スクリプトは、データベースプロジェクトを配置するたびに実行されることに注意してください。 このため、このスクリプトを記述するときは、要件を慎重に検討する必要があります。 場合によっては、プロジェクトが配置されるたびに既知のデータセットからやり直すことが必要になる場合があります。 それ以外の場合は、既存のデータを変更しないようにする必要があります。 要件に基づいて、配置後スクリプトが必要か、スクリプトに含める必要があるものかを決定できます。 配置後スクリプトを使用したデータベースの設定の詳細については、「 [SQL Server データベースプロジェクトにデータを含める](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)」を参照してください。

これで、4つの SQL スクリプトファイルが作成されましたが、実際のテーブルはありません。 これで、データベースプロジェクトを localdb にデプロイする準備が整いました。 Visual Studio で、[スタート] ボタン (または F5 キー) をクリックして、データベースプロジェクトをビルドして配置します。 **[出力]** タブを確認して、ビルドと配置が成功したことを確認します。

新しいデータベースが作成されたことを確認するには、 **SQL Server オブジェクトエクスプローラー**を開き、正しいローカルデータベースサーバー (この場合は**localdb)** でプロジェクトの名前を探します。

テーブルにデータが入力されていることを確認するには、テーブルを右クリックし、 **[データの表示]** を選択します。

![テーブルデータの表示](setting-up-database/_static/image9.png)

テーブルデータの編集可能なビューが表示されます。 たとえば、[**テーブル** > **dbo. course** > **データを表示**する] を選択した場合は、3つの列 (**コース**、**タイトル**、および**クレジット**) と4つの行を含むテーブルが表示されます。

## <a name="additional-resources"></a>その他のリソース

Code First 開発の入門例については、「[はじめに with ASP.NET MVC 5](../introduction/getting-started.md)」を参照してください。 より高度な例については、「 [ASP.NET MVC 4 アプリの Entity Framework データモデルの作成](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。

使用する Entity Framework 方法の選択に関するガイダンスについては、「[開発方法の Entity Framework](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)」を参照してください。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * データベースを設定する

次のチュートリアルに進み、web アプリケーションとデータモデルを作成する方法を学習してください。
> [!div class="nextstepaction"]
> [Web アプリケーションとデータモデルを作成する](creating-the-web-application.md)

---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 'チュートリアル: ASP.NET MVC を使用して EF Database First 用の Web アプリケーションとデータモデルを作成する'
description: このチュートリアルでは、web アプリケーションを作成し、データベーステーブルに基づいてデータモデルを生成する方法について説明します。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499528"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a>チュートリアル: ASP.NET MVC を使用して EF Database First 用の Web アプリケーションとデータモデルを作成する

 MVC、Entity Framework、ASP.NET のスキャフォールディングを使用して、既存のデータベースへのインターフェイスを提供する web アプリケーションを作成できます。 このチュートリアルシリーズでは、ユーザーがデータベーステーブルに格納されているデータを表示、編集、作成、および削除できるようにするコードを自動的に生成する方法について説明します。 生成されたコードは、データベーステーブルの列に対応しています。

このチュートリアルでは、web アプリケーションを作成し、データベーステーブルに基づいてデータモデルを生成する方法について説明します。

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * ASP.NET Web アプリを作成する
> * モデルを生成する

## <a name="prerequisites"></a>前提条件

* [MVC 5 を使用した Entity Framework 6 Database First の概要](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a>ASP.NET Web アプリを作成する

新しいソリューションまたはデータベースプロジェクトと同じソリューションのどちらかで、Visual Studio で新しいプロジェクトを作成し、 **ASP.NET Web アプリケーション**テンプレートを選択します。 プロジェクトに**ContosoSite**という名前を指定します。

![プロジェクトの作成](creating-the-web-application/_static/image1.png)

**[OK]** をクリックします。

New ASP.NET プロジェクト ウィンドウで、 **MVC** テンプレートを選択します。 ここでは、クラウドにアプリケーションを後でデプロイするため、[クラウド] オプション**でホスト**をクリアできます。 **[OK]** をクリックしてアプリケーションを作成します。

既定のファイルとフォルダーを使用してプロジェクトが作成されます。

このチュートリアルでは Entity Framework 6 を使用します。 [NuGet パッケージの管理] ウィンドウで、プロジェクトの Entity Framework のバージョンを再確認できます。 必要に応じて、Entity Framework のバージョンを更新します。

![バージョンの表示](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a>モデルを生成する

次に、データベーステーブルから Entity Framework モデルを作成します。 これらのモデルは、データを操作するために使用するクラスです。 各モデルは、データベース内のテーブルをミラー化し、テーブル内の列に対応するプロパティを格納します。

**[モデル]** フォルダーを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択します。

新しい項目の追加 ウィンドウで、左ペインの **データ** を選択し、中央のウィンドウのオプションから**Entity Data Model を ADO.NET**します。 新しいモデルファイルに**ContosoModel**という名前を指定します。

**[追加]** をクリックします。

Entity Data Model ウィザードで、 **[データベースから EF Designer]** を選択します。

**[次へ]** をクリックします。

開発環境内にデータベース接続が定義されている場合は、これらの接続のいずれかが事前に選択されている可能性があります。 ただし、このチュートリアルの最初の部分で作成したデータベースへの新しい接続を作成する必要があります。 **[新しい接続]** ボタンをクリックします。

接続プロパティウィンドウで、データベースが作成されたローカルサーバーの名前を指定します (この場合は **(localdb)、projectsv13**)。 サーバー名を指定した後、使用可能なデータベースからコンテキストデータを選択します。

![接続プロパティの設定](creating-the-web-application/_static/image8.png)

**[OK]** をクリックします。

これで、正しい接続プロパティが表示されます。 Web.config ファイルでは、接続の既定の名前を使用できます。

**[次へ]** をクリックします。

Entity Framework の最新バージョンを選択します。

**[次へ]** をクリックします。

**[テーブル]** を選択すると、3つのテーブルすべてに対してモデルが生成されます。

**[完了]** をクリックします。

セキュリティの警告が表示された場合は、 **[OK]** を選択してテンプレートの実行を続行します。

モデルはデータベーステーブルから生成され、テーブル間のプロパティとリレーションシップを示すダイアグラムが表示されます。

![モデルの図](creating-the-web-application/_static/image11.png)

[モデル] フォルダーには、データベースから生成されたモデルに関連する多数の新しいファイルが含まれるようになりました。

**ContosoModel.Context.cs**ファイルには、 **dbcontext**クラスから派生したクラスが含まれており、データベーステーブルに対応する各モデルクラスのプロパティを提供します。 **Course.cs**、 **Enrollment.cs**、および**Student.cs**の各ファイルには、databases テーブルを表すモデルクラスが含まれています。 スキャフォールディングを操作するときは、コンテキストクラスとモデルクラスの両方を使用します。

このチュートリアルを続行する前に、プロジェクトをビルドしてください。 次のセクションでは、データモデルに基づいてコードを生成しますが、プロジェクトがビルドされていない場合は、そのセクションは機能しません。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * ASP.NET web アプリを作成しました
> * モデルが生成されました

次のチュートリアルに進み、データモデルに基づいてコードを生成する方法を学習してください。
> [!div class="nextstepaction"]
> [ビューの生成](generating-views.md)

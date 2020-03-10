---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 'チュートリアル: ASP.NET MVC アプリで EF Database First のデータベースを変更する'
description: このチュートリアルでは、データベース構造を更新し、web アプリケーション全体でその変更を反映する方法について説明します。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499522"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a>チュートリアル: ASP.NET MVC アプリで EF Database First のデータベースを変更する

MVC、Entity Framework、ASP.NET のスキャフォールディングを使用して、既存のデータベースへのインターフェイスを提供する web アプリケーションを作成できます。 このチュートリアルシリーズでは、ユーザーがデータベーステーブルに格納されているデータを表示、編集、作成、および削除できるようにするコードを自動的に生成する方法について説明します。 生成されたコードは、データベーステーブルの列に対応しています。

このチュートリアルでは、データベース構造を更新し、web アプリケーション全体でその変更を反映する方法について説明します。

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * 列を追加する
> * ビューにプロパティを追加します。

## <a name="prerequisites"></a>前提条件

* [ビューの生成](generating-views.md)

## <a name="add-a-column"></a>列を追加する

データベース内のテーブルの構造を更新する場合は、変更がデータモデル、ビュー、およびコントローラーに反映されていることを確認する必要があります。

このチュートリアルでは、student テーブルに新しい列を追加して、学生のミドルネームを記録します。 この列を追加するには、データベースプロジェクトを開き、Student .sql ファイルを開きます。 デザイナーまたは T-sql コードを使用して、 **MiddleName**という名前の列を追加します。これは NVARCHAR (50) であり、NULL 値を許容します。

データベースプロジェクト (または F5 キー) を起動して、この変更をローカルデータベースに配置します。 新しいフィールドがテーブルに追加されます。 SQL Server オブジェクトエクスプローラーに表示されない場合は、ウィンドウの [更新] ボタンをクリックします。

![新しい列の表示](changing-the-database/_static/image2.png)

新しい列はデータベーステーブルに存在しますが、現在はデータモデルクラスに存在しません。 新しい列を含めるようにモデルを更新する必要があります。 **[モデル]** フォルダーで、 **ContosoModel**ファイルを開いてモデル図を表示します。 学生モデルには、MiddleName プロパティが含まれていないことに注意してください。 デザイン画面の任意の場所を右クリックし、 **[データベースからモデルを更新]** を選択します。

更新ウィザードで、[最新の情報に**更新**] タブを選択し、[**テーブル** > **dbo** > **Student**] を選択します。 **[完了]** をクリックします。

更新プロセスが完了すると、データベースダイアグラムに新しい**MiddleName**プロパティが含まれます。 **ContosoModel**ファイルを保存します。 新しいプロパティを**Student.cs**クラスに反映させるには、このファイルを保存する必要があります。 これで、データベースとモデルが更新されました。

ソリューションをビルドします。

## <a name="add-the-property-to-the-views"></a>ビューにプロパティを追加します。

残念ながら、ビューには新しいプロパティが含まれていません。 ビューを更新するには、2つのオプションがあります。もう一度 Student クラスのスキャフォールディングを追加することで、ビューを再生成するか、既存のビューに新しいプロパティを手動で追加することができます。 このチュートリアルでは、自動的に生成されたビューに変更を加えていないため、スキャフォールディングを再び追加します。 ビューに変更を加えたときに、その変更が失われないようにする場合は、プロパティを手動で追加することを検討してください。

ビューが再作成されるようにするには、 **[表示]** の下にある **[Students]** フォルダーを削除し、 **StudentsController**を削除します。 次に、 **Controllers**フォルダーを右クリックし、 **Student**モデルのスキャフォールディングを追加します。 ここでも、コントローラーに**StudentsController**という名前を指定します。 **[追加]** を選択します。

ソリューションをもう一度ビルドします。 ビューには、MiddleName プロパティが含まれるようになりました。

![ミドルネームの表示](changing-the-database/_static/image5.png)

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * 列を追加しました
> * ビューにプロパティを追加しました

次のチュートリアルに進み、学生レコードの詳細を表示するようにビューをカスタマイズする方法を学習してください。
> [!div class="nextstepaction"]
> [ビューのカスタマイズ](customizing-a-view.md)
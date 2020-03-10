---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 'チュートリアル: ASP.NET MVC アプリで EF Database First のビューをカスタマイズする'
description: このチュートリアルでは、自動的に生成されたビューを変更してプレゼンテーションを拡張する方法について説明します。
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471520"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a>チュートリアル: ASP.NET MVC アプリで EF Database First のビューをカスタマイズする

MVC、Entity Framework、ASP.NET のスキャフォールディングを使用して、既存のデータベースへのインターフェイスを提供する web アプリケーションを作成できます。 このチュートリアルシリーズでは、ユーザーがデータベーステーブルに格納されているデータを表示、編集、作成、および削除できるようにするコードを自動的に生成する方法について説明します。 生成されたコードは、データベーステーブルの列に対応しています。

このチュートリアルでは、自動的に生成されたビューを変更してプレゼンテーションを拡張する方法について説明します。

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * 学生の詳細ページにコースを追加する
> * コースがページに追加されたことを確認する

## <a name="prerequisites"></a>前提条件

* [データベースの変更](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a>学生の詳細にコースを追加する

生成されたコードはアプリケーションの開始点として適していますが、必ずしもアプリケーションで必要なすべての機能を提供するわけではありません。 コードをカスタマイズして、アプリケーションの特定の要件を満たすことができます。 現在、選択した学生に登録されているコースはアプリケーションで表示されません。 このセクションでは、受講者ごとに登録されているコースを、学生の**詳細**ビューに追加します。

 > **Students** > Details. *Cshtml*という**ビュー**を開きます。 最後の &lt;/dl&gt; タグの下に、終了 &lt;/div&gt; タグの前に、次のコードを追加します。

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

このコードは、選択した学生の登録テーブル内の各レコードの行を表示するテーブルを作成します。 **Display**メソッドは、式を表すオブジェクト (modelitem) の HTML をレンダリングします。 (単にプロパティ値をコードに埋め込むのではなく) 表示メソッドを使用して、その型とその型のテンプレートに基づいて値が正しく書式設定されるようにします。 この例では、各式はループ内の現在のレコードから1つのプロパティを返し、値はテキストとして表示されるプリミティブ型です。

## <a name="confirm-courses-are-added"></a>コースが追加されたことを確認する

ソリューションを実行する **[学生の一覧]** をクリックし、いずれかの学生の **[詳細]** を選択します。 登録されているコースがビューに含まれていることがわかります。

![登録される学生](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a>次のステップ
このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * 学生の詳細ページへのコースの追加
> * コースがページに追加されたことを確認しました

次のチュートリアルに進み、データ注釈を追加して検証要件を指定し、書式設定を表示する方法を学習します。
> [!div class="nextstepaction"]
> [データの検証を強化する](enhancing-data-validation.md)

---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 'チュートリアル: ASP.NET MVC アプリを使用して EF Database First のデータ検証を強化する'
description: このチュートリアルでは、データモデルへのデータ注釈の追加に焦点を当て、検証要件を指定し、書式設定を表示します。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499534"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a>チュートリアル: ASP.NET MVC アプリを使用して EF Database First のデータ検証を強化する

MVC、Entity Framework、ASP.NET のスキャフォールディングを使用して、既存のデータベースへのインターフェイスを提供する web アプリケーションを作成できます。 このチュートリアルシリーズでは、ユーザーがデータベーステーブルに格納されているデータを表示、編集、作成、および削除できるようにするコードを自動的に生成する方法について説明します。 生成されたコードは、データベーステーブルの列に対応しています。

このチュートリアルでは、データモデルへのデータ注釈の追加に焦点を当て、検証要件を指定し、書式設定を表示します。 コメントセクションのユーザーからのフィードバックに基づいて改善されました。

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * データ注釈の追加
> * メタデータクラスの追加

## <a name="prerequisites"></a>前提条件

* [ビューのカスタマイズ](customizing-a-view.md)

## <a name="add-data-annotations"></a>データ注釈の追加

前のトピックで説明したように、一部のデータ検証規則はユーザー入力に自動的に適用されます。 たとえば、"学年" プロパティには数値のみを指定できます。 さらに多くのデータ検証規則を指定するには、モデルクラスにデータ注釈を追加します。 これらの注釈は、指定されたプロパティの web アプリケーション全体に適用されます。 また、プロパティの表示方法を変更する書式設定属性を適用することもできます。たとえば、テキストラベルに使用される値を変更します。

このチュートリアルでは、FirstName、LastName、および MiddleName の各プロパティに指定された値の長さを制限するデータ注釈を追加します。 データベースでは、これらの値は50文字までに制限されています。ただし、web アプリケーションでは、文字制限は現在適用されていません。 ユーザーがこれらの値の1つに対して50文字を超える文字を入力すると、データベースに値を保存しようとしたときにページがクラッシュします。 また、グレードを 0 ~ 4 の値に制限します。

[ > **モデル**] を選択し、 **ContosoModel** > **ContosoModel.tt**を選択して、 *Student.cs*ファイルを開きます。 次の強調表示されたコードをクラスに追加します。

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

*Enrollment.cs*を開き、次の強調表示されたコードを追加します。

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

ソリューションをビルドします。

**[学生の一覧]** をクリックし、 **[編集]** を選択します。 50文字を超える文字を入力しようとすると、エラーメッセージが表示されます。

![エラーメッセージを表示する](enhancing-data-validation/_static/image1.png)

ホームページに戻ります。 登録 **[の一覧]** をクリックし、 **[編集]** を選択します。 4以上のレベルを指定しようとしています。 このエラーが表示されます。*フィールドグレードは0から4までの範囲で指定する必要があります。*

## <a name="add-metadata-classes"></a>メタデータクラスの追加

モデルクラスに検証属性を直接追加することは、データベースが変更されることを期待していない場合に機能します。ただし、データベースが変更され、モデルクラスを再生成する必要がある場合は、モデルクラスに適用したすべての属性が失われます。 このアプローチは、非常に非効率的で、重要な検証ルールが失われる可能性があります。

この問題を回避するには、属性を含むメタデータクラスを追加します。 モデルクラスをメタデータクラスに関連付けると、それらの属性がモデルに適用されます。 この方法では、メタデータクラスに適用されているすべての属性を失うことなく、モデルクラスを再生成できます。

**[モデル]** フォルダーで、 *Metadata.cs*という名前のクラスを追加します。

*Metadata.cs*のコードを次のコードに置き換えます。

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

これらのメタデータクラスには、モデルクラスに以前に適用したすべての検証属性が含まれています。 **表示**属性は、テキストラベルに使用される値を変更するために使用されます。

ここで、モデルクラスをメタデータクラスに関連付ける必要があります。

**[モデル]** フォルダーで、 *PartialClasses.cs*という名前のクラスを追加します。

このファイルの内容を次のコードに置き換えます。

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

各クラスは `partial` クラスとしてマークされ、各クラスは、自動的に生成されるクラスと同じ名前と名前空間に一致することに注意してください。 メタデータ属性を部分クラスに適用することで、データ検証属性が自動的に生成されたクラスに適用されるようになります。 これらの属性は、再生成されない部分クラスにメタデータ属性が適用されるため、モデルクラスを再生成しても失われません。

自動的に生成されたクラスを再生成するには、 *ContosoModel*ファイルを開きます。 ここでも、デザイン画面を右クリックし、 **[データベースからモデルを更新]** を選択します。 データベースを変更していない場合でも、このプロセスによってクラスが再生成されます。 **[更新]** タブで、 **[テーブル]** を選択し、 **[完了**] をクリックします。

*ContosoModel*ファイルを保存して、変更を適用します。

*Student.cs*ファイルまたは*Enrollment.cs*ファイルを開くと、前に適用したデータ検証属性がファイルに存在しなくなっていることがわかります。 ただし、アプリケーションを実行すると、データを入力したときに検証規則が適用されていることがわかります。

## <a name="conclusion"></a>まとめ

このシリーズでは、ユーザーがデータを編集、更新、作成、および削除できるようにする、既存のデータベースからコードを生成する簡単な例を提供しました。 ASP.NET MVC 5、Entity Framework および ASP.NET スキャフォールディングを使用してプロジェクトを作成していました。 

Code First 開発の入門例については、「[はじめに with ASP.NET MVC 5](../introduction/getting-started.md)」を参照してください。 

より高度な例については、「 [ASP.NET MVC 4 アプリの Entity Framework データモデルの作成](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。 Database First のデータを操作するために使用する DbContext API は、Code First でデータを操作するために使用する API と同じであることに注意してください。 Database First を使用する場合でも、関連データの読み取りと更新、同時実行の競合の処理など、より複雑なシナリオを処理する方法については、Code First チュートリアルを参照してください。 唯一の違いは、データベース、コンテキストクラス、およびエンティティクラスの作成方法です。

## <a name="additional-resources"></a>その他のリソース

プロパティとクラスに適用できるデータ検証注釈の完全な一覧については、「 [system.componentmodel](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)」を参照してください。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * 追加されたデータ注釈
> * 追加されたメタデータクラス

Azure App Service に web アプリと SQL データベースをデプロイする方法については、次のチュートリアルを参照してください。
> [!div class="nextstepaction"]
> [Azure App Service に .NET アプリをデプロイする](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)

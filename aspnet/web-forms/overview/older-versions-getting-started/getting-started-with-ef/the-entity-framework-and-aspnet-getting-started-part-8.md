---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート 8 |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションは、Entity Framework を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 サンプルアプリケーションは...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473506"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a>Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート8

[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 チュートリアルシリーズの詳細については、[シリーズの最初のチュートリアル](the-entity-framework-and-aspnet-getting-started-part-1.md)を参照してください。

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a>動的データ機能を使用したデータの書式設定と検証

前のチュートリアルでは、ストアドプロシージャを実装しています。 このチュートリアルでは、動的データ機能によって次のような利点が得られることについて説明します。

- フィールドは、データ型に基づいて自動的に書式設定されます。
- フィールドは、データ型に基づいて自動的に検証されます。
- データモデルにメタデータを追加して、書式設定や検証の動作をカスタマイズできます。 これを行うと、書式設定規則と検証規則を1つの場所にのみ追加できます。また、動的データコントロールを使用して、フィールドにアクセスするすべての場所に自動的に適用されます。

これがどのように動作するかを確認するには、既存の*student .aspx*ページのフィールドの表示と編集に使用するコントロールを変更し、`Student` エンティティ型の名前と日付のフィールドに書式設定および検証メタデータを追加します。

[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a>DynamicField および Dynamicfield コントロールの使用

*Student*ページを開き、`StudentsGridView` コントロールで、**名前**と**登録の日付**`TemplateField` 要素を次のマークアップに置き換えます。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

このマークアップは、[student name template] フィールドの `TextBox` および `Label` コントロールの代わりに `DynamicControl` コントロールを使用し、登録日に `DynamicField` コントロールを使用します。 書式指定文字列が指定されていません。

`StudentsGridView` コントロールの後に `ValidationSummary` コントロールを追加します。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

`SearchGridView` コントロールで、 **[名前]** 列と **[登録日付]** 列のマークアップを、`StudentsGridView` コントロールで行ったように置き換えます。ただし、`EditItemTemplate` 要素は省略します。 `SearchGridView` コントロールの `Columns` 要素には、次のマークアップが含まれるようになりました。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

*Students.aspx.cs*を開き、次の `using` ステートメントを追加します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

ページの `Init` イベントのハンドラーを追加します。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

このコードは、`Student` エンティティのフィールドに対して、これらのデータバインドコントロールで書式設定と検証を行う動的データことを指定します。 ページを実行するときに、次の例のようなエラーメッセージが表示された場合は、通常、`Page_Init`で `EnableDynamicData` メソッドを呼び出さないことを意味します。

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

ページを実行します。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)

**[登録日]** 列には、プロパティの型が `DateTime`なので、日付と共に時刻が表示されます。 これは後で修正します。

ここでは、動的データによって基本的なデータの検証が自動的に提供されることに注意してください。 たとえば、 **[編集]** をクリックし、日付 フィールドをオフにして、 **[更新]** をクリックすると、データモデルで null 値が許容されないため、動的データによって自動的に必須フィールドになります。 このページでは、フィールドの後にアスタリスクが表示され、`ValidationSummary` コントロールにエラーメッセージが表示されます。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)

エラーメッセージを表示するには、アスタリスクの上にマウスポインターを置くこともできるため、`ValidationSummary` コントロールを省略できます。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)

また動的データは、**登録日**フィールドに入力されたデータが有効な日付であることを検証します。

[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)

ご覧のように、これは一般的なエラーメッセージです。 次のセクションでは、メッセージのカスタマイズ方法と検証規則および書式設定規則について説明します。

## <a name="adding-metadata-to-the-data-model"></a>データモデルへのメタデータの追加

通常は、動的データによって提供される機能をカスタマイズします。 たとえば、データの表示方法とエラーメッセージの内容を変更することができます。 また、データ型に基づいて自動的に提供される機能動的データよりも多くの機能を提供するように、データ検証ルールをカスタマイズすることもできます。 これを行うには、エンティティ型に対応する部分クラスを作成します。

**ソリューションエクスプローラー**で、 **ContosoUniversity**プロジェクトを右クリックし、 **[参照の追加]** を選択して、`System.ComponentModel.DataAnnotations`への参照を追加します。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)

*DAL*フォルダーで、新しいクラスファイルを作成し、 *Student.cs*という名前を付け、テンプレートコードを次のコードに置き換えます。

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

このコードでは、`Student` エンティティの部分クラスを作成します。 この部分クラスに適用される `MetadataType` 属性は、メタデータの指定に使用しているクラスを識別します。 メタデータクラスには任意の名前を付けることができますが、エンティティ名と "メタデータ" を使用するのが一般的な方法です。

メタデータクラスのプロパティに適用される属性は、書式設定、検証、規則、およびエラーメッセージを指定します。 ここに表示される属性の結果は次のようになります。

- `EnrollmentDate` は日付として表示されます (時刻は含まれません)。
- 両方の名前フィールドは25文字以下である必要があり、カスタムエラーメッセージが表示されます。
- 両方の名前フィールドが必須であり、カスタムエラーメッセージが表示されます。

もう一度*student*ページを実行すると、日付が何度も表示されなくなっていることがわかります。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)

行を編集して、[名前] フィールドの値をクリアします。 **[更新]** をクリックする前に、フィールドを終了するとすぐにフィールドエラーを示すアスタリスクが表示されます。 **[更新]** をクリックすると、指定したエラーメッセージのテキストがページに表示されます。

[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)

25文字を超える名前を入力してください。 **[更新]** をクリックすると、指定したエラーメッセージのテキストが表示されます。

[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)

これで、これらの書式設定と検証規則がデータモデルメタデータに設定されたので、`DynamicControl` または `DynamicField` コントロールを使用している限り、これらのフィールドを表示または変更できるすべてのページに規則が自動的に適用されます。 これにより、記述する必要がある冗長なコードの量が減り、プログラミングとテストが容易になり、アプリケーション全体でデータの書式設定と検証の一貫性が保たれます。

## <a name="more-information"></a>詳細情報

これで、Entity Framework を使用したはじめにに関するこの一連のチュートリアルは終了です。 Entity Framework の使用方法を学習するのに役立つその他のリソースについては、[次の Entity Framework チュートリアルシリーズの最初のチュートリアル](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)に進んでください。または、次のサイトを参照してください。

- [Entity Framework FAQ](http://www.ef-faq.org/introduction.html)
- [Entity Framework チームのブログ](https://blogs.msdn.com/b/adonet/)
- [MSDN ライブラリの Entity Framework](https://msdn.microsoft.com/library/bb399572.aspx)
- [MSDN Data Developer Center の Entity Framework](https://msdn.microsoft.com/data/ef.aspx)
- [MSDN ライブラリの EntityDataSource Web サーバーコントロールの概要](https://msdn.microsoft.com/library/cc488502.aspx)
- [MSDN ライブラリの EntityDataSource control API リファレンス](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [MSDN の Entity Framework フォーラム](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [ジュリー Lerman のブログ](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [[戻る]](the-entity-framework-and-aspnet-getting-started-part-7.md)

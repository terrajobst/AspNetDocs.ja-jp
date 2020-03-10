---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
title: Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート 6 |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションは、Entity Framework を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 サンプルアプリケーションは...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 994a5496-c648-4830-b03c-55bb43f325d2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
msc.type: authoredcontent
ms.openlocfilehash: 8bfbe74f90eb03ea9aab7610842ef2578e80d113
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454918"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-6"></a>Entity Framework 4.0 Database First および ASP.NET 4 Web フォームでのはじめに-パート6

[Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 4.0 と Visual Studio 2010 を使用して ASP.NET Web フォームアプリケーションを作成する方法を示しています。 チュートリアルシリーズの詳細については、[シリーズの最初のチュートリアル](the-entity-framework-and-aspnet-getting-started-part-1.md)を参照してください。

## <a name="implementing-table-per-hierarchy-inheritance"></a>Table-Per-Hierarchy 継承の実装

前のチュートリアルでは、リレーションシップを追加および削除し、既存のエンティティとのリレーションシップを持つ新しいエンティティを追加することによって、関連データを操作しました。 このチュートリアルでは、データ モデルで継承を実装する方法を示します。

オブジェクト指向プログラミングでは、継承を使用して、関連するクラスを簡単に操作できるようになります。 たとえば、`Person` の基底クラスから派生したクラス `Instructor` と `Student` を作成できます。 Entity Framework では、エンティティ間に同じ種類の継承構造を作成できます。

チュートリアルのこの部分では、新しい web ページを作成しません。 代わりに、派生エンティティをデータモデルに追加し、既存のページを変更して新しいエンティティを使用します。

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>階層ごとのテーブルと型ごとの継承の比較

データベースでは、関連するオブジェクトに関する情報を1つのテーブルまたは複数のテーブルに格納できます。 たとえば、`School` データベースの場合、`Person` テーブルには、1つのテーブルに学生とインストラクターの両方に関する情報が含まれています。 一部の列は、インストラクター (`HireDate`) にのみ適用されます。学生のみに (`EnrollmentDate`)、一部は (`LastName`、`FirstName`) にのみ適用されます。

[![image11](the-entity-framework-and-aspnet-getting-started-part-6/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image1.png)

Entity Framework を構成して、`Person` エンティティから継承する `Instructor` と `Student` エンティティを作成できます。 1つのデータベーステーブルからエンティティの継承構造を生成するこのパターンは、*階層単位*(TPH) の継承と呼ばれます。

コースの場合、`School` データベースは別のパターンを使用します。 オンラインコースとオンサイトコースは別々のテーブルに格納されており、各テーブルには `Course` テーブルを指す外部キーがあります。 両方のコースの種類に共通する情報は、`Course` テーブルにのみ格納されます。

[![image12](the-entity-framework-and-aspnet-getting-started-part-6/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image3.png)

`OnlineCourse` エンティティと `OnsiteCourse` エンティティが `Course` エンティティから継承されるように、Entity Framework データモデルを構成できます。 このパターンでは、各型に対して個別のテーブルからエンティティの継承構造を生成しています。各テーブルは、すべての型に共通のデータを格納するテーブルを参照しています。このパターンは、 *table per type* (TPT) 継承と呼ばれます。

TPH 継承パターンを使用すると、一般に、TPT 継承パターンよりも Entity Framework でパフォーマンスが向上します。 TPT パターンでは、複雑な結合クエリが発生する可能性があるためです。 このチュートリアルでは、TPH 継承を実装する方法について説明します。 これを行うには、次の手順を実行します。

- `Person`から派生するエンティティ型 `Instructor` および `Student` を作成します。
- 派生エンティティに関連するプロパティを、`Person` エンティティから派生エンティティに移動します。
- 派生型のプロパティに制約を設定します。
- `Person` エンティティを抽象エンティティにします。
- `Person` の行がその派生型を表すかどうかを判断する方法を指定する条件を使用して、各派生エンティティを `Person` テーブルにマップします。

## <a name="adding-instructor-and-student-entities"></a>講師と学生のエンティティの追加

<em>SchoolModel</em>ファイルを開き、デザイナーで未使用の領域を右クリックし、[<strong>追加</strong>]、[<strong>エンティティ</strong>] の順に選択し<em>ます。</em>

[![image01](the-entity-framework-and-aspnet-getting-started-part-6/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image5.png)

**エンティティの追加** ダイアログボックスで、エンティティに `Instructor` という名前を指定し、**基本データ型** オプションを `Person`に設定します。

[![image02](the-entity-framework-and-aspnet-getting-started-part-6/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image7.png)

**[OK]** をクリックします。 デザイナーは、`Person` エンティティから派生する `Instructor` エンティティを作成します。 新しいエンティティにはプロパティがまだありません。

[![image03](the-entity-framework-and-aspnet-getting-started-part-6/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image9.png)

手順を繰り返して、`Person`からも派生する `Student` エンティティを作成します。

インストラクターのみが入社日を持っているため、そのプロパティを `Person` エンティティから `Instructor` エンティティに移動する必要があります。 `Person` エンティティで `HireDate` プロパティを右クリックし、 **[切り取り]** をクリックします。 次に、`Instructor` エンティティで **[プロパティ]** を右クリックし、 **[貼り付け]** をクリックします。

[![image04](the-entity-framework-and-aspnet-getting-started-part-6/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image11.png)

`Instructor` エンティティの入社日を null にすることはできません。 `HireDate` プロパティを右クリックし、 **[プロパティ]** をクリックします。次に、 **[プロパティ]** ウィンドウで `Nullable` を `False`に変更します。

[![image05](the-entity-framework-and-aspnet-getting-started-part-6/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image13.png)

この手順を繰り返して、`Person` エンティティから `Student` エンティティに `EnrollmentDate` プロパティを移動します。 `EnrollmentDate` プロパティの `False` に `Nullable` も設定していることを確認します。

`Person` エンティティには、`Instructor` および `Student` のエンティティに共通するプロパティのみがあるため (移動していないナビゲーションプロパティを除く)、エンティティは継承構造の基本エンティティとしてのみ使用できます。 そのため、独立したエンティティとして扱われないようにする必要があります。 `Person` エンティティを右クリックし、 **[プロパティ]** をクリックします。次に、 **[プロパティ]** ウィンドウで、 **[Abstract]** プロパティの値を**True**に変更します。

[![image06](the-entity-framework-and-aspnet-getting-started-part-6/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image15.png)

## <a name="mapping-instructor-and-student-entities-to-the-person-table"></a>インストラクターと学生のエンティティを Person テーブルにマップする

次に、データベース内の `Instructor` エンティティと `Student` エンティティを区別する方法を Entity Framework に指示する必要があります。

`Instructor` エンティティを右クリックし、 **[テーブルマッピング]** を選択します。 **[マッピングの詳細]** ウィンドウで、 **[テーブルまたはビューの追加]** をクリックし、 **[個人]** を選択します。

[![image07](the-entity-framework-and-aspnet-getting-started-part-6/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image17.png)

**[条件の追加]** をクリックし、 **[HireDate]** を選択します。

[![image09](the-entity-framework-and-aspnet-getting-started-part-6/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image19.png)

**演算子**を**Is**に、**値/プロパティ**を**not Null**に変更します。

[![image10](the-entity-framework-and-aspnet-getting-started-part-6/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image21.png)

`Students` エンティティに対してこの手順を繰り返し、`EnrollmentDate` 列が null でない場合にこのエンティティが `Person` テーブルにマップされるように指定します。 次に、データモデルを保存して閉じます。

新しいエンティティをクラスとして作成し、デザイナーで使用できるようにするために、プロジェクトをビルドします。

## <a name="using-the-instructor-and-student-entities"></a>講師と学生のエンティティの使用

学生およびインストラクターのデータを使用する web ページを作成した場合は、それらを `Person` エンティティセットにデータバインドし、`HireDate` または `EnrollmentDate` プロパティをフィルター処理して、返されるデータを学生またはインストラクターに限定します。 ただし現在は、各データソースコントロールを `Person` エンティティセットにバインドするときに、`Student` または `Instructor` のエンティティ型のみを選択するように指定できます。 Entity Framework は、`Person` エンティティセットで学生とインストラクターを区別する方法を認識しているので、手動で入力した `Where` プロパティ設定を削除することができます。

次の例に示すように、Visual Studio デザイナーでは、`EntityDataSource` コントロールが `Configure Data Source` ウィザードの **[EntityTypeFilter]** ボックスで選択する必要があるエンティティ型を指定できます。

[![image13](the-entity-framework-and-aspnet-getting-started-part-6/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image23.png)

また、 **[プロパティ]** ウィンドウでは、次の例に示すように、不要になった `Where` 句の値を削除できます。

[![image14](the-entity-framework-and-aspnet-getting-started-part-6/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image25.png)

ただし、`ContextTypeName` 属性を使用するように `EntityDataSource` コントロールのマークアップを変更したため、既に作成したコントロールに `EntityDataSource` 対して**データソースの構成**ウィザードを実行することはできません。 そのため、代わりにマークアップを変更することによって、必要な変更を行います。

*Student .aspx*ページを開きます。 `StudentsEntityDataSource` コントロールで、`Where` 属性を削除し、`EntityTypeFilter="Student"` 属性を追加します。 マークアップは、次の例のようになります。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample1.aspx)]

`EntityTypeFilter` 属性を設定すると、`EntityDataSource` コントロールが指定されたエンティティ型のみを選択するようになります。 `Student` と `Instructor` の両方のエンティティ型を取得する場合は、この属性を設定しません。 (読み取り専用データアクセスに対してコントロールを使用している場合にのみ、1つの `EntityDataSource` コントロールを持つ複数のエンティティ型を取得することもできます。 エンティティを挿入、更新、または削除するために `EntityDataSource` コントロールを使用していて、バインドされているエンティティセットに複数の型を含めることができる場合は、1つのエンティティ型のみを使用でき、この属性を設定する必要があります。

`SearchEntityDataSource` コントロールに対してこの手順を繰り返します。ただし、プロパティを完全に削除するのではなく `Student` エンティティを選択する `Where` 属性の部分のみを削除します。 コントロールの開始タグは、次の例のようになります。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample2.aspx)]

ページを実行して、以前と同じように動作することを確認します。

[![image15](the-entity-framework-and-aspnet-getting-started-part-6/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image27.png)

前のチュートリアルで作成した次のページを更新して、`Person` エンティティではなく新しい `Student` と `Instructor` エンティティを使用し、それを実行して前と同じように動作することを確認します。

- *StudentsAdd*で、`StudentsEntityDataSource` コントロールに `EntityTypeFilter="Student"` を追加します。 マークアップは、次の例のようになります。 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample3.aspx)]

    [![image16](the-entity-framework-and-aspnet-getting-started-part-6/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image29.png)
- *About .aspx*で、`StudentStatisticsEntityDataSource` コントロールに `EntityTypeFilter="Student"` を追加し、`Where="it.EnrollmentDate is not null"`を削除します。 マークアップは、次の例のようになります。 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample4.aspx)]

    [![image17](the-entity-framework-and-aspnet-getting-started-part-6/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image31.png)
- *講師*と*InstructorsCourses*で、`InstructorsEntityDataSource` コントロールに `EntityTypeFilter="Instructor"` を追加し、`Where="it.HireDate is not null"`を削除します。 これで、*講師*のマークアップは次の例のようになります。 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample5.aspx)]

    [![image18](the-entity-framework-and-aspnet-getting-started-part-6/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image33.png)

    *InstructorsCourses*のマークアップは、次の例のようになります。

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample6.aspx)]

    [![image19](the-entity-framework-and-aspnet-getting-started-part-6/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image35.png)

これらの変更の結果として、Contoso 大学アプリケーションの保守容易性がいくつかの点で改善されました。 選択と検証のロジックを UI レイヤー ( *.aspx*マークアップ) から移動し、データアクセス層の重要な部分にしました。 これにより、将来的にデータベーススキーマまたはデータモデルに加えられた変更からアプリケーションコードを分離することができます。 たとえば、学生が教師の補助として採用されている可能性があるため、採用日を取得するとします。 次に、新しいプロパティを追加して、講師と生徒を区別し、データモデルを更新できます。 学生の入社日を表示する場合を除き、web アプリケーションのコードを変更する必要はありません。 `Instructor` エンティティと `Student` エンティティを追加するもう1つの利点は、実際に生徒やインストラクターの `Person` オブジェクトを参照するよりも、コードがより簡単に理解できることです。

これで、Entity Framework に継承パターンを実装する1つの方法が見られました。 次のチュートリアルでは、Entity Framework がデータベースにアクセスする方法をより細かく制御するために、ストアドプロシージャを使用する方法について説明します。

> [!div class="step-by-step"]
> [前へ](the-entity-framework-and-aspnet-getting-started-part-5.md)
> [次へ](the-entity-framework-and-aspnet-getting-started-part-7.md)

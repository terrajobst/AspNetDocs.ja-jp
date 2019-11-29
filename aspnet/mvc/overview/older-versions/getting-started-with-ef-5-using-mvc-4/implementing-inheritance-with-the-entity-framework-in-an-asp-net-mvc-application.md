---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーションでの Entity Framework による継承の実装 (8/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595319"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="d023e-103">ASP.NET MVC アプリケーションでの Entity Framework による継承の実装 (8/10)</span><span class="sxs-lookup"><span data-stu-id="d023e-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>

<span data-ttu-id="d023e-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d023e-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="d023e-105">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="d023e-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="d023e-106">Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d023e-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="d023e-107">チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d023e-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="d023e-108">チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。</span><span class="sxs-lookup"><span data-stu-id="d023e-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="d023e-109">解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。</span><span class="sxs-lookup"><span data-stu-id="d023e-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="d023e-110">一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="d023e-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="d023e-111">一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d023e-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="d023e-112">前のチュートリアルでは、同時実行例外を処理しています。</span><span class="sxs-lookup"><span data-stu-id="d023e-112">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="d023e-113">このチュートリアルでは、データ モデルで継承を実装する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="d023e-113">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="d023e-114">オブジェクト指向プログラミングでは、継承を使用して冗長なコードを排除できます。</span><span class="sxs-lookup"><span data-stu-id="d023e-114">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="d023e-115">このチュートリアルでは、`Instructor` と `Student` クラスを `Person` 基底クラスから派生するように変更します。この基底クラスはインストラクターと受講者の両方に共通な `LastName` などのプロパティを含んでいます。</span><span class="sxs-lookup"><span data-stu-id="d023e-115">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="d023e-116">どの Web ページも追加または変更しませんが、コードの一部を変更し、それらの変更はデータベースに自動的に反映されます。</span><span class="sxs-lookup"><span data-stu-id="d023e-116">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="d023e-117">階層ごとのテーブルと型ごとの継承の比較</span><span class="sxs-lookup"><span data-stu-id="d023e-117">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="d023e-118">オブジェクト指向プログラミングでは、継承を使用して、関連するクラスを簡単に操作できるようになります。</span><span class="sxs-lookup"><span data-stu-id="d023e-118">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="d023e-119">たとえば、`School` データモデルの `Instructor` クラスと `Student` クラスは、次のようないくつかのプロパティを共有します。これにより、冗長なコードが生成されます。</span><span class="sxs-lookup"><span data-stu-id="d023e-119">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="d023e-121">`Instructor` エンティティと `Student` エンティティで共有されるプロパティの冗長なコードを削除すると仮定します。</span><span class="sxs-lookup"><span data-stu-id="d023e-121">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="d023e-122">次の図に示すように、共有プロパティだけを含む `Person` 基本クラスを作成し、その基本クラスから `Instructor` と `Student` のエンティティを継承させることができます。</span><span class="sxs-lookup"><span data-stu-id="d023e-122">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="d023e-124">データベースでこの継承構造を表すことができるいくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="d023e-124">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="d023e-125">1つのテーブルに学生とインストラクターの両方に関する情報を含む `Person` テーブルを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="d023e-125">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="d023e-126">一部の列は、インストラクター (`HireDate`) にのみ適用されます。学生のみに (`EnrollmentDate`)、一部の列 (`LastName`、`FirstName`) にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="d023e-126">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="d023e-127">通常、各行が表す型を示す*識別子*列があります。</span><span class="sxs-lookup"><span data-stu-id="d023e-127">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="d023e-128">たとえば、識別子列にインストラクターを示す "Instructor" と受講者を示す "Student" がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="d023e-128">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![Hierarchy_example あたりのテーブル数](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="d023e-130">1つのデータベーステーブルからエンティティの継承構造を生成するこのパターンは、*階層単位*(TPH) の継承と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="d023e-130">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="d023e-131">代わりに、継承構造と同じように見えるデータベースを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="d023e-131">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="d023e-132">たとえば、`Person` テーブルには name フィールドだけを指定し、`Instructor` テーブルと `Student` テーブルには日付フィールドを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="d023e-132">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Type_inheritance あたりのテーブル数](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="d023e-134">各エンティティクラスのデータベーステーブルを作成するこのパターンは、 *table per type* (TPT) 継承と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="d023e-134">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="d023e-135">TPH 継承パターンを使用すると、一般に、TPT 継承パターンよりも Entity Framework でパフォーマンスが向上します。 TPT パターンでは、複雑な結合クエリが発生する可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="d023e-135">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="d023e-136">このチュートリアルでは、TPH 継承の実装方法を示します。</span><span class="sxs-lookup"><span data-stu-id="d023e-136">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="d023e-137">これを行うには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="d023e-137">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="d023e-138">`Person` クラスを作成し、`Person`から派生するように `Instructor` および `Student` クラスを変更します。</span><span class="sxs-lookup"><span data-stu-id="d023e-138">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="d023e-139">データベースコンテキストクラスにモデルとデータベースのマッピングコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="d023e-139">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="d023e-140">プロジェクト全体で `InstructorID` および `StudentID` 参照を変更して `PersonID`します。</span><span class="sxs-lookup"><span data-stu-id="d023e-140">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="d023e-141">Person クラスの作成</span><span class="sxs-lookup"><span data-stu-id="d023e-141">Creating the Person Class</span></span>

 <span data-ttu-id="d023e-142">注: これらのクラスを使用するコントローラーを更新するまで、以下のクラスを作成した後にプロジェクトをコンパイルすることはできません。</span><span class="sxs-lookup"><span data-stu-id="d023e-142">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="d023e-143">[*モデル*] フォルダーで*Person.cs*を作成し、テンプレートコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="d023e-143">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="d023e-144">*Instructor.cs*で、`Person` クラスから `Instructor` クラスを派生させ、key フィールドと name フィールドを削除します。</span><span class="sxs-lookup"><span data-stu-id="d023e-144">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="d023e-145">コードは次の例のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="d023e-145">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="d023e-146">*Student.cs*に同様の変更を加えます。</span><span class="sxs-lookup"><span data-stu-id="d023e-146">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="d023e-147">`Student` クラスは次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="d023e-147">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="d023e-148">Person エンティティ型をモデルに追加する</span><span class="sxs-lookup"><span data-stu-id="d023e-148">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="d023e-149">*SchoolContext.cs*で、`Person` エンティティ型の `DbSet` プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="d023e-149">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="d023e-150">Table-per-Hierarchy 継承を構成するために Entity Framework に必要なのことはこれですべてです。</span><span class="sxs-lookup"><span data-stu-id="d023e-150">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="d023e-151">ご覧のように、データベースを再作成すると、`Student` テーブルと `Instructor` テーブルの代わりに `Person` テーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="d023e-151">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="d023e-152">InstructorID と StudentID を PersonID に変更する</span><span class="sxs-lookup"><span data-stu-id="d023e-152">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="d023e-153">*SchoolContext.cs*のインストラクター-講座マッピングステートメントで、`MapRightKey("InstructorID")` を `MapRightKey("PersonID")`に変更します。</span><span class="sxs-lookup"><span data-stu-id="d023e-153">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="d023e-154">この変更は必要ありません。これは、多対多の結合テーブルの InstructorID 列の名前を変更するだけです。</span><span class="sxs-lookup"><span data-stu-id="d023e-154">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="d023e-155">名前を InstructorID として残した場合でも、アプリケーションは正常に動作します。</span><span class="sxs-lookup"><span data-stu-id="d023e-155">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="d023e-156">完成した*SchoolContext.cs*は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="d023e-156">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="d023e-157">次に、`InstructorID` を `PersonID` に変更し、[*移行*] フォルダー内のタイムスタンプ付きの移行ファイルを***除き***、プロジェクト全体で `PersonID` に `StudentID` する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d023e-157">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except*** in the time-stamped migrations files in the *Migrations* folder.</span></span> <span data-ttu-id="d023e-158">これを行うには、変更する必要があるファイルのみを見つけて開き、開いたファイルに対してグローバルな変更を実行します。</span><span class="sxs-lookup"><span data-stu-id="d023e-158">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="d023e-159">変更する必要がある*移行*フォルダー内のファイルは*Migrations\Configuration.cs.* だけです。</span><span class="sxs-lookup"><span data-stu-id="d023e-159">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
   > <span data-ttu-id="d023e-160">まず、Visual Studio で開いているすべてのファイルを閉じます。</span><span class="sxs-lookup"><span data-stu-id="d023e-160">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="d023e-161">**検索と置換** をクリックし、**編集** メニューの すべてのファイルを検索 をクリックし、`InstructorID`を含むプロジェクト内のすべてのファイルを検索します。</span><span class="sxs-lookup"><span data-stu-id="d023e-161">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="d023e-162">**[検索結果]** ウィンドウで各ファイルを開きます。***ただし***、[*マイグレー*ション] フォルダーにある [&lt;タイムスタンプ&gt; *\_* ] をクリックして、各ファイルの1行をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="d023e-162">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="d023e-163">[**フォルダーを**選択して置換] ダイアログを開き、開いている**すべてのドキュメント**に移動します。</span><span class="sxs-lookup"><span data-stu-id="d023e-163">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="d023e-164">[フォルダーを選択して**置換**] ダイアログボックスを使用して、すべての `InstructorID` を `PersonID.` に変更します。</span><span class="sxs-lookup"><span data-stu-id="d023e-164">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="d023e-165">`StudentID`が含まれているプロジェクト内のすべてのファイルを検索します。</span><span class="sxs-lookup"><span data-stu-id="d023e-165">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="d023e-166">**検索結果** ウィンドウで各ファイルを開きます。***ただし*** *、migration フォルダーに*ある &lt;タイムスタンプ&gt; *\_\** の場合は、各ファイルの1行をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="d023e-166">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="d023e-167">[**フォルダーを**選択して置換] ダイアログを開き、開いている**すべてのドキュメント**に移動します。</span><span class="sxs-lookup"><span data-stu-id="d023e-167">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="d023e-168">[**フォルダーを**選択して置換] ダイアログボックスを使用すると、すべての `StudentID` を `PersonID`に変更できます。</span><span class="sxs-lookup"><span data-stu-id="d023e-168">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="d023e-169">プロジェクトをビルドする。</span><span class="sxs-lookup"><span data-stu-id="d023e-169">Build the project.</span></span>

<span data-ttu-id="d023e-170">(これは、主キーの名前付けに `classnameID` パターンの*欠点*を示すことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d023e-170">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="d023e-171">クラス名の前にプレフィックスを付けずに主キー ID を指定した場合は、名前を変更する必要は*ありません*)。</span><span class="sxs-lookup"><span data-stu-id="d023e-171">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="d023e-172">移行ファイルを作成および更新する</span><span class="sxs-lookup"><span data-stu-id="d023e-172">Create and Update a Migrations File</span></span>

<span data-ttu-id="d023e-173">パッケージマネージャーコンソール (PMC) で、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="d023e-173">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="d023e-174">PMC で `Update-Database` コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="d023e-174">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="d023e-175">この時点では、移行によって処理方法がわからない既存のデータがあるため、このコマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="d023e-175">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="d023e-176">次のエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d023e-176">You get the following error:</span></span>

<span data-ttu-id="d023e-177">*ALTER TABLE ステートメントが FOREIGN KEY 制約 "FK\_dbo と競合しています。Department\_dbo です。Person\_PersonID "。データベース "ContosoUniversity"、テーブル "dbo で競合が発生しました。Person ", column ' PersonID '。*</span><span class="sxs-lookup"><span data-stu-id="d023e-177">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="d023e-178">移行を開いて *\&lt; timestamp&gt;\_Inheritance.cs*を開き、`Up` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="d023e-178">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="d023e-179">`update-database` コマンドをもう一度実行します。</span><span class="sxs-lookup"><span data-stu-id="d023e-179">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="d023e-180">データを移行してスキーマを変更するときに、他のエラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d023e-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="d023e-181">解決できない移行エラーが発生した場合*は、web.config ファイルの*接続文字列を変更するか、データベースを削除することで、チュートリアルを続行できます。</span><span class="sxs-lookup"><span data-stu-id="d023e-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="d023e-182">最も簡単な方法*は、web.config ファイル内*のデータベースの名前を変更することです。</span><span class="sxs-lookup"><span data-stu-id="d023e-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="d023e-183">たとえば、次の例に示すように、データベース名を CU\_test に変更します。</span><span class="sxs-lookup"><span data-stu-id="d023e-183">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="d023e-184">新しいデータベースでは、移行するデータは存在せず、`update-database` のコマンドはエラーなしで完了する可能性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="d023e-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="d023e-185">データベースを削除する方法については、「 [Visual Studio 2012 からデータベースを削除する方法](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d023e-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="d023e-186">このチュートリアルを続行するには、このチュートリアルの最後にあるデプロイ手順をスキップします。これは、展開されたサイトが移行を自動的に実行するときに、同じエラーが発生するためです。</span><span class="sxs-lookup"><span data-stu-id="d023e-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="d023e-187">移行エラーのトラブルシューティングを行う場合は、Entity Framework フォーラムまたは StackOverflow.com のいずれかのリソースを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d023e-187">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="testing"></a><span data-ttu-id="d023e-188">Testing (テスト)</span><span class="sxs-lookup"><span data-stu-id="d023e-188">Testing</span></span>

<span data-ttu-id="d023e-189">サイトを実行し、さまざまなページを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="d023e-189">Run the site and try various pages.</span></span> <span data-ttu-id="d023e-190">すべてが前と同じように動作します。</span><span class="sxs-lookup"><span data-stu-id="d023e-190">Everything works the same as it did before.</span></span>

<span data-ttu-id="d023e-191">**サーバーエクスプローラーで、** **[schoolcontext.cs]** 、 **[Tables]** の順に展開し、 **Student**テーブルと**教師**テーブルが**Person**テーブルに置き換えられていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d023e-191">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="d023e-192">**Person**テーブルを展開すると、 **Student**テーブルと**教師**テーブルに使用されていたすべての列が含まれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="d023e-192">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="d023e-194">Person テーブルを右クリックし、 **[テーブル データの表示]** をクリックして識別子列を表示します。</span><span class="sxs-lookup"><span data-stu-id="d023e-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="d023e-195">次の図は、新しい School データベースの構造を示しています。</span><span class="sxs-lookup"><span data-stu-id="d023e-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="d023e-197">要約</span><span class="sxs-lookup"><span data-stu-id="d023e-197">Summary</span></span>

<span data-ttu-id="d023e-198">`Person`、`Student`、および `Instructor` の各クラスに対して、階層構造の継承が実装されました。</span><span class="sxs-lookup"><span data-stu-id="d023e-198">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="d023e-199">このとその他の継承構造の詳細については、「Morteza Manavi のブログの[継承マッピング方法](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d023e-199">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="d023e-200">次のチュートリアルでは、リポジトリと作業単位パターンを実装するいくつかの方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d023e-200">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="d023e-201">その他の Entity Framework リソースへのリンクについては、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d023e-201">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d023e-202">[前へ](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [次へ](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="d023e-202">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>

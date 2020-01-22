---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'チュートリアル: ASP.NET MVC 5 アプリで EF を使用して継承を実装する'
description: このチュートリアルでは、データ モデルで継承を実装する方法を示します。
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 73a01ed47b0935a1a9734c197377470defb1fe36
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519389"
---
# <a name="tutorial-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a><span data-ttu-id="e1551-103">チュートリアル: ASP.NET MVC 5 アプリで EF を使用して継承を実装する</span><span class="sxs-lookup"><span data-stu-id="e1551-103">Tutorial: Implement Inheritance with EF in an ASP.NET MVC 5 app</span></span>

<span data-ttu-id="e1551-104">前のチュートリアルでは、同時実行例外を処理しています。</span><span class="sxs-lookup"><span data-stu-id="e1551-104">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="e1551-105">このチュートリアルでは、データ モデルで継承を実装する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="e1551-105">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="e1551-106">オブジェクト指向プログラミングでは、[継承](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming))を使用して[コードの再利用](http://en.wikipedia.org/wiki/Code_reuse)を容易にすることができます。</span><span class="sxs-lookup"><span data-stu-id="e1551-106">In object-oriented programming, you can use [inheritance](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) to facilitate [code reuse](http://en.wikipedia.org/wiki/Code_reuse).</span></span> <span data-ttu-id="e1551-107">このチュートリアルでは、`Instructor` と `Student` クラスを `Person` 基底クラスから派生するように変更します。この基底クラスはインストラクターと受講者の両方に共通な `LastName` などのプロパティを含んでいます。</span><span class="sxs-lookup"><span data-stu-id="e1551-107">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="e1551-108">どの Web ページも追加または変更しませんが、コードの一部を変更し、それらの変更はデータベースに自動的に反映されます。</span><span class="sxs-lookup"><span data-stu-id="e1551-108">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

<span data-ttu-id="e1551-109">このチュートリアルでは、次の作業を行います。</span><span class="sxs-lookup"><span data-stu-id="e1551-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1551-110">継承をデータベースにマップする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e1551-110">Learn to map inheritance to database</span></span>
> * <span data-ttu-id="e1551-111">Person クラスの作成</span><span class="sxs-lookup"><span data-stu-id="e1551-111">Create the Person class</span></span>
> * <span data-ttu-id="e1551-112">Instructor と Student を更新する</span><span class="sxs-lookup"><span data-stu-id="e1551-112">Update Instructor and Student</span></span>
> * <span data-ttu-id="e1551-113">Person をモデルに追加する</span><span class="sxs-lookup"><span data-stu-id="e1551-113">Add Person to the Model</span></span>
> * <span data-ttu-id="e1551-114">移行の作成と更新</span><span class="sxs-lookup"><span data-stu-id="e1551-114">Create and Update Migrations</span></span>
> * <span data-ttu-id="e1551-115">実装をテストする</span><span class="sxs-lookup"><span data-stu-id="e1551-115">Test the implementation</span></span>
> * <span data-ttu-id="e1551-116">Azure に配置する</span><span class="sxs-lookup"><span data-stu-id="e1551-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1551-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e1551-117">Prerequisites</span></span>

* [<span data-ttu-id="e1551-118">コンカレンシーの処理</span><span class="sxs-lookup"><span data-stu-id="e1551-118">Handling Concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a><span data-ttu-id="e1551-119">継承をデータベースにマップする</span><span class="sxs-lookup"><span data-stu-id="e1551-119">Map inheritance to database</span></span>

<span data-ttu-id="e1551-120">`School` データモデルの `Instructor` クラスと `Student` クラスには、同一のいくつかのプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="e1551-120">The `Instructor` and `Student` classes in the `School` data model have several properties that are identical:</span></span>

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="e1551-122">`Instructor` エンティティと `Student` エンティティで共有されるプロパティの冗長なコードを削除すると仮定します。</span><span class="sxs-lookup"><span data-stu-id="e1551-122">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="e1551-123">または、インストラクターと学生のどちらから名前を取得したかに関係なく、名前をフォーマットできるサービスを記述するとします。</span><span class="sxs-lookup"><span data-stu-id="e1551-123">Or you want to write a service that can format names without caring whether the name came from an instructor or a student.</span></span> <span data-ttu-id="e1551-124">次の図に示すように、共有プロパティだけを含む `Person` 基本クラスを作成し、その基本クラスから `Instructor` と `Student` のエンティティを継承させることができます。</span><span class="sxs-lookup"><span data-stu-id="e1551-124">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="e1551-126">データベースでこの継承構造を表すことができるいくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="e1551-126">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="e1551-127">1つのテーブルに学生とインストラクターの両方に関する情報を含む `Person` テーブルを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="e1551-127">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="e1551-128">一部の列は、インストラクター (`HireDate`) にのみ適用されます。学生のみに (`EnrollmentDate`)、一部の列 (`LastName`、`FirstName`) にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="e1551-128">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="e1551-129">通常、各行が表す型を示す*識別子*列があります。</span><span class="sxs-lookup"><span data-stu-id="e1551-129">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="e1551-130">たとえば、識別子列にインストラクターを示す "Instructor" と受講者を示す "Student" がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="e1551-130">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![Hierarchy_example あたりのテーブル数](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="e1551-132">1つのデータベーステーブルからエンティティの継承構造を生成するこのパターンは、*階層単位*(TPH) の継承と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="e1551-132">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="e1551-133">代わりに、継承構造と同じように見えるデータベースを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="e1551-133">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="e1551-134">たとえば、`Person` テーブルには name フィールドだけを指定し、`Instructor` テーブルと `Student` テーブルには日付フィールドを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="e1551-134">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Table-per-type_inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="e1551-136">各エンティティクラスのデータベーステーブルを作成するこのパターンは、 *table per type* (TPT) 継承と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="e1551-136">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="e1551-137">他のオプションとして、個々のテーブルにすべての非抽象型をマップすることもできます。</span><span class="sxs-lookup"><span data-stu-id="e1551-137">Yet another option is to map all non-abstract types to individual tables.</span></span> <span data-ttu-id="e1551-138">継承されたプロパティを含むクラスのすべてのプロパティは、対応するテーブルの列にマップされます。</span><span class="sxs-lookup"><span data-stu-id="e1551-138">All properties of a class, including inherited properties, map to columns of the corresponding table.</span></span> <span data-ttu-id="e1551-139">このパターンは、Table-per-Concrete Class (TPC) 継承と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="e1551-139">This pattern is called Table-per-Concrete Class (TPC) inheritance.</span></span> <span data-ttu-id="e1551-140">前に示したように、`Person`、`Student`、および `Instructor` クラスに対して TPC の継承を実装した場合、以前と比べて、`Student` テーブルと `Instructor` テーブルは、継承を実装した後に違いがないように見えます。</span><span class="sxs-lookup"><span data-stu-id="e1551-140">If you implemented TPC inheritance for the `Person`, `Student`, and `Instructor` classes as shown earlier, the `Student` and `Instructor` tables would look no different after implementing inheritance than they did before.</span></span>

<span data-ttu-id="e1551-141">通常、TPC と TPH の継承パターンでは、TPT 継承パターンよりも Entity Framework でのパフォーマンスが向上します。これは、TPT パターンが複雑な結合クエリにつながる可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="e1551-141">TPC and TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span>

<span data-ttu-id="e1551-142">このチュートリアルでは、TPH 継承の実装方法を示します。</span><span class="sxs-lookup"><span data-stu-id="e1551-142">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="e1551-143">TPH は Entity Framework の既定の継承パターンなので、`Person` クラスを作成し、`Person`から派生するように `Instructor` および `Student` クラスを変更し、新しいクラスを `DbContext`に追加して、移行を作成するだけです。</span><span class="sxs-lookup"><span data-stu-id="e1551-143">TPH is the default inheritance pattern in the Entity Framework, so all you have to do is create a `Person` class, change the `Instructor` and `Student` classes to derive from `Person`, add the new class to the `DbContext`, and create a migration.</span></span> <span data-ttu-id="e1551-144">(他の継承パターンを実装する方法の詳細については、MSDN Entity Framework ドキュメントの「[テーブルごとのテーブル (TPT) の継承のマッピング](https://msdn.microsoft.com/data/jj591617#2.5)と、[具象クラス (TPC) の継承の](https://msdn.microsoft.com/data/jj591617#2.6)マッピング)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e1551-144">(For information about how to implement the other inheritance patterns, see [Mapping the Table-Per-Type (TPT) Inheritance](https://msdn.microsoft.com/data/jj591617#2.5) and [Mapping the Table-Per-Concrete Class (TPC) Inheritance](https://msdn.microsoft.com/data/jj591617#2.6) in the MSDN Entity Framework documentation.)</span></span>

## <a name="create-the-person-class"></a><span data-ttu-id="e1551-145">Person クラスの作成</span><span class="sxs-lookup"><span data-stu-id="e1551-145">Create the Person class</span></span>

<span data-ttu-id="e1551-146">[*モデル*] フォルダーで*Person.cs*を作成し、テンプレートコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e1551-146">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a><span data-ttu-id="e1551-147">Instructor と Student を更新する</span><span class="sxs-lookup"><span data-stu-id="e1551-147">Update Instructor and Student</span></span>

<span data-ttu-id="e1551-148">次に、 *Instructor.cs*と*Student.cs*を更新して、 *Person.sc*から値を継承します。</span><span class="sxs-lookup"><span data-stu-id="e1551-148">Now update the *Instructor.cs* and *Student.cs* to inherit values from the *Person.sc*.</span></span>

<span data-ttu-id="e1551-149">*Instructor.cs*で、`Person` クラスから `Instructor` クラスを派生させ、key フィールドと name フィールドを削除します。</span><span class="sxs-lookup"><span data-stu-id="e1551-149">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="e1551-150">コードは次の例のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="e1551-150">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="e1551-151">*Student.cs*に同様の変更を加えます。</span><span class="sxs-lookup"><span data-stu-id="e1551-151">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="e1551-152">`Student` クラスは次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="e1551-152">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a><span data-ttu-id="e1551-153">Person をモデルに追加する</span><span class="sxs-lookup"><span data-stu-id="e1551-153">Add Person to the Model</span></span>

<span data-ttu-id="e1551-154">*SchoolContext.cs*で、`Person` エンティティ型の `DbSet` プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="e1551-154">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="e1551-155">Table-per-Hierarchy 継承を構成するために Entity Framework に必要なのことはこれですべてです。</span><span class="sxs-lookup"><span data-stu-id="e1551-155">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="e1551-156">ご覧のように、データベースが更新されると、`Student` テーブルと `Instructor` テーブルの代わりに `Person` テーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="e1551-156">As you'll see, when the database is updated, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="create-and-update-migrations"></a><span data-ttu-id="e1551-157">移行の作成と更新</span><span class="sxs-lookup"><span data-stu-id="e1551-157">Create and Update Migrations</span></span>

<span data-ttu-id="e1551-158">パッケージマネージャーコンソール (PMC) で、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="e1551-158">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="e1551-159">PMC で `Update-Database` コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="e1551-159">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="e1551-160">この時点では、移行によって処理方法がわからない既存のデータがあるため、このコマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="e1551-160">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="e1551-161">次のようなエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e1551-161">You get an error message like the following one:</span></span>

> <span data-ttu-id="e1551-162">*オブジェクト ' dbo ' を削除できませんでした。インストラクターは、外部キー制約によって参照されています。*</span><span class="sxs-lookup"><span data-stu-id="e1551-162">*Could not drop object 'dbo.Instructor' because it is referenced by a FOREIGN KEY constraint.*</span></span>

<span data-ttu-id="e1551-163">移行を開いて *\&lt; timestamp&gt;\_Inheritance.cs*を開き、`Up` メソッドを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e1551-163">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="e1551-164">このコードは、次のデータベースの更新タスクを処理します。</span><span class="sxs-lookup"><span data-stu-id="e1551-164">This code takes care of the following database update tasks:</span></span>

- <span data-ttu-id="e1551-165">外部キー制約と Student テーブルをポイントするインデックスを削除します。</span><span class="sxs-lookup"><span data-stu-id="e1551-165">Removes foreign key constraints and indexes that point to the Student table.</span></span>
- <span data-ttu-id="e1551-166">Instructor テーブルの名前の Person に変更し、Student データを格納するために必要な変更を加えます。</span><span class="sxs-lookup"><span data-stu-id="e1551-166">Renames the Instructor table as Person and makes changes needed for it to store Student data:</span></span>

    - <span data-ttu-id="e1551-167">受講者の null 許容 EnrollmentDate を追加します。</span><span class="sxs-lookup"><span data-stu-id="e1551-167">Adds nullable EnrollmentDate for students.</span></span>
    - <span data-ttu-id="e1551-168">行が、受講者かインストラクターかを示すために識別子列を追加します。</span><span class="sxs-lookup"><span data-stu-id="e1551-168">Adds Discriminator column to indicate whether a row is for a student or an instructor.</span></span>
    - <span data-ttu-id="e1551-169">受講者行には雇用日がないので HireDate を nul 許容にします。</span><span class="sxs-lookup"><span data-stu-id="e1551-169">Makes HireDate nullable since student rows won't have hire dates.</span></span>
    - <span data-ttu-id="e1551-170">受講者をポイントする外部キーの更新に使用する一時的なフィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="e1551-170">Adds a temporary field that will be used to update foreign keys that point to students.</span></span> <span data-ttu-id="e1551-171">学生を Person テーブルにコピーすると、新しい主キー値が取得されます。</span><span class="sxs-lookup"><span data-stu-id="e1551-171">When you copy students into the Person table they'll get new primary key values.</span></span>
- <span data-ttu-id="e1551-172">Student テーブルから Person テーブルにデータをコピーします。</span><span class="sxs-lookup"><span data-stu-id="e1551-172">Copies data from the Student table into the Person table.</span></span> <span data-ttu-id="e1551-173">これにより、受講者に新しい主キー値が割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="e1551-173">This causes students to get assigned new primary key values.</span></span>
- <span data-ttu-id="e1551-174">受講者をポイントする外部キー値を修正します。</span><span class="sxs-lookup"><span data-stu-id="e1551-174">Fixes foreign key values that point to students.</span></span>
- <span data-ttu-id="e1551-175">今は Person テーブルをポイントしている外部キー制約とインデックスを再作成します</span><span class="sxs-lookup"><span data-stu-id="e1551-175">Re-creates foreign key constraints and indexes, now pointing them to the Person table.</span></span>

<span data-ttu-id="e1551-176">(主キーの型として整数の代わりに GUID を使用した場合は、受講者の主キー値を変更する必要はなく、これらの手順のいくつかを省略できます)。</span><span class="sxs-lookup"><span data-stu-id="e1551-176">(If you had used GUID instead of integer as the primary key type, the student primary key values wouldn't have to change, and several of these steps could have been omitted.)</span></span>

<span data-ttu-id="e1551-177">`update-database` コマンドをもう一度実行します。</span><span class="sxs-lookup"><span data-stu-id="e1551-177">Run the `update-database` command again.</span></span>

<span data-ttu-id="e1551-178">(実稼働システムでは、以前のバージョンのデータベースに戻るために使用する必要があった場合に備えて、ダウンメソッドに対して、対応する変更を行います。</span><span class="sxs-lookup"><span data-stu-id="e1551-178">(In a production system you would make corresponding changes to the Down method in case you ever had to use that to go back to the previous database version.</span></span> <span data-ttu-id="e1551-179">このチュートリアルでは、Down メソッドは使用しません)。</span><span class="sxs-lookup"><span data-stu-id="e1551-179">For this tutorial you won't be using the Down method.)</span></span>

> [!NOTE]
> <span data-ttu-id="e1551-180">データを移行してスキーマを変更するときに、他のエラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e1551-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="e1551-181">解決できない移行エラーが発生した場合は、 *web.config ファイルの*接続文字列を変更するか、データベースを削除することで、チュートリアルを続行できます。</span><span class="sxs-lookup"><span data-stu-id="e1551-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or by deleting the database.</span></span> <span data-ttu-id="e1551-182">最も簡単な方法*は、web.config ファイル内*のデータベースの名前を変更することです。</span><span class="sxs-lookup"><span data-stu-id="e1551-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="e1551-183">たとえば、次の例に示すように、データベース名を ContosoUniversity2 に変更します。</span><span class="sxs-lookup"><span data-stu-id="e1551-183">For example, change the database name to ContosoUniversity2 as shown in the following example:</span></span>
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> <span data-ttu-id="e1551-184">新しいデータベースでは、移行するデータは存在せず、`update-database` のコマンドはエラーなしで完了する可能性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="e1551-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="e1551-185">データベースを削除する方法については、「 [Visual Studio 2012 からデータベースを削除する方法](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e1551-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="e1551-186">このチュートリアルを続行するためにこの方法を使用する場合は、このチュートリアルの最後にあるデプロイ手順をスキップするか、新しいサイトとデータベースに配置してください。</span><span class="sxs-lookup"><span data-stu-id="e1551-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial or deploy to a new site and database.</span></span> <span data-ttu-id="e1551-187">既に展開している同じサイトに更新プログラムを展開した場合、自動的に移行を実行すると、EF によって同じエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="e1551-187">If you deploy an update to the same site you've been deploying to already, EF will get the same error there when it runs migrations automatically.</span></span> <span data-ttu-id="e1551-188">移行エラーのトラブルシューティングを行う場合は、Entity Framework フォーラムまたは StackOverflow.com のいずれかのリソースを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="e1551-188">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="test-the-implementation"></a><span data-ttu-id="e1551-189">実装をテストする</span><span class="sxs-lookup"><span data-stu-id="e1551-189">Test the implementation</span></span>

<span data-ttu-id="e1551-190">サイトを実行し、さまざまなページを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="e1551-190">Run the site and try various pages.</span></span> <span data-ttu-id="e1551-191">すべてが前と同じように動作します。</span><span class="sxs-lookup"><span data-stu-id="e1551-191">Everything works the same as it did before.</span></span>

<span data-ttu-id="e1551-192">**サーバーエクスプローラーで、** **[Data Connections\SchoolContext]** 、 **[Tables]** の順に展開し、 **Student**テーブルと**教師**テーブルが**Person**テーブルに置き換えられていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e1551-192">In **Server Explorer,** expand **Data Connections\SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="e1551-193">**Person**テーブルを展開すると、 **Student**テーブルと**教師**テーブルに使用されていたすべての列が含まれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="e1551-193">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

<span data-ttu-id="e1551-194">Person テーブルを右クリックし、 **[テーブル データの表示]** をクリックして識別子列を表示します。</span><span class="sxs-lookup"><span data-stu-id="e1551-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

<span data-ttu-id="e1551-195">次の図は、新しい School データベースの構造を示しています。</span><span class="sxs-lookup"><span data-stu-id="e1551-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="e1551-197">Azure に配置する</span><span class="sxs-lookup"><span data-stu-id="e1551-197">Deploy to Azure</span></span>

<span data-ttu-id="e1551-198">このセクションでは、このチュートリアルシリーズの[パート3、並べ替え、フィルター処理、およびページング](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)に関するページの「 **Azure へのアプリのデプロイ**」セクションを完了している必要があります。</span><span class="sxs-lookup"><span data-stu-id="e1551-198">This section requires you to have completed the optional **Deploying the app to Azure** section in [Part 3, Sorting, Filtering, and Paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) of this tutorial series.</span></span> <span data-ttu-id="e1551-199">ローカルプロジェクトでデータベースを削除することによって解決した移行エラーが発生した場合は、この手順をスキップします。または、新しいサイトとデータベースを作成し、新しい環境にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="e1551-199">If you had migrations errors that you resolved by deleting the database in your local project, skip this step; or create a new site and database, and deploy to the new environment.</span></span>

1. <span data-ttu-id="e1551-200">Visual Studio の**ソリューション エクスプローラー**で、プロジェクトを右クリックし、コンテキスト メニューの **[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e1551-200">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>

2. <span data-ttu-id="e1551-201">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e1551-201">Click **Publish**.</span></span>

    <span data-ttu-id="e1551-202">Web アプリが既定のブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="e1551-202">The Web app opens in your default browser.</span></span>

3. <span data-ttu-id="e1551-203">アプリケーションをテストして、動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e1551-203">Test the application to verify it's working.</span></span>

    <span data-ttu-id="e1551-204">データベースにアクセスするページを初めて実行する場合、Entity Framework は、現在のデータモデルを使用してデータベースを最新の状態にするために必要なすべての移行 `Up` 方法を実行します。</span><span class="sxs-lookup"><span data-stu-id="e1551-204">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="e1551-205">コードを取得する</span><span class="sxs-lookup"><span data-stu-id="e1551-205">Get the code</span></span>

[<span data-ttu-id="e1551-206">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="e1551-206">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="e1551-207">その他の技術情報</span><span class="sxs-lookup"><span data-stu-id="e1551-207">Additional resources</span></span>

<span data-ttu-id="e1551-208">その他の Entity Framework リソースへのリンクについては、 [ASP.NET Data Access の推奨リソース](../../../../whitepapers/aspnet-data-access-content-map.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e1551-208">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="e1551-209">このとその他の継承構造の詳細については、MSDN の「 [TPT 継承パターン](https://msdn.microsoft.com/data/jj618293)と[TPH 継承パターン](https://msdn.microsoft.com/data/jj618292)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e1551-209">For more information about this and other inheritance structures, see [TPT Inheritance Pattern](https://msdn.microsoft.com/data/jj618293) and [TPH Inheritance Pattern](https://msdn.microsoft.com/data/jj618292) on MSDN.</span></span> <span data-ttu-id="e1551-210">次のチュートリアルでは、比較的高度なさまざまな Entity Framework のシナリオを処理する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="e1551-210">In the next tutorial you'll see how to handle a variety of relatively advanced Entity Framework scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1551-211">次のステップ:</span><span class="sxs-lookup"><span data-stu-id="e1551-211">Next steps</span></span>

<span data-ttu-id="e1551-212">このチュートリアルでは、次の作業を行います。</span><span class="sxs-lookup"><span data-stu-id="e1551-212">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1551-213">継承をデータベースにマップする方法について学習しました</span><span class="sxs-lookup"><span data-stu-id="e1551-213">Learned to map inheritance to database</span></span>
> * <span data-ttu-id="e1551-214">Person クラスを作成した</span><span class="sxs-lookup"><span data-stu-id="e1551-214">Created the Person class</span></span>
> * <span data-ttu-id="e1551-215">Instructor と Student を更新した</span><span class="sxs-lookup"><span data-stu-id="e1551-215">Updated Instructor and Student</span></span>
> * <span data-ttu-id="e1551-216">モデルにユーザーを追加しました</span><span class="sxs-lookup"><span data-stu-id="e1551-216">Added Person to the Model</span></span>
> * <span data-ttu-id="e1551-217">移行の作成と更新</span><span class="sxs-lookup"><span data-stu-id="e1551-217">Created and Update Migrations</span></span>
> * <span data-ttu-id="e1551-218">実装をテストした</span><span class="sxs-lookup"><span data-stu-id="e1551-218">Tested the implementation</span></span>
> * <span data-ttu-id="e1551-219">Azure にデプロイ済み</span><span class="sxs-lookup"><span data-stu-id="e1551-219">Deployed to Azure</span></span>

<span data-ttu-id="e1551-220">次の記事に進み、Entity Framework Code First を使用する ASP.NET web アプリケーションの開発の基本について理解しておくと役立つトピックについて説明します。</span><span class="sxs-lookup"><span data-stu-id="e1551-220">Advance to the next article to learn about topics that are useful to be aware of when you go beyond the basics of developing ASP.NET web applications that use Entity Framework Code First.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e1551-221">高度な Entity Framework シナリオ</span><span class="sxs-lookup"><span data-stu-id="e1551-221">Advanced Entity Framework Scenarios</span></span>](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)

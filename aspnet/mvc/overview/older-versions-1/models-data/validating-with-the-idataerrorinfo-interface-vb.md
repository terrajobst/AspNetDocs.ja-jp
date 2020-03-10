---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
title: IDataErrorInfo インターフェイスを使用した検証 (VB) |Microsoft Docs
author: StephenWalther
description: Stephen Walther は、モデルクラスに IDataErrorInfo インターフェイスを実装することによって、カスタム検証エラーメッセージを表示する方法を示しています。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3a8a9d9f-82dd-4959-b7c6-960e9ce95df1
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 8ff3adc5db8114dcca2c66d937e1706f0bac0d30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436300"
---
# <a name="validating-with-the-idataerrorinfo-interface-vb"></a><span data-ttu-id="e66af-103">IDataErrorInfo インターフェイスの検証 (VB)</span><span class="sxs-lookup"><span data-stu-id="e66af-103">Validating with the IDataErrorInfo Interface (VB)</span></span>

<span data-ttu-id="e66af-104">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="e66af-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="e66af-105">Stephen Walther は、モデルクラスに IDataErrorInfo インターフェイスを実装することによって、カスタム検証エラーメッセージを表示する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="e66af-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>

<span data-ttu-id="e66af-106">このチュートリアルの目的は、ASP.NET MVC アプリケーションで検証を実行する方法の1つについて説明することです。</span><span class="sxs-lookup"><span data-stu-id="e66af-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="e66af-107">必要なフォームフィールドの値を指定せずに、他のユーザーが HTML フォームを送信できないようにする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e66af-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="e66af-108">このチュートリアルでは、IErrorDataInfo インターフェイスを使用して検証を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e66af-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="e66af-109">前提条件</span><span class="sxs-lookup"><span data-stu-id="e66af-109">Assumptions</span></span>

<span data-ttu-id="e66af-110">このチュートリアルでは、MoviesDB データベースとムービーデータベーステーブルを使用します。</span><span class="sxs-lookup"><span data-stu-id="e66af-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="e66af-111">このテーブルには、次の列があります。</span><span class="sxs-lookup"><span data-stu-id="e66af-111">This table has the following columns:</span></span>

<a id="0.6_table01"></a>

| <span data-ttu-id="e66af-112">**列名**</span><span class="sxs-lookup"><span data-stu-id="e66af-112">**Column Name**</span></span> | <span data-ttu-id="e66af-113">**[データ型]**</span><span class="sxs-lookup"><span data-stu-id="e66af-113">**Data Type**</span></span> | <span data-ttu-id="e66af-114">**[NULL を許容]**</span><span class="sxs-lookup"><span data-stu-id="e66af-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e66af-115">Id</span><span class="sxs-lookup"><span data-stu-id="e66af-115">Id</span></span> | <span data-ttu-id="e66af-116">int</span><span class="sxs-lookup"><span data-stu-id="e66af-116">Int</span></span> | <span data-ttu-id="e66af-117">False</span><span class="sxs-lookup"><span data-stu-id="e66af-117">False</span></span> |
| <span data-ttu-id="e66af-118">タイトル</span><span class="sxs-lookup"><span data-stu-id="e66af-118">Title</span></span> | <span data-ttu-id="e66af-119">Nvarchar (100)</span><span class="sxs-lookup"><span data-stu-id="e66af-119">Nvarchar(100)</span></span> | <span data-ttu-id="e66af-120">False</span><span class="sxs-lookup"><span data-stu-id="e66af-120">False</span></span> |
| <span data-ttu-id="e66af-121">ディレクター</span><span class="sxs-lookup"><span data-stu-id="e66af-121">Director</span></span> | <span data-ttu-id="e66af-122">Nvarchar (100)</span><span class="sxs-lookup"><span data-stu-id="e66af-122">Nvarchar(100)</span></span> | <span data-ttu-id="e66af-123">False</span><span class="sxs-lookup"><span data-stu-id="e66af-123">False</span></span> |
| <span data-ttu-id="e66af-124">DateReleased</span><span class="sxs-lookup"><span data-stu-id="e66af-124">DateReleased</span></span> | <span data-ttu-id="e66af-125">DateTime</span><span class="sxs-lookup"><span data-stu-id="e66af-125">DateTime</span></span> | <span data-ttu-id="e66af-126">False</span><span class="sxs-lookup"><span data-stu-id="e66af-126">False</span></span> |

<span data-ttu-id="e66af-127">このチュートリアルでは、Microsoft Entity Framework を使用して、データベースモデルクラスを生成します。</span><span class="sxs-lookup"><span data-stu-id="e66af-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="e66af-128">Entity Framework によって生成されたムービークラスは、図1に表示されます。</span><span class="sxs-lookup"><span data-stu-id="e66af-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>

<span data-ttu-id="e66af-129">[Movie エンティティの ![](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e66af-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span></span>

<span data-ttu-id="e66af-130">**図 01**: Movie エンティティ ([クリックすると、フルサイズの画像が表示](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png)されます)</span><span class="sxs-lookup"><span data-stu-id="e66af-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png))</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e66af-131">Entity Framework を使用してデータベースモデルクラスを生成する方法の詳細については、Entity Framework を使用したモデルクラスの作成に関するチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="e66af-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>

## <a name="the-controller-class"></a><span data-ttu-id="e66af-132">コントローラークラス</span><span class="sxs-lookup"><span data-stu-id="e66af-132">The Controller Class</span></span>

<span data-ttu-id="e66af-133">Home コントローラーを使用して映画を一覧表示し、新しいムービーを作成します。</span><span class="sxs-lookup"><span data-stu-id="e66af-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="e66af-134">このクラスのコードは、リスト1に含まれています。</span><span class="sxs-lookup"><span data-stu-id="e66af-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="e66af-135">**リスト 1-Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="e66af-135">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample1.vb)]

<span data-ttu-id="e66af-136">リスト1の Home controller クラスには、2つの Create () アクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e66af-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="e66af-137">最初のアクションでは、新しいムービーを作成するための HTML フォームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e66af-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="e66af-138">2番目の Create () アクションでは、データベースへの新しいムービーの実際の挿入を実行します。</span><span class="sxs-lookup"><span data-stu-id="e66af-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="e66af-139">2番目の Create () アクションは、最初の Create () アクションによって表示されるフォームがサーバーに送信されるときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="e66af-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="e66af-140">2番目の Create () アクションには、次のコード行が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e66af-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample2.vb)]

<span data-ttu-id="e66af-141">検証エラーが発生した場合、IsValid プロパティは false を返します。</span><span class="sxs-lookup"><span data-stu-id="e66af-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="e66af-142">その場合、ムービーを作成するための HTML フォームを含む [作成] ビューが再表示されます。</span><span class="sxs-lookup"><span data-stu-id="e66af-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="e66af-143">部分クラスの作成</span><span class="sxs-lookup"><span data-stu-id="e66af-143">Creating a Partial Class</span></span>

<span data-ttu-id="e66af-144">Movie クラスは、Entity Framework によって生成されます。</span><span class="sxs-lookup"><span data-stu-id="e66af-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="e66af-145">[ソリューションエクスプローラー] ウィンドウで MoviesDBModel ファイルを展開し、コードエディターで MoviesDBModel ファイルを開くと、Movie クラスのコードが表示されます (図2を参照)。</span><span class="sxs-lookup"><span data-stu-id="e66af-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.vb file in the Code Editor (see Figure 2).</span></span>

<span data-ttu-id="e66af-146">[Movie エンティティのコードの ![](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e66af-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span></span>

<span data-ttu-id="e66af-147">**図 02**: ムービーエンティティのコード ([クリックしてフルサイズの画像を表示](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="e66af-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))</span></span>

<span data-ttu-id="e66af-148">Movie クラスは、部分クラスです。</span><span class="sxs-lookup"><span data-stu-id="e66af-148">The Movie class is a partial class.</span></span> <span data-ttu-id="e66af-149">これは、同じ名前を持つ別の部分クラスを追加して、Movie クラスの機能を拡張できることを意味します。</span><span class="sxs-lookup"><span data-stu-id="e66af-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="e66af-150">ここでは、新しい部分クラスに検証ロジックを追加します。</span><span class="sxs-lookup"><span data-stu-id="e66af-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="e66af-151">リスト2のクラスを [モデル] フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="e66af-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="e66af-152">**リスト 2-モデルの表示 (vb)**</span><span class="sxs-lookup"><span data-stu-id="e66af-152">**Listing 2 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample3.vb)]

<span data-ttu-id="e66af-153">リスト2のクラスには、*部分*修飾子が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e66af-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="e66af-154">このクラスに追加したメソッドまたはプロパティは、Entity Framework によって生成される Movie クラスの一部になります。</span><span class="sxs-lookup"><span data-stu-id="e66af-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="e66af-155">OnChanging および OnChanged Partial メソッドの追加</span><span class="sxs-lookup"><span data-stu-id="e66af-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="e66af-156">Entity Framework がエンティティクラスを生成すると、Entity Framework は部分メソッドをクラスに自動的に追加します。</span><span class="sxs-lookup"><span data-stu-id="e66af-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="e66af-157">Entity Framework によって、クラスの各プロパティに対応する OnChanging メソッドと OnChanged 部分メソッドが生成されます。</span><span class="sxs-lookup"><span data-stu-id="e66af-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="e66af-158">Movie クラスの場合、Entity Framework は次のメソッドを作成します。</span><span class="sxs-lookup"><span data-stu-id="e66af-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="e66af-159">OnIdChanging</span><span class="sxs-lookup"><span data-stu-id="e66af-159">OnIdChanging</span></span>
- <span data-ttu-id="e66af-160">OnIdChanged</span><span class="sxs-lookup"><span data-stu-id="e66af-160">OnIdChanged</span></span>
- <span data-ttu-id="e66af-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="e66af-161">OnTitleChanging</span></span>
- <span data-ttu-id="e66af-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="e66af-162">OnTitleChanged</span></span>
- <span data-ttu-id="e66af-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="e66af-163">OnDirectorChanging</span></span>
- <span data-ttu-id="e66af-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="e66af-164">OnDirectorChanged</span></span>
- <span data-ttu-id="e66af-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="e66af-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="e66af-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="e66af-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="e66af-167">OnChanging メソッドは、対応するプロパティが変更される直前に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="e66af-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="e66af-168">OnChanged メソッドは、プロパティが変更された直後に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="e66af-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="e66af-169">これらの部分メソッドを利用して、ムービークラスに検証ロジックを追加できます。</span><span class="sxs-lookup"><span data-stu-id="e66af-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="e66af-170">リスト3の [ムービーの更新] クラスでは、Title プロパティと Director プロパティに空でない値が割り当てられていることが確認されます。</span><span class="sxs-lookup"><span data-stu-id="e66af-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e66af-171">部分メソッドは、実装する必要がないクラスで定義されたメソッドです。</span><span class="sxs-lookup"><span data-stu-id="e66af-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="e66af-172">部分メソッドを実装しない場合、コンパイラはメソッドのシグネチャとメソッドのすべての呼び出しを削除するため、部分メソッドに関連付けられた実行時のコストが発生しません。</span><span class="sxs-lookup"><span data-stu-id="e66af-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="e66af-173">Visual Studio Code エディターで、部分メソッドを追加するには、キーワード*partial*を入力し、その後にスペースを入力して、実装するパーシャルの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="e66af-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>

<span data-ttu-id="e66af-174">**リスト 3-modelmo? vb**</span><span class="sxs-lookup"><span data-stu-id="e66af-174">**Listing 3 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample4.vb)]

<span data-ttu-id="e66af-175">たとえば、Title プロパティに空の文字列を割り当てようとすると、エラーメッセージが \_のエラーという名前のディクショナリに割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="e66af-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="e66af-176">この時点で、Title プロパティに空の文字列を割り当てても、エラーがプライベート \_のエラーフィールドに追加された場合は、何も起こりません。</span><span class="sxs-lookup"><span data-stu-id="e66af-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="e66af-177">これらの検証エラーを ASP.NET MVC フレームワークに公開するには、IDataErrorInfo インターフェイスを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e66af-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="e66af-178">IDataErrorInfo インターフェイスの実装</span><span class="sxs-lookup"><span data-stu-id="e66af-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="e66af-179">IDataErrorInfo インターフェイスは、最初のバージョン以降、.NET framework に含まれています。</span><span class="sxs-lookup"><span data-stu-id="e66af-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="e66af-180">このインターフェイスは、非常に単純なインターフェイスです。</span><span class="sxs-lookup"><span data-stu-id="e66af-180">This interface is a very simple interface:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample5.vb)]

<span data-ttu-id="e66af-181">クラスが IDataErrorInfo インターフェイスを実装している場合、ASP.NET MVC フレームワークは、クラスのインスタンスを作成するときにこのインターフェイスを使用します。</span><span class="sxs-lookup"><span data-stu-id="e66af-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="e66af-182">たとえば、Home controller Create () アクションは、Movie クラスのインスタンスを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="e66af-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample6.vb)]

<span data-ttu-id="e66af-183">ASP.NET MVC フレームワークは、モデルバインダー (DefaultModelBinder) を使用して Create () アクションに渡されるムービーのインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="e66af-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="e66af-184">モデルバインダーは、ムービーオブジェクトのインスタンスに HTML フォームフィールドをバインドすることによって、ムービーオブジェクトのインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="e66af-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="e66af-185">DefaultModelBinder は、クラスが IDataErrorInfo インターフェイスを実装しているかどうかを検出します。</span><span class="sxs-lookup"><span data-stu-id="e66af-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="e66af-186">クラスがこのインターフェイスを実装する場合、モデルバインダーは IDataErrorInfo を呼び出します。このインデクサーはクラスの各プロパティに対して呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="e66af-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="e66af-187">インデクサーからエラーメッセージが返された場合、モデルバインダーは、このエラーメッセージをモデル状態に自動的に追加します。</span><span class="sxs-lookup"><span data-stu-id="e66af-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="e66af-188">DefaultModelBinder は、IDataErrorInfo プロパティも確認します。</span><span class="sxs-lookup"><span data-stu-id="e66af-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="e66af-189">このプロパティは、クラスに関連付けられているプロパティ以外の検証エラーを表すことを目的としています。</span><span class="sxs-lookup"><span data-stu-id="e66af-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="e66af-190">たとえば、Movie クラスの複数のプロパティの値に依存する検証規則を適用することができます。</span><span class="sxs-lookup"><span data-stu-id="e66af-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="e66af-191">その場合は、エラープロパティから検証エラーを返します。</span><span class="sxs-lookup"><span data-stu-id="e66af-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="e66af-192">リスト4の更新されたムービークラスは、IDataErrorInfo インターフェイスを実装しています。</span><span class="sxs-lookup"><span data-stu-id="e66af-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="e66af-193">**リスト 4-モデル (IDataErrorInfo を実装)**</span><span class="sxs-lookup"><span data-stu-id="e66af-193">**Listing 4 - Models\Movie.vb (implements IDataErrorInfo)**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample7.vb)]

<span data-ttu-id="e66af-194">リスト4では、インデクサープロパティは、インデクサーに渡されたプロパティ名に対応するキーが含まれているかどうかを確認するために、\_errors コレクションを確認します。</span><span class="sxs-lookup"><span data-stu-id="e66af-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="e66af-195">プロパティに検証エラーが関連付けられていない場合は、空の文字列が返されます。</span><span class="sxs-lookup"><span data-stu-id="e66af-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="e66af-196">変更した Movie クラスを使用するために、Home コントローラーを変更する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="e66af-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="e66af-197">図3に表示されるページは、タイトルまたはディレクターフォームフィールドに値が入力されていない場合に何が起こるかを示しています。</span><span class="sxs-lookup"><span data-stu-id="e66af-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>

<span data-ttu-id="e66af-198">[アクションメソッドを自動的に作成 ![](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="e66af-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span></span>

<span data-ttu-id="e66af-199">**図 03**: 欠損値のあるフォーム ([クリックすると、フルサイズの画像が表示](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="e66af-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png))</span></span>

<span data-ttu-id="e66af-200">DateReleased 値が自動的に検証されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e66af-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="e66af-201">DateReleased プロパティは NULL 値を受け付けないため、DefaultModelBinder は、値がない場合にこのプロパティの検証エラーを自動的に生成します。</span><span class="sxs-lookup"><span data-stu-id="e66af-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="e66af-202">DateReleased プロパティのエラーメッセージを変更する場合は、カスタムモデルバインダーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e66af-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="e66af-203">まとめ</span><span class="sxs-lookup"><span data-stu-id="e66af-203">Summary</span></span>

<span data-ttu-id="e66af-204">このチュートリアルでは、IDataErrorInfo インターフェイスを使用して検証エラーメッセージを生成する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="e66af-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="e66af-205">まず、Entity Framework によって生成される部分的なムービークラスの機能を拡張する部分的なムービークラスを作成しました。</span><span class="sxs-lookup"><span data-stu-id="e66af-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="e66af-206">次に、Movie class OnTitleChanging () および OnDirectorChanging () 部分メソッドに検証ロジックを追加しました。</span><span class="sxs-lookup"><span data-stu-id="e66af-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="e66af-207">最後に、これらの検証メッセージを ASP.NET MVC フレームワークに公開するために、IDataErrorInfo インターフェイスを実装しています。</span><span class="sxs-lookup"><span data-stu-id="e66af-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e66af-208">[前へ](performing-simple-validation-vb.md)
> [次へ](validating-with-a-service-layer-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e66af-208">[Previous](performing-simple-validation-vb.md)
[Next](validating-with-a-service-layer-vb.md)</span></span>

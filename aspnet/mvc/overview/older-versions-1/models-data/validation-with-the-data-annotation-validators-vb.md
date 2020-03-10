---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: データ注釈検証コントロールを使用した検証 (VB) |Microsoft Docs
author: microsoft
description: データ注釈モデルバインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行します。 さまざまな種類の検証コントロールの使用方法について説明します。
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 00150575baabc659f7dd0c07349cde52105f6c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435940"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a><span data-ttu-id="8c474-104">データ検証注釈コントロールの検証 (VB)</span><span class="sxs-lookup"><span data-stu-id="8c474-104">Validation with the Data Annotation Validators (VB)</span></span>

<span data-ttu-id="8c474-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8c474-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="8c474-106">データ注釈モデルバインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行します。</span><span class="sxs-lookup"><span data-stu-id="8c474-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="8c474-107">さまざまな種類の検証コントロール属性を使用して、Microsoft Entity Framework でそれらを操作する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8c474-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="8c474-108">このチュートリアルでは、データ注釈検証コントロールを使用して、ASP.NET MVC アプリケーションで検証を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8c474-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="8c474-109">データ注釈検証コントロールを使用する利点は、必須または StringLength 属性などの1つ以上の属性をクラスプロパティに追加するだけで検証を実行できることです。</span><span class="sxs-lookup"><span data-stu-id="8c474-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="8c474-110">データ注釈検証コントロールを使用するには、データ注釈モデルバインダーをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c474-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="8c474-111">データ注釈モデルバインダーのサンプルは、CodePlex web サイトからダウンロードできます。これを行うには、[ここ](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c474-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="8c474-112">データ注釈モデルバインダーは Microsoft ASP.NET MVC フレームワークの正式な部分ではないことを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="8c474-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="8c474-113">データ注釈モデルバインダーは Microsoft ASP.NET MVC チームによって作成されましたが、Microsoft では、このチュートリアルで説明されているデータ注釈モデルバインダーの公式製品サポートを提供していません。</span><span class="sxs-lookup"><span data-stu-id="8c474-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="8c474-114">データ注釈モデルバインダーの使用</span><span class="sxs-lookup"><span data-stu-id="8c474-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="8c474-115">ASP.NET MVC アプリケーションでデータ注釈モデルバインダーを使用するには、最初に、System.componentmodel アセンブリおよびアセンブリへの参照を追加する必要がありますので、この方法は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="8c474-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="8c474-116">メニューオプションプロジェクトの **[参照の追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8c474-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="8c474-117">次に、 **[参照]** タブをクリックし、データ注釈モデルバインダーサンプルをダウンロード (および解凍) した場所を参照します (**図 1**を参照)。</span><span class="sxs-lookup"><span data-stu-id="8c474-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

<span data-ttu-id="8c474-118">**図 1**: データ注釈モデルバインダーへの参照の追加 ([クリックすると、フルサイズの画像が表示](validation-with-the-data-annotation-validators-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="8c474-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span></span>

<span data-ttu-id="8c474-119">System.componentmodel アセンブリとアセンブリの両方を選択し、**OK** ボタンをクリックします。 をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c474-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="8c474-120">.NET Framework Service Pack 1 に含まれている System.componentmodel アセンブリをデータ注釈モデルバインダーと共に使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="8c474-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="8c474-121">データ注釈モデルバインダーサンプルのダウンロードに含まれているバージョンの System.componentmodel アセンブリを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c474-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="8c474-122">最後に、DataAnnotations モデルバインダーを global.asax ファイルに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c474-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="8c474-123">Application\_Start () イベントハンドラーに次のコード行を追加して、アプリケーション\_Start () メソッドが次のようになるようにします。</span><span class="sxs-lookup"><span data-stu-id="8c474-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

<span data-ttu-id="8c474-124">このコード行では、ASP.NET MVC アプリケーション全体の既定のモデルバインダーとして Data注釈を登録します。</span><span class="sxs-lookup"><span data-stu-id="8c474-124">This line of code registers the DataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="8c474-125">データ注釈検証コントロール属性の使用</span><span class="sxs-lookup"><span data-stu-id="8c474-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="8c474-126">データ注釈モデルバインダーを使用する場合は、検証を実行するために検証属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="8c474-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="8c474-127">System.componentmodel 名前空間には、次のバリデーター属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8c474-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="8c474-128">範囲–プロパティの値が、指定された値の範囲に収まるかどうかを検証できます。</span><span class="sxs-lookup"><span data-stu-id="8c474-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="8c474-129">RegularExpression –プロパティの値が指定した正規表現パターンと一致するかどうかを検証できます。</span><span class="sxs-lookup"><span data-stu-id="8c474-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="8c474-130">必須–プロパティを必要に応じてマークできます。</span><span class="sxs-lookup"><span data-stu-id="8c474-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="8c474-131">StringLength –文字列プロパティの最大長を指定できます。</span><span class="sxs-lookup"><span data-stu-id="8c474-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="8c474-132">検証: すべての検証コントロール属性の基本クラス。</span><span class="sxs-lookup"><span data-stu-id="8c474-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8c474-133">標準の検証コントロールで検証のニーズが満たされない場合、基本検証属性から新しい検証属性を継承することによって、カスタム検証属性を作成するオプションが常にあります。</span><span class="sxs-lookup"><span data-stu-id="8c474-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="8c474-134">**リスト 1**の Product クラスは、これらの検証属性の使用方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="8c474-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="8c474-135">Name、Description、および UnitPrice プロパティは必須としてマークされています。</span><span class="sxs-lookup"><span data-stu-id="8c474-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="8c474-136">Name プロパティの文字列の長さは10文字未満である必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c474-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="8c474-137">最後に、UnitPrice プロパティは、通貨金額を表す正規表現パターンと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c474-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

<span data-ttu-id="8c474-138">**リスト 1**: modelproductproduct. vb</span><span class="sxs-lookup"><span data-stu-id="8c474-138">**Listing 1**: Models\Product.vb</span></span>

<span data-ttu-id="8c474-139">Product クラスは、1つの追加の属性 (DisplayName 属性) の使用方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="8c474-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="8c474-140">DisplayName 属性を使用すると、プロパティがエラーメッセージに表示されたときにプロパティの名前を変更できます。</span><span class="sxs-lookup"><span data-stu-id="8c474-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="8c474-141">"UnitPrice フィールドが必要です" というエラーメッセージが表示されるのではなく、"価格フィールドが必要です" というエラーメッセージを表示できます。</span><span class="sxs-lookup"><span data-stu-id="8c474-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8c474-142">バリデーターによって表示されるエラーメッセージを完全にカスタマイズする場合は、次のように、カスタムエラーメッセージを検証コントロールの ErrorMessage プロパティに割り当てることができ `<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="8c474-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="8c474-143">リスト**2**の [作成] () コントローラーアクションを使用して、**リスト 1**の Product クラスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="8c474-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="8c474-144">このコントローラーアクションは、モデルの状態にエラーが含まれている場合に、Create ビューを再表示します。</span><span class="sxs-lookup"><span data-stu-id="8c474-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

<span data-ttu-id="8c474-145">**リスト 2**: コントローラーと vb</span><span class="sxs-lookup"><span data-stu-id="8c474-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="8c474-146">最後に、**リスト 3**のビューを作成するには、作成 () アクションを右クリックし、**ビューの追加** メニューオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="8c474-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="8c474-147">Product クラスをモデルクラスとして使用して、厳密に型指定されたビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="8c474-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="8c474-148">ビューコンテンツ ドロップダウンリストから **作成** を選択します (**図 2**を参照)。</span><span class="sxs-lookup"><span data-stu-id="8c474-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

<span data-ttu-id="8c474-149">**図 2**: Create ビューの追加</span><span class="sxs-lookup"><span data-stu-id="8c474-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

<span data-ttu-id="8c474-150">**リスト 3**: Views\Product\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="8c474-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8c474-151">**[ビューの追加]** メニューオプションで生成された作成フォームから Id フィールドを削除します。</span><span class="sxs-lookup"><span data-stu-id="8c474-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="8c474-152">Id フィールドは Id 列に対応しているため、このフィールドに値を入力することをユーザーに許可しないようにします。</span><span class="sxs-lookup"><span data-stu-id="8c474-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="8c474-153">製品を作成するためのフォームを送信し、必須フィールドに値を入力しない場合、**図 3**の検証エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c474-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

<span data-ttu-id="8c474-154">**図 3**: 必要なフィールドがない</span><span class="sxs-lookup"><span data-stu-id="8c474-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="8c474-155">無効な通貨金額を入力すると、**図 4**のエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c474-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

<span data-ttu-id="8c474-156">**図 4**: 通貨金額が無効である</span><span class="sxs-lookup"><span data-stu-id="8c474-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="8c474-157">Entity Framework と共にデータ注釈検証コントロールを使用する</span><span class="sxs-lookup"><span data-stu-id="8c474-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="8c474-158">Microsoft Entity Framework を使用してデータモデルクラスを生成する場合は、クラスにバリデーター属性を直接適用することはできません。</span><span class="sxs-lookup"><span data-stu-id="8c474-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="8c474-159">Entity Framework Designer によってモデルクラスが生成されるため、モデルクラスに加えた変更は、デザイナーで次に変更を行ったときに上書きされます。</span><span class="sxs-lookup"><span data-stu-id="8c474-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="8c474-160">Entity Framework によって生成されたクラスで検証コントロールを使用する場合は、メタデータクラスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c474-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="8c474-161">検証コントロールは、実際のクラスに適用するのではなく、メタデータクラスに適用します。</span><span class="sxs-lookup"><span data-stu-id="8c474-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="8c474-162">たとえば、Entity Framework を使用して Movie クラスを作成したとします (**図 5**を参照)。</span><span class="sxs-lookup"><span data-stu-id="8c474-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="8c474-163">さらに、ムービータイトルとディレクタープロパティに必要なプロパティを設定するとします。</span><span class="sxs-lookup"><span data-stu-id="8c474-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="8c474-164">その場合は、**リスト 4**で部分クラスとメタデータクラスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="8c474-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

<span data-ttu-id="8c474-165">**図 5**: Entity Framework によって生成されたムービークラス</span><span class="sxs-lookup"><span data-stu-id="8c474-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

<span data-ttu-id="8c474-166">**リスト 4**: modelmo? vb</span><span class="sxs-lookup"><span data-stu-id="8c474-166">**Listing 4**: Models\Movie.vb</span></span>

<span data-ttu-id="8c474-167">**リスト 4**のファイルには、Movie と MovieMetaData という名前の2つのクラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8c474-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="8c474-168">Movie クラスは、部分クラスです。</span><span class="sxs-lookup"><span data-stu-id="8c474-168">The Movie class is a partial class.</span></span> <span data-ttu-id="8c474-169">これは、DataModel ファイルに格納されている Entity Framework によって生成される部分クラスに対応します。</span><span class="sxs-lookup"><span data-stu-id="8c474-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="8c474-170">現在、.NET framework では部分的なプロパティはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="8c474-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="8c474-171">したがって、DataModel ファイルで定義されている Movie クラスのプロパティにバリデーター属性を適用する方法はありません。これには、**リスト 4**のファイルで定義されている movie クラスのプロパティにバリデーター属性を適用します。</span><span class="sxs-lookup"><span data-stu-id="8c474-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="8c474-172">Movie 部分クラスは、MovieMetaData クラスをポイントする MetadataType 属性で修飾されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8c474-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="8c474-173">MovieMetaData クラスには、Movie クラスのプロパティのプロキシプロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8c474-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="8c474-174">バリデーターの属性は、MovieMetaData クラスのプロパティに適用されます。</span><span class="sxs-lookup"><span data-stu-id="8c474-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="8c474-175">Title、Director、および DateReleased の各プロパティはすべて必須プロパティとしてマークされます。</span><span class="sxs-lookup"><span data-stu-id="8c474-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="8c474-176">Director プロパティには、5文字未満の文字列を割り当てる必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c474-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="8c474-177">最後に、DisplayName 属性が DateReleased プロパティに適用され、"リリース日フィールドが必要です。" のようなエラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c474-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="8c474-178">"DateReleased" フィールドは必須です。</span><span class="sxs-lookup"><span data-stu-id="8c474-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8c474-179">MovieMetaData クラスのプロキシプロパティは、Movie クラスの対応するプロパティと同じ型を表す必要がないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8c474-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="8c474-180">たとえば、"Director" プロパティは、Movie クラスの文字列プロパティと、MovieMetaData クラスのオブジェクトプロパティです。</span><span class="sxs-lookup"><span data-stu-id="8c474-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="8c474-181">**図 6**のページは、ムービープロパティに無効な値を入力したときに返されるエラーメッセージを示しています。</span><span class="sxs-lookup"><span data-stu-id="8c474-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

<span data-ttu-id="8c474-182">**図 6**: Entity Framework での検証コントロールの使用 ([クリックしてフルサイズのイメージを表示する](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="8c474-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="8c474-183">まとめ</span><span class="sxs-lookup"><span data-stu-id="8c474-183">Summary</span></span>

<span data-ttu-id="8c474-184">このチュートリアルでは、データ注釈モデルバインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="8c474-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="8c474-185">必須の属性や StringLength 属性など、さまざまな種類の検証コントロール属性の使用方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="8c474-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="8c474-186">また、Microsoft Entity Framework の使用時にこれらの属性を使用する方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="8c474-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8c474-187">[[戻る]](validating-with-a-service-layer-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8c474-187">[Previous](validating-with-a-service-layer-vb.md)</span></span>

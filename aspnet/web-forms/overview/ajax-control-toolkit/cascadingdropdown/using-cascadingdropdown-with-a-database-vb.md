---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
title: データベースでの CascadingDropDown の使用 (VB) |Microsoft Docs
author: wenz
description: AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって anoth に関連付けられた値が読み込まれるようにします。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 97a3d33c-c856-43f3-8acb-f1ccbc48221a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 4482aa18c4446ec8f5f160c423008398ea2e1d0d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430654"
---
# <a name="using-cascadingdropdown-with-a-database-vb"></a><span data-ttu-id="f49c7-103">データベースで CascadingDropDown を使用する (VB)</span><span class="sxs-lookup"><span data-stu-id="f49c7-103">Using CascadingDropDown with a Database (VB)</span></span>

<span data-ttu-id="f49c7-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="f49c7-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f49c7-105">[コードのダウンロード](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f49c7-105">[Download Code](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1VB.pdf)</span></span>

> <span data-ttu-id="f49c7-106">AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="f49c7-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="f49c7-107">これを機能させるには、特別な web サービスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f49c7-107">In order for this to work, a special web service must be created.</span></span>

## <a name="overview"></a><span data-ttu-id="f49c7-108">概要</span><span class="sxs-lookup"><span data-stu-id="f49c7-108">Overview</span></span>

<span data-ttu-id="f49c7-109">AJAX コントロールツールキットの CascadingDropDown コントロールは、dropdownlist コントロールを拡張して、1つの DropDownList の変更によって別の DropDownList に関連付けられた値が読み込まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="f49c7-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="f49c7-110">(たとえば、1つのリストに米国の州の一覧が表示され、その州の主要都市が次の一覧に入力されます)。これを機能させるには、特別な web サービスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f49c7-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="f49c7-111">手順</span><span class="sxs-lookup"><span data-stu-id="f49c7-111">Steps</span></span>

<span data-ttu-id="f49c7-112">まず、データソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="f49c7-112">First of all, a data source is required.</span></span> <span data-ttu-id="f49c7-113">このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。</span><span class="sxs-lookup"><span data-stu-id="f49c7-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="f49c7-114">このデータベースは、Visual Studio のインストール (express edition を含む) の省略可能な部分であり、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="f49c7-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="f49c7-115">AdventureWorks データベースは SQL Server 2005 サンプルおよびサンプルデータベース ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)) に含まれています。</span><span class="sxs-lookup"><span data-stu-id="f49c7-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="f49c7-116">データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) を使用して、`AdventureWorks.mdf` データベースファイルをアタッチすることです。</span><span class="sxs-lookup"><span data-stu-id="f49c7-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="f49c7-117">このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。</span><span class="sxs-lookup"><span data-stu-id="f49c7-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="f49c7-118">セットアップが異なる場合は、データベースの接続情報を調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f49c7-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="f49c7-119">ASP.NET AJAX と Control Toolkit の機能をアクティブ化するには、ページの任意の場所に `ScriptManager` コントロールを配置する必要があります (&lt;`form`&gt; 要素内)。</span><span class="sxs-lookup"><span data-stu-id="f49c7-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample1.aspx)]

<span data-ttu-id="f49c7-120">次の手順では、2つの DropDownList コントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="f49c7-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="f49c7-121">このサンプルでは、AdventureWorks の仕入先と連絡先の情報を使用します。そのため、利用可能なベンダーの一覧と、利用可能な連絡先のリストを1つ作成します。</span><span class="sxs-lookup"><span data-stu-id="f49c7-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample2.aspx)]

<span data-ttu-id="f49c7-122">次に、2つの CascadingDropDown extender をページに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f49c7-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="f49c7-123">1つ目の (ベンダ) リストを入力し、もう1つは2番目 (連絡先) の一覧に入力します。</span><span class="sxs-lookup"><span data-stu-id="f49c7-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="f49c7-124">次の属性を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f49c7-124">The following attributes must be set:</span></span>

- <span data-ttu-id="f49c7-125">`ServicePath`: リストエントリを提供する web サービスの URL</span><span class="sxs-lookup"><span data-stu-id="f49c7-125">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="f49c7-126">`ServiceMethod`: リストエントリを配信する Web メソッド</span><span class="sxs-lookup"><span data-stu-id="f49c7-126">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="f49c7-127">`TargetControlID`: ドロップダウンリストの ID</span><span class="sxs-lookup"><span data-stu-id="f49c7-127">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="f49c7-128">`Category`: 呼び出されたときに web メソッドに送信されるカテゴリ情報</span><span class="sxs-lookup"><span data-stu-id="f49c7-128">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="f49c7-129">`PromptText`: サーバーからリストデータを非同期的に読み込むときに表示されるテキスト</span><span class="sxs-lookup"><span data-stu-id="f49c7-129">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>
- <span data-ttu-id="f49c7-130">`ParentControlID`: (省略可能) 現在のリストの読み込みをトリガーする親ドロップダウンリスト</span><span class="sxs-lookup"><span data-stu-id="f49c7-130">`ParentControlID`: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="f49c7-131">使用するプログラミング言語によっては、問題の web サービスの名前が変わりますが、他のすべての属性値は同じです。</span><span class="sxs-lookup"><span data-stu-id="f49c7-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="f49c7-132">最初のドロップダウンリストの CascadingDropDown 要素は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="f49c7-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample3.aspx)]

<span data-ttu-id="f49c7-133">2番目のリストの制御エクステンダーは、`ParentControlID` 属性を設定する必要があります。これにより、ベンダリスト内のエントリを選択すると、連絡先リストに関連する要素の読み込みがトリガーされるようになります。</span><span class="sxs-lookup"><span data-stu-id="f49c7-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample4.aspx)]

<span data-ttu-id="f49c7-134">実際の作業は、次のように設定された web サービスで実行されます。</span><span class="sxs-lookup"><span data-stu-id="f49c7-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="f49c7-135">`[ScriptService]` 属性が使用されていることに注意してください。それ以外の場合、ASP.NET AJAX では、クライアント側のスクリプトコードから web メソッドにアクセスするための JavaScript プロキシを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="f49c7-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample5.aspx)]

<span data-ttu-id="f49c7-136">CascadingDropDown によって呼び出される web メソッドのシグネチャは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="f49c7-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample6.vb)]

<span data-ttu-id="f49c7-137">したがって、戻り値は、Control Toolkit によって定義される `CascadingDropDownNameValue` 型の配列である必要があります。</span><span class="sxs-lookup"><span data-stu-id="f49c7-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="f49c7-138">`GetVendors()` メソッドは非常に簡単に実装できます。コードは AdventureWorks データベースに接続し、最初の25個のベンダーにクエリを実行します。</span><span class="sxs-lookup"><span data-stu-id="f49c7-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="f49c7-139">`CascadingDropDownNameValue` コンストラクターの最初のパラメーターは、リストエントリのキャプション、2番目のパラメーターの値 (HTML の &lt;`option`&gt; 要素の値属性) です。</span><span class="sxs-lookup"><span data-stu-id="f49c7-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="f49c7-140">次にコードを示します。</span><span class="sxs-lookup"><span data-stu-id="f49c7-140">Here is the code:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample7.vb)]

<span data-ttu-id="f49c7-141">仕入先に関連付けられている連絡先を取得する (メソッド名: `GetContactsForVendor()`) のは少し複雑です。</span><span class="sxs-lookup"><span data-stu-id="f49c7-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="f49c7-142">まず、最初のドロップダウンリストで選択されているベンダーを特定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f49c7-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="f49c7-143">Control Toolkit は、そのタスクのヘルパーメソッドを定義します。 `ParseKnownCategoryValuesString()` メソッドは、ドロップダウンデータを含む `StringDictionary` 要素を返します。</span><span class="sxs-lookup"><span data-stu-id="f49c7-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample8.vb)]

<span data-ttu-id="f49c7-144">セキュリティ上の理由から、まずこのデータを検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f49c7-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="f49c7-145">(最初の CascadingDropDown 要素の `Category` プロパティが `"Vendor"`) に設定されているため、ベンダエントリがある場合は、選択したベンダの ID を取得できます。</span><span class="sxs-lookup"><span data-stu-id="f49c7-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample9.vb)]

<span data-ttu-id="f49c7-146">メソッドの残りの部分は、非常に単純です。</span><span class="sxs-lookup"><span data-stu-id="f49c7-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="f49c7-147">ベンダーの ID は、その仕入先に関連付けられているすべての連絡先を取得する SQL クエリのパラメーターとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="f49c7-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="f49c7-148">この場合も、メソッドは `CascadingDropDownNameValue`型の配列を返します。</span><span class="sxs-lookup"><span data-stu-id="f49c7-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample10.vb)]

<span data-ttu-id="f49c7-149">ASP.NET ページを読み込み、しばらくすると、仕入先リストに25個のエントリが格納されます。</span><span class="sxs-lookup"><span data-stu-id="f49c7-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="f49c7-150">1つのエントリを選択し、2番目のドロップダウンリストにデータが格納されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f49c7-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>

<span data-ttu-id="f49c7-151">[最初のリストが自動的に入力される ![](using-cascadingdropdown-with-a-database-vb/_static/image2.png)](using-cascadingdropdown-with-a-database-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f49c7-151">[![The first list is filled automatically](using-cascadingdropdown-with-a-database-vb/_static/image2.png)](using-cascadingdropdown-with-a-database-vb/_static/image1.png)</span></span>

<span data-ttu-id="f49c7-152">最初の一覧が自動的に入力されます ([クリックすると、フルサイズの画像が表示](using-cascadingdropdown-with-a-database-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="f49c7-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-vb/_static/image3.png))</span></span>

<span data-ttu-id="f49c7-153">[![2 番目のリストは、最初のリストの選択に従って塗りつぶされます。](using-cascadingdropdown-with-a-database-vb/_static/image5.png)](using-cascadingdropdown-with-a-database-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f49c7-153">[![The second list is filled according to the selection in the first list](using-cascadingdropdown-with-a-database-vb/_static/image5.png)](using-cascadingdropdown-with-a-database-vb/_static/image4.png)</span></span>

<span data-ttu-id="f49c7-154">2番目のリストは、最初のリストの選択に従って塗りつぶされます ([クリックすると、フルサイズの画像が表示](using-cascadingdropdown-with-a-database-vb/_static/image6.png)されます)。</span><span class="sxs-lookup"><span data-stu-id="f49c7-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f49c7-155">[前へ](filling-a-list-using-cascadingdropdown-vb.md)
> [次へ](presetting-list-entries-with-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f49c7-155">[Previous](filling-a-list-using-cascadingdropdown-vb.md)
[Next](presetting-list-entries-with-cascadingdropdown-vb.md)</span></span>

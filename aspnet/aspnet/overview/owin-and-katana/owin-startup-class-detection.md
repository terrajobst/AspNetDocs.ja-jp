---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWIN Startup クラスの検出 |Microsoft Docs
author: Praburaj
description: このチュートリアルでは、読み込まれる OWIN startup クラスを構成する方法について説明します。 OWIN の詳細については、「Project Katana の概要」を参照してください。 このチュートリアルは...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500182"
---
# <a name="owin-startup-class-detection"></a><span data-ttu-id="a68e3-105">OWIN スタートアップ クラス検出</span><span class="sxs-lookup"><span data-stu-id="a68e3-105">OWIN Startup Class Detection</span></span>

> <span data-ttu-id="a68e3-106">このチュートリアルでは、読み込まれる OWIN startup クラスを構成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-106">This tutorial shows how to configure which OWIN startup class is loaded.</span></span> <span data-ttu-id="a68e3-107">OWIN の詳細については、「 [Project Katana の概要](an-overview-of-project-katana.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a68e3-107">For more information on OWIN, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="a68e3-108">このチュートリアルは、Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )、Praburaj Thiagarajan、Howard Dierking ( [@howard\_Dierking](https://twitter.com/howard_dierking) ) によって作成されました。</span><span class="sxs-lookup"><span data-stu-id="a68e3-108">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan, and Howard Dierking ( [@howard\_dierking](https://twitter.com/howard_dierking) ).</span></span>
>
> ## <a name="prerequisites"></a><span data-ttu-id="a68e3-109">前提条件</span><span class="sxs-lookup"><span data-stu-id="a68e3-109">Prerequisites</span></span>
>
> [<span data-ttu-id="a68e3-110">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a68e3-110">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a><span data-ttu-id="a68e3-111">OWIN スタートアップ クラス検出</span><span class="sxs-lookup"><span data-stu-id="a68e3-111">OWIN Startup Class Detection</span></span>

 <span data-ttu-id="a68e3-112">すべての OWIN アプリケーションには、アプリケーションパイプラインのコンポーネントを指定する startup クラスがあります。</span><span class="sxs-lookup"><span data-stu-id="a68e3-112">Every OWIN Application has a startup class where you specify components for the application pipeline.</span></span> <span data-ttu-id="a68e3-113">スタートアップクラスは、選択したホスティングモデル (OwinHost、IIS、および IIS Express) に応じて、ランタイムに接続する方法が異なります。</span><span class="sxs-lookup"><span data-stu-id="a68e3-113">There are different ways you can connect your startup class with the runtime, depending on the hosting model you choose (OwinHost, IIS, and IIS-Express).</span></span> <span data-ttu-id="a68e3-114">このチュートリアルで示されている startup クラスは、すべてのホストアプリケーションで使用できます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-114">The startup class shown in this tutorial can be used in every hosting application.</span></span> <span data-ttu-id="a68e3-115">スタートアップクラスは、次のいずれかの方法を使用してホスティングランタイムに接続します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-115">You connect the startup class with the hosting runtime using one of the these approaches:</span></span>

1. <span data-ttu-id="a68e3-116">**名前付け規則**: Katana は、アセンブリ名またはグローバル名前空間に一致する名前空間内の `Startup` という名前のクラスを検索します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-116">**Naming Convention**: Katana looks for a class named `Startup` in namespace matching the assembly name or the global namespace.</span></span>
2. <span data-ttu-id="a68e3-117">**Owinstartup 属性**: これは、ほとんどの開発者がスタートアップクラスを指定するために実行するアプローチです。</span><span class="sxs-lookup"><span data-stu-id="a68e3-117">**OwinStartup Attribute**: This is the approach most developers will take to specify the startup class.</span></span> <span data-ttu-id="a68e3-118">次の属性は、startup クラスを `StartupDemo` 名前空間の `TestStartup` クラスに設定します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-118">The following attribute will set the startup class to the `TestStartup` class in the `StartupDemo` namespace.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   <span data-ttu-id="a68e3-119">`OwinStartup` 属性は、名前付け規則をオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="a68e3-119">The `OwinStartup` attribute overrides the naming convention.</span></span> <span data-ttu-id="a68e3-120">この属性を使用してフレンドリ名を指定することもできますが、フレンドリ名を使用するには、構成ファイルの `appSetting` 要素も使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a68e3-120">You can also specify a friendly name with this attribute, however, using a friendly name requires you to also use the `appSetting` element in the configuration file.</span></span>
3. <span data-ttu-id="a68e3-121">**構成ファイルの appSetting 要素**: `appSetting` 要素は、`OwinStartup` 属性と名前付け規則をオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="a68e3-121">**The appSetting element in the Configuration file**: The `appSetting` element overrides the `OwinStartup` attribute and naming convention.</span></span> <span data-ttu-id="a68e3-122">(それぞれ `OwinStartup` 属性を使用して) 複数のスタートアップクラスを設定し、次のようなマークアップを使用して構成ファイルに読み込むスタートアップクラスを構成することができます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-122">You can have multiple startup classes (each using an `OwinStartup` attribute) and configure which startup class will be loaded in a configuration file using markup similar to the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   <span data-ttu-id="a68e3-123">スタートアップクラスとアセンブリを明示的に指定する次のキーを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-123">The following key, which explicitly specifies the startup class and assembly can also be used:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   <span data-ttu-id="a68e3-124">構成ファイルの次の XML では、`ProductionConfiguration`のわかりやすいスタートアップクラス名を指定しています。</span><span class="sxs-lookup"><span data-stu-id="a68e3-124">The following XML in the configuration file specifies a friendly startup class name of `ProductionConfiguration`.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   <span data-ttu-id="a68e3-125">上のマークアップは、フレンドリ名を指定し、`ProductionStartup2` クラスを実行する次の `OwinStartup` 属性と共に使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a68e3-125">The above markup must be used with the following `OwinStartup` attribute which specifies a friendly name and causes the `ProductionStartup2` class to run.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. <span data-ttu-id="a68e3-126">OWIN スタートアップ検出を無効にするには、web.config ファイルで `"false"` の値を使用して `appSetting owin:AutomaticAppStartup` を追加します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-126">To disable OWIN startup discovery add the `appSetting owin:AutomaticAppStartup` with a value of `"false"` in the web.config file.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a><span data-ttu-id="a68e3-127">OWIN Startup を使用して ASP.NET Web アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="a68e3-127">Create an ASP.NET Web App using OWIN Startup</span></span>

1. <span data-ttu-id="a68e3-128">空の Asp.Net web アプリケーションを作成し、 **Startupdemo**という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-128">Create an empty Asp.Net web application and name it **StartupDemo**.</span></span> <span data-ttu-id="a68e3-129">-NuGet パッケージマネージャーを使用して `Microsoft.Owin.Host.SystemWeb` をインストールします。</span><span class="sxs-lookup"><span data-stu-id="a68e3-129">- Install `Microsoft.Owin.Host.SystemWeb` using the NuGet package manager.</span></span> <span data-ttu-id="a68e3-130">**[ツール]** メニューの **[NuGet パッケージマネージャー]** をポイントし、 **[パッケージマネージャーコンソール]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a68e3-130">From the **Tools** menu, select **NuGet Package Manager**, and then **Package Manager Console**.</span></span> <span data-ttu-id="a68e3-131">次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-131">Enter the following command:</span></span>

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. <span data-ttu-id="a68e3-132">OWIN startup クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-132">Add an OWIN startup class.</span></span> <span data-ttu-id="a68e3-133">Visual Studio 2017 でプロジェクトを右クリックし、 **[クラスの追加]** を選択します。 **[新しい項目の追加]** ダイアログボックスで、検索フィールドに「 *OWIN* 」と入力し、名前を「Startup.cs」に変更し、 **[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-133">In Visual Studio 2017 right-click the project and select **Add Class**.- In the **Add New Item** dialog box, enter *OWIN* in the search field, and change the name to Startup.cs, and then select **Add**.</span></span>

     ![](owin-startup-class-detection/_static/image1.png)

   <span data-ttu-id="a68e3-134">次に*Owin Startup クラス*を追加するときに、 **[追加]** メニューから使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="a68e3-134">The next time you want to add an *Owin Startup class*, it will be in available from the **Add** menu.</span></span>

     ![](owin-startup-class-detection/_static/image2.png)

   <span data-ttu-id="a68e3-135">または、プロジェクトを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択して、 **Owin Startup クラス**を選択します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-135">Alternatively, you can right-click the project and select **Add**, then select **New Item**, and then select the **Owin Startup class**.</span></span>

     ![](owin-startup-class-detection/_static/image3.png)

- <span data-ttu-id="a68e3-136">*Startup.cs*ファイル内の生成されたコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-136">Replace the generated code in the *Startup.cs* file with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  <span data-ttu-id="a68e3-137">`app.Use` のラムダ式は、指定されたミドルウェアコンポーネントを OWIN パイプラインに登録するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-137">The `app.Use` lambda expression is used to register the specified middleware component to the OWIN pipeline.</span></span> <span data-ttu-id="a68e3-138">この例では、受信要求に応答する前に、受信要求のログ記録を設定しています。</span><span class="sxs-lookup"><span data-stu-id="a68e3-138">In this case we are setting up logging of incoming requests before responding to the incoming request.</span></span> <span data-ttu-id="a68e3-139">`next` パラメーターは、パイプラインの次のコンポーネントに対するデリゲート ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt;[タスク](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx)&gt;) です。</span><span class="sxs-lookup"><span data-stu-id="a68e3-139">The `next` parameter is the delegate ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) to the next component in the pipeline.</span></span> <span data-ttu-id="a68e3-140">`app.Run` のラムダ式は、パイプラインを受信要求にフックし、応答機構を提供します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-140">The `app.Run` lambda expression hooks up the pipeline to incoming requests and provides the response mechanism.</span></span>
     > [!NOTE]
     > <span data-ttu-id="a68e3-141">上記のコードでは、`OwinStartup` 属性をコメントアウトし、`Startup` という名前のクラスを実行する規則に依存しています。- ***F5***キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-141">In the code above we have commented out the `OwinStartup` attribute and we're relying on the convention of running the class named `Startup` .- Press ***F5*** to run the application.</span></span> <span data-ttu-id="a68e3-142">数回更新します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-142">Hit refresh a few times.</span></span>

    <span data-ttu-id="a68e3-143">![](owin-startup-class-detection/_static/image4.png) メモ: このチュートリアルの画像に示されている数字は、表示される数字と一致しません。</span><span class="sxs-lookup"><span data-stu-id="a68e3-143">![](owin-startup-class-detection/_static/image4.png) Note: The number shown in the images in this tutorial will not match the number you see.</span></span> <span data-ttu-id="a68e3-144">ミリ秒の文字列は、ページを更新したときに新しい応答を表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-144">The millisecond string is used to show a new response when you refresh the page.</span></span>
  <span data-ttu-id="a68e3-145">**[出力]** ウィンドウにトレース情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-145">You can see the trace information in the **Output** window.</span></span>

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a><span data-ttu-id="a68e3-146">スタートアップクラスをさらに追加する</span><span class="sxs-lookup"><span data-stu-id="a68e3-146">Add More Startup Classes</span></span>

<span data-ttu-id="a68e3-147">このセクションでは、別のスタートアップクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-147">In this section we'll add another Startup class.</span></span> <span data-ttu-id="a68e3-148">複数の OWIN startup クラスをアプリケーションに追加できます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-148">You can add multiple OWIN startup class to your application.</span></span> <span data-ttu-id="a68e3-149">たとえば、開発、テスト、および運用のスタートアップクラスを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-149">For example, you might want to create startup classes for development, testing and production.</span></span>

1. <span data-ttu-id="a68e3-150">新しい OWIN Startup クラスを作成し、`ProductionStartup`という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-150">Create a new OWIN Startup class and name it `ProductionStartup`.</span></span>
2. <span data-ttu-id="a68e3-151">生成されたコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-151">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. <span data-ttu-id="a68e3-152">Ctrl F5 キーを押してアプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-152">Press Control F5 to run the app.</span></span> <span data-ttu-id="a68e3-153">`OwinStartup` 属性は、実稼働スタートアップクラスを実行することを指定します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-153">The `OwinStartup` attribute specifies the production startup class is run.</span></span>

    ![](owin-startup-class-detection/_static/image6.png)
4. <span data-ttu-id="a68e3-154">別の OWIN Startup クラスを作成し、`TestStartup`という名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-154">Create another OWIN Startup class and name it `TestStartup`.</span></span>
5. <span data-ttu-id="a68e3-155">生成されたコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-155">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   <span data-ttu-id="a68e3-156">上の `OwinStartup` 属性オーバーロードは、スタートアップクラスの*フレンドリ*名として `TestingConfiguration` を指定します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-156">The `OwinStartup` attribute overload above specifies `TestingConfiguration` as the *friendly* name of the Startup class.</span></span>
6. <span data-ttu-id="a68e3-157">*Web.config ファイルを*開き、スタートアップクラスのフレンドリ名を指定する OWIN App スタートアップキーを追加します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-157">Open the *web.config* file and add the OWIN App startup key which specifies the friendly name of the Startup class:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. <span data-ttu-id="a68e3-158">Ctrl F5 キーを押してアプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-158">Press Control F5 to run the app.</span></span> <span data-ttu-id="a68e3-159">アプリ設定要素が優先され、テスト構成が実行されます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-159">The app settings element takes precedent, and the test configuration is run.</span></span>

    ![](owin-startup-class-detection/_static/image7.png)
8. <span data-ttu-id="a68e3-160">`TestStartup` クラスの `OwinStartup` 属性から*表示名を削除します*。</span><span class="sxs-lookup"><span data-stu-id="a68e3-160">Remove the *friendly* name from the `OwinStartup` attribute in the `TestStartup` class.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. <span data-ttu-id="a68e3-161">*Web.config ファイルの*OWIN App スタートアップキーを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-161">Replace the OWIN App startup key in the *web.config* file with the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. <span data-ttu-id="a68e3-162">各クラスの `OwinStartup` 属性を、Visual Studio によって生成される既定の属性コードに戻します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-162">Revert the `OwinStartup` attribute in each class to the default attribute code generated by Visual Studio:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    <span data-ttu-id="a68e3-163">次に示す OWIN App スタートアップキーを使うと、実稼働クラスが実行されます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-163">Each of the OWIN App startup keys below will cause the production class to run.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    <span data-ttu-id="a68e3-164">最後のスタートアップキーは、スタートアップの構成方法を指定します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-164">The last startup key specifies the startup configuration method.</span></span> <span data-ttu-id="a68e3-165">次の OWIN App スタートアップキーを使用すると、構成クラスの名前を `MyConfiguration` に変更できます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-165">The following OWIN App startup key allows you to change the name of the configuration class to `MyConfiguration` .</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a><span data-ttu-id="a68e3-166">Owinhost .exe の使用</span><span class="sxs-lookup"><span data-stu-id="a68e3-166">Using Owinhost.exe</span></span>

1. <span data-ttu-id="a68e3-167">Web.config ファイルを次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-167">Replace the Web.config file with the following markup:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   <span data-ttu-id="a68e3-168">最後のキーが優先されるため、この場合は `TestStartup` が指定されます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-168">The last key wins, so in this case `TestStartup` is specified.</span></span>
2. <span data-ttu-id="a68e3-169">PMC から Owinhost をインストールします。</span><span class="sxs-lookup"><span data-stu-id="a68e3-169">Install Owinhost from the PMC:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. <span data-ttu-id="a68e3-170">アプリケーションフォルダー ( *web.config ファイルが格納されて*いるフォルダー) に移動し、コマンドプロンプトで次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-170">Navigate to the application folder (the folder containing the *Web.config* file) and in a command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   <span data-ttu-id="a68e3-171">次のコマンドウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-171">The command window will show:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. <span data-ttu-id="a68e3-172">URL `http://localhost:5000/`でブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-172">Launch a browser with the URL `http://localhost:5000/`.</span></span>

    ![](owin-startup-class-detection/_static/image8.png)

   <span data-ttu-id="a68e3-173">OwinHost は、上記のスタートアップ規約を受け入れています。</span><span class="sxs-lookup"><span data-stu-id="a68e3-173">OwinHost honored the startup conventions listed above.</span></span>
5. <span data-ttu-id="a68e3-174">コマンドウィンドウで、Enter キーを押して OwinHost を終了します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-174">In the command window, press Enter to exit OwinHost.</span></span>
6. <span data-ttu-id="a68e3-175">`ProductionStartup` クラスで、 *ProductionConfiguration*のフレンドリ名を指定する次の OwinStartup 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-175">In the `ProductionStartup` class, add the following OwinStartup attribute which specifies a friendly name of *ProductionConfiguration*.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. <span data-ttu-id="a68e3-176">コマンドプロンプトで、次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="a68e3-176">In the command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   <span data-ttu-id="a68e3-177">Production startup クラスが読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="a68e3-177">The Production startup class is loaded.</span></span>
    ![](owin-startup-class-detection/_static/image9.png)

   <span data-ttu-id="a68e3-178">このアプリケーションには複数のスタートアップクラスがあります。この例では、ランタイムまで読み込まれるスタートアップクラスを遅延しています。</span><span class="sxs-lookup"><span data-stu-id="a68e3-178">Our application has multiple startup classes, and in this example we have deferred which startup class to load until runtime.</span></span>
8. <span data-ttu-id="a68e3-179">次のランタイムスタートアップオプションをテストします。</span><span class="sxs-lookup"><span data-stu-id="a68e3-179">Test the following runtime startup options:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]

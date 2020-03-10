---
uid: mvc/overview/advanced/custom-mvc-templates
title: カスタム MVC テンプレート |Microsoft Docs
author: joeloff
description: VSIX 拡張機能としてテンプレートを作成します。
ms.author: riande
ms.date: 12/10/2012
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 0603bc24e070e223551813f66a75889a2e46fd35
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499600"
---
# <a name="custom-mvc-template"></a><span data-ttu-id="6ac52-103">カスタム MVC テンプレート</span><span class="sxs-lookup"><span data-stu-id="6ac52-103">Custom MVC Template</span></span>

<span data-ttu-id="6ac52-104">[jacques victor 氏](https://github.com/joeloff)</span><span class="sxs-lookup"><span data-stu-id="6ac52-104">by [Jacques Eloff](https://github.com/joeloff)</span></span>

<span data-ttu-id="6ac52-105">MVC 3 Tools Update for Visual Studio 2010 のリリースでは、MVC プロジェクト用に個別のプロジェクトウィザードが導入されました。</span><span class="sxs-lookup"><span data-stu-id="6ac52-105">The release of MVC 3 Tools Update for Visual Studio 2010 introduced a separate project wizard for MVC projects.</span></span> <span data-ttu-id="6ac52-106">この変更は、2つの要素によって行われました。</span><span class="sxs-lookup"><span data-stu-id="6ac52-106">The change was driven by two factors.</span></span> <span data-ttu-id="6ac52-107">まず、MVC 3 の新しいテンプレートの導入と、Visual Studio の [新しいプロジェクト] ダイアログボックスの overcrowding のための Razor リーダーなどの追加のビューエンジンのサポートを紹介します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-107">First, the introduction of new templates in MVC 3 and support for additional view engines such as Razor lead to overcrowding the New Project dialog in Visual Studio.</span></span> <span data-ttu-id="6ac52-108">2つ目は、顧客が拡張ポイントを要求していて、MVC プロジェクトの新規作成ウィザードでこれらの要求に応答する機会があることです。</span><span class="sxs-lookup"><span data-stu-id="6ac52-108">Second, customers had been asking for extensibility points and the new MVC project wizard would afford us the opportunity to respond to these requests.</span></span>

<span data-ttu-id="6ac52-109">カスタムテンプレートの追加は、困難なプロセスで、レジストリを使用して MVC プロジェクトウィザードで新しいテンプレートを表示することに依存していました。</span><span class="sxs-lookup"><span data-stu-id="6ac52-109">Adding custom templates was an arduous process that relied on using the registry to make new templates visible to the MVC project wizard.</span></span> <span data-ttu-id="6ac52-110">新しいテンプレートの作成者は、インストール時に必要なレジストリエントリが確実に作成されるように、MSI 内にラップする必要がありました。</span><span class="sxs-lookup"><span data-stu-id="6ac52-110">The author of a new template had to wrap it inside an MSI to ensure that the necessary registry entries would be created at install time.</span></span> <span data-ttu-id="6ac52-111">別の方法としては、テンプレートを含む ZIP ファイルを使用可能にし、エンドユーザーが必要なレジストリエントリを手動で作成するようにします。</span><span class="sxs-lookup"><span data-stu-id="6ac52-111">The alternative was to make a ZIP file containing the template available and have the end-user create the required registry entries by hand.</span></span>

<span data-ttu-id="6ac52-112">前述のいずれの方法も理想的ではないため、Visual Studio 2012 の MVC 4 以降でカスタム MVC テンプレートを簡単に作成、配布、およびインストールできるように、 [VSIX](https://msdn.microsoft.com/library/ff363239.aspx)拡張機能に用意されている既存のインフラストラクチャの一部を利用することにしました。</span><span class="sxs-lookup"><span data-stu-id="6ac52-112">Neither of the aforementioned approaches is ideal so we decided to leverage some of the existing infrastructure provided by [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) extensions to make it easier to author, distribute and install custom MVC templates starting with MVC 4 for Visual Studio 2012.</span></span> <span data-ttu-id="6ac52-113">この方法で提供される利点の一部を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-113">Some of the benefits provided by this approach are:</span></span>

- <span data-ttu-id="6ac52-114">VSIX 拡張機能には、さまざまな言語 (C#および Visual Basic) と複数のビューエンジン (ASPX および Razor) をサポートする複数のテンプレートを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-114">A VSIX extension can contain multiple templates that support different languages (C# and Visual Basic) and multiple view engines (ASPX and Razor).</span></span>
- <span data-ttu-id="6ac52-115">VSIX 拡張機能は、Express Sku を含む Visual Studio の複数の Sku をターゲットにすることができます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-115">A VSIX extension can target multiple SKUs of Visual Studio including Express SKUs.</span></span>
- <span data-ttu-id="6ac52-116">[Visual Studio ギャラリー](https://visualstudiogallery.msdn.microsoft.com/)では、拡張機能を広範囲の対象ユーザーに配布することができます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-116">The [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/) facilitates distributing the extension to a wide audience.</span></span>
- <span data-ttu-id="6ac52-117">VSIX 拡張機能をアップグレードすると、カスタムテンプレートの修正や更新を簡単に作成できるようになります。</span><span class="sxs-lookup"><span data-stu-id="6ac52-117">VSIX extensions can be upgraded making it easier to author corrections and updates to your custom templates.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ac52-118">前提条件</span><span class="sxs-lookup"><span data-stu-id="6ac52-118">Prerequisites</span></span>

- <span data-ttu-id="6ac52-119">ユーザーは、.vstemplate ファイルに必要なマークアップなどのプロジェクトテンプレートの作成について理解している必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ac52-119">Users need to be familiar with authoring project templates, including the required markup for vstemplate files, etc.</span></span>
- <span data-ttu-id="6ac52-120">ユーザーは、Visual Studio Professional 以降がインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ac52-120">Users will need to have Visual Studio Professional and higher installed.</span></span> <span data-ttu-id="6ac52-121">Express Sku では、VSIX プロジェクトの作成はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="6ac52-121">Express SKUs do not support creating VSIX projects.</span></span>
- <span data-ttu-id="6ac52-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668)がインストールされました。</span><span class="sxs-lookup"><span data-stu-id="6ac52-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) installed.</span></span>

## <a name="example"></a><span data-ttu-id="6ac52-123">例</span><span class="sxs-lookup"><span data-stu-id="6ac52-123">Example</span></span>

<span data-ttu-id="6ac52-124">最初の手順では、 C#または Visual Basic を使用して、新しい VSIX プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-124">The first step is to create a new VSIX project using either C# or Visual Basic.</span></span> <span data-ttu-id="6ac52-125">**[ファイル > 新しいプロジェクト]** を選択し、左側のウィンドウで **[拡張機能]** をクリックして、 **VSIX プロジェクト**を選択します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-125">Select **File > New Project**, then click **Extensibility** in the left pane and select the **VSIX Project**.</span></span>

![[新しいプロジェクト]](custom-mvc-templates/_static/image1.jpg)

<span data-ttu-id="6ac52-127">プロジェクトが作成されると、VSIX デザイナーが開きます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-127">After the project is created, the VSIX designer will be opened.</span></span>

![プロジェクトデザイナーのメタデータ](custom-mvc-templates/_static/image2.jpg)

<span data-ttu-id="6ac52-129">デザイナーを使用すると、拡張機能をインストールするときにユーザーに表示される拡張機能の全般的なプロパティを編集したり、Visual Studio でインストールされている拡張機能を参照したりすることができます (**ツール > の拡張機能と更新プログラム**)。</span><span class="sxs-lookup"><span data-stu-id="6ac52-129">The designer can be used to edit some of the general properties of the extension that will be shown to users when they install the extension or browse the installed extensions in Visual Studio (**Tools > Extensions and Updates**).</span></span> <span data-ttu-id="6ac52-130">一般情報を完了したら、[インストールの**対象] タブ**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="6ac52-130">Once you have completed the general information click on the **Install Targets tab**.</span></span>

![プロジェクトデザイナーのインストールターゲット](custom-mvc-templates/_static/image3.jpg)

<span data-ttu-id="6ac52-132">このタブは、拡張機能でサポートされている Visual Studio の Sku とバージョンを指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-132">This tab is used to specify the SKUs and versions of Visual Studio that are supported by your extension.</span></span> <span data-ttu-id="6ac52-133">**すべてのユーザーが**vsix のコンピューター単位のインストールを有効にするには、[この vsix をインストールする] チェックボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="6ac52-133">Select the checkbox for **This VSIX is installed for all users** to enable per-machine installs of the VSIX.</span></span> <span data-ttu-id="6ac52-134">右側にある **[新規]** ボタンをクリックして、Web Developer Express (vwd) などのその他の sku を追加します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-134">Click on the **New** button on the right to add additional SKUs such as Web Developer Express (VWD).</span></span>

![新しいインストール先の追加](custom-mvc-templates/_static/image4.jpg)

<span data-ttu-id="6ac52-136">すべての Professional およびそれ以降の Sku (Professional、Premium、および Ultimate) をサポートする場合は、ファミリ**Microsoft.VisualStudio.Pro**の最小 sku のみを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ac52-136">If you intend to support all the Professional and higher SKUs (Professional, Premium and Ultimate) you only need to select the minimum SKU in the family, **Microsoft.VisualStudio.Pro**.</span></span> <span data-ttu-id="6ac52-137">インストールターゲットを完了したら、すべての変更を保存してください。</span><span class="sxs-lookup"><span data-stu-id="6ac52-137">Remember to save all your changes once you have completed the Install Targets.</span></span>

![プロジェクトデザイナーのインストールターゲット](custom-mvc-templates/_static/image5.jpg)

<span data-ttu-id="6ac52-139">**[アセット]** タブは、すべてのコンテンツファイルを VSIX に追加するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-139">The **Assets** tab is used to add all your content files to the VSIX.</span></span> <span data-ttu-id="6ac52-140">MVC にはカスタムメタデータが必要であるため、 **[アセット]** タブを使用してコンテンツを追加するのではなく、VSIX マニフェストファイルの未加工の XML を編集します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-140">Since MVC requires custom metadata you will be editing the raw XML of the VSIX manifest file instead of using the **Assets** tab to add content.</span></span> <span data-ttu-id="6ac52-141">まず、VSIX プロジェクトにテンプレートの内容を追加します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-141">Start by adding the template contents to the VSIX project.</span></span> <span data-ttu-id="6ac52-142">フォルダーの構造とコンテンツは、プロジェクトのレイアウトをミラー化することが重要です。</span><span class="sxs-lookup"><span data-stu-id="6ac52-142">It is important that the structure of the folder and the contents mirror the layout of the project.</span></span> <span data-ttu-id="6ac52-143">次の例には、Basic MVC プロジェクトテンプレートから派生した4つのプロジェクトテンプレートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="6ac52-143">The example below contains four project templates that were derived from the Basic MVC project template.</span></span> <span data-ttu-id="6ac52-144">プロジェクトテンプレートを構成するすべてのファイル (ProjectTemplates フォルダーの下にあるすべてのファイル) が VSIX プロジェクトファイルの**コンテンツ**itemgroup に追加されていること、および次の例に示すように、各項目に**Copytooutputdirectory**と**IncludeInVsix**メタデータセットが含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-144">Make sure that all the files that comprise your project template (everything underneath the ProjectTemplates folder) are added to the **Content** itemgroup in the VSIX project file and that each item contains the **CopyToOutputDirectory** and **IncludeInVsix** metadata set as shown in the example below.</span></span>

<span data-ttu-id="6ac52-145">&lt;コンテンツインクルード =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="6ac52-145">&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span></span>

<span data-ttu-id="6ac52-146">&lt;CopyToOutputDirectory&gt;常に&lt;/CopyToOutputDirectory&gt;</span><span class="sxs-lookup"><span data-stu-id="6ac52-146">&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;</span></span>

<span data-ttu-id="6ac52-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span><span class="sxs-lookup"><span data-stu-id="6ac52-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span></span>

<span data-ttu-id="6ac52-148">&lt;/コンテンツ&gt;</span><span class="sxs-lookup"><span data-stu-id="6ac52-148">&lt;/Content&gt;</span></span>

<span data-ttu-id="6ac52-149">そうでない場合は、VSIX のビルド時に IDE によってテンプレートの内容がコンパイルされ、エラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6ac52-149">If not, the IDE will try to compile the contents of the template when you build the VSIX and you will likely see an error.</span></span> <span data-ttu-id="6ac52-150">多くの場合、テンプレート内のコードファイルには、プロジェクトテンプレートがインスタンス化されるときに Visual Studio によって使用される特殊な[テンプレートパラメーター](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx)が含まれているため、IDE でコンパイルすることはできません。</span><span class="sxs-lookup"><span data-stu-id="6ac52-150">Code files in templates often contain special [template parameters](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) used by Visual Studio when the project template is instantiated and therefore cannot be compiled in the IDE.</span></span>

![ソリューション エクスプローラー](custom-mvc-templates/_static/image6.jpg)

<span data-ttu-id="6ac52-152">VSIX デザイナーを閉じ、**ソリューションエクスプローラー**で**ソースの拡張子のマニフェスト**ファイルを右クリックし、 **[ファイルを開くアプリケーション]** の選択 をクリックして **[XML (テキスト) エディター]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-152">Close the VSIX designer, then right click on the **source.extension.manifest** file in **Solution Explorer** and select **Open With** and choose the **XML (Text) Editor** option.</span></span>

![ダイアログで開く](custom-mvc-templates/_static/image7.jpg)

<span data-ttu-id="6ac52-154">**&lt;Assets&gt;** 要素を作成し、VSIX に含める必要がある各ファイルに **&lt;Asset&gt;** 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-154">Create an **&lt;Assets&gt;** element and add an **&lt;Asset&gt;** element for each file that must be included in the VSIX.</span></span> <span data-ttu-id="6ac52-155">各 **&lt;Asset&gt;** 要素の**Type**属性は、 **VisualStudio**に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ac52-155">The **Type** attribute of each **&lt;Asset&gt;** element must be set to **Microsoft.VisualStudio.Mvc.Template**.</span></span> <span data-ttu-id="6ac52-156">これは、MVC プロジェクトウィザードのみで認識されるカスタムの名前空間です。</span><span class="sxs-lookup"><span data-stu-id="6ac52-156">This is a custom namespace that only the MVC project wizard understands.</span></span> <span data-ttu-id="6ac52-157">マニフェストファイルの構造とレイアウトの詳細については、VSIX 2.0 スキーマのドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="6ac52-157">Refer to the VSIX 2.0 Schema documentation for additional information on the structure and layout of the manifest file.</span></span>

<span data-ttu-id="6ac52-158">VSIX にファイルを追加するだけでは、テンプレートを MVC ウィザードに登録するのに十分ではありません。</span><span class="sxs-lookup"><span data-stu-id="6ac52-158">Just adding the files to the VSIX is not sufficient to register the templates with the MVC wizard.</span></span> <span data-ttu-id="6ac52-159">MVC ウィザードでは、テンプレート名、説明、サポートされているビューエンジン、プログラミング言語などの情報を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ac52-159">You need to provide information such as the template name, description, supported view engines and programming language to the MVC wizard.</span></span> <span data-ttu-id="6ac52-160">この情報は、各 **.vstemplate**ファイルの **&lt;Asset&gt;** 要素に関連付けられているカスタム属性に格納されます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-160">This information is carried in custom attributes associated with the **&lt;Asset&gt;** element for each **vstemplate** file.</span></span>

<span data-ttu-id="6ac52-161">&lt;Asset d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span><span class="sxs-lookup"><span data-stu-id="6ac52-161">&lt;Asset d:VsixSubPath=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span></span>

<span data-ttu-id="6ac52-162">「=&quot;VisualStudio&quot;」と入力します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-162">Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;</span></span>

<span data-ttu-id="6ac52-163">&quot;ファイル&quot;</span><span class="sxs-lookup"><span data-stu-id="6ac52-163">d:Source=&quot;File&quot;</span></span>

<span data-ttu-id="6ac52-164">Path =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span><span class="sxs-lookup"><span data-stu-id="6ac52-164">Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span></span>

<span data-ttu-id="6ac52-165">ProjectType =&quot;MVC&quot;</span><span class="sxs-lookup"><span data-stu-id="6ac52-165">ProjectType=&quot;MVC&quot;</span></span>

<span data-ttu-id="6ac52-166">言語 =&quot;C#&quot;</span><span class="sxs-lookup"><span data-stu-id="6ac52-166">Language=&quot;C#&quot;</span></span>

<span data-ttu-id="6ac52-167">ViewEngine =&quot;Aspx&quot;</span><span class="sxs-lookup"><span data-stu-id="6ac52-167">ViewEngine=&quot;Aspx&quot;</span></span>

<span data-ttu-id="6ac52-168">TemplateId =&quot;MyMvcApplication&quot;</span><span class="sxs-lookup"><span data-stu-id="6ac52-168">TemplateId=&quot;MyMvcApplication&quot;</span></span>

<span data-ttu-id="6ac52-169">Title = カスタム基本的な Web アプリケーション&quot; の&quot;</span><span class="sxs-lookup"><span data-stu-id="6ac52-169">Title=&quot;Custom Basic Web Application&quot;</span></span>

<span data-ttu-id="6ac52-170">Description = 基本的な MVC web アプリケーション (Razor) から派生したカスタムテンプレートを&quot;&quot;</span><span class="sxs-lookup"><span data-stu-id="6ac52-170">Description=&quot;A custom template derived from a Basic MVC web application (Razor)&quot;</span></span>

<span data-ttu-id="6ac52-171">バージョン =&quot;4.0&quot;/&gt;</span><span class="sxs-lookup"><span data-stu-id="6ac52-171">Version=&quot;4.0&quot;/&gt;</span></span>

<span data-ttu-id="6ac52-172">次に示すのは、存在する必要があるカスタム属性の説明です。</span><span class="sxs-lookup"><span data-stu-id="6ac52-172">Below is an explanation of the custom attributes that must be present:</span></span>

- <span data-ttu-id="6ac52-173">**ProjectType**は MVC に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ac52-173">**ProjectType** must be set to MVC.</span></span>
- <span data-ttu-id="6ac52-174">**Language**は、テンプレートでサポートされている開発言語を指定します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-174">**Language** designates the development language supported by the template.</span></span> <span data-ttu-id="6ac52-175">有効な値はC# 、または VB です。</span><span class="sxs-lookup"><span data-stu-id="6ac52-175">Valid values are either C# or VB.</span></span>
- <span data-ttu-id="6ac52-176">**Viewengine**は、テンプレートでサポートされているビューエンジン (Aspx、Razor など) を指定します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-176">**ViewEngine** designates the view engine supported by the template such as Aspx or Razor.</span></span> <span data-ttu-id="6ac52-177">このフィールドには、カスタム値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-177">You can specify a custom value for this field.</span></span>
- <span data-ttu-id="6ac52-178">**TemplateId**は、テンプレートをグループ化するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-178">**TemplateId** is used for grouping the templates.</span></span> <span data-ttu-id="6ac52-179">値が既存のテンプレート ID と一致する場合は、MVC ウィザードで以前に登録されたテンプレートより優先されます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-179">If the value matches an existing template ID it will be override templates previously registered with the MVC wizard.</span></span>
- <span data-ttu-id="6ac52-180">**[タイトル]** は、各プロジェクトテンプレートの下にある MVC ウィザードに表示される短い説明を指定します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-180">**Title** designates the short description displayed in the MVC wizard beneath each project template.</span></span>
- <span data-ttu-id="6ac52-181">**説明**テンプレートの詳細な説明を指定します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-181">**Description** designates a more verbose description of the template.</span></span>

<span data-ttu-id="6ac52-182">すべてのファイルをマニフェストに追加して保存すると、デザイナーの **[アセット]** タブにはすべてのファイルが表示されますが、 **.vstemplate**ファイルの **&lt;Asset&gt;** 要素に追加したカスタム属性は表示されません。</span><span class="sxs-lookup"><span data-stu-id="6ac52-182">After you have added all the files to the manifest and saved it, you will notice that the **Assets** tab in the designer will display all the files, but not the custom attributes you added to the **&lt;Asset&gt;** elements for the **vstemplate** files.</span></span>

![プロジェクトデザイナーのアセット](custom-mvc-templates/_static/image8.jpg)

<span data-ttu-id="6ac52-184">これで、VSIX プロジェクトをコンパイルしてインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-184">All that remains now is to compile the VSIX project and install it.</span></span>

<span data-ttu-id="6ac52-185">VSIX 拡張機能をテストするコンピューターで Visual Studio のすべてのインスタンスが閉じられていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-185">Make sure that all instances of Visual Studio are closed on the machine where you intend to test the VSIX extension.</span></span> <span data-ttu-id="6ac52-186">Visual Studio は起動時に新しい拡張機能をスキャンします。そのため、VSIX のインストール中に IDE が開いている場合は、Visual Studio を再起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6ac52-186">Visual Studio scans for new extensions during startup, so if the IDE is open while installing a VSIX you will need to restart Visual Studio.</span></span> <span data-ttu-id="6ac52-187">[エクスプローラー] で、VSIX ファイルをダブルクリックして、 **Vsix インストーラー**を起動します。次に、 **[インストール]** をクリックし、Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-187">In Explorer, double click on the VSIX file to launch the **VSIX Installer**, click **Install** and then launch Visual Studio.</span></span>

![VSIX インストーラー](custom-mvc-templates/_static/image9.jpg)

<span data-ttu-id="6ac52-189">メニューから [ **> ツール] [拡張機能と更新プログラム**] を選択して、拡張機能がインストールされたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="6ac52-189">From the menu, select **Tools > Extensions and Updates** to confirm that your extension was installed.</span></span> <span data-ttu-id="6ac52-190">拡張機能のインストール中に VSIX インストーラーによってエラーが報告された場合は、VSIX インストーラーログで詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-190">If the VSIX Installer reported any errors during the installation of the extension you can view the VSIX Installer log for more information.</span></span> <span data-ttu-id="6ac52-191">通常、ログは、拡張機能をインストールしたユーザーの **% temp%** フォルダー (たとえば、 **C:\Users\Bob\AppData\Local\Temp**) に作成されます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-191">The log is usually created in the **%temp%** folder of the user that installed the extension, for example **C:\Users\Bob\AppData\Local\Temp**.</span></span>

![拡張機能と更新プログラム](custom-mvc-templates/_static/image10.jpg)

<span data-ttu-id="6ac52-193">ウィンドウを閉じた後、MVC 4 プロジェクトを作成して、新しいテンプレートが MVC ウィザードに表示されているかどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-193">After closing the window you can create an MVC 4 project to see whether your new templates are shown in the MVC wizard.</span></span>

![新しい ASP.NET MVC 4 プロジェクト](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a><span data-ttu-id="6ac52-195">制限事項</span><span class="sxs-lookup"><span data-stu-id="6ac52-195">Limitations</span></span>

1. <span data-ttu-id="6ac52-196">MVC ウィザードでは、ローカライズされたカスタムテンプレートはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="6ac52-196">The MVC wizard does not support localized custom templates.</span></span>
2. <span data-ttu-id="6ac52-197">カスタムテンプレートの特定に失敗した場合、ウィザードはエラーを報告しません。</span><span class="sxs-lookup"><span data-stu-id="6ac52-197">The wizard will not report any errors if it fails to locate custom templates.</span></span> <span data-ttu-id="6ac52-198">必要なカスタム属性のいずれかが存在しない場合、テンプレートは単純にウィザードから除外されます。</span><span class="sxs-lookup"><span data-stu-id="6ac52-198">If any of the required custom attributes are absent, the template would simply be excluded from the Wizard.</span></span>

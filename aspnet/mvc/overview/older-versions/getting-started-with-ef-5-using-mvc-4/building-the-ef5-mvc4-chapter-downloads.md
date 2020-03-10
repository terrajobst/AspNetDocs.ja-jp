---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: EF 5 MVC 4 チュートリアルのダウンロード章をビルドするMicrosoft Docs
author: Rick-Anderson
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 10237af40e3914b65e5181f17555697e86adea4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485122"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a><span data-ttu-id="49b91-103">EF 5 MVC 4 チュートリアルのダウンロード章をビルドする</span><span class="sxs-lookup"><span data-stu-id="49b91-103">Building the Chapter Downloads for the EF 5 MVC 4 Tutorials</span></span>

<span data-ttu-id="49b91-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="49b91-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[<span data-ttu-id="49b91-105">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="49b91-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="49b91-106">Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="49b91-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="49b91-107">チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="49b91-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

## <a name="building-the-chapter-downloads"></a><span data-ttu-id="49b91-108">章ダウンロードの構築</span><span class="sxs-lookup"><span data-stu-id="49b91-108">Building the Chapter Downloads</span></span>

1. <span data-ttu-id="49b91-109">プロジェクトサンプル zip ファイルをダウンロードして解凍します。</span><span class="sxs-lookup"><span data-stu-id="49b91-109">Download and unzip the  project sample zip file.</span></span> <span data-ttu-id="49b91-110">解凍されたダウンロードパッケージには、各章の完了のための追加の zip ファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="49b91-110">In the unzipped download package, you will find additional zip files, one for the completion of each chapter.</span></span>
2. <span data-ttu-id="49b91-111">目的の zip ファイルを右クリックし、 **[プロパティ]** をクリックして、 **[ブロック解除]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="49b91-111">Right click on the desired zip file, click **Properties**, and click the **Unblock** button.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. <span data-ttu-id="49b91-112">ファイルを解凍します。</span><span class="sxs-lookup"><span data-stu-id="49b91-112">Unzip the file.</span></span>
4. <span data-ttu-id="49b91-113">*Cux .sln*ファイルをダブルクリックして、Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="49b91-113">Double-click the *CUx.sln* file to launch Visual Studio.</span></span>
5. <span data-ttu-id="49b91-114">**[ツール]** メニューの **[NuGet パッケージマネージャー]** 、 **[パッケージマネージャーコンソール]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="49b91-114">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. <span data-ttu-id="49b91-115">パッケージマネージャーコンソール (PMC) で、 **[復元]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="49b91-115">In the Package Manager Console (PMC), click **Restore**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. <span data-ttu-id="49b91-116">Visual Studio を終了します。</span><span class="sxs-lookup"><span data-stu-id="49b91-116">Exit Visual Studio.</span></span>
8. <span data-ttu-id="49b91-117">Visual Studio を再起動し、前の手順で閉じたソリューションファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="49b91-117">Restart Visual Studio, opening the solution file you closed in the step above.</span></span>
9. <span data-ttu-id="49b91-118">パッケージマネージャーコンソール (PMC) で、`Update-Database` コマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="49b91-118">In the Package Manager Console (PMC), enter the `Update-Database` command:</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > <span data-ttu-id="49b91-119">次のエラーが発生する場合:</span><span class="sxs-lookup"><span data-stu-id="49b91-119">If you get the following error:</span></span>  
    >   
    >  <span data-ttu-id="49b91-120">*"データベースの更新" という用語は、コマンドレット、関数、スクリプトファイル、または操作可能なプログラムの名前として認識されません。名前の綴りを確認するか、パスが含まれている場合は、パスが正しいことを確認してから、もう一度やり直してください。*</span><span class="sxs-lookup"><span data-stu-id="49b91-120">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*</span></span>  
    > <span data-ttu-id="49b91-121">Visual Studio を終了し、再起動します。</span><span class="sxs-lookup"><span data-stu-id="49b91-121">Exit and restart Visual Studio.</span></span>

    <span data-ttu-id="49b91-122">各移行が実行された後、seed メソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="49b91-122">Each migration will run, then the seed method will run.</span></span> <span data-ttu-id="49b91-123">これで、アプリを実行できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="49b91-123">You can now run the app.</span></span>

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> <span data-ttu-id="49b91-124">[[戻る]](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="49b91-124">[Previous](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span></span>

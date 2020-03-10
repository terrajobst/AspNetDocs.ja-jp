---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 | にアップグレードするMicrosoft Docs
author: rick-anderson
description: このドキュメントでは、手動でアップグレードする方法と、ウィザードを使用して ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードする方法について説明します。 このドキュメントは、d...
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517300"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a><span data-ttu-id="e53a4-104">ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードする</span><span class="sxs-lookup"><span data-stu-id="e53a4-104">Upgrading an ASP.NET MVC 1.0 Application to ASP.NET MVC 2</span></span>

> <span data-ttu-id="e53a4-105">このドキュメントでは、手動でアップグレードする方法と、ウィザードを使用して ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-105">This document describes both how to upgrade manually and with a wizard an ASP.NET MVC 1.0 Application to ASP.NET MVC 2.</span></span> <span data-ttu-id="e53a4-106">このドキュメントは、[ダウンロード](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)することもできます。</span><span class="sxs-lookup"><span data-stu-id="e53a4-106">This document is also available for [Download](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span></span>

## <a name="introduction"></a><span data-ttu-id="e53a4-107">はじめに</span><span class="sxs-lookup"><span data-stu-id="e53a4-107">Introduction</span></span>

<span data-ttu-id="e53a4-108">ASP.NET MVC 2 は、同じサーバーに ASP.NET MVC 1.0 とサイドバイサイドでインストールできます。</span><span class="sxs-lookup"><span data-stu-id="e53a4-108">ASP.NET MVC 2 can be installed side by side with ASP.NET MVC 1.0 on the same server.</span></span> <span data-ttu-id="e53a4-109">これにより、アプリケーション開発者は、ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードするタイミングを柔軟に選択できます。</span><span class="sxs-lookup"><span data-stu-id="e53a4-109">This gives application developers flexibility in choosing when to upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2.</span></span>

<span data-ttu-id="e53a4-110">Visual Studio 2010 には、Visual Studio 2008 でビルドされた既存の ASP.NET MVC 1.0 プロジェクトを ASP.NET MVC 2 にアップグレードするウィザードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e53a4-110">Visual Studio 2010 includes a wizard that upgrades existing ASP.NET MVC 1.0 projects built with Visual Studio 2008 to ASP.NET MVC 2.</span></span> <span data-ttu-id="e53a4-111">アップグレードウィザードを開始するには、Visual Studio 2010 で ASP.NET MVC 1.0 プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="e53a4-111">The upgrade wizard is initiated by opening an ASP.NET MVC 1.0 project in Visual Studio 2010.</span></span>

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a><span data-ttu-id="e53a4-112">Visual Studio 2008 SP1 での ASP.NET MVC 1.0 のアップグレードウィザード</span><span class="sxs-lookup"><span data-stu-id="e53a4-112">Upgrade Wizard for ASP.NET MVC 1.0 on Visual Studio 2008 SP1</span></span>

<span data-ttu-id="e53a4-113">Visual Studio 2008 SP1 で ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードするには、(サポートされていない) MvcAppConverter アプリケーションを使用します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-113">To upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2 in Visual Studio 2008 SP1, use the (unsupported) MvcAppConverter application.</span></span> <span data-ttu-id="e53a4-114">このアプリケーションは、次の URL からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="e53a4-114">You can download this application from the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a><span data-ttu-id="e53a4-115">ASP.NET MVC 1.0 プロジェクトの手動アップグレード</span><span class="sxs-lookup"><span data-stu-id="e53a4-115">Manually Upgrading an ASP.NET MVC 1.0 Project</span></span>

<span data-ttu-id="e53a4-116">既存の ASP.NET MVC 1.0 アプリケーションをバージョン2に手動でアップグレードするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-116">To manually upgrade an existing ASP.NET MVC 1.0 application to version 2, follow these steps:</span></span>

1. <span data-ttu-id="e53a4-117">既存のプロジェクトのバックアップを作成します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-117">Make a backup of the existing project.</span></span>
2. <span data-ttu-id="e53a4-118">テキストエディターで、プロジェクトファイル (.csproj または .vbproj ファイル拡張子の付いたファイル) を開き、ProjectTypeGuid 要素を検索します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-118">In a text editor, open the project file (the file with the .csproj or .vbproj file extension) and find the ProjectTypeGuid element.</span></span> <span data-ttu-id="e53a4-119">この要素の値として、GUID {603c0e0b-11db56の値を {F85E285D-A4E0-4152-9332-AB1D724D3325} に置き換えます。この値を変更します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-119">As the value of that element, replace the GUID {603c0e0b-db56-11dc-be95-000d561079b0} with {F85E285D-A4E0-4152-9332-AB1D724D3325}.</span></span> <span data-ttu-id="e53a4-120">完了すると、その要素の値は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="e53a4-120">When you are done, the value of that element should be as follows:</span></span> 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. <span data-ttu-id="e53a4-121">Web アプリケーションのルートフォルダーで、web.config ファイルを編集します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-121">In the Web application root folder, edit the Web.config file.</span></span> <span data-ttu-id="e53a4-122">System.web. Mvc, Version = 1.0.0.0 を検索し、すべてのインスタンスを System.web. Mvc, Version = 2.0.0.0 に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e53a4-122">Search for System.Web.Mvc, Version=1.0.0.0 and replace all instances with System.Web.Mvc, Version=2.0.0.0.</span></span>
4. <span data-ttu-id="e53a4-123">Views フォルダーにある web.config ファイルに対して、前の手順を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-123">Repeat the previous step for the Web.config file located in the Views folder.</span></span>
5. <span data-ttu-id="e53a4-124">Visual Studio を使用してプロジェクトを開き、**ソリューションエクスプローラー**で **[参照]** ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-124">Open the project using Visual Studio, and in **Solution Explorer**, expand the **References** node.</span></span> <span data-ttu-id="e53a4-125">(バージョン1.0 アセンブリを指す) System.web. Mvc への参照を削除します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-125">Delete the reference to System.Web.Mvc (which points to the version 1.0 assembly).</span></span> <span data-ttu-id="e53a4-126">System.web. Mvc (v 2.0.0.0) への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-126">Add a reference to System.Web.Mvc (v2.0.0.0).</span></span>
6. <span data-ttu-id="e53a4-127">次の bindingRedirect 要素を、アプリケーションルートの構成セクションにある web.config ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-127">Add the following bindingRedirect element to the Web.config file in the application root under the configuraton section:</span></span>   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. <span data-ttu-id="e53a4-128">新しい空の ASP.NET MVC 2 アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-128">Create a new empty ASP.NET MVC 2 application.</span></span> <span data-ttu-id="e53a4-129">新しいアプリケーションの Scripts フォルダーにあるファイルを、既存のアプリケーションの Scripts フォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="e53a4-129">Copy the files from the Scripts folder of the new application into the Scripts folder of the existing application.</span></span>
8. <span data-ttu-id="e53a4-130">既存の™アプリケーションの css ファイルを、サイトの .css ファイルの CSS スタイル定義で更新します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-130">Update the existing applicationâ€™s CSS file with the CSS style definitions in the Site.css file.</span></span>
9. <span data-ttu-id="e53a4-131">アプリケーションをコンパイルして実行します。</span><span class="sxs-lookup"><span data-stu-id="e53a4-131">Compile the application and run it.</span></span> <span data-ttu-id="e53a4-132">エラーが発生した場合は、「 [ASP.NET MVC 2 の新機能](https://go.microsoft.com/fwlink/?LinkID=185038)」ページの「互換性に影響する変更点」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="e53a4-132">If any errors occur, refer to the Breaking Changes section of the [What's New in ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) page.</span></span>

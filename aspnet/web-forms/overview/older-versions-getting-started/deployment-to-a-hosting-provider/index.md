---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/index
title: ASP.NET 4-Visual Studio を使用した SQL Server Compact を使用した Web 配置 |Microsoft Docs
author: rick-anderson
description: このチュートリアルシリーズでは、SQL Server Compact を使用する ASP.NET web アプリケーションを、サードパーティの h にデプロイすることにより、インターネット経由で使用できるようにする方法について説明します。
ms.author: riande
ms.date: 11/29/2011
ms.assetid: 6798c7e4-f08e-4802-9fa5-443f67d5df62
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider
msc.type: chapter
ms.openlocfilehash: bb9a47eeb4197348e85bb469b68c0055e7c696a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514696"
---
# <a name="aspnet-4---web-deployment-with-sql-server-compact-using-visual-studio"></a><span data-ttu-id="cbe8d-103">ASP.NET 4 - Visual Studio を利用した SQL Server Compact の Web 配置</span><span class="sxs-lookup"><span data-stu-id="cbe8d-103">ASP.NET 4 - Web Deployment with SQL Server Compact using Visual Studio</span></span>

> <span data-ttu-id="cbe8d-104">このチュートリアルシリーズでは、SQL Server Compact を使用する ASP.NET web アプリケーションを、サードパーティのホスティングプロバイダーにデプロイすることによって、インターネット経由で使用できるようにする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="cbe8d-104">This tutorial series shows how to make an ASP.NET web application that uses SQL Server Compact available over the internet by deploying it to a third-party hosting provider.</span></span> <span data-ttu-id="cbe8d-105">Visual Studio 2012 RC または Visual Studio 2010 が必要です。</span><span class="sxs-lookup"><span data-stu-id="cbe8d-105">Requires Visual Studio 2012 RC or Visual Studio 2010.</span></span> <span data-ttu-id="cbe8d-106">配置機能の最新情報については、または SQL Server Compact 以外の SQL Server のエディションをデプロイする方法の詳細については、「 [ASP.NET Web deployment Using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cbe8d-106">For more up-to-date information about deployment features, or for information about how to deploy SQL Server editions other than SQL Server Compact, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

- [<span data-ttu-id="cbe8d-107">Visual Studio による SQL Server Compact の Web 展開 - 概要</span><span class="sxs-lookup"><span data-stu-id="cbe8d-107">Visual Studio Web Deployment with SQL Server Compact - Introduction</span></span>](deployment-to-a-hosting-provider-introduction-1-of-12.md)
- [<span data-ttu-id="cbe8d-108">Visual Studio による SQL Server Compact の Web 展開 - SQL Server Compact データベースの展開</span><span class="sxs-lookup"><span data-stu-id="cbe8d-108">Visual Studio Web Deployment with SQL Server Compact- Deploying SQL Server Compact Databases</span></span>](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
- [<span data-ttu-id="cbe8d-109">Visual Studio による SQL Server Compact の Web 展開 - Web.Config ファイル変換</span><span class="sxs-lookup"><span data-stu-id="cbe8d-109">Visual Studio Web Deployment with SQL Server Compact - Web.Config File Transformations</span></span>](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
- [<span data-ttu-id="cbe8d-110">Visual Studio による SQL Server Compact の Web 展開 - プロジェクト プロパティの構成</span><span class="sxs-lookup"><span data-stu-id="cbe8d-110">Visual Studio Web Deployment with SQL Server Compact - Configuring Project Properties</span></span>](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
- [<span data-ttu-id="cbe8d-111">Visual Studio による SQL Server Compact の Web 展開 - テスト環境として IIS に展開する</span><span class="sxs-lookup"><span data-stu-id="cbe8d-111">Visual Studio Web Deployment with SQL Server Compact - Deploying to IIS as a Test Environment</span></span>](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
- [<span data-ttu-id="cbe8d-112">Visual Studio による SQL Server Compact の Web 展開 - フォルダー アクセス許可の設定</span><span class="sxs-lookup"><span data-stu-id="cbe8d-112">Visual Studio Web Deployment with SQL Server Compact - Setting Folder Permissions</span></span>](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
- [<span data-ttu-id="cbe8d-113">Visual Studio による SQL Server Compact の Web 展開 - 運用環境に展開する</span><span class="sxs-lookup"><span data-stu-id="cbe8d-113">Visual Studio Web Deployment with SQL Server Compact - Deploying to the Production Environment</span></span>](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
- [<span data-ttu-id="cbe8d-114">Visual Studio による SQL Server Compact の Web 展開 - コード限定更新の展開</span><span class="sxs-lookup"><span data-stu-id="cbe8d-114">Visual Studio Web Deployment with SQL Server Compact - Deploying a Code-Only Update</span></span>](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
- [<span data-ttu-id="cbe8d-115">Visual Studio による SQL Server Compact の Web 展開 - データベース更新の展開</span><span class="sxs-lookup"><span data-stu-id="cbe8d-115">Visual Studio Web Deployment with SQL Server Compact - Deploying a Database Update</span></span>](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
- [<span data-ttu-id="cbe8d-116">Visual Studio による SQL Server Compact の Web 展開 - SQL Server に移行する</span><span class="sxs-lookup"><span data-stu-id="cbe8d-116">Visual Studio Web Deployment with SQL Server Compact - Migrating to SQL Server</span></span>](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
- [<span data-ttu-id="cbe8d-117">Visual Studio による SQL Server Compact の Web 展開 - SQL Server データベース更新の展開</span><span class="sxs-lookup"><span data-stu-id="cbe8d-117">Visual Studio Web Deployment with SQL Server Compact - Deploying a SQL Server Database Update</span></span>](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
- [<span data-ttu-id="cbe8d-118">Visual Studio による SQL Server Compact の Web 展開 - トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="cbe8d-118">Visual Studio Web Deployment with SQL Server Compact - Troubleshooting</span></span>](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)

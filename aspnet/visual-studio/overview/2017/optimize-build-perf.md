---
uid: visual-studio/overview/2017/optimize-build-perf
title: ソリューションのビルド パフォーマンスを最適化する
author: AngelosP
description: ソリューションのビルド パフォーマンスを最適化する
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504976"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="45ba0-103">ソリューションのビルド パフォーマンスを最適化する</span><span class="sxs-lookup"><span data-stu-id="45ba0-103">Optimize build performance for solution</span></span>

<span data-ttu-id="45ba0-104">Visual Studio 2017 15.8 以降にはメニュー項目が含まれています:**ビルド** > **ASP.NET のコンパイル** > **ソリューションのビルドパフォーマンスを最適化**します。</span><span class="sxs-lookup"><span data-stu-id="45ba0-104">Visual Studio 2017 15.8 or later include a menu item: **Build** > **ASP.NET Compilation** > **Optimize Build Performance for Solution**.</span></span>

![新しいメニュー項目のスクリーンショット](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="45ba0-106">ASP.NET は実行時にビューをコンパイルします。つまり、ASP.NET プロジェクトには、コンパイラのコピーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="45ba0-106">ASP.NET compiles its views at runtime, which means that an ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="45ba0-107">ただし、コンパイラのコピーが Visual Studio のコピーと一致しない場合、開発者のコンピューターでは、ビルドのパフォーマンスはインクリメンタルビルドあたり1-3 秒の順序で影響を受けます。</span><span class="sxs-lookup"><span data-stu-id="45ba0-107">However on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="45ba0-108">この機能により、プロジェクトのコンパイラコピーが更新され、Visual Studio のが一致するようになります。これにより、通常はインクリメンタルビルドが高速化されます。</span><span class="sxs-lookup"><span data-stu-id="45ba0-108">This feature updates your project's copy of the compiler to match Visual Studio's, which usually speeds up incremental builds.</span></span>

<span data-ttu-id="45ba0-109">**これは、ASP.NET Framework 4.7.1 以降のプロジェクトにのみ適用されます。 ASP.NET Core には適用されません。**</span><span class="sxs-lookup"><span data-stu-id="45ba0-109">**This is applicable to ASP.NET Framework 4.7.1 or later projects only, it does not apply to ASP.NET Core.**</span></span>

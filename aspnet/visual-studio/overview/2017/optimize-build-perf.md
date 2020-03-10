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
# <a name="optimize-build-performance-for-solution"></a>ソリューションのビルド パフォーマンスを最適化する

Visual Studio 2017 15.8 以降にはメニュー項目が含まれています:**ビルド** > **ASP.NET のコンパイル** > **ソリューションのビルドパフォーマンスを最適化**します。

![新しいメニュー項目のスクリーンショット](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

ASP.NET は実行時にビューをコンパイルします。つまり、ASP.NET プロジェクトには、コンパイラのコピーが含まれています。 ただし、コンパイラのコピーが Visual Studio のコピーと一致しない場合、開発者のコンピューターでは、ビルドのパフォーマンスはインクリメンタルビルドあたり1-3 秒の順序で影響を受けます。 この機能により、プロジェクトのコンパイラコピーが更新され、Visual Studio のが一致するようになります。これにより、通常はインクリメンタルビルドが高速化されます。

**これは、ASP.NET Framework 4.7.1 以降のプロジェクトにのみ適用されます。 ASP.NET Core には適用されません。**

---
uid: visual-studio/overview/2017/optimize-build-perf
title: ソリューションのビルド パフォーマンスを最適化する
author: AngelosP
description: ソリューションのビルド パフォーマンスを最適化する
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050509"
---
# <a name="optimize-build-performance-for-solution"></a>ソリューションのビルド パフォーマンスを最適化する

Visual Studio 2017 15.8年または後で、メニュー項目を含めます。**ビルド** > **ASP.NET コンパイル** > **ソリューションのビルドのパフォーマンスを最適化**します。

![新しいメニュー項目のスクリーン ショット](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

ASP.NET、ASP.NET プロジェクトを伴って、コンパイラのコピーは、実行時にそのビューをコンパイルします。 ただし、開発者のコンピューターで、コンパイラのコピーは、Visual Studio のコピーと一致しない場合ビルド パフォーマンスに影響インクリメンタル ビルドごとに 1 ~ 3 秒の順序。 この機能は、通常、インクリメンタル ビルドが高速化、Visual Studio の一致するようにコンパイラのプロジェクトのコピーを更新します。

**これは ASP.NET Framework 4.7.1 に適用されますまたはプロジェクトが後でのみ、ASP.NET Core には適用されません。**

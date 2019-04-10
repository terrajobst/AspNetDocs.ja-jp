---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[How Do I]: Persist the State of a User Control During a Postback | Microsoft Docs'
author: rick-anderson
description: このビデオの Chris Pels では、ユーザー コントロール内の 1 つまたは複数のオブジェクトの状態を維持する方法を示します。 まず、abilit を表すユーザー コントロールを作成しています.
ms.author: riande
ms.date: 04/02/2009
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: c87bd6c5c993a1bde8f8a84f6d53b431e54541d9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59414778"
---
# <a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a><span data-ttu-id="eb93e-103">[操作方法]。ポストバック中、ユーザー コントロールの状態を保持する</span><span class="sxs-lookup"><span data-stu-id="eb93e-103">[How Do I]: Persist the State of a User Control During a Postback</span></span>

<span data-ttu-id="eb93e-104">によって[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="eb93e-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="eb93e-105">このビデオの Chris Pels では、ユーザー コントロール内の 1 つまたは複数のオブジェクトの状態を維持する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="eb93e-105">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="eb93e-106">最初に、ユーザーが検索のフィルター条件を指定するための機能を表すユーザー コントロールが作成されます。</span><span class="sxs-lookup"><span data-stu-id="eb93e-106">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="eb93e-107">さらに、フィルター情報を格納するコンパニオン フィルター クラスが作成されます。</span><span class="sxs-lookup"><span data-stu-id="eb93e-107">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="eb93e-108">いくつかのユーザー インターフェイス要素は、いくつかのメソッドとプロパティ フィルター クラスのインスタンスに現在のフィルター情報を格納すると共に、フィルター コントロールに追加されます。</span><span class="sxs-lookup"><span data-stu-id="eb93e-108">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="eb93e-109">次に、ユーザー コントロールの永続化では、RegisterRequiresControlState メソッドと保存/復元の関連するメソッドを使用して実装されます。</span><span class="sxs-lookup"><span data-stu-id="eb93e-109">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="eb93e-110">これらのメソッドは、ページのポストバック時にフィルター クラスとそのデータのインスタンスを格納します。</span><span class="sxs-lookup"><span data-stu-id="eb93e-110">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="eb93e-111">最後に、状態のコントロール実装で複数のオブジェクトを格納する方法の詳細については。</span><span class="sxs-lookup"><span data-stu-id="eb93e-111">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="eb93e-112">&#9654;ビデオ (23 分)</span><span class="sxs-lookup"><span data-stu-id="eb93e-112">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)

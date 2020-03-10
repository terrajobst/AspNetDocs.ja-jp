---
uid: web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
title: '[操作方法:]UpdatePanel の条件付き UpdateMode を使用しますか? | Microsoft Docs'
author: JoeStagner
description: ASP.NET AJAX UpdatePanel には、' Always ' または ' Conditional ' に設定できる UpdateMode プロパティが含まれています。 既定値は常にです。その場合は、UpdatePan...
ms.author: riande
ms.date: 08/01/2007
ms.assetid: 10b5bad3-4c18-464f-9454-0b3e60b7b8be
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
msc.type: video
ms.openlocfilehash: c05d4f262d56dfba858443b830d72ff0520b65d7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510124"
---
# <a name="how-do-i-use-the-conditional-updatemode-of-the-updatepanel"></a><span data-ttu-id="397ac-105">[操作方法:]UpdatePanel の条件付き UpdateMode を使用しますか?</span><span class="sxs-lookup"><span data-stu-id="397ac-105">[How Do I:] Use the Conditional UpdateMode of the UpdatePanel?</span></span>

<span data-ttu-id="397ac-106">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="397ac-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="397ac-107">ASP.NET AJAX UpdatePanel には、' Always ' または ' Conditional ' に設定できる UpdateMode プロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="397ac-107">The ASP.NET AJAX UpdatePanel includes an UpdateMode property that may be set to 'Always' or 'Conditional'.</span></span> <span data-ttu-id="397ac-108">既定値は常にです。この場合、UpdatePanel は非同期ポストバック中に常にコンテンツを更新します。</span><span class="sxs-lookup"><span data-stu-id="397ac-108">The default is Always, in which case the UpdatePanel will always update its content during an asynchronous postback.</span></span> <span data-ttu-id="397ac-109">このビデオでは、UpdateMode を条件に設定する方法について説明します。この場合、UpdatePanel は、サーバー側コードが Update メソッドを呼び出したときにのみコンテンツを更新します。</span><span class="sxs-lookup"><span data-stu-id="397ac-109">In this video we learn how we can set the UpdateMode to Conditional, in which case the UpdatePanel will only update its content when our server-side code calls its Update method.</span></span> <span data-ttu-id="397ac-110">これにより、または Visual Basic コードでC#条件付きロジックを使用して、現在の非同期ポストバック中に UpdatePanel がコンテンツを更新するかどうかを判断できます。</span><span class="sxs-lookup"><span data-stu-id="397ac-110">This allows you to use conditional logic in your C# or Visual Basic code to determine whether the UpdatePanel will update its content during the current asynchronous postback.</span></span>

[<span data-ttu-id="397ac-111">&#9654;ビデオを見る (13 分)</span><span class="sxs-lookup"><span data-stu-id="397ac-111">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-conditional-updatemode-of-the-updatepanel)

> [!div class="step-by-step"]
> <span data-ttu-id="397ac-112">[前へ](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
> [次へ](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span><span class="sxs-lookup"><span data-stu-id="397ac-112">[Previous](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
[Next](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span></span>

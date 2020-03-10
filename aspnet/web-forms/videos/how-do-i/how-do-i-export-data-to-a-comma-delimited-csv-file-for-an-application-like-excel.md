---
uid: web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
title: '[操作方法:]Excel のようなアプリケーションのコンマ区切り (CSV) ファイルにデータをエクスポートします。Microsoft Docs'
author: rick-anderson
description: このビデオでは、データベースまたは他のソースからデータを取得し、アプリケーション li で使用できるコンマ区切りファイルにエクスポートする方法を紹介しています。
ms.author: riande
ms.date: 01/22/2009
ms.assetid: c9df86ad-aec2-43d5-bb8a-413ebb666673
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
msc.type: video
ms.openlocfilehash: f27873eee345fe5347023b154de2b3833c9b6138
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458068"
---
# <a name="how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel"></a><span data-ttu-id="db783-103">[操作方法:]Excel などのアプリケーションのコンマ区切り (CSV) ファイルにデータをエクスポートする</span><span class="sxs-lookup"><span data-stu-id="db783-103">[How Do I:] Export Data to a Comma Delimited (CSV) File for an Application Like Excel</span></span>

<span data-ttu-id="db783-104">[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="db783-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="db783-105">このビデオでは、データベースまたは他のソースからデータを取得し、Excel などのアプリケーションで使用できるコンマ区切りファイルにエクスポートする方法を紹介します。</span><span class="sxs-lookup"><span data-stu-id="db783-105">In this video Chris Pels shows how to take data from a database or other source and export it to a comma delimited file that can be used in an application like Excel.</span></span> <span data-ttu-id="db783-106">まず、データのセットが DataTable オブジェクトとして作成されます。</span><span class="sxs-lookup"><span data-stu-id="db783-106">First, a set of data is created as a DataTable object.</span></span> <span data-ttu-id="db783-107">次に、現在の web ページ要求に対する応答がクリアされ、ヘッダーとコンテンツの種類が csv ファイルとして構成されます。</span><span class="sxs-lookup"><span data-stu-id="db783-107">Next, the Response for the current web page request is cleared and the header and content type are configured to be a csv file.</span></span> <span data-ttu-id="db783-108">次に、最初に csv ファイルの列ヘッダーを書き込んだ後、データ値を入力して、実際のデータを応答ストリームに追加します。</span><span class="sxs-lookup"><span data-stu-id="db783-108">Then the actual data is added to the response stream by first writing the column headers for the csv file followed by the data values.</span></span> <span data-ttu-id="db783-109">この方法は、Excel などのプログラムでローカルに操作できるように、ユーザーがデータをエクスポートする必要がある場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="db783-109">This approach can be useful when users require an export of data so it can be manipulated locally in a program like Excel.</span></span>

[<span data-ttu-id="db783-110">&#9654;ビデオを見る (19 分)</span><span class="sxs-lookup"><span data-stu-id="db783-110">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel)

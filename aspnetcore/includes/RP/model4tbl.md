---
ms.openlocfilehash: 61f96e43f558302dd96348fd309be1a84f040be0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037249"
---
<a name="codegenerator"></a> <span data-ttu-id="8fc17-101">次の表で、ASP.NET Core コード ジェネレーターのパラメーターについて詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="8fc17-101">The following table details the ASP.NET Core code generators\` parameters:</span></span>

| <span data-ttu-id="8fc17-102">パラメーター</span><span class="sxs-lookup"><span data-stu-id="8fc17-102">Parameter</span></span>               | <span data-ttu-id="8fc17-103">説明</span><span class="sxs-lookup"><span data-stu-id="8fc17-103">Description</span></span>|
| ----------------- | ------------ |
| <span data-ttu-id="8fc17-104">-m</span><span class="sxs-lookup"><span data-stu-id="8fc17-104">-m</span></span>  | <span data-ttu-id="8fc17-105">モデルの名前。</span><span class="sxs-lookup"><span data-stu-id="8fc17-105">The name of the model.</span></span> |
| <span data-ttu-id="8fc17-106">-dc</span><span class="sxs-lookup"><span data-stu-id="8fc17-106">-dc</span></span>  | <span data-ttu-id="8fc17-107">データ コンテキスト。</span><span class="sxs-lookup"><span data-stu-id="8fc17-107">The data context.</span></span> |
| <span data-ttu-id="8fc17-108">-udl</span><span class="sxs-lookup"><span data-stu-id="8fc17-108">-udl</span></span> | <span data-ttu-id="8fc17-109">既定のレイアウトを使用します。</span><span class="sxs-lookup"><span data-stu-id="8fc17-109">Use the default layout.</span></span> |
| <span data-ttu-id="8fc17-110">-outDir</span><span class="sxs-lookup"><span data-stu-id="8fc17-110">-outDir</span></span> | <span data-ttu-id="8fc17-111">ビューを作成するための相対出力フォルダー パス。</span><span class="sxs-lookup"><span data-stu-id="8fc17-111">The relative output folder path to create the views.</span></span> |
| <span data-ttu-id="8fc17-112">--referenceScriptLibraries</span><span class="sxs-lookup"><span data-stu-id="8fc17-112">--referenceScriptLibraries</span></span> | <span data-ttu-id="8fc17-113">[編集] および [作成] ページに `_ValidationScriptsPartial` を追加します。</span><span class="sxs-lookup"><span data-stu-id="8fc17-113">Adds `_ValidationScriptsPartial` to Edit and Create pages</span></span> |

<span data-ttu-id="8fc17-114">次のように、`h` スイッチを使用して、`aspnet-codegenerator razorpage` コマンドに関するヘルプを取得します。</span><span class="sxs-lookup"><span data-stu-id="8fc17-114">Use the `h` switch to get help on the `aspnet-codegenerator razorpage` command:</span></span>

```console
dotnet aspnet-codegenerator razorpage -h
```

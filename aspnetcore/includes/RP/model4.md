---
ms.openlocfilehash: 5ed24cd8a7e880a496d0c0295f7c1fb07f0e1032
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035989"
---
<span data-ttu-id="7abcd-101">次の表で、ASP.NET Core コード ジェネレーターのパラメーターについて詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="7abcd-101">The following table details the ASP.NET Core code generator parameters:</span></span>

| <span data-ttu-id="7abcd-102">パラメーター</span><span class="sxs-lookup"><span data-stu-id="7abcd-102">Parameter</span></span>               | <span data-ttu-id="7abcd-103">説明</span><span class="sxs-lookup"><span data-stu-id="7abcd-103">Description</span></span>|
| ----------------- | ------------ |
| <span data-ttu-id="7abcd-104">-m</span><span class="sxs-lookup"><span data-stu-id="7abcd-104">-m</span></span>  | <span data-ttu-id="7abcd-105">モデルの名前。</span><span class="sxs-lookup"><span data-stu-id="7abcd-105">The name of the model.</span></span> |
| <span data-ttu-id="7abcd-106">-dc</span><span class="sxs-lookup"><span data-stu-id="7abcd-106">-dc</span></span>  | <span data-ttu-id="7abcd-107">使用する `DbContext` クラス。</span><span class="sxs-lookup"><span data-stu-id="7abcd-107">The `DbContext` class to use.</span></span> |
| <span data-ttu-id="7abcd-108">-udl</span><span class="sxs-lookup"><span data-stu-id="7abcd-108">-udl</span></span> | <span data-ttu-id="7abcd-109">既定のレイアウトを使用します。</span><span class="sxs-lookup"><span data-stu-id="7abcd-109">Use the default layout.</span></span> |
| <span data-ttu-id="7abcd-110">-outDir</span><span class="sxs-lookup"><span data-stu-id="7abcd-110">-outDir</span></span> | <span data-ttu-id="7abcd-111">ビューを作成するための相対出力フォルダー パス。</span><span class="sxs-lookup"><span data-stu-id="7abcd-111">The relative output folder path to create the views.</span></span> |
| <span data-ttu-id="7abcd-112">--referenceScriptLibraries</span><span class="sxs-lookup"><span data-stu-id="7abcd-112">--referenceScriptLibraries</span></span> | <span data-ttu-id="7abcd-113">[編集] および [作成] ページに `_ValidationScriptsPartial` を追加します。</span><span class="sxs-lookup"><span data-stu-id="7abcd-113">Adds `_ValidationScriptsPartial` to Edit and Create pages</span></span> |

<span data-ttu-id="7abcd-114">次のように、`h` スイッチを使用して、`aspnet-codegenerator razorpage` コマンドに関するヘルプを取得します。</span><span class="sxs-lookup"><span data-stu-id="7abcd-114">Use the `h` switch to get help on the `aspnet-codegenerator razorpage` command:</span></span>

```console
dotnet aspnet-codegenerator razorpage -h
```

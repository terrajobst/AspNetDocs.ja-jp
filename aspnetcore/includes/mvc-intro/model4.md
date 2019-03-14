---
ms.openlocfilehash: 568fa161b27e554fd8b474670b8f9a7ec2f39f45
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047129"
---
<span data-ttu-id="824e3-101">次の表で、ASP.NET Core コード ジェネレーターのパラメーターについて詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="824e3-101">The following table details the ASP.NET Core code generator parameters:</span></span>

| <span data-ttu-id="824e3-102">パラメーター</span><span class="sxs-lookup"><span data-stu-id="824e3-102">Parameter</span></span>               | <span data-ttu-id="824e3-103">説明</span><span class="sxs-lookup"><span data-stu-id="824e3-103">Description</span></span>|
| ----------------- | ------------ |
| <span data-ttu-id="824e3-104">-m</span><span class="sxs-lookup"><span data-stu-id="824e3-104">-m</span></span>  | <span data-ttu-id="824e3-105">モデルの名前。</span><span class="sxs-lookup"><span data-stu-id="824e3-105">The name of the model.</span></span> |
| <span data-ttu-id="824e3-106">-dc</span><span class="sxs-lookup"><span data-stu-id="824e3-106">-dc</span></span>  | <span data-ttu-id="824e3-107">データ コンテキスト。</span><span class="sxs-lookup"><span data-stu-id="824e3-107">The data context.</span></span> |
| <span data-ttu-id="824e3-108">-udl</span><span class="sxs-lookup"><span data-stu-id="824e3-108">-udl</span></span> | <span data-ttu-id="824e3-109">既定のレイアウトを使用します。</span><span class="sxs-lookup"><span data-stu-id="824e3-109">Use the default layout.</span></span> |
| <span data-ttu-id="824e3-110">--relativeFolderPath</span><span class="sxs-lookup"><span data-stu-id="824e3-110">--relativeFolderPath</span></span> | <span data-ttu-id="824e3-111">ビューを作成するための相対出力フォルダー パス。</span><span class="sxs-lookup"><span data-stu-id="824e3-111">The relative output folder path to create the views.</span></span> |
| <span data-ttu-id="824e3-112">--useDefaultLayout</span><span class="sxs-lookup"><span data-stu-id="824e3-112">--useDefaultLayout</span></span> | <span data-ttu-id="824e3-113">ビューには既定のレイアウトを使用してください。</span><span class="sxs-lookup"><span data-stu-id="824e3-113">The default layout should be used for the views.</span></span> |
| <span data-ttu-id="824e3-114">--referenceScriptLibraries</span><span class="sxs-lookup"><span data-stu-id="824e3-114">--referenceScriptLibraries</span></span> | <span data-ttu-id="824e3-115">[編集] および [作成] ページに `_ValidationScriptsPartial` を追加します。</span><span class="sxs-lookup"><span data-stu-id="824e3-115">Adds `_ValidationScriptsPartial` to Edit and Create pages</span></span> |

<span data-ttu-id="824e3-116">次のように、`h` スイッチを使用して、`aspnet-codegenerator controller` コマンドに関するヘルプを取得します。</span><span class="sxs-lookup"><span data-stu-id="824e3-116">Use the `h` switch to get help on the `aspnet-codegenerator controller` command:</span></span>

```console
dotnet aspnet-codegenerator controller -h
```
---
uid: webhooks/diagnostics/debugging
title: ASP.NET Webhook のデバッグ |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook をデバッグする方法。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520600"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="ac28e-103">ASP.NET Webhook のデバッグ</span><span class="sxs-lookup"><span data-stu-id="ac28e-103">ASP.NET WebHooks debugging</span></span>  

## <a name="debugging-in-azure"></a><span data-ttu-id="ac28e-104">Azure でのデバッグ</span><span class="sxs-lookup"><span data-stu-id="ac28e-104">Debugging in Azure</span></span>

<span data-ttu-id="ac28e-105">Azure での実行中に Web アプリケーションをデバッグする方法については、 [Visual Studio を使用した Azure App Service での web アプリのトラブルシューティングに関する](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)チュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="ac28e-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="ac28e-106">ソースとシンボルを使用したデバッグ</span><span class="sxs-lookup"><span data-stu-id="ac28e-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="ac28e-107">独自のコードをデバッグするだけでなく、Microsoft ASP.NET Webhook に直接デバッグすることもできます。実際にはすべて .NET です。</span><span class="sxs-lookup"><span data-stu-id="ac28e-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="ac28e-108">これは、ローカルまたはリモートのどちらでデバッグするかに関係なく機能します。</span><span class="sxs-lookup"><span data-stu-id="ac28e-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="ac28e-109">最初に、 **[デバッグ]** 、[**オプションと設定]** の順に移動して、ソースとシンボルを検索するように Visual Studio を構成します。</span><span class="sxs-lookup"><span data-stu-id="ac28e-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="ac28e-110">次のようなオプションを設定します。</span><span class="sxs-lookup"><span data-stu-id="ac28e-110">Set the options like this:</span></span>

![オプションと設定](_static/SourceSymbols.png)

<span data-ttu-id="ac28e-112">次に、ソースとシンボルをダウンロードするためのリンクを[symbolsource.org](http://symbolsource.org)に追加します。</span><span class="sxs-lookup"><span data-stu-id="ac28e-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="ac28e-113">上のメニューの **[シンボル]** タブに移動し、次のコードをシンボルの場所として追加します。</span><span class="sxs-lookup"><span data-stu-id="ac28e-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="ac28e-114">また、キャッシュディレクトリに短い名前を使用していることを確認します。それ以外の場合は、ファイル名が長すぎて、シンボルが読み込まれない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ac28e-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="ac28e-115">サンプルパスは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="ac28e-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="ac28e-116">設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ac28e-116">The settings should look similar to this:</span></span>

![オプションシンボルファイルの場所の例](_static/SymSource.png)

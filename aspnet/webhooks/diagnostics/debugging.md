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
# <a name="aspnet-webhooks-debugging"></a>ASP.NET Webhook のデバッグ  

## <a name="debugging-in-azure"></a>Azure でのデバッグ

Azure での実行中に Web アプリケーションをデバッグする方法については、 [Visual Studio を使用した Azure App Service での web アプリのトラブルシューティングに関する](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)チュートリアルを参照してください。

## <a name="debugging-with-source-and-symbols"></a>ソースとシンボルを使用したデバッグ

独自のコードをデバッグするだけでなく、Microsoft ASP.NET Webhook に直接デバッグすることもできます。実際にはすべて .NET です。 これは、ローカルまたはリモートのどちらでデバッグするかに関係なく機能します。 最初に、 **[デバッグ]** 、[**オプションと設定]** の順に移動して、ソースとシンボルを検索するように Visual Studio を構成します。 次のようなオプションを設定します。

![オプションと設定](_static/SourceSymbols.png)

次に、ソースとシンボルをダウンロードするためのリンクを[symbolsource.org](http://symbolsource.org)に追加します。 上のメニューの **[シンボル]** タブに移動し、次のコードをシンボルの場所として追加します。

```
http://srv.symbolsource.org/pdb/Public
```

また、キャッシュディレクトリに短い名前を使用していることを確認します。それ以外の場合は、ファイル名が長すぎて、シンボルが読み込まれない可能性があります。 サンプルパスは次のとおりです。

```
C:\SymCache
```

設定は次のようになります。

![オプションシンボルファイルの場所の例](_static/SymSource.png)

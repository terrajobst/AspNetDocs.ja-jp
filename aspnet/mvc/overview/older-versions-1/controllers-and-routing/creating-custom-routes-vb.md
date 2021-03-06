---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: カスタムルートを作成する (VB) |Microsoft Docs
author: microsoft
description: ASP.NET MVC アプリケーションにカスタムルートを追加する方法について説明します。 このチュートリアルでは、global.asax ファイルの既定のルートテーブルを変更する方法について説明します。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: 22b44e9e575c9d404881a23ee735bb0c8b7109e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486694"
---
# <a name="creating-custom-routes-vb"></a>カスタム ルートを作成する (VB)

[Microsoft](https://github.com/microsoft)

> ASP.NET MVC アプリケーションにカスタムルートを追加する方法について説明します。 このチュートリアルでは、global.asax ファイルの既定のルートテーブルを変更する方法について説明します。

このチュートリアルでは、ASP.NET MVC アプリケーションにカスタムルートを追加する方法について説明します。 Global.asax ファイルの既定のルートテーブルをカスタムルートで変更する方法について説明します。

ASP.NET MVC アプリケーションでは、既定のルートテーブルは正常に機能します。 ただし、特化されたルーティングニーズがあることがわかります。 その場合は、カスタムルートを作成できます。

たとえば、ブログアプリケーションを作成する場合を考えてみましょう。 次のような受信要求を処理することができます。

/アーカイブ/月3日

ユーザーがこの要求を入力すると、12/25/2009 日付に対応するブログエントリが返されます。 この種類の要求を処理するには、カスタムルートを作成する必要があります。

リスト1の global.asax ファイルには、"ブログ" という名前の新しいカスタムルートが含まれています。このルートは、/アーカイブ/*エントリ日付*のような要求を処理します。

**リスト 1-global.asax (カスタムルートを使用)**

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

ルートテーブルに追加するルートの順序は重要です。 新しいカスタムブログルートは、既存の既定のルートの前に追加されます。 順序を逆にした場合、既定のルートは常にカスタムルートではなく呼び出されます。

カスタムブログルートは、/Archive/. で始まるすべての要求と一致します。 そのため、これは次のすべての Url と一致します。

- /アーカイブ/月3日

- /Archive/10-6-2004

- /アーカイブ/apple

カスタムルートは、受信要求を Archive という名前のコントローラーにマップし、Entry () アクションを呼び出します。 Entry () メソッドが呼び出されると、エントリ日付は entryDate という名前のパラメーターとして渡されます。

リスト2のコントローラーで、ブログカスタムルートを使用できます。

**リスティング 2-ArchiveController**

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

リスト2の Entry () メソッドでは、DateTime 型のパラメーターを受け取ることに注意してください。 MVC フレームワークは、URL のエントリ日付を DateTime 値に自動的に変換するのに十分なスマートです。 URL のエントリ日付パラメーターを DateTime に変換できない場合は、エラーが発生します (図1を参照)。

**図 1-パラメーターの変換エラー**

[[新しいプロジェクト] ダイアログボックスの ![](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)

**図 01**: パラメーターの変換時のエラー ([クリックすると、フルサイズの画像が表示](creating-custom-routes-vb/_static/image2.png)される)

## <a name="summary"></a>まとめ

このチュートリアルの目的は、カスタムルートを作成する方法を説明することでした。 ブログエントリを表す global.asax ファイルのルートテーブルにカスタムルートを追加する方法について学習しました。 ブログエントリの要求を、ArchiveController という名前のコントローラーと、Entry () という名前のコントローラーアクションにマップする方法について説明しました。

> [!div class="step-by-step"]
> [前へ](asp-net-mvc-controller-overview-vb.md)
> [次へ](creating-a-route-constraint-vb.md)

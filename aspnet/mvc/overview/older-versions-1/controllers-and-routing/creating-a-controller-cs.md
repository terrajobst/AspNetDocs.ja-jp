---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: コントローラーを作成するC#() |Microsoft Docs
author: StephenWalther
description: このチュートリアルでは、Stephen Walther は、ASP.NET MVC アプリケーションにコントローラーを追加する方法を示しています。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: 6e3d0bae7f07410637c2b06c500d94a02c821f5c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437650"
---
# <a name="creating-a-controller-c"></a>コントローラーを作成する (C#)

[Stephen Walther](https://github.com/StephenWalther)

> このチュートリアルでは、Stephen Walther は、ASP.NET MVC アプリケーションにコントローラーを追加する方法を示しています。

このチュートリアルの目的は、新しい ASP.NET MVC コントローラーを作成する方法を説明することです。 コントローラーを作成する方法については、Visual Studio の [コントローラーの追加] メニューオプションを使用する方法と、手動でクラスファイルを作成する方法に関するページを参照してください。

### <a name="using-the-add-controller-menu-option"></a>[コントローラーの追加] メニューオプションの使用

新しいコントローラーを作成する最も簡単な方法は、Visual Studio のソリューションエクスプローラーウィンドウで Controllers フォルダーを右クリックし、[**追加]、[コントローラー** ] メニューオプション (図1を参照) を選択することです。 このメニューオプションを選択すると、 **[コントローラーの追加]** ダイアログボックスが開きます (図2を参照)。

[[新しいプロジェクト] ダイアログボックスの ![](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)

**図 01**: 新しいコントローラーを追加[する (クリックすると、フルサイズの画像が表示](creating-a-controller-cs/_static/image2.png)される)

[[新しいプロジェクト] ダイアログボックスの ![](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)

**図 02**: [コントローラーの追加] ダイアログボックス ([クリックすると、フルサイズの画像が表示](creating-a-controller-cs/_static/image4.png)されます)

コントローラー名の最初の部分が **[コントローラーの追加]** ダイアログボックスで強調表示されていることに注意してください。 すべてのコントローラー名は、サフィックス*コントローラー*で終わる必要があります。 たとえば、 *Productcontroller*という名前のコントローラーを作成できますが、 *product*という名前のコントローラーは作成できません。

*コントローラーのサフィックスが*ないコントローラーを作成すると、コントローラーを呼び出すことができなくなります。 そうしないでください。この間違いを犯した後、非常に時間を無駄にすることはありません。

**リスト 1-コントローラー (productコントローラー)**

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

コントローラーは、常に Controllers フォルダーに作成する必要があります。 そうしないと、ASP.NET MVC の規則に違反することになり、他の開発者はアプリケーションを理解するのが困難になります。

### <a name="scaffolding-action-methods"></a>スキャフォールディングアクションメソッド

コントローラーを作成するときに、Create、Update、および Details アクションメソッドを自動的に生成するオプションがあります (図3を参照)。 このオプションを選択すると、リスト2のコントローラークラスが生成されます。

[アクションメソッドを自動的に作成 ![](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)

**図 03**: アクションメソッドを自動的に作成[する (クリックすると、フルサイズの画像が表示](creating-a-controller-cs/_static/image6.png)される)

**リスト 2-コントローラーの顧客コントローラー**

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

これらのメソッドは、スタブメソッドです。 顧客の詳細を作成、更新、表示するための実際のロジックを自分で追加する必要があります。 ただし、スタブメソッドは、適切な開始点を提供します。

### <a name="creating-a-controller-class"></a>コントローラークラスの作成

ASP.NET MVC コントローラーはクラスにすぎません。 必要に応じて、Visual Studio コントローラーの便利なスキャフォールディングを無視し、手動でコントローラークラスを作成することもできます。 次の手順に従います。

1. Controllers フォルダーを右クリックし、[**追加]、[新しい項目**] の順に選択し、 **[クラス]** テンプレートを選択します (図4を参照)。
2. 新しいクラスに PersonController.cs という名前を指定し、 **[追加]** ボタンをクリックします。
3. 生成されたクラスファイルを変更して、クラスが基本の System.web. Mvc. Controller クラスから継承するようにします (リスト3を参照)。

[新しいクラスの作成 ![](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)

**図 04**: 新しいクラスを作成[する (クリックすると、フルサイズの画像が表示](creating-a-controller-cs/_static/image8.png)される)

**リスト 3-コントローラー (& c)**

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

リスト3のコントローラーは、"Hello World!" という文字列を返す Index () という名前の1つのアクションを公開します。 このコントローラーアクションを呼び出すには、アプリケーションを実行し、次のような URL を要求します。

`http://localhost:40071/Person`

> [!NOTE]
> 
> ASP.NET 開発サーバーはランダムなポート番号 (40071 など) を使用します。 コントローラーを起動するための URL を入力するときは、適切なポート番号を指定する必要があります。 ポート番号を確認するには、Windows 通知領域 (画面の右下) にある ASP.NET 開発サーバーのアイコンの上にマウスポインターを置きます。
> 
> [!div class="step-by-step"]
> [前へ](adding-dynamic-content-to-a-cached-page-cs.md)
> [次へ](creating-an-action-cs.md)

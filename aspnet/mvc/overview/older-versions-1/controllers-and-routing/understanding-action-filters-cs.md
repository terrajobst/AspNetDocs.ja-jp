---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: アクションフィルターについC#て () |Microsoft Docs
author: microsoft
description: このチュートリアルの目的は、アクションフィルターについて説明することです。 アクションフィルターは、コントローラーアクションまたはコントローラー全体に適用できる属性です...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: d1c72c2355c6122f851351a8c1e8f04fa63ae04e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590092"
---
# <a name="understanding-action-filters-c"></a>アクション フィルターについて理解する (C#)

[Microsoft](https://github.com/microsoft)

[PDF のダウンロード](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> このチュートリアルの目的は、アクションフィルターについて説明することです。 アクションフィルターは、アクションが実行される方法を変更するコントローラーアクション (またはコントローラー全体) に適用可能な属性です。

## <a name="understanding-action-filters"></a>アクションフィルターについて

このチュートリアルの目的は、アクションフィルターについて説明することです。 アクションフィルターは、アクションが実行される方法を変更するコントローラーアクション (またはコントローラー全体) に適用可能な属性です。 ASP.NET MVC フレームワークには、いくつかのアクションフィルターが含まれています。

- OutputCache –このアクションフィルターは、指定された時間だけコントローラーアクションの出力をキャッシュします。
- HandleError –このアクションフィルターは、コントローラーアクションの実行時に発生したエラーを処理します。
- 承認–このアクションフィルターを使用すると、特定のユーザーまたはロールへのアクセスを制限できます。

独自のカスタムアクションフィルターを作成することもできます。 たとえば、カスタム認証システムを実装するためにカスタムアクションフィルターを作成することができます。 または、コントローラーアクションによって返されるビューデータを変更するアクションフィルターを作成することもできます。

このチュートリアルでは、最初からアクションフィルターを作成する方法について説明します。 Visual Studio の [出力] ウィンドウに対するアクションの処理のさまざまな段階をログに記録するログアクションフィルターを作成します。

### <a name="using-an-action-filter"></a>アクションフィルターの使用

アクションフィルターは属性です。 ほとんどのアクションフィルターは、個々のコントローラーアクションまたはコントローラー全体に適用できます。

たとえば、リスト1のデータコントローラーは、現在の時刻を返す `Index()` という名前のアクションを公開します。 この操作は、`OutputCache` アクションフィルターで修飾されています。 このフィルターを使用すると、アクションによって返される値が10秒間キャッシュされます。

**リスト1– `Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

ブラウザーのアドレスバーに/Data/Index URL を入力して [更新] ボタンを複数回押すことによって `Index()` アクションを繰り返し呼び出すと、10秒間は同じ時間が表示されます。 `Index()` アクションの出力は10秒間キャッシュされます (図1を参照)。

[![キャッシュ時間](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**図 01**: キャッシュされた時間 ([クリックすると、フルサイズの画像が表示](understanding-action-filters-cs/_static/image3.png)されます)

リスト1では、1つのアクションフィルター (`OutputCache` アクションフィルター) が `Index()` メソッドに適用されます。 必要に応じて、同じアクションに複数のアクションフィルターを適用できます。 たとえば、`OutputCache` と `HandleError` の両方のアクションフィルターを同じアクションに適用することができます。

リスト1では、`OutputCache` アクションフィルターが `Index()` アクションに適用されます。 また、この属性を `DataController` クラス自体に適用することもできます。 その場合、コントローラーによって公開されたアクションによって返される結果は10秒間キャッシュされます。

### <a name="the-different-types-of-filters"></a>さまざまな種類のフィルター

ASP.NET MVC フレームワークでは、次の4種類のフィルターがサポートされています。

1. 承認フィルター– `IAuthorizationFilter` 属性を実装します。
2. アクションフィルター– `IActionFilter` 属性を実装します。
3. 結果フィルター– `IResultFilter` 属性を実装します。
4. 例外フィルター– `IExceptionFilter` 属性を実装します。

フィルターは、上記の順序で実行されます。 たとえば、承認フィルターは常に実行され、他のすべての種類のフィルターの後に常に例外フィルターが実行されます。

承認フィルターは、コントローラーアクションの認証と承認を実装するために使用されます。 たとえば、承認フィルターは、承認フィルターの一例です。

アクションフィルターには、コントローラーアクションの実行前と実行後に実行されるロジックが含まれます。 たとえば、アクションフィルターを使用して、コントローラーアクションが返すビューデータを変更できます。

結果フィルターには、ビューの結果が実行される前後に実行されるロジックが含まれます。 たとえば、ビューがブラウザーに表示される直前に、ビューの結果を変更することができます。

例外フィルターは、実行するフィルターの最後の種類です。 例外フィルターを使用して、コントローラーアクションまたはコントローラーアクションの結果によって発生するエラーを処理できます。 また、例外フィルターを使用してエラーをログに記録することもできます。

それぞれの種類のフィルターは、特定の順序で実行されます。 同じ種類のフィルターを実行する順序を制御する場合は、フィルターの [順序] プロパティを設定します。

すべてのアクションフィルターの基本クラスは `System.Web.Mvc.FilterAttribute` クラスです。 特定の種類のフィルターを実装する場合は、基本フィルタークラスを継承するクラスを作成し、1つ以上の `IAuthorizationFilter`、`IActionFilter`、`IResultFilter`、または `IExceptionFilter` インターフェイスを実装する必要があります。

### <a name="the-base-actionfilterattribute-class"></a>基本 ActionFilterAttribute クラス

カスタムアクションフィルターを簡単に実装できるようにするために、ASP.NET MVC フレームワークには基本 `ActionFilterAttribute` クラスが含まれています。 このクラスは、`IActionFilter` インターフェイスと `IResultFilter` インターフェイスの両方を実装し、`Filter` クラスから継承します。

ここでは、完全に一致していない用語について説明します。 技術的には、ActionFilterAttribute クラスを継承するクラスは、アクションフィルターと結果フィルターの両方です。 ただし、厳密な意味では、ASP.NET MVC フレームワークの任意の種類のフィルターを参照するために、word アクションフィルターが使用されます。

基本 `ActionFilterAttribute` クラスには、オーバーライドできる次のメソッドがあります。

- OnActionExecuting –コントローラーアクションが実行される前に、このメソッドが呼び出されます。
- OnActionExecuted –このメソッドは、コントローラーアクションが実行された後に呼び出されます。
- OnResultExecuting –コントローラーアクションの結果が実行される前に、このメソッドが呼び出されます。
- OnResultExecuted –このメソッドは、コントローラーアクションの結果が実行された後に呼び出されます。

次のセクションでは、これらのさまざまな方法を実装する方法について説明します。

### <a name="creating-a-log-action-filter"></a>ログアクションフィルターの作成

カスタムアクションフィルターを作成する方法を説明するために、Visual Studio の [出力] ウィンドウへのコントローラーアクションの処理の段階をログに記録するカスタムアクションフィルターを作成します。 この `LogActionFilter` は、リスト2に含まれています。

**リスト2– `ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

リスト2では、`OnActionExecuting()`、`OnActionExecuted()`、`OnResultExecuting()`、および `OnResultExecuted()` の各メソッドはすべて、`Log()` メソッドを呼び出します。 メソッドの名前と現在のルートデータが `Log()` メソッドに渡されます。 `Log()` メソッドは、Visual Studio の出力ウィンドウにメッセージを書き込みます (図2を参照)。

[Visual Studio の出力ウィンドウに書き込む ![](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**図 02**: Visual Studio の出力ウィンドウへの書き込み ([クリックすると、フルサイズの画像が表示](understanding-action-filters-cs/_static/image6.png)されます)

リスト3の Home コントローラーは、ログアクションフィルターをコントローラークラス全体に適用する方法を示しています。 Home コントローラーによって公開されているアクションのいずれかが呼び出されるたびに、`Index()` メソッドまたは `About()` メソッドのいずれかによって、アクションを処理する段階が Visual Studio の出力ウィンドウに記録されます。

**リスト3– `Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>要約

このチュートリアルでは、ASP.NET MVC アクションフィルターについて説明しました。 4種類のフィルター (承認フィルター、アクションフィルター、結果フィルター、例外フィルター) について学習しました。 また、基本 `ActionFilterAttribute` クラスについても学習しました。

最後に、簡単なアクションフィルターを実装する方法について学習しました。 ここでは、Visual Studio の出力ウィンドウへのコントローラーアクションの処理の段階をログに記録するログアクションフィルターを作成しました。

> [!div class="step-by-step"]
> [前へ](asp-net-mvc-routing-overview-cs.md)
> [次へ](improving-performance-with-output-caching-cs.md)

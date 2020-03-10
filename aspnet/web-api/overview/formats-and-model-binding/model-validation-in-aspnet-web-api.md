---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API でのモデル検証-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x の ASP.NET Web API でのモデル検証の概要について説明します。
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448930"
---
# <a name="model-validation-in-aspnet-web-api"></a>ASP.NET Web API でのモデル検証

[Mike Wasson](https://github.com/MikeWasson)

この記事では、モデルに注釈を付け、データ検証に注釈を使用して、web API で検証エラーを処理する方法について説明します。 クライアントが web API にデータを送信する場合、多くの場合、処理を行う前にデータを検証する必要があります。 

## <a name="data-annotations"></a>データの注釈

ASP.NET Web API では、 [system.componentmodel](/dotnet/api/system.componentmodel.dataannotations)名前空間の属性を使用して、モデルのプロパティの検証規則を設定できます。 次のモデルがあるとします。

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

ASP.NET MVC でモデルの検証を使用したことがある場合は、このことを理解しておく必要があります。 **Required**属性では、`Name` プロパティを null にすることはできません。 **Range**属性では、`Weight` が0から999の間である必要があることが示されます。

クライアントが POST 要求を次の JSON 表現で送信するとします。

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

クライアントには、必須としてマークされている `Name` プロパティが含まれていないことがわかります。 Web API が JSON を `Product` インスタンスに変換すると、検証属性に対して `Product` が検証されます。 コントローラーアクションでは、モデルが有効かどうかを確認できます。

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

モデルの検証では、クライアントデータが安全であることは保証されません。 アプリケーションの他の層では、追加の検証が必要になる場合があります。 (たとえば、データ層によって外部キー制約が適用される場合があります)。[WEB API と Entity Framework を使用し](../data/using-web-api-with-entity-framework/part-1.md)たチュートリアルでは、これらの問題について説明します。

**"投稿中"** : クライアントがいくつかのプロパティを除外した場合に発生します。 たとえば、クライアントが次のものを送信するとします。

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

ここでは、クライアントは `Price` または `Weight`の値を指定しませんでした。 JSON フォーマッタは、不足しているプロパティに既定値の0を割り当てます。

![](model-validation-in-aspnet-web-api/_static/image1.png)

モデルの状態は有効です。これは、これらのプロパティの値が0であるためです。 これが問題かどうかは、実際のシナリオによって異なります。 たとえば、更新操作では、"zero" と "not set" の区別が必要になる場合があります。 強制的にクライアントが値を設定するようにするには、プロパティを nullable にし、 **Required**属性を設定します。

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

**"過剰ポスト"** : クライアントは、予想よりも*多く*のデータを送信できます。 次に例を示します。

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

ここでは、JSON には、`Product` モデルに存在しないプロパティ ("Color") が含まれています。 この場合、JSON フォーマッタは単にこの値を無視します。 (XML フォーマッタは同じように動作します)。モデルに読み取り専用のプロパティが含まれている場合、過剰なポストによって問題が発生します。 次に例を示します。

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

ユーザーが `IsAdmin` プロパティを更新し、自身を管理者に昇格させたくない。 最も安全な方法は、クライアントが送信できるものと完全に一致するモデルクラスを使用することです。

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> Brad Wilson のブログ投稿「[ASP.NET MVC での入力検証とモデル検証」で](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)は、投稿と過剰投稿についてよく説明しています。 この投稿は ASP.NET MVC 2 に関するものですが、問題は引き続き Web API に関連しています。

## <a name="handling-validation-errors"></a>検証エラーの処理

検証が失敗した場合、Web API からクライアントに自動的にエラーが返されることはありません。 モデルの状態を確認し、適切に応答するには、コントローラーアクションが必要です。

また、アクションフィルターを作成して、コントローラーアクションが呼び出される前にモデルの状態を確認することもできます。 次に例を示します。

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

モデルの検証が失敗した場合、このフィルターは検証エラーを含む HTTP 応答を返します。 その場合、コントローラーアクションは呼び出されません。

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

このフィルターをすべての Web API コントローラーに適用するには、構成時にフィルターのインスタンスを**Httpconfiguration. Filters**コレクションに追加します。

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

別の方法として、フィルターを個々のコントローラーまたはコントローラーアクションの属性として設定することもできます。

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]

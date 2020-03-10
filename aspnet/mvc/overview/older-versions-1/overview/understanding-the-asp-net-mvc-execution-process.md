---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: ASP.NET MVC 実行プロセスについて |Microsoft Docs
author: microsoft
description: ASP.NET MVC フレームワークがブラウザーの要求を処理する方法について説明します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435454"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>ASP.NET MVC 実行プロセスを理解する

[Microsoft](https://github.com/microsoft)

> ASP.NET MVC フレームワークがブラウザーの要求を処理する方法について説明します。

ASP.NET MVC ベースの Web アプリケーションに対する要求は、まず、HTTP モジュールである**Urlroutingmodule**オブジェクトをパススルーします。 このモジュールは、要求を解析してルートの選択を行います。 **Urlroutingmodule**オブジェクトは、現在の要求に一致する最初のルートオブジェクトを選択します。 ルートオブジェクトは**Routebase**を実装するクラスであり、通常は**route**クラスのインスタンスです。一致するルートがない場合、 **Urlroutingmodule**オブジェクトは何も行いません。これにより、要求は通常の ASP.NET または IIS 要求の処理に戻されます。

選択された**ルート**オブジェクトから、 **urlroutingmodule**オブジェクトは、**ルート**オブジェクトに関連付けられている**iroutehandler**オブジェクトを取得します。 通常、MVC アプリケーションでは、これは**Mvcroutehandler**のインスタンスになります。 **Iroutehandler**インスタンスは、 **IHttpHandler**オブジェクトを作成し、それに**ihttpcontext**オブジェクトを渡します。 既定では、MVC の**IHttpHandler**インスタンスは**MvcHandler**オブジェクトです。 次に、 **MvcHandler**オブジェクトは、最終的に要求を処理するコントローラーを選択します。

> [!NOTE]
> ASP.NET MVC Web アプリケーションを IIS 7.0 で実行する場合、MVC プロジェクトにファイル名の拡張子は必要ありません。 IIS 6.0 で実行する場合は、ファイル名の拡張子 .mvc を ASP.NET ISAPI DLL に関連付ける必要があります。

モジュールとハンドラーは、ASP.NET MVC フレームワークへのエントリポイントです。 これらは次のアクションを実行します。

- MVC Web アプリケーションの適切なコントローラーを選択する。
- 特定のコントローラー インスタンスを取得する。
- コントローラーの**Execute**メソッドを呼び出します。

MVC Web プロジェクトの実行段階を次に示します。

- アプリケーションへの最初の要求を受け取る 

    - Global.asax ファイルで、 **route**オブジェクトが**routetable**オブジェクトに追加されます。
- ルーティングを実行する 

    - **Urlroutingmodule**モジュールは、 **routetable**コレクション内の最初に一致する**ルート**オブジェクトを使用して、 **routetable**オブジェクトを作成します。このオブジェクトは、このオブジェクトを使用して**RequestContext** (**ihttpcontext**) オブジェクトを作成します。
- MVC 要求ハンドラーを作成する 

    - **Mvcroutehandler**オブジェクトは、 **MvcHandler**クラスのインスタンスを作成し、そのインスタンスを**RequestContext**インスタンスに渡します。
- コントローラーを作成する 

    - **MvcHandler**オブジェクトは、 **RequestContext**インスタンスを使用して、コントローラーインスタンスを作成するための**IControllerFactory**オブジェクト (通常は**defaultcontroller ファクトリ**クラスのインスタンス) を識別します。
- コントローラーの実行- **MvcHandler**インスタンスは、コントローラーの**execute**メソッドを呼び出します。 |
- アクションを呼び出す 

    - ほとんどのコントローラーは、**コントローラー**の基本クラスを継承します。 コントローラーの場合、コントローラーに関連付けられているコントローラーのコントローラークラスのアクションメソッドを決定**し、その**メソッドを呼び出します。
- 結果を実行する 

    - 一般的なアクションメソッドでは、ユーザー入力を受け取り、適切な応答データを準備してから、結果の型を返すことによって結果を実行できます。 実行できる組み込みの結果型には、 **viewresult** (ビューをレンダリングし、最も頻繁に使用される結果型)、 **RedirectToRouteResult**、 **redirectresult**、 **Contentresult**、 **jsonresult**、および**emptyresult**があります。

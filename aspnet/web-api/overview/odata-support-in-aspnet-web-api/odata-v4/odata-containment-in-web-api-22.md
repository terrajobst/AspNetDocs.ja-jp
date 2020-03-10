---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: Web API 2.2 | を使用した OData v4 の含有Microsoft Docs
author: rick-anderson
description: 従来、エンティティはエンティティセット内にカプセル化されている場合にのみアクセスできました。 ただし、OData v4 には、シングルトンと Con という2つの追加オプションがあります。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 50050e40c4c42bf6d769d077c27864ee6417d4db
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421402"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a>Web API 2.2 を使用した OData v4 の含有

Jinfu Tan 別

> 従来、エンティティはエンティティセット内にカプセル化されている場合にのみアクセスできました。 ただし、OData v4 には、シングルトンとコンテインメントという2つの追加オプションが用意されています。どちらも WebAPI 2.2 でサポートされています。

このトピックでは、WebApi 2.2 の OData エンドポイントでコンテインメントを定義する方法について説明します。 コンテインメントの詳細については、「[コンテインメントは OData v4 に付属](https://blogs.msdn.com/b/odatateam/archive/2014/03/13/containment-is-coming-with-odata-v4.aspx)しています」を参照してください。 Web API で OData V4 エンドポイントを作成するには、「 [ASP.NET Web API 2.2 を使用して odata V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を参照してください。

まず、次のデータモデルを使用して、OData サービスにコンテインメントドメインモデルを作成します。

![データ モデル](odata-containment-in-web-api-22/_static/image1.png)

アカウントには多くの PaymentInstruments (PI) が含まれていますが、PI のエンティティセットは定義されていません。 代わりに、Pi にはアカウントを使用してのみアクセスできます。

このトピックで使用するソリューションは、 [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)からダウンロードできます。

## <a name="defining-the-data-model"></a>データモデルの定義

1. CLR 型を定義します。

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    `Contained` 属性は、コンテインメントナビゲーションプロパティに使用されます。
2. CLR 型に基づいて EDM モデルを生成します。

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    `Contained` 属性が対応するナビゲーションプロパティに追加された場合、`ODataConventionModelBuilder` は EDM モデルの作成を処理します。 プロパティがコレクション型の場合は、`GetCount(string NameContains)` 関数も作成されます。

    生成されたメタデータは、次のようになります。

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    `ContainsTarget` 属性は、ナビゲーションプロパティがコンテインメントであることを示します。

## <a name="define-the-containing-entity-set-controller"></a>含まれているエンティティセットコントローラーを定義する

含まれているエンティティは独自のコントローラーを持っていません。アクションは、含んでいるエンティティセットコントローラーで定義されています。 このサンプルでは、AccountsController がありますが、PaymentInstrumentsController はありません。

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

OData パスが4つ以上のセグメントの場合、上記のコントローラーの `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` など、属性ルーティングのみが機能します。 それ以外の場合は、属性と従来のルーティングの両方が機能します。たとえば、`GetPayInPIs(int key)` は `GET ~/Accounts(1)/PayinPIs`と一致します。

*この記事の元の内容については、Leo Hu に感謝します。*

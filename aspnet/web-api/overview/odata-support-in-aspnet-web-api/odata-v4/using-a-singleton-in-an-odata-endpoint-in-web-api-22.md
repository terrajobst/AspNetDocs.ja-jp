---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Web API 2.2 を使用して OData v4 でシングルトンを作成する |Microsoft Docs
author: rick-anderson
description: このトピックでは、Web API 2.2 で OData エンドポイントにシングルトンを定義する方法について説明します。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504502"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a>Web API 2.2 を使用して OData v4 でシングルトンを作成する

Zoe Luo 別

> 従来、エンティティはエンティティセット内にカプセル化されている場合にのみアクセスできました。 ただし、OData v4 には、シングルトンとコンテインメントという2つの追加オプションが用意されています。どちらも WebAPI 2.2 でサポートされています。

この記事では、Web API 2.2 で OData エンドポイントにシングルトンを定義する方法について説明します。 シングルトンとは何か、およびそれを使用する利点については、「[シングルトンを使用した特殊なエンティティの定義](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)」を参照してください。 Web API で OData V4 エンドポイントを作成するには、「 [ASP.NET Web API 2.2 を使用して odata V4 エンドポイントを作成](create-an-odata-v4-endpoint.md)する」を参照してください。 

次のデータモデルを使用して、Web API プロジェクトにシングルトンを作成します。

![データ モデル](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

`Umbrella` という名前のシングルトンが `Company`型に基づいて定義され、`Employees` という名前のエンティティセットが `Employee`型に基づいて定義されます。

このチュートリアルで使用するソリューションは、 [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)からダウンロードできます。

## <a name="define-the-data-model"></a>データ モデルを定義する

1. CLR 型を定義します。

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. CLR 型に基づいて EDM モデルを生成します。

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    ここでは、`builder.Singleton<Company>("Umbrella")` はモデルビルダーに対して、EDM モデルで `Umbrella` という名前のシングルトンを作成するように指示します。

    生成されたメタデータは、次のようになります。

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    メタデータから、`Employees` エンティティセットのナビゲーションプロパティ `Company` がシングルトン `Umbrella`にバインドされていることがわかります。 バインドは `ODataConventionModelBuilder`によって自動的に行われます。これは、`Umbrella` には `Company` 型しかないためです。 モデルにあいまいさがある場合は、`HasSingletonBinding` を使用して、ナビゲーションプロパティをシングルトンに明示的にバインドすることができます。`HasSingletonBinding` は、CLR 型定義で `Singleton` 属性を使用するのと同じ効果があります。

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a>シングルトンコントローラーを定義する

EntitySet コントローラーと同様に、シングルトンコントローラーは `ODataController`から継承し、シングルトンコントローラー名を `[singletonName]Controller`する必要があります。

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

さまざまな種類の要求を処理するには、コントローラーでアクションを事前定義する必要があります。 WebApi 2.2 では、既定で**属性ルーティング**が有効になっています。 たとえば、属性ルーティングを使用して `Company` からの `Revenue` のクエリを処理するアクションを定義するには、次のように指定します。

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

各アクションの属性を定義しない場合は、 [OData ルーティング規則](../odata-routing-conventions.md)に従うアクションを定義するだけです。 シングルトンに対してクエリを実行するためにキーは必要ないため、シングルトンコントローラーで定義されたアクションは、entityset コントローラーで定義されているアクションとは少し異なります。

参照用に、シングルトンコントローラーのすべてのアクション定義のメソッドシグネチャを次に示します。

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

基本的に、これはサービス側で行う必要があることです。 [サンプルプロジェクト](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)には、ソリューションのすべてのコードと、シングルトンの使用方法を示す OData クライアントが含まれています。 クライアントは、「 [OData V4 クライアントアプリの作成](create-an-odata-v4-client-app.md)」の手順に従って構築されます。

。 

*この記事の元の内容については、Leo Hu に感謝します。*

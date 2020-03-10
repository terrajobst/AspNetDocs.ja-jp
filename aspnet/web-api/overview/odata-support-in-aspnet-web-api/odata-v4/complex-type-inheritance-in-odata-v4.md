---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: ASP.NET Web API | を使用した OData v4 での複合型の継承Microsoft Docs
author: microsoft
description: OData v4 仕様によれば、複合型は別の複合型から継承できます。 複合型は、キーを持たない構造化された型です。Web API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448132"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>ASP.NET Web API を使用した OData v4 での複合型の継承

[Microsoft](https://github.com/microsoft)

> OData v4[仕様](http://www.odata.org/documentation/odata-version-4-0/)によれば、複合型は別の複合型から継承できます。 *複合*型は、キーを持たない構造化された型です。Web API OData 5.3 では、複合型の継承がサポートされています。
> 
> このトピックでは、複雑な継承型を使用して entity data model (EDM) を構築する方法について説明します。 完全なソースコードについては、「 [OData 複合型の継承のサンプル](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)」を参照してください。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - Web API OData 5.3
> - OData v4

## <a name="model-hierarchy"></a>モデル階層

複合型の継承について説明するために、次のクラス階層を使用します。

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape` は抽象複合型です。 `Rectangle`、`Triangle`、および `Circle` は `Shape`から派生した複合型であり、`RoundRectangle` から派生します。`Rectangle` `Window` はエンティティ型で、`Shape` インスタンスが含まれています。

これらの型を定義する CLR クラスを次に示します。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>EDM モデルの構築

EDM を作成するには、CLR 型から継承関係を推論する**ODataConventionModelBuilder**を使用できます。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

**使用**を使用して、EDM を明示的に構築することもできます。 この処理にはより多くのコードが必要ですが、EDM をより細かく制御できます。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

次の2つの例では、同じ EDM スキーマを作成します。

## <a name="metadata-document"></a>メタデータドキュメント

ここでは、複合型の継承を示す OData メタデータドキュメントについて説明します。

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

メタデータドキュメントから、次のことを確認できます。

- `Shape` 複合型は abstract です。
- `Rectangle`、`Triangle`、および `Circle` 複合型には `Shape`の基本型があります。
- `RoundRectangle` 型には `Rectangle`基本型があります。

## <a name="casting-complex-types"></a>キャスト (複合型を)

複合型へのキャストがサポートされるようになりました。 たとえば、次のクエリでは、`Shape` を `Rectangle`にキャストします。

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

応答ペイロードを次に示します。

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]

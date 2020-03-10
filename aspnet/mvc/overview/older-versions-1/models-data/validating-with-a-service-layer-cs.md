---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: サービス層を使用したC#検証 () |Microsoft Docs
author: StephenWalther
description: コントローラーアクションから別のサービスレイヤーに検証ロジックを移動する方法について説明します。 このチュートリアルでは、Stephen Walther がその方法について説明します。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: da1a1c9cc79a452eb0d7597810e86f7bcf6cd179
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436606"
---
# <a name="validating-with-a-service-layer-c"></a>サービス層の検証 (C#)

[Stephen Walther](https://github.com/StephenWalther)

> コントローラーアクションから別のサービスレイヤーに検証ロジックを移動する方法について説明します。 このチュートリアルでは、Stephen Walther は、コントローラーレイヤーからサービス層を分離することによって、問題を明確に分離する方法について説明します。

このチュートリアルの目的は、ASP.NET MVC アプリケーションで検証を実行する1つの方法を説明することです。 このチュートリアルでは、検証ロジックをコントローラーから別のサービス層に移動する方法について説明します。

## <a name="separating-concerns"></a>懸念事項の分離

ASP.NET MVC アプリケーションをビルドする場合は、コントローラーアクション内にデータベースロジックを配置しないでください。 データベースとコントローラーのロジックを混在させると、時間の経過と共にアプリケーションの保守が困難になります。 すべてのデータベースロジックを別のリポジトリレイヤーに配置することをお勧めします。

たとえば、リスト1には、ProductRepository という名前の単純なリポジトリが含まれています。 製品リポジトリには、アプリケーションのすべてのデータアクセスコードが含まれています。 この一覧には、製品リポジトリによって実装される IProductRepository インターフェイスも含まれています。

**リスト 1--Models\ProductRepository.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

リスト2のコントローラーは、Index () アクションと Create () アクションの両方でリポジトリレイヤーを使用します。 このコントローラーには、データベースロジックが含まれていないことに注意してください。 リポジトリレイヤーを作成することで、問題の明確な分離を維持することができます。 コントローラーはアプリケーションフロー制御ロジックを担当し、リポジトリはデータアクセスロジックを担当します。

**リスト 2-コントローラー (productコントローラー)**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a>サービス層の作成

そのため、アプリケーションフロー制御ロジックはコントローラーに属し、データアクセスロジックはリポジトリに属します。 その場合は、検証ロジックをどこに配置すればよいでしょうか。 1つの方法として、検証ロジックを*サービス層*に配置する方法があります。

サービスレイヤーは、コントローラーとリポジトリレイヤー間の通信を仲介する ASP.NET MVC アプリケーションの追加レイヤーです。 サービス層にはビジネスロジックが含まれます。 特に、検証ロジックが含まれています。

たとえば、リスト3の product service レイヤーには CreateProduct () メソッドがあります。 CreateProduct () メソッドは、製品リポジトリに製品を渡す前に、ValidateProduct () メソッドを呼び出して新しい製品を検証します。

**リスト 3-Modelproductservice.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

製品コントローラーは、リポジトリレイヤーではなくサービスレイヤーを使用するように、リスト4で更新されています。 コントローラーレイヤーは、サービスレイヤーと通信します。 サービス層は、リポジトリレイヤーと通信します。 各レイヤーには個別の責任があります。

**リスト 4-コントローラー (productコントローラー)**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

Product service が product controller コンストラクターに作成されていることに注意してください。 製品サービスが作成されると、モデル状態ディクショナリがサービスに渡されます。 製品サービスは、モデルの状態を使用して、検証エラーメッセージをコントローラーに返します。

## <a name="decoupling-the-service-layer"></a>サービス層の分離

コントローラー層とサービス層を1つの観点で分離できませんでした。 コントローラー層とサービス層は、モデルの状態を介して通信します。 つまり、サービスレイヤーは、ASP.NET MVC フレームワークの特定の機能に依存しています。

サービス層は、可能な限りコントローラーレイヤーから分離する必要があります。 理論的には、ASP.NET MVC アプリケーションだけでなく、あらゆる種類のアプリケーションでサービスレイヤーを使用できるようにする必要があります。 たとえば、将来的には、アプリケーションの WPF フロントエンドを構築することが必要になる場合があります。 サービスレイヤーから ASP.NET MVC モデルの状態に対する依存関係を削除する方法が見つかります。

リスト5では、サービス層が更新され、モデルの状態が使用されなくなりました。 代わりに、IValidationDictionary インターフェイスを実装する任意のクラスを使用します。

**リスト 5-Modelproductservice.cs (分離)**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

IValidationDictionary インターフェイスは、リスト6で定義されています。 この単純なインターフェイスには、1つのメソッドと1つのプロパティがあります。

**リスト 6-modelivalidationdictionary, cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

リスト7のクラス (ModelStateWrapper クラス) には、IValidationDictionary インターフェイスが実装されています。 モデル状態ディクショナリをコンストラクターに渡すことによって、ModelStateWrapper クラスをインスタンス化できます。

**リスト 7-Models\ModelStateWrapper.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

最後に、リスト8の更新されたコントローラーは、コンストラクターでサービス層を作成するときに ModelStateWrapper を使用します。

**8-コントローラーの一覧表示**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

IValidationDictionary インターフェイスと ModelStateWrapper クラスを使用すると、サービスレイヤーをコントローラーレイヤーから完全に分離することができます。 サービス層は、モデルの状態に依存しなくなりました。 IValidationDictionary インターフェイスを実装する任意のクラスをサービス層に渡すことができます。 たとえば、WPF アプリケーションでは、単純なコレクションクラスを使用して IValidationDictionary インターフェイスを実装できます。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、ASP.NET MVC アプリケーションで検証を実行する方法の1つについて説明することでした。 このチュートリアルでは、すべての検証ロジックをコントローラーから別のサービス層に移動する方法について学習しました。 また、ModelStateWrapper クラスを作成して、コントローラーレイヤーからサービス層を分離する方法についても学習しました。

> [!div class="step-by-step"]
> [前へ](validating-with-the-idataerrorinfo-interface-cs.md)
> [次へ](validation-with-the-data-annotation-validators-cs.md)

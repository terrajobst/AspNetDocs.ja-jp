---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: ASP.NET Web API 2 OData-ASP.NET 4.x のセキュリティガイダンス
author: MikeWasson
description: ASP.NET 4.x で ASP.NET Web API 2 の OData を使用してデータセットを公開するときに考慮する必要があるセキュリティの問題について説明します。
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448294"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a>ASP.NET Web API 2 OData のセキュリティガイダンス

[Mike Wasson](https://github.com/MikeWasson)

このトピックでは、ASP.NET 4.x で ASP.NET Web API 2 の OData を使用してデータセットを公開するときに考慮する必要があるセキュリティの問題について説明します。

## <a name="edm-security"></a>EDM のセキュリティ

クエリセマンティクスは、基になるモデル型ではなく、entity data model (EDM) に基づいています。 EDM からプロパティを除外することはできますが、クエリには表示されません。 たとえば、モデルに Salary プロパティを持つ Employee 型が含まれているとします。 このプロパティを EDM から除外して、クライアントから非表示にすることができます。

EDM からプロパティを除外するには、2つの方法があります。 モデルクラスのプロパティに対して **[Ignoredatamember]** 属性を設定できます。

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

プログラムを使用して EDM からプロパティを削除することもできます。

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a>クエリのセキュリティ

悪意のあるクライアントや単純なクライアントでは、実行に非常に長い時間がかかるクエリを作成できる場合があります。 最悪の場合、これによってサービスへのアクセスが中断される可能性があります。

[クエリ可能 **]** 属性は、クエリを解析、検証、適用するアクションフィルターです。 このフィルターにより、クエリオプションが LINQ 式に変換されます。 OData コントローラーが**iqueryable**型を返すと、 **iqueryable** linq プロバイダーは linq 式をクエリに変換します。 そのため、パフォーマンスは、使用される LINQ プロバイダーと、データセットまたはデータベーススキーマの特定の特性に依存します。

ASP.NET Web API での OData クエリオプションの使用の詳細については、「 [Odata クエリオプションのサポート](supporting-odata-query-options.md)」を参照してください。

すべてのクライアントが信頼されている (たとえば、エンタープライズ環境で) ことがわかっている場合、またはデータセットが小さい場合は、クエリのパフォーマンスが問題になるとは限りません。 それ以外の場合は、次の推奨事項を考慮する必要があります。

- さまざまなクエリを使用してサービスをテストし、データベースをプロファイルします。
- サーバードリブンページングを有効にして、1つのクエリで大きなデータセットを返さないようにします。 詳細については、「[サーバードリブンページング](supporting-odata-query-options.md#server-paging)」を参照してください。 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- $Filter と $orderby 必要がありますか。 アプリケーションによっては、$top と $skip を使用したクライアントのページングが許可されているが、他のクエリオプションは無効になっている場合があります 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- クラスター化インデックスのプロパティに $orderby を制限することを検討してください。 クラスター化インデックスを使用せずに大きなデータを並べ替えると、処理が遅くなります。 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- 最大ノード数: **[クエリ可能]** の**MaxNodeCount**プロパティは、$filter 構文ツリーで許可される最大ノード数を設定します。 既定値は100ですが、多数のノードがコンパイルに時間がかかる場合があるため、値を小さく設定することをお勧めします。 これは、LINQ to Objects (つまり、中間の LINQ プロバイダーを使用せずにメモリ内のコレクションに対する LINQ クエリ) を使用している場合に特に当てはまります。 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- Any () 関数と all () 関数は、処理速度が低下する可能性があるため、無効にすることを検討してください。 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- 文字列プロパティに大きな文字列&#8212;が含まれている場合は、製品の説明また&#8212;はブログのエントリによって文字列関数の無効化が検討されます。 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- ナビゲーションプロパティのフィルター選択を禁止することを検討してください。 ナビゲーションプロパティをフィルター処理すると、データベーススキーマによっては、結合が遅くなる可能性があります。 次のコードは、ナビゲーションプロパティのフィルター処理を妨げるクエリ検証コントロールを示しています。 クエリ検証コントロールの詳細については、「[クエリの検証](supporting-odata-query-options.md#query-validation)」を参照してください。 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- データベース用にカスタマイズされたバリデーターを記述して、$filter クエリを制限することを検討してください。 たとえば、次の2つのクエリについて考えてみます。 

  - "A" で始まる姓を持つアクターを持つすべてのムービー。
  - 1994でリリースされたすべてのムービー。

    映画がアクターによってインデックス付けされていない限り、最初のクエリでは、データベースエンジンがムービーの一覧全体をスキャンするように要求することがあります。 2番目のクエリは許容できるかもしれませんが、release year によってムービーのインデックスが作成されると想定します。

    次のコードは、"ReleaseYear" プロパティと "Title" プロパティをフィルター処理できますが、その他のプロパティは使用できないバリデーターを示しています。

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- 一般に、必要な $filter 関数を検討してください。 クライアントが $filter の完全な表現力を必要としない場合は、許可される関数を制限できます。

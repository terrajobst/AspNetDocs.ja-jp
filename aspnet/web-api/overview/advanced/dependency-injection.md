---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2 での依存関係の注入-ASP.NET 4.x
author: MikeWasson
description: このチュートリアルでは、ASP.NET 4.x の ASP.NET Web API controller に依存関係を挿入する方法について説明します。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: f9c212af92168ac02644625b9aa8ec1bef329cab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504946"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a>ASP.NET Web API 2 での依存関係の挿入

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> このチュートリアルでは、ASP.NET Web API コントローラーに依存関係を挿入する方法について説明します。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - Web API 2
> - [Unity アプリケーションブロック](https://www.nuget.org/packages/Unity/)
> - Entity Framework 6 (バージョン5も動作)

## <a name="what-is-dependency-injection"></a>依存関係の挿入とは

"*依存関係*" とは、他のオブジェクトが必要とする任意のオブジェクトのことです。 たとえば、データアクセスを処理する[リポジトリ](http://martinfowler.com/eaaCatalog/repository.html)を定義するのは一般的です。 例を使って説明します。 まず、ドメインモデルを定義します。

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

Entity Framework を使用してデータベースに項目を格納する単純なリポジトリクラスを次に示します。

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

次に、`Product` エンティティの GET 要求をサポートする Web API コントローラーを定義します。 (簡潔にするために POST やその他の方法を抜けています)。最初の試行は次のとおりです。

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

コントローラークラスが `ProductRepository`に依存しており、コントローラーが `ProductRepository` インスタンスを作成することに注意してください。 ただし、いくつかの理由から、この方法で依存関係をハードコーディングすることは不適切です。

- `ProductRepository` を別の実装に置き換える場合は、コントローラークラスも変更する必要があります。
- `ProductRepository` に依存関係がある場合は、コントローラー内でこれらを構成する必要があります。 複数のコントローラーを持つ大規模なプロジェクトの場合、構成コードはプロジェクト全体にわたって分散されます。
- コントローラーはデータベースに対してクエリを実行するようにハードコーディングされているため、単体テストは困難です。 単体テストでは、モックまたはスタブリポジトリを使用する必要があります。これは、現在の設計ではできません。

これらの問題に対処するには、コントローラーにリポジトリを*挿入*します。 まず、`ProductRepository` クラスをインターフェイスにリファクタリングします。

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

次に、`IProductRepository` をコンストラクターパラメーターとして指定します。

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

この例では、[コンストラクターの挿入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)を使用します。 Setter*インジェクション*を使用することもできます。 setter メソッドまたはプロパティを使用して依存関係を設定します。

しかし、アプリケーションではコントローラーが直接作成されないため、問題が発生しました。 Web API は要求をルーティングするときにコントローラーを作成し、Web API は `IProductRepository`について何も知らない。 ここで、Web API 依存関係競合回避モジュールが登場します。

## <a name="the-web-api-dependency-resolver"></a>Web API 依存関係競合回避モジュール

Web API は、依存関係を解決するための**Idependencyresolver**インターフェイスを定義します。 インターフェイスの定義を次に示します。

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

**IDependencyScope**インターフェイスには、次の2つのメソッドがあります。

- **GetService**は、型のインスタンスを1つ作成します。
- **Getservices**は、指定された型のオブジェクトのコレクションを作成します。

**Idependencyresolver**メソッドは**IDependencyScope**を継承し、 **beginscope**メソッドを追加します。 スコープについては、このチュートリアルで後ほど説明します。

Web API はコントローラーインスタンスを作成するときに、まず**Idependencyresolver. GetService**を呼び出し、コントローラーの種類を渡します。 この機能拡張フックを使用してコントローラーを作成し、依存関係を解決することができます。 **GetService**が null を返す場合、Web API はコントローラークラスでパラメーターなしのコンストラクターを検索します。

## <a name="dependency-resolution-with-the-unity-container"></a>Unity コンテナーを使用した依存関係の解決

完全な**Idependencyresolver**実装をゼロから作成することもできますが、インターフェイスは Web API と既存の IoC コンテナーの間のブリッジとして機能するように設計されています。

IoC コンテナーは、依存関係の管理を担当するソフトウェアコンポーネントです。 型をコンテナーに登録した後、コンテナーを使用してオブジェクトを作成します。 コンテナーは、依存関係の関係を自動的に判別します。 多くの IoC コンテナーでは、オブジェクトの有効期間やスコープなどを制御することもできます。

> [!NOTE]
> "IoC" は、フレームワークがアプリケーションコードを呼び出す一般的なパターンである "コントロールの反転" を表します。 IoC コンテナーによってオブジェクトが構築され、通常の制御フローが "反転" されます。

このチュートリアルでは、Microsoft のパターン &amp; プラクティスから[Unity](https://msdn.microsoft.com/library/ff647202.aspx)を使用します。 (他の一般的なライブラリには、[城主の Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Ninject](http://www.ninject.org/)、および構造体の[マップ](http://structuremap.github.io/documentation/)が含まれています)。NuGet パッケージマネージャーを使用して Unity をインストールできます。 Visual Studio の **[ツール]** メニューで、 **[NuGet パッケージマネージャー]** 、 **[パッケージマネージャーコンソール]** の順に選択します。 [パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

Unity コンテナーをラップする**Idependencyresolver**の実装を次に示します。

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> **GetService**メソッドが型を解決できない場合は、 **null**を返す必要があります。 **Getservices**メソッドが型を解決できない場合は、空のコレクションオブジェクトが返されます。 不明な型に対しては例外をスローしません。

## <a name="configuring-the-dependency-resolver"></a>依存関係競合回避モジュールの構成

グローバル**Httpconfiguration**オブジェクトの**dependencyresolver**プロパティに依存関係競合回避モジュールを設定します。

次のコードでは、`IProductRepository` インターフェイスを Unity に登録し、`UnityResolver`を作成します。

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a>依存関係のスコープとコントローラーの有効期間

コントローラーは要求ごとに作成されます。 オブジェクトの有効期間を管理するために、 **Idependencyresolver**は*スコープ*の概念を使用します。

**Httpconfiguration**オブジェクトにアタッチされている依存関係競合回避モジュールには、グローバルスコープがあります。 Web API がコントローラーを作成すると、 **Beginscope**が呼び出されます。 このメソッドは、子スコープを表す**IDependencyScope**を返します。

Web API は、子スコープで**GetService**を呼び出してコントローラーを作成します。 要求が完了すると、Web API は子スコープで**Dispose**を呼び出します。 **Dispose**メソッドを使用して、コントローラーの依存関係を破棄します。

**Beginscope**の実装方法は、IoC コンテナーによって異なります。 Unity の場合、スコープは子コンテナーに対応します。

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

ほとんどの IoC コンテナーには同様の同等のものがあります。

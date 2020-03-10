---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: モデルの追加 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: c5525cfe940cadff5113c63eb0508d15697b5606
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499084"
---
# <a name="adding-a-model"></a>モデルの追加

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

このセクションでは、データベースのムービーを管理するためのクラスをいくつか追加します。 これらのクラスは、ASP.NET MVC アプリの一部&quot; &quot;モデルになります。

[Entity Framework](https://docs.microsoft.com/ef/)と呼ばれる .NET Framework のデータアクセステクノロジを使用して、これらのモデルクラスを定義および操作します。 Entity Framework (EF と呼ばれることもあります) では、 *Code First*と呼ばれる開発パラダイムがサポートされています。 Code First を使用すると、単純なクラスを記述することによってモデルオブジェクトを作成できます。 (これらは、&quot;の古い CLR オブジェクトからの POCO クラスとも呼ばれます。&quot;)その後、データベースをクラスからすぐに作成することができます。これにより、非常にクリーンで迅速な開発ワークフローが可能になります。 データベースを最初に作成する必要がある場合でも、このチュートリアルに従って MVC と EF アプリの開発について学習することができます。 その後、Tom Fizmakens [ASP.NET スキャフォールディング](xref:visual-studio/overview/2013/aspnet-scaffolding-overview)チュートリアルに従うことができます。このチュートリアルでは、データベースの最初のアプローチについて説明します。

## <a name="adding-model-classes"></a>モデルクラスの追加

**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。

![](adding-a-model/_static/image1.png)

&quot;Movie&quot;*クラス*名を入力します。

次の5つのプロパティを `Movie` クラスに追加します。

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

`Movie` クラスを使用して、データベース内の映画を表します。 `Movie` オブジェクトの各インスタンスは、データベーステーブル内の行に対応し、`Movie` クラスの各プロパティはテーブル内の列にマップされます。

注: system.object と関連クラスを使用するには、 [Entity Framework NuGet パッケージ](https://www.nuget.org/packages/EntityFramework/)をインストールする必要があります。 詳細な手順については、リンク先を参照してください。

同じファイルで、次の `MovieDBContext` クラスを追加します。

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext` クラスは Entity Framework ムービーデータベースコンテキストを表します。このコンテキストでは、データベース内の `Movie` クラスインスタンスのフェッチ、格納、および更新が処理されます。 `MovieDBContext` は、Entity Framework によって提供される `DbContext` 基底クラスから派生します。

`DbContext` と `DbSet`を参照できるようにするには、ファイルの先頭に次の `using` ステートメントを追加する必要があります。

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

これを行うには、using ステートメントを手動で追加するか、赤色の波線の上にマウスポインターを移動し、`Show potential fixes` をクリックして `using System.Data.Entity;` をクリックします。

![](adding-a-model/_static/image2.png)

注: いくつかの未使用の `using` ステートメントが削除されました。 Visual Studio では、未使用の依存関係が灰色で表示されます。 灰色の依存関係をポイントし、[`Show potential fixes`] をクリックし、 **[未使用の using の削除]** をクリックすることで、未使用の依存関係を削除できます。

![](adding-a-model/_static/image3.png)

最後にモデル (MVC では M) を追加しました。 次のセクションでは、データベース接続文字列を操作します。

> [!div class="step-by-step"]
> [前へ](adding-a-view.md)
> [次へ](creating-a-connection-string.md)

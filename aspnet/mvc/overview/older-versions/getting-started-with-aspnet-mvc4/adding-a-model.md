---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: モデルの追加 |Microsoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457805"
---
# <a name="adding-a-model"></a>モデルの追加

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../getting-started/introduction/getting-started.md)入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。

このセクションでは、データベースのムービーを管理するためのクラスをいくつか追加します。 これらのクラスは、ASP.NET MVC アプリケーションの一部&quot; &quot;モデルになります。

[Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx)と呼ばれる .NET Framework のデータアクセステクノロジを使用して、これらのモデルクラスを定義および操作します。 Entity Framework (EF と呼ばれることもあります) では、 *Code First*と呼ばれる開発パラダイムがサポートされています。 Code First を使用すると、単純なクラスを記述することによってモデルオブジェクトを作成できます。 (これらは、&quot;の古い CLR オブジェクトからの POCO クラスとも呼ばれます。&quot;)その後、データベースをクラスからすぐに作成することができます。これにより、非常にクリーンで迅速な開発ワークフローが可能になります。

## <a name="adding-model-classes"></a>モデルクラスの追加

**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。

![](adding-a-model/_static/image1.png)

&quot;Movie&quot;*クラス*名を入力します。

次の5つのプロパティを `Movie` クラスに追加します。

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

`Movie` クラスを使用して、データベース内の映画を表します。 `Movie` オブジェクトの各インスタンスは、データベーステーブル内の行に対応し、`Movie` クラスの各プロパティはテーブル内の列にマップされます。

同じファイルで、次の `MovieDBContext` クラスを追加します。

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext` クラスは Entity Framework ムービーデータベースコンテキストを表します。このコンテキストでは、データベース内の `Movie` クラスインスタンスのフェッチ、格納、および更新が処理されます。 `MovieDBContext` は、Entity Framework によって提供される `DbContext` 基底クラスから派生します。

`DbContext` と `DbSet`を参照できるようにするには、ファイルの先頭に次の `using` ステートメントを追加する必要があります。

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

完全な*Movie.cs*ファイルを次に示します。 (不要な using ステートメントがいくつか削除されました)。

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>接続文字列の作成と SQL Server LocalDB の使用

作成した `MovieDBContext` クラスによって、データベースへの接続と `Movie` オブジェクトのデータベースレコードへのマッピングのタスクが処理されます。 ただし、接続先のデータベースを指定する方法について質問することもできます。 これを行うに*は、アプリケーションの web.config ファイルに*接続情報を追加します。

アプリケーション*ルートの web.config ファイル*を開きます。 ( *Views*フォルダー*内の web.config ファイルで*はありません)。赤で囲まれた web.config ファイルを*開きます。*

![](adding-a-model/_static/image2.png)

次の接続文字列を web.config ファイルの `<connectionStrings>` 要素に追加*します。*

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

次の例は、新しい接続文字列が追加された web.config ファイルの一部を示して*い*ます。

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

この少量のコードと XML は、ムービーデータを表現してデータベースに格納するために記述する必要があるすべてのものです。

次に、ムービーデータを表示するために使用できる新しい `MoviesController` クラスを作成し、ユーザーが新しいムービーの一覧を作成できるようにします。

> [!div class="step-by-step"]
> [前へ](adding-a-view.md)
> [次へ](accessing-your-models-data-from-a-controller.md)

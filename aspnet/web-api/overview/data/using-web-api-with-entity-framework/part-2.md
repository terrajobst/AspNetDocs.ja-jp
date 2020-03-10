---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: モデルとコントローラーの追加 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449188"
---
# <a name="add-models-and-controllers"></a>モデルとコントローラーの追加

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://github.com/MikeWasson/BookService)

このセクションでは、データベースエンティティを定義するモデルクラスを追加します。 次に、それらのエンティティに対して CRUD 操作を実行する Web API コントローラーを追加します。

## <a name="add-model-classes"></a>モデルクラスの追加

このチュートリアルでは、Entity Framework (EF) への "Code First" アプローチを使用してデータベースを作成します。 Code First では、データベースC#テーブルに対応するクラスを記述し、EF によってデータベースが作成されます。 (詳細については、「 [Entity Framework の開発方法](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf)」を参照してください)。

まず、ドメインオブジェクトを POCOs (plain old CLR object) として定義します。 次の POCOs が作成されます。

- Author
- Book

ソリューションエクスプローラーで、[モデル] フォルダーを右クリックします。 **[追加]** を選択し、 **[クラス]** を選択します。 クラスに `Author` という名前を付けます。

![](part-2/_static/image1.png)

Author.cs のすべての定型コードを次のコードに置き換えます。

[!code-csharp[Main](part-2/samples/sample1.cs)]

次のコードを使用して、`Book`という名前の別のクラスを追加します。

[!code-csharp[Main](part-2/samples/sample2.cs)]

Entity Framework は、これらのモデルを使用してデータベーステーブルを作成します。 モデルごとに、`Id` プロパティがデータベーステーブルの主キー列になります。

Book クラスでは、`AuthorId` によって `Author` テーブルに外部キーが定義されます。 (わかりやすくするために、各書籍には1人の著者がいることを前提としています)。Book クラスには、関連する `Author`へのナビゲーションプロパティも含まれています。 ナビゲーションプロパティを使用して、コード内の関連する `Author` にアクセスできます。 第4部では、エンティティの関係を[処理](part-4.md)するナビゲーションプロパティについて詳しく説明します。

## <a name="add-web-api-controllers"></a>Web API コントローラーの追加

このセクションでは、CRUD 操作 (作成、読み取り、更新、および削除) をサポートする Web API コントローラーを追加します。 コントローラーは Entity Framework を使用してデータベース層と通信します。

最初に、ファイルコントローラー/ファイルコントローラーの .cs を削除します。 このファイルには Web API コントローラーの例が含まれていますが、このチュートリアルでは必要ありません。

![](part-2/_static/image2.png)

次に、プロジェクトをビルドします。 Web API のスキャフォールディングは、リフレクションを使用してモデルクラスを検索するため、コンパイルされたアセンブリが必要です。

ソリューションエクスプローラーで、Controllers フォルダーを右クリックします。 **[追加]** を選択し、 **[コントローラー]** を選択します。

![](part-2/_static/image3.png)

**スキャフォールディングの追加** ダイアログで、Entity Framework アクションを含む Web API 2 コントローラー を選択します。 **[追加]** をクリックします。

![](part-2/_static/image4.png)

**[コントローラーの追加]** ダイアログで、次の操作を行います。

1. **[モデルクラス]** ドロップダウンで、`Author` クラスを選択します。 (ドロップダウンリストに表示されない場合は、プロジェクトをビルドしたことを確認してください)。
2. [Async controller アクションを使用する] をオンにします。
3. コントローラー名は &quot;AuthorsController&quot;のままにします。
4. **[データコンテキストクラス]** の横にある正符号 (+) ボタンをクリックします。

![](part-2/_static/image5.png)

**[新しいデータコンテキスト]** ダイアログボックスで、既定の名前をそのまま使用し、 **[追加]** をクリックします。

![](part-2/_static/image6.png)

**[追加]** をクリックして、 **[コントローラーの追加]** ダイアログを完了します。 このダイアログでは、2つのクラスがプロジェクトに追加されます。

- `AuthorsController` は、Web API コントローラーを定義します。 コントローラーは、クライアントが作成者の一覧に対して CRUD 操作を実行するために使用する REST API を実装します。
- `BookServiceContext` は、実行時にエンティティオブジェクトを管理します。これには、データベースからのデータを使用したオブジェクトの読み込み、変更の追跡、データベースへのデータの保持などが含まれます。 `DbContext` から継承します。

![](part-2/_static/image7.png)

この時点で、プロジェクトをもう一度ビルドします。 次に、同じ手順を実行して `Book` エンティティの API コントローラーを追加します。 今度は、モデルクラスの `Book` を選択し、データコンテキストクラスの既存の `BookServiceContext` クラスを選択します。 (新しいデータコンテキストを作成しないでください)。 **[追加]** をクリックしてコントローラーを追加します。

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> [前へ](part-1.md)
> [次へ](part-3.md)

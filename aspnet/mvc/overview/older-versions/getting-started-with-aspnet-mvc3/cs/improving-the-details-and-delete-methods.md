---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/improving-the-details-and-delete-methods
title: Details メソッドと Delete メソッドの改善C#() |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 3f42edd9-c5b8-4712-9055-970f7d38e350
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/improving-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 54d7be8fe1bff604ae9c9e9914d7c6426ab85c1c
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457506"
---
# <a name="improving-the-details-and-delete-methods-c"></a>Details メソッドと Delete メソッドの改善 (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../../getting-started/introduction/getting-started.md)入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。
> 
> 
> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。
> 
> - [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)
> 
> Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> このトピックには、ソースC#コードが含まれる Visual Web Developer プロジェクトが用意されています。 [バージョンをC#ダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。 Visual Basic を希望する場合は、このチュートリアルの[Visual Basic バージョン](../vb/intro-to-aspnet-mvc-3.md)に切り替えてください。

チュートリアルのこの部分では、自動的に生成された `Details` および `Delete` メソッドに対していくつかの機能強化を行います。 これらの変更は必要ありませんが、わずか数ビットのコードだけで、アプリケーションを簡単に拡張できます。

## <a name="improving-the-details-and-delete-methods"></a>Details メソッドと Delete メソッドの改善

`Movie` コントローラーをスキャフォールディングすると、ASP.NET MVC によって正常に機能したコードが生成されますが、わずかな変更を加えるだけでより堅牢にすることができます。

`Movie` コントローラーを開き、ムービーが見つからないときに `HttpNotFound` を返すことによって `Details` メソッドを変更します。 また、`Details` メソッドを変更して、渡された ID の既定値を設定する必要があります。 (このチュートリアルの[パート 6](examining-the-edit-methods-and-edit-view.md)では、`Edit` メソッドに対して同様の変更を行いました)。ただし、`HttpNotFound` メソッドが `ViewResult` オブジェクトを返さないため、`Details` メソッドの戻り値の型を `ViewResult` から `ActionResult`に変更する必要があります。 次の例は、変更された `Details` メソッドを示しています。

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample1.cs)]

Code First により、`Find` メソッドを使用してデータを簡単に検索できます。 メソッドに組み込まれている重要なセキュリティ機能は、コードがコードで何かを実行しようとする前に、`Find` メソッドがムービーを見つけたことを検証することです。 たとえば、ハッカーは、リンクによって作成された URL を `http://localhost:xxxx/Movies/Details/1` から `http://localhost:xxxx/Movies/Details/12345` (または実際のムービーを表さない他の値) に変更することによって、サイトにエラーを持ち込む可能性があります。 Null ムービーを確認しないと、データベースエラーが発生する可能性があります。

同様に、`Delete` および `DeleteConfirmed` メソッドを変更して、ID パラメーターの既定値を指定し、ムービーが見つからない場合に `HttpNotFound` を返すようにします。 `Movie` コントローラーで更新された `Delete` メソッドを次に示します。

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample2.cs)]

`Delete` メソッドはデータを削除しないことに注意してください。 GET 要求の応答で削除操作を実行すると (さらに言えば、編集操作、作成操作、データを変更するその他のあらゆる操作を実行すると)、セキュリティに穴が空きます。 詳細については、「Stephen Walther's blog entry ASP.NET MVC Tip #46」を参照してください。[削除リンクは、セキュリティホールを作成するため、使用しないで](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)ください。

データを削除する `HttpPost` メソッドの名前は「`DeleteConfirmed`」になり、HTTP POST メソッドに一意のシグネチャまたは名前が与えられます。 2 つのメソッド シグネチャは下の画像のようになります。

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample3.cs)]

共通言語ランタイム (CLR) では、オーバーロードされたメソッドに一意のシグネチャ (同じ名前、異なるパラメーターのリスト) が必要です。 ただし、ここでは2つの Delete メソッドが必要です。1つは GET 用で、もう1つは POST 用であり、両方とも同じシグネチャが必要です。 (いずれも、1 つの整数をパラメーターとして受け取る必要があります。)

これを並べ替えるために、いくつかのことを行うことができます。 1つは、メソッドに異なる名前を付けることです。 前の例で行ったようになりました。 ただし、これは小さな問題を引き起こします。ASP.NET が URL のセグメントをアクション メソッドに名前でマッピングします。メソッドの名前を変更すると、通常、ルーティングでそのメソッドが見つからなくなります。 この解決策はこの例で確認できます。`ActionName("Delete")` 属性を `DeleteConfirmed` メソッドに追加しています。 これにより、ルーティングシステムのマッピングが効果的に実行されるため、POST 要求の<em>/Delete/</em>が含まれている URL が `DeleteConfirmed` メソッドを見つけることができます。

同じ名前およびシグネチャを持つメソッドに関する問題を回避するもう1つの方法は、POST メソッドのシグネチャを意図的に変更して、未使用のパラメーターを含めることです。 たとえば、一部の開発者は、POST メソッドに渡される `FormCollection` パラメーター型を追加し、パラメーターを使用しないようにします。

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="wrapping-up"></a>折り返し

これで、SQL Server Compact データベースにデータを格納する完全な ASP.NET MVC アプリケーションが完成しました。 ムービーの作成、読み取り、更新、削除、検索を行うことができます。

![](improving-the-details-and-delete-methods/_static/image1.png)

この基本的なチュートリアルでは、コントローラーの作成、ビューへの関連付け、ハードコーディングされたデータの受け渡しを開始しました。 次に、データモデルを作成して設計しました。 Entity Framework Code First によってデータモデルからデータベースが作成され、ASP.NET MVC スキャフォールディングシステムによって基本的な CRUD 操作のアクションメソッドとビューが自動的に生成されます。 次に、ユーザーがデータベースを検索できる検索フォームを追加しました。 新しいデータ列が含まれるようにデータベースを変更し、この新しいデータを作成して表示する2つのページを更新しました。 `DataAnnotations` 名前空間の属性を使用してデータモデルをマークすることによって検証を追加しました。 結果の検証は、クライアントとサーバー上で実行されます。

アプリケーションをデプロイする場合は、まずローカルの IIS 7 サーバーでアプリケーションをテストすると便利です。 この[Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;)リンクを使用して、ASP.NET アプリケーションの IIS 設定を有効にすることができます。 次のデプロイリンクを参照してください。

- [ASP.NET 展開コンテンツマップ](https://msdn.microsoft.com/library/dd394698.aspx)
- [IIS 2.x を有効にする](https://blogs.msdn.com/b/rickandy/archive/2011/03/14/enabling-iis-7-x-on-windows-7-vista-sp1-windows-2008-windows-2008-r2.aspx)
- [Web アプリケーションプロジェクトの配置](https://msdn.microsoft.com/library/dd394698.aspx)

ここでは、ASP.NET MVC アプリケーションと[Mvc ミュージックストア](../../mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルのための Entity Framework データモデルを作成](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)する中間レベルに進み、 [MSDN の ASP.NET](https://msdn.microsoft.com/library/gg416514(VS.98).aspx)に関する記事をご覧ください。 ASP.NET MVC の詳細については、 [https://asp.net/mvc](https://asp.net/mvc)にある多くのビデオとリソースをご覧ください。 [ASP.NET MVC フォーラム](https://forums.asp.net/1146.aspx)は、質問するための優れた場所です。

機能を有効にご活用ください。

— Scott マン Selman ([http://hanselman.com](http://hanselman.com)と[@shanselman](http://twitter.com/shanselman) Twitter) と Rick Anderson [blogs.msdn.com/rickAndy](https://blogs.msdn.com/rickAndy)

> [!div class="step-by-step"]
> [[戻る]](adding-validation-to-the-model.md)

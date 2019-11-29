---
uid: web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-vb
title: アーキテクチャでデータをキャッシュする (VB) |Microsoft Docs
author: rick-anderson
description: 前のチュートリアルでは、プレゼンテーション層でキャッシュを適用する方法を学習しました。 このチュートリアルでは、階層型アーキテクチャを活用する方法について説明します。
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 5e189dd7-f4f9-4f28-9b3a-6cb7d392e9c7
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-vb
msc.type: authoredcontent
ms.openlocfilehash: dc991a205fa7e61f604bc0f26e9b24b3faefd3d3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607470"
---
# <a name="caching-data-in-the-architecture-vb"></a>アーキテクチャでデータをキャッシュする (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_59_VB.exe)または[PDF のダウンロード](caching-data-in-the-architecture-vb/_static/datatutorial59vb1.pdf)

> 前のチュートリアルでは、プレゼンテーション層でキャッシュを適用する方法を学習しました。 このチュートリアルでは、階層型アーキテクチャを利用してビジネスロジック層でデータをキャッシュする方法について説明します。 これを行うには、アーキテクチャを拡張してキャッシュレイヤーを含めます。

## <a name="introduction"></a>はじめに

前のチュートリアルで見たように、ObjectDataSource のデータのキャッシュは、いくつかのプロパティを設定するのと同じように簡単に行うことができます。 残念ながら、ObjectDataSource はプレゼンテーション層でキャッシュを適用し、キャッシュポリシーと ASP.NET ページを密に結合します。 階層型アーキテクチャを作成する理由の1つは、このような結合が壊れることを許可することです。 たとえば、ビジネスロジック層は、ASP.NET ページからビジネスロジックを分離し、データアクセス層はデータアクセスの詳細を分離します。 ビジネスロジックとデータアクセスの詳細の分離は、システムが読みやすく、保守が容易で、変更が柔軟な場合にも使用することをお勧めします。 また、ドメインの知識と労力の分担も可能です。プレゼンテーション層で作業する開発者は、自分の仕事を行うためにデータベースの詳細について理解している必要はありません。 プレゼンテーション層からキャッシュポリシーを分離すると、同様の利点が得られます。

このチュートリアルでは、キャッシュポリシーを使用する*キャッシュレイヤー* (短い場合は CL) を含めるようにアーキテクチャを拡張します。 キャッシュレイヤーには、`GetProducts()`、`GetProductsByCategoryID(categoryID)`などのメソッドを使用して製品情報へのアクセスを提供する `ProductsCL` クラスが含まれます。このクラスは、呼び出されると、最初にキャッシュからデータを取得しようとします。 キャッシュが空の場合、これらのメソッドは BLL の適切な `ProductsBLL` メソッドを呼び出します。これにより、DAL からデータが取得されます。 `ProductsCL` メソッドは、BLL から取得したデータをキャッシュしてから返します。

図1に示すように、CL はプレゼンテーション層とビジネスロジック層の間に配置されます。

![キャッシュレイヤー (CL) は、アーキテクチャにおけるもう1つのレイヤーです。](caching-data-in-the-architecture-vb/_static/image1.png)

**図 1**: キャッシュレイヤー (CL) は、アーキテクチャにおけるもう1つのレイヤーです。

## <a name="step-1-creating-the-caching-layer-classes"></a>手順 1: キャッシュレイヤークラスの作成

このチュートリアルでは、少数のメソッドのみを持つ1つのクラス `ProductsCL` を持つ非常に単純な CL を作成します。 アプリケーション全体の完全なキャッシュレイヤーを構築するには、`CategoriesCL`、`EmployeesCL`、および `SuppliersCL` クラスを作成し、BLL の各データアクセスまたは変更メソッドに対して、これらのキャッシュ層クラスのメソッドを提供する必要があります。 BLL と DAL と同様に、キャッシュレイヤーは、個別のクラスライブラリプロジェクトとして実装するのが理想的です。ただし、これは `App_Code` フォルダーのクラスとして実装します。

DAL クラスと BLL クラスの CL クラスをより明確に分離するには、`App_Code` フォルダーに新しいサブフォルダーを作成します。 ソリューションエクスプローラーで `App_Code` フォルダーを右クリックし、[新しいフォルダー] を選択して、新しいフォルダーに `CL`という名前を指定します。 このフォルダーを作成したら、`ProductsCL.vb`という名前の新しいクラスを追加します。

![CL という名前の新しいフォルダーと ProductsCL. vb という名前のクラスを追加します。](caching-data-in-the-architecture-vb/_static/image2.png)

**図 2**: `CL` という名前の新しいフォルダーとという名前のクラスを追加する `ProductsCL.vb`

`ProductsCL` クラスには、対応するビジネスロジックレイヤークラス (`ProductsBLL`) にあるものと同じデータアクセスおよび変更メソッドのセットを含める必要があります。 これらのメソッドをすべて作成するのではなく、ここでいくつかのコードを作成して、CL で使用されるパターンの感覚を得ます。 具体的には、手順 3. の `GetProducts()` と `GetProductsByCategoryID(categoryID)` のメソッドと、手順 4. の `UpdateProduct` オーバーロードを追加します。 残りの `ProductsCL` メソッド、`CategoriesCL`、`EmployeesCL`、および `SuppliersCL` クラスを、都合のよいときに追加できます。

## <a name="step-2-reading-and-writing-to-the-data-cache"></a>手順 2: データキャッシュの読み取りと書き込み

前のチュートリアルで説明した ObjectDataSource キャッシュ機能では、内部的に ASP.NET データキャッシュを使用して、BLL から取得したデータを格納します。 データキャッシュは、ASP.NET pages 分離コードクラスから、または web アプリケーションのアーキテクチャのクラスから、プログラムによってアクセスすることもできます。 ASP.NET ページの分離コードクラスからデータキャッシュの読み取りと書き込みを行うには、次のパターンを使用します。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample1.vb)]

[`Cache` クラス](https://msdn.microsoft.com/library/system.web.caching.cache.aspx)s [`Insert` メソッド](https://msdn.microsoft.com/library/system.web.caching.cache.insert.aspx)には、多くのオーバーロードがあります。 `Cache("key") = value` と `Cache.Insert(key, value)` は同義であり、有効期限が定義されていなくても、指定したキーを使用してキャッシュに項目を追加します。 通常は、キャッシュに項目を追加するときに、依存関係、時間ベースの有効期限、またはその両方の有効期限を指定します。 他の `Insert` メソッドのオーバーロードのいずれかを使用して、依存関係または時間ベースの有効期限情報を指定します。

キャッシュレイヤーのメソッドは、要求されたデータがキャッシュ内にあるかどうかを最初に確認し、存在する場合はそこから返す必要があります。 要求されたデータがキャッシュにない場合は、適切な BLL メソッドを呼び出す必要があります。 次のシーケンス図に示すように、戻り値はキャッシュしてから返される必要があります。

![キャッシュレイヤーのメソッドは、使用可能な場合は、キャッシュからデータを返します。](caching-data-in-the-architecture-vb/_static/image3.png)

**図 3**: キャッシュレイヤーのメソッドが、使用可能な場合はキャッシュからデータを返す

図3に示されているシーケンスは、次のパターンを使用して、CL クラスで実行されます。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample2.vb)]

ここで、 *type*はキャッシュ `Northwind.ProductsDataTable`に格納されているデータの種類です。たとえば、 *key*はキャッシュ項目を一意に識別するキーです。 指定した*キー*を持つ項目がキャッシュ内にない場合、*インスタンス*は `Nothing` され、データは適切な BLL メソッドから取得され、キャッシュに追加されます。 *インスタンス*には `Return instance` に達した時点で、キャッシュから、または BLL からプルしたデータへの参照が格納されます。

キャッシュからデータにアクセスするときは、必ず上記のパターンを使用してください。 次のパターンは、一見しても同じように見えますが、競合状態を示す微妙な違いがあります。 競合状態は散発的に見え、再現が困難なため、デバッグが困難です。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample3.vb)]

この2番目のコードスニペットの違いは、キャッシュされた項目への参照をローカル変数に格納するのではなく、条件付きステートメント*および*`Return`でデータキャッシュに直接アクセスすることです。 このコードに達したときに、`Cache("key")` が `Nothing`ではなく、`Return` ステートメントに到達する前に、システムがキャッシュから*キー*を見つけしていると仮定します。 このまれなケースでは、コードは、予期された型のオブジェクトではなく `Nothing` を返します。

> [!NOTE]
> データキャッシュはスレッドセーフであるため、単純な読み取りまたは書き込みのためにスレッドアクセスを同期する必要はありません。 ただし、アトミックである必要があるキャッシュ内のデータに対して複数の操作を実行する必要がある場合は、ロックまたはその他のメカニズムを実装してスレッドセーフを確保する必要があります。 詳細について[は、「ASP.NET Cache へのアクセスの同期](http://www.ddj.com/184406369)」を参照してください。

項目は、次のように[`Remove` メソッド](https://msdn.microsoft.com/library/system.web.caching.cache.remove.aspx)を使用して、プログラムによってデータキャッシュから削除できます。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample4.vb)]

## <a name="step-3-returning-product-information-from-theproductsclclass"></a>手順 3:`ProductsCL`クラスから製品情報を取得する

このチュートリアルでは、を使用して `ProductsCL` クラスから製品情報を返す2つのメソッドを実装します。 `GetProducts()` と `GetProductsByCategoryID(categoryID)`です。 ビジネスロジック層の `ProductsBL` クラスと同様に、CL の `GetProducts()` メソッドは、すべての製品に関する情報を `Northwind.ProductsDataTable` オブジェクトとして返します。一方、`GetProductsByCategoryID(categoryID)` は指定したカテゴリのすべての製品を返します。

次のコードは、`ProductsCL` クラスのメソッドの一部を示しています。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample5.vb)]

まず、クラスとメソッドに適用されている属性 `DataObject` と `DataObjectMethodAttribute` を確認します。 これらの属性は、ObjectDataSource s ウィザードに情報を提供し、ウィザードのステップでどのクラスとメソッドを表示するかを示します。 CL のクラスとメソッドは、プレゼンテーション層の ObjectDataSource からアクセスされるため、デザイン時のエクスペリエンスを向上させるためにこれらの属性を追加しました。 これらの属性とその効果の詳細については、「[ビジネスロジック層の作成](../introduction/creating-a-business-logic-layer-vb.md)」チュートリアルを参照してください。

`GetProducts()` メソッドと `GetProductsByCategoryID(categoryID)` メソッドでは、`GetCacheItem(key)` メソッドから返されたデータがローカル変数に割り当てられます。 `GetCacheItem(key)` メソッドは、後で確認します。指定された*キー*に基づいてキャッシュから特定の項目を返します。 このようなデータがキャッシュに見つからない場合は、対応する `ProductsBLL` クラスメソッドから取得され、`AddCacheItem(key, value)` メソッドを使用してキャッシュに追加されます。

`GetCacheItem(key)` および `AddCacheItem(key, value)` メソッドは、データキャッシュを使用して、値の読み取りと書き込みをそれぞれ行います。 `GetCacheItem(key)` メソッドは、この2つの方法よりも単純です。 単に、渡された*キー*を使用して Cache クラスから値を返します。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample6.vb)]

`GetCacheItem(key)` は、指定されたとおりに*キー*値を使用しませんが、代わりに、ProductsCache-を付加した*キー*を返す `GetCacheKey(key)` メソッドを呼び出します。 文字列 ProductsCache を保持する `MasterCacheKeyArray`も `AddCacheItem(key, value)` メソッドによって使用されます。これは、後で説明するようになります。

ASP.NET page s 分離コードクラスからは、`Page` クラス s [`Cache` プロパティ](https://msdn.microsoft.com/library/system.web.ui.page.cache.aspx)を使用してデータキャッシュにアクセスできます。手順 2. で説明したように、`Cache("key") = value`のような構文を使用できます。 アーキテクチャ内のクラスから、`HttpRuntime.Cache` または `HttpContext.Current.Cache`を使用してデータキャッシュにアクセスできます。 [Peter ジョンソン](https://weblogs.asp.net/pjohnson/default.aspx)のブログエントリ[HttpRuntime](https://weblogs.asp.net/pjohnson/httpruntime-cache-vs-httpcontext-current-cache)と、キャッシュに関する記事では、`HttpContext.Current`ではなく `HttpRuntime` を使用する場合のわずかなパフォーマンス上の利点について説明しています。そのため、`ProductsCL` は `HttpRuntime`を使用します。

> [!NOTE]
> クラスライブラリプロジェクトを使用してアーキテクチャを実装する場合は、 [`HttpRuntime`](https://msdn.microsoft.com/library/system.web.httpruntime.aspx)クラスと[`HttpContext`](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)クラスを使用するために、`System.Web` アセンブリへの参照を追加する必要があります。

項目がキャッシュ内で見つからない場合、`ProductsCL` クラスのメソッドは、BLL からデータを取得し、`AddCacheItem(key, value)` メソッドを使用してそのデータをキャッシュに追加します。 キャッシュに*値*を追加するには、60秒の有効期限を使用する次のコードを使用できます。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample7.vb)]

`DateTime.Now.AddSeconds(CacheDuration)` は、時間ベースの有効期限60秒を指定し、 [`System.Web.Caching.Cache.NoSlidingExpiration`](https://msdn.microsoft.com/library/system.web.caching.cache.noslidingexpiration(vs.80).aspx)はスライド式有効期限がないことを示します。 この `Insert` メソッドオーバーロードには、絶対有効期限とスライド式有効期限の両方の入力パラメーターがありますが、どちらか1つしか指定できません。 絶対時刻と時間範囲の両方を指定しようとすると、`Insert` メソッドによって `ArgumentException` 例外がスローされます。

> [!NOTE]
> 現在、この `AddCacheItem(key, value)` メソッドの実装にはいくつかの欠点があります。 これらの問題については、手順 4. で説明します。

## <a name="step-4-invalidating-the-cache-when-the-data-is-modified-through-the-architecture"></a>手順 4: アーキテクチャを使用してデータが変更されたときにキャッシュを無効にする

キャッシュレイヤーでは、データの取得方法と共に、データの挿入、更新、および削除のために、BLL と同じメソッドを提供する必要があります。 CL s のデータ変更メソッドは、キャッシュされたデータを変更するのではなく、BLL の対応するデータ変更メソッドを呼び出してから、キャッシュを無効にします。 前のチュートリアルで説明したように、これは、キャッシュ機能が有効になっており、その `Insert`、`Update`、または `Delete` メソッドが呼び出されたときに ObjectDataSource が適用される動作と同じです。

次の `UpdateProduct` オーバーロードは、データ変更メソッドを CL で実装する方法を示しています。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample8.vb)]

適切なデータ変更ビジネスロジックレイヤーメソッドが呼び出されますが、応答が返される前に、キャッシュを無効にする必要があります。 残念ながら、`ProductsCL` クラス s `GetProducts()` と `GetProductsByCategoryID(categoryID)` メソッドがそれぞれ異なるキーを使用してキャッシュに項目を追加するため、キャッシュを無効にするのは簡単ではありません。また、`GetProductsByCategoryID(categoryID)` メソッドによって、一意の*categoryID*ごとに異なるキャッシュ項目が追加されます。

キャッシュを無効にする場合は、`ProductsCL` クラスによって追加された可能性のある*すべて*の項目を削除する必要があります。 これは、`AddCacheItem(key, value)` メソッドでキャッシュに追加された各項目と*キャッシュの依存関係*を関連付けることによって実現できます。 一般に、キャッシュの依存関係は、キャッシュ内の別の項目、ファイルシステム上のファイル、または Microsoft SQL Server データベースのデータにすることができます。 依存関係が変更されるか、キャッシュから削除されると、関連付けられているキャッシュ項目がキャッシュから自動的に削除されます。 このチュートリアルでは、`ProductsCL` クラスによって追加されたすべての項目のキャッシュ依存関係として機能する追加の項目をキャッシュに作成します。 こうすることで、キャッシュの依存関係を削除するだけで、これらすべての項目をキャッシュから削除できます。

では、このメソッドを使用してキャッシュに追加された各項目が1つのキャッシュ依存関係に関連付けられるように、`AddCacheItem(key, value)` メソッドを更新します。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample9.vb)]

`MasterCacheKeyArray` は、1つの値 ProductsCache を保持する文字列配列です。 まず、キャッシュ項目がキャッシュに追加され、現在の日付と時刻が割り当てられます。 キャッシュ項目が既に存在する場合は、更新されます。 次に、キャッシュの依存関係が作成されます。 [`CacheDependency` クラス](https://msdn.microsoft.com/library/system.web.caching.cachedependency(VS.80).aspx)s コンストラクターには多くのオーバーロードがありますが、ここで使用されるコンストラクターには、2つの `String` 配列入力が必要です。 最初の1つは、依存関係として使用するファイルのセットを指定します。 ファイルベースの依存関係を使用しないため、最初の入力パラメーターには `Nothing` の値が使用されます。 2番目の入力パラメーターは、依存関係として使用するキャッシュキーのセットを指定します。 ここでは、1つの依存関係、`MasterCacheKeyArray`を指定します。 その後、`CacheDependency` が `Insert` メソッドに渡されます。

この変更を `AddCacheItem(key, value)`すると、invaliding は依存関係を削除するのと同じように簡単にキャッシュを解除できます。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample10.vb)]

## <a name="step-5-calling-the-caching-layer-from-the-presentation-layer"></a>手順 5: プレゼンテーション層からキャッシュ層を呼び出す

キャッシュレイヤーのクラスとメソッドを使用して、これらのチュートリアル全体で調査した手法を使用してデータを操作できます。 キャッシュされたデータを操作する方法を示すために、変更を `ProductsCL` クラスに保存し、`Caching` フォルダーの `FromTheArchitecture.aspx` ページを開き、GridView を追加します。 GridView s スマートタグから新しい ObjectDataSource を作成します。 ウィザードの最初のステップでは、`ProductsCL` クラスがドロップダウンリストのオプションの1つとして表示されます。

[ProductsCL クラスがビジネスオブジェクトのドロップダウンリストに含まれて ![](caching-data-in-the-architecture-vb/_static/image5.png)](caching-data-in-the-architecture-vb/_static/image4.png)

**図 4**: `ProductsCL` クラスはビジネスオブジェクトのドロップダウンリストに含まれています ([クリックすると、フルサイズの画像が表示](caching-data-in-the-architecture-vb/_static/image6.png)されます)

`ProductsCL`を選択したら、[次へ] をクリックします。 [選択] タブのドロップダウンリストには、`GetProducts()` と `GetProductsByCategoryID(categoryID)` の2つの項目があり、[更新] タブには唯一の `UpdateProduct` オーバーロードがあります。 [選択] タブで `GetProducts()` メソッドを選択し、[更新] タブで `UpdateProducts` メソッドを選択し、[完了] をクリックします。

[ProductsCL クラス s のメソッドがドロップダウンリストに表示され ![](caching-data-in-the-architecture-vb/_static/image8.png)](caching-data-in-the-architecture-vb/_static/image7.png)

**図 5**: `ProductsCL` クラス s のメソッドがドロップダウンリストに表示される ([クリックしてフルサイズのイメージを表示する](caching-data-in-the-architecture-vb/_static/image9.png))

ウィザードを完了すると、Visual Studio は ObjectDataSource s `OldValuesParameterFormatString` プロパティを `original_{0}` に設定し、適切なフィールドを GridView に追加します。 `OldValuesParameterFormatString` プロパティを既定値に戻して `{0}`を変更し、ページング、並べ替え、および編集をサポートするように GridView を構成します。 CL で使用される `UploadProducts` オーバーロードは、編集された製品名と価格のみを受け入れるため、これらのフィールドのみが編集可能になるように GridView を制限します。

前のチュートリアルでは、`ProductName`、`CategoryName`、および `UnitPrice` フィールドのフィールドを含む GridView を定義しています。 この書式設定と構造は自由にレプリケートできます。この場合、GridView および ObjectDataSource s 宣言マークアップは次のようになります。

[!code-aspx[Main](caching-data-in-the-architecture-vb/samples/sample11.aspx)]

この時点で、キャッシュレイヤーを使用するページがあります。 キャッシュの動作を確認するには、`ProductsCL` クラス s `GetProducts()` と `UpdateProduct` メソッドにブレークポイントを設定します。 ブラウザーでページにアクセスし、並べ替えとページングの際にコードをステップ実行して、キャッシュから取得されたデータを確認します。 次に、レコードを更新し、キャッシュが無効になっていることを確認します。これにより、データが GridView に再バインドされるときに、BLL から取得されます。

> [!NOTE]
> この記事に付属するダウンロードで提供されているキャッシュレイヤーは完全ではありません。 このクラスには、1つのクラス (`ProductsCL`) のみが含まれています。これは、いくつかのメソッドにのみ使用できます。 さらに、CL (`~/Caching/FromTheArchitecture.aspx`) を使用するのは1つの ASP.NET ページのみですが、他のすべてのページは BLL を直接参照しています。 アプリケーションで CL の使用を計画している場合、プレゼンテーション層からのすべての呼び出しは CL に送られる必要があります。そのためには、CL のクラスとメソッドが、プレゼンテーション層で現在使用されている BLL のクラスとメソッドをカバーしている必要があります。

## <a name="summary"></a>要約

キャッシュは ASP.NET 2.0 s SqlDataSource および ObjectDataSource コントロールと共にプレゼンテーション層で適用できますが、理想的なキャッシュの役割はアーキテクチャの別の層に委任されます。 このチュートリアルでは、プレゼンテーション層とビジネスロジック層の間に存在するキャッシュレイヤーを作成しました。 キャッシュレイヤーは、BLL に存在し、プレゼンテーション層から呼び出されるクラスとメソッドの同じセットを提供する必要があります。

このチュートリアルで説明したキャッシュレイヤーの例と前のチュートリアルでは、*リアクティブな読み込み*が示されていました。 リアクティブ読み込みでは、データの要求が行われ、そのデータがキャッシュにない場合にのみ、データがキャッシュに読み込まれます。 データをキャッシュに*事前に読み込む*こともできます。これは、実際に必要になる前にデータをキャッシュに読み込む技法です。 次のチュートリアルでは、アプリケーションの起動時に静的値をキャッシュに格納する方法について、事前読み込みの例を示します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>作成者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Teresa Murphy でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](caching-data-with-the-objectdatasource-vb.md)
> [次へ](caching-data-at-application-startup-vb.md)

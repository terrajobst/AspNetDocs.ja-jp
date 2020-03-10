---
uid: web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
title: アプリケーションの起動時にデータをC#キャッシュする () |Microsoft Docs
author: rick-anderson
description: どの Web アプリケーションでも、一部のデータは頻繁に使用され、一部のデータはあまり使用されません。 ASP.NET アプリケーション b のパフォーマンスを向上させることができます。
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 22ca8efa-7cd1-45a7-b9ce-ce6eb3b3ff95
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
msc.type: authoredcontent
ms.openlocfilehash: a0b55b0df1b7843120de284891e16178df23fabe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465790"
---
# <a name="caching-data-at-application-startup-c"></a>アプリケーションの起動時にデータをキャッシュする (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[[Download PDF]\(PDF をダウンロード\)](caching-data-at-application-startup-cs/_static/datatutorial60cs1.pdf)

> どの Web アプリケーションでも、一部のデータは頻繁に使用され、一部のデータはあまり使用されません。 頻繁に使用されるデータ (キャッシュと呼ばれます) を事前に読み込むことで、ASP.NET アプリケーションのパフォーマンスを向上させることができます。 このチュートリアルでは、プロアクティブな読み込みの1つの方法を示します。この方法では、アプリケーションの起動時にデータをキャッシュに読み込みます。

## <a name="introduction"></a>はじめに

前の2つのチュートリアルでは、プレゼンテーション層とキャッシュ層のデータのキャッシュについて説明しました。 [Objectdatasource を使用したデータのキャッシュ](caching-data-with-the-objectdatasource-cs.md)では、objectdatasource のキャッシュ機能を使用して、プレゼンテーション層にデータをキャッシュする方法を検討しました。 [アーキテクチャのデータをキャッシュ](caching-data-in-the-architecture-cs.md)することで、新しい個別のキャッシュレイヤーでキャッシュが検証されます。 これらのチュートリアルでは、どちらもデータキャッシュを使用した*リアクティブな読み込み*を使用していました。 リアクティブ読み込みでは、データが要求されるたびに、システムはまずキャッシュ内にあるかどうかを確認します。 そうでない場合は、データベースなどの元のソースからデータを取得し、キャッシュに格納します。 リアクティブ読み込みの主な利点は、実装が簡単になることです。 欠点の1つは、要求間での不均一なパフォーマンスです。 前のチュートリアルのキャッシュレイヤーを使用して製品情報を表示するページを想像してください。 このページに初めてアクセスしたとき、またはメモリの制約によってキャッシュデータが削除された後に初めてアクセスした場合、または指定した有効期限に達した場合は、データをデータベースから取得する必要があります。 そのため、これらのユーザーの要求は、キャッシュによって処理されるユーザーの要求よりも長くかかります。

*プロアクティブな読み込み*は、キャッシュされたデータを必要とする前に読み込むことによって、要求間でパフォーマンスを低下させる代替キャッシュ管理戦略を提供します。 通常、プロアクティブな読み込みでは、基になるデータが更新されたときに定期的にチェックされるか通知されるプロセスを使用します。 その後、キャッシュを更新して最新の状態に保ちます。 プロアクティブ読み込みは、基になるデータが低速データベース接続、Web サービス、またはその他の特に低速なデータソースから取得される場合に特に便利です。 ただし、このプロアクティブな読み込みには、変更を確認してキャッシュを更新するプロセスを作成、管理、および展開する必要があるため、実装がより困難になります。

プロアクティブな読み込みの別のフレーバーと、このチュートリアルで調査する型は、アプリケーションの起動時にキャッシュにデータを読み込みます。 この方法は、データベースルックアップテーブルのレコードなどの静的データをキャッシュする場合に特に便利です。

> [!NOTE]
> プロアクティブとリアクティブの読み込みの違い、および長所、短所、実装に関する推奨事項の一覧については、「 [.NET Framework アプリケーションのキャッシュアーキテクチャガイド](https://msdn.microsoft.com/library/ms978498.aspx)」の[キャッシュの内容の管理](https://msdn.microsoft.com/library/ms978503.aspx)に関するセクションを参照してください。

## <a name="step-1-determining-what-data-to-cache-at-application-startup"></a>手順 1: アプリケーションの起動時にキャッシュするデータを決定する

前の2つのチュートリアルで検証したリアクティブな読み込みを使用したキャッシュの例は、定期的に変更される可能性があり、生成に exorbitantly 時間がかかることのないデータでもうまく機能します。 ただし、キャッシュされたデータが変更されない場合、リアクティブな読み込みで使用される有効期限は余分になります。 同様に、キャッシュされているデータの生成に非常に長い時間がかかる場合、キャッシュが空であるという要求を持つユーザーは、基になるデータを取得する間に長時間待機する必要があります。 アプリケーションの起動時に生成に非常に長い時間がかかる静的データとデータをキャッシュすることを検討してください。

データベースには動的で頻繁に変化する多くの値がありますが、ほとんどの場合、静的なデータが大量にあります。 たとえば、ほぼすべてのデータモデルには、固定された一連の選択肢から特定の値を含む1つまたは複数の列があります。 `Patients` データベーステーブルには、`PrimaryLanguage` 列がある場合があります。この列の値のセットは、英語、スペイン語、フランス語、ロシア語、日本語などです。 多くの場合、これらの種類の列は*参照テーブル*を使用して実装されます。 文字列 English またはフランス語を `Patients` テーブルに格納するのではなく、一般的に2つの列 (一意の識別子と文字列の説明) を持つ2つのテーブルが作成されます。これには、可能な値ごとにレコードが含まれます。 `Patients` テーブルの `PrimaryLanguage` 列には、対応する一意の識別子が参照テーブルに格納されます。 図1では、患者 John Doe の主要言語は英語ですが、Ed ジョンソンはロシア語です。

![言語テーブルは、患者テーブルによって使用されるルックアップテーブルです。](caching-data-at-application-startup-cs/_static/image1.png)

**図 1**: `Languages` テーブルは `Patients` テーブルによって使用されるルックアップテーブルです。

新しい患者を編集したり作成したりするためのユーザーインターフェイスには、`Languages` テーブルのレコードによって設定される使用可能な言語のドロップダウンリストが含まれます。 キャッシュを使用しない場合、このインターフェイスにアクセスするたびに、システムによって `Languages` テーブルに対してクエリを実行する必要があります。 これは、参照テーブルの値が非常に頻繁に変更されるため、無駄が不要であり、不要です。

前のチュートリアルで検証したのと同じリアクティブ読み込み手法を使用して、`Languages` データをキャッシュできます。 ただし、リアクティブな読み込みでは、時間ベースの有効期限が使用されますが、これは静的なルックアップテーブルデータには必要ありません。 事後対応型の読み込みを使用したキャッシュは、キャッシュがまったくないことよりも優れていますが、アプリケーションの起動時に参照テーブルのデータをキャッシュに事前に読み込むことをお勧めします。

このチュートリアルでは、参照テーブルのデータとその他の静的な情報をキャッシュする方法について説明します。

## <a name="step-2-examining-the-different-ways-to-cache-data"></a>手順 2: データをキャッシュするさまざまな方法を調べる

さまざまな方法を使用して、ASP.NET アプリケーションで情報をプログラムでキャッシュすることができます。 前のチュートリアルでデータキャッシュを使用する方法については既に説明しました。 また、*静的メンバー*または*アプリケーションの状態*を使用して、オブジェクトをプログラムでキャッシュすることもできます。

クラスを使用する場合は、通常、クラスをインスタンス化してから、そのメンバーにアクセスできるようにする必要があります。 たとえば、ビジネスロジック層のクラスの1つからメソッドを呼び出すためには、まずクラスのインスタンスを作成する必要があります。

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample1.cs)]

*Somemethod*を呼び出したり、何かの*プロパティ*を使用したりする前に、まず、`new` キーワードを使用してクラスのインスタンスを作成する必要があります。 *Somemethod*とその他の*プロパティ*は、特定のインスタンスに関連付けられています。 これらのメンバーの有効期間は、関連付けられているオブジェクトの有効期間に関連付けられています。 一方、*静的メンバー*は、クラスの*すべて*のインスタンス間で共有される変数、プロパティ、およびメソッドであり、その結果、クラスの有効期間が設定されます。 静的メンバーは、キーワード `static`によって示されます。

静的メンバーに加えて、アプリケーションの状態を使用してデータをキャッシュすることもできます。 各 ASP.NET アプリケーションは、アプリケーションのすべてのユーザーとページで共有される名前と値のコレクションを保持します。 このコレクションには、 [`HttpContext` クラス](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)の[`Application` プロパティ](https://msdn.microsoft.com/library/system.web.httpcontext.application.aspx)を使用してアクセスし、次のように ASP.NET ページの分離コードクラスから使用できます。

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample2.cs)]

データキャッシュには、データをキャッシュするための豊富な API が用意されています。これにより、時間と依存関係ベースの expiries、キャッシュ項目の優先度などのメカニズムが提供されます。 静的メンバーとアプリケーションの状態を使用する場合、このような機能は、ページの開発者が手動で追加する必要があります。 ただし、アプリケーションの有効期間中、アプリケーションの起動時にデータをキャッシュする場合、データキャッシュの利点は議論です。 このチュートリアルでは、静的なデータをキャッシュする3つの手法をすべて使用するコードを見ていきます。

## <a name="step-3-caching-thesupplierstable-data"></a>手順 3:`Suppliers`テーブルデータをキャッシュする

日付に実装した Northwind データベーステーブルには、従来のルックアップテーブルは含まれていません。 この4つの Datatable は、値が非静的であるすべてのモデルテーブルに対して実装されています。 このチュートリアルでは、新しい DataTable を DAL に追加してから、新しいクラスとメソッドを BLL に追加するのに時間を費やすのではなく、`Suppliers` テーブルのデータが静的であると考えてみましょう。 このため、アプリケーションの起動時にこのデータをキャッシュすることができます。

開始するには、`CL` フォルダーに `StaticCache.cs` という名前の新しいクラスを作成します。

![CL フォルダーに StaticCache.cs クラスを作成する](caching-data-at-application-startup-cs/_static/image2.png)

**図 2**: `CL` フォルダーに `StaticCache.cs` クラスを作成する

このキャッシュからデータを返すメソッドだけでなく、スタートアップ時にデータを読み込むメソッドを追加する必要があります。

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample3.cs)]

上記のコードでは、静的メンバー変数 `suppliers`を使用して、`SuppliersBLL` クラスの `GetSuppliers()` メソッドの結果を保持します。これは、`LoadStaticCache()` メソッドから呼び出されます。 `LoadStaticCache()` メソッドは、アプリケーションの開始時に呼び出されることを意図しています。 このデータがアプリケーションの起動時に読み込まれると、supplier データを操作する必要があるすべてのページで、`StaticCache` クラスの `GetSuppliers()` メソッドを呼び出すことができます。 そのため、サプライヤーを取得するためのデータベースへの呼び出しは、アプリケーションの起動時に1回だけ行われます。

静的メンバー変数をキャッシュストアとして使用するのではなく、アプリケーションの状態またはデータキャッシュを使用することもできます。 次のコードは、アプリケーションの状態を使用するクラスを示しています。

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample4.cs)]

`LoadStaticCache()`では、supplier 情報はアプリケーション変数*キー*に格納されます。 これは、`GetSuppliers()`から適切な型 (`Northwind.SuppliersDataTable`) として返されます。 `Application["key"]`を使用して ASP.NET pages の分離コードクラスでアプリケーションの状態にアクセスできますが、アーキテクチャでは、現在の `HttpContext`を取得するために `HttpContext.Current.Application["key"]` を使用する必要があります。

同様に、次のコードに示すように、データキャッシュをキャッシュストアとして使用することもできます。

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample5.cs)]

時間ベースの有効期限なしでデータキャッシュに項目を追加するには、`System.Web.Caching.Cache.NoAbsoluteExpiration` と `System.Web.Caching.Cache.NoSlidingExpiration` の値を入力パラメーターとして使用します。 データキャッシュの `Insert` メソッドのこの特定のオーバーロードが選択され、キャッシュ項目の*優先順位*を指定できるようになりました。 優先順位は、使用可能なメモリが不足しているときにキャッシュからどの項目を清掃するかを決定するために使用されます。 ここでは、優先順位 `NotRemovable`を使用します。これにより、このキャッシュ項目は清掃されません。

> [!NOTE]
> このチュートリアルのダウンロードでは、静的メンバー変数の方法を使用して `StaticCache` クラスを実装します。 アプリケーションの状態とデータキャッシュの手法のコードについては、クラスファイルのコメントを参照してください。

## <a name="step-4-executing-code-at-application-startup"></a>手順 4: アプリケーションの起動時にコードを実行する

Web アプリケーションが初めて起動したときにコードを実行するには、`Global.asax`という名前の特別なファイルを作成する必要があります。 このファイルには、アプリケーション、セッション、および要求レベルのイベントのイベントハンドラーを含めることができます。ここでは、アプリケーションが起動するたびに実行されるコードを追加できます。

Web アプリケーションのルートディレクトリに `Global.asax` ファイルを追加します。そのためには、Visual Studio のソリューションエクスプローラーで web サイトプロジェクト名を右クリックし、[新しい項目の追加] を選択します。 [新しい項目の追加] ダイアログボックスで、グローバルアプリケーションクラスの項目の種類を選択し、[追加] ボタンをクリックします。

> [!NOTE]
> プロジェクトに既に `Global.asax` ファイルがある場合、[新しい項目の追加] ダイアログボックスにはグローバルアプリケーションクラスの項目の種類は表示されません。

[Web アプリケーションのルートディレクトリに global.asax ファイルを追加 ![には](caching-data-at-application-startup-cs/_static/image4.png)](caching-data-at-application-startup-cs/_static/image3.png)

**図 3**: Web アプリケーションのルートディレクトリに `Global.asax` ファイルを追加する ([クリックすると、フルサイズの画像が表示](caching-data-at-application-startup-cs/_static/image5.png)されます)

既定の `Global.asax` ファイルテンプレートには、サーバー側の `<script>` タグ内の5つのメソッドが含まれています。

- **`Application_Start`** は、web アプリケーションが最初に起動したときに実行されます。
- アプリケーションのシャットダウン時に **`Application_End`** が実行される
- 未処理の例外がアプリケーションに到達するたびに、 **`Application_Error`** が実行されます
- **`Session_Start`** は、新しいセッションが作成されたときに実行されます。
- セッションの有効期限が切れたとき、または破棄されたときに **`Session_End`** 実行する

`Application_Start` イベントハンドラーは、アプリケーションのライフサイクル中に1回だけ呼び出されます。 アプリケーションから ASP.NET リソースが最初に要求されたときにアプリケーションが起動し、アプリケーションが再起動されるまで実行が継続されます。そのためには、`/Bin` フォルダーの内容の変更、`Global.asax`の変更、`App_Code` フォルダー内の内容の変更、または `Web.config` ファイルの変更などが考えられます。 アプリケーションのライフサイクルの詳細については、 [「ASP.NET アプリケーションのライフサイクルの概要」](https://msdn.microsoft.com/library/ms178473.aspx)を参照してください。

これらのチュートリアルでは、`Application_Start` メソッドにコードを追加するだけで済むため、他のユーザーを自由に削除できます。 `Application_Start`では、`StaticCache` クラスの `LoadStaticCache()` メソッドを呼び出します。これにより、仕入先の情報が読み込まれ、キャッシュされます。

[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample6.aspx)]

これですべて完了です。 アプリケーションの起動時には、`LoadStaticCache()` メソッドによって、BLL から供給業者の情報が取得され、静的メンバー変数 (または、`StaticCache` クラスのを使用して終了した任意のキャッシュストア) に格納されます。 この動作を確認するには、`Application_Start` メソッドにブレークポイントを設定し、アプリケーションを実行します。 アプリケーションの開始時にブレークポイントがヒットすることに注意してください。 ただし、後続の要求では、`Application_Start` メソッドは実行されません。

[ブレークポイントを使用して Application_Start イベントハンドラーが実行されていることを確認 ![](caching-data-at-application-startup-cs/_static/image7.png)](caching-data-at-application-startup-cs/_static/image6.png)

**図 4**: ブレークポイントを使用して `Application_Start` イベントハンドラーが実行されていることを確認する ([クリックすると、フルサイズの画像が表示](caching-data-at-application-startup-cs/_static/image8.png)されます)

> [!NOTE]
> 最初にデバッグを開始したときに `Application_Start` ブレークポイントにヒットしない場合は、アプリケーションが既に起動していることが原因です。 `Global.asax` または `Web.config` ファイルを変更してアプリケーションを強制的に再起動してから、操作をやり直してください。 これらのファイルのいずれかの末尾に空白行を追加 (または削除) するだけで、アプリケーションをすばやく再起動できます。

## <a name="step-5-displaying-the-cached-data"></a>手順 5: キャッシュされたデータを表示する

この時点で、`StaticCache` クラスには、アプリケーションの起動時にキャッシュされ、`GetSuppliers()` メソッドを使用してアクセスできる supplier データのバージョンが含まれています。 プレゼンテーション層からこのデータを操作するには、ObjectDataSource を使用するか、ASP.NET ページの分離コードクラスから `StaticCache` クラスの `GetSuppliers()` メソッドをプログラムによって呼び出すことができます。 ObjectDataSource コントロールと GridView コントロールを使用して、キャッシュされた業者情報を表示する方法を見てみましょう。

まず、`Caching` フォルダーの [`AtApplicationStartup.aspx`] ページを開きます。 GridView をツールボックスからデザイナーにドラッグし、その `ID` プロパティを `Suppliers`に設定します。 次に、GridView のスマートタグから、`SuppliersCachedDataSource`という名前の新しい ObjectDataSource を作成します。 `StaticCache` クラスの `GetSuppliers()` メソッドを使用するように ObjectDataSource を構成します。

[StaticCache クラスを使用するように ObjectDataSource を構成 ![には](caching-data-at-application-startup-cs/_static/image10.png)](caching-data-at-application-startup-cs/_static/image9.png)

**図 5**: `StaticCache` クラスを使用するように ObjectDataSource を構成する ([クリックしてフルサイズのイメージを表示する](caching-data-at-application-startup-cs/_static/image11.png))

[GetSuppliers () メソッドを使用して、キャッシュされた仕入先データを取得 ![](caching-data-at-application-startup-cs/_static/image13.png)](caching-data-at-application-startup-cs/_static/image12.png)

**図 6**: `GetSuppliers()` メソッドを使用してキャッシュされた Supplier データを取得する ([クリックしてフルサイズの画像を表示する](caching-data-at-application-startup-cs/_static/image14.png))

ウィザードを完了すると、Visual Studio によって `SuppliersDataTable`の各データフィールドに対して BoundFields が自動的に追加されます。 GridView および ObjectDataSource の宣言型マークアップは、次のようになります。

[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample7.aspx)]

図7は、ブラウザーを使用して表示するときのページを示しています。 出力は、BLL の `SuppliersBLL` クラスからデータを取得したのと同じですが、`StaticCache` クラスを使用すると、アプリケーションの起動時にキャッシュされた仕入先データが返されます。 `StaticCache` クラスの `GetSuppliers()` メソッドにブレークポイントを設定して、この動作を確認できます。

[キャッシュされた仕入先データが GridView に表示される ![](caching-data-at-application-startup-cs/_static/image16.png)](caching-data-at-application-startup-cs/_static/image15.png)

**図 7**: キャッシュされた仕入先データが GridView に表示される ([クリックしてフルサイズのイメージを表示する](caching-data-at-application-startup-cs/_static/image17.png))

## <a name="summary"></a>まとめ

ほとんどのデータモデルには、通常、参照テーブルの形式で実装される、静的なデータが大量に含まれています。 この情報は静的であるため、この情報を表示する必要があるたびにデータベースに継続的にアクセスする理由はありません。 さらに、静的な性質上、データをキャッシュする場合、有効期限は不要です。 このチュートリアルでは、このようなデータを取得し、データキャッシュ、アプリケーションの状態、および静的メンバー変数にキャッシュする方法を説明しました。 この情報はアプリケーションの起動時にキャッシュされ、アプリケーションの有効期間中はキャッシュに残ります。

このチュートリアルと過去2つでは、時間ベースの expiries を使用するだけでなく、アプリケーションの有効期間中のデータのキャッシュについても説明しました。 ただし、データベースデータをキャッシュする場合は、時間ベースの有効期限が理想的な値よりも小さくなることがあります。 キャッシュを定期的にフラッシュするのではなく、基になるデータベースデータが変更された場合にのみ、キャッシュされた項目を削除することをお勧めします。 これは、次のチュートリアルで説明する SQL キャッシュ依存関係を使用することによって可能です。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Teresa Murphy と Zack Jones でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](caching-data-in-the-architecture-cs.md)
> [次へ](using-sql-cache-dependencies-cs.md)

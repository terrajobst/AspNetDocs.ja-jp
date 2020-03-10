---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
title: ASP.NET 4 Web アプリケーションでの Entity Framework 4.0 を使用したパフォーマンスの最大化 |Microsoft Docs
author: tdykstra
description: このチュートリアルシリーズは、Entity Framework 4.0 チュートリアルシリーズを使用してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 ...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 4e43455e-dfa1-42db-83cb-c987703f04b5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 5630200a1ad1d30f6d89b38e15179f15b699fa9f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439264"
---
# <a name="maximizing-performance-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>ASP.NET 4 Web アプリケーションでの Entity Framework 4.0 を使用したパフォーマンスの最大化

[Tom Dykstra](https://github.com/tdykstra)

> このチュートリアルシリーズは、 [Entity Framework 4.0 チュートリアルシリーズを使用](https://asp.net/entity-framework/tutorials#Getting%20Started)してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 前のチュートリアルを完了していない場合は、このチュートリアルの開始点として、作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)できます。 チュートリアルシリーズ全体で作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)することもできます。 チュートリアルについてご質問がある場合は、 [ASP.NET Entity Framework フォーラム](https://forums.asp.net/1227.aspx)に投稿することができます。

前のチュートリアルでは、同時実行の競合を処理する方法を説明しました。 このチュートリアルでは、Entity Framework を使用する ASP.NET web アプリケーションのパフォーマンスを向上させるためのオプションについて説明します。 パフォーマンスを最大化したり、パフォーマンスの問題を診断したりするためのいくつかの方法について説明します。

以下のセクションに記載されている情報は、さまざまなシナリオで役に立つ可能性があります。

- 関連データを効率的に読み込みます。
- ビューステートを管理します。

以下のセクションに記載されている情報は、パフォーマンスの問題が発生する個々のクエリがある場合に役立ちます。

- `NoTracking` merge オプションを使用します。
- LINQ クエリをプリコンパイルします。
- データベースに送信されたクエリコマンドを確認します。

次のセクションで説明する情報は、非常に大きなデータモデルを持つアプリケーションに役立つ可能性があります。

- ビューを事前に生成します。

> [!NOTE]
> Web アプリケーションのパフォーマンスは多くの要因の影響を受けます。これには、要求と応答のデータのサイズ、データベースクエリの速度、サーバーがキューに入れられる要求の数、サーバーがキューに入れられる要求の数、サービスの効率、クライアントスクリプトライブラリを使用している可能性があります。 アプリケーションでパフォーマンスが重要な場合、またはテストまたは経験によってアプリケーションのパフォーマンスが不十分であることが示された場合は、パフォーマンスチューニングのために通常のプロトコルに従う必要があります。 パフォーマンスのボトルネックが発生している場所を判断し、アプリケーション全体のパフォーマンスに最大の影響を与える領域に対処します。
> 
> このトピックでは、主に ASP.NET の Entity Framework のパフォーマンスを向上させる方法に焦点を当てています。 ここでの推奨事項は、データアクセスがアプリケーションのパフォーマンスボトルネックの1つであると判断した場合に役立ちます。 ただし、前述のように、ここで説明する方法は、一般的&quot; のベストプラクティス &quot;とは見なされません。その多くは、例外的な状況にのみ適しています。また、非常に具体的なパフォーマンスのボトルネックに対処するためにも適しています。

チュートリアルを開始するには、Visual Studio を起動し、前のチュートリアルで使用していた Contoso 大学 web アプリケーションを開きます。

## <a name="efficiently-loading-related-data"></a>関連データの効率的な読み込み

Entity Framework がエンティティのナビゲーションプロパティに関連データを読み込むには、いくつかの方法があります。

- *遅延読み込み*。 エンティティが最初に読み込まれるときに、関連データは取得されません。 ただし、ナビゲーション プロパティに初めてアクセスしようとすると、そのナビゲーション プロパティに必要なデータが自動的に取得されます。 この結果、複数のクエリがデータベースに送信されます。1つはエンティティ自体に対して、もう1つはエンティティの関連データを取得する必要があるときです。 

    [![Image05](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

*一括読み込み*。 エンティティが読み取られるときに、関連データがエンティティと共に取得されます。 これは通常、必要なデータをすべて取得する 1 つの結合クエリになります。 このチュートリアルで既に説明したように、`Include` メソッドを使用して一括読み込みを指定します。

[![Image07](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

- *明示的読み込み*。 これは、コード内の関連データを明示的に取得する点を除いて、遅延読み込みに似ています。ナビゲーションプロパティにアクセスしても、自動的には発生しません。 関連データは、コレクションのナビゲーションプロパティの `Load` メソッドを使用して手動で読み込むか、または1つのオブジェクトを保持するプロパティの reference プロパティの `Load` メソッドを使用します。 (たとえば、`PersonReference.Load` メソッドを呼び出して、`Department` エンティティの `Person` ナビゲーションプロパティを読み込みます)。

    [![Image06](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

遅延読み込みと明示的な読み込みは、すぐにプロパティ値を取得しないため、*遅延読み込み*とも呼ばれます。

遅延読み込みは、デザイナーによって生成されたオブジェクトコンテキストの既定の動作です。 オブジェクトコンテキストクラスを定義する*SchoolModel.Designer.cs*ファイルを開くと、3つのコンストラクターメソッドが見つかり、それぞれに次のステートメントが含まれています。

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

一般に、取得したすべてのエンティティに関連データが必要であることがわかっている場合は、一括読み込みで最高のパフォーマンスが得られます。これは、データベースに送信される単一のクエリは、通常、取得されたエンティティごとに個別のクエリよりも効率的であるためです。 一方、エンティティのナビゲーションプロパティにアクセスする頻度が低い場合、または少数のエンティティセットに対してのみアクセスする必要がある場合は、一括読み込みで必要以上のデータが取得されるため、遅延読み込みまたは明示的な読み込みの方が効率的です。

Web アプリケーションでは、関連するデータのニーズに影響を与えるユーザー操作がブラウザーで実行されるため、遅延読み込みの値が比較的小さくなることがあります。これは、ページをレンダリングしたオブジェクトコンテキストへの接続がないためです。 一方、コントロールをデータバインドする場合は、通常、必要なデータを把握しているため、通常は、各シナリオに適した方法に基づいて、一括読み込みまたは遅延読み込みを選択することをお勧めします。

また、オブジェクトコンテキストが破棄された後で、データバインドコントロールでエンティティオブジェクトを使用する場合もあります。 その場合、ナビゲーションプロパティの遅延読み込みの試行は失敗します。 次のエラーメッセージが表示されます。 &quot;`The ObjectContext instance has been disposed and can no longer be used for operations that require a connection.`&quot;

`EntityDataSource` コントロールは、既定で遅延読み込みを無効にします。 現在のチュートリアルで使用している `ObjectDataSource` コントロール (またはページコードからオブジェクトコンテキストにアクセスする場合) では、遅延読み込みを既定で無効にする方法がいくつかあります。 オブジェクトコンテキストをインスタンス化するときに無効にすることができます。 たとえば、次の行を `SchoolRepository` クラスのコンストラクターメソッドに追加できます。

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

Contoso 大学アプリケーションでは、コンテキストがインスタンス化されるたびにこのプロパティを設定する必要がないように、オブジェクトコンテキストによって遅延読み込みが自動的に無効になります。

*SchoolModel*データモデルを開き、デザイン画面をクリックします。次に、[プロパティ] ペインで、[**遅延読み込みを有効**にする] プロパティを `False`に設定します。 データモデルを保存して閉じます。

[![Image04](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

## <a name="managing-view-state"></a>ビューステートの管理

更新機能を提供するために、ページを表示するときに、ASP.NET web ページにエンティティの元のプロパティ値を格納する必要があります。 ポストバック処理中に、コントロールはエンティティの元の状態を再作成し、変更を適用して `SaveChanges` メソッドを呼び出す前に、エンティティの `Attach` メソッドを呼び出すことができます。 既定では、ASP.NET Web フォームデータコントロールは、ビューステートを使用して元の値を格納します。 ただし、ビューステートは、ブラウザーとの間で送受信されるページのサイズを大幅に増やすことができる非表示フィールドに格納されているため、パフォーマンスに影響する可能性があります。

ビューステートを管理する方法、またはセッション状態などの代替手段は Entity Framework に固有のものではないため、このチュートリアルでは詳しく説明しません。 詳細については、チュートリアルの最後にあるリンクを参照してください。

ただし、ASP.NET のバージョン4では、Web フォームアプリケーションのすべての ASP.NET 開発者が認識する必要がある、ビューステートを操作する新しい方法が提供されます。これは、`ViewStateMode` プロパティです。 この新しいプロパティは、ページレベルまたはコントロールレベルで設定できます。また、ページのビューステートを既定で無効にし、それを必要とするコントロールに対してのみ有効にすることができます。

パフォーマンスが重要なアプリケーションの場合は、常にページレベルでビューステートを無効にし、それを必要とするコントロールに対してのみ有効にすることをお勧めします。 Contoso 大学のページのビューステートのサイズは、この方法によって大幅に減少することはありませんが、そのしくみを確認するために、*教員の .aspx*ページに対して行います。 このページには、ビューステートが無効になっている `Label` コントロールなど、多くのコントロールが含まれています。 このページのコントロールでは、実際にはビューステートを有効にする必要がありません。 (`GridView` コントロールの `DataKeyNames` プロパティは、ポストバック間で管理する必要がある状態を指定しますが、これらの値は `ViewStateMode` プロパティの影響を受けないコントロールの状態で保持されます)。

現在、`Page` ディレクティブと `Label` コントロールのマークアップは、次の例のようになります。

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

次の変更を行います。

- `Page` ディレクティブに `ViewStateMode="Disabled"` を追加します。
- `Label` コントロールから `ViewStateMode="Disabled"` を削除します。

このマークアップは、次の例のようになります。

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

すべてのコントロールでビューステートが無効になりました。 ビューステートを使用する必要があるコントロールを後で追加する場合は、そのコントロールの `ViewStateMode="Enabled"` 属性を含めるだけで済みます。

## <a name="using-the-notracking-merge-option"></a>NoTracking マージオプションの使用

オブジェクトコンテキストがデータベース行を取得し、それらを表すエンティティオブジェクトを作成すると、既定では、オブジェクト状態マネージャーを使用してそれらのエンティティオブジェクトも追跡されます。 この追跡データはキャッシュとして機能し、エンティティを更新するときに使用されます。 通常、web アプリケーションには有効期間が短いオブジェクトコンテキストインスタンスがあるため、クエリは、読み取られる必要のないデータを返すことがよくあります。これは、読み取られたすべてのエンティティが再度使用されるか、または更新される前に、それらを読み取るオブジェクトコンテキストが破棄されるためです。

Entity Framework では、*マージオプション*を設定することによって、オブジェクトコンテキストでエンティティオブジェクトを追跡するかどうかを指定できます。 マージオプションは、個々のクエリまたはエンティティセットに対して設定できます。 エンティティセットに対して設定した場合、そのエンティティセットに対して作成されるすべてのクエリに対して、既定のマージオプションを設定することになります。

Contoso 大学アプリケーションでは、リポジトリからアクセスするエンティティセットの追跡は必要ありません。そのため、リポジトリクラスでオブジェクトコンテキストをインスタンス化するときに、これらのエンティティセットの `NoTracking` にマージオプションを設定できます。 (このチュートリアルでは、merge オプションを設定しても、アプリケーションのパフォーマンスに大きな影響はありません。 `NoTracking` オプションは、データ量の多い特定のシナリオでのみ監視可能なパフォーマンス向上を実現する可能性があります)。

DAL フォルダーで、 *SchoolRepository.cs*ファイルを開き、リポジトリがアクセスするエンティティセットのマージオプションを設定するコンストラクターメソッドを追加します。

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

## <a name="pre-compiling-linq-queries"></a>LINQ クエリのプリコンパイル

Entity Framework が、指定された `ObjectContext` インスタンスの有効期間内に Entity SQL クエリを初めて実行するときは、クエリのコンパイルに多少の時間がかかります。 コンパイルの結果がキャッシュされます。これは、クエリの後続の実行がはるかに高速になることを意味します。 LINQ クエリは同様のパターンに従います。ただし、クエリをコンパイルするために必要な作業の一部は、クエリが実行されるたびに実行されます。 つまり、LINQ クエリの場合、既定では、コンパイルのすべての結果がキャッシュされるわけではありません。

オブジェクトコンテキストの有効期間内に繰り返し実行することが予想される LINQ クエリがある場合は、LINQ クエリを初めて実行するときにコンパイルのすべての結果がキャッシュされるようにするコードを記述できます。

図として、`SchoolRepository` クラスの2つの `Get` メソッドに対してこれを実行します。1つはパラメーター (`GetInstructorNames` メソッド) を取らず、もう1つはパラメーター (`GetDepartmentsByAdministrator` メソッド) を必要とします。 これらのメソッドは、LINQ クエリではないため、実際にコンパイルする必要がなくなりました。

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

ただし、コンパイル済みのクエリを試すことができるように、次の LINQ クエリとして記述されているかのように続行します。

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

これらのメソッドのコードを上記のように変更し、アプリケーションを実行して、続行する前に動作することを確認できます。 ただし、次の手順は、事前にコンパイルされたバージョンを作成することに直接対応しています。

*DAL*フォルダーにクラスファイルを作成し、 *SchoolEntities.cs*という名前を付けて、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

このコードは、自動的に生成されたオブジェクトコンテキストクラスを拡張する部分クラスを作成します。 部分クラスには、`CompiledQuery` クラスの `Compile` メソッドを使用する2つのコンパイル済み LINQ クエリが含まれています。 また、クエリを呼び出すために使用できるメソッドも作成します。 このファイルを保存して閉じます。

次に、 *SchoolRepository.cs*で、コンパイルされたクエリを呼び出すように、リポジトリクラスの既存の `GetInstructorNames` および `GetDepartmentsByAdministrator` メソッドを変更します。

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

Department *.aspx*ページを実行して、以前と同じように動作することを確認します。 `GetInstructorNames` メソッドは、管理者 ドロップダウンリストを設定するために呼び出されます。 **更新** をクリックすると、複数の部門の管理者であるインストラクターがいないことを確認するために、`GetDepartmentsByAdministrator` メソッドが呼び出されます。

[![Image03](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

Contoso 大学アプリケーションで事前にコンパイルされたクエリは、その方法を確認するためにのみ使用できます。これは、パフォーマンスがある程度までになるためです。 LINQ クエリをプリコンパイルすると、コードに複雑さのレベルが追加されるため、アプリケーションのパフォーマンスのボトルネックを実際に表すクエリに対してのみ実行してください。

## <a name="examining-queries-sent-to-the-database"></a>データベースに送信されたクエリの調査

パフォーマンスの問題を調査しているときに、Entity Framework がデータベースに送信している SQL コマンドを正確に把握しておくと役立つ場合があります。 `IQueryable` オブジェクトを使用している場合は、`ToTraceString` メソッドを使用する方法があります。

*SchoolRepository.cs*で、次の例に一致するように `GetDepartmentsByName` メソッドのコードを変更します。

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.cs)]

`departments` 変数は、前の行の末尾にある `Where` メソッドによって `IQueryable` オブジェクトが作成されるため、`ObjectQuery` 型にのみキャストする必要があります。`Where` メソッドを使用しない場合、キャストは必要ありません。

`return` 行にブレークポイントを設定し、デバッガーで department *.aspx*ページを実行します。 ブレークポイントにヒットしたら、 **[ローカル]** ウィンドウで `commandText` 変数を調べ、テキストビジュアライザー ( **[値]** 列の虫眼鏡) を使用して、 **[テキストビジュアライザー]** ウィンドウに値を表示します。 次のコードから結果として得られた SQL コマンド全体を確認できます。

[![Image08](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

別の方法として、Visual Studio Ultimate の IntelliTrace 機能を使用すると、Entity Framework によって生成された SQL コマンドを表示して、コードを変更したり、ブレークポイントを設定したりする必要がなくなります。

> [!NOTE]
> 次の手順は、Visual Studio Ultimate がある場合にのみ実行できます。

`GetDepartmentsByName` メソッドで元のコードを復元した後、デバッガーで department *.aspx*ページを実行します。

Visual Studio で、 **[デバッグ]** メニュー、 **[intellitrace]** 、 **[intellitrace イベント]** の順に選択します。

[![Image11](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

**[IntelliTrace]** ウィンドウで、 **[すべて中断]** をクリックします。

[![Image12](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

**[IntelliTrace]** ウィンドウには、最近のイベントの一覧が表示されます。

[![Image09](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

**[ADO.NET]** 行をクリックします。 展開すると、コマンドテキストが表示されます。

[![Image10](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

コマンドテキスト文字列全体をクリップボードにコピーするには、 **[ローカル]** ウィンドウを使用します。

単純な `School` データベースよりも多くのテーブル、リレーションシップ、および列を含むデータベースを操作しているとします。 複数の `Join` 句を含む1つの `Select` ステートメントで必要なすべての情報を収集するクエリが複雑すぎるため、効率的に作業できなくなる場合があります。 その場合は、一括読み込みから明示的な読み込みに切り替えて、クエリを簡略化することができます。

たとえば、 *SchoolRepository.cs*の `GetDepartmentsByName` メソッドでコードを変更してみてください。 現在、このメソッドには、`Person` と `Courses` ナビゲーションプロパティの `Include` メソッドを持つオブジェクトクエリがあります。 次の例に示すように、`return` ステートメントを明示的な読み込みを実行するコードに置き換えます。

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

デバッガーで学科の *.aspx*ページを実行し、前と同じように **[IntelliTrace]** ウィンドウをもう一度確認します。 ここでは、1つのクエリがあったところで、長いシーケンスが表示されています。

[![Image13](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

最初の **[ADO.NET]** 行をクリックして、前に表示した複雑なクエリに何が起こったかを確認します。

[![Image14](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

部門からのクエリは、`Join` 句を使用しない単純な `Select` クエリになっていますが、その後に、元のクエリによって返された部門ごとに2つのクエリのセットを使用して、関連するコースと管理者を取得する個別のクエリが続きます。

> [!NOTE]
> 遅延読み込みを有効にしたままにした場合、ここに表示されるパターンは、同じクエリが何度も繰り返されるため、遅延読み込みによって発生する可能性があります。 一般的に回避するパターンは、プライマリテーブルのすべての行について、遅延読み込み関連データです。 1つの結合クエリが複雑すぎて効率的に処理できないことを確認していない場合は、通常、一括読み込みを使用するようにプライマリクエリを変更することで、パフォーマンスを向上させることができます。

## <a name="pre-generating-views"></a>生成前のビュー

`ObjectContext` オブジェクトが新しいアプリケーションドメインに最初に作成されると、Entity Framework によって、データベースへのアクセスに使用するクラスのセットが生成されます。 これらのクラスは*ビュー*と呼ばれ、非常に大きなデータモデルがある場合、これらのビューを生成すると、新しいアプリケーションドメインの初期化後にページの最初の要求に対して web サイトの応答が遅れることがあります。 実行時ではなく、コンパイル時にビューを作成することによって、この最初の要求の遅延を減らすことができます。

> [!NOTE]
> アプリケーションに非常に大きなデータモデルがない場合、またはデータモデルが大規模な場合に、IIS を再利用した後の最初のページ要求のみに影響するパフォーマンス上の問題を懸念していない場合は、このセクションをスキップできます。 ビューはアプリケーションドメインにキャッシュされるため、`ObjectContext` オブジェクトをインスタンス化するたびにビューの作成は行われません。 そのため、IIS でアプリケーションを頻繁にリサイクルしていない限り、事前に生成されたビューを使用すると、ページ要求の数が非常に少なくなります。

*Edmgen.exe*コマンドラインツールを使用するか、*テキストテンプレート変換ツールキット*(T4) テンプレートを使用して、ビューを事前に生成できます。 このチュートリアルでは、T4 テンプレートを使用します。

*DAL*フォルダーで、**テキストテンプレート**テンプレート ( **[インストールされたテンプレート]** の一覧の **[全般]** ノードの下にあります) を使用してファイルを追加し、 *SchoolModel.Views.tt*という名前を指定します。 ファイル内の既存のコードを次のコードに置き換えます。

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

このコードは、テンプレートと同じフォルダーに配置され、テンプレートファイルと同じ名前を持つ *.edmx*ファイルのビューを生成します。 たとえば、テンプレートファイルの名前が*SchoolModel.Views.tt*の場合、 *SchoolModel*という名前のデータモデルファイルが検索されます。

ファイルを保存し、**ソリューションエクスプローラー**でファイルを右クリックして、 **[カスタムツールの実行]** を選択します。

[![Image02](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

Visual Studio では、テンプレートに基づいて*SchoolModel.Views.cs*という名前のビューを作成するコードファイルが生成されます。 (テンプレートファイルを保存するとすぐに **[カスタムツールの実行]** を選択する前に、コードファイルが生成されていることに気付きます)。

[![Image01](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

これで、アプリケーションを実行し、以前と同じように動作することを確認できます。

事前に生成されたビューの詳細については、次のリソースを参照してください。

- [方法: ビューを事前に生成してクエリのパフォーマンスを向上](https://msdn.microsoft.com/library/bb896240.aspx)させるには、MSDN web サイトを参照してください。 `EdmGen.exe` コマンドラインツールを使用して、ビューを事前に生成する方法について説明します。
- Windows Server AppFabric カスタマーアドバイザリチームブログの[Entity Framework 4 で、プリコンパイル済み/生成済みのビューを使用してパフォーマンスを分離](https://blogs.msdn.com/b/appfabriccat/archive/2010/08/06/isolating-performance-with-precompiled-pre-generated-views-in-the-entity-framework-4.aspx)します。

このチュートリアルでは、Entity Framework を使用する ASP.NET web アプリケーションでのパフォーマンス向上の概要について説明します。 詳細については、次のリソースを参照してください。

- MSDN web サイトの[パフォーマンスに関する考慮事項 (Entity Framework)](https://msdn.microsoft.com/library/cc853327.aspx) 。
- [Entity Framework チームブログのパフォーマンス関連の投稿](https://blogs.msdn.com/b/adonet/archive/tags/performance/)。
- [EF のマージオプションとコンパイル](https://blogs.msdn.com/b/dsimmons/archive/2010/01/12/ef-merge-options-and-compiled-queries.aspx)されたクエリ。 コンパイル済みクエリの予期しない動作と、`NoTracking`などのマージオプションについて説明するブログ記事。 コンパイル済みのクエリを使用する場合、またはアプリケーションでマージオプションの設定を操作する場合は、まずこれを参照してください。
- [データとモデリングのカスタマーアドバイザリチームブログの Entity Framework 関連の投稿](https://blogs.msdn.com/b/dmcat/archive/tags/entity+framework/)。 コンパイルされたクエリに関する投稿を含み、Visual Studio 2010 Profiler を使用してパフォーマンスの問題を検出します。
- [非常に複雑なクエリのパフォーマンス向上に関するアドバイスを含むフォーラムスレッド Entity Framework](https://social.msdn.microsoft.com/Forums/adodotnetentityframework/thread/ffe8b2ab-c5b5-4331-8988-33a872d0b5f6)ます。
- [ASP.NET 状態管理に関する推奨事項](https://msdn.microsoft.com/library/z1hkazw7.aspx)。
- [Entity Framework と ObjectDataSource: カスタムページングを使用](http://geekswithblogs.net/Frez/articles/using-the-entity-framework-and-the-objectdatasource-custom-paging.aspx)します。 これらのチュートリアルで作成した ContosoUniversity アプリケーションを基にしたブログ投稿では、department*ページで*ページングを実装する方法を説明しています。

次のチュートリアルでは、バージョン4の新機能である Entity Framework のいくつかの重要な機能強化について確認します。

> [!div class="step-by-step"]
> [前へ](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
> [次へ](what-s-new-in-the-entity-framework-4.md)

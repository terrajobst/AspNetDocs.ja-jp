---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーションでのリポジトリと作業単位のパターンの実装 (9 件) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 18de9b125ee5d10795b9ce1a366918dadf4fc4e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434380"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a>ASP.NET MVC アプリケーションでのリポジトリと作業単位のパターンの実装 (9 件)

[Tom Dykstra](https://github.com/tdykstra)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。 チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。 チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。
> 
> > [!NOTE] 
> > 
> > 解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。 一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。 一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。

前のチュートリアルでは、継承を使用して、`Student` および `Instructor` エンティティクラスの冗長コードを減らしています。 このチュートリアルでは、CRUD 操作にリポジトリと作業単位パターンを使用するいくつかの方法について説明します。 前のチュートリアルと同様に、このチュートリアルでは、新しいページを作成するのではなく、既に作成したページに対するコードの動作方法を変更します。

## <a name="the-repository-and-unit-of-work-patterns"></a>リポジトリと作業単位のパターン

リポジトリと作業単位のパターンは、アプリケーションのデータアクセス層とビジネスロジック層の間に抽象レイヤーを作成することを目的としています。 これらのパターンを実装すると、データ ストアの変更からアプリケーションを隔離でき、自動化された単体テストやテスト駆動開発 (TDD) を円滑化できます。

このチュートリアルでは、エンティティ型ごとにリポジトリクラスを実装します。 `Student` エンティティ型については、リポジトリインターフェイスとリポジトリクラスを作成します。 コントローラーでリポジトリをインスタンス化する場合は、コントローラーがリポジトリインターフェイスを実装するオブジェクトへの参照を受け入れるように、インターフェイスを使用します。 コントローラーは、web サーバーで実行されると、Entity Framework と連携するリポジトリを受け取ります。 単体テストクラスで実行されているコントローラーは、メモリ内コレクションなど、テストのために簡単に操作できる方法で格納されているデータと連携するリポジトリを受け取ります。

このチュートリアルの後半では、複数のリポジトリと、`Course` コントローラーのエンティティ型の `Course` および `Department` の作業単位クラスを使用します。 作業単位クラスは、すべてのリポジトリで共有される単一のデータベースコンテキストクラスを作成することによって、複数のリポジトリの作業を調整します。 自動単体テストを実行できるようにする場合は、`Student` リポジトリの場合と同じように、これらのクラスのインターフェイスを作成して使用します。 ただし、このチュートリアルを簡単にするために、インターフェイスを使用せずにこれらのクラスを作成して使用します。

次の図は、リポジトリまたは作業単位のパターンをまったく使用しない場合と比較して、コントローラーとコンテキストクラス間のリレーションシップを概念化する方法の一例を示しています。

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

このチュートリアルシリーズでは単体テストを作成しません。 リポジトリパターンを使用する MVC アプリケーションでの TDD の概要については、「[チュートリアル: ASP.NET MVC での tdd の使用](https://msdn.microsoft.com/library/ff847525.aspx)」を参照してください。 リポジトリパターンの詳細については、次のリソースを参照してください。

- MSDN の[リポジトリパターン](https://msdn.microsoft.com/library/ff649690.aspx)。
- Entity Framework チームブログの[「Entity Framework 4.0 でリポジトリと作業単位のパターンを使用する](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx)」をご覧ください。
- ジュリー Lerman のブログで、[アジャイル Entity Framework 4 リポジトリ](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/)シリーズの投稿
- Dan Wahlin のブログで、この[アカウントを一目で HTML5/JQuery アプリケーションで作成](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx)できます。

> [!NOTE]
> リポジトリと作業単位パターンを実装するには、さまざまな方法があります。 作業単位クラスの有無にかかわらず、リポジトリクラスを使用できます。 すべてのエンティティ型に対して1つのリポジトリを実装することも、型ごとに1つのリポジトリを実装することもできます。 型ごとに1つのを実装する場合は、個別のクラス、ジェネリック基底クラスと派生クラス、または抽象基底クラスと派生クラスを使用できます。 リポジトリにビジネスロジックを含めることも、データアクセスロジックに限定することもできます。 また、エンティティセットの[Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)型ではなく、 [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx)インターフェイスを使用して、データベースコンテキストクラスに抽象レイヤーを構築することもできます。 このチュートリアルで示す抽象化レイヤーを実装する方法は、すべてのシナリオと環境について推奨するものではなく、考慮する必要がある1つのオプションです。

## <a name="creating-the-student-repository-class"></a>Student Repository クラスの作成

*DAL*フォルダーで、 *IStudentRepository.cs*という名前のクラスファイルを作成し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

このコードは、2つの read メソッド (すべての `Student` エンティティを返すメソッドと、ID によって1つの `Student` エンティティを検索するメソッド) を含む、一般的な CRUD メソッドのセットを宣言します。

*DAL*フォルダーで、 *StudentRepository.cs* file という名前のクラスファイルを作成します。 既存のコードを、`IStudentRepository` インターフェイスを実装する次のコードに置き換えます。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

データベースコンテキストはクラス変数で定義され、コンストラクターは呼び出し元のオブジェクトがコンテキストのインスタンスを渡すことを想定しています。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

リポジトリで新しいコンテキストをインスタンス化することもできますが、1つのコントローラーで複数のリポジトリを使用した場合は、それぞれが個別のコンテキストで終了します。 後で、`Course` コントローラーで複数のリポジトリを使用します。また、作業単位のクラスによって、すべてのリポジトリで同じコンテキストが使用されるかどうかを確認できます。

リポジトリは[IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx)を実装し、コントローラーで前に見たようにデータベースコンテキストを破棄します。その CRUD メソッドは、前に見たのと同じ方法でデータベースコンテキストを呼び出します。

## <a name="change-the-student-controller-to-use-the-repository"></a>リポジトリを使用するように学生コントローラーを変更する

*StudentController.cs*で、現在クラスにあるコードを次のコードに置き換えます。 変更が強調表示されます。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

コントローラーは、コンテキストクラスではなく、`IStudentRepository` インターフェイスを実装するオブジェクトのクラス変数を宣言するようになりました。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

既定の (パラメーターなしの) コンストラクターは、新しいコンテキストインスタンスを作成します。また、省略可能なコンストラクターによって、呼び出し元はコンテキストインスタンスを渡すことができます。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

(*依存関係の挿入*(di) を使用していた場合は、既定のコンストラクターは必要ありません。 di ソフトウェアによって、正しいリポジトリオブジェクトが常に提供されるためです)。

CRUD メソッドでは、リポジトリはコンテキストではなく呼び出されます。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

`Dispose` メソッドは、コンテキストではなくリポジトリを破棄するようになりました。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

サイトを実行し、 **[Students]** タブをクリックします。

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

このページは、リポジトリを使用するようにコードを変更した場合と同じように動作し、他の学生ページも同じように動作します。 ただし、コントローラーの `Index` メソッドがフィルター処理と順序付けを行う方法には、重要な違いがあります。 このメソッドの元のバージョンには、次のコードが含まれていました。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

更新された `Index` メソッドには、次のコードが含まれています。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

強調表示されたコードのみが変更されています。

コードの元のバージョンでは、`students` は `IQueryable` オブジェクトとして型指定されます。 `ToList`などのメソッドを使用してコレクションに変換されるまで、クエリはデータベースに送信されません。これは、インデックスビューが student モデルにアクセスするまで発生しません。 上記の元のコードの `Where` メソッドは、データベースに送信される SQL クエリの `WHERE` 句になります。 また、選択したエンティティのみがデータベースによって返されることを意味します。 ただし、`context.Students` を `studentRepository.GetStudents()`に変更すると、このステートメントの後にある `students` 変数は、データベース内のすべての学生を含む `IEnumerable` コレクションになります。 `Where` メソッドを適用した結果は同じになりますが、作業は、データベースではなく、web サーバー上のメモリで実行されます。 大量のデータを返すクエリの場合、これは非効率的になる可能性があります。

> [!TIP]
> 
> **IQueryable と IEnumerable**
> 
> 次に示すように、リポジトリを実装した後、**検索**ボックスに何かを入力しても、SQL Server に送信されたクエリは、検索条件を含まないため、すべての Student 行を返します。
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> このクエリでは、検索条件を認識せずにクエリが実行されたため、すべての学生データが返されます。 検索、検索条件の適用、ページング用のデータのサブセットの選択 (このケースでは3つの行のみを表示) の処理は、後で `ToPagedList` メソッドが `IEnumerable` コレクションで呼び出されたときにメモリ内で行われます。
> 
> 以前のバージョンのコードでは (リポジトリを実装する前)、`IQueryable` オブジェクトで `ToPagedList` が呼び出されたときに、検索条件が適用されるまで、クエリはデータベースに送信されません。
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> `IQueryable` オブジェクトで ToPagedList が呼び出されると、SQL Server に送信されるクエリによって検索文字列が指定されます。結果として、検索条件を満たす行だけが返されます。メモリ内でフィルター処理を行う必要はありません。
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> (次のチュートリアルでは、SQL Server に送信されたクエリを確認する方法について説明します)。

次のセクションでは、データベースでこの作業を実行することを指定できるようにするリポジトリメソッドを実装する方法について説明します。

これで、コントローラーと Entity Framework データベースコンテキストの間に抽象レイヤーが作成されました。 このアプリケーションで自動単体テストを実行する場合は、`IStudentRepository`を実装する単体テストプロジェクトで代替リポジトリクラスを作成でき*ます。* このモックリポジトリクラスは、コンテキストを呼び出してデータの読み取りと書き込みを行うのではなく、コントローラー関数をテストするためにインメモリコレクションを操作できます。

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a>汎用リポジトリと作業単位クラスを実装する

エンティティ型ごとにリポジトリクラスを作成すると、冗長なコードが大量に生成され、部分的な更新が発生する可能性があります。 たとえば、同じトランザクションの一部として、2つの異なるエンティティ型を更新する必要があるとします。 それぞれが別のデータベースコンテキストインスタンスを使用している場合は、成功する可能性があり、もう1つは失敗する可能性があります。 冗長なコードを最小限に抑える方法の1つとして、汎用リポジトリを使用し、すべてのリポジトリが同じデータベースコンテキストを使用する (つまり、すべての更新を調整する) ことを保証するには、作業単位クラスを使用する方法があります。

チュートリアルのこのセクションでは、`GenericRepository` クラスと `UnitOfWork` クラスを作成し、それらを `Course` コントローラーで使用して、`Department` と `Course` の両方のエンティティセットにアクセスします。 前に説明したように、チュートリアルのこの部分を単純にするために、これらのクラスのインターフェイスを作成しません。 ただし、TDD を容易にするために使用する場合は、通常、`Student` リポジトリと同じようにインターフェイスを使用して実装します。

### <a name="create-a-generic-repository"></a>汎用リポジトリを作成する

*DAL*フォルダーで、 *GenericRepository.cs*を作成し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

クラス変数は、データベースコンテキストと、リポジトリがインスタンス化されるエンティティセットに対して宣言されます。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

コンストラクターは、データベースコンテキストインスタンスを受け取り、エンティティセット変数を初期化します。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

`Get` メソッドは、ラムダ式を使用して、呼び出し元のコードがフィルター条件と結果を並べ替える列を指定できるようにします。また、文字列パラメーターを使用すると、呼び出し元は一括読み込みのためのナビゲーションプロパティのコンマ区切りリストを指定できます。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

コード `Expression<Func<TEntity, bool>> filter` は、呼び出し元が `TEntity` の型に基づいてラムダ式を提供し、この式がブール値を返すことを意味します。 たとえば、`Student` エンティティ型に対してリポジトリがインスタンス化されている場合、呼び出し元のメソッドのコードでは、`filter` パラメーターに対して `student => student.LastName == "Smith`&quot; を指定できます。

また、コード `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` は、呼び出し元がラムダ式を提供することも意味します。 ただし、この場合、式への入力は `TEntity` 型の `IQueryable` オブジェクトです。 式は、その `IQueryable` オブジェクトの順序付けされたバージョンを返します。 たとえば、`Student` エンティティ型に対してリポジトリがインスタンス化されている場合、呼び出し元のメソッドのコードでは、`orderBy` パラメーターの `q => q.OrderBy(s => s.LastName)` を指定できます。

`Get` メソッドのコードは、`IQueryable` オブジェクトを作成し、フィルター式がある場合はそれを適用します。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

次に、コンマ区切りのリストを解析した後、一括読み込み式を適用します。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

最後に、`orderBy` 式がある場合はそれを適用し、結果を返します。それ以外の場合は、順序付けられていないクエリの結果を返します。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

`Get` メソッドを呼び出すと、これらの関数のパラメーターを指定する代わりに、メソッドによって返される `IEnumerable` コレクションに対してフィルター処理や並べ替えを行うことができます。 ただし、並べ替えとフィルター処理は、web サーバー上のメモリで実行されます。 これらのパラメーターを使用して、作業が web サーバーではなくデータベースによって実行されるようにします。 別の方法としては、特定のエンティティ型の派生クラスを作成し、`GetStudentsInNameOrder` や `GetStudentsByName`などの特殊な `Get` メソッドを追加します。 ただし、複雑なアプリケーションでは、このような派生クラスや特殊なメソッドが多数発生する可能性があります。これは、保守作業がより多くなる可能性があります。

`GetByID`、`Insert`、および `Update` メソッドのコードは、非ジェネリックリポジトリで見たものと似ています。 (`Find` メソッドを使用して一括読み込みを実行することはできないため、`GetByID` シグネチャに一括読み込みパラメーターを指定することはできません。

`Delete` メソッドには、次の2つのオーバーロードが用意されています。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

これらのいずれかを使用すると、削除するエンティティの ID だけを渡すことができ、1つのエンティティインスタンスを受け取ります。 [同時実行の処理](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)に関するチュートリアルで説明したように、同時実行の処理では、追跡プロパティの元の値を含むエンティティインスタンスを受け取る `Delete` メソッドが必要です。

この汎用リポジトリは、一般的な CRUD 要件を処理します。 特定のエンティティ型に特別な要件 (より複雑なフィルター処理や順序付けなど) がある場合は、その型の追加のメソッドを持つ派生クラスを作成できます。

## <a name="creating-the-unit-of-work-class"></a>作業単位クラスの作成

作業単位クラスは、1つの目的を果たします。複数のリポジトリを使用するときに、1つのデータベースコンテキストを共有します。 これにより、作業単位が完了したら、そのコンテキストのインスタンスで `SaveChanges` メソッドを呼び出して、関連するすべての変更が調整されることを保証できます。 クラスが必要とするのは、`Save` メソッドと各リポジトリのプロパティです。 各リポジトリプロパティは、他のリポジトリインスタンスと同じデータベースコンテキストインスタンスを使用してインスタンス化されたリポジトリインスタンスを返します。

*DAL*フォルダーで、 *UnitOfWork.cs*という名前のクラスファイルを作成し、テンプレートコードを次のコードに置き換えます。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

このコードは、データベースコンテキストと各リポジトリのクラス変数を作成します。 `context` 変数の場合、新しいコンテキストがインスタンス化されます。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

各リポジトリプロパティは、リポジトリが既に存在するかどうかを確認します。 そうでない場合は、リポジトリがインスタンス化され、コンテキストインスタンスが渡されます。 その結果、すべてのリポジトリは同じコンテキストインスタンスを共有します。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

`Save` メソッドは、データベースコンテキストで `SaveChanges` を呼び出します。

クラス変数内のデータベースコンテキストをインスタンス化するクラスと同様に、`UnitOfWork` クラスは `IDisposable` を実装し、コンテキストを破棄します。

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a>UnitOfWork クラスとリポジトリを使用するようにコースコントローラーを変更する

*CourseController.cs*で現在使用しているコードを次のコードに置き換えます。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

このコードは、`UnitOfWork` クラスのクラス変数を追加します。 (ここでインターフェイスを使用していた場合は、ここで変数を初期化するのではなく、`Student` リポジトリの場合と同じように、2つのコンストラクターのパターンを実装します)。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

クラスの残りの部分では、`UnitOfWork` プロパティを使用してリポジトリにアクセスすることにより、データベースコンテキストへのすべての参照が適切なリポジトリへの参照に置き換えられます。 `Dispose` メソッドは、`UnitOfWork` インスタンスを破棄します。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

サイトを実行し、 **[コース]** タブをクリックします。

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

ページは変更前と同じように見えますが、他のコースページも同じように動作します。

## <a name="summary"></a>まとめ

これで、リポジトリと作業単位の両方のパターンが実装されました。 汎用リポジトリでは、メソッドパラメーターとしてラムダ式を使用しました。 これらの式を `IQueryable` オブジェクトと共に使用する方法の詳細については、MSDN ライブラリの「 [IQueryable (t) インターフェイス (system.string)](https://msdn.microsoft.com/library/bb351562.aspx) 」を参照してください。 次のチュートリアルでは、いくつかの高度なシナリオを処理する方法について学習します。

その他の Entity Framework リソースへのリンクについては、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [次へ](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)

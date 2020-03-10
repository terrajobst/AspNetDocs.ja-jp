---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: 'Entity Framework 4.0 と ObjectDataSource コントロールの使用、パート 2: ビジネスロジック層と単体テストの追加 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズは、Entity Framework 4.0 チュートリアルシリーズを使用してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 ...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: 24344cc33d7c26d7c408db26c0530ef2c708a7d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439954"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a>Entity Framework 4.0 と ObjectDataSource コントロールの使用、パート 2: ビジネスロジック層と単体テストの追加

[Tom Dykstra](https://github.com/tdykstra)

> このチュートリアルシリーズは、 [Entity Framework 4.0 チュートリアルシリーズを使用](https://asp.net/entity-framework/tutorials#Getting%20Started)してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 前のチュートリアルを完了していない場合は、このチュートリアルの開始点として、作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)できます。 チュートリアルシリーズ全体で作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)することもできます。 チュートリアルについてご質問がある場合は、 [ASP.NET Entity Framework フォーラム](https://forums.asp.net/1227.aspx)に投稿することができます。

前のチュートリアルでは、Entity Framework と `ObjectDataSource` コントロールを使用して n 層 web アプリケーションを作成しました。 このチュートリアルでは、ビジネスロジック層 (BLL) とデータアクセス層 (DAL) を分離した状態でビジネスロジックを追加する方法について説明します。また、BLL 用の自動化された単体テストを作成する方法についても説明します。

このチュートリアルでは、次のタスクを実行します。

- 必要なデータアクセスメソッドを宣言するリポジトリインターフェイスを作成します。
- リポジトリクラスにリポジトリインターフェイスを実装します。
- リポジトリクラスを呼び出してデータアクセス関数を実行するビジネスロジッククラスを作成します。
- `ObjectDataSource` コントロールを、リポジトリクラスではなくビジネスロジッククラスに接続します。
- 単体テストプロジェクトと、そのデータストアのメモリ内コレクションを使用するリポジトリクラスを作成します。
- ビジネスロジッククラスに追加するビジネスロジックの単体テストを作成し、テストを実行して失敗したことを確認します。
- ビジネスロジッククラスにビジネスロジックを実装し、単体テストを再実行して、合格したことを確認します。

前のチュートリアルで作成した department および*DepartmentsAdd*ページを操作し*ます。*

## <a name="creating-a-repository-interface"></a>リポジトリインターフェイスの作成

まず、リポジトリインターフェイスを作成します。

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)

*DAL*フォルダーで、新しいクラスファイルを作成し、 *ISchoolRepository.cs*という名前を付けて、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

このインターフェイスは、repository クラスで作成した CRUD (作成、読み取り、更新、削除) の各メソッドに対して1つのメソッドを定義します。

*SchoolRepository.cs*の `SchoolRepository` クラスで、このクラスが `ISchoolRepository` インターフェイスを実装することを示します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a>ビジネスロジッククラスの作成

次に、ビジネスロジッククラスを作成します。 これにより、`ObjectDataSource` コントロールによって実行されるビジネスロジックを追加できるようになります。ただし、これはまだ行われません。 現時点では、新しいビジネスロジッククラスは、リポジトリと同じ CRUD 操作のみを実行します。

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)

新しいフォルダーを作成し、 *BLL*という名前を指定します。 (実際のアプリケーションでは、ビジネスロジック層は通常、独立したプロジェクトであるクラスライブラリとして実装されますが、このチュートリアルを単純にするために、BLL クラスはプロジェクトフォルダーに保持されます)。

[ *BLL* ] フォルダーで、新しいクラスファイルを作成し、 *SchoolBL.cs*という名前を付けて、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

このコードは、前にリポジトリクラスで見たものと同じ CRUD メソッドを作成しますが、Entity Framework メソッドに直接アクセスするのではなく、リポジトリクラスのメソッドを呼び出します。

リポジトリクラスへの参照を保持するクラス変数は、インターフェイス型として定義され、リポジトリクラスをインスタンス化するコードは2つのコンストラクターに含まれています。 パラメーターなしのコンストラクターは、`ObjectDataSource` コントロールによって使用されます。 これにより、前に作成した `SchoolRepository` クラスのインスタンスが作成されます。 もう1つのコンストラクターは、ビジネスロジッククラスをインスタンス化するすべてのコードが、リポジトリインターフェイスを実装する任意のオブジェクトに渡すことを許可します。

Repository クラスと2つのコンストラクターを呼び出す CRUD メソッドにより、選択した任意のバックエンドデータストアでビジネスロジッククラスを使用できるようになります。 ビジネスロジッククラスは、呼び出し元のクラスがデータを永続化する方法を認識する必要はありません。 (これは、"*永続化無視*" と呼ばれることがよくあります)。これにより、単体テストが容易になります。これは、データを格納するためのメモリ内 `List` コレクションと同様に単純なものを使用するリポジトリ実装にビジネスロジッククラスを接続できるためです。

> [!NOTE]
> 技術的には、エンティティオブジェクトは、Entity Framework の `EntityObject` クラスを継承するクラスからインスタンス化されるため、永続化非依存とは見なされません。 完全な永続化の無視では、`EntityObject` クラスを継承するオブジェクトの代わりに、 *plain OLD CLR オブジェクト*または*pocos*を使用できます。 POCOs の使用は、このチュートリアルの範囲を超えています。 詳細については、MSDN web サイトの「[テストの容易性と Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx) 」を参照してください)。

これで、リポジトリではなくビジネスロジッククラスに `ObjectDataSource` コントロールを接続し、すべてが以前と同じように動作することを確認できます。

Department および*DepartmentsAdd*で、各 `TypeName="ContosoUniversity.DAL.SchoolRepository"` が `TypeName="ContosoUniversity.BLL.SchoolBL` *"に変更*されます。 (すべてに4つのインスタンスがあります)。

Department *.aspx*と*DepartmentsAdd*ページを実行して、以前と同じように動作することを確認します。

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)

## <a name="creating-a-unit-test-project-and-repository-implementation"></a>単体テストプロジェクトとリポジトリの実装の作成

**テストプロジェクト**テンプレートを使用してソリューションに新しいプロジェクトを追加し、`ContosoUniversity.Tests`という名前を指定します。

テストプロジェクトで、`System.Data.Entity` への参照を追加し、`ContosoUniversity` プロジェクトにプロジェクト参照を追加します。

これで、単体テストで使用するリポジトリクラスを作成できるようになりました。 このリポジトリのデータストアは、クラス内にあります。

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)

テストプロジェクトで、新しいクラスファイルを作成し、 *MockSchoolRepository.cs*という名前を付けて、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

このリポジトリクラスには、Entity Framework に直接アクセスするものと同じ CRUD メソッドがありますが、データベースではなくメモリ内の `List` コレクションを使用します。 これにより、テストクラスはビジネスロジッククラスの単体テストを簡単に設定および検証できます。

## <a name="creating-unit-tests"></a>単体テストの作成

**テスト**プロジェクトテンプレートによってスタブ単体テストクラスが作成されました。次のタスクでは、ビジネスロジッククラスに追加するビジネスロジックに対して単体テストメソッドを追加することによって、このクラスを変更します。

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)

Contoso 大学では、個々のインストラクターは1つの部門の管理者にしかできません。このルールを適用するには、ビジネスロジックを追加する必要があります。 まず、テストを追加し、テストを実行して失敗したことを確認します。 次に、コードを追加し、テストを再実行します。成功したかどうかを確認します。

*UnitTest1.cs*ファイルを開き、ContosoUniversity プロジェクトで作成したビジネスロジックとデータアクセス層の `using` ステートメントを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

`TestMethod1` メソッドを次のメソッドに置き換えます。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

`CreateSchoolBL` メソッドは、単体テストプロジェクト用に作成したリポジトリクラスのインスタンスを作成し、そのインスタンスをビジネスロジッククラスの新しいインスタンスに渡します。 次に、メソッドはビジネスロジッククラスを使用して、テストメソッドで使用できる3つの部門を挿入します。

テストメソッドは、他のユーザーが既存の部署と同じ管理者を持つ新しい部署を挿入しようとした場合、または他のユーザーが自分の ID に設定して部門の管理者を更新しようとした場合に、ビジネスロジッククラスが例外をスローすることを確認します。既に別の部門の管理者であるユーザー。

例外クラスをまだ作成していないため、このコードはコンパイルされません。 コンパイルするには、`DuplicateAdministratorException` を右クリックし、**生成**、**クラス** の順に選択します。

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)

これにより、テストプロジェクトにクラスが作成されます。このクラスは、メインプロジェクトで例外クラスを作成した後に削除できます。 とは、ビジネスロジックを実装したものです。

テストプロジェクトを実行します。 予想どおり、テストは失敗します。

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)

## <a name="adding-business-logic-to-make-a-test-pass"></a>テストパスを作成するためのビジネスロジックの追加

次に、別の部門の管理者である部署の管理者として設定できないビジネスロジックを実装します。 ビジネスロジック層から例外をスローし、ユーザーが部署を編集し、既に管理者であるユーザーを選択した後に **[更新]** をクリックした場合に、プレゼンテーション層でキャッチします。 (ページを表示する前に、既に管理者であることを示すドロップダウンリストから講師を削除することもできますが、ここではビジネスロジックレイヤーを使用することを目的としています)。

まず、ユーザーが複数の部門の管理者を作成しようとしたときにスローされる例外クラスを作成します。 メインプロジェクトで、[ *BLL* ] フォルダーに新しいクラスファイルを作成し、 *DuplicateAdministratorException.cs*という名前を付けて、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

次に、前の手順でテストプロジェクトで作成した一時*DuplicateAdministratorException.cs*ファイルを、コンパイルできるように削除します。

メインプロジェクトで、 *SchoolBL.cs*ファイルを開き、検証ロジックを含む次のメソッドを追加します。 (コードは、後で作成するメソッドを参照します)。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

別の部門が既に同じ管理者を持っているかどうかを確認するために `Department` エンティティを挿入または更新するときに、このメソッドを呼び出します。

このコードは、メソッドを呼び出して、挿入または更新されるエンティティと同じ `Administrator` プロパティ値を持つ `Department` エンティティをデータベースで検索します。 見つかった場合、コードは例外をスローします。 挿入または更新するエンティティに `Administrator` 値がない場合、検証チェックは必要ありません。更新中にメソッドが呼び出され、見つかった `Department` エンティティが更新される `Department` エンティティと一致する場合、例外はスローされません。

`Insert` および `Update` メソッドから新しいメソッドを呼び出します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

*ISchoolRepository.cs*で、新しいデータアクセスメソッドに次の宣言を追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

*SchoolRepository.cs*で、次の `using` ステートメントを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

*SchoolRepository.cs*で、次の新しいデータアクセスメソッドを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

このコードは、指定された管理者を持つ `Department` エンティティを取得します。 1つの部門のみが検索されます (存在する場合)。 ただし、データベースには制約が組み込まれていないため、複数の部門が見つかった場合の戻り値の型はコレクションです。

既定では、オブジェクトコンテキストは、データベースからエンティティを取得するときに、オブジェクト状態マネージャーでエンティティを追跡します。 `MergeOption.NoTracking` パラメーターは、このクエリに対してこの追跡が行われないことを指定します。 この操作が必要なのは、更新しようとしているエンティティがクエリで返される可能性があるためです。そのエンティティをアタッチすることはできません。 たとえば、department *. .aspx*ページで履歴部門を編集し、管理者を変更しないままにした場合、このクエリは履歴部門を返します。 `NoTracking` が設定されていない場合、オブジェクトコンテキストでは、オブジェクト状態マネージャーに History department エンティティが既に存在します。 次に、ビューステートから再作成された履歴部署エンティティをアタッチすると、オブジェクトコンテキストによって `"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`という例外がスローされます。

(`MergeOption.NoTracking`を指定する代わりに、このクエリに対してのみ新しいオブジェクトコンテキストを作成することもできます。 新しいオブジェクトコンテキストには独自のオブジェクト状態マネージャーがあるため、`Attach` メソッドを呼び出すときに競合が発生することはありません。 新しいオブジェクトコンテキストでは、メタデータとデータベース接続が元のオブジェクトコンテキストと共有されるため、この代替アプローチのパフォーマンスが低下することは少なくありません。 ただし、ここに示す方法では `NoTracking` オプションが導入されており、他のコンテキストでも便利です。 `NoTracking` オプションの詳細については、このシリーズの後のチュートリアルで説明します)。

テストプロジェクトで、新しいデータアクセスメソッドを*MockSchoolRepository.cs*に追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

このコードでは、LINQ を使用して、`ContosoUniversity` プロジェクトリポジトリが LINQ to Entities に使用するのと同じデータ選択を実行します。

テストプロジェクトを再度実行します。 今回はテストに合格します。

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)

## <a name="handling-objectdatasource-exceptions"></a>ObjectDataSource 例外の処理

`ContosoUniversity` プロジェクト*で、department ページを*実行し、部門の管理者を別の部門の管理者に変更してみます。 (このチュートリアルで追加したのは、データベースに無効なデータが事前に読み込まれているためです)。次のサーバーエラーページが表示されます。

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)

この種類のエラーページを表示しないようにするには、エラー処理コードを追加する必要があります。 Department *.aspx*を開き、`DepartmentsObjectDataSource`の `OnUpdated` イベントのハンドラーを指定します。 `ObjectDataSource` 開始タグは、次の例のようになります。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

*Departments.aspx.cs*で、次の `using` ステートメントを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

`Updated` イベントに対して次のハンドラーを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

`ObjectDataSource` コントロールは、更新を実行しようとしたときに例外をキャッチした場合、イベント引数 (`e`) の例外をこのハンドラーに渡します。 ハンドラーのコードは、例外が管理者の重複する例外であるかどうかを確認します。 そうである場合、コードは、表示する `ValidationSummary` コントロールのエラーメッセージを含むバリデーターコントロールを作成します。

ページを実行し、2つの部門の管理者をもう一度作成します。 今回は、`ValidationSummary` コントロールによってエラーメッセージが表示されます。

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)

*DepartmentsAdd*ページに同様の変更を加えます。 *DepartmentsAdd*で、`DepartmentsObjectDataSource`の `OnInserted` イベントのハンドラーを指定します。 結果のマークアップは、次の例のようになります。

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

*DepartmentsAdd.aspx.cs*で、同じ `using` ステートメントを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

次のイベントハンドラーを追加します。

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

これで、 *DepartmentsAdd.aspx.cs*ページをテストして、1人のユーザーが複数の部門の管理者になる試みも正しく処理していることを確認できます。

このチュートリアルでは、Entity Framework で `ObjectDataSource` コントロールを使用するためのリポジトリパターンの実装の概要について説明します。 リポジトリパターンとテストの容易性の詳細については、MSDN ホワイトペーパー「[テストの容易性と Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx)」を参照してください。

次のチュートリアルでは、並べ替えとフィルター処理の機能をアプリケーションに追加する方法について説明します。

> [!div class="step-by-step"]
> [前へ](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
> [次へ](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)

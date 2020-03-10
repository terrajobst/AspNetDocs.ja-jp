---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: Entity Framework 4.0 | の新機能Microsoft Docs
author: tdykstra
description: このチュートリアルシリーズは、Entity Framework 4.0 チュートリアルシリーズを使用してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 ...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 29d2bd61e8361b130e7b9415dad4fe1d5b847945
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522148"
---
# <a name="whats-new-in-the-entity-framework-40"></a>Entity Framework 4.0 の新機能

[Tom Dykstra](https://github.com/tdykstra)

> このチュートリアルシリーズは、Entity Framework チュートリアルシリーズ[を使用](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)してはじめにによって作成された Contoso 大学 web アプリケーションに基づいています。 前のチュートリアルを完了していない場合は、このチュートリアルの開始点として、作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)できます。 チュートリアルシリーズ全体で作成した[アプリケーションをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)することもできます。 チュートリアルについてご質問がある場合は、 [ASP.NET Entity Framework フォーラム](https://forums.asp.net/1227.aspx)に投稿することができます。

前のチュートリアルでは、Entity Framework を使用する web アプリケーションのパフォーマンスを最大化するための方法をいくつか紹介しました。 このチュートリアルでは、Entity Framework のバージョン4で最も重要な新機能の一部を紹介し、すべての新機能について詳しく説明しているリソースへのリンクを示します。 このチュートリアルで強調表示されている機能には、次のものがあります。

- 外部キーの関連付け。
- ユーザー定義の SQL コマンドを実行しています。
- モデルファースト開発。
- POCO のサポート。

さらに、このチュートリアルでは、Entity Framework の次のリリースで導入されている機能である*コードファースト開発*について簡単に紹介します。

チュートリアルを開始するには、Visual Studio を起動し、前のチュートリアルで使用していた Contoso 大学 web アプリケーションを開きます。

## <a name="foreign-key-associations"></a>外部キーの関連付け

Entity Framework のバージョン3.5 にはナビゲーションプロパティが含まれていますが、データモデルの外部キープロパティが含まれていませんでした。 たとえば、`StudentGrade` テーブルの `CourseID` 列と `StudentID` 列は、`StudentGrade` エンティティから除外されます。

[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)

このアプローチの理由は、厳密に言えば、外部キーは物理的な実装の詳細であり、概念データモデルに属していないためです。 ただし、外部キーに直接アクセスできる場合は、コード内のエンティティを使用する方が、実際には簡単です。

データモデルの外部キーによってコードが簡略化される方法の例については、 *DepartmentsAdd*ページを使用せずにコードを記述する方法を検討してください。 `Department` エンティティの `Administrator` プロパティは、`Person` エンティティ内の `PersonID` に対応する外部キーです。 新しい部門と管理者の間の関連付けを確立するために必要なのは、データバインドコントロールの `ItemInserting` イベントハンドラーで `Administrator` プロパティの値を設定することだけでした。

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

データモデルに外部キーがない場合は、エンティティがエンティティセットに追加される前にエンティティ自体への参照を取得するために、データバインドコントロールの `ItemInserting` イベントではなく、データソースコントロールの `Inserting` イベントを処理します。 この参照があれば、次の例に示すようなコードを使用して関連付けを確立します。

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

[外部キーの関連付けに関する](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx)Entity Framework チームのブログ記事でわかるように、コードの複雑さの違いがかなり大きくなる場合もあります。 単純なコードを作成するために、概念データモデルで実装の詳細を使用する必要があるユーザーのニーズを満たすために、Entity Framework には、データモデルに外部キーを含めるオプションが用意されています。

Entity Framework 用語では、外部キーをデータモデルに含める場合、外部キーの*関連付け*を使用していて、外部キーを除外する場合は、独立した*関連付け*を使用しています。

## <a name="executing-user-defined-sql-commands"></a>ユーザー定義の SQL コマンドの実行

以前のバージョンの Entity Framework では、独自の SQL コマンドをすぐに作成して実行する簡単な方法はありませんでした。 Entity Framework 動的に生成された SQL コマンドを使用するか、ストアドプロシージャを作成して関数としてインポートする必要がありました。 バージョン4では、クエリをデータベースに直接渡すことが簡単になるように、`ExecuteStoreQuery` メソッドと `ExecuteStoreCommand` メソッドが `ObjectContext` クラスに追加されています。

Contoso 大学の管理者が、ストアドプロシージャを作成してデータモデルにインポートするプロセスを実行しなくても、データベースで一括変更を実行できるようにするとします。 最初の要求は、データベース内のすべてのコースのクレジット数を変更できるページを対象としています。 Web ページでは、`Course` のすべての行の `Credits` 列の値を乗算するために使用する数値を入力できるようにする必要があります。

*UpdateCredits*マスターページを使用する新しいページを作成*し、と*いう名前を指定します。 次に、`Content2`という名前の `Content` コントロールに次のマークアップを追加します。

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

このマークアップは、ユーザーが乗数値を入力できる `TextBox` コントロール、コマンドを実行するためにクリックする `Button` コントロール、および影響を受ける行の数を示す `Label` コントロールを作成します。

*UpdateCredits.aspx.cs*を開き、次の `using` ステートメントと、ボタンの `Click` イベントのハンドラーを追加します。

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

このコードは、テキストボックスの値を使用して SQL `Update` コマンドを実行し、ラベルを使用して、影響を受ける行の数を表示します。 ページを実行する前*に、course ページを*実行して、一部のデータの "前" の画像を取得します。

[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)

*UpdateCredits*を実行し、乗数として「10」と入力して、 **[実行]** をクリックします。

[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)

もう一度*course ページを*実行して、変更されたデータを確認します。

[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)

(クレジットの数を元の値に戻す場合は、 *UpdateCredits.aspx.cs*  で `Credits * {0}` を `Credits / {0}` に変更し、ページを再実行します。その際、「10」と入力します。

コードで定義したクエリの実行の詳細については、「[方法: データソースに対してコマンドを直接実行する](https://msdn.microsoft.com/library/ee358769.aspx)」を参照してください。

## <a name="model-first-development"></a>モデルファースト開発

これらのチュートリアルでは、まずデータベースを作成し、次にデータベースの構造に基づいてデータモデルを生成しました。 Entity Framework 4 では、代わりにデータモデルから開始し、データモデル構造に基づいてデータベースを生成できます。 データベースがまだ存在しないアプリケーションを作成する場合、モデル優先のアプローチを使用すると、アプリケーションに対して概念的に理にかなったエンティティとリレーションシップを作成できますが、物理的な実装の詳細について心配する必要はありません. (ただし、これは開発の初期段階でのみ当てはまります。 最終的には、データベースが作成され、実稼働データが含まれるようになり、モデルから再作成するのは実用的ではなくなります。この時点で、データベース優先のアプローチに戻ります)。

チュートリアルのこのセクションでは、単純なデータモデルを作成し、そこからデータベースを生成します。

**ソリューションエクスプローラー**で、[ *DAL* ] フォルダーを右クリックし、 **[新しい項目の追加]** を選択します。 **[新しい項目の追加]** ダイアログボックスの **[インストールされたテンプレート]** で **[データ]** を選択し、 **[ADO.NET Entity Data Model]** テンプレートを選択します。 新しいファイルに*AlumniAssociationModel*という名前を指定し、 **[追加]** をクリックします。

[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)

Entity Data Model ウィザードが起動します。 **[モデルの内容の選択]** ステップで、空の **[モデル]** を選択し、 **[完了]** をクリックします。

[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)

**Entity Data Model デザイナー**が開き、空のデザインサーフェイスが表示されます。 **エンティティ**項目を**ツールボックス**からデザインサーフェイスにドラッグします。

[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)

エンティティ名を `Entity1` から `Alumnus`に変更し、`Id` プロパティ名を `AlumnusId`に変更して、`Name`という名前の新しいスカラープロパティを追加します。 新しいプロパティを追加するには、`Id` 列の名前を変更した後に Enter キーを押すか、エンティティを右クリックして **[スカラープロパティの追加]** を選択します。 新しいプロパティの既定の種類は `String`です。この単純なデモンストレーションでは問題ありませんが、もちろん、 **[プロパティ]** ウィンドウでデータ型などを変更できます。

同じ方法で別のエンティティを作成し、`Donation`という名前を指定します。 `Id` プロパティを `DonationId` に変更し、`DateAndAmount`という名前のスカラープロパティを追加します。

[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)

これら2つのエンティティ間の関連付けを追加するには、`Alumnus` エンティティを右クリックし、 **[追加]** をクリックして、 **[アソシエーション]** を選択します。

[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)

**[関連付けの追加]** ダイアログボックスの既定値は、必要なものです (一対多、ナビゲーションプロパティを含める、外部キーを含む)。そのため、[ **OK]** をクリックします。

[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)

デザイナーによって、関連行と外部キープロパティが追加されます。

[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)

これで、データベースを作成する準備が整いました。 デザイン画面を右クリックし、 **[モデルからデータベースを生成]** を選択します。

[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)

これにより、データベース生成ウィザードが起動します。 (エンティティがマップされていないことを示す警告が表示される場合は、その時点でこれらのエンティティを無視してかまいません)。

**[データ接続の選択]** ステップで、 **[新しい接続]** をクリックします。

[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)

**[接続プロパティ]** ダイアログボックスで、ローカル SQL Server Express インスタンスを選択し、データベースに `AlumniAssociation`名前を指定します。

[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)

データベースを作成するかどうかを確認するメッセージが表示されたら、[**はい]** をクリックします。 **[データ接続の選択]** ステップが再び表示されたら、 **[次へ]** をクリックします。

**[概要と設定]** 手順で、 **[完了]** をクリックします。

[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)

データ定義言語 (DDL) コマンドを含む *.sql*ファイルが作成されますが、コマンドはまだ実行されていません。

[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)

[はじめにチュートリアルシリーズの最初のチュートリアルで](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)`School` データベースを作成したときと同じように、 **SQL Server Management Studio**などのツールを使用してスクリプトを実行し、テーブルを作成します。 (データベースをダウンロードしていない場合)。

`School` モデルを使用した場合と同じように、web ページで `AlumniAssociation` データモデルを使用できるようになりました。 これを試すには、いくつかのデータをテーブルに追加し、データを表示する web ページを作成します。

**サーバーエクスプローラー**を使用して、`Alumnus` テーブルと `Donation` テーブルに次の行を追加します。

[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)

*Alumni*という名前の新しい web ページを作成*し、そのマスターページ*を使用します。 `Content2`という名前の `Content` コントロールに次のマークアップを追加します。

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

このマークアップは、入れ子になった `GridView` コントロールを作成し、alumni 名を表示するための外側のコントロールと、寄付された日付と金額を表示するための内部1を作成します。

*Alumni.aspx.cs*を開きます。 データアクセス層の `using` ステートメントと、外側の `GridView` コントロールの `RowDataBound` イベントのハンドラーを追加します。

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

このコードは、現在の行の `Alumnus` エンティティの `Donations` ナビゲーションプロパティを使用して、内部 `GridView` コントロールをバインドします。

ページを実行します。

[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)

(注: このページはダウンロード可能なプロジェクトに含まれていますが、機能させるには、ローカル SQL Server Express インスタンスにデータベースを作成する必要があります。このデータベースは、 *App\_Data*フォルダーに *.mdf*ファイルとして含まれていません)。

Entity Framework のモデル優先機能の使用方法の詳細については、 [Entity Framework 4 の「model-first](https://msdn.microsoft.com/data/ff830362.aspx)」を参照してください。

## <a name="poco-support"></a>POCO サポート

ドメイン駆動設計手法を使用する場合は、ビジネスドメインに関連するデータと動作を表すデータクラスを設計します。 これらのクラスは、データを格納 (永続化) するために使用される特定のテクノロジに依存しないようにする必要があります。つまり、永続化を*意識*する必要はありません。 また、単体テストプロジェクトでは、テストに最も便利な永続化テクノロジを使用できるため、永続化によってクラスを簡単に単体テストできるように無視こともできます。 以前のバージョンの Entity Framework では、エンティティクラスが `EntityObject` クラスを継承する必要があり、Entity Framework 固有の機能が多数含まれているため、永続性の無視が限定的にサポートされていました。

Entity Framework 4 では、`EntityObject` クラスから継承しないため、永続化を意識しないエンティティクラスを使用する機能が導入されています。 Entity Framework のコンテキストでは、このようなクラスは通常、 *plain OLD CLR オブジェクト*(POCO または pocos) と呼ばれます。 POCO クラスは手動で作成できます。また、Entity Framework によって提供されるテキストテンプレート変換ツールキット (T4) テンプレートを使用して、既存のデータモデルに基づいて自動的に生成することもできます。

Entity Framework での POCOs の使用の詳細については、次のリソースを参照してください。

- [POCO エンティティの使用](https://msdn.microsoft.com/library/dd456853.aspx)。 これは、POCOs の概要である MSDN ドキュメントであり、より詳細な情報が記載されている他のドキュメントへのリンクがあります。
- [チュートリアル: Entity Framework の POCO テンプレート](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx)これは、Entity Framework 開発チームからのブログ投稿であり、POCOs に関する他のブログ記事へのリンクがあります。

## <a name="code-first-development"></a>コードファースト開発

Entity Framework 4 の POCO サポートでも、データモデルを作成し、エンティティクラスをデータモデルにリンクする必要があります。 Entity Framework の次のリリースには、 *code first 開発*と呼ばれる機能が含まれています。 この機能を使用すると、データモデルデザイナーまたはデータモデルの XML ファイルを使用しなくても、独自の POCO クラスで Entity Framework を使用できます。 (したがって、このオプションも*コードのみ*と呼ばれていました。*コード 1*と*コードのみ*が同じ Entity Framework 機能を参照しています)。

コード優先アプローチを使用した開発の詳細については、次のリソースを参照してください。

- [Entity Framework 4 でのコードファースト開発](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx)。 これは、Scott Guthrie によるコードファースト開発の導入によるブログ投稿です。
- [Entity Framework 開発チームのブログ-タグ付きコードのみを投稿する](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [Entity Framework 開発チームのブログ-タグ付き Code First の投稿](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [MVC ミュージックストアチュートリアル-パート 4: モデルとデータアクセス](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [MVC 3 でのはじめに-パート 4: Entity Framework コードファースト開発](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

さらに、Contoso 大学アプリケーションと同様のアプリケーションを構築する新しい MVC コードファーストチュートリアルは、2011の spring で公開される予定です[https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)

## <a name="more-information"></a>詳細情報

ここでは、Entity Framework の新機能の概要と、Entity Framework チュートリアルシリーズの続きを説明します。 ここでは説明されていない Entity Framework 4 の新機能の詳細については、次のリソースを参照してください。

- [ADO.NET の新機能](https://msdn.microsoft.com/library/ex6y04yf.aspx)Entity Framework のバージョン4の新機能に関する MSDN トピック。
- [Entity Framework 4 のリリースの発表](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx)Entity Framework 開発チームのブログ投稿では、バージョン4の新機能について説明しています。

> [!div class="step-by-step"]
> [[戻る]](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)

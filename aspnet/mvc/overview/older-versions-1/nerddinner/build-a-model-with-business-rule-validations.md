---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: ビジネスルール検証を使用してモデルを構築する |Microsoft Docs
author: microsoft
description: 手順 3. では、データベースのクエリと更新の両方に使用できるモデルを作成する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 6ebf1b71c089229ba9139ff7dc788b8978724046
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435580"
---
# <a name="build-a-model-with-business-rule-validations"></a>ビジネス ルール検証でモデルをビルドする

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法について説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順3です。
> 
> 手順 3. では、データベースのクエリと更新の両方に使用できるモデルを作成する方法を示します。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-3-building-the-model"></a>手順 3: モデルを作成する

モデルビューコントローラーフレームワークでは、"モデル" という用語は、アプリケーションのデータを表すオブジェクトと、検証とビジネスルールを統合するための対応するドメインロジックを指します。 このモデルは、多くの点で MVC ベースのアプリケーションの "ハート" と呼ばれています。このモデルの動作は、後ほど根本的に左右されます。

ASP.NET MVC フレームワークは、任意のデータアクセステクノロジの使用をサポートしており、開発者は、LINQ to Entities、LINQ to SQL、NHibernate、LLBLGen Pro、SubSonic、、または生の ADO のようなモデルを実装するために、さまざまな豊富な .NET データオプションから選択できます。NET Datareader またはデータセット。

このアプリケーションでは、LINQ to SQL を使用して、データベースの設計に厳密に対応する単純なモデルを作成し、カスタム検証ロジックとビジネスルールを追加します。 次に、アプリケーションの他の部分からデータ永続化の実装を抽象化するのに役立つリポジトリクラスを実装します。これにより、簡単に単体テストを実行できるようになります。

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ to SQL は、.NET 3.5 の一部として出荷される ORM (オブジェクトリレーショナルマッパー) です。

LINQ to SQL を使用すると、コードに対して使用できる .NET クラスにデータベーステーブルを簡単にマップできます。 このアプリケーションでは、このアプリケーションを使用して、データベース内のディナーテーブルと RSVP テーブルをディナーおよび RSVP クラスにマップします。 ディナーテーブルと RSVP テーブルの列は、ディナークラスと RSVP クラスのプロパティに対応しています。 各ディナーおよび RSVP オブジェクトは、データベース内のディナーテーブルまたは RSVP テーブル内の個別の行を表します。

LINQ to SQL を使用すると、SQL ステートメントを手動で作成して、データベースデータでディナーおよび RSVP オブジェクトを取得および更新する必要がなくなります。 代わりに、ディナークラスと RSVP クラス、データベースとの間のマッピング、およびそれらの間のリレーションシップを定義します。 次に、操作と使用時に実行時に使用する適切な SQL 実行ロジックの生成が LINQ to SQL によって行われます。

VB の LINQ 言語サポートを使用して、 C#データベースからディナーおよび RSVP オブジェクトを取得する表現力のあるクエリを記述することができます。 これにより、記述する必要があるデータコードの量が最小限に抑えられ、本当にクリーンなアプリケーションを作成できるようになります。

### <a name="adding-linq-to-sql-classes-to-our-project"></a>プロジェクトへの LINQ to SQL クラスの追加

まず、プロジェクト内の "モデル" フォルダーを右クリックし、[**新しい項目の&gt;追加**] メニューコマンドを選択します。

![](build-a-model-with-business-rule-validations/_static/image1.png)

[新しい項目の追加] ダイアログボックスが表示されます。 "Data" カテゴリによってフィルター処理を行い、その中に "LINQ to SQL Classes" テンプレートを選択します。

![](build-a-model-with-business-rule-validations/_static/image2.png)

項目に "" という名前を指定し、[追加] ボタンをクリックします。 Visual Studio は、次のように、モデルのディレクトリにある .dbml ファイルを追加し、LINQ to SQL オブジェクトリレーショナルデザイナーを開きます。

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>LINQ to SQL を使用したデータモデルクラスの作成

LINQ to SQL を使用すると、既存のデータベーススキーマからデータモデルクラスをすばやく作成できます。 これを行うには、サーバーエクスプローラーで [データベース] を開き、モデル化するテーブルを選択します。

![](build-a-model-with-business-rule-validations/_static/image4.png)

テーブルを LINQ to SQL デザイナー画面にドラッグすることができます。 LINQ to SQL この操作を実行すると、テーブルのスキーマ (データベーステーブルの列にマップされたクラスプロパティを含む) を使用して、ディナーおよび RSVP クラスが自動的に作成されます。

![](build-a-model-with-business-rule-validations/_static/image5.png)

既定では、データベーススキーマに基づいてクラスを作成するときに、LINQ to SQL デザイナーはテーブル名と列名を自動的に "複数化" します。 たとえば、上の例の "ディナー" テーブルは "ディナー" クラスになりました。 このクラスの名前付けは、モデルを .NET の名前付け規則と一貫性のあるものにするために役立ちます。また、通常は、デザイナーを使用して適切に修正することをお勧めします (多数のテーブルを追加する場合は特に)。 デザイナーが生成するクラスまたはプロパティの名前が気に入らない場合は、いつでもオーバーライドして任意の名前に変更することができます。 これを行うには、デザイナー内のエンティティまたはプロパティ名をインラインで編集するか、プロパティグリッドを使用して変更します。

既定では、LINQ to SQL デザイナーによってテーブルの主キー/外部キーのリレーションシップも検査され、作成される異なるモデルクラス間に既定の "リレーションシップの関連付け" が自動的に作成されます。 たとえば、ディナーテーブルと RSVP テーブルを LINQ to SQL デザイナーにドラッグした場合、その2つの間の一対多リレーションシップの関連付けは、RSVP テーブルにディナーテーブルへの外部キーがあるという事実に基づいて推定されます (これは、デザイナー):

![](build-a-model-with-business-rule-validations/_static/image6.png)

上記の関連付けにより、厳密に型指定された "ディナー" プロパティが、開発者が特定の RSVP に関連付けられているディナーにアクセスするために使用できる、RSVP クラスに追加さ LINQ to SQL ます。 また、ディナークラスに "RSVPs" コレクションプロパティが含まれるようになります。これにより、開発者は特定のディナーに関連付けられた RSVP オブジェクトを取得および更新できます。

新しい RSVP オブジェクトを作成してディナーの RSVPs collection に追加すると、Visual Studio 内の intellisense の例が表示されます。 LINQ to SQL によって、ディナーオブジェクトに "RSVPs" コレクションが自動的に追加されていることに注意してください。

![](build-a-model-with-business-rule-validations/_static/image7.png)

ここでは、RSVPs コレクションに RSVP オブジェクトを追加することにより、ディナーとデータベース内の RSVP 行との間に外部キーのリレーションシップを関連付けるように LINQ to SQL 指示します。

![](build-a-model-with-business-rule-validations/_static/image8.png)

デザイナーがテーブルの関連付けをモデル化または名前付けした方法が気に入らない場合は、それをオーバーライドできます。 デザイナー内の [association] 矢印をクリックし、プロパティグリッドを使用してプロパティにアクセスし、名前の変更、削除、または変更を行います。 ただし、このアプリケーションでは、既定のアソシエーションルールは、開発中のデータモデルクラスに対して適切に機能します。既定の動作を使用するだけで済みます。

### <a name="nerddinnerdatacontext-class"></a>のクラス

Visual Studio では、LINQ to SQL デザイナーを使用して定義されたモデルとデータベースリレーションシップを表す .NET クラスが自動的に作成されます。 LINQ to SQL DataContext クラスは、ソリューションに追加された各 LINQ to SQL デザイナーファイルに対しても生成されます。 ここでは LINQ to SQL クラス項目に "" は "" という名前を付けているので、作成された DataContext クラスは "" という名前になります。 このクラスは、データベースを操作する主な方法です。

"ディナー" と "RSVPs" という2つのプロパティが公開されています。このクラスは、データベース内でモデル化された2つのテーブルを表しています。 を使用C#すると、これらのプロパティに対して LINQ クエリを作成し、データベースからディナーおよび RSVP オブジェクトを照会して取得することができます。

次のコードは、ディナーオブジェクトをインスタンス化し、それに対して LINQ クエリを実行して、今後発生する一連のを取得する方法を示しています。 Visual Studio は、LINQ クエリを記述するときに完全な intellisense を提供します。また、そのオブジェクトから返されたオブジェクトは厳密に型指定され、intellisense もサポートしています。

![](build-a-model-with-business-rule-validations/_static/image9.png)

ディナーおよび RSVP オブジェクトのクエリを実行できるようにするだけでなく、それを通じて取得したディナーおよび RSVP オブジェクトに対して行われた変更も、自動的に追跡されます。 この機能を使用すると、明示的な SQL update コードを記述しなくても、データベースに変更を簡単に保存できます。

たとえば、次のコードは、LINQ クエリを使用してデータベースから単一のディナーオブジェクトを取得し、2つのディナープロパティを更新して、変更をデータベースに保存する方法を示しています。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

上記のコードでは、このオブジェクトから取得したディナーオブジェクトに対して行われたプロパティの変更が自動的に追跡されています。 "SubmitChanges ()" メソッドを呼び出した場合、更新された値を保持するために、適切な SQL "UPDATE" ステートメントをデータベースに対して実行します。

### <a name="creating-a-dinnerrepository-class"></a>Dinのリポジトリクラスを作成する

小規模なアプリケーションの場合、コントローラーを LINQ to SQL DataContext クラスに対して直接動作させ、コントローラー内に LINQ クエリを埋め込むことが問題になることがあります。 しかし、アプリケーションの規模が大きくなるにつれて、このアプローチは保守とテストが煩雑になります。 また、同じ LINQ クエリを複数の場所で複製することもできます。

アプリケーションの保守とテストを容易にする方法の1つは、"リポジトリ" パターンを使用することです。 リポジトリクラスは、データのクエリと永続化ロジックをカプセル化し、アプリケーションからのデータ永続化の実装の詳細を抽象化するのに役立ちます。 アプリケーションコードをすっきりさせるだけでなく、リポジトリパターンを使用すると、将来のデータストレージの実装を簡単に変更できるようになります。また、実際のデータベースを必要とせずに、アプリケーションの単体テストを容易にすることができます。

このアプリケーションでは、次のシグネチャを使用して Dinのリポジトリクラスを定義します。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*注: この章の後の方で、このクラスから IDinnerRepository インターフェイスを抽出し、コントローラーでの依存関係の挿入を有効にします。最初に、簡単に始めて、Dinのリポジトリクラスを直接操作します。*

このクラスを実装するには、[モデル] フォルダーを右クリックし、[**新しい項目の&gt;追加**] メニューコマンドを選択します。 [新しい項目の追加] ダイアログボックスで、"Class" テンプレートを選択し、ファイルに "DinnerRepository.cs" という名前を指定します。

![](build-a-model-with-business-rule-validations/_static/image10.png)

次のコードを使用して、Din: Repository クラスを実装できます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>Dinのリポジトリクラスを使用した取得、更新、挿入、および削除

これで、Dinのリポジトリクラスが作成されました。次に、それを使用して実行できる一般的なタスクを示すいくつかのコード例を見てみましょう。

#### <a name="querying-examples"></a>クエリの例

次のコードは、Dinid 値を使用して1つのディナーを取得します。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

次のコードは、今後のすべてのディナーとループを取得します。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>挿入と更新の例

次のコードは、2つの新しいディナーを追加する方法を示しています。 リポジトリに対する追加や変更は、"Save ()" メソッドが呼び出されるまでデータベースにコミットされません。 LINQ to SQL によって、データベーストランザクションのすべての変更が自動的にラップされます。そのため、すべての変更が行われるか、リポジトリに保存されるときにいずれの変更も行われません。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

次のコードでは、既存のディナーオブジェクトを取得し、そのオブジェクトの2つのプロパティを変更します。 リポジトリで "Save ()" メソッドが呼び出されると、変更がデータベースにコミットされます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

次のコードは、ディナーを取得し、それに対して RSVP を追加します。 これを行うには、LINQ to SQL 作成したディナーオブジェクトの RSVPs コレクションを使用します (データベース内の2つの間に主キー/外部キーのリレーションシップがあるため)。 この変更は、リポジトリで "Save ()" メソッドが呼び出されたときに、新しい RSVP テーブル行としてデータベースに戻されます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>Delete の例

次のコードでは、既存のディナーオブジェクトを取得し、削除対象としてマークします。 リポジトリで "Save ()" メソッドが呼び出されると、削除がデータベースにコミットされます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>検証とビジネスルールロジックのモデルクラスとの統合

検証とビジネスルールのロジックの統合は、データを処理するアプリケーションの重要な部分です。

#### <a name="schema-validation"></a>スキーマの検証

LINQ to SQL デザイナーを使用してモデルクラスが定義されている場合、データモデルクラスのプロパティのデータ型はデータベーステーブルのデータ型に対応します。 たとえば、ディナーテーブルの "EventDate" 列が "datetime" の場合、LINQ to SQL によって作成されたデータモデルクラスは "DateTime" (組み込みの .NET データ型) になります。 つまり、コードから整数またはブール値を割り当てようとするとコンパイルエラーが発生し、実行時に有効でない文字列型を暗黙的に変換しようとすると、エラーが自動的に発生します。

また、LINQ to SQL では、文字列を使用する場合に SQL の値のエスケープが自動的に処理されます。これにより、SQL インジェクション攻撃を防ぐのに役立ちます。

#### <a name="validation-and-business-rule-logic"></a>検証とビジネスルールのロジック

スキーマの検証は、最初の手順としては便利ですが、あまり十分ではありません。 ほとんどの実際のシナリオでは、より高度な検証ロジックを指定する機能が必要です。これは、複数のプロパティにまたがることができ、コードを実行し、多くの場合、モデルの状態を認識します。 モデルクラスに検証ルールを定義して適用するために使用できるさまざまなパターンとフレームワークが用意されています。また、これを支援するために使用できる .NET ベースのフレームワークがいくつかあります。 ASP.NET MVC アプリケーション内では、ほとんどすべてを使用できます。

私たちは、このアプリケーションのために、ディナーモデルオブジェクトに対して IsValid プロパティと GetRuleViolations () メソッドを公開する、比較的単純でストレートなパターンを使用します。 IsValid プロパティは、検証ルールとビジネスルールがすべて有効であるかどうかに応じて、true または false を返します。 GetRuleViolations () メソッドは、ルールエラーの一覧を返します。

"部分クラス" をプロジェクトに追加して、ディナーモデルに対して IsValid と GetRuleViolations () を実装します。 部分クラスを使用すると、VS デザイナーによって管理されているクラス (LINQ to SQL デザイナーによって生成されるディナークラスなど) にメソッド/プロパティ/イベントを追加したり、ツールがコードと触っことがないようにすることができます。 新しい部分クラスをプロジェクトに追加するには、[モデル] フォルダーを右クリックし、[新しい項目の追加] メニューコマンドを選択します。 次に、[新しい項目の追加] ダイアログボックスで "Class" テンプレートを選択して、Dinner.cs という名前を付けることができます。

![](build-a-model-with-business-rule-validations/_static/image11.png)

[追加] ボタンをクリックすると、Dinner.cs ファイルがプロジェクトに追加され、IDE 内で開かれます。 その後、次のコードを使用して、基本的なルール/検証実施フレームワークを実装できます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

上記のコードについては、次の点に注意してください。

- ディナークラスには "partial" キーワードが付いています。これは、その中に含まれるコードが、LINQ to SQL デザイナーによって生成または管理され、1つのクラスにコンパイルされたクラスと結合されることを意味します。
- RuleViolation クラスは、プロジェクトに追加するヘルパークラスであり、規則違反に関する詳細情報を提供することができます。
- GetRuleViolations () メソッドを使用すると、検証とビジネスルールが評価されます (後で実装します)。 次に、ルールエラーに関する詳細情報を提供する RuleViolation オブジェクトのシーケンスを返します。
- ディナープロパティは、ディナーオブジェクトにアクティブな RuleViolations があるかどうかを示す便利なヘルパープロパティを提供します。 常にディナーオブジェクトを使用して開発者が積極的にチェックすることができます (例外は発生しません)。
- ディナー () 部分メソッドは、ディナーオブジェクトがデータベース内で保持されようとしているときに通知を受け取ることができるようにするフック LINQ to SQL です。 上記の OnValidate () 実装により、ディナーが保存される前に、ディナー違反がないことが保証されます。 無効な状態にある場合は、例外が発生し、LINQ to SQL によってトランザクションが中止されます。

この方法では、検証とビジネスルールをに統合できる単純なフレームワークが提供されます。 ここでは、次のルールを GetRuleViolations () メソッドに追加します。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

ここでは、のC# "yield return" 機能を使用して、ruleviolations のシーケンスを返しています。 上記の最初の6つのルールチェックでは、ディナーの文字列プロパティを null または空にすることはできません。 最後の規則はもう少し興味深いものであり、次のように、プロジェクトに追加して、ContactPhone の番号の形式がディナーの国と一致することを確認するためにプロジェクトに追加できる、参照してください。 IsValidNumber () ヘルパーメソッドを呼び出します。

を使用できます。この電話検証サポートを実装するための、NET の正規表現サポート。 次に示すのは、国固有の正規表現パターンチェックを追加できるようにするプロジェクトに追加できる、次のような、簡単な電話検証の実装です。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>検証とビジネスロジック違反の処理

上記の検証とビジネスルールコードを追加したので、ディナーを作成または更新しようとするたびに、検証ロジックルールが評価され、適用されます。

開発者は、次のようなコードを記述して、ディナーオブジェクトが有効かどうかを事前に判断し、例外を発生させずにすべての違反の一覧を取得することができます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

ディナーを無効な状態で保存しようとすると、Dinrepository で Save () メソッドを呼び出すと例外が発生します。 これは、LINQ to SQL がディナーの変更を保存する前に、ディナー () 部分メソッドを自動的に呼び出し、ディナーに規則違反が存在する場合に例外を発生させるコードをディナー () に追加したためです。 この例外をキャッチして、修正する違反の一覧を事後で取得することができます。

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

検証とビジネスルールは、UI レイヤー内ではなく、モデルレイヤー内に実装されるため、アプリケーション内のすべてのシナリオで適用および使用されます。 後でビジネスルールを変更または追加し、ディナーオブジェクトで動作するすべてのコードでそれらを優先することができます。

これらの変更をアプリケーションおよび UI ロジック全体に波及させずに、ビジネスルールを1か所で柔軟に変更できるようにすることは、適切に記述されたアプリケーションの署名であり、MVC フレームワークが推奨する利点です。

### <a name="next-step"></a>次の手順

これで、データベースのクエリと更新の両方に使用できるモデルが完成しました。

ここで、いくつかのコントローラーとビューをプロジェクトに追加して、それに関する HTML UI エクスペリエンスを構築するために使用できるようにしましょう。

> [!div class="step-by-step"]
> [前へ](create-a-database.md)
> [次へ](use-controllers-and-views-to-implement-a-listingdetails-ui.md)

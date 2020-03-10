---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: データソースコントロール |Microsoft Docs
author: microsoft
description: ASP.NET 1.x の DataGrid コントロールは、Web アプリケーションでのデータアクセスの大幅な向上をマークしました。 ただし、これはユーザーにとってわかりやすいということではありませんでした。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: a2e2cfbec3e5aebf42a2de30bab7d45b4b610298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519352"
---
# <a name="data-source-controls"></a>データ ソース コントロール

[Microsoft](https://github.com/microsoft)

> ASP.NET 1.x の DataGrid コントロールは、Web アプリケーションでのデータアクセスの大幅な向上をマークしました。 ただし、これはユーザーにとってわかりやすいものではありませんでした。 それでも、はるかに便利な機能を取得するには、かなりの量のコードが必要です。 このようなモデルは、すべてのデータアクセスにおける 1. x のモデルです。

ASP.NET 1.x の DataGrid コントロールは、Web アプリケーションでのデータアクセスの大幅な向上をマークしました。 ただし、これはユーザーにとってわかりやすいものではありませんでした。 それでも、はるかに便利な機能を取得するには、かなりの量のコードが必要です。 このようなモデルは、すべてのデータアクセスにおける 1. x のモデルです。

ASP.NET 2.0 では、データソースコントロールを使用して、これをで扱います。 ASP.NET 2.0 のデータソースコントロールは、データの取得、データの表示、データの編集を行うための宣言型モデルを開発者に提供します。 データソースコントロールの目的は、データのソースに関係なく、データバインドコントロールに一貫性のあるデータ表現を提供することです。 ASP.NET 2.0 のデータソースコントロールの中核となるのは、DataSourceControl 抽象クラスです。 DataSourceControl クラスは、IDataSource インターフェイスと IListSource インターフェイスの基本実装を提供します。後者の場合は、新しい DataSourceId プロパティを使用して、データバインドコントロールの DataSource としてデータソースコントロールを割り当てることができます。後で説明します) と、そのデータをリストとして公開します。 データソースコントロールのデータの各リストは、DataSourceView オブジェクトとして公開されます。 DataSourceView インスタンスへのアクセスは、IDataSource インターフェイスによって提供されます。 たとえば、GetViewNames メソッドは、特定のデータソースコントロールに関連付けられている DataSourceViews を列挙できる ICollection を返します。また、GetView メソッドを使用すると、特定の DataSourceView インスタンスに名前でアクセスできます。

データソースコントロールには、ユーザーインターフェイスはありません。 これらはサーバーコントロールとして実装されるため、宣言構文をサポートし、必要に応じてページの状態にアクセスできるようにします。 データソースコントロールは、HTML マークアップをクライアントに表示しません。

> [!NOTE]
> 後で説明するように、データソースコントロールを使用して得られるキャッシュの利点もあります。

## <a name="storing-connection-strings"></a>保存 (接続文字列を)

データソースコントロールの構成方法を確認する前に、接続文字列に関する ASP.NET 2.0 の新機能について説明します。 ASP.NET 2.0 では、実行時に動的に読み取ることができる接続文字列を簡単に格納できるようにする新しいセクションが構成ファイルに導入されています。 &lt;connectionStrings&gt; セクションを使用すると、接続文字列を簡単に格納できます。

次のスニペットは、新しい接続文字列を追加します。

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> &lt;appSettings&gt; セクションと同様に、&lt;connectionStrings&gt; セクションは、構成ファイルの &lt;system.web&gt; セクションの外側に表示されます。

この接続文字列を使用するには、サーバーコントロールの ConnectionString 属性を設定するときに、次の構文を使用します。

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

&lt;connectionStrings&gt; セクションを暗号化して、機密情報が公開されないようにすることもできます。 その機能については、後のモジュールで説明します。

## <a name="caching-data-sources"></a>データソースのキャッシュ

各 DataSourceControl には、キャッシュを構成するための4つのプロパティがあります。EnableCaching、CacheDuration、CacheExpirationPolicy、および CacheKeyDependency。

## <a name="enablecaching"></a>EnableCaching

EnableCaching は、データソースコントロールのキャッシュを有効にするかどうかを決定するブール型プロパティです。

## <a name="cacheduration-property"></a>CacheDuration プロパティ

CacheDuration プロパティは、キャッシュを有効なままにする秒数を設定します。 このプロパティを**0**に設定すると、明示的に無効になるまでキャッシュが有効のままになります。

## <a name="cacheexpirationpolicy-property"></a>CacheExpirationPolicy プロパティ

CacheExpirationPolicy プロパティは、**絶対**または**スライディング**に設定できます。 このオプションを [絶対] に設定すると、データがキャッシュされる最大時間は、CacheDuration プロパティで指定された秒数になります。 [スライディング] に設定すると、各操作の実行時に有効期限がリセットされます。

## <a name="cachekeydependency-property"></a>CacheKeyDependency プロパティ

CacheKeyDependency プロパティに文字列値が指定されている場合、ASP.NET はその文字列に基づいて新しいキャッシュ依存関係を設定します。 これにより、CacheKeyDependency を変更または削除するだけで、キャッシュを明示的に無効にすることができます。

**重要**: 権限借用が有効になっており、データソースやデータのコンテンツへのアクセスがクライアント id に基づいている場合は、EnableCaching を False に設定することにより、キャッシュを無効にすることをお勧めします。 このシナリオでキャッシュが有効になっていて、最初にデータを要求したユーザー以外のユーザーが要求を発行した場合、データソースへの承認は適用されません。 データは、単にキャッシュから提供されます。

## <a name="the-sqldatasource-control"></a>SqlDataSource コントロール

SqlDataSource コントロールを使用すると、開発者は、ADO.NET をサポートする任意のリレーショナルデータベースに格納されているデータにアクセスできます。 System.data.oracleclient プロバイダーを使用すると、Oracle にアクセスするために、プロバイダー、または、system.string プロバイダー、またはプロバイダーに SQL Server アクセスすることができますが、このプロバイダーを使用することもできます。 そのため、SqlDataSource は、SQL Server データベースのデータにアクセスするためだけに使用されるわけではありません。

SqlDataSource を使用するには、単に ConnectionString プロパティの値を指定し、SQL コマンドまたはストアドプロシージャを指定します。 SqlDataSource コントロールは、基になる ADO.NET アーキテクチャを操作します。 接続を開くか、データソースにクエリを実行するか、ストアドプロシージャを実行してデータを返し、接続を閉じます。

> [!NOTE]
> DataSourceControl クラスは自動的に接続を閉じるため、データベース接続のリークによって生成される顧客呼び出しの数を減らす必要があります。

次のコードスニペットでは、前に示したように、構成ファイルに格納されている接続文字列を使用して、DropDownList コントロールを SqlDataSource コントロールにバインドしています。

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

上に示したように、SqlDataSource の DataSourceMode プロパティは、データソースのモードを指定します。 上記の例では、DataSourceMode は DataReader に設定されています。 この場合、SqlDataSource は、順方向専用および読み取り専用のカーソルを使用して、IDataReader オブジェクトを返します。 返される指定された型のオブジェクトは、使用されるプロバイダーによって制御されます。 この例では、web.config ファイルの &lt;connectionStrings&gt; セクションで指定されているように、system.string プロバイダーを使用します。 したがって、返されるオブジェクトは、SqlDataReader 型になります。 データセットの DataSourceMode 値を指定することにより、データをサーバー上のデータセットに格納できます。 このモードでは、並べ替え、ページングなどの機能を追加できます。SqlDataSource を GridView コントロールにデータバインドしていた場合は、データセットモードを選択します。 ただし、DropDownList の場合は、DataReader モードが適切な選択です。

> [!NOTE]
> SqlDataSource または AccessDataSource をキャッシュする場合は、DataSourceMode プロパティを DataSet に設定する必要があります。 DataReader の DataSourceMode でキャッシュを有効にすると、例外が発生します。

## <a name="sqldatasource-properties"></a>SqlDataSource プロパティ

次に、SqlDataSource コントロールのプロパティの一部を示します。

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

パラメーターのいずれかが null の場合に select コマンドを取り消すかどうかを指定するブール値です。 既定では true です。

### <a name="conflictdetection"></a>ConflictDetection

複数のユーザーが同時にデータソースを更新している場合は、ConflictDetection プロパティによって SqlDataSource コントロールの動作が決定されます。 このプロパティは、ConflictOptions 列挙値のいずれかに評価されます。 これらの値は、 **Compareallvalues**および**overwritechanges**内容です。 オーバー書き込みが設定されている場合、データソースに最後にデータを書き込んだユーザーが以前の変更を上書きします。 ただし、ConflictDetection プロパティが CompareAllValues に設定されている場合は、SelectCommand によって返される列に対してパラメーターが作成され、それらの列の元の値が保持されます。SelectCommand が実行されてから値が変更されたかどうかを確認します。

### <a name="deletecommand"></a>DeleteCommand

データベースから行を削除するときに使用する SQL 文字列を設定または取得します。 SQL クエリまたはストアドプロシージャ名のいずれかを指定できます。

### <a name="deletecommandtype"></a>DeleteCommandType

SQL クエリ (テキスト) またはストアドプロシージャ (StoredProcedure) のいずれかである、delete コマンドの種類を設定または取得します。

### <a name="deleteparameters"></a>DeleteParameters

SqlDataSource コントロールに関連付けられている SqlDataSourceView オブジェクトの DeleteCommand によって使用されるパラメーターを返します。

### <a name="oldvaluesparameterformatstring"></a>OldValuesParameterFormatString

このプロパティは、ConflictDetection プロパティが CompareAllValues に設定されている場合に、元の値パラメーターの形式を指定するために使用されます。 既定値は {0} 元の値のパラメーターが元のパラメーターと同じ名前であることを意味します。 つまり、フィールド名が EmployeeID の場合、元の値パラメーターは @EmployeeIDになります。

### <a name="selectcommand"></a>SelectCommand

データベースからデータを取得するために使用される SQL 文字列を設定または取得します。 SQL クエリまたはストアドプロシージャ名のいずれかを指定できます。

### <a name="selectcommandtype"></a>SelectCommandType

SQL クエリ (テキスト) またはストアドプロシージャ (StoredProcedure) のいずれかの select コマンドの種類を設定または取得します。

### <a name="selectparameters"></a>SelectParameters

SqlDataSource コントロールに関連付けられている SqlDataSourceView オブジェクトの SelectCommand によって使用されるパラメーターを返します。

### <a name="sortparametername"></a>SortParameterName

データソースコントロールによって取得されるデータを並べ替えるときに使用されるストアドプロシージャパラメーターの名前を取得します。値の設定もできます。 SelectCommandType が StoredProcedure に設定されている場合にのみ有効です。

### <a name="sqlcachedependency"></a>SqlCacheDependency

SQL Server キャッシュの依存関係で使用されるデータベースとテーブルを指定する、セミコロンで区切られた文字列。 (SQL キャッシュの依存関係については、後のモジュールで説明します)。

### <a name="updatecommand"></a>UpdateCommand

データベース内のデータを更新するときに使用される SQL 文字列を設定または取得します。 SQL クエリまたはストアドプロシージャ名のいずれかを指定できます。

### <a name="updatecommandtype"></a>UpdateCommandType

Update コマンドの種類 (SQL クエリ (テキスト) またはストアドプロシージャ (StoredProcedure)) を設定または取得します。

### <a name="updateparameters"></a>UpdateParameters

SqlDataSource コントロールに関連付けられている SqlDataSourceView オブジェクトの UpdateCommand によって使用されるパラメーターを返します。

## <a name="the-accessdatasource-control"></a>AccessDataSource コントロール

AccessDataSource コントロールは、SqlDataSource クラスから派生し、Microsoft Access データベースにデータをバインドするために使用されます。 AccessDataSource コントロールの ConnectionString プロパティは、読み取り専用プロパティです。 ConnectionString プロパティを使用する代わりに、次に示すように、Access データベースを指すようにデータファイルプロパティを使用します。

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource は常に、ベース SqlDataSource の ProviderName をに設定し、OLE DB Microsoft のプロバイダーを使用してデータベースに接続します。 AccessDataSource コントロールを使用して、パスワードで保護された Access データベースに接続することはできません。 パスワードで保護されたデータベースに接続する必要がある場合は、SqlDataSource コントロールを使用する必要があります。

> [!NOTE]
> Web サイト内に格納されているデータベースへのアクセスは、アプリの\_データディレクトリに配置する必要があります。 ASP.NET では、このディレクトリ内のファイルを参照することはできません。 Access データベースを使用する場合は、アプリ\_データディレクトリに対する読み取りと書き込みのアクセス許可をプロセスアカウントに付与する必要があります。

## <a name="the-xmldatasource-control"></a>XmlDataSource コントロール

XmlDataSource は、XML データをデータバインドコントロールにデータバインドするために使用されます。 データファイルプロパティを使用して XML ファイルにバインドすることも、Data プロパティを使用して XML 文字列にバインドすることもできます。 XmlDataSource は、バインド可能フィールドとして XML 属性を公開します。 属性として表されない値にバインドする必要がある場合は、XSL 変換を使用する必要があります。 XPath 式を使用して XML データをフィルター処理することもできます。

次の XML ファイルについて考えてみます。

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

XmlDataSource は、Person */person*の XPath プロパティを使用して、&lt;Person&gt; ノードのみをフィルター処理することに注意してください。 DropDownList は、DataTextField プロパティを使用して、LastName 属性にデータをバインドします。

XmlDataSource コントロールは、主に読み取り専用の XML データにデータバインドするために使用されますが、XML データファイルを編集することもできます。 このような場合、XML ファイル内の情報の自動挿入、更新、および削除は、他のデータソースコントロールと同様に自動的には行われないことに注意してください。 代わりに、XmlDataSource コントロールの次のメソッドを使用してデータを手動で編集するコードを記述する必要があります。

### <a name="getxmldocument"></a>GetXmlDocument

XmlDataSource によって取得された XML コードを含む XmlDocument オブジェクトを取得します。

### <a name="save"></a>保存

メモリ内の XmlDocument をデータソースに保存します。

Save メソッドは、次の2つの条件が満たされている場合にのみ機能することを認識しておくことが重要です。

1. XmlDataSource は、データプロパティではなく XML ファイルにバインドするためにデータファイルプロパティを使用して、インメモリ XML データにバインドしています。
2. Transform または TransformFile プロパティを使用して変換を指定することはできません。

また、Save メソッドでは、複数のユーザーによって同時に呼び出された場合に予期しない結果が生成されることもあります。

## <a name="the-objectdatasource-control"></a>ObjectDataSource コントロール

この時点までに説明したデータソースコントロールは、データソースコントロールがデータストアと直接通信する2層アプリケーションに適しています。 ただし、多くの実際のアプリケーションは多階層アプリケーションであり、データソースコントロールは、データレイヤーと通信するビジネスオブジェクトと通信する必要がある場合があります。 このような状況では、ObjectDataSource によって請求書が適切に入力されます。 ObjectDataSource は、ソースオブジェクトと連携して動作します。 ObjectDataSource コントロールは、ソースオブジェクトのインスタンスを作成し、指定されたメソッドを呼び出します。また、オブジェクトに静的メソッドではなくインスタンスメソッド (Visual Basic で共有) がある場合は、1つの要求のスコープ内でオブジェクトインスタンスをすべて破棄します。 そのため、オブジェクトはステートレスである必要があります。 つまり、オブジェクトは、1つの要求の範囲内で必要なすべてのリソースを取得して解放する必要があります。 ObjectDataSource コントロールの ObjectCreating イベントを処理することによって、ソースオブジェクトの作成方法を制御できます。 ソースオブジェクトのインスタンスを作成し、そのインスタンスに対して ObjectDataSourceEventArgs クラスの ObjectInstance プロパティを設定できます。 ObjectDataSource コントロールは、独自のインスタンスを作成するのではなく、ObjectCreating イベントで作成されたインスタンスを使用します。

ObjectDataSource コントロールのソースオブジェクトが、データを取得および変更するために呼び出すことができるパブリック静的メソッド (Visual Basic で共有) を公開する場合、ObjectDataSource コントロールはこれらのメソッドを直接呼び出します。 ObjectDataSource コントロールで、メソッド呼び出しを行うためにソースオブジェクトのインスタンスを作成する必要がある場合、オブジェクトにはパラメーターをとらないパブリックコンストラクターを含める必要があります。 ObjectDataSource コントロールは、ソースオブジェクトの新しいインスタンスを作成するときに、このコンストラクターを呼び出します。

ソースオブジェクトに、パラメーターのないパブリックコンストラクターが含まれていない場合は、ObjectCreating イベントの ObjectDataSource コントロールによって使用されるソースオブジェクトのインスタンスを作成できます。

## <a name="specifying-object-methods"></a>オブジェクトメソッドの指定

ObjectDataSource コントロールのソースオブジェクトには、データの選択、挿入、更新、または削除に使用される任意の数のメソッドを含めることができます。 これらのメソッドは、ObjectDataSource コントロールの SelectMethod、InsertMethod、UpdateMethod、または DeleteMethod プロパティのいずれかを使用して識別されるように、メソッドの名前に基づいて ObjectDataSource コントロールによって呼び出されます。 ソースオブジェクトには、省略可能な SelectCount メソッドを含めることもできます。これは、データソースのオブジェクトの合計数を返す SelectCountMethod プロパティを使用して ObjectDataSource コントロールによって識別されます。 ObjectDataSource コントロールは、ページング時に使用するデータソースのレコードの合計数を取得するために、Select メソッドが呼び出された後に SelectCount メソッドを呼び出します。

## <a name="lab-using-data-source-controls"></a>データソースコントロールを使用するラボ

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>演習 1-SqlDataSource コントロールを使用したデータの表示

次の演習では、SqlDataSource コントロールを使用して Northwind データベースに接続します。 SQL Server 2000 インスタンスで Northwind データベースにアクセスできることを前提としています。

1. 新しい ASP.NET Web サイトの作成
2. 新しい web.config ファイルを追加します。

    1. ソリューションエクスプローラーでプロジェクトを右クリックし、[新しい項目の追加] をクリックします。
    2. テンプレートの一覧から [Web 構成ファイル] を選択し、[追加] をクリックします。
3. 次のように &lt;connectionStrings&gt; セクションを編集します。 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. 次のように、コードビューに切り替えて、ConnectionString 属性と SelectCommand 属性を &lt;asp: SqlDataSource&gt; コントロールに追加します。 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. デザインビューから、新しい GridView コントロールを追加します。
6. [GridView タスク] メニューの [データソースの選択] ドロップダウンで、[SqlDataSource1] を選択します。
7. Default.aspx を右クリックし、メニューから [ブラウザーで表示] を選択します。 保存を求めるメッセージが表示されたら、[はい] をクリックします。
8. GridView には、Products テーブルのデータが表示されます。

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>演習 2-SqlDataSource コントロールを使用したデータの編集

次の演習では、宣言構文を使用して DropDownList コントロールをデータバインドし、DropDownList コントロールに表示されるデータを編集できるようにする方法について説明します。

1. デザインビューで、GridView コントロールを default.aspx から削除します。 

    **重要**: ページの SqlDataSource コントロールはそのままにしておきます。
2. DropDownList コントロールを default.aspx に追加します。
3. ソースビューに切り替えます。
4. 次のように、DataSourceId、DataTextField、および DataValueField 属性を &lt;asp: DropDownList&gt; コントロールに追加します。 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Default.aspx を保存し、ブラウザーで表示します。 DropDownList には Northwind データベースのすべての製品が含まれていることに注意してください。
6. ブラウザーを閉じます。
7. Default.aspx のソースビューで、DropDownList コントロールの下に新しい TextBox コントロールを追加します。 テキストボックスの ID プロパティを txtProductName に変更します。
8. TextBox コントロールの下に、新しいボタンコントロールを追加します。 ボタンの ID プロパティを btnUpdate に変更し、Text プロパティを**Product Name に更新**します。
9. Default.aspx のソースビューで、次のように、UpdateCommand プロパティと2つの新しい UpdateParameters を SqlDataSource タグに追加します。 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > このコードには、2つの更新パラメーター (ProductName と ProductID) が追加されていることに注意してください。 これらのパラメーターは、txtProductName テキストボックスの Text プロパティと ddlProducts DropDownList の SelectedValue プロパティにマップされます。
10. デザインビューに切り替えて、ボタンコントロールをダブルクリックし、イベントハンドラーを追加します。
11. 次のコードを btnUpdate\_クリックしてコードを追加します。 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Default.aspx を右クリックし、ブラウザーで表示するように選択します。 すべての変更を保存するように求められたら、[はい] をクリックします。
13. ASP.NET 2.0 部分クラスでは、実行時にコンパイルを行うことができます。 コードの変更が有効になるようにアプリケーションを構築する必要はありません。
14. DropDownList から製品を選択します。
15. テキストボックスに選択した製品の新しい名前を入力し、[更新] ボタンをクリックします。
16. 製品名はデータベースで更新されます。

## <a name="exercise-3-using-the-objectdatasource-control"></a>手順 3. ObjectDataSource コントロールの使用

この演習では、ObjectDataSource コントロールとソースオブジェクトを使用して Northwind データベースと対話する方法について説明します。

1. ソリューションエクスプローラーでプロジェクトを右クリックし、[新しい項目の追加] をクリックします。
2. [テンプレート] ボックスの一覧で [Web フォーム] を選択します。 名前を「オブジェクト .aspx」に変更し、[追加] をクリックします。
3. ソリューションエクスプローラーでプロジェクトを右クリックし、[新しい項目の追加] をクリックします。
4. [テンプレート] ボックスの一覧で [クラス] を選択します。 クラスの名前を NorthwindData.cs に変更し、[追加] をクリックします。
5. アプリ\_コードフォルダーにクラスを追加するように求めるメッセージが表示されたら、[はい] をクリックします。
6. NorthwindData.cs ファイルに次のコードを追加します。 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. オブジェクト .aspx のソースビューに次のコードを追加します。 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. すべてのファイルを保存し、オブジェクト .aspx を参照します。
9. 詳細を表示したり、従業員を編集したり、従業員を追加したり、従業員を削除したりして、インターフェイスを操作します。

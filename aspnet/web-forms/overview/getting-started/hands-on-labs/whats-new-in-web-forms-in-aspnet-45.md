---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: ASP.NET 4.5 | の Web フォームの新機能Microsoft Docs
author: rick-anderson
description: 新しいバージョンの ASP.NET Web フォームでは、データを操作する際のユーザーエクスペリエンスの向上に焦点を合わせた多くの機能強化が導入されています。 以前のバージョンの
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 301af8ed877b58624e419c04f605c41f27dbdd0c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421924"
---
# <a name="whats-new-in-web-forms-in-aspnet-45"></a>ASP.NET 4.5 の Web フォームの新機能

[Web キャンプチーム](https://twitter.com/webcamps)別

> 新しいバージョンの ASP.NET Web フォームでは、データを操作する際のユーザーエクスペリエンスの向上に焦点を合わせた多くの機能強化が導入されています。
> 
> 以前のバージョンの Web フォームでは、データバインディングを使用してオブジェクトメンバーの値を出力する場合、データバインディング式 Bind () または Eval () が使用されていました。 新しいバージョンの ASP.NET では、新しい ItemType プロパティを使用して、コントロールがバインドされるデータの種類を宣言できます。 このプロパティを設定すると、厳密に型指定された変数を使用して、IntelliSense、メンバーナビゲーション、コンパイル時のチェックなど、Visual Studio の開発エクスペリエンスのすべての利点を得ることができます。
> 
> データバインドコントロールを使用すると、データを選択、更新、削除、挿入するための独自のカスタムメソッドを指定できるようになりました。また、ページコントロールとアプリケーションロジックの間のやり取りが簡単になります。 また、モデルバインド機能が ASP.NET に追加されています。つまり、ページからのデータをメソッドの型パラメーターに直接マップできます。
> 
> ユーザー入力の検証は、Web フォームの最新バージョンでも簡単に行うことができます。 **System.componentmodel**名前空間の検証属性を使用してモデルクラスに注釈を付け、すべてのサイトコントロールがその情報を使用してユーザー入力を検証するように要求できるようになりました。 Web フォームでのクライアント側の検証が jQuery と統合され、クライアント側のコードと控えめな JavaScript 機能が提供されるようになりました。
> 
> [要求の検証] 領域では、アプリケーションの特定の部分に対する要求の検証を選択的にオフにするか、無効化された要求データを読み取ることができるようになりました。
> 
> HTML5 の新機能を利用するために、Web フォームサーバーコントロールにいくつかの機能強化が行われています。
> 
> - TextBox コントロールの TextMode プロパティが更新され、email や datetime などの新しい HTML5 入力型がサポートされるようになりました。
> - FileUpload コントロールで、この HTML5 機能をサポートするブラウザーからの複数のファイルアップロードがサポートされるようになりました。
> - 検証コントロールは、HTML5 入力要素の検証をサポートするようになりました。
> - URL を表す属性を持つ新しい HTML5 要素では、runat =&quot;server&quot;がサポートされるようになりました。 その結果、URL パスで ASP.NET 規則を使用することができます。たとえば、~ 演算子を使用すると、アプリケーションのルートを表すことができます (&lt;video runat =&quot;server&quot; src =&quot;~/myvideo&quot;&gt;&lt;/ビデオ&gt;)。
> - UpdatePanel コントロールは、HTML5 入力フィールドの投稿をサポートするように修正されました。
> 
> 公式 ASP.NET ポータルでは、ASP.NET WebForms 4.5 の新機能の例をご覧いただけます。 [ASP.NET 4.5 と Visual Studio 2012 の新](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)機能
> 
> すべてのサンプルコードとスニペットは、 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)で入手できる Web キャンプトレーニングキットに含まれています。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- 厳密に型指定されたデータバインディング式を使用する
- Web フォームでの新しいモデルバインド機能の使用
- ページデータを分離コードメソッドにマップするための値プロバイダーの使用
- ユーザー入力の検証にデータ注釈を使用する
- Web フォームの jQuery を使用した控えめなクライアント側の検証を活用する
- 詳細な要求の検証を実装する
- Web フォームでの非同期ページ処理の実装

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

このラボを完了するには、次の項目が必要です。

- Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)ます (付録 a をインストールする手順については[、「付録 a](#AppendixA) 」を参照してください)。

<a id="Setup"></a>
### <a name="setup"></a>セットアップ

**コードスニペットのインストール**

便宜上、このラボで管理するコードの多くは、Visual Studio のコードスニペットとして提供されています。 コードスニペットをインストールするには、 **.\Source\Setup\CodeSnippets.vsi**ファイルを実行します。

Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習したい場合は、この &quot;ドキュメントの付録「[付録 C: コードスニペットの使用](#AppendixC)&quot;」を参照してください。

<a id="Exercises"></a>
## <a name="exercises"></a>手順

このハンズオンラボには、次の演習が含まれています。

1. [演習 1: ASP.NET Web フォームでのモデルバインド](#Exercise1)
2. [演習 2: データの検証](#Exercise2)
3. [演習 3: ASP.NET Web フォームでの非同期ページ処理](#Exercise3)

> [!NOTE]
> 各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。 演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。

このラボの推定所要時間: **60 分**。

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a>演習 1: ASP.NET Web フォームでのモデルバインド

新しいバージョンの ASP.NET Web フォームでは、データを操作する際のエクスペリエンスの向上に焦点を合わせた多くの拡張機能が導入されています。 この演習では、厳密に型指定されたデータコントロールとモデルバインドについて学習します。

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a>タスク 1-厳密に型指定されたデータバインディングの使用

このタスクでは、ASP.NET 4.5 で使用可能な新しい厳密に型指定されたバインディングについて説明します。

1. **Source/Ex1-ModelBinding/begin/** folder にある**begin**ソリューションを開きます。

   1. 続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **[Customers]** ページを開きます。 メインコントロールに番号なしのリストを配置し、各顧客を一覧表示するための内に repeater コントロールを含めます。 次のコードに示すように、リピータ名を「**顧客 Srepeater** 」に設定します。

    以前のバージョンの Web フォームでは、データバインディングを使用して、データバインディング先のオブジェクトのメンバーの値を出力する場合、Eval メソッドの呼び出しと共にデータバインディング式を使用して、メンバーの名前を文字列として渡します。

    実行時に、Eval へのこれらの呼び出しは、指定された名前を持つメンバーの値を読み取るために、現在バインドされているオブジェクトに対してリフレクションを使用し、結果を HTML に表示します。 この方法を使用すると、任意の整形されていないデータに対してデータバインドを非常に簡単に行うことができます。

    残念ながら、メンバー名の IntelliSense、ナビゲーションのサポート ([定義へ移動] など)、およびコンパイル時チェックを含む、Visual Studio の優れた開発時エクスペリエンス機能の多くが失われています。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. **Customers.aspx.cs**ファイルを開きます。
4. 次の using ステートメントを追加します。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. **ページ\_Load**メソッドで、顧客の一覧を使用してリピータに設定するコードを追加します。

    (コードスニペット- *Web フォーム Ex01-Bind Customers データソース*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    このソリューションでは、EntityFramework と CodeFirst を使用して、データベースを作成し、アクセスします。 次のコードでは、顧客の Srepeater は、データベースからすべての顧客を返す具体化されたクエリにバインドされています。
6. **F5**キーを押してソリューションを実行し、 **[Customers]** ページにアクセスして、リピータが動作していることを確認します。 ソリューションが CodeFirst を使用しているときは、アプリケーションの実行時にデータベースが作成され、ローカルの SQL Express インスタンスに設定されます。

    ![リピータを使用した顧客の一覧表示](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "リピータを使用した顧客の一覧表示")

    *リピータを使用した顧客の一覧表示*

    > [!NOTE]
    > Visual Studio 2012 では、IIS Express は既定の Web 開発サーバーです。
7. ブラウザーを閉じて、Visual Studio に戻ります。
8. ここで、実装を置き換えて、厳密に型指定されたバインディングを使用します。 **Customers**ページを開き、repeater の新しい**ItemType**属性を使用して、**顧客**の種類をバインドの種類として設定します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    ItemType プロパティを使用すると、コントロールがバインドされるデータの種類を宣言し、データバインドコントロール内で厳密に型指定されたバインディングを使用できるようになります。
9. ItemTemplate コンテンツを次のコードに置き換えます。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    上記のアプローチの欠点の1つは、Eval () および Bind () の呼び出しが遅延バインディングされることです。つまり、プロパティ名を表す文字列を渡します。 つまり、メンバー名に対して Intellisense を使用したり、コードナビゲーション ([定義へ移動] など) をサポートしたり、コンパイル時のチェックをサポートしたりすることはありません。

    ItemType プロパティを設定すると、2つの新しい型指定された変数が、 **Item**および**BindItem**というデータバインディング式のスコープ内に生成されます。 これらの厳密に型指定された変数をデータバインディング式で使用して、Visual Studio 開発環境のすべての利点を得ることができます。

    式で使用されている &quot; **:** &quot; は、セキュリティの問題 (クロスサイトスクリプティング攻撃など) を回避するために、出力を自動的に HTML エンコードします。 この表記は、応答の書き込みのために .NET 4 以降で使用できるようになりましたが、現在はデータバインディング式でも使用できます。

    > [!NOTE]
    > 項目メンバーは、一方向のバインドに対して機能します。 双方向のバインドを実行する場合は、 **BindItem**メンバーを使用します。

    ![厳密に型指定されたバインディングでの IntelliSense のサポート](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "厳密に型指定されたバインディングでの IntelliSense のサポート")

    *厳密に型指定されたバインディングでの IntelliSense のサポート*
10. **F5**キーを押してソリューションを実行し、[Customers] ページにアクセスして、変更が期待どおりに動作することを確認します。

    ![顧客の詳細の一覧表示](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "顧客の詳細の一覧表示")

    *顧客の詳細の一覧表示*
11. ブラウザーを閉じて、Visual Studio に戻ります。

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a>タスク 2-Web フォームでのモデルバインドの概要

以前のバージョンの ASP.NET Web フォームでは、データの取得と更新の両方で双方向のデータバインディングを実行する場合、データソースオブジェクトを使用する必要がありました。 これには、オブジェクトデータソース、SQL データソース、LINQ データソースなどがあります。 ただし、データを処理するためのカスタムコードが必要なシナリオでは、オブジェクトデータソースを使用する必要があります。これにより、いくつかの欠点がもたらされます。 たとえば、複合型を避け、検証ロジックの実行時に例外を処理する必要があるとします。

新しいバージョンの ASP.NET Web フォームでは、データバインドコントロールはモデルバインドをサポートしています。 つまり、選択、更新、挿入、および削除の各メソッドをデータバインドコントロールに直接指定して、分離コードファイルまたは別のクラスからロジックを呼び出すことができます。

この詳細については、GridView を使用して、新しい**SelectMethod**属性を使用して製品カテゴリを一覧表示します。 この属性を使用すると、GridView データを取得するメソッドを指定できます。

1. **Products**ページを開き、 **GridView**を含めます。 次に示すように GridView を構成して、厳密に型指定されたバインディングを使用し、並べ替えとページングを有効にします。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. 新しい**SelectMethod**属性を使用して、 **GetCategories**メソッドを呼び出してデータを選択するように GridView を構成します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. **Products.aspx.cs**分離コードファイルを開き、次の using ステートメントを追加します。

    (コードスニペット- *Web フォーム Ex01-名前空間*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. Products クラスにプライベートメンバーを追加し、**製品** **コンテキスト**の新しいインスタンスを割り当てます。 このプロパティには、データベースに接続できるようにする Entity Framework データコンテキストが格納されます。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. LINQ を使用してカテゴリの一覧を取得するための**GetCategories**メソッドを作成します。 このクエリには**products**プロパティが含まれているため、GridView は各カテゴリの製品の量を表示できます。 メソッドは、ページのライフサイクルで後で実行されるクエリを表す未加工の IQueryable オブジェクトを返します。

    (コードスニペット- *Web フォーム Ex01-GetCategories*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > 以前のバージョンの ASP.NET Web フォームでは、オブジェクトデータソースコンテキスト内で独自のリポジトリロジックを使用して並べ替えとページングを有効にすることで、独自のカスタムコードを記述し、必要なすべてのパラメーターを受け取る必要があります。 これで、データバインディングメソッドが IQueryable を返すことができるようになりました。これは実行されているクエリを表しているため、ASP.NET はクエリを変更して適切な並べ替えとページングパラメーターを追加することができます。
6. **F5**キーを押してサイトのデバッグを開始し、[製品] ページにアクセスします。 GridView には、GetCategories メソッドによって返されるカテゴリが設定されていることがわかります。

    ![モデルバインドを使用した GridView の設定](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "モデルバインドを使用した GridView の設定")

    *モデルバインドを使用した GridView の設定*
7. **SHIFT**キーを押し+**F5**キーを押してデバッグを停止します。

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a>タスク 3-モデルバインドの値プロバイダー

モデルバインドを使用すると、データバインドコントロールでデータを直接操作するカスタムメソッドを指定できるだけでなく、ページのデータをこれらのメソッドのパラメーターにマップすることもできます。 メソッドパラメーターでは、値プロバイダーの属性を使用して値のデータソースを指定できます。 次に例を示します。

- ページ上のコントロール
- クエリ文字列の値
- データの表示
- セッションの状態
- Cookie
- ポストされたフォームデータ
- 状態の表示
- カスタム値プロバイダーもサポートされています。

ASP.NET MVC 4 を使用している場合は、モデルバインディングのサポートも似ていることがわかります。 実際、これらの機能は ASP.NET MVC から取得さ**れ、system.web アセンブリに**移動され、web フォームでも使用できるようになりました。

このタスクでは、GridView を更新して、各カテゴリの製品の数によって結果をフィルター処理し、モデルバインドでフィルターパラメーターを受け取ります。

1. **[Products]** ページに戻ります。
2. GridView の上部に、次に示すように、各カテゴリの製品数を選択する**ラベル**と**コンボボックス**を追加します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. 選択した数の製品が含まれているカテゴリが存在しない場合にメッセージを表示するには、 **EmptyDataTemplate**を GridView に追加します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. **Products.aspx.cs**の分離コードを開き、次の using ステートメントを追加します。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. **GetCategories**メソッドを変更して、整数の**min製品カウント**引数を受け取り、返された結果をフィルター処理します。 これを行うには、メソッドを次のコードに置き換えます。

    (コードスニペット- *Web フォーム Ex01-GetCategories 2*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    **Min$ count**引数の新しい **[Control]** 属性は、ページ内のコントロールを使用してその値を設定する必要があることを ASP.NET に伝えます。 ASP.NET は、引数の名前 (Min$ Count) に一致するコントロールを検索し、必要なマッピングと変換を実行して、パラメーターにコントロールの値を設定します。

    または、属性はオーバーロードされたコンストラクターを提供します。このコンストラクターを使用すると、値の取得元のコントロールを指定できます。

    > [!NOTE]
    > データバインディング機能の1つの目的は、ページの操作のために記述する必要があるコードの量を減らすことです。 [コントロール] 値プロバイダーとは別に、メソッドパラメーターで他のモデルバインディングプロバイダーを使用できます。 これらの一部は、タスクの概要に記載されています。
6. **F5**キーを押してサイトのデバッグを開始し、[製品] ページにアクセスします。 ドロップダウンリストから複数の製品を選択すると、GridView がどのように更新されたかがわかります。

    ![ドロップダウンリストの値を使用して GridView をフィルター処理する](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "ドロップダウンリストの値を使用して GridView をフィルター処理する")

    *ドロップダウンリストの値を使用して GridView をフィルター処理する*
7. デバッグを停止します。

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a>タスク 4-フィルター処理にモデルバインドを使用する

このタスクでは、選択したカテゴリ内の製品を表示するために、2番目の子 GridView を追加します。

1. **Products**ページを開き、カテゴリ GridView を更新して、[選択] ボタンを自動生成します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. 一番下にある $ $ 2 番目の "製品" という**名前の 2**つ目の**GridView**を追加 **ItemType**を**webいる datakeynames**に設定します。これは**ProductId**に 、 **SelectMethod**を**getproducts**に設定します。 **AutoGenerateColumns**を**false**に設定し、ProductId、ProductName、Description、および UnitPrice の列を追加します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. **Products.aspx.cs**分離コードファイルを開きます。 Category GridView からカテゴリ ID を受け取り、製品をフィルター処理するには、 **Getproducts**メソッドを実装します。 モデルバインドでは、**カテゴリグリッド**で選択された行を使用して、パラメーター値が設定されます。 引数の名前とコントロール名が一致しないため、コントロールの名前をコントロールの値プロバイダーに指定する必要があります。

    (コードスニペット- *Web フォーム Ex01-GetProducts*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > この方法を使用すると、これらのメソッドの単体テストが簡単になります。 Web フォームが実行されていない単体テストコンテキストでは、[コントロール] 属性は特定のアクションを実行しません。
4. **Products**ページを開き、[Products] GridView を見つけます。 Products GridView を更新して、選択した製品を編集するためのリンクを表示します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. **Productdetails .aspx**ページを開き、 **selectproduct**メソッドを次のコードに置き換えます。

    (コードスニペット- *Web フォーム Ex01-SelectProduct メソッド*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > **[QueryString]** 属性を使用して、クエリ文字列の productId パラメーターからメソッドパラメーターを設定することに注意してください。
6. **F5**キーを押してサイトのデバッグを開始し、[製品] ページにアクセスします。 [カテゴリ] GridView から任意のカテゴリを選択し、[products] GridView が更新されていることを確認します。

    ![選択したカテゴリの製品を表示しています](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "選択したカテゴリの製品を表示しています")

    *選択したカテゴリの製品を表示しています*
7. 製品の **[表示]** リンクをクリックして、productdetails .aspx ページを開きます。

    ページが、クエリ文字列から productId パラメーターを使用して、SelectMethod を使用して製品を取得していることに注意してください。

    ![製品の詳細を表示する](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "製品の詳細を表示する")

    *製品の詳細を表示する*

    > [!NOTE]
    > 次の演習では、HTML の説明を入力する機能を実装します。

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a>タスク 5-モデルバインドを使用した更新操作

前のタスクでは、主にデータを選択するためにモデルバインドを使用しました。このタスクでは、更新操作でモデルバインドを使用する方法を学習します。

カテゴリ GridView を更新して、ユーザーがカテゴリを更新できるようにします。

1. **Products**ページを開き、[カテゴリ] GridView を更新して [Edit] \ (編集 \) ボタンを自動生成し、[new **UpdateMethod** ] 属性を使用して、選択した項目を更新する**UpdateCategory**メソッドを指定します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    GridView のいる datakeynames 属性は、モデルバインドオブジェクトを一意に識別するメンバーであることを定義します。この属性は、update メソッドが少なくとも受信する必要があるパラメーターです。
2. **Products.aspx.cs**分離コードファイルを開き、 **UpdateCategory**メソッドを実装します。 メソッドは、現在のカテゴリを読み込むためにカテゴリ ID を受け取り、GridView から値を設定して、カテゴリを更新する必要があります。

    (コードスニペット- *Web フォーム Ex01-UpdateCategory*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    ページクラスの新しい**TryUpdateModel**メソッドは、ページ内のコントロールの値を使用して、モデルオブジェクトに値を設定します。 この場合、更新された値は、編集中の現在の GridView 行から**category**オブジェクトに置き換えられます。

    > [!NOTE]
    > 次の演習では、オブジェクトの編集時にユーザーが入力したデータを検証するための ModelState. IsValid の使用方法について説明します。
3. サイトを実行し、[製品] ページにアクセスします。 カテゴリを編集します。 新しい名前を入力し、 **[更新]** をクリックして変更を保存します。

    ![カテゴリの編集](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "カテゴリの編集")

    *カテゴリの編集*

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a>演習 2: データの検証

この演習では、ASP.NET 4.5 の新しいデータ検証機能について説明します。 新しい控えめな検証機能については、Web フォームをご覧ください。 ユーザー入力の検証には、アプリケーションモデルクラスのデータ注釈を使用します。最後に、ページ内の個々のコントロールに対する要求の検証をオンまたはオフにする方法について学習します。

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a>タスク 1-控えめな検証

検証コントロールなどの複雑なデータを含むフォームでは、ページ内の JavaScript コードの生成回数が多すぎる傾向があります。これは、コードの約60% を表す可能性があります。 控えめな検証が有効になっていると、HTML コードはすっきりと tidier に見えます。

このセクションでは、ASP.NET で控えめな検証を有効にして、両方の構成で生成された HTML コードを比較します。

1. **Visual Studio 2012**を開き、このラボの ソース の **開始** フォルダーにある **開始** ソリューションを開きます。 または、前の演習の既存のソリューションで作業を続行することもできます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、ソリューションエクスプローラーで、 **[Web フォームラボ]** プロジェクト **[NuGet パッケージの管理]** をクリックします。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **F5**キーを押して web アプリケーションを起動します。 顧客 ページにアクセスし、**新しい顧客の追加** リンクをクリックします。
3. ブラウザーページを右クリックし、[ソースの**表示**] オプションを選択して、アプリケーションによって生成された HTML コードを開きます。

    ![ページの HTML コードを表示する](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "ページの HTML コードを表示する")

    *ページの HTML コードを表示する*
4. ページのソースコードをスクロールして、検証を実行してエラー一覧を表示するために、ASP.NET によって JavaScript コードとデータ検証コントロールがページに挿入されていることを確認します。

    ![[顧客の詳細] ページの検証 JavaScript コード](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "[顧客の詳細] ページの検証 JavaScript コード")

    *[顧客の詳細] ページの検証 JavaScript コード*
5. ブラウザーを閉じて、Visual Studio に戻ります。
6. 次に、控えめな検証を有効にします。 Web.config**を開き、** **AppSettings**セクションで**validationsettings: UnobtrusiveValidationMode** key を**見つけます。** キーの値を**WebForms**に設定します。

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > また、一部のページに対してのみ控えめな検証を有効にする場合は、[&quot;] ページでこのプロパティを設定して&quot; イベント **\_読み込む**こともできます。
7. [**顧客の詳細] .aspx**を開き、 **F5**キーを押して Web アプリケーションを起動します。
8. F12 キーを押して、IE 開発者ツールを開きます。 開発者ツールが開いたら、スクリプト タブを選択します。メニューから **顧客詳細** を選択し、ページで jQuery を実行するために必要なスクリプトがローカルサイトからブラウザーに読み込まれていることを確認します。

    ![ローカル IIS サーバーから直接 jQuery JavaScript ファイルを読み込む](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "ローカル IIS サーバーから直接 jQuery JavaScript ファイルを読み込む")

    *ローカル IIS サーバーから直接 jQuery JavaScript ファイルを読み込む*
9. ブラウザーを閉じて、Visual Studio に戻ります。 もう一度、**サイトの .master**ファイルを開き、 **ScriptManager**を見つけます。 属性**Enablecdn**プロパティに値**True**を追加します。 これにより、ローカルサイトの URL からではなく、オンライン URL から jQuery が読み込まれるようになります。
10. Visual Studio で [**顧客の詳細] .aspx**を開きます。 F5 キーを押してサイトを実行します。 Internet Explorer が開いたら、F12 キーを押して開発者ツールを開きます。 **[スクリプト]** タブを選択し、ドロップダウンリストを確認します。 JQuery JavaScript ファイルはローカルサイトから読み込まれなくなりますが、オンライン jQuery CDN から読み込まれることに注意してください。

    ![CDN からの jQuery JavaScript ファイルの読み込み](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "CDN からの jQuery JavaScript ファイルの読み込み")

    *CDN からの jQuery JavaScript ファイルの読み込み*
11. ブラウザーで [ソースの表示] オプションを使用して、HTML ページのソースコードをもう一度開きます。 控えめな検証 ASP.NET を有効にすると、挿入された JavaScript コードがデータ \*属性に置き換えられていることに注意してください。

    ![控えめに検証するコード](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "控えめに検証するコード")

    *控えめに検証するコード*

    > [!NOTE]
    > この例では、データ注釈付きの検証の概要がいくつかの HTML および JavaScript の行に簡略化されています。 以前は、控えめな検証を行わないと、追加する検証コントロールが増えるにつれて、JavaScript の検証コードが大きくなります。

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a>タスク 2-データ注釈を使用してモデルを検証する

ASP.NET 4.5 では、Web フォームのデータ注釈の検証について説明します。 各入力に対して検証コントロールを作成するのではなく、モデルクラスで制約を定義し、すべての web アプリケーションで使用できるようになりました。 このセクションでは、データ注釈を使用して、顧客の新規/編集フォームを検証する方法について説明します。

1. [**顧客の詳細] .aspx**ページを開きます。 **EditItemTemplate**セクションと**insertitemposition**セクションの顧客名と2番目の名前は、RequiredFieldValidator コントロールを使用して検証されることに注意してください。 各検証コントロールは特定の条件に関連付けられているため、確認する条件として複数の検証コントロールを含める必要があります。
2. Customer モデルクラスを検証するためのデータ注釈を追加します。 **モデル**フォルダーの**Customer.cs**クラスを開き、データ注釈の属性を使用して各プロパティを*装飾*します。

    (コードスニペット- *Web フォーム Ex02-データ注釈*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > .NET Framework 4.5 により、既存のデータ注釈のコレクションが拡張されました。 使用できるデータ注釈の一部を次に示します。 [CreditCard]、[Phone]、[EmailAddress]、[Range]、[Compare]、[Url]、[FileExtensions]、[Required]、 [Key]、[RegularExpression]。
    > 
    > いくつかの使用例を次に示します。
    > 
    > [Key]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > 各属性内に独自のエラーメッセージを定義することもできます。
3. RequiredFieldValidators**を開き、** FormView コントロールの EditItemTemplate セクションと insertitemposition セクションで、first name フィールドと last name フィールドのすべてのを削除します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > データ注釈を使用する利点の1つは、アプリケーションページで検証ロジックが複製されないことです。 モデルに一度定義し、データを操作するすべてのアプリケーションページで使用します。
4. [**顧客の詳細] .aspx**分離コードを開き、SaveCustomer メソッドを見つけます。 このメソッドは、新しい顧客を挿入するときに呼び出され、FormView コントロール値から Customer パラメーターを受け取ります。 ページコントロールとパラメーターオブジェクトの間のマッピングが発生すると、ASP.NET はすべてのデータ注釈属性に対してモデル検証を実行し、ModelState ディクショナリに発生したエラーがある場合はそれを入力します。

    ModelState. IsValid は、検証を実行した後、モデルのすべてのフィールドが有効な場合にのみ true を返します。

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. 顧客の詳細 ページの最後に  **Validationsummary** コントロールを追加して、モデルエラーの一覧を表示します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    **Showmodelstateerrors**は、validationsummary コントロールの新しいプロパティです。 **true**に設定すると、コントロールに modelstate ディクショナリからのエラーが表示されます。 これらのエラーは、データ注釈の検証から取得されます。
6. **F5**キーを押して Web アプリケーションを実行します。 いくつかの誤った値を指定してフォームに入力し、 **[保存]** をクリックして検証を実行します。 下部にエラーの概要が表示されます。

    ![データ注釈を使用した検証](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "データ注釈を使用した検証")

    *データ注釈を使用した検証*

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a>タスク 3-ModelState を使用してカスタムデータベースエラーを処理する

以前のバージョンの Web フォームでは、長い文字列や一意のキー違反などのデータベースエラーを処理する場合、リポジトリコードで例外をスローし、コードビハインドで例外を処理してエラーを表示することがあります。 比較的単純な操作を実行するには、コードの大部分が必要です。

Web フォーム4.5 では、ModelState オブジェクトを使用して、モデルまたはデータベースから、一貫性のある方法でページのエラーを表示できます。

このタスクでは、データベースの例外を適切に処理し、ModelState オブジェクトを使用してユーザーに適切なメッセージを表示するコードを追加します。

1. アプリケーションがまだ実行中の場合は、重複する値を使用してカテゴリの名前を更新してみてください。

    ![重複する名前を持つカテゴリの更新](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "重複する名前を持つカテゴリの更新")

    *重複する名前を持つカテゴリの更新*

    &quot;は、**区分**列の一意の&quot; 制約があるため、例外がスローされることに注意してください。

    ![重複するカテゴリ名の例外](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "重複するカテゴリ名の例外")

    *重複するカテゴリ名の例外*
2. デバッグを停止します。 **Products.aspx.cs**分離コードファイルで、 **UpdateCategory**メソッドを更新して、db によってスローされた例外を処理します。SaveChanges () メソッドを呼び出し、 **Modelstate**オブジェクトにエラーを追加します。

    新しい**TryUpdateModel**メソッドは、ユーザーが指定したフォームデータを使用して、データベースから取得したカテゴリオブジェクトを更新します。

    (コードスニペット- *Web フォーム Ex02-UpdateCategory Handle エラー*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > 理想的には、DbUpdateException の原因を特定し、根本原因が一意キー制約の違反であるかどうかを確認する必要があります。
3. **Products**を開き、[カテゴリ] GridView の下に**validationsummary**コントロールを追加して、モデルエラーの一覧を表示します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. サイトを実行し、[製品] ページにアクセスします。 重複する値を使用して、カテゴリの名前を更新してみてください。

    例外が処理され、 **Validationsummary**コントロールにエラーメッセージが表示されることに注意してください。

    ![重複したカテゴリエラー](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "重複したカテゴリエラー")

    *重複したカテゴリエラー*

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a>タスク 4-ASP.NET Web フォーム4.5 での要求の検証

ASP.NET の要求検証機能は、クロスサイトスクリプティング (XSS) 攻撃に対して一定レベルの既定の保護を提供します。 以前のバージョンの ASP.NET では、要求の検証は既定で有効になっており、ページ全体に対してのみ無効にすることができました。 新しいバージョンの ASP.NET Web フォームを使用すると、1つのコントロールの要求の検証を無効にしたり、レイジー要求の検証を実行したり、検証されていない要求データにアクセスしたりできます (これを行う場合は注意してください)。

1. Ctrl キーを押し**ながら F5**キーを押して、デバッグなしでサイトを起動し、[製品] ページにアクセスします。 カテゴリを選択し、いずれかの製品の **[編集]** リンクをクリックします。
2. 危険性のあるコンテンツを含む説明を入力します。たとえば、HTML タグを含めます。 要求の検証によってスローされた例外を確認します。

    ![危険性のあるコンテンツを含む製品の編集](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "危険性のあるコンテンツを含む製品の編集")

    *危険性のあるコンテンツを含む製品の編集*

    ![要求の検証により例外がスローされました](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "要求の検証により例外がスローされました")

    *要求の検証により例外がスローされました*
3. ページを閉じ、Visual Studio で SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。
4. **Productdetails .aspx**ページを開き、 **[説明]** ボックスを見つけます。
5. 新しい**ValidateRequestMode**プロパティをテキストボックスに追加し、その値を **[無効]** に設定します。

    新しい**ValidateRequestMode**属性を使用すると、各コントロールの要求の検証を無効にすることができます。 これは、HTML コードを受け取る可能性があるものの、ページの残りの部分では検証の動作を維持する必要がある入力を使用する場合に便利です。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. **F5**キーを押して web アプリケーションを実行します。 [製品の編集] ページをもう一度開き、HTML タグを含む製品の説明を入力します。 ここで、説明に HTML コンテンツを追加できることに注意してください。

    ![製品の説明に対して要求の検証が無効になりました](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "製品の説明に対して要求の検証が無効になりました")

    *製品の説明に対して要求の検証が無効になりました*

    > [!NOTE]
    > 実稼働アプリケーションでは、ユーザーが入力した HTML コードをサニタイズして、安全な HTML タグのみが入力されていることを確認する必要があります (たとえば、&lt;スクリプト&gt; タグはありません)。 これを行うには、 [Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS)を使用します。
7. 製品をもう一度編集します。 名前 フィールドに HTML コードを入力し、**保存** をクリックします。 要求の検証は説明フィールドに対してのみ無効になっており、残りのフィールドは危険な可能性のあるコンテンツに対して引き続き検証されます。

    ![残りのフィールドで、要求の検証が有効になります。](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "残りのフィールドで、要求の検証が有効になります。")

    *残りのフィールドで、要求の検証が有効になります。*

    ASP.NET Web フォーム4.5 には、要求の検証を遅延させる新しい要求検証モードが含まれています。 要求の検証モードが**4.5**に設定されている場合、コードの一部が ASP.NET *[&quot;key&quot;]* にアクセスすると、フォームコレクション内の特定の要素に対する要求の検証のみがトリガーされます。

    さらに、ASP.NET 4.5 には、Microsoft の XSS ライブラリ v4.0 のコアエンコードルーチンが含まれるようになりました。 XSS 防止エンコードルーチンは、新しい**system.web. web.config**名前空間で検出された新しい*アンチ Xssenプログラマ*型によって実装されます。 **EncoderType**パラメーターを使用するように構成されている場合は、ASP.NET 内の*すべての出力*エンコードによって、新しいエンコードルーチンが自動的に使用されます。
8. ASP.NET 4.5 要求の検証では、要求データへの検証されていないアクセスもサポートされています。 ASP.NET 4.5 は、**未検証**という**HttpRequest**オブジェクトに新しいコレクションプロパティを追加します。 **未検証**に移動すると、フォーム、Querystrings、Cookie、url など、要求データのすべての共通部分にアクセスできます。

    ![未検証オブジェクト](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "未検証オブジェクト")

    *未検証オブジェクト*

    > [!NOTE]
    > **未検証プロパティは注意して使用してください。** 生の要求データに対してカスタム検証を慎重に実行して、危険なテキストがラウンドトリップされず、疑いのない顧客に返されることを確認してください。

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a>演習 3: ASP.NET Web フォームでの非同期ページ処理

この演習では、ASP.NET Web フォームの新しい非同期ページ処理機能について紹介します。

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a>タスク 1-[製品の詳細] ページを更新してイメージをアップロードして表示する

このタスクでは、製品の詳細ページを更新して、ユーザーが製品のイメージの URL を指定し、読み取り専用のビューに表示できるようにします。 指定されたイメージを同期的にダウンロードして、ローカルコピーを作成します。 次のタスクでは、この実装を更新して非同期的に動作するようにします。

1. **Visual Studio 2012**を開き、このラボのフォルダーから**開始**して、ソースにある**begin**ソリューションを読み込みます。 または、前の演習の既存のソリューションで作業を続行することもできます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、ソリューションエクスプローラーで、 **[Webフォームラボ]** プロジェクトをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **Productdetails .aspx**ページソースを開き、FormView の ItemTemplate にフィールドを追加して、製品の画像を表示します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. フィールドを追加して、FormView の EditTemplate に画像の URL を指定します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. **ProductDetails.aspx.cs**分離コードファイルを開き、次の名前空間ディレクティブを追加します。

    (コードスニペット- *Web フォーム Ex03-名前空間*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. リモートイメージをローカル**イメージ**フォルダーに格納する**UpdateProductImage**メソッドを作成し、[新しいイメージの場所] の値を使用して product エンティティを更新します。

    (コードスニペット- *Web フォーム Ex03-UpdateProductImage*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. **UpdateProductImage**メソッドを呼び出すように**updateproduct**メソッドを更新します。

    (コードスニペット- *Web フォーム Ex03-UpdateProductImage 呼び出し*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. アプリケーションを実行して、製品のイメージをアップロードします。 たとえば、Office クリップアートから次の画像の URL を使用できます: [ [http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)

    ![製品のイメージの設定](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "製品のイメージの設定")

    *製品のイメージの設定*

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a>タスク 2-[製品の詳細] ページに非同期処理を追加する

このタスクでは、[製品の詳細] ページを更新して、非同期で動作するようにします。 ASP.NET 4.5 の非同期ページ処理を使用して、実行時間の長いタスク (イメージのダウンロードプロセス) を強化します。

Web アプリケーションの非同期メソッドは、ASP.NET スレッドプールの使用方法を最適化するために使用できます。 ASP.NET では、要求に参加するためのスレッドの数には制限があります。したがって、すべてのスレッドがビジー状態になると、ASP.NET は新しい要求を拒否し、アプリケーションエラーメッセージを送信して、サイトを使用できなくなります。

Web サイトでの時間のかかる操作は、割り当てられたスレッドを長時間にわたって占有するため、非同期プログラミングに適しています。 これには、データベースに対するクエリや外部 web サーバーへのアクセスなど、オフライン操作を必要とする多数の異なる要素やページを含むページが長時間要求されることが含まれます。 これらの操作に非同期メソッドを使用すると、ページの処理中にスレッドが解放されてスレッドプールに戻され、新しいページ要求への参加に使用できるという利点があります。 つまり、ページはスレッドプールからの1つのスレッドで処理を開始し、非同期処理が完了すると、別のスレッドで処理が完了する可能性があります。

1. **Productdetails .aspx**ページを開きます。 **Async**属性を**Page**要素に追加し、 **true**に設定します。 この属性は、IHttpAsyncHandler インターフェイスを実装するように ASP.NET に指示します。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. ページの下部にラベルを追加すると、ページを実行しているスレッドの詳細が表示されます。

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. **ProductDetails.aspx.cs**を開き、次の名前空間ディレクティブを追加します。

    (コードスニペット- *Web フォーム Ex03-名前空間 2*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. 非同期タスクを使用してイメージをダウンロードするように**UpdateProductImage**メソッドを変更します。 **WebClient** **Downloadfile**メソッドを**downloadfiletaskasync**メソッドに置き換え、 **await**キーワードを含めます。

    (コードスニペット- *Web フォーム Ex03-UpdateProductImage Async*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    RegisterAsyncTask は、別のスレッドで実行される新しいページ非同期タスクを登録します。 このメソッドは、実行するタスク (t) を含むラムダ式を受け取ります。 **Downloadfiletaskasync**メソッドの**await**キーワードは、 **downloadfiletaskasync**メソッドが完了した後に非同期的に呼び出されるコールバックにメソッドの残りの部分を変換します。 ASP.NET は、すべての HTTP 要求の元の値を自動的に維持することで、メソッドの実行を再開します。 .NET 4.5 の新しい非同期プログラミングモデルを使用すると、同期コードと非常によく似た非同期コードを記述し、コンパイラがコールバック関数または継続コードの複雑さを処理できるようにすることができます。
    > [!NOTE]
    > RegisterAsyncTask と PageAsyncTask は、.NET 2.0 以降で既に利用できました。 Await キーワードは、.NET 4.5 の非同期プログラミングモデルの新しいものであり、.NET WebClient オブジェクトの新しい TaskAsync メソッドと共に使用できます。
5. コードを追加して、コードが開始され、実行が完了したスレッドを表示します。 これを行うには、次のコードを使用して**UpdateProductImage**メソッドを更新します。

    (コードスニペット- *Web フォーム Ex03-スレッドの表示*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. **Web サイトの web.config ファイルを**開きます。 次の appSetting 変数を追加します。

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. **F5**キーを押してアプリケーションを実行し、製品のイメージをアップロードします。 コードが開始および終了したスレッド ID が異なる場合があることに注意してください。 これは、非同期タスクは ASP.NET スレッドプールとは別のスレッドで実行されるためです。 タスクが完了すると、ASP.NET はタスクをキューに戻し、使用可能なすべてのスレッドを割り当てます。

    ![画像を非同期的にダウンロードする](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "画像を非同期的にダウンロードする")

    *画像を非同期的にダウンロードする*

> [!NOTE]
> また、 [「付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixB)」に従って、このアプリケーションを Azure にデプロイすることもできます。

---

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボでは、次の概念について説明しました。

- 厳密に型指定されたデータバインディング式を使用する
- Web フォームでの新しいモデルバインド機能の使用
- ページデータを分離コードメソッドにマップするための値プロバイダーの使用
- ユーザー入力の検証にデータ注釈を使用する
- Web フォームの jQuery を使用した控えめなクライアント側の検証を活用する
- 詳細な要求の検証を実装する
- Web フォームでの非同期ページ処理の実装

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>付録 A: Visual Studio Express 2012 を Web 用にインストールする

**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。 次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、 <em>AZURE SDK&quot;で web 用に 2012 Visual Studio Express を</em>検索 &quot;ことができます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![Visual Studio Express のインストール](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Visual Studio Express のインストール")

    *Visual Studio Express のインストール*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![Installation progress](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。
8. Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。

    ![VS Express for Web タイル](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    *VS Express for Web タイル*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>付録 B: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

この付録では、azure によって提供される Web 配置公開機能を活用して、Azure Portal から新しい web サイトを作成し、取得したアプリケーションを発行する方法について説明します。

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>タスク 1-Azure Portal から新しい Web サイトを作成する

1. [Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。

    > [!NOTE]
    > Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。 [ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。

    ![Windows Azure portal にログオンします。](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Windows Azure portal にログオンします。")

    *ポータルへのログオン*
2. コマンドバーの **[新規]** をクリックします。

    ![新しい Web サイトの作成](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "新しい Web サイトの作成")

    *新しい Web サイトの作成*
3. [ **Compute** | **Web サイト**] をクリックします。 次に、 **[簡易作成]** オプションを選択します。 新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。

    > [!NOTE]
    > Azure は、管理および管理が可能なクラウドで実行されている web アプリケーションのホストです。 [簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Azure にデプロイできます。 データベースを設定する手順は含まれていません。

    ![簡易作成を使用した新しい Web サイトの作成](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "簡易作成を使用した新しい Web サイトの作成")

    *簡易作成を使用した新しい Web サイトの作成*
4. 新しい**Web サイト**が作成されるまで待ちます。
5. Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。 新しい Web サイトが機能していることを確認します。

    ![新しい web サイトを参照しています](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "新しい web サイトを参照しています")

    *新しい web サイトを参照しています*

    ![実行中の Web サイト](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "実行中の Web サイト")

    *実行中の Web サイト*
6. ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。

    ![Web サイトの管理ページを開く](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "Web サイトの管理ページを開く")

    *Web サイトの管理ページを開く*
7. **[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。

    > [!NOTE]
    > *発行プロファイル*には、有効になっている各発行方法について、Azure に web アプリケーションを発行するために必要なすべての情報が含まれています。 発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Azure に発行するためのこれらのプログラムの構成を自動化することがサポートされています。

    ![Web サイト発行プロファイルをダウンロードしています](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "Web サイト発行プロファイルをダウンロードしています")

    *Web サイト発行プロファイルをダウンロードしています*
8. 発行プロファイルファイルを既知の場所にダウンロードします。 この演習では、このファイルを使用して Visual Studio から Azure に web アプリケーションを発行する方法について説明します。

    ![発行プロファイルファイルを保存しています](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "発行プロファイルを保存しています")

    *発行プロファイルファイルを保存しています*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>タスク 2-データベースサーバーの構成

アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。 SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。

1. アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。 Azure 管理ポータルのサブスクリプションから**SQL Database サーバーを**表示するには、 **SQL データベース** | サーバー | **サーバーのダッシュボード**を参照してください。 サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。 次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。 データベースは、後の段階で作成されるため、まだ作成しないでください。

    ![SQL Database サーバーダッシュボード](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database サーバーダッシュボード")

    *SQL Database サーバーダッシュボード*
2. 次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。 これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) 追加] をクリックします。

    ![クライアント IP アドレスを追加しています](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    *クライアント IP アドレスを追加しています*
3. [許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。

    ![変更の確認](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    *変更の確認*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

1. ASP.NET MVC 4 ソリューションに戻ります。 **ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。

    ![アプリケーションの発行](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "アプリケーションの発行")

    *Web サイトの公開*
2. 最初のタスクで保存した発行プロファイルをインポートします。

    ![発行プロファイルをインポートしています](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "発行プロファイルをインポートしています")

    *発行プロファイルをインポートしています*
3. **[接続の検証]** をクリックします。 検証が完了したら、 **[次へ]** をクリックします。

    > [!NOTE]
    > 検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。

    ![接続の検証](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "接続の検証")

    *接続の検証*
4. **[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。

    ![Web deploy の構成](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web deploy の構成")

    *Web deploy の構成*
5. 次のようにデータベース接続を構成します。

   - **サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。
   - **User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。
   - **パスワード**で、サーバー管理者のログインパスワードを入力します。
   - 新しいデータベース名を入力します。

     ![変換先の接続文字列を構成しています](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "変換先の接続文字列を構成しています")

     *変換先の接続文字列を構成しています*
6. 次に、 **[OK]** をクリックします データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。

    ![データベースの作成](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "データベース文字列の作成")

    *データベースの作成*
7. Azure で SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。 続けて、 **[次へ]** をクリックします。

    ![SQL Database を指す接続文字列](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "SQL Database を指す接続文字列")

    *SQL Database を指す接続文字列*
8. **[プレビュー]** ページで、 **[発行]** をクリックします。

    ![Web アプリケーションの発行](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "Web アプリケーションの発行")

    *Web アプリケーションの発行*
9. 発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>付録 C: コードスニペットの使用

コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。 次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。

![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")

*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*

***キーボードを使用してコードスニペットを追加C#するには (のみ)***

1. コードを挿入する場所にカーソルを置きます。
2. (スペースまたはハイフンを含まない) スニペット名の入力を開始します。
3. IntelliSense によって、一致するスニペットの名前が表示されます。
4. 正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。
5. Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。

![スニペット名の入力を開始します](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "スニペット名の入力を開始します")

*スニペット名の入力を開始します*

![Tab キーを押して、強調表示されているスニペットを選択します](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Tab キーを押して、強調表示されているスニペットを選択します")

*Tab キーを押して、強調表示されているスニペットを選択します*

![もう一度 Tab キーを押すと、スニペットが展開されます。](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "もう一度 Tab キーを押すと、スニペットが展開されます。")

*もう一度 Tab キーを押すと、スニペットが展開されます。*

***マウスC#(、Visual Basic および XML) を使用してコードスニペットを追加するに***は1. コードスニペットを挿入する場所を右クリックします。

1. **[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。
2. 一覧から該当するスニペットをクリックして選択します。

![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")

*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*

![一覧から関連するスニペットをクリックして選択します。](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "一覧から関連するスニペットをクリックして選択します。")

*一覧から関連するスニペットをクリックして選択します。*

---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-cs
title: データアクセス層の接続レベルとコマンドレベルの設定を構成するC#() |Microsoft Docs
author: rick-anderson
description: 型指定されたデータセット内の Tableadapter は、データベースへの接続、コマンドの発行、および結果を含む DataTable へのデータの読み込みを自動的に行います...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: cd330dd9-6254-4305-9351-dd727384c83b
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-cs
msc.type: authoredcontent
ms.openlocfilehash: 8fe7a5a2e410b47c8c2be62851f2b7b775d60209
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78444388"
---
# <a name="configuring-the-data-access-layers-connection--and-command-level-settings-c"></a>データ アクセス層の接続レベルとコマンド レベルの設定を構成する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_72_CS.zip)または[PDF のダウンロード](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/datatutorial72cs1.pdf)

> 型指定されたデータセット内の Tableadapter は、データベースへの接続、コマンドの発行、および結果の DataTable へのデータの読み込みを自動的に行います。 ただし、これらの詳細を自分で処理する必要がある場合もあります。このチュートリアルでは、TableAdapter のデータベース接続とコマンドレベルの設定にアクセスする方法について説明します。

## <a name="introduction"></a>はじめに

チュートリアルシリーズ全体で、型指定されたデータセットを使用して、階層型アーキテクチャのデータアクセス層とビジネスオブジェクトを実装しました。 [最初のチュートリアル](../introduction/creating-a-data-access-layer-cs.md)で説明したように、型指定されたデータセットの datatable はデータのリポジトリとして機能しますが、tableadapter はデータベースと通信して基になるデータを取得および変更するラッパーとして機能します。 Tableadapter は、データベースの操作に関係する複雑さをカプセル化し、データベースに接続したり、コマンドを発行したり、結果を DataTable に入力したりするコードを記述する必要がなくなります。

ただし、TableAdapter の深さに burrow し、ADO.NET オブジェクトと直接連携するコードを記述する必要がある場合もあります。 たとえば、[トランザクション内でのデータベースの変更のラップ](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md)に関するチュートリアルでは、ADO.NET トランザクションを開始、コミット、およびロールバックするためのメソッドを TableAdapter に追加しました。 これらのメソッドでは、TableAdapter の `SqlCommand` オブジェクトに割り当てられた、内部的に作成された `SqlTransaction` オブジェクトが使用されていました。

このチュートリアルでは、TableAdapter のデータベース接続とコマンドレベルの設定にアクセスする方法を確認します。 特に、基になる接続文字列とコマンドタイムアウト設定へのアクセスを可能にする機能を `ProductsTableAdapter` に追加します。

## <a name="working-with-data-using-adonet"></a>ADO.NET を使用したデータの操作

Microsoft .NET Framework には、特にデータを操作するように設計された多数のクラスが含まれています。 これらのクラスは[`System.Data` 名前空間](https://msdn.microsoft.com/library/system.data.aspx)内にあり、 *ADO.NET*クラスと呼ばれます。 ADO.NET の一部のクラスは、特定の*データプロバイダー*に関連付けられています。 データプロバイダーは、ADO.NET クラスと基になるデータストアの間の情報フローを可能にする通信チャネルと考えることができます。 OleDb や ODBC などの一般化されたプロバイダーと、特定のデータベースシステム向けに特別に設計されたプロバイダーがあります。 たとえば、OleDb プロバイダーを使用して Microsoft SQL Server データベースに接続することは可能ですが、SqlClient プロバイダーは SQL Server 専用に設計および最適化されているため、はるかに効率的です。

プログラムによってデータにアクセスする場合は、次のパターンが一般的に使用されます。

- データベースへの接続を確立します。
- コマンドを実行します。
- `SELECT` クエリの場合は、結果として得られるレコードを操作します。

これらの各手順を実行するための個別の ADO.NET クラスがあります。 たとえば、SqlClient プロバイダーを使用してデータベースに接続するには、 [`SqlConnection` クラス](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection(VS.80).aspx)を使用します。 `INSERT`、`UPDATE`、`DELETE`、または `SELECT` コマンドをデータベースに発行するには、 [`SqlCommand` クラス](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx)を使用します。

[トランザクションでのデータベースの変更のラッピング](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md)に関するチュートリアルでは、tableadapter の自動生成コードには、データベースへの接続、コマンドの発行、データの取得、および datatable へのデータの読み込みに必要な機能が含まれているため、低レベルの ADO.NET コードを作成する必要はありませんでした。 ただし、これらの低レベルの設定をカスタマイズする必要がある場合もあります。 次のいくつかの手順で、Tableadapter によって内部的に使用される ADO.NET オブジェクトを活用する方法を確認します。

## <a name="step-1-examining-with-the-connection-property"></a>手順 1: 接続プロパティを使用して検査する

各 TableAdapter クラスには、データベース接続情報を指定する `Connection` プロパティがあります。 このプロパティのデータ型と `ConnectionString` 値は、TableAdapter 構成ウィザードで選択した値によって決まります。 最初に、型指定されたデータセットに TableAdapter を追加すると、このウィザードではデータベースソースを入力するように求められます (図1を参照)。 この最初の手順のドロップダウンリストには、構成ファイルで指定されたデータベースと、サーバーエクスプローラー s データ接続内の他のデータベースが含まれます。 使用するデータベースがドロップダウンリストに存在しない場合は、[新しい接続] ボタンをクリックし、必要な接続情報を入力して、新しいデータベース接続を指定できます。

[TableAdapter 構成ウィザードの最初の手順 ![](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image2.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image1.png)

**図 1**: TableAdapter 構成ウィザードの最初の手順 ([クリックすると、フルサイズの画像が表示](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image3.png)されます)

では、TableAdapter s `Connection` プロパティのコードを調べてみましょう。 「[データアクセス層の作成](../introduction/creating-a-data-access-layer-cs.md)」チュートリアルで説明したように、[クラスビュー] ウィンドウに移動し、適切なクラスにドリルダウンして、メンバー名をダブルクリックすると、自動生成された TableAdapter コードを表示できます。

[表示] メニューに移動して [クラスビュー] を選択するか、Ctrl + Shift + C キーを押してクラスビューウィンドウに移動します。 クラスビューウィンドウの上半分で `NorthwindTableAdapters` 名前空間にドリルダウンし、`ProductsTableAdapter` クラスを選択します。 これにより、図2に示すように、クラスビューの下半分に `ProductsTableAdapter` s メンバーが表示されます。 [`Connection`] プロパティをダブルクリックして、そのコードを表示します。

![クラスビューの [接続] プロパティをダブルクリックして、自動生成されたコードを表示します。](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image4.png)

**図 2**: クラスビューの [接続] プロパティをダブルクリックして、自動生成されたコードを表示する

TableAdapter の `Connection` プロパティおよびその他の接続関連のコードは、次のようになります。

[!code-csharp[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/samples/sample1.cs)]

TableAdapter クラスがインスタンス化されると、メンバー変数 `_connection` が `null`と等しくなります。 `Connection` プロパティにアクセスすると、まず、`_connection` メンバー変数がインスタンス化されているかどうかを確認します。 そうでない場合は、`InitConnection` メソッドが呼び出されます。このメソッドは、`_connection` をインスタンス化し、`ConnectionString` プロパティを TableAdapter 構成ウィザードの最初の手順で指定した接続文字列値に設定します。

`Connection` プロパティは、`SqlConnection` オブジェクトに割り当てることもできます。 これにより、新しい `SqlConnection` オブジェクトが各 TableAdapter の `SqlCommand` オブジェクトに関連付けられます。

## <a name="step-2-exposing-connection-level-settings"></a>手順 2: 接続レベルの設定を公開する

接続情報は TableAdapter 内にカプセル化され、アプリケーションアーキテクチャの他の層からはアクセスできません。 ただし、クエリ、ユーザー、または ASP.NET ページに対して、TableAdapter の接続レベル情報にアクセスしたり、カスタマイズしたりする必要がある場合もあります。

では、`Northwind` データセット内の `ProductsTableAdapter` を拡張して、TableAdapter によって使用される接続文字列の読み取りや変更を行うためにビジネスロジック層で使用できる `ConnectionString` プロパティを含めるようにします。

> [!NOTE]
> *接続文字列*は、使用するプロバイダー、データベースの場所、認証の資格情報、およびその他のデータベース関連の設定など、データベース接続情報を指定する文字列です。 さまざまなデータストアとプロバイダーで使用される接続文字列パターンの一覧については、「 [ConnectionStrings.com](http://www.connectionstrings.com/)」を参照してください。

[データアクセス層の作成](../introduction/creating-a-data-access-layer-cs.md)に関するチュートリアルで説明したように、型指定されたデータセットの自動生成クラスは、部分クラスを使用して拡張できます。 最初に、`~/App_Code/DAL` フォルダーの下にある `ConnectionAndCommandSettings` という名前のプロジェクトに新しいサブフォルダーを作成します。

![ConnectionAndCommandSettings という名前のサブフォルダーを追加します。](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image5.png)

**図 3**: `ConnectionAndCommandSettings` という名前のサブフォルダーを追加する

`ProductsTableAdapter.ConnectionAndCommandSettings.cs` という名前の新しいクラスファイルを追加し、次のコードを入力します。

[!code-csharp[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/samples/sample2.cs)]

この部分クラスは、`ConnectionString` という名前の `public` プロパティを `ProductsTableAdapter` クラスに追加します。これにより、任意のレイヤーが TableAdapter の基になる接続の接続文字列を読み取りまたは更新できるようになります。

この部分クラスが作成され、保存されたので、`ProductsBLL` クラスを開きます。 既存のメソッドのいずれかに移動し `Adapter` を入力し、ピリオドキーを押すと、IntelliSense が表示されます。 IntelliSense で使用できる新しい `ConnectionString` プロパティが表示されます。つまり、BLL からこの値をプログラムによって読み取ったり調整したりすることができます。

## <a name="exposing-the-entire-connection-object"></a>接続オブジェクト全体の公開

この部分クラスは、基になる接続オブジェクトのプロパティを1つだけ公開します: `ConnectionString`。 接続オブジェクト全体を TableAdapter の範囲を超えて使用できるようにする場合は、`Connection` プロパティの保護レベルを変更することもできます。 手順 1. で検証した自動生成コードは、TableAdapter の `Connection` プロパティが `internal`としてマークされていることを示しています。つまり、同じアセンブリ内のクラスからのみアクセスできます。 ただし、これは、TableAdapter s の `ConnectionModifier` プロパティを使用して変更できます。

`Northwind` データセットを開き、デザイナーで `ProductsTableAdapter` をクリックして、プロパティウィンドウに移動します。 `ConnectionModifier` が既定値の `Assembly`に設定されていることがわかります。 `Connection` プロパティを型指定されたデータセットのアセンブリの外部で使用できるようにするには、`ConnectionModifier` プロパティを `Public`に変更します。

[接続プロパティのアクセシビリティレベルは、ConnectionModifier プロパティを使用して構成でき ![](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image7.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image6.png)

**図 4**: `Connection` プロパティのアクセシビリティレベルは、`ConnectionModifier` プロパティを使用して構成できます ([クリックすると、フルサイズの画像が表示](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/_static/image8.png)されます)。

データセットを保存し、`ProductsBLL` クラスに戻ります。 前と同様に、既存のメソッドのいずれかに移動して `Adapter` を入力し、ピリオドキーを押すと、IntelliSense が表示されます。 一覧には `Connection` プロパティが含まれている必要があります。これは、プログラムで BLL から接続レベルの設定を読み取りまたは割り当てることができることを意味します。

## <a name="step-3-examining-the-command-related-properties"></a>手順 3: コマンド関連のプロパティを調べる

TableAdapter は、既定では、自動生成された `INSERT`、`UPDATE`、および `DELETE` ステートメントを持つメインクエリで構成されます。 このメインクエリ s `INSERT`、`UPDATE`、および `DELETE` ステートメントは、`Adapter` プロパティを介して ADO.NET data adapter オブジェクトとして TableAdapter s コードに実装されています。 `Connection` プロパティと同様に、`Adapter` プロパティのデータ型は、使用するデータプロバイダーによって決まります。 これらのチュートリアルでは SqlClient プロバイダーを使用するため、`Adapter` プロパティは[`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter(VS.80).aspx)型になります。

TableAdapter s の `Adapter` プロパティには、`INSERT`、`UPDATE`、および `DELETE` ステートメントを発行するために使用する `SqlCommand` 型の3つのプロパティがあります。

- `InsertCommand`
- `UpdateCommand`
- `DeleteCommand`

`SqlCommand` オブジェクトは、特定のクエリをデータベースに送信する役割を担い、次のようなプロパティを持っています。これには、アドホック SQL ステートメントまたは実行するストアドプロシージャが含まれて[`CommandText`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtext.aspx)です。および[`Parameters`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.parameters.aspx)。これは `SqlParameter` オブジェクトのコレクションです。 [データアクセス層の作成](../introduction/creating-a-data-access-layer-cs.md)に関するチュートリアルで説明したように、これらのコマンドオブジェクトはプロパティウィンドウを使用してカスタマイズできます。

TableAdapter には、メインのクエリに加えて、指定されたコマンドをデータベースにディスパッチする、さまざまな数のメソッドを含めることができます。 その他のすべてのメソッドのメインクエリ s コマンドオブジェクトとコマンドオブジェクトは、TableAdapter s の `CommandCollection` プロパティに格納されます。

ここでは、これら2つのプロパティの `Northwind` データセットの `ProductsTableAdapter` によって生成されるコードと、そのサポートするメンバー変数とヘルパーメソッドについて説明します。

[!code-csharp[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/samples/sample3.cs)]

`Adapter` プロパティと `CommandCollection` プロパティのコードは、`Connection` プロパティのコードとよく似ています。 プロパティによって使用されるオブジェクトを保持するメンバー変数があります。 プロパティ `get` アクセサーは、対応するメンバー変数が `null`かどうかを確認することから始めます。 その場合は、初期化メソッドが呼び出されます。このメソッドは、メンバー変数のインスタンスを作成し、コマンドに関連するコアプロパティを割り当てます。

## <a name="step-4-exposing-command-level-settings"></a>手順 4: コマンドレベルの設定を公開する

理想的には、コマンドレベルの情報がデータアクセスレイヤー内にカプセル化されている必要があります。 この情報は、アーキテクチャの他のレイヤーで必要となりますが、接続レベルの設定と同様に、部分クラスを使用して公開できます。

TableAdapter には `Connection` プロパティが1つしかないため、接続レベルの設定を公開するためのコードは非常に簡単です。 TableAdapter には複数のコマンドオブジェクト (`InsertCommand`、`UpdateCommand`、および `DeleteCommand`) と、`CommandCollection` プロパティの可変個のコマンドオブジェクトを含めることができるため、コマンドレベルの設定を変更するときには少し複雑になります。 コマンドレベルの設定を更新する場合は、これらの設定をすべてのコマンドオブジェクトに反映させる必要があります。

たとえば、TableAdapter に特定のクエリを実行するのに非常に長い時間がかかっていたとします。 TableAdapter を使用してこれらのクエリの1つを実行する場合は、command オブジェクト s [`CommandTimeout` プロパティ](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtimeout.aspx)を増やすことをお勧めします。 このプロパティは、コマンドの実行を待機する秒数を指定します。既定値は30です。

BLL によって `CommandTimeout` プロパティを調整できるようにするには、手順2で作成した部分クラスファイル (`ProductsTableAdapter.ConnectionAndCommandSettings.cs`) を使用して、次の `public` メソッドを `ProductsDataTable` に追加します。

[!code-csharp[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs/samples/sample4.cs)]

このメソッドは、BLL またはプレゼンテーション層から呼び出して、その TableAdapter インスタンスによって実行されるすべてのコマンドのタイムアウトを設定することができます。

> [!NOTE]
> `Adapter` プロパティと `CommandCollection` プロパティは `private`としてマークされます。つまり、TableAdapter 内のコードからのみアクセスできます。 `Connection` プロパティとは異なり、これらのアクセス修飾子は構成できません。 したがって、コマンドレベルのプロパティをアーキテクチャ内の他のレイヤーに公開する必要がある場合は、上記の部分クラスのアプローチを使用して、`private` コマンドオブジェクトの読み取りまたは書き込みを行う `public` メソッドまたはプロパティを指定する必要があります。

## <a name="summary"></a>まとめ

型指定された DataSet 内の Tableadapter は、データアクセスの詳細と複雑さをカプセル化するために機能します。 Tableadapter を使用して、データベースに接続したり、コマンドを実行したり、DataTable に結果を設定したりするための ADO.NET コードの記述について心配する必要はありません。 すべて自動的に処理されます。

ただし、接続文字列や既定の接続やコマンドのタイムアウト値を変更するなど、低レベルの ADO.NET の詳細をカスタマイズする必要が生じる場合もあります。 TableAdapter には、`Connection`、`Adapter`、および `CommandCollection` の各プロパティが自動生成されていますが、これらは既定で `internal` または `private`です。 この内部情報を公開するには、部分クラスを使用して TableAdapter を拡張し `public` メソッドまたはプロパティを含めることができます。 また、tableadapter s `Connection` プロパティアクセス修飾子は、TableAdapter s `ConnectionModifier` プロパティを使用して構成できます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Burnadette Leigh、S ren Jacob Lauritsen、Teresa Murphy、Hilton Geisenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](working-with-computed-columns-cs.md)
> [次へ](protecting-connection-strings-and-other-configuration-information-cs.md)

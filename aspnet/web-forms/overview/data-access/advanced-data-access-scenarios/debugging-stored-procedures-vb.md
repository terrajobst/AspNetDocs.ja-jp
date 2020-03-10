---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-vb
title: ストアドプロシージャのデバッグ (VB) |Microsoft Docs
author: rick-anderson
description: Visual Studio Professional および Team System edition を使用すると、SQL Server 内のストアドプロシージャにブレークポイントを設定してステップインし、デバッグを格納することができます。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 9ed8ccb5-5f31-4eb4-976d-cabf4b45ca09
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/debugging-stored-procedures-vb
msc.type: authoredcontent
ms.openlocfilehash: 13d213ef4baf493a4f05a82daae8d2dc3b0aa61b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78443818"
---
# <a name="debugging-stored-procedures-vb"></a>ストアド プロシージャのデバッグ (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_74_VB.zip)または[PDF のダウンロード](debugging-stored-procedures-vb/_static/datatutorial74vb1.pdf)

> Visual Studio Professional および Team System edition を使用すると、SQL Server 内のストアドプロシージャにブレークポイントを設定してステップインすることができます。これにより、アプリケーションコードのデバッグと同様に、デバッグストアドプロシージャを簡単に実行できます。 このチュートリアルでは、ストアドプロシージャの直接データベースデバッグとアプリケーションデバッグについて説明します。

## <a name="introduction"></a>はじめに

Visual Studio には、豊富なデバッグ機能が用意されています。 いくつかのキーストロークやマウスのクリックを使用して、ブレークポイントを使用してプログラムの実行を停止し、その状態と制御フローを調べることができます。 Visual Studio では、アプリケーションコードのデバッグと共に、SQL Server 内からストアドプロシージャをデバッグするためのサポートを提供しています。 ブレークポイントは、ASP.NET 分離コードクラスまたはビジネスロジックレイヤークラスのコード内で設定できるのと同様に、ストアドプロシージャ内に配置することもできます。

このチュートリアルでは、Visual Studio 内のサーバーエクスプローラーからストアドプロシージャへのステップインと、実行中の ASP.NET アプリケーションからストアドプロシージャが呼び出されたときにヒットするブレークポイントを設定する方法について説明します。

> [!NOTE]
> 残念ながら、ストアドプロシージャは、Visual Studio の Professional および Team system バージョンでのみ段階的に、デバッグできます。 Visual Web Developer または standard バージョンの Visual Studio を使用している場合は、ストアドプロシージャをデバッグするために必要な手順について説明しますが、これらの手順をコンピューターでレプリケートすることはできません。

## <a name="sql-server-debugging-concepts"></a>SQL Server デバッグの概念

Microsoft SQL Server 2005 は、[共通言語ランタイム (CLR)](https://msdn.microsoft.com/netframework/aa497266.aspx)との統合を提供するように設計されています。これは、すべての .net アセンブリで使用されるランタイムです。 その結果、SQL Server 2005 ではマネージデータベースオブジェクトがサポートされます。 つまり、ストアドプロシージャやユーザー定義関数 (Udf) などのデータベースオブジェクトは、Visual Basic クラスのメソッドとして作成できます。 これにより、これらのストアドプロシージャおよび Udf は、.NET Framework と独自のカスタムクラスの機能を利用できるようになります。 もちろん、SQL Server 2005 では、T-sql データベースオブジェクトもサポートされています。

SQL Server 2005 では、T-sql オブジェクトとマネージデータベースオブジェクトの両方のデバッグサポートが提供されます。 ただし、これらのオブジェクトは、Visual Studio 2005 Professional および Team system の各エディションでのみデバッグできます。 このチュートリアルでは、T-sql database オブジェクトのデバッグについて説明します。 以降のチュートリアルでは、マネージデータベースオブジェクトのデバッグについて見ていきます。

[SQL Server 2005 CLR 統合チーム](https://blogs.msdn.com/sqlclr/default.aspx)の[SQL Server 2005 ブログエントリでの T-sql と CLR デバッグの概要](https://blogs.msdn.com/sqlclr/archive/2006/06/29/651644.aspx)については、Visual Studio から SQL Server 2005 オブジェクトをデバッグする3つの方法について説明します。

- **Direct Database デバッグ (DDD)** -サーバーエクスプローラーは、ストアドプロシージャや udf などの t-sql データベースオブジェクトにステップインできます。 DDD は、手順 1. で確認します。
- **アプリケーションのデバッグ**-データベースオブジェクト内にブレークポイントを設定し、ASP.NET アプリケーションを実行できます。 データベースオブジェクトが実行されると、ブレークポイントがヒットし、制御がデバッガーに対して有効になります。 アプリケーションのデバッグでは、アプリケーションコードからデータベースオブジェクトにステップインすることはできないことに注意してください。 デバッガーを停止するストアドプロシージャまたは Udf には、明示的にブレークポイントを設定する必要があります。 アプリケーションのデバッグは、手順 2. で開始します。
- **SQL Server のプロジェクト**Visual Studio Professional および Team Systems エディションからのデバッグには、マネージデータベースオブジェクトを作成するために一般的に使用される SQL Server のプロジェクトの種類が含まれています。 次のチュートリアルでは、SQL Server プロジェクトを使用し、その内容をデバッグします。

Visual Studio では、ローカルおよびリモートの SQL Server インスタンスでストアドプロシージャをデバッグできます。 ローカル SQL Server インスタンスは、Visual Studio と同じコンピューターにインストールされています。 使用している SQL Server データベースが開発用コンピューターに配置されていない場合は、リモートインスタンスと見なされます。 これらのチュートリアルでは、ローカル SQL Server インスタンスを使用しています。 リモート SQL server インスタンスでストアドプロシージャをデバッグするには、ローカルインスタンスでストアドプロシージャをデバッグする場合よりも多くの構成手順が必要です。

ローカル SQL Server インスタンスを使用している場合は、手順1から開始して、このチュートリアルを最後まで実行できます。 ただし、リモートの SQL Server インスタンスを使用している場合は、まず、リモートインスタンスで SQL Server ログインを持つ Windows ユーザーアカウントを使用して開発用コンピューターにログインするときに、デバッグを行う必要があります。 さらに、このデータベースログインと、実行中の ASP.NET アプリケーションからデータベースへの接続に使用されるデータベースログインの両方が、`sysadmin` ロールのメンバーである必要があります。 Visual Studio の構成と SQL Server リモートインスタンスのデバッグの詳細については、このチュートリアルの最後にある「リモートインスタンスでの T-sql SQL Database オブジェクトのデバッグ」セクションを参照してください。

最後に、T-sql database オブジェクトのデバッグサポートは、.NET アプリケーションのデバッグサポートほど豊富な機能ではないことを理解しておいてください。 たとえば、ブレークポイントの条件とフィルターはサポートされていません。デバッグウィンドウのサブセットのみ使用できます。エディットコンティニュを使用することはできません。 [イミディエイト] ウィンドウは役に立たないように表示されます。 詳細については[、「デバッガーのコマンドと機能に関する制限事項](https://msdn.microsoft.com/library/ms165035(VS.80).aspx)」を参照してください。

## <a name="step-1-directly-stepping-into-a-stored-procedure"></a>手順 1: ストアドプロシージャに直接ステップインする

Visual Studio を使用すると、データベースオブジェクトを簡単に直接デバッグできます。 ここでは、Direct Database デバッグ (DDD) 機能を使用して、Northwind データベースの `Products_SelectByCategoryID` ストアドプロシージャにステップインする方法について説明します。 名前が示すように、`Products_SelectByCategoryID` によって、特定のカテゴリの製品情報が返されます。「」では、[型指定されたデータセットの tableadapter チュートリアルに既存のストアドプロシージャを使用して](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)作成されました。 まず、サーバーエクスプローラーに移動し、Northwind データベースノードを展開します。 次に、[ストアドプロシージャ] フォルダーをドリルダウンし、`Products_SelectByCategoryID` ストアドプロシージャを右クリックして、コンテキストメニューから [ストアドプロシージャにステップイン] オプションを選択します。 これにより、デバッガーが開始されます。

`Products_SelectByCategoryID` ストアドプロシージャには `@CategoryID` 入力パラメーターが必要であるため、この値を指定するように求められます。 「1」と入力すると、飲み物に関する情報が返されます。

![@CategoryID パラメーターに値1を使用します。](debugging-stored-procedures-vb/_static/image1.png)

**図 1**: `@CategoryID` パラメーターに値1を使用する

`@CategoryID` パラメーターの値を指定すると、ストアドプロシージャが実行されます。 ただし、完了まで実行されるのではなく、デバッガーは最初のステートメントで実行を停止します。 余白の黄色の矢印は、ストアドプロシージャ内の現在の場所を示しています。 パラメーター値を表示および編集するには、ウォッチウィンドウを使用するか、ストアドプロシージャのパラメーター名の上にカーソルを合わせます。

[ストアドプロシージャの最初のステートメントでデバッガーが停止した ![](debugging-stored-procedures-vb/_static/image3.png)](debugging-stored-procedures-vb/_static/image2.png)

**図 2**: デバッガーがストアドプロシージャの最初のステートメントで停止した ([クリックすると、フルサイズの画像が表示](debugging-stored-procedures-vb/_static/image4.png)されます)

ストアドプロシージャを一度に1つずつステップ実行するには、ツールバーの [ステップオーバー] ボタンをクリックするか、F10 キーを押します。 `Products_SelectByCategoryID` ストアドプロシージャには1つの `SELECT` ステートメントが含まれているため、F10 キーを押すと、1つのステートメントがステップオーバーされ、ストアドプロシージャの実行が完了します。 ストアドプロシージャが完了すると、出力が出力ウィンドウに表示され、デバッガーが終了します。

> [!NOTE]
> T-sql のデバッグはステートメントレベルで行われます。`SELECT` ステートメントにステップインすることはできません。

## <a name="step-2-configuring-the-website-for-application-debugging"></a>手順 2: アプリケーションデバッグ用に Web サイトを構成する

ストアドプロシージャをサーバーエクスプローラーから直接デバッグすることは便利ですが、多くのシナリオでは、ストアドプロシージャが ASP.NET アプリケーションから呼び出されたときのデバッグに興味があります。 Visual Studio 内からストアドプロシージャにブレークポイントを追加し、ASP.NET アプリケーションのデバッグを開始できます。 ブレークポイントが設定されたストアドプロシージャがアプリケーションから呼び出されると、ブレークポイントで実行が停止し、ストアドプロシージャのパラメーター値を表示および変更し、ステートメントをステップ実行できます。手順1で行ったのと同じです。

アプリケーションから呼び出されたストアドプロシージャのデバッグを開始する前に、ASP.NET web アプリケーションに SQL Server デバッガーとの統合を指示する必要があります。 まず、ソリューションエクスプローラー (`ASPNET_Data_Tutorial_74_VB`) の web サイト名を右クリックします。 コンテキストメニューの [プロパティページ] オプションを選択し、左側の [開始オプション] 項目を選択して、[デバッガー] セクションの [SQL Server] チェックボックスをオンにします (図3を参照)。

[[アプリケーション] プロパティページの [SQL Server] チェックボックスをオンに ![ます。](debugging-stored-procedures-vb/_static/image6.png)](debugging-stored-procedures-vb/_static/image5.png)

**図 3**: アプリケーションのプロパティページの [SQL Server] チェックボックスをオン[にする (クリックすると、フルサイズの画像が表示](debugging-stored-procedures-vb/_static/image7.png)されます)

また、接続プールが無効になるように、アプリケーションで使用されるデータベース接続文字列を更新する必要があります。 データベースへの接続が切断されると、対応する `SqlConnection` オブジェクトが使用可能な接続のプールに配置されます。 データベースへの接続を確立するときに、新しい接続を作成して確立するのではなく、このプールから使用可能な接続オブジェクトを取得できます。 この接続オブジェクトのプーリングはパフォーマンスが向上し、既定で有効になっています。 ただし、デバッグ時には、プールから取得した接続を操作するときにデバッグインフラストラクチャが正しく再確立されないため、接続プールを無効にする必要があります。

接続プールを無効にするには、`Web.config` の `NORTHWNDConnectionString` を更新して、`Pooling=false` 設定が含まれるようにします。

[!code-xml[Main](debugging-stored-procedures-vb/samples/sample1.xml)]

> [!NOTE]
> ASP.NET アプリケーションを使用して SQL Server のデバッグを終了したら、接続文字列から `Pooling` 設定を削除して (または `Pooling=true` に設定して)、接続プールを復元してください。

この時点で、ASP.NET アプリケーションは、Visual Studio が web アプリケーションから呼び出されたときに SQL Server データベースオブジェクトをデバッグできるように構成されています。 ここまでで、ブレークポイントをストアドプロシージャに追加し、デバッグを開始します。

## <a name="step-3-adding-a-breakpoint-and-debugging"></a>手順 3: ブレークポイントとデバッグの追加

`Products_SelectByCategoryID` ストアドプロシージャを開き、`SELECT` ステートメントの先頭にブレークポイントを設定します。そのためには、適切な場所にある余白をクリックするか `SELECT` ステートメントの先頭にカーソルを置き、F9 キーを押します。 図4に示すように、ブレークポイントは、余白に赤い円として表示されます。

[Products_SelectByCategoryID ストアドプロシージャにブレークポイントを設定 ![には](debugging-stored-procedures-vb/_static/image9.png)](debugging-stored-procedures-vb/_static/image8.png)

**図 4**: `Products_SelectByCategoryID` ストアドプロシージャにブレークポイントを設定[する (クリックしてフルサイズの画像を表示する](debugging-stored-procedures-vb/_static/image10.png))

クライアントアプリケーションを使用して SQL database オブジェクトをデバッグするには、アプリケーションのデバッグをサポートするようにデータベースを構成する必要があります。 最初にブレークポイントを設定すると、この設定は自動的にオンになりますが、再度確認することをお勧めします。 サーバーエクスプローラーの [`NORTHWND.MDF`] ノードを右クリックします。 コンテキストメニューには、アプリケーションデバッグという名前のチェックされたメニュー項目が含まれている必要があります。

![[アプリケーションデバッグ] オプションが有効になっていることを確認します。](debugging-stored-procedures-vb/_static/image11.png)

**図 5**: アプリケーションのデバッグオプションが有効になっていることを確認する

ブレークポイントを設定し、[アプリケーションデバッグ] オプションを有効にすると、ASP.NET アプリケーションから呼び出されたときにストアドプロシージャをデバッグする準備が整います。 デバッガーを起動するには、[デバッグ] メニューに移動し、F5 キーを押すか、ツールバーの緑色の再生アイコンをクリックします。 これにより、デバッガーが起動し、web サイトが起動します。

`Products_SelectByCategoryID` ストアドプロシージャは、型指定された[データセットの tableadapter チュートリアル用の既存のストアドプロシージャを使用して](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)、で作成されました。 対応する web ページ (`~/AdvancedDAL/ExistingSprocs.aspx`) には、このストアドプロシージャによって返された結果を表示する GridView が含まれています。 ブラウザーでこのページを参照してください。 ページに到達すると、`Products_SelectByCategoryID` ストアドプロシージャ内のブレークポイントにヒットし、Visual Studio に制御が返されます。 手順1と同様に、ストアドプロシージャ s ステートメントをステップ実行し、パラメーター値を表示および変更することができます。

[ExistingSprocs .aspx ページが最初に飲み物を表示 ![](debugging-stored-procedures-vb/_static/image13.png)](debugging-stored-procedures-vb/_static/image12.png)

**図 6**: `ExistingSprocs.aspx` ページには、最初に飲み物が表示されます ([クリックすると、フルサイズの画像が表示](debugging-stored-procedures-vb/_static/image14.png)されます)

[ストアドプロシージャ s のブレークポイントに達した ![](debugging-stored-procedures-vb/_static/image16.png)](debugging-stored-procedures-vb/_static/image15.png)

**図 7**: ストアドプロシージャ s のブレークポイントに達しました ([クリックすると、フルサイズの画像が表示](debugging-stored-procedures-vb/_static/image17.png)されます)

図7のウォッチウィンドウに示すように、`@CategoryID` パラメーターの値は1です。 これは、[`ExistingSprocs.aspx`] ページで、[飲料] カテゴリの製品が最初に表示されるためです。これには、`CategoryID` 値が1になっています。 ドロップダウンリストから別のカテゴリを選択します。 これにより、ポストバックが発生し、`Products_SelectByCategoryID` ストアドプロシージャが再実行されます。 ブレークポイントは再びヒットしますが、今度は `@CategoryID` パラメーター s の値に、選択したドロップダウンリスト項目の `CategoryID`が反映されます。

[ドロップダウンリストから別のカテゴリを選択 ![には](debugging-stored-procedures-vb/_static/image19.png)](debugging-stored-procedures-vb/_static/image18.png)

**図 8**: ドロップダウンリストから別のカテゴリを選択する ([クリックすると、フルサイズの画像が表示](debugging-stored-procedures-vb/_static/image20.png)されます)

[![@CategoryID パラメーターには、Web ページから選択されたカテゴリが反映されます。](debugging-stored-procedures-vb/_static/image22.png)](debugging-stored-procedures-vb/_static/image21.png)

**図 9**: `@CategoryID` パラメーターには、Web ページから選択したカテゴリが反映されます ([クリックすると、フルサイズの画像が表示](debugging-stored-procedures-vb/_static/image23.png)されます)

> [!NOTE]
> [`ExistingSprocs.aspx`] ページにアクセスするときに `Products_SelectByCategoryID` ストアドプロシージャ内のブレークポイントにヒットしない場合は、[ASP.NET application s] プロパティページの [デバッガー] セクションで [SQL Server] チェックボックスがオンになっていること、接続プーリングが無効になっていること、および [データベース s アプリケーションデバッグ] オプションが有効になっていることを確認します。 問題が解決しない場合は、Visual Studio を再起動して、もう一度やり直してください。

## <a name="debugging-t-sql-database-objects-on-remote-instances"></a>リモートインスタンスでの T SQL Database オブジェクトのデバッグ

SQL Server データベースインスタンスが Visual Studio と同じコンピューター上にある場合、Visual Studio を使用してデータベースオブジェクトをデバッグするのは非常に簡単です。 ただし、SQL Server と Visual Studio が異なるコンピューターに存在する場合は、すべてが正常に動作するためには慎重に構成する必要があります。 ここでは、次の2つの主要なタスクに直面します。

- ADO.NET 経由でデータベースに接続するために使用されるログインが、`sysadmin` ロールに属していることを確認します。
- 開発用コンピューターの Visual Studio で使用されている Windows ユーザーアカウントが、`sysadmin` ロールに属している有効な SQL Server ログインアカウントであることを確認します。

最初の手順は比較的簡単です。 まず、ASP.NET アプリケーションからデータベースに接続するために使用するユーザーアカウントを特定し、SQL Server Management Studio から、そのログインアカウントを `sysadmin` ロールに追加します。

2番目のタスクでは、アプリケーションのデバッグに使用する Windows ユーザーアカウントが、リモートデータベースの有効なログインである必要があります。 ただし、ワークステーションにログオンした Windows アカウントが SQL Server の有効なログインではない可能性があります。 特定のログインアカウントを SQL Server に追加するのではなく、一部の Windows ユーザーアカウントを SQL Server デバッグアカウントとして指定する方が適しています。 次に、リモート SQL Server インスタンスのデータベースオブジェクトをデバッグするには、その Windows ログインアカウントの資格情報を使用して Visual Studio を実行します。

例を使用すると、わかりやすくなります。 Windows ドメイン内に `SQLDebug` という名前の Windows アカウントがあると仮定します。 このアカウントは、リモート SQL Server インスタンスに有効なログインとして追加し、`sysadmin` ロールのメンバーとして追加する必要があります。 次に、Visual Studio からリモート SQL Server インスタンスをデバッグするには、`SQLDebug` ユーザーとして Visual Studio を実行する必要があります。 これを行うには、ワークステーションからログアウトし、`SQLDebug`としてログインした後、Visual Studio を起動しますが、より簡単な方法は、独自の資格情報を使用してワークステーションにログインし、`runas.exe` を使用して `SQLDebug` ユーザーとして Visual Studio を起動することです。 `runas.exe` を使用すると、特定のアプリケーションを別のユーザーアカウントの guise で実行できます。 `SQLDebug`として Visual Studio を起動するには、コマンドラインで次のステートメントを入力します。

[!code-console[Main](debugging-stored-procedures-vb/samples/sample2.cmd)]

このプロセスの詳細については、 *Visual Studio と SQL Server、7番目のエディション*の「[ウィリアム R. Vaughn](http://betav.com/BLOG/billva/) s ヒットガイド」、および「[方法: デバッグのための SQL Server アクセス許可を設定する](https://msdn.microsoft.com/library/w1bhybwz(VS.80).aspx)」を参照してください。

> [!NOTE]
> 開発用コンピューターで Windows XP Service Pack 2 が実行されている場合は、リモートデバッグを許可するようにインターネット接続ファイアウォールを構成する必要があります。 「[方法: SQL Server 2005 デバッグを有効](https://msdn.microsoft.com/library/s0fk6z6e(VS.80).aspx)にする」の記事では、Visual Studio ホストコンピューターでの2つの手順 (a) が必要であることに注意してください。 `Devenv.exe` を例外の一覧に追加し、TCP 135 ポートを開く必要があります。リモート (SQL) マシンでは、(b) TCP 135 ポートを開き、`sqlservr.exe` を例外一覧に追加する必要があります。 ドメインポリシーで IPSec 経由でネットワーク通信を行う必要がある場合は、UDP 4500 および UDP 500 ポートを開く必要があります。

## <a name="summary"></a>まとめ

Visual Studio では、.NET アプリケーションコードに対してデバッグサポートを提供するだけでなく、SQL Server 2005 用のさまざまなデバッグオプションも用意されています。 このチュートリアルでは、直接データベースデバッグとアプリケーションデバッグという2つのオプションについて説明しました。 T-sql database オブジェクトを直接デバッグするには、サーバーエクスプローラーでオブジェクトを見つけて右クリックし、[ステップイン] を選択します。 これにより、デバッガーが起動し、データベースオブジェクトの最初のステートメントで停止します。この時点で、オブジェクトのステートメントをステップ実行し、パラメーター値を表示および変更できます。 手順1では、この方法を使用して `Products_SelectByCategoryID` ストアドプロシージャにステップインしました。

アプリケーションのデバッグを使用すると、データベースオブジェクト内でブレークポイントを直接設定できます。 ブレークポイントを持つデータベースオブジェクトがクライアントアプリケーション (ASP.NET web アプリケーションなど) から呼び出された場合、デバッガーが引き継ぐと、プログラムは停止します。 アプリケーションのデバッグは、特定のデータベースオブジェクトが呼び出されるアプリケーションアクションをより明確に示すため便利です。 ただし、データベースの直接デバッグよりも少し多くの構成と設定が必要です。

データベースオブジェクトは、SQL Server プロジェクトでデバッグすることもできます。 SQL Server プロジェクトの使用方法と、それらを使用して、次のチュートリアルでマネージデータベースオブジェクトを作成およびデバッグする方法について説明します。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

> [!div class="step-by-step"]
> [前へ](protecting-connection-strings-and-other-configuration-information-vb.md)
> [次へ](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb.md)

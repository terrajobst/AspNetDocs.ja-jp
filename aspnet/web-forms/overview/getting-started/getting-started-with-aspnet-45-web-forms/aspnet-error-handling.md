---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET のエラー処理 |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 9514142ca50b33470a3f4c033e4f8e319a9ee09b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457024"
---
# <a name="aspnet-error-handling"></a>ASP.NET エラー処理

[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。

> このチュートリアルシリーズでは、ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎と、Web 用の Microsoft Visual Studio Express 2013 について説明します。 このチュートリアルシリーズ[でC#は、ソースコードが含ま](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)れる Visual Studio 2013 プロジェクトを利用できます。

このチュートリアルでは、Wingtip Toys サンプルアプリケーションを変更して、エラー処理とエラーログを含めます。 エラー処理により、アプリケーションはエラーを適切に処理し、それに応じてエラーメッセージを表示できます。 エラーログを使用すると、発生したエラーを検出して修正することができます。 このチュートリアルは、前の「URL ルーティング」チュートリアルに基づいており、Wingtip Toys チュートリアルシリーズの一部です。

## <a name="what-youll-learn"></a>ここでは、次の内容について学習します。

- アプリケーションの構成にグローバルエラー処理を追加する方法。
- アプリケーション、ページ、およびコードレベルでエラー処理を追加する方法について説明します。
- 後で確認するためにエラーをログに記録する方法。
- セキュリティを損なうことのないエラーメッセージを表示する方法。
- エラーログモジュールとハンドラー (ELMAH) のエラーログを実装する方法。

## <a name="overview"></a>概要

ASP.NET アプリケーションは、実行中に発生したエラーを一貫した方法で処理できる必要があります。 ASP.NET は、共通言語ランタイム (CLR) を使用します。これにより、一貫した方法でアプリケーションにエラーを通知することができます。 エラーが発生すると、例外がスローされます。 例外とは、アプリケーションで発生したエラー、条件、または予期しない動作のことです。

.NET Framework では、例外は `System.Exception` クラスから継承されるオブジェクトです。 例外は問題が発生したコード領域からスローされます。 例外は、例外を処理するコードがアプリケーションによって提供される場所に、呼び出し履歴が渡されます。 アプリケーションが例外を処理しない場合、ブラウザーはエラーの詳細を表示するように強制されます。

ベストプラクティスとして、`Try`/のコードレベルでのエラーを処理し、コード内の `Finally` ブロックを /`Catch`ます。 ユーザーが発生したコンテキストで問題を修正できるように、これらのブロックを配置してみてください。 エラー処理ブロックがエラーが発生した場所から離れすぎている場合は、問題を修正するために必要な情報をユーザーに提供することが難しくなります。

### <a name="exception-class"></a>Exception クラス

Exception クラスは、例外の継承元となる基本クラスです。 ほとんどの例外オブジェクトは、`SystemException` クラス、`IndexOutOfRangeException` クラス、`ArgumentNullException` クラスなど、例外クラスの派生クラスのインスタンスです。 Exception クラスには、`StackTrace` プロパティ、`InnerException` プロパティ、`Message` プロパティなどのプロパティがあり、発生したエラーに関する特定の情報を提供します。

### <a name="exception-inheritance-hierarchy"></a>例外の継承階層

ランタイムには、例外が発生したときにランタイムがスローする `SystemException` クラスから派生した例外の基本セットがあります。 `IndexOutOfRangeException` クラスや `ArgumentNullException` クラスなど、例外クラスを継承するほとんどのクラスは、追加のメンバーを実装しません。 そのため、例外の最も重要な情報は、例外の階層、例外の名前、および例外に含まれる情報にあります。

### <a name="exception-handling-hierarchy"></a>例外処理の階層

ASP.NET Web フォームアプリケーションでは、特定の処理階層に基づいて例外を処理できます。 例外は、次のレベルで処理できます。

- アプリケーション レベル
- ページレベルのロック
- コードレベル

アプリケーションで例外を処理する場合、例外クラスから継承された例外に関する追加情報を取得して、ユーザーに表示できます。 アプリケーション、ページ、およびコードレベルに加えて、HTTP モジュールレベルおよび IIS カスタムハンドラーを使用して例外を処理することもできます。

### <a name="application-level-error-handling"></a>アプリケーションレベルのエラー処理

アプリケーションの構成を変更するか、アプリケーションの*global.asax*ファイルに `Application_Error` ハンドラーを追加することによって、アプリケーションレベルで既定のエラーを処理できます。

*Web.config ファイルに*`customErrors` セクションを追加することによって、既定のエラーと HTTP エラーを処理できます。 `customErrors` セクションでは、エラーが発生したときにユーザーがリダイレクトされる既定のページを指定できます。 また、特定のステータスコードエラーのページを個別に指定することもできます。

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

残念ながら、構成を使用してユーザーを別のページにリダイレクトすると、発生したエラーの詳細は表示されません。

ただし、 *global.asax*ファイルの `Application_Error` ハンドラーにコードを追加することで、アプリケーション内の任意の場所で発生したエラーをトラップできます。

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a>ページレベルのエラーイベントの処理

ページレベルのハンドラーは、エラーが発生したページにユーザーを返しますが、コントロールのインスタンスは保持されないため、ページ上の何も表示されなくなります。 アプリケーションのユーザーにエラーの詳細を提供するには、エラーの詳細をページに明示的に書き込む必要があります。

通常は、ページレベルのエラーハンドラーを使用して、未処理のエラーをログに記録するか、役に立つ情報を表示できるページに移動します。

このコード例では、ASP.NET Web ページの Error イベントのハンドラーを示します。 このハンドラーは、ページ内の `try`/`catch` ブロック内でまだ処理されていないすべての例外をキャッチします。

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

エラーを処理した後、サーバーオブジェクト (`HttpServerUtility` クラス) の `ClearError` メソッドを呼び出すことによって、エラーをクリアする必要があります。そうしないと、以前に発生したエラーが表示されます。

### <a name="code-level-error-handling"></a>コードレベルのエラー処理

Try-catch ステートメントは、try ブロックとそれに続く1つ以上の catch 句で構成されます。これは、さまざまな例外のハンドラーを指定します。 例外がスローされると、共通言語ランタイム (CLR) は、この例外を処理する catch ステートメントを検索します。 現在実行中のメソッドに catch ブロックが含まれていない場合、CLR は現在のメソッドを呼び出したメソッドを参照します。 Catch ブロックが見つからない場合、CLR はハンドルされない例外メッセージをユーザーに表示し、プログラムの実行を停止します。

次のコード例は、`try`/`catch`/`finally` を使用してエラーを処理する一般的な方法を示しています。

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

上記のコードでは、try ブロックには、考えられる例外に対して保護する必要があるコードが含まれています。 ブロックは、例外がスローされるか、ブロックが正常に完了するまで実行されます。 `FileNotFoundException` の例外または `IOException` の例外が発生した場合、実行は別のページに転送されます。 次に、finally ブロックに含まれているコードが、エラーが発生したかどうかにかかわらず実行されます。

## <a name="adding-error-logging-support"></a>エラーログのサポートの追加

Wingtip Toys サンプルアプリケーションにエラー処理を追加する前に、*ロジック*フォルダーに `ExceptionUtility` クラスを追加して、エラーログサポートを追加します。 これにより、アプリケーションがエラーを処理するたびにエラーの詳細がエラーログファイルに追加されます。

1. *Logic*フォルダーを右クリックし、[ **Add** -&gt;**新しい項目**] を選択します。   
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. 左側の **[ C# Visual** -&gt;**コード**テンプレート] グループを選択します。 次に、中央の一覧から **[クラス]** を選択し、「 **ExceptionUtility.cs**」という名前を指定します。
3. **[追加]** をクリックします。 新しいクラスファイルが表示されます。
4. 既存のコードを次のコードに置き換えます。  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

例外が発生した場合は、`LogException` メソッドを呼び出すことによって例外を例外ログファイルに書き込むことができます。 このメソッドは、例外オブジェクトと、例外の原因の詳細を含む文字列の2つのパラメーターを受け取ります。 例外ログは、 *App\_Data*フォルダー内の*エラー*ログファイルに書き込まれます。

### <a name="adding-an-error-page"></a>エラーページの追加

Wingtip Toys サンプルアプリケーションでは、1つのページを使用してエラーが表示されます。 このエラーページは、サイトのユーザーにセキュリティで保護されたエラーメッセージを表示するように設計されています。 ただし、ユーザーが、コードが存在するコンピューターでローカルに提供されている HTTP 要求を行う開発者の場合は、エラーページに追加のエラーの詳細が表示されます。

1. **ソリューションエクスプローラー**でプロジェクト名 (**Wingtip Toys**) を右クリックし、 **[追加]** [ -&gt;**新しい項目**] の順に選択します。   
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. 左側の **[ C# Visual** -&gt; **Web**テンプレート] グループを選択します。 中央の一覧で **[マスターページを使用した Web フォーム]** を選択し、「 **errorpage .aspx**」という名前を付けます。
3. **[追加]** をクリックします。
4. マスターページとして [] を選択し、[ **OK]** を選択し*ます。*
5. 既存のマークアップを次のように置き換えます。   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. 次のように、分離コード (*ErrorPage.aspx.cs*) の既存のコードを置き換えます。   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

エラーページが表示されると、`Page_Load` イベントハンドラーが実行されます。 `Page_Load` ハンドラーでは、エラーが最初に処理された場所が決定されます。 その後、発生した最後のエラーは、サーバーオブジェクトの `GetLastError` メソッドを呼び出すことによって決定されます。 例外が既に存在しない場合は、汎用的な例外が作成されます。 その後、HTTP 要求がローカルに作成された場合は、すべてのエラーの詳細が表示されます。 この場合、web アプリケーションを実行しているローカルコンピューターにのみ、これらのエラーの詳細が表示されます。 エラー情報が表示されると、エラーがログファイルに追加され、サーバーからエラーがクリアされます。

### <a name="displaying-unhandled-error-messages-for-the-application"></a>アプリケーションの未処理のエラーメッセージを表示する

*Web.config ファイルに*`customErrors` セクションを追加することで、アプリケーション全体で発生する単純なエラーを迅速に処理できます。 また、404-ファイルが見つからないなどのステータスコード値に基づいて、エラーの処理方法を指定することもできます。

#### <a name="update-the-configuration"></a>構成を更新する

*Web.config ファイルに*`customErrors` セクションを追加して、構成を更新します。

1. **ソリューションエクスプローラー**で、Wingtip Toys サンプルアプリケーションのルートにある*web.config*ファイルを見つけて開きます。
2. 次のように `<system.web>` ノード内の*web.config*ファイルに `customErrors` セクションを追加します。   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. *Web.config* ファイルを保存します。

`customErrors` セクションでは、モードを指定します。これは "On" に設定されています。 また、`defaultRedirect`を指定します。これは、エラーが発生したときに移動するページをアプリケーションに通知します。 また、ページが見つからない場合に404エラーを処理する方法を指定する特定の error 要素を追加しました。 このチュートリアルの後の方で、アプリケーションレベルでエラーの詳細をキャプチャする追加のエラー処理を追加します。

#### <a name="running-the-application"></a>アプリケーションの実行

アプリケーションを今すぐ実行して、更新されたルートを確認することができます。

1. **F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。  
 ブラウザーが開き、 *default.aspx*ページが表示されます。
2. ブラウザーに次の URL を入力します (**必ずポート番号を使用**してください)。  
    `https://localhost:44300/NoPage.aspx`
3. ブラウザーに表示されている*Errorpage .aspx*を確認します。 

    ![ASP.NET エラー処理-ページが見つかりませんでした](aspnet-error-handling/_static/image1.png)

存在しない*Nopage .aspx*ページを要求すると、エラーページには単純なエラーメッセージと詳細なエラー情報が表示されます (追加の詳細情報がある場合)。 ただし、ユーザーが存在しないページをリモートの場所から要求した場合、エラーページに表示されるのはエラーメッセージだけです。

### <a name="including-an-exception-for-testing-purposes"></a>テスト目的で例外を含める

エラーが発生したときにアプリケーションがどのように機能するかを確認するには、ASP.NET でエラー条件を意図的に作成します。 Wingtip Toys サンプルアプリケーションでは、既定のページが読み込まれて何が発生するかを確認すると、テスト例外がスローされます。

1. Visual Studio で*default.aspx*ページの分離コードを開きます。   
   *Default.aspx.cs*の分離コードページが表示されます。
2. `Page_Load` ハンドラーで、次のようにハンドラーが表示されるようにコードを追加します。   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

さまざまな種類の例外を作成することができます。 上のコードでは、 *default.aspx*ページが読み込まれたときに `InvalidOperationException` を作成しています。

#### <a name="running-the-application"></a>アプリケーションの実行

アプリケーションを実行して、アプリケーションが例外を処理する方法を確認できます。

1. CTRL キーを押し**ながら F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。  
 アプリケーションは、InvalidOperationException をスローします。 

    > [!NOTE] 
    > 
    > Visual Studio でエラーの原因を表示するには、コードを中断せずに、CTRL キーを押し**ながら F5**キーを押してページを表示する必要があります。
2. ブラウザーに表示されている*Errorpage .aspx*を確認します。 

    ![ASP.NET エラー処理-エラーページ](aspnet-error-handling/_static/image2.png)

エラーの詳細を見るとわかるように、 *web.config ファイルの*`customError` セクションで例外がトラップされています。

### <a name="adding-application-level-error-handling"></a>アプリケーションレベルのエラー処理の追加

*Web.config ファイルの*`customErrors` セクションを使用して例外をトラップするのではなく、例外に関する情報がほとんど得られない場合は、アプリケーションレベルでエラーをトラップし、エラーの詳細を取得することができます。

1. **ソリューションエクスプローラー**で、 *Global.asax.cs*ファイルを見つけて開きます。
2. 次のように表示されるように、**アプリケーション\_のエラー**ハンドラーを追加します。   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

アプリケーションでエラーが発生すると、`Application_Error` ハンドラーが呼び出されます。 このハンドラーでは、最後の例外が取得され、確認されます。 例外がハンドルされず、例外に内部例外の詳細が含まれている (つまり `InnerException` が null ではない) 場合、アプリケーションは、例外の詳細が表示されるエラーページに実行を転送します。

#### <a name="running-the-application"></a>アプリケーションの実行

アプリケーションを実行して、アプリケーションレベルで例外を処理することによって提供される追加のエラーの詳細を確認できます。

1. CTRL キーを押し**ながら F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。  
 アプリケーションによって `InvalidOperationException` がスローされます。
2. ブラウザーに表示されている*Errorpage .aspx*を確認します。 

    ![ASP.NET エラー処理-アプリケーションレベルのエラー](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a>ページレベルのエラー処理の追加

ページの `@Page` ディレクティブに `ErrorPage` 属性を追加するか、ページの分離コードに `Page_Error` イベントハンドラーを追加することによって、ページレベルのエラー処理をページに追加できます。 このセクションでは、実行を*errorpage .aspx*ページに転送する `Page_Error` イベントハンドラーを追加します。

1. **ソリューションエクスプローラー**で、 *Default.aspx.cs*ファイルを見つけて開きます。
2. `Page_Error` ハンドラーを追加して、分離コードが次のように表示されるようにします。   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

ページでエラーが発生すると、`Page_Error` イベントハンドラーが呼び出されます。 このハンドラーでは、最後の例外が取得され、確認されます。 `InvalidOperationException` が発生した場合、`Page_Error` イベントハンドラーは、例外の詳細が表示されているエラーページに実行を転送します。

#### <a name="running-the-application"></a>アプリケーションの実行

アプリケーションを今すぐ実行して、更新されたルートを確認することができます。

1. CTRL キーを押し**ながら F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。  
 アプリケーションによって `InvalidOperationException` がスローされます。
2. ブラウザーに表示されている*Errorpage .aspx*を確認します。 

    ![ASP.NET エラー処理-ページレベルのエラー](aspnet-error-handling/_static/image4.png)
3. ブラウザーウィンドウを閉じます。

### <a name="removing-the-exception-used-for-testing"></a>テストに使用された例外を削除しています

このチュートリアルの前半で追加した例外をスローせずに Wingtip Toys サンプルアプリケーションを機能させるには、例外を削除します。

1. *Default.aspx*ページの分離コードを開きます。
2. `Page_Load` ハンドラーで、例外をスローするコードを削除して、ハンドラーが次のように表示されるようにします。   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a>コードレベルのエラーログの追加

このチュートリアルで既に説明したように、try/catch ステートメントを追加して、コードのセクションを実行し、発生した最初のエラーを処理することができます。 この例では、エラーの詳細をエラーログファイルに書き込むだけで、エラーを後で確認できます。

1. **ソリューションエクスプローラー**の*Logic*フォルダーで、 *PayPalFunctions.cs*ファイルを見つけて開きます。
2. コードが次のように表示されるように、`HttpCall` メソッドを更新します。   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

上のコードは、`ExceptionUtility` クラスに含まれている `LogException` メソッドを呼び出します。 このチュートリアルの前半で、*ロジック*フォルダーに*ExceptionUtility.cs*クラスファイルを追加しました。 `LogException` は、次の 2 つのパラメーターを受け取ります。 最初のパラメーターは、exception オブジェクトです。 2番目のパラメーターは、エラーの原因を認識するために使用される文字列です。

### <a name="inspecting-the-error-logging-information"></a>エラーのログ情報を検査しています

前に説明したように、エラーログを使用して、アプリケーションでどのエラーを先に修正する必要があるかを判断できます。 もちろん、トラップされ、エラーログに書き込まれたエラーのみが記録されます。

1. **ソリューションエクスプローラー**で、 *App\_Data*フォルダー内の*ログ*ファイルを見つけて開きます。   
 場合によっては、 **[すべてのファイルを表示]** オプションを選択するか、**ソリューションエクスプローラー**の上部にある **[更新]** オプションを選択して、*エラーログ*ファイルを確認する必要があります。
2. Visual Studio に表示されるエラーログを確認します。 

    ![ASP.NET エラー処理-エラーログ](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a>安全なエラーメッセージ

アプリケーションでエラーメッセージが表示される場合は、悪意のあるユーザーがアプリケーションを攻撃する際に役立つ情報を提供しないようにする必要があること**に注意し**てください。 たとえば、アプリケーションがデータベースへの書き込みに失敗した場合、使用しているユーザー名を含むエラーメッセージが表示されないようにする必要があります。 このため、赤の一般的なエラーメッセージがユーザーに表示されます。 その他のエラーの詳細はすべて、ローカルコンピューターの開発者にのみ表示されます。

## <a name="using-elmah"></a>ELMAH の使用

ELMAH (エラーログモジュールとハンドラー) は、NuGet パッケージとして ASP.NET アプリケーションにプラグインするエラーログ機能です。 ELMAH には、次の機能が用意されています。

- 未処理の例外のログ記録。
- 記録の未処理の例外のログ全体を表示する web ページ。
- ログに記録された各例外の詳細を表示する web ページ。
- 発生時の各エラーに関する電子メール通知。
- ログからの過去15件のエラーの RSS フィード。

ELMAH を使用するには、事前にインストールしておく必要があります。 これは、 *NuGet*パッケージインストーラーを使用して簡単に行うことができます。 このチュートリアルシリーズで既に説明したように、NuGet は visual Studio の拡張機能であり、Visual Studio でのオープンソースライブラリとツールのインストールと更新を簡単に行うことができます。

1. Visual Studio で、 **[ツール]** メニューの **[nuget パッケージマネージャー]** を選択し、 **[ソリューションの nuget パッケージの管理]**  > します。 

    ![ASP.NET エラー処理-ソリューションの NuGet パッケージの管理](aspnet-error-handling/_static/image6.png)
2. **[NuGet パッケージの管理]** ダイアログボックスは、Visual Studio 内に表示されます。
3. **[NuGet パッケージの管理]** ダイアログボックスで、左側の **[オンライン]** を展開し、 **[nuget.org]** を選択します。次に、利用可能なパッケージの一覧から、オンラインで**ELMAH**パッケージを検索してインストールします。 

    ![ASP.NET エラー処理-ELMA NuGet パッケージ](aspnet-error-handling/_static/image7.png)
4. パッケージをダウンロードするには、インターネットに接続している必要があります。
5. **[プロジェクトの選択**] ダイアログボックスで、 **[ウィングヒント]** が選択されていることを確認し、 **[OK]** をクリックします。 

    ![ASP.NET エラー処理-[プロジェクトの選択] ダイアログ](aspnet-error-handling/_static/image8.png)
6. 必要に応じて、 **[NuGet パッケージの管理]** ダイアログボックスで **[閉じる]** をクリックします。
7. 開いているファイルを再度読み込むように Visual Studio から要求された場合は、 **[すべてはい]** を選択します。
8. ELMAH パッケージは、プロジェクトのルートにある*web.config ファイルに*自身のエントリを追加します。 *変更した web.config ファイル*を再読み込みするかどうかを確認するメッセージが Visual Studio で表示されたら、 **[はい]** をクリックします。

ELMAH は、発生した未処理のエラーを格納する準備ができました。

### <a name="viewing-the-elmah-log"></a>ELMAH ログの表示

ELMAH ログを表示するのは簡単ですが、最初に、ELMAH ログに記録されるハンドルされない例外を作成します。

1. CTRL キーを押し**ながら F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。
2. 未処理の例外を ELMAH ログに書き込むには、ブラウザーで次の URL (ポート番号を使用) に移動します。  
    `https://localhost:44300/NoPage.aspx` エラーページが表示されます。
3. ELMAH ログを表示するには、ブラウザーで次の URL (ポート番号を使用) に移動します。  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET エラー処理-ELMAH エラーログ](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a>まとめ

このチュートリアルでは、アプリケーションレベル、ページレベル、およびコードレベルでエラーを処理する方法について学習しました。 また、処理されたエラーと未処理のエラーをログに記録して後で確認する方法についても学習しました。 ここでは、NuGet を使用してアプリケーションに例外ログと通知を提供するために、ELMAH ユーティリティを追加しました。 また、安全なエラーメッセージの重要性についても説明しました。

## <a name="tutorial-series-conclusion"></a>チュートリアルシリーズの結論

次のようにしていただき、ありがとうございます。 この一連のチュートリアルを使用すると、ASP.NET Web フォームを理解しやすくなります。 ASP.NET 4.5 および Visual Studio 2013 で使用できる Web フォーム機能の詳細については、「 [ASP.NET and Web Tools Visual Studio 2013 リリースノート](../../../../visual-studio/overview/2013/release-notes.md)」を参照してください。 また、「**次のステップ**」のセクションに記載されているチュートリアルを参照して、[無料の Azure 試用版](https://azure.microsoft.com/pricing/free-trial/)を defintely してください。

![ありがとうございました-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a>次の手順

Microsoft Azure するための web アプリケーションのデプロイの詳細については、「 [Azure の Web サイトへのメンバーシップ、OAuth、SQL Database を使用した安全な ASP.NET Web フォームアプリのデプロイ](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)」を参照してください。

## <a name="free-trial"></a>無料試用版

[Microsoft Azure-無料試用版](https://azure.microsoft.com/pricing/free-trial/)  
 Web サイトを Microsoft Azure に公開すると、時間、メンテナンス、コストが節約されます。 これは、web アプリを Azure にデプロイするための簡単なプロセスです。 Web アプリを保守および監視する必要がある場合、Azure にはさまざまなツールとサービスが用意されています。 Azure のデータ、トラフィック、id、バックアップ、メッセージング、メディア、パフォーマンスを管理します。 また、これらはすべて、非常にコスト効率のよい方法で提供されます。

## <a name="additional-resources"></a>その他のリソース

[ASP.NET Health Monitoring  でエラーの詳細をログに記録](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md)する  
[ELMAH](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a>謝辞

このチュートリアルシリーズの内容に多大な貢献をした次の人々に感謝したいと思います。

- [Alberto Poblacion, MVP &amp; MCT, スペイン](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- [Alex、オランダ](http://blog.alexthissen.nl/)(twitter: [@alexthissen](http://twitter.com/alexthissen))
- [Andre Tournier、USA](http://andret503.wordpress.com/)
- Apurva Joshi、Microsoft
- [Bojan Vrhovnik、スロベニア](http://twitter.com/bvrhovnik)
- [Bruno Sonnino、ブラジル](http://msmvps.com/blogs/bsonnino)(twitter: [@bsonnino](http://twitter.com/bsonnino))
- [Carlos dos Santos、ブラジル](http://www.carloscds.net/)
- [Dave Campbell, USA](http://www.wynapse.com/) (twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))
- [Jon Galloway、Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))
- [Michael シャープ、USA](http://www.930solutions.com/) (twitter: [@mrsharps](http://twitter.com/mrsharps))
- Mike Pope
- [米国 Mitchel](http://www.mitchelsellers.com/) (twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))
- [Paul Cociuba、Microsoft](http://linqto.me/Links/pcociuba)
- [パウロ Morgado、ポルトガル](http://paulomorgado.net/)
- [Pranav Rastogi、Microsoft](https://blogs.msdn.com/b/pranav_rastogi)
- [Tim Ammann、Microsoft](https://blogs.iis.net/timamm/default.aspx)
- [Tom Dykstra、Microsoft](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a>コミュニティへの投稿

- Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))  
  MSDN の Visual Studio 2012 関連コードサンプル:[ナビゲーション Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)
- James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))  
  MSDN の Visual Studio 2012 関連コードサンプル: [ASP.NET 4.5 Web フォームチュートリアルシリーズ (Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63) )
- Andrielle Azevedo-Microsoft テクニカルオーディエンス共同作成者 (twitter: @driazevedo)  
  Visual Studio 2012 translation: [Iniciando com ASP.NET Web フォーム 4.5-Parte 1-Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)

> [!div class="step-by-step"]
> [[戻る]](url-routing.md)

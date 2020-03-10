---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: PayPal を使用したチェックアウトと支払い |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455932"
---
# <a name="checkout-and-payment-with-paypal"></a>精算と PayPal による支払い

[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。

> このチュートリアルシリーズでは、ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎と、Web 用の Microsoft Visual Studio Express 2013 について説明します。 このチュートリアルシリーズ[でC#は、ソースコードが含ま](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)れる Visual Studio 2013 プロジェクトを利用できます。

このチュートリアルでは、Wingtip Toys サンプルアプリケーションを変更して、PayPal を使用したユーザーの承認、登録、支払いを含むようにする方法について説明します。 ログインしているユーザーのみが製品の購入を許可されます。 ASP.NET 4.5 Web フォームプロジェクトテンプレートには、必要なものの多くが既に組み込まれています。 PayPal Express のチェックアウト機能を追加します。 このチュートリアルでは、PayPal 開発者テスト環境を使用しているため、実際の資金は譲渡されません。 このチュートリアルの最後では、ショッピングカートに追加する製品を選択し、[チェックアウト] ボタンをクリックして、PayPal テスト web サイトにデータを転送することで、アプリケーションをテストします。 PayPal テスト web サイトでは、出荷と支払いに関する情報を確認し、ローカル Wingtip Toys サンプルアプリケーションに戻って、購入を確認して完了します。

拡張性とセキュリティに対処するオンラインショッピングに特化した、経験豊富なサードパーティの支払いプロセッサがいくつかあります。 ASP.NET 開発者は、ショッピングおよび購入ソリューションを実装する前に、サードパーティの支払いソリューションを利用する利点を考慮する必要があります。

> [!NOTE] 
> 
> Wingtip Toys サンプルアプリケーションは、ASP.NET web 開発者が使用できる特定の ASP.NET の概念と機能を示すように設計されています。 このサンプルアプリケーションは、スケーラビリティとセキュリティに関して考えられるすべての状況に合わせて最適化されていませんでした。

## <a name="what-youll-learn"></a>ここでは、次の内容について学習します。

- フォルダー内の特定のページへのアクセスを制限する方法。
- 匿名ショッピングカートから既知のショッピングカートを作成する方法。
- プロジェクトに対して SSL を有効にする方法。
- OAuth プロバイダーをプロジェクトに追加する方法。
- Paypal を使用して、PayPal テスト環境を使用して製品を購入する方法。
- **DetailsView**コントロールで PayPal の詳細を表示する方法。
- Wingtip Toys アプリケーションのデータベースを、PayPal から取得した詳細情報で更新する方法について説明します。

## <a name="adding-order-tracking"></a>注文追跡の追加

このチュートリアルでは、ユーザーが作成した注文からデータを追跡する2つの新しいクラスを作成します。 これらのクラスは、出荷情報、購入合計、および支払いの確認に関するデータを追跡します。

### <a name="add-the-order-and-orderdetail-model-classes"></a>Order および OrderDetail モデルクラスを追加する

このチュートリアルシリーズの前半では、[*モデル*] フォルダーに `Category`、`Product`、および `CartItem` クラスを作成することによって、カテゴリ、製品、およびショッピングカート項目のスキーマを定義しています。 ここでは、2つの新しいクラスを追加して、製品の注文のスキーマと注文の詳細を定義します。

1. **[モデル]** フォルダーに、 *Order.cs*という名前の新しいクラスを追加します。   
   新しいクラスファイルがエディターに表示されます。
2. 既定のコードを次のコードに置き換えます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. *OrderDetail.cs*クラスを [*モデル*] フォルダーに追加します。
4. 既定のコードを以下のコードに置き換えます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order` クラスと `OrderDetail` クラスには、購入および発送に使用する注文情報を定義するためのスキーマが含まれています。

さらに、エンティティクラスを管理し、データベースへのデータアクセスを提供するデータベースコンテキストクラスを更新する必要があります。 これを行うには、新しく作成された Order クラスと `OrderDetail` モデルクラスを `ProductContext` クラスに追加します。

1. **ソリューションエクスプローラー**で、 *ProductContext.cs*ファイルを見つけて開きます。
2. 次に示すように、強調表示されているコードを*ProductContext.cs*ファイルに追加します。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

このチュートリアルシリーズで前述したように、 *ProductContext.cs*ファイルのコードは、Entity Framework のすべてのコア機能にアクセスできるように、`System.Data.Entity` 名前空間を追加します。 この機能には、厳密に型指定されたオブジェクトを操作することによって、データのクエリ、挿入、更新、および削除を行う機能が含まれています。 `ProductContext` クラスの上記のコードは、新しく追加された `Order` および `OrderDetail` クラスへの Entity Framework アクセスを追加します。

## <a name="adding-checkout-access"></a>チェックアウトアクセスの追加

Wingtip Toys サンプルアプリケーションを使用すると、匿名ユーザーは、ショッピングカートに製品を確認して追加することができます。 ただし、匿名ユーザーがショッピングカートに追加した製品を購入する場合は、サイトにログオンする必要があります。 ログオンすると、チェックアウトおよび購入プロセスを処理する Web アプリケーションの制限付きページにアクセスできるようになります。 これらの制限付きページは、アプリケーションの*Checkout*フォルダーに含まれています。

### <a name="add-a-checkout-folder-and-pages"></a>チェックアウトフォルダーとページを追加する

ここ*で、チェックアウトフォルダーと*、チェックアウトプロセス中に顧客に表示されるページを作成します。 これらのページは、このチュートリアルの後半で更新します。

1. **ソリューションエクスプローラー**でプロジェクト名 (**Wingtip Toys**) を右クリックし、 **[新しいフォルダーの追加]** を選択します。 

    ![PayPal を使用したチェックアウトと支払い-新しいフォルダー](checkout-and-payment-with-paypal/_static/image1.png)
2. 新しいフォルダーに「*チェックアウト*」という名前を指定します。
3. [*チェックアウト*] フォルダーを右クリックし、[**新しい項目**の-&gt;**追加**] を選択します。 

    ![PayPal を使用したチェックアウトと支払い-新しい項目](checkout-and-payment-with-paypal/_static/image2.png)
4. **[新しい項目の追加]** ダイアログ ボックスが表示されます。
5. 左側の **[ C# Visual** -&gt; **Web**テンプレート] グループを選択します。 次に、中央のウィンドウで、 **[マスターページを含む Web フォーム]** を選択し、 *CheckoutStart*という名前を付けます。 

    ![[新しい項目の追加] ダイアログボックスでの [チェックと支払い]](checkout-and-payment-with-paypal/_static/image3.png)
6. 前と同様に、マスターページとして [] を選択し*ます。*
7. 上記と同じ手順を使用して、次の追加ページを*Checkout*フォルダーに追加します。   

    - CheckoutReview.aspx
    - CheckoutComplete.aspx
    - CheckoutCancel.aspx
    - CheckoutError.aspx

### <a name="add-a-webconfig-file"></a>Web.config ファイルを追加する

新しい web.config ファイルを*Checkout*フォルダーに追加することで、フォルダーに含まれるすべてのページへのアクセスを制限できるように*なります。*

1. [*チェックアウト*] フォルダーを右クリックし、[**新しい項目**の**追加** -&gt;] を選択します。  
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. 左側の **[ C# Visual** -&gt; **Web**テンプレート] グループを選択します。 次に、中央のペインで **[Web 構成ファイル]** を選択し、web.config*の既定*の名前をそのまま使用して、 **[追加]** を選択します。
3. *Web.config* ファイルの XML の内容を次の内容で置き換えます。  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. *Web.config* ファイルを保存します。

Web.config*ファイルは*、web アプリケーションのすべての不明なユーザーが、 *Checkout*フォルダーに格納されているページへのアクセスを拒否する必要があることを指定します。 ただし、ユーザーがアカウントを登録し、ログオンしている場合は、既知のユーザーになり、 *Checkout*フォルダー内のページにアクセスできるようになります。

ASP.NET の構成は階層に従っていることに注意してください。各 web.config ファイルでは、構成設定が含まれているフォルダーとその下のすべての子ディレクトリに適用さ*れます。*

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>プロジェクトに対して SSL を有効にする

 Secure Sockets Layer (SSL) は、Web サーバーと Web クライアント間の通信に定義されたプロトコルで、暗号化によって通信の安全性を強化することができます。 SSL を使わないと、クライアントとサーバー間で送信されるデータが、ネットワークに物理的にアクセスできる第三者によるパケット スニッフィングの標的になります。 また、プレーンな HTTP を使用すると、いくつかの一般的な認証方式の安全性も低下します。 具体的には、基本認証とフォーム認証で送信する資格情報が暗号化されません。 安全性を確保するには、これらの認証方式で SSL を使用する必要があります。 

1. **ソリューションエクスプローラー**で、**ウィングヒントの toys**プロジェクトをクリックし、 **F4**キーを押して **[プロパティ]** ウィンドウを表示します。
2. **SSL Enabled**を `true`に変更します。
3. 後で使用するための **SSL URL** をコピーします。   
 Ssl Web サイトを以前に作成した場合を除き、SSL URL は `https://localhost:44300/` になります (以下の図を参照)。   
    ![プロジェクト プロパティ](checkout-and-payment-with-paypal/_static/image4.png)
4. **ソリューションエクスプローラー**で、**ウィングヒントの toys**プロジェクトを右クリックし、 **[プロパティ]** をクリックします。
5. 左側のタブで **[Web]** をクリックします。
6. 以前に保存した**SSL url**を使用するように**プロジェクト url**を変更します。   
    ![プロジェクトの Web プロパティ](checkout-and-payment-with-paypal/_static/image5.png)
7. **CTRL + S キーを押して**ページを保存します。
8. **Ctrl キーを押しながら F5 キーを押して** アプリケーションを実行します。 Visual Studio により、SSL の警告を回避するためのオプションが表示されます。
9. IIS Express SSL 証明書を信頼する場合は **[はい]** をクリックして続行します。   
    ![IIS Express SSL 証明書の詳細](checkout-and-payment-with-paypal/_static/image6.png)  
 セキュリティ警告が表示されます。
10. **[はい]** をクリックしてローカルホストに証明書をインストールします。   
    ![セキュリティ警告ダイアログ ボックス](checkout-and-payment-with-paypal/_static/image7.png)  
 ブラウザー ウィンドウが表示されます。

SSL を使用して、Web アプリケーションをローカルで簡単にテストできるようになりました。

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>OAuth 2.0 プロバイダーを追加する

ASP.NET Web フォームは、メンバーシップと認証のオプションが強化されています。 OAuth もこうした強化点の 1 つです。 OAuth は、Web、モバイル、およびデスクトップのアプリケーションからシンプルで標準的な方法で安全に認証するためのオープン プロトコルです。 ASP.NET Web フォームテンプレートでは、OAuth を使用して、Facebook、Twitter、Google、Microsoft を認証プロバイダーとして公開しています。 このチュートリアルでは Google のみを認証プロバイダーとして使用しますが、コードを少し変更すれば他のプロバイダーも使用できます。 他のプロバイダーを実装する手順は、このチュートリアルで説明する手順とほとんど同じです。

このチュートリアルでは、認証の他にロールを使用して権限を付与します。 `canEdit` ロールに追加したユーザーだけが連絡先を変更 (作成、編集、削除) できます。

> [!NOTE] 
> 
> Windows Live アプリケーションは、実用的な web サイトのライブ URL のみを受け入れるため、ログインのテストにローカル web サイトの URL を使用することはできません。

次の手順を実行することで、Google 認証プロバイダーを追加できます。

1. *アプリ\_Start\Startup.Auth.cs*ファイルを開きます。
2. `app.UseGoogleAuthentication()` メソッドのコメント文字を削除して、メソッドを次のような記述にします。 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. [Google Developers Console](https://console.developers.google.com/)にアクセスします。 Google デベロッパーの電子メール アカウント (gmail.com) でサインインする必要があります。 Google アカウントを持っていない場合は、 **[Create an account]** リンクを選択します。   
   **Google Developers Console**が表示されます。   
    ![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)
4. **[プロジェクトの作成]** ボタンをクリックし、プロジェクトの名前と ID を入力します (既定値を使用できます)。 次に、[**アグリーメント] チェックボックス**と **[作成]** ボタンをクリックします。  

    ![Google-新しいプロジェクト](checkout-and-payment-with-paypal/_static/image9.png)

   新しいプロジェクトが数秒で作成され、新しいプロジェクトのページがブラウザーに表示されます。
5. 左側のタブで、[ **api &amp; auth**] をクリックし、 **[資格情報]** をクリックします。
6. **[OAuth]** の **[新しいクライアント ID の作成]** をクリックします。   
   **[Create Client ID]** ダイアログ ボックスが表示されます。   
    ![Google - クライアント ID の作成](checkout-and-payment-with-paypal/_static/image10.png)
7. **[クライアント ID の作成]** ダイアログボックスで、アプリケーションの種類の既定の**Web アプリケーション**をそのまま使用します。
8. 承認された**JavaScript オリジン**を、このチュートリアルの前半で使用した ssl URL (他の ssl プロジェクトを作成していない場合は`https://localhost:44300/`) に設定します。   
   この URL は、アプリケーションのオリジンです。 このサンプルでは、localhost テスト URL だけを入力します。 ただし、複数の Url を入力して、localhost と運用環境を考慮することができます。
9. **[Authorized Redirect URI]** には次の値を設定します。 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   この値は、ASP.NET OAuth ユーザーが Google の OAuth サーバーとの通信に使用する URI です。 上記で使用した SSL URL を記憶します (他の SSL プロジェクトを作成していない場合は `https://localhost:44300/`)。
10. **[クライアント ID の作成]** ボタンをクリックします。
11. Google 開発者コンソールの左側のメニューで、 **[同意画面]** メニュー項目をクリックし、電子メールアドレスと製品名を設定します。 フォームが完了したら、 **[保存]** をクリックします。
12. **[Api]** メニュー項目をクリックして下にスクロールし、 **[Google + API]** の横にある **[オフ]** ボタンをクリックします。   
    このオプションを受け入れると、Google + API が有効になります。
13. また、 **Owin** NuGet パッケージをバージョン3.0.0 に更新する必要があります。   
    **[ツール]** メニューの **[nuget パッケージマネージャー]** を選択し、 **[ソリューションの nuget パッケージの管理]** を選択します。  
    **[NuGet パッケージの管理]** ウィンドウで、 **Owin**パッケージを検索し、バージョン3.0.0 に更新します。
14. Visual Studio で、**クライアント ID**と**クライアントシークレット**をコピーしてメソッドに貼り付けることにより、 *Startup.Auth.cs*ページの `UseGoogleAuthentication` メソッドを更新します。 次に示す**クライアント ID**と**クライアントシークレット**の値はサンプルであり、機能しません。 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. **Ctrl キーを押しながら F5 キーを押して** アプリケーションをビルドし、実行します。 **[Log in]** リンクをクリックします。
16. **[別のサービスを使用してログインする]** で、 **[Google]** をクリックします。  
    ![ログイン](checkout-and-payment-with-paypal/_static/image11.png)
17. 資格情報の入力が必要な場合、Google のサイトにリダイレクトされるので、リダイレクト先のサイトで資格情報を入力します。  
    ![Google - サインイン](checkout-and-payment-with-paypal/_static/image12.png)
18. 資格情報を入力すると、作成した web アプリケーションにアクセス許可を付与するように求められます。  
    ![プロジェクトのデフォルト サービス アカウント](checkout-and-payment-with-paypal/_static/image13.png)
19. **[Accept]\(受け入れる\)** をクリックします。 これで、**ウィングヒント toys**アプリケーションの**登録**ページにリダイレクトされ、Google アカウントを登録できるようになります。  
    ![Google アカウントへの登録](checkout-and-payment-with-paypal/_static/image14.png)
20. Google アカウントに使用するローカルの電子メール登録名を変更できますが、通常は既定の電子メール エイリアス (認証に使用したエイリアス) を変更しません。 上に示すよう**に、[ログイン**] をクリックします。

### <a name="modifying-login-functionality"></a>ログイン機能の変更

このチュートリアルシリーズで既に説明したように、既定では、ユーザー登録機能の多くが ASP.NET Web Forms テンプレートに含まれています。 次に、既定の*login.aspx*ページを変更し、`MigrateCart` メソッドを呼び出すように .aspx ページを*登録*します。 `MigrateCart` メソッドを使用すると、新しくログインしたユーザーを匿名のショッピングカートに関連付けることができます。 ユーザーとショッピングカートを関連付けることにより、Wingtip Toys サンプルアプリケーションは、ユーザーのショッピングカートを訪問後に管理できるようになります。

1. **ソリューションエクスプローラー**で、*アカウント*フォルダーを見つけて開きます。
2. 次のように表示されるように、 *Login.aspx.cs*という名前の分離コードページを変更して、黄色で強調表示されているコードを含めます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. *Login.aspx.cs*ファイルを保存します。

ここでは、`MigrateCart` メソッドの定義がないという警告は無視してかまいません。 このチュートリアルでは、少し後で追加します。

*Login.aspx.cs*分離コードファイルは、ログインメソッドをサポートしています。 Login.aspx ページを調べると、このページに [ログイン] ボタンが含まれていることがわかります。このボタンをクリックすると、コードビハインドで `LogIn` ハンドラーがトリガーされます。

*Login.aspx.cs*の `Login` メソッドが呼び出されると、`usersShoppingCart` という名前のショッピングカートの新しいインスタンスが作成されます。 ショッピングカートの ID (GUID) が取得され、`cartId` 変数に設定されます。 次に、`MigrateCart` メソッドが呼び出され、ログインユーザーの `cartId` と名前の両方がこのメソッドに渡されます。 ショッピングカートを移行すると、匿名ショッピングカートの識別に使用される GUID がユーザー名に置き換えられます。

ユーザーがログインするときにショッピングカートを移行するために*Login.aspx.cs*分離コードファイルを変更するだけでなく、ユーザーが新しいアカウントを作成してログインするときに、ショッピングカートを移行するように*Register.aspx.cs 分離コードファイル*を変更する必要もあります。

1. *Account*フォルダーで、 *Register.aspx.cs*という名前の分離コードファイルを開きます。
2. 次のように、コードを黄色で含めてコードビハインドファイルを変更します。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. *Register.aspx.cs*ファイルを保存します。 ここでも、`MigrateCart` メソッドに関する警告は無視してください。

`CreateUser_Click` イベントハンドラーで使用したコードは、`LogIn` メソッドで使用したコードと非常によく似ていることに注意してください。 ユーザーがサイトに登録またはログインすると、`MigrateCart` メソッドの呼び出しが行われます。

## <a name="migrating-the-shopping-cart"></a>ショッピングカートの移行

これで、ログインと登録のプロセスが更新されたので、`MigrateCart` 方法を使用して、ショッピングカートを移行するコードを追加できます。

1. **ソリューションエクスプローラー**で、 *Logic*フォルダーを見つけて、 *ShoppingCartActions.cs*クラスファイルを開きます。
2. 次のように、 *ShoppingCartActions.cs*ファイルのコードが次のように表示されるように、黄色で強調表示されているコードを*ShoppingCartActions.cs*ファイルの既存のコードに追加します。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

`MigrateCart` メソッドは、既存の cartId を使用して、ユーザーのショッピングカートを検索します。 次に、すべてのショッピングカート項目をループし、`CartItem` スキーマによって指定された `CartId` プロパティをログインユーザー名に置き換えます。

### <a name="updating-the-database-connection"></a>データベース接続を更新しています

構築済みの Wingtip Toys サンプルアプリケーションを使用してこの**チュートリアルに従う**場合は、既定のメンバーシップデータベースを再作成する必要があります。 既定の接続文字列を変更することで、次回アプリケーションを実行したときにメンバーシップデータベースが作成されます。

1. プロジェクトのルートにある*web.config ファイルを開きます。*
2. 既定の接続文字列を更新して、次のように表示されるようにします。   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>PayPal の統合

PayPal は、オンラインの商人による支払いを受け入れる web ベースの課金プラットフォームです。 このチュートリアルでは、PayPal の高速チェックアウト機能をアプリケーションに統合する方法について説明します。 Express Checkout では、顧客が PayPal を使用して、ショッピングカートに追加した商品の支払いを行うことができます。

### <a name="create-paypal-test-accounts"></a>PayPal テストアカウントの作成

PayPal テスト環境を使用するには、開発者テストアカウントを作成して確認する必要があります。 開発者テストアカウントを使用して、購入者テストアカウントと販売者テストアカウントを作成します。 開発者テストアカウントの資格情報では、Wingtip Toys サンプルアプリケーションが PayPal テスト環境にアクセスすることもできます。

1. ブラウザーで、PayPal 開発者テストサイトに移動します。   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. PayPal 開発者アカウントを持っていない場合は、 **[サインアップ]** をクリックし、サインアップ手順に従って新しいアカウントを作成します。 既存の PayPal 開発者アカウントを持っている場合は、 **[ログイン]** をクリックしてサインインします。 Wingtip Toys サンプルアプリケーションをテストするには、このチュートリアルの後半で PayPal 開発者アカウントが必要です。
3. PayPal 開発者アカウントにサインアップしたばかりの場合は、paypal で PayPal 開発者アカウントを確認することが必要になる場合があります。 アカウントは、PayPal が電子メールアカウントに送信した手順に従って確認できます。 PayPal 開発者アカウントを確認したら、PayPal 開発者テストサイトに戻ります。
4. Paypal 開発者アカウントを使用して PayPal developer サイトにログインした後は、PayPal 購入者テストアカウントを作成する必要があります (まだお持ちでない場合)。 購入者テストアカウントを作成するには、PayPal サイトで **[アプリケーション]** タブをクリックし、 **[サンドボックスアカウント]** をクリックします。   
 **[サンドボックステストアカウント]** ページが表示されます。   

    > [!NOTE] 
    > 
    > PayPal 開発者サイトには、既にマーチャントテストアカウントが用意されています。

    ![PayPal を使用したチェックアウトと支払い-サンドボックステストアカウント](checkout-and-payment-with-paypal/_static/image15.png)
5. サンドボックステストアカウント ページで、**アカウントの作成** をクリックします。
6. **[テストアカウントの作成]** ページで、購入者テストアカウントの電子メールとパスワードを選択します。   

    > [!NOTE] 
    > 
    > このチュートリアルの最後に Wingtip Toys サンプルアプリケーションをテストするには、購入者の電子メールアドレスとパスワードが必要です。

    ![PayPal を使用したチェックアウトと支払い-サンドボックステストアカウント](checkout-and-payment-with-paypal/_static/image16.png)
7. **[アカウントの作成]** ボタンをクリックして購入者テストアカウントを作成します。  
 **[サンドボックステストアカウント]** ページが表示されます。 

    ![PayPal-PayPal アカウントを使用したチェックアウトと支払い](checkout-and-payment-with-paypal/_static/image17.png)
8. **[サンドボックステストアカウント]** ページで、**進行**中の電子メールアカウントをクリックします。  
    **プロファイル**と**通知**のオプションが表示されます。
9. **[プロファイル]** オプションを選択し、 **[api 資格情報]** をクリックして、マーチャントテストアカウントの api 資格情報を表示します。
10. テスト API 資格情報をメモ帳にコピーします。

Wingtip Toys サンプルアプリケーションから PayPal テスト環境への API 呼び出しを行うには、表示されているクラシックテスト API 資格情報 (ユーザー名、パスワード、署名) が必要です。 次の手順で資格情報を追加します。

### <a name="add-paypal-class-and-api-credentials"></a>PayPal クラスと API 資格情報の追加

ほとんどの PayPal コードを1つのクラスに配置します。 このクラスには、PayPal との通信に使用されるメソッドが含まれています。 また、PayPal の資格情報をこのクラスに追加します。

1. Visual Studio 内の Wingtip Toys サンプルアプリケーションで、 **Logic**フォルダーを右クリックし、[ **Add** -&gt;**新しい項目**] を選択します。   
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. 左側の **[インストール済み]** ウィンドウの **[ビジュアルC# ]** で、 **[コード]** を選択します。
3. 中央のウィンドウで、 **[クラス]** を選択します。 この新しいクラスに**PayPalFunctions.cs**という名前を指定します。
4. **[追加]** をクリックします。  
   新しいクラスファイルがエディターに表示されます。
5. 既定のコードを以下のコードに置き換えます。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. このチュートリアルで前に表示したマーチャント API 資格情報 (ユーザー名、パスワード、署名) を追加して、PayPal テスト環境への関数呼び出しを行うことができるようにします。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> このサンプルアプリケーションでは、単に資格情報をC#ファイル (.cs) に追加します。 ただし、実装されたソリューションでは、構成ファイルで資格情報を暗号化することを検討する必要があります。

NVPAPICaller クラスには、PayPal 機能の大部分が含まれています。 クラスのコードは、PayPal テスト環境からのテスト購入を行うために必要なメソッドを提供します。 購入するには、次の3つの PayPal 関数を使用します。

- `SetExpressCheckout` 関数
- `GetExpressCheckoutDetails` 関数
- `DoExpressCheckoutPayment` 関数

`ShortcutExpressCheckout` メソッドは、ショッピングカートからテスト購入情報と製品の詳細を収集し、`SetExpressCheckout` PayPal 関数を呼び出します。 `GetCheckoutDetails` メソッドは、購入の詳細を確認し、テストを購入する前に `GetExpressCheckoutDetails` PayPal 関数を呼び出します。 `DoCheckoutPayment` メソッドは、`DoExpressCheckoutPayment` PayPal 関数を呼び出して、テスト環境からのテストの購入を完了します。 残りのコードでは、文字列のエンコード、文字列のデコード、配列の処理、資格情報の確認など、PayPal のメソッドとプロセスをサポートしています。

> [!NOTE] 
> 
> PayPal では、 [paypal の API 仕様](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)に基づいて、オプションの購入の詳細を含めることができます。 Wingtip Toys サンプルアプリケーションのコードを拡張することで、ローカライズの詳細、製品の説明、税金、顧客のサービス番号、およびその他のオプションのフィールドを含めることができます。

**ShortcutExpressCheckout**メソッドに指定されている return および Cancel の url では、ポート番号が使用されていることに注意してください。

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

Visual Web Developer で SSL を使用して web プロジェクトを実行する場合は、通常、web サーバーに対してポート44300が使用されます。 上記のように、ポート番号は44300です。 アプリケーションを実行すると、別のポート番号が表示される場合があります。 このチュートリアルの最後に Wingtip Toys サンプルアプリケーションを正常に実行できるように、コードでポート番号を正しく設定する必要があります。 このチュートリアルの次のセクションでは、ローカルホストのポート番号を取得し、PayPal クラスを更新する方法について説明します。

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>PayPal クラスの LocalHost ポート番号を更新する

Wingtip Toys サンプルアプリケーションは、PayPal テストサイトに移動し、Wingtip Toys サンプルアプリケーションのローカルインスタンスに戻ることによって、製品を購入します。 PayPal が正しい URL に戻るようにするには、上で説明した PayPal コードでローカルに実行されるサンプルアプリケーションのポート番号を指定する必要があります。

1. **ソリューションエクスプローラー**でプロジェクト名 (ウィングの**おもちゃ**) を右クリックし、 **[プロパティ]** を選択します。
2. 左側の列で、 **[Web]** タブを選択します。
3. **[プロジェクト Url]** ボックスからポート番号を取得します。
4. 必要に応じて、 *PayPalFunctions.cs*ファイルの PayPal クラス (`NVPAPICaller`) の `returnURL` と `cancelURL` を更新して、web アプリケーションのポート番号を使用します。   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

これで、追加したコードが、ローカル Web アプリケーションで想定されているポートと一致するようになります。 PayPal は、ローカルコンピューターの正しい URL に戻ることができます。

### <a name="add-the-paypal-checkout-button"></a>PayPal の [チェックアウト] ボタンを追加する

これで、主な PayPal 関数がサンプルアプリケーションに追加されたので、これらの関数を呼び出すために必要なマークアップとコードの追加を開始できます。 最初に、ユーザーに表示される [チェックアウト] ボタンを [ショッピングカート] ページに追加する必要があります。

1. *ShoppingCart*ファイルを開きます。
2. ファイルの一番下までスクロールし、`<!--Checkout Placeholder -->` のコメントを見つけます。
3. コメントを `ImageButton` コントロールに置き換えて、マークアップが次のように置き換えられるようにします。  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. *ShoppingCart.aspx.cs*ファイルで、ファイルの末尾付近にある `UpdateBtn_Click` イベントハンドラーの後に、`CheckOutBtn_Click` イベントハンドラーを追加します。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. また、 *ShoppingCart.aspx.cs*ファイルで `CheckoutBtn`への参照を追加して、[新しいイメージ] ボタンが次のように参照されるようにします。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. 変更内容を*ShoppingCart*ファイルと*ShoppingCart.aspx.cs*ファイルの両方に保存します。
7. メニューから、[**デバッグ**-] を選択して、**ウィングヒント toys を構築**&gt;ます。  
   プロジェクトは、新しく追加された**ImageButton**コントロールを使用してリビルドされます。

### <a name="send-purchase-details-to-paypal"></a>購入の詳細を PayPal に送信する

ユーザーがショッピングカートページ (*ShoppingCart*) の **[チェックアウト]** ボタンをクリックすると、購入プロセスが開始されます。 次のコードは、製品を購入するために必要な最初の PayPal 関数を呼び出します。

1. *Checkout*フォルダーから、 *CheckoutStart.aspx.cs*という名前の分離コードファイルを開きます。   
   分離コードファイルを必ず開いてください。
2. 既存のコードを次のコードに置き換えます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

アプリケーションのユーザーがショッピングカートページの **[チェックアウト]** ボタンをクリックすると、ブラウザーは*CheckoutStart*ページに移動します。 *CheckoutStart*ページが読み込まれると、`ShortcutExpressCheckout` メソッドが呼び出されます。 この時点で、ユーザーは PayPal テスト web サイトに転送されます。 PayPal サイトでは、ユーザーが PayPal 資格情報を入力し、購入の詳細を確認し、PayPal アグリーメントを受け入れ、`ShortcutExpressCheckout` メソッドが完了した Wingtip Toys サンプルアプリケーションに戻ります。 `ShortcutExpressCheckout` メソッドが完了すると、`ShortcutExpressCheckout` メソッドに指定された*CheckoutReview*ページにユーザーがリダイレクトされます。 これにより、ユーザーは Wingtip Toys サンプルアプリケーション内から注文の詳細を確認できます。

### <a name="review-order-details"></a>注文の詳細の確認

PayPal から戻った後、Wingtip Toys サンプルアプリケーションの*CheckoutReview*ページに注文の詳細が表示されます。 このページでは、ユーザーは製品を購入する前に注文の詳細を確認できます。 *CheckoutReview*ページは次のように作成する必要があります。

1. *Checkout*フォルダーで、 *CheckoutReview*という名前のページを開きます。
2. 既存のマークアップを次のように置き換えます。   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. *CheckoutReview.aspx.cs*という名前の分離コードページを開き、既存のコードを次のコードに置き換えます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

**DetailsView**コントロールは、PayPal から返された注文の詳細を表示するために使用されます。 また、上記のコードでは、注文の詳細を `OrderDetail` オブジェクトとして Wingtip Toys データベースに保存します。 ユーザーが **[注文の完了]** ボタンをクリックすると、 *CheckoutComplete*ページにリダイレクトされます。

> [!NOTE] 
> 
> **ヒント**
> 
> *CheckoutReview*ページのマークアップで、ページの下部付近にある**DetailsView**コントロール内の項目のスタイルを変更するために `<ItemStyle>` タグが使用されていることに注意してください。 **デザインビュー**でページを表示するには (Visual Studio の左下隅にある **[デザイン]** を選択)、 **detailsview**コントロールを選択し、**スマートタグ**(コントロールの右上にある矢印アイコン) を選択します。これにより、 **detailsview タスク**を表示できます。
> 
> ![PayPal を使用したチェックアウトと支払い-フィールドの編集](checkout-and-payment-with-paypal/_static/image18.png)
> 
> **[フィールドの編集]** を選択すると、 **[フィールド]** ダイアログボックスが表示されます。 このダイアログボックスでは、 **DetailsView**コントロールの**itemstyle**などのビジュアルプロパティを簡単に制御できます。
> 
> ![[PayPal-フィールド] ダイアログボックスでのチェックアウトと支払い](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>購入を完了する

*CheckoutComplete*ページでは、PayPal から購入を行います。 前述のように、ユーザーは、アプリケーションが*CheckoutComplete*ページに移動する前に、 **[Complete Order]** ボタンをクリックする必要があります。

1. *Checkout*フォルダーで、 *CheckoutComplete*という名前のページを開きます。
2. 既存のマークアップを次のように置き換えます。   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. *CheckoutComplete.aspx.cs*という名前の分離コードページを開き、既存のコードを次のコードに置き換えます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

*CheckoutComplete*ページが読み込まれると、`DoCheckoutPayment` メソッドが呼び出されます。 前述のように、`DoCheckoutPayment` 方法では、PayPal テスト環境からの購入を完了します。 PayPal が注文の購入を完了すると、 *CheckoutComplete*ページに、購入者に `ID` 支払いトランザクションが表示されます。

### <a name="handle-cancel-purchase"></a>購入取り消しの処理

ユーザーが購入を取り消すことにした場合は、 *CheckoutCancel*ページにリダイレクトされ、注文が取り消されたことがわかります。

1. *Checkout*フォルダーの*CheckoutCancel*という名前のページを開きます。
2. 既存のマークアップを次のように置き換えます。   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>購入エラーの処理

購入処理中のエラーは、 *CheckoutError*ページによって処理されます。 *CheckoutStart*ページ、 *CheckoutReview*ページ、および*CheckoutComplete*ページの分離コードは、エラーが発生した場合に、それぞれが*CheckoutError*ページにリダイレクトされます。

1. *Checkout*フォルダーの*CheckoutError*という名前のページを開きます。
2. 既存のマークアップを次のように置き換えます。   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

チェックアウト処理中にエラーが発生すると、 *CheckoutError*ページにエラーの詳細が表示されます。

## <a name="running-the-application"></a>アプリケーションの実行

アプリケーションを実行して、製品を購入する方法を確認します。 PayPal テスト環境で実行されることに注意してください。 実際の金額は交換されていません。

1. すべてのファイルが Visual Studio に保存されていることを確認します。
2. Web ブラウザーを開き、 [https://developer.paypal.com](https://developer.paypal.com/)に移動します。
3. このチュートリアルの前の手順で作成した PayPal 開発者アカウントでログインします。  
   PayPal の開発者サンドボックスの場合は、 [https://developer.paypal.com](https://developer.paypal.com/)でログインして、高速チェックアウトをテストする必要があります。 これは、paypal のライブ環境ではなく、PayPal のサンドボックステストにのみ適用されます。
4. Visual Studio で、 **F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。  
   データベースを再構築すると、ブラウザーが開き、 *default.aspx*ページが表示されます。
5. 商品カテゴリ ("車" など) を選択し、各製品の横にある **[カートに追加]** をクリックして、3つの異なる製品をショッピングカートに追加します。  
   ショッピングカートには、選択した製品が表示されます。
6. **[PayPal]** ボタンをクリックしてチェックアウトします。 

    ![PayPal を使用したチェックアウトと支払い-カート](checkout-and-payment-with-paypal/_static/image20.png)

   確認するには、Wingtip Toys サンプルアプリケーションのユーザーアカウントが必要です。
7. ページの右側にある**Google**リンクをクリックして、既存の gmail.com 電子メールアカウントでログインします。  
   Gmail.com アカウントを持っていない場合は、 [www.gmail.com](https://www.gmail.com/)でテスト目的で作成できます。 [登録] をクリックして、標準のローカルアカウントを使用することもできます。 

    ![PayPal を使用したチェックアウトと支払い-ログイン](checkout-and-payment-with-paypal/_static/image21.png)
8. Gmail アカウントとパスワードを使用してサインインします。 

    ![PayPal を使用したチェックアウトと支払い-Gmail サインイン](checkout-and-payment-with-paypal/_static/image22.png)
9. **[ログイン]** ボタンをクリックして、gmail アカウントを Wingtip Toys サンプルアプリケーションのユーザー名に登録します。 

    ![PayPal を使用した精算と支払い-アカウントの登録](checkout-and-payment-with-paypal/_static/image23.png)
10. PayPal テストサイトで、このチュートリアルの前の手順で作成した**購入**者の電子メールアドレスとパスワードを追加し、 **[ログイン]** ボタンをクリックします。 

    ![PayPal を使用したチェックアウトと支払い-PayPal サインイン](checkout-and-payment-with-paypal/_static/image24.png)
11. PayPal ポリシーに同意し、 **[同意して続行]** ボタンをクリックします。  
    このページは、この PayPal アカウントを初めて使用するときにのみ表示されることに注意してください。 ここでも、これはテストアカウントであり、実際の金額は交換されないことに注意してください。 

    ![PayPal を使用した精算と支払い-PayPal ポリシー](checkout-and-payment-with-paypal/_static/image25.png)
12. PayPal テスト環境の確認 ページで注文情報を確認し、**続行** をクリックします。 

    ![PayPal を使用した精算と支払い-レビュー情報](checkout-and-payment-with-paypal/_static/image26.png)
13. *CheckoutReview*ページで注文金額を確認し、生成された出荷先住所を表示します。 次に、 **[注文の完了]** ボタンをクリックします。 

    ![PayPal を使用したチェックアウトと支払い-注文レビュー](checkout-and-payment-with-paypal/_static/image27.png)
14. **CheckoutComplete**ページには、支払いトランザクション ID が表示されます。 

    ![PayPal を使用したチェックアウトと支払い-チェックアウト完了](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>データベースの確認

アプリケーションの実行後に Wingtip Toys サンプルアプリケーションデータベースの更新されたデータを確認することで、アプリケーションが製品の購入を正常に記録したことを確認できます。

このチュートリアルシリーズで既に説明したように、 **[データベースエクスプローラー]** ウィンドウ (Visual Studio の**サーバーエクスプローラー**ウィンドウ) を使用して、*ウィングの toys. .mdf*データベースファイルに格納されているデータを調べることができます。

1. ブラウザーウィンドウが開いたままの場合は閉じます。
2. Visual Studio で、**ソリューションエクスプローラー**の上部にある **[すべてのファイルを表示]** アイコンを選択して、**アプリ\_データ**フォルダーを展開できるようにします。
3. [**アプリ\_データ**] フォルダーを展開します。  
 場合によっては、フォルダーの **[すべてのファイルを表示]** アイコンを選択する必要があります。
4. *ウィングヒントの toys*データベースファイルを右クリックし、 **[開く]** を選択します。  
    **サーバーエクスプローラー**が表示されます。
5. **[テーブル]** フォルダーを展開します。
6. **Orders**テーブルを右クリックし、 **[テーブルデータの表示]** をクリックします。  
 **Orders**テーブルが表示されます。
7. **PaymentTransactionID**列を確認して、成功したトランザクションを確認します。 

    ![PayPal を使用した精算と支払い-データベースの確認](checkout-and-payment-with-paypal/_static/image29.png)
8. **Orders**テーブルウィンドウを閉じます。
9. サーバーエクスプローラーで、 **OrderDetails**テーブルを右クリックし、 **[テーブルデータの表示]** をクリックします。
10. **OrderDetails**テーブルの `OrderId` と `Username` の値を確認します。 これらの値は、 **Orders**テーブルに含まれる `OrderId` および `Username` の値と一致することに注意してください。
11. **OrderDetails**テーブルウィンドウを閉じます。
12. Wingtip Toys データベースファイル (*ウィングのおもちゃ*) を右クリックし、[接続を**閉じる**] を選択します。
13. **[ソリューションエクスプローラー]** ウィンドウが表示されない場合は、**サーバーエクスプローラー**ウィンドウの下部にある **[ソリューションエクスプローラー]** をクリックして、もう一度**ソリューションエクスプローラー**を表示します。

## <a name="summary"></a>まとめ

このチュートリアルでは、注文と注文の詳細スキーマを追加して、製品の購入を追跡しました。 また、PayPal の機能を Wingtip Toys サンプルアプリケーションに統合しています。

## <a name="additional-resources"></a>その他のリソース

[ASP.NET 構成の概要](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET Web フォームアプリを Azure App Service にデプロイする](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure-無料試用版](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>免責事項

このチュートリアルには、サンプルコードが含まれています。 このようなサンプルコードは、いかなる種類の保証も伴わず、「現状有姿」で提供されます。 そのため、Microsoft では、サンプルコードの精度、整合性、品質を保証していません。 独自のリスクでサンプルコードを使用することに同意します。 どのような場合でも、どのようなサンプルコードやコンテンツについても、どのような方法でもお客様に対して一切の責任を負いません。ただし、すべてのサンプルコード、コンテンツ、またはサンプルコードを使用した結果として発生するあらゆる種類の損失や損害については一切ありません。 お客様は、お客様が通知を受け取り、補償に同意することになります。マイクロソフトは、いかなる損失、損失の損害、けが、または損害についても、いかなる場合でも、または投稿したマテリアルによって occasioned されたかどうかにかかわらず、いかなるものでもありません。送信、使用、またはその中に表示されているビューへの制限はありません。

> [!div class="step-by-step"]
> [前へ](shopping-cart.md)
> [次へ](membership-and-administration.md)

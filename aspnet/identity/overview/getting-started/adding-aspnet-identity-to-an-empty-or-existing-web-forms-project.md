---
uid: identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
title: 空または既存の Web フォームプロジェクトへの ASP.NET Identity の追加-ASP.NET 4.x
author: raquelsa
description: このチュートリアルでは、ASP.NET Identity (ASP.NET のメンバーシップシステム) を ASP.NET アプリケーションに追加する方法について説明します。 新しい Web フォームまたは MVC を作成する場合
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 1cbc0ed2-5bd6-4b62-8d34-4c193dcd8b25
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: 8e82951d57f0b8052ee3f6530a7470be7d030206
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471976"
---
# <a name="adding-aspnet-identity-to-an-empty-or-existing-web-forms-project"></a>ASP.NET Identity を空または既存の Web フォーム プロジェクトに追加する

> このチュートリアルでは、ASP.NET (の新しいメンバーシップシステム) を ASP.NET アプリケーションに[ASP.NET Identity](introduction-to-aspnet-identity.md)追加する方法について説明します。
> 
> 個々のアカウントを使用して Visual Studio 2017 RTM で新しい Web フォームまたは MVC プロジェクトを作成すると、Visual Studio は必要なすべてのパッケージをインストールし、必要なすべてのクラスを追加します。 このチュートリアルでは、既存の Web フォームプロジェクトまたは新しい空のプロジェクトに ASP.NET Identity サポートを追加する手順について説明します。 ここでは、インストールする必要があるすべての NuGet パッケージと、追加する必要があるクラスについて説明します。 ここでは、ユーザー管理と認証の主要なエントリポイント Api をすべて強調表示しながら、新しいユーザーを登録してログインするためのサンプル Web フォームを使用します。 このサンプルでは、Entity Framework 上に構築された SQL データストレージに ASP.NET Identity 既定の実装を使用します。 このチュートリアルでは、SQL database に LocalDB を使用します。
> 

## <a name="get-started-with-aspnet-identity"></a>ASP.NET Identity を使ってみる

1. まず、 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)をインストールして実行します。
2. スタートページで **[新しいプロジェクト]** を選択するか、メニューを使用して **[ファイル]** 、 **[新しいプロジェクト]** の順に選択します。
3. 左側のウィンドウで、 **[ビジュアルC# ]** を展開し、 **[web]** 、 **[ASP.NET web Application (.net Framework)]** の順に選択します。 プロジェクトに "WebFormsIdentity" という名前を指定し、[ **OK]** を選択します。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image17.png)
4. **[New ASP.NET Project]** ダイアログボックスで、**空**のテンプレートを選択します。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image2.png)  
  
   **[認証の変更]** ボタンは無効になっており、このテンプレートでは認証がサポートされていないことに注意してください。 Web フォーム、MVC、および Web API テンプレートを使用すると、認証方法を選択できます。

## <a name="add-identity-packages-to-your-app"></a>アプリに Id パッケージを追加する

ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選択します。 **Microsoft .net framework**パッケージを検索してインストールします。 
  
![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image15.png)
  
このパッケージは依存関係パッケージをインストールすることに注意してください。**Entityframework**と**Microsoft ASP.NET Identity Core**。

## <a name="add-a-web-form-to-register-users"></a>ユーザーを登録するための web フォームを追加する

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[追加]** 、 **[Web フォーム]** の順に選択します。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image4.png)
2. **[項目の名前の指定]** ダイアログボックスで、新しい Web フォーム**Register**という名前を入力し、 **[OK]** を選択します。
3. 生成された*login.aspx*ファイルのマークアップを次のコードに置き換えます。 コードの変更が強調表示されています。 

    [!code-html[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample1.aspx?highlight=9,12-40)]

    > [!NOTE]
    > これは、新しい ASP.NET Web フォームプロジェクトを作成するときに作成される、 *default.aspx*ファイルの簡略化されたバージョンです。 上のマークアップは、フォームフィールドと、新しいユーザーを登録するボタンを追加します。
4. *Register.aspx.cs*ファイルを開き、ファイルの内容を次のコードに置き換えます。

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample2.cs)]

    > [!NOTE] 
    > 
    > 1. 上記のコードは、新しい ASP.NET Web フォームプロジェクトを作成するときに作成される*Register.aspx.cs*ファイルの簡略化されたバージョンです。
    > 2. 既定の*entityframework*クラスは、 *iuser*インターフェイスの既定の entityframework 実装です。 *Iuser*インターフェイスは ASP.NET Identity コアのユーザーのための最小限のインターフェイスです。
    > 3. *Userstore*クラスは、ユーザーストアの既定の entityframework の実装です。 このクラスは、ASP.NET Identity コアの最小インターフェイスを実装します。*IUserStore*、 *IUserLoginStore*、 *IUserClaimStore* 、および*IUserRoleStore*。
    > 4. *Usermanager*クラスは、ユーザーに関連する api を公開します。これにより、自動的に*usermanager*に変更が保存されます。
    > 5. Id 操作の結果を表す、id の*結果*クラス。
5. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[追加]** 、 **[ASP.NET フォルダーの追加]** 、[**アプリ\_データ**] の順に選択します。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image5.png)
6. *Web.config ファイルを*開き、ユーザー情報を格納するために使用するデータベースの接続文字列エントリを追加します。 データベースは、Entity Framework によって Id エンティティに対して実行時に作成されます。 接続文字列は、新しい Web フォームプロジェクトを作成するときに作成されるものと似ています。 強調表示されたコードは、追加する必要があるマークアップを示しています。

    [!code-xml[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample3.xml?highlight=11-14)]
    
    > [!NOTE] 
    > Visual Studio 2015 以降の場合は、接続文字列で `(localdb)\v11.0` を `(localdb)\MSSQLLocalDB` に置き換えます。
    
7. プロジェクトの file *Register .aspx*を右クリックし、 **[スタートページとして設定]** を選択します。 Ctrl キーを押しながら F5 キーを押して、web アプリケーションをビルドして実行します。 新しいユーザー名とパスワードを入力し、 **[Register]** \ (登録 \) を選択します。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image6.png)  

    > [!NOTE]
    > ASP.NET Identity は検証をサポートしており、このサンプルでは、Id コアパッケージから取得されたユーザーとパスワードの検証コントロールの既定の動作を確認できます。 User (`UserValidator`) の既定の検証コントロールには、既定値が `true`に設定された `AllowOnlyAlphanumericUserNames` プロパティがあります。 パスワードの既定の検証 (`MinimumLengthValidator`) では、パスワードが6文字以上であることが保証されます。 これらの検証コントロールは、カスタム検証を行う場合にオーバーライドできる `UserManager` のプロパティです。

## <a name="verify-the-localdb-identity-database-and-tables-generated-by-entity-framework"></a>LocalDb Id データベースと、によって生成されたテーブルを確認し Entity Framework

1. **[表示]** メニューの **[サーバーエクスプローラー]** をクリックします。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image7.png)
2. **Defaultconnection (WebFormsIdentity)** を展開し、 **[テーブル]** を展開します。次に、 **[AspNetUsers]** を右クリックし、 **[テーブルデータの表示]** を選択します。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image8.png)  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image9.png)

## <a name="configure-the-application-for-owin-authentication"></a>OWIN 認証用にアプリケーションを構成する

この時点で、ユーザーを作成するためのサポートが追加されました。 ここでは、ユーザーのログインに認証を追加する方法について説明します。 ASP.NET Identity は、フォーム認証に Microsoft OWIN Authentication ミドルウェアを使用します。 OWIN Cookie 認証は、 [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)または IIS でホストされている任意のフレームワークで使用できる cookie と要求ベースの認証メカニズムです。 このモデルでは、ASP.NET MVC や Web フォームを含む複数のフレームワークで同じ認証パッケージを使用できます。 プロジェクト Katana と、ホストに依存しないミドルウェアを実行する方法の詳細については[、Katana プロジェクト](https://msdn.microsoft.com/magazine/dn451439.aspx)でのはじめにに関する説明を参照してください。

## <a name="install-authentication-packages-to-your-application"></a>アプリケーションへの認証パッケージのインストール

1. ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選択します。 ***Owin***パッケージを検索してインストールします。 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image16.png)

2. ***Owin***パッケージを検索してインストールします。

    > [!NOTE]
    > **Owin**パッケージには、ASP.NET Identity コアパッケージによって使用される Owin 認証ミドルウェアを管理および構成するための Owin 拡張クラスのセットが含まれています。
    > **Owin**パッケージには、ASP.NET 要求パイプラインを使用して Owin ベースのアプリケーションを IIS で実行できるようにする Owin サーバーが含まれています。 詳細について[は、「OWIN ミドルウェア in THE IIS integrated pipeline](../../../aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline.md)」を参照してください。

## <a name="add-owin-startup-and-authentication-configuration-classes"></a>OWIN のスタートアップと認証の構成クラスを追加する

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[追加]** 、 **[新しい項目の追加]** の順に選択します。 [検索テキストボックス] ダイアログボックスで、「*owin*」と入力します。 クラスに "*Startup*" という名前を指定し、 **[追加]** を選択します。 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image11.png)
2. Startup.cs ファイルで、下の強調表示されているコードを追加して、OWIN cookie 認証を構成します。

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample4.cs?highlight=1,3,15-19)]

    > [!NOTE]
    > このクラスには、OWIN startup クラスを指定するための `OwinStartup` 属性が含まれています。 すべての OWIN アプリケーションには、アプリケーションパイプラインのコンポーネントを指定する startup クラスがあります。 このモデルの詳細については、「 [OWIN Startup Class Detection](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) 」を参照してください。

## <a name="add-web-forms-for-registering-and-signing-in-users"></a>ユーザーを登録してサインインするための web フォームを追加する

1. *Register.aspx.cs*ファイルを開き、登録が成功したときにユーザーにサインインする次のコードを追加します。

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample5.cs)]

    > [!NOTE] 
    > 
    > - ASP.NET Identity と OWIN Cookie 認証はクレームベースのシステムであるため、フレームワークでは、アプリ開発者がユーザーの[ClaimsIdentity](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.claimsidentity.aspx)を生成する必要があります。 ClaimsIdentity には、ユーザーが属するロールなど、ユーザーのすべての要求に関する情報が含まれています。 この段階で、ユーザーに対する要求をさらに追加することもできます。
    > - OWIN から AuthenticationManager を使用して `SignIn` を呼び出して、上記のように ClaimsIdentity に渡すことによって、ユーザーをサインインさせることができます。 このコードは、ユーザーにサインインし、cookie も生成します。 この呼び出しは、 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)モジュールで使用される[Formauthentication](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx)に似ています。
2. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[追加]** 、 **[Web フォーム]** の順に選択します。 Web フォームに**ログイン**名を指定します。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image12.png)
3. *Login.aspx*ファイルの内容を次のコードに置き換えます。

    [!code-aspx[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample6.aspx)]
4. *Login.aspx.cs*ファイルの内容を次の内容に置き換えます。

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample7.cs)]

    > [!NOTE] 
    > 
    > - `Page_Load` は現在のユーザーの状態を確認し、`Context.User.Identity.IsAuthenticated` の状態に基づいてアクションを実行するようになりました。
    >   **ログインしたユーザー名を表示**する:Microsoft ASP.NET Identity Framework には、ログインしているユーザーの `UserName` と `UserId` を取得できるようにするための拡張メソッドが追加され[ました。](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx) これらの拡張メソッドは、`Microsoft.AspNet.Identity.Core` アセンブリで定義されています。 これらの拡張メソッドは、 [HttpContext.User.Identity.Name](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)の代わりに使用されます。
    > - サインイン方法: `This` メソッドは、このサンプルの前の `CreateUser_Click` メソッドを置き換え、ユーザーが正常に作成された後にユーザーをサインインさせるようになりました。   
    >   Microsoft OWIN Framework では、`IOwinContext`への参照を取得するための拡張メソッドが `System.Web.HttpContext` に追加されました。 これらの拡張メソッドは `Microsoft.Owin.Host.SystemWeb` アセンブリで定義されています。 `OwinContext` クラスは、現在の要求で使用できる認証ミドルウェア機能を表す `IAuthenticationManager` プロパティを公開します。 OWIN から `AuthenticationManager` を使用し、`SignIn` を呼び出して、前述のように `ClaimsIdentity` に渡すことによって、ユーザーにサインインできます。 ASP.NET Identity と OWIN Cookie 認証はクレームベースのシステムであるため、フレームワークでは、ユーザーの `ClaimsIdentity` を生成するためにアプリが必要です。 `ClaimsIdentity` には、ユーザーが属するロールなど、ユーザーのすべての要求に関する情報が含まれています。 この段階で、ユーザーに対する要求をさらに追加することもできます。このコードはユーザーにサインインし、cookie も生成します。 この呼び出しは、 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)モジュールで使用される[Formauthentication](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx)に似ています。
    > - `SignOut` メソッド: OWIN から `AuthenticationManager` への参照を取得し、`SignOut`を呼び出します。 これは、 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)モジュールで使用される[FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)メソッドに似ています。
5. Ctrl キーを押し**ながら F5**キーを押して、web アプリケーションをビルドして実行します。 新しいユーザー名とパスワードを入力し、 **[Register]** \ (登録 \) を選択します。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image13.png)  
   メモ:この時点で、新しいユーザーが作成され、ログインされます。
6. **[ログアウト]** をクリックします。 ログインフォームにリダイレクトされます。
7. 無効なユーザー名またはパスワードを入力し、 **[ログイン]** ボタンを選択します。 
   `UserManager.Find` メソッドは、null とエラーメッセージを返します。"*ユーザー名またはパスワードが無効です*"が表示されます。
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image14.png)

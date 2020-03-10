---
uid: identity/overview/getting-started/introduction-to-aspnet-identity
title: ASP.NET Identity の概要-ASP.NET 4.x
author: jongalloway
description: ASP.NET メンバーシップシステムは、ASP.NET 2.0 を使用して2005に戻されました。そのため、web アプリケーションでは、さまざまな変更が行われています。
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 38717fc1-5989-43cf-952d-4007cc1dd923
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/introduction-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0268dfc16cd2cfb1e79ee14997a4c5eb247af950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471736"
---
# <a name="introduction-to-aspnet-identity"></a>ASP.NET Identity 入門

> ASP.NET メンバーシップシステムは、ASP.NET 2.0 を使用して2005に戻されました。そのため、web アプリケーションは通常、認証と承認を処理する方法に多くの変更が加えられています。 ASP.NET Identity は、web、電話、タブレット用の最新のアプリケーションを構築する際に、メンバーシップシステムがどのようなものである必要があるかを詳しく見ていきます。

## <a name="background-membership-in-aspnet"></a>背景: ASP.NET のメンバーシップ

### <a name="aspnet-membership"></a>ASP.NET メンバーシップ

[ASP.NET のメンバーシップ](https://msdn.microsoft.com/library/yh26yfzy(v=VS.100).aspx)は、フォーム認証に関連する2005に共通するサイトメンバーシップ要件と、ユーザー名、パスワード、およびプロファイルデータの SQL Server データベースを解決するように設計されています。 現在、web アプリケーション用のデータストレージオプションははるかに広範囲になっており、ほとんどの開発者は、サイトで認証と承認の機能にソーシャル id プロバイダーを使用できるようにしたいと考えています。 ASP.NET メンバーシップの設計の制限によって、この移行は困難になります。

- データベーススキーマは SQL Server 向けに設計されており、変更することはできません。 プロファイル情報を追加できますが、追加データは別のテーブルにパックされるため、プロファイルプロバイダー API を使用する場合を除き、どのような方法でもアクセスが困難になります。
- プロバイダーシステムを使用すると、バッキングデータストアを変更できますが、システムはリレーショナルデータベースに適した想定に基づいて設計されています。 メンバーシップ情報を非リレーショナルストレージメカニズム (Azure Storage テーブルなど) に格納するプロバイダーを作成することができますが、多くのコードを記述し、NoSQL データベースには適用されないメソッドの `System.NotImplementedException` の例外を大量に記述することで、リレーショナル設計を回避する必要があります。
- ログイン/ログアウト機能はフォーム認証に基づいているため、メンバーシップシステムで[OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)を使用することはできません。 OWIN には、認証用のミドルウェアコンポーネントが含まれています。これには、外部 id プロバイダー (Microsoft アカウント、Facebook、Google、Twitter など) を使用したログインのサポートや、オンプレミス Active Directory の組織アカウントを使用したログインなどがあります。Azure Active Directory。 OWIN には、OAuth 2.0、JWT、CORS のサポートも含まれています。

### <a name="aspnet-simple-membership"></a>ASP.NET Simple メンバーシップ

[ASP.NET simple メンバーシップ](../../../web-pages/overview/security/16-adding-security-and-membership.md)は、ASP.NET Web ページのメンバーシップシステムとして開発されました。 WebMatrix と Visual Studio 2010 SP1 でリリースされました。 単純なメンバーシップの目的は、Web ページアプリケーションにメンバーシップ機能を簡単に追加できるようにすることでした。

単純なメンバーシップを使用すると、ユーザープロファイル情報のカスタマイズが容易になりますが、ASP.NET メンバーシップに関する他の問題は引き続き共有され、いくつかの制限があります。

- 非リレーショナルストアにメンバーシップシステムデータを保持することは困難でした。
- OWIN で使用することはできません。
- 既存の ASP.NET メンバーシッププロバイダーではうまく機能せず、拡張もできません。

### <a name="aspnet-universal-providers"></a>ASP.NET ユニバーサル プロバイダー

[ASP.NET ユニバーサルプロバイダー](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)は Microsoft Azure SQL Database でメンバーシップ情報を永続化できるように開発されており、SQL Server Compact でも使用できます。 ユニバーサルプロバイダーは Entity Framework Code First 上に構築されています。これは、EF によってサポートされる任意のストアのデータを保持するためにユニバーサルプロバイダーを使用できることを意味します。 ユニバーサルプロバイダーでは、データベーススキーマも大幅にクリーンアップされています。

ユニバーサルプロバイダーは ASP.NET メンバーシップインフラストラクチャ上に構築されているので、SqlMembership プロバイダーと同じ制限があります。 つまり、リレーショナルデータベース向けに設計されており、プロファイルとユーザー情報をカスタマイズするのは困難です。 これらのプロバイダーでは、サインインとサインアウトの機能にもフォーム認証を使用します。

## <a name="aspnet-identity"></a>ASP.NET Identity

ASP.NET のメンバーシップのストーリーが長年にわたって進化したため、ASP.NET チームはお客様からのフィードバックから膨大なことを学んできました。

ユーザーが自分のアプリケーションに登録したユーザー名とパスワードを入力することによってサインインすることを前提としています。 Web がより社会的になりました。 ユーザーは、Facebook、Twitter、その他のソーシャル web サイトなどのソーシャルチャネルを使用して、リアルタイムで相互に対話しています。 開発者は、ユーザーが自分のソーシャル id を使用してサインインできるようにすることで、web サイトに豊富なエクスペリエンスを提供できます。 最新のメンバーシップシステムでは、Facebook、Twitter などの認証プロバイダーに対するリダイレクトベースのログインを有効にする必要があります。

Web 開発の進化に応じて、web 開発のパターンを作成しました。 アプリケーションコードの単体テストは、アプリケーション開発者にとって重要な問題になりました。 2008では、開発者が単体テスト可能な ASP.NET アプリケーションを構築するのに役立つ、モデルビューコントローラー (MVC) パターンに基づく新しいフレームワークが ASP.NET に追加されました。 また、アプリケーションロジックの単体テストを行う開発者は、メンバーシップシステムを使用してそれを実行できるようにしたいと考えています。

これらの変更を web アプリケーション開発で検討すると、ASP.NET Identity は次の目的で開発されました。

- **1つの ASP.NET Identity システム**

    - ASP.NET Identity は、ASP.NET MVC、Web フォーム、Web ページ、Web API、SignalR など、すべての ASP.NET フレームワークで使用できます。
    - ASP.NET Identity は、web、電話、ストア、またはハイブリッドアプリケーションを構築するときに使用できます。
- **ユーザーに関するプロファイルデータを簡単にプラグインする**

    - ユーザーおよびプロファイル情報のスキーマを制御できます。 たとえば、ユーザーがアプリケーションにアカウントを登録するときにユーザーが入力した生年月日を格納できるように、システムを簡単に有効にすることができます。

- **永続化コントロール**

    - 既定では、ASP.NET Identity システムによって、すべてのユーザー情報がデータベースに格納されます。 ASP.NET Identity は Entity Framework Code First を使用して、すべての永続化メカニズムを実装します。
    - データベーススキーマを制御するため、テーブル名の変更や主キーのデータ型の変更などの一般的なタスクは簡単に行うことができます。
    - `System.NotImplementedExceptions` 例外をスローすることなく、SharePoint、Azure Storage Table Service、NoSQL databases などのさまざまなストレージメカニズムを簡単にプラグインできます。
- **単体テスト**

    - ASP.NET Identity により、web アプリケーションの単体テストが容易になります。 ASP.NET Identity を使用するアプリケーションの一部に対して単体テストを記述できます。
- **ロールプロバイダー**

    - ロールによってアプリケーションの一部へのアクセスを制限できるロールプロバイダーがあります。 "Admin" などのロールを簡単に作成し、ユーザーをロールに追加することができます。
- **要求ベース**

    - ASP.NET Identity は、クレームベースの認証をサポートしています。この場合、ユーザーの id はクレームのセットとして表されます。 要求を使用すると、開発者はロールで許可されているユーザーの id を記述する際に、はるかに表現力を高めることができます。 ロールのメンバーシップはブール値 (メンバーまたは非メンバー) であるのに対し、クレームには、ユーザーの id とメンバーシップに関する豊富な情報を含めることができます。
- **ソーシャルログインプロバイダー**

    - Microsoft アカウント、Facebook、Twitter、Google などのソーシャルログをアプリケーションに簡単に追加し、ユーザー固有のデータをアプリケーションに格納することができます。

- **OWIN の統合**

    - ASP.NET 認証は、任意の OWIN ベースのホストで使用できる OWIN ミドルウェアに基づいています。 ASP.NET Identity は、System.web に依存していません。 これは完全に準拠した OWIN フレームワークであり、OWIN でホストされるアプリケーションで使用できます。
    - ASP.NET Identity は、web サイトのユーザーのログイン/ログアウトに OWIN 認証を使用します。 つまり、FormsAuthentication を使用して cookie を生成する代わりに、アプリケーションで OWIN CookieAuthentication を使用します。
- **NuGet パッケージ**

    - ASP.NET Identity は、Visual Studio 2017 に付属する ASP.NET MVC、Web フォーム、Web API テンプレートにインストールされている NuGet パッケージとして再配布されます。 この NuGet パッケージは、NuGet ギャラリーからダウンロードできます。
    - NuGet パッケージとして ASP.NET Identity をリリースすることにより、ASP.NET チームは新しい機能やバグ修正を簡単に反復処理し、アジャイルな方法で開発者に配信できます。

## <a name="get-started-with-aspnet-identity"></a>ASP.NET Identity を使ってみる

ASP.NET Identity は、ASP.NET MVC、Web フォーム、Web API、および SPA 用の Visual Studio 2017 プロジェクトテンプレートで使用されます。 このチュートリアルでは、プロジェクトテンプレートで ASP.NET Identity を使用して、ユーザーの登録、サインイン、サインアウトを行う機能を追加する方法を説明します。

ASP.NET Identity は、次の手順を使用して実装されます。 この記事の目的は、ASP.NET Identity の概要を説明することです。詳細については、「ステップバイステップ」または「詳細」を参照してください。 新しい API を使用してユーザー、ロール、およびプロファイル情報を追加するなど、ASP.NET Identity を使用してアプリを作成する手順の詳細については、この記事の最後にある「次のステップ」を参照してください。

1. 個々のアカウントを使用して ASP.NET MVC アプリケーションを作成します。 ASP.NET Identity は、ASP.NET MVC、Web フォーム、Web API、SignalR などで使用できます。この記事では、ASP.NET MVC アプリケーションから始めます。  
  
    ![](introduction-to-aspnet-identity/_static/image1.png)
2. 作成されたプロジェクトには、ASP.NET Identity 用の次の3つのパッケージが含まれています。

    - [`Microsoft.AspNet.Identity.EntityFramework`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)  
   このパッケージには ASP.NET Identity の Entity Framework 実装があり、ASP.NET Identity のデータとスキーマは SQL Server に保存されます。
    - [`Microsoft.AspNet.Identity.Core`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Core/)  
   このパッケージには ASP.NET Identity のコアインターフェイスがあります。 このパッケージは、Azure Table Storage、NoSQL データベースなどのさまざまな永続ストアを対象とする ASP.NET Identity の実装を記述するために使用できます。
    - [`Microsoft.AspNet.Identity.OWIN`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Owin/)  
   このパッケージには、OWIN 認証を ASP.NET アプリケーションの ASP.NET Identity にプラグインするために使用される機能が含まれています。 これは、サインイン機能をアプリケーションに追加し、OWIN Cookie 認証ミドルウェアを呼び出して cookie を生成するときに使用されます。
3. ユーザーを作成しています。  
   アプリケーションを起動し、 **[登録]** リンクをクリックしてユーザーを作成します。 次の図は、ユーザー名とパスワードを収集する登録ページを示しています。  
  
    ![](introduction-to-aspnet-identity/_static/image2.png)  
  
   ユーザーが **[登録]** ボタンを選択すると、アカウントコントローラーの `Register` アクションで、次に示すように ASP.NET Identity API を呼び出すことによってユーザーが作成されます。

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample1.cs?highlight=8-9)]
4. サインインします。  
   ユーザーが正常に作成された場合は、`SignInAsync` メソッドによってサインインされます。  

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample6.cs?highlight=12)]

   `SignInManager.SignInAsync` メソッドは、 [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)を生成します。 ASP.NET Identity と OWIN Cookie 認証はクレームベースのシステムであるため、フレームワークでは、ユーザーの ClaimsIdentity を生成するようにアプリに要求します。 ClaimsIdentity には、ユーザーが属するロールなど、ユーザーのすべての要求に関する情報が含まれています。   
 
5. ログオフします。  
   [ログオフ **] リンクを**選択して、アカウントコントローラーでログオフアクションを呼び出します。 

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample5.cs?highlight=6)]

   上の強調表示されているコードは、OWIN `AuthenticationManager.SignOut` メソッドを示しています。 これは、Web フォームの[FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)モジュールで使用される[サインアウト](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)メソッドに似ています。

## <a name="components-of-aspnet-identity"></a>ASP.NET Identity のコンポーネント

次の図は、ASP.NET Identity システムのコンポーネントを示しています ([こ](introduction-to-aspnet-identity/_static/image3.png)のコンポーネントを選択するか、図を拡大して拡大します)。 緑のパッケージは、ASP.NET Identity システムを構成します。 他のすべてのパッケージは、ASP.NET アプリケーションで ASP.NET Identity システムを使用するために必要な依存関係です。

[![](introduction-to-aspnet-identity/_static/image5.png)](introduction-to-aspnet-identity/_static/image4.png)

前に説明しなかった NuGet パッケージの簡単な説明を次に示します。

- [Microsoft.Owin.Security.Cookies](http://www.nuget.org/packages/Microsoft.Owin.Security.Cookies/)  
 アプリケーションが、ASP と同様に cookie ベースの認証を使用できるようにするミドルウェア。NET のフォーム認証。
- [EntityFramework](http://www.nuget.org/packages/EntityFramework/)  
 Entity Framework は、リレーショナルデータベースに対して Microsoft が推奨するデータアクセステクノロジです。

## <a name="migrating-from-membership-to-aspnet-identity"></a>メンバーシップから ASP.NET Identity への移行

ASP.NET メンバーシップを使用する既存のアプリや、単純なメンバーシップを新しい ASP.NET Identity システムに移行する方法についてのガイダンスをすぐに提供することをお勧めします。

## <a name="next-steps"></a>次の手順

- [Facebook と Google OAuth2 と OpenID サインオンを使用して ASP.NET MVC 5 アプリを作成する](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)  
 このチュートリアルでは、ASP.NET Identity API を使用して、ユーザーデータベースにプロファイル情報を追加し、Google と Facebook で認証する方法を説明します。
- [認証および SQL DB を使用する ASP.NET MVC アプリの作成と、Azure App Service へのデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)  
 このチュートリアルでは、Identity API を使用してユーザーとロールを追加する方法について説明します。
- [https://github.com/rustd/AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample)  
 基本的な役割とユーザーサポートを追加する方法と、役割とユーザー管理を行う方法を示すサンプルアプリケーション。

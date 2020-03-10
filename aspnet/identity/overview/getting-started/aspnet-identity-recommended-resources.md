---
uid: identity/overview/getting-started/aspnet-identity-recommended-resources
title: 推奨されるリソースの ASP.NET Identity-ASP.NET 4.x
author: Rick-Anderson
description: このトピックでは、ASP.NET Identity の使用方法に関するドキュメントリソースへのリンクを示します。 優れたブログ投稿、stackoverflow スレッド、またはその他のリンク...
ms.author: riande
ms.date: 04/09/2015
ms.assetid: 0f78aec2-f509-46fa-b20f-d5208425d8ec
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-recommended-resources
msc.type: authoredcontent
ms.openlocfilehash: 4b2a6689839f66121f4a32ee5934f6cda50ae812
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499792"
---
# <a name="aspnet-identity-recommended-resources"></a>ASP.NET Identity 推奨リソース

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このトピックでは、ASP.NET Identity の使用方法に関するドキュメントリソースへのリンクを示します。
>
> 優れたブログ投稿、 [stackoverflow](http://stackoverflow.com)スレッド、または役に立つその他のリンクがわかっている場合は、リンクを含む[電子メールを送信](mailto:aspnetue@microsoft.com?subject=Identity recommended resources)するか、このページの下部にメッセージを残してください。

- [ASP.NET Identity の概要](#gettingstarted)
- [新しいおすすめの記事を読む必要があります](#feat)
- [中間 ASP.NET Identity](#adv)
- [ビデオ](#video)
- [質問、機能のリクエスト、バグの報告、夜間ビルド](#samp)
- [Id に関するブログ投稿](#blog)
- [ASP.NET Identity 用のカスタムストレージプロバイダー](#cust)
- [追加の Id リソース](#additional)
- [Q &amp; A (質問/回答)](#qand)

<a id="gettingstarted"></a>

## <a name="getting-started-with-aspnet-identity"></a>ASP.NET Identity の概要

- [Facebook、Twitter、LinkedIn、Google OAuth2 サインオンを使用した MVC 5 アプリ](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)このチュートリアルでは、Facebook と Google OAuth 2 認証を使用して ASP.NET MVC 5 アプリを作成する方法について説明します。 また、Id データベースにデータを追加する方法についても説明します。
- [メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET MVC アプリを Azure にデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)します。 このチュートリアルでは、Azure のデプロイ、ロールを使用してアプリをセキュリティで保護する方法、メンバーシップ API を使用してユーザーとロールを追加する方法、および追加のセキュリティ機能を追加します。
- [ASP.NET Identity 入門](introduction-to-aspnet-identity.md)
- [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (ログイン、電子メールの確認、およびパスワードのリセットでセキュリティで保護された ASP.NET MVC 5 web アプリを作成する)](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)
- [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication (SMS と電子メールの 2 要素認証を使用する ASP.NET MVC 5 アプリケーション)](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)

<a id="feat"></a>

## <a name="new-featured-must-read-articles"></a>新しいおすすめの記事を読む必要があります

- チュートリアル: [Benjamin Day](http://www.benday.com/about/)による[Microsoft アカウント認証を使用した ASP.NET MVC id](http://www.benday.com/2014/02/25/walkthrough-asp-net-mvc-identity-with-microsoft-account-authentication/)
- [ASP.NET Identity 2.0 では、Id モデルを拡張し、文字列ではなく整数キーを使用します。](http://typecastexception.com/post/2014/07/13/ASPNET-Identity-20-Extending-Identity-Models-and-Using-Integer-Keys-Instead-of-Strings.aspx)
- [ASP.NET Web API 2、Owin、Id を使用した AngularJS トークン認証](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
- [WSAT の代わりとしての Thinktecture](http://www.hanselman.com/blog/ThinktectureIdentityManagerAsAReplacementForTheASPNETWebSiteAdministrationTool.aspx)
- [ASP.NET Identity 2.0: ユーザーとロールのカスタマイズ](http://typecastexception.com/post/2014/06/22/ASPNET-Identity-20-Customizing-Users-and-Roles.aspx)

<a id="adv"></a>

## <a name="intermediate-aspnet-identity"></a>中間 ASP.NET Identity

- [ASP.NET Identity を使用したアカウントの確認とパスワードの回復](../features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET Identity で SMS と電子メールを利用して 2 要素認証を行う](../features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [既存 Web サイトを SQL メンバーシップから ASP.NET Identity に移行する](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [ASP.NET Identity を空または既存の Web フォーム プロジェクトに追加する](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md)
- [ASP.NET Identity を使用した MSDN マガジンの外部認証 (](https://msdn.microsoft.com/magazine/dn745860.aspx)恐竜 Esposito)
- MSDN マガジン[は、](https://msdn.microsoft.com/magazine/dn605872.aspx) Esposito による初めての ASP.NET Identity
- [ASP.NET Identity –ユーザーロックアウト](http://tech.trailmax.info/2014/06/asp-net-identity-user-lockout/)

<a id="samp"></a>

## <a name="where-to-ask-questions-request-features-report-a-bug-and-nightly-builds"></a>質問、機能のリクエスト、バグの報告、夜間ビルド

- StackOverflow の場合は、「 [aspnet-identity](http://stackoverflow.com/questions/tagged/asp.net-identity) 」というタグを使用します。
- ASP.NET フォーラムについては、[セキュリティフォーラム](https://forums.asp.net/25.aspx)に投稿し、 **ASP.NET Identity**をタイトルに追加してください。
- [GitHub での ASP.NET Identity](https://github.com/aspnet/AspNetIdentity)夜間のビルドを取得し、機能を要求し、バグを開きます。

<a id="blog"></a>

## <a name="blog-posts-on-identity"></a>Id に関するブログ投稿

- [ASP.NET Identity にはどのようなものがありますか。](http://stackoverflow.com/questions/19487322/what-is-asp-net-identitys-iusersecuritystampstoretuser-interface/19505060#19505060)
- [John の添付 en](https://twitter.com/xivSolutions)

    - [ASP.NET Identity 2.0 では、Id モデルを拡張し、文字列ではなく整数キーを使用します。](http://typecastexception.com/post/2014/07/13/ASPNET-Identity-20-Extending-Identity-Models-and-Using-Integer-Keys-Instead-of-Strings.aspx)
    - [ASP.NET Identity 2.0: ユーザーとロールのカスタマイズ](http://typecastexception.com/post/2014/06/22/ASPNET-Identity-20-Customizing-Users-and-Roles.aspx)
    - [ASP.NET MVC and Id 2.0: 基本を理解する](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)
    - [アカウントの検証と2要素認証の設定](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)
    - [ASP.NET MVC 5 および Visual Studio 2013 での Id アカウントの Db 接続とコード優先移行の構成](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)
- [Taiseer Joudeh](http://bitoftech.net/taiseer-joudeh-blog/)

    - [ASP.NET Web API 2、Owin ミドルウェア、および ASP.NET Identity を使用したトークンベースの認証](http://bitoftech.net/2014/06/01/token-based-authentication-asp-net-web-api-2-owin-asp-net-identity/)
    - [ASP.NET Web API 2、Owin、Id を使用した AngularJS トークン認証](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
    - [ASP .NET Web API 2 と Owin –パート3を使用して、AngularJS アプリで OAuth 更新トークンを有効にします。](http://bitoftech.net/2014/07/16/enable-oauth-refresh-tokens-angularjs-app-using-asp-net-web-api-2-owin/)
- [Anders Abel](https://twitter.com/anders_abel)

    - [Owin 外部認証パイプラインについて](http://coding.abel.nu/2014/06/understanding-the-owin-external-authentication-pipeline/)
    - [ASP.NET Identity と Owin の概要](http://coding.abel.nu/2014/06/asp-net-identity-and-owin-overview/)

  (K) コードへのコードの[Scott Allen](https://twitter.com/OdeToCode)

    - [ASP.NET Core id](http://odetocode.com/blogs/scott/archive/2013/11/25/asp-net-core-identity.aspx)このブログでは、IUser、IUserStore、I\*Store のインターフェイスなど、コアの抽象化について確認します。
    - [Entity Framework を使用した ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/03/asp-net-identity-with-the-entity-framework.aspx)MVC 5 の個々のユーザーアカウント、Web API と SPA アプリ、接続文字列、およびコンテキストの管理
    - [ASP.NET Identity のカスタマイズオプション](http://odetocode.com/blogs/scott/archive/2014/01/09/customization-options-with-asp-net-identity.aspx)
    - [ASP.NET Identity の実装](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- [Benjamin Day](http://www.benday.com/about/)[チュートリアル: ASP.NET MVC Identity With Microsoft アカウント認証](http://www.benday.com/2014/02/25/walkthrough-asp-net-mvc-identity-with-microsoft-account-authentication/)
- [Brock Allen](https://twitter.com/BrockLAllen)

    - [OWIN/Katana 認証ミドルウェアを使用した外部ログインプロバイダー (ソーシャルログイン) の入門](http://brockallen.com/2014/01/09/a-primer-on-external-login-providers-social-logins-with-owinkatana-authentication-middleware/)
    - "登録の[再起動](http://brockallen.com/2014/02/11/introducing-identityreboot/)" の導入: 不満のある主要な機能を実装する ASP.NET Identity の一連の拡張機能です。
- [Pranav Rastogi](https://twitter.com/rustd)

    - [ソーシャルプロバイダーから詳細情報を取得する](https://blogs.msdn.com/b/webdev/archive/2013/10/16/get-more-information-from-social-providers-used-in-the-vs-2013-project-templates.aspx)
- [@beabigrockstar](https://twitter.com/beabigrockstar) (Jerrie Pelser)

    - [2要素認証](http://www.beabigrockstar.com/blog/2-factor-authentication-with-asp-net-identity-2-0-beta-1/)
    - [ASP.NET Identity で Google Authenticator を使用する](http://www.beabigrockstar.com/blog/using-google-authenticator-asp-net-identity/)
    - [ASP.NET MVC 5 認証ガイド](http://www.beabigrockstar.com/)
- [VS 2013 プロジェクトテンプレートで使用されるソーシャルプロバイダーから詳細情報を取得する](https://blogs.msdn.com/b/webdev/archive/2013/10/16/get-more-information-from-social-providers-used-in-the-vs-2013-project-templates.aspx)
- [ASP.NET Identity を使用した単純な ToDo アプリケーションの構築とユーザーの ToDoes の関連付け](https://blogs.msdn.com/b/webdev/archive/2013/10/20/building-a-simple-todo-application-with-asp-net-identity-and-associating-users-with-todoes.aspx)
- [ASP.NET Identity での Google OpenId の統合に関する問題](http://blog.technovert.com/2014/01/google-openid-integration-issues-asp-net-identity/)"HTTP エラー 404.15-見つかりませんでした" というエラーが発生した場合は、要求フィルターモジュールが、クエリ文字列が長すぎる要求を拒否するように構成されています。
- [WSAT の代わりとしての Thinktecture](http://www.hanselman.com/blog/ThinktectureIdentityManagerAsAReplacementForTheASPNETWebSiteAdministrationTool.aspx)
- [ASP.NET Web API 2、Owin、Id を使用した AngularJS トークン認証](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
- [Entity Framework なしの単純な Asp.net Identity Core](https://code.msdn.microsoft.com/Simple-Aspnet-Identiy-Core-7475a961)
- [Sheo Narayan](http://www.dotnetfunda.com/profile/sheonarayan.aspx)による[MVC の ASP.NET Identity でのロールの操作](http://www.dotnetfunda.com/articles/show/2898/working-with-roles-in-aspnet-identity-for-mvc)
- [ASP.NET のメンバーシップによるのメンバーシップからの ASP.NET Identity への移動](http://webdojo.sharepoint.com/ajmatthews/_layouts/15/start.aspx#/Lists/Posts/Post.aspx?ID=2)

<a id="video"></a>

## <a name="videos"></a>ビデオ

- Channel 9 [ASP.NET アプリケーションとサービスのセキュリティ保護: Ido Flatow による最新のアプリケーションのセキュリティの facの](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B421#fbid=PhVT9E1WRtr?hashlink=fbid)強化
- 「Channel 9 [ASP.NET Identity 入門](https://channel9.msdn.com/Events/dotnetConf/2014/ASP-NET-Identity-Security)者の Pranav Rastogi
- Channel 9 [ASP.NET による ASP.NET Identity を使用した認証](https://channel9.msdn.com/Shows/Web+Camps+TV/Special-Movember-Episode-ASPNET-Authentication-Provider)の Fowler
- Channel 9[新しい Web Apps の構築:](https://channel9.msdn.com/Series/Building-Modern-Web-Apps/03) Jeff の ASP.NET Identity
- Channel 9 Alex で[web サイト ASP.NET Identity をセキュリティで保護する](https://channel9.msdn.com/Events/TechDays/Techdays-2014-the-Netherlands/Securing-your-website-with-ASP-NET-Identity)
- [既存の DB モデルでの ASP.NET Identity の使用 (アレクサンドロス・](https://www.youtube.com/watch?v=elfqejow5hM) midt)
- Telerik の Ivaylo Kenov によって[1 つの id を ASP.NET](https://www.youtube.com/watch?v=w8GD-QIusKk)
- [チェコ ASP.NET Identity](https://www.youtube.com/watch?v=tVbZp5brcpY)この講義では、基本認証をデプロイする方法、Twitter や Facebook などの外部 id プロバイダーのサポートを追加する方法、ワンタイムパスワード (OTP) の使用方法について説明します。 [ASP.NET Identity je nástupce Membership a Role provider&#367; v ASP.NET, tedy knihovna pro zajišt&#283;ní autentizace uživatel&#367;. V této p&#345;ednášce si ukážeme、jak nasad]

<a id="cust"></a>

## <a name="custom-storage-providers-for-aspnet-identity"></a>ASP.NET Identity 用のカスタムストレージプロバイダー

独自のプロバイダーを作成する場合は、 [ASP.NET Identity 用のカスタムストレージプロバイダーの概要](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)と[ASP.NET Identity の実装](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)に関するトピックを読み、次に示すいずれかの OSS プロジェクトのソースを確認してください。

- チュートリアル: Tom FitzMacken による[ASP.NET Identity 用のカスタム記憶域プロバイダーの概要](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- ブログ: [ASP.NET Identity の実装](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- チュートリアル:[基本的な id アカウントを設定し、外部 DB でポイント](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)する。 [@xivSolutions](https://twitter.com/xivSolutions)。
- チュートリアル[: カスタム MySQL ASP.NET Identity ストレージプロバイダーの実装](../extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- [Azure Table Storage](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/) James randall)。
- Azure Table Storage: [@stuartleeks](https://twitter.com/stuartleeks)による[tablestorage](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage) 。
- [CouchDB/Cloudant by Daniel Wertheim。](https://github.com/danielwertheim/mycouch.aspnet.identity)
- [エラスティック検索:](https://github.com/bmbsqd/elastic-identity) Bombsquad AB によるエラスティック id。
- Jonathan Sheely Jonathan Sheely による[MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) 。
- [N](https://github.com/milesibastos/NHibernate.AspNet.Identity) Io ミル Esi Bastos によって Id が識別されます。
- [@tourismgeek](https://twitter.com/tourismgeek)による[RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) 。
- [RavenDB](https://github.com/ILMServices/RavenDB.AspNet.Identity) [ilmservices](http://www.ilmservice.com/)によって識別されます。
- Redis: [redis. Identity](https://github.com/aminjam/Redis.AspNet.Identity)
- "データベースの最初の" ユーザーストアの EF コードを生成する T4 テンプレート: [AspNet. Identity. EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)

<a id="additional"></a>

## <a name="additional-aspnet-identity-resources"></a>その他の ASP.NET Identity リソース

- OWIN by Jerrie Pelser for Yahoo and LinkedIn の手順に関する[yahoo および Linkedin OAuth セキュリティプロバイダーの概要](http://blog.beabigrockstar.com/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/)を説明します。

<a id="qand"></a>

## <a name="qampa-questionanswer"></a>Q&amp;A (質問/回答)

- Q: ロックアウトされたユーザーを有効にした場合 (そのコンピューター/ブラウザーで2FA を通過する必要はありません)、ロックアウトされません。なぜこれを回避するのですか。 [ここ](http://stackoverflow.com/questions/24312247/locked-out-users-can-login-if-they-have-auth-cookie)に回答してください。
- **Q**: ユーザーの名前などのカスタム要求を ASP.NET Identity の cookie に格納して、要求ごとに不要なデータベースクエリを回避するにはどうすればよいですか。 [ここ](http://stackoverflow.com/questions/23622047/identity-cookie-loses-custom-claim-information-after-a-period-of-time)に回答してください。
- **Q: AspNetUser パスワードハッシュを更新**しています。2つのプロジェクトがあります。 そのうちの1つは ASP.NET 認証を使用しており、もう1つは管理側である Windows 認証を使用します。 管理プロジェクトが、他のユーザーを管理できるようにする必要があります。 パスワード以外のすべてを変更することができます。 [ここに回答](http://stackoverflow.com/questions/23880666/updating-aspnetuser-password-hash)してください。
- **Q**: 他のユーザーの管理者としてパスワードをリセットするにはどうすればよいですか。 [ここ](http://stackoverflow.com/questions/23783249/identity-2-0-reset-password-by-admin/24211766#24211766)に回答してください。
- **Q**: ASP.NET MVC ユーザー名フィールドの表示名を変更することはできますか。 [ここ](http://stackoverflow.com/questions/23256650/can-i-change-the-displayed-name-of-the-username-field-in-asp-net-mvc-identityuse)に回答してください。
- **Q**: 他のユーザーを特定のロールに追加するためのアクセス許可をユーザーに付与するにはどうすればよいですか。 [ここ](http://stackoverflow.com/questions/23695373/allow-users-to-grant-permissions-to-other-users-for-their-account-in-asp-net-ide)に回答してください。
- **Q**: AspNetUsers テーブルと AspNetUserClaims テーブルにプロファイル情報を格納しています。 [ここ](http://stackoverflow.com/questions/23215727/is-there-any-benefit-to-storing-user-information-in-aspnetuserclaims-with-asp-ne)に回答してください。
- **Q**: 外部認証プロバイダーを使用する場合は注意してください。 [ここ](http://stackoverflow.com/questions/23180896/how-to-remember-the-login-in-mvc5-when-an-external-provider-is-used)に回答してください。
- **Q**: すべての要求に ApplicationDBContext が必要なのはなぜですか。これで、オーバーヘッドが過剰になります。 答えはありませんが、オーバーヘッドは低くなります。
- Q: ログインしているユーザーの一覧を取得操作方法には、 [ここ](http://stackoverflow.com/questions/22995653/getting-a-list-of-logged-in-users-in-asp-net-identity/)に回答してください。
- Q: ユーザーがどのような場合に、どのような方法でログインしたかを検出するにはどうすればよいですか。 [ここ](http://stackoverflow.com/questions/22956486/how-can-i-detect-when-a-user-logs-in-with-microsoft-aspnet-identity/22970698#22970698)に回答してください。
- Q: ローカライズされたエラーメッセージを Id として取得操作方法には [ここ](http://stackoverflow.com/questions/22835981/asp-net-identity-localization-publickeytoken/22845864#22845864)に回答してください。
- Q: CookieMiddleware を構成して30分ごとに新しい要求を取得操作方法 [ここ](http://stackoverflow.com/questions/22682663/how-to-hold-the-cookies-claims-updated-with-mcv5-owin/22796932#22796932)に回答してください。
- Q: サインイン後にユーザーの要求を変更するにはどうすればよいですか。 [ここ](http://stackoverflow.com/questions/22768836/can-i-modify-claims-in-asp-net-identity-with-owin-after-calling-signin/22769963#22769963)に回答してください。
- Q: 操作方法セキュリティトークンを無効にしますか? [ここ](http://stackoverflow.com/questions/22755700/revoke-token-generated-by-usertokenprovider-in-asp-net-identity-2-0/22767286#22767286)に回答してください。
- Q: cookie ミドルウェアに要求を格納するにはどうすればよいですか。 [ここ](http://stackoverflow.com/questions/22320632/storing-retrieving-user-data-without-database-when-using-owin-cookie-authenticat/22541856#22541856)に回答してください。
- Q: MVC アプリの各アクションメソッドに対して PIN またはセキュリティチェックを行う必要がありますが、ユーザーの成功を格納したいので、そのアクションメソッドへの要求ごとに PIN を入力する必要はありません。 [ここ](http://stackoverflow.com/questions/22479958/security-check-an-user-to-a-access-controller-action/22486075#22486075)に回答してください。
- Q: 返された電子メールアドレスをソーシャルプロバイダーから DB に保存しますか? これを行うにはどうすればよいですか。 回答[:](http://stackoverflow.com/questions/22888397/save-claims-to-db-on-login/22970969#22970969)
- Q: ユーザーが "覚える" cookie を使用するかどうかによって、ユーザーがログインしたことを検出するにはどうすればよいですか。 [ここ](http://stackoverflow.com/questions/22956486/how-can-i-detect-when-a-user-logs-in-with-microsoft-aspnet-identity/22970698#22970698)に回答してください。
- Q: サインインを呼び出した後、OWIN を使用して ASP.NET Identity の要求を変更することはできますか。 回答: サインインの呼び出しは、ユーザーの要求を変更する場合に実行することを意図したものです。 これにより、基本的に ClaimsIdentity がクッキーにシリアル化されます。これは、新しい要求が後続の要求に表示されることを示しています。

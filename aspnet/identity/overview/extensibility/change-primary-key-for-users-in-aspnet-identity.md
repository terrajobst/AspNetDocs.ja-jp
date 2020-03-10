---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: ASP.NET Identity のユーザーのプライマリキーを変更する-ASP.NET 4.x
author: Rick-Anderson
description: Visual Studio 2013 では、既定の web アプリケーションは、ユーザーアカウントのキーに文字列値を使用します。 ASP.NET Identity を使用すると、...
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472264"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a>ASP.NET Identity でユーザーの主キーを変更する

[Tom FitzMacken](https://github.com/tfitzmac)

> Visual Studio 2013 では、既定の web アプリケーションは、ユーザーアカウントのキーに文字列値を使用します。 ASP.NET Identity を使用すると、データ要件に合わせてキーの種類を変更できます。 たとえば、キーの型を文字列から整数に変更できます。
> 
> このトピックでは、既定の web アプリケーションを使用してを開始し、ユーザーアカウントキーを整数に変更する方法について説明します。 同じ変更を使用して、プロジェクト内の任意の種類のキーを実装できます。 既定の web アプリケーションでこれらの変更を行う方法を示していますが、カスタマイズされたアプリケーションに同様の変更を適用することもできます。 MVC または Web フォームを操作するときに必要な変更を示します。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - Update 2 (またはそれ以降) の Visual Studio 2013
> - ASP.NET Identity 2.1 以降

このチュートリアルの手順を実行するには、Visual Studio 2013 Update 2 (以降)、および ASP.NET Web アプリケーションテンプレートから作成された web アプリケーションが必要です。 Update 3 でテンプレートが変更されました。 このトピックでは、Update 2 および Update 3 でテンプレートを変更する方法について説明します。

このトピックには、次のセクションが含まれます。

- [Identity user クラスのキーの種類を変更する](#userclass)
- [キーの種類を使用するカスタマイズされた Id クラスを追加する](#customclass)
- [キーの種類を使用するようにコンテキストクラスとユーザーマネージャーを変更する](#context)
- [キーの種類を使用するようにスタートアップ構成を変更する](#startup)
- [Update 2 の MVC では、キーの種類を渡すために AccountController を変更します。](#mvcupdate2)
- [Update 3 の MVC では、キーの種類を渡すように AccountController と ManageController を変更します。](#mvcupdate3)
- [Web フォーム Update 2 では、キーの種類を渡すようにアカウントページを変更します。](#webformsupdate2)
- [Update 3 で Web フォームを使用する場合は、キーの種類を渡すようにアカウントページを変更します。](#webformsupdate3)
- [アプリケーションの実行](#run)
- [その他のリソース](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a>Identity user クラスのキーの種類を変更する

ASP.NET Web アプリケーションテンプレートから作成したプロジェクトで、ApplicationUser クラスがユーザーアカウントのキーに整数を使用するように指定します。 IdentityModels.cs の ApplicationUser クラスを、TKey ジェネリックパラメーターの**int**型を持つユーザーから継承するように変更します。 まだ実装していない3つのカスタマイズされたクラスの名前を渡すこともできます。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

キーの種類を変更しましたが、既定では、アプリケーションの残りの部分では、キーが文字列であると想定しています。 文字列を想定するコードでは、キーの型を明示的に指定する必要があります。

次の強調表示されているコードに示すように、 **Applicationuser**クラスで、 **Generateuserの async**メソッドを変更して int を含めます。 この変更は、Update 3 テンプレートを使用した Web フォームプロジェクトには必要ありません。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a>キーの種類を使用するカスタマイズされた Id クラスを追加する

その他の Id クラス (ユーザー Id、ユーザー Id クレーム、ユーザー名ログイン、Id ロール、UserStore、RoleStore など) は、文字列キーを使用するように設定されたままです。 キーの整数を指定する、これらのクラスの新しいバージョンを作成します。 これらのクラスでは、多くの実装コードを指定する必要はありません。主に、キーとして int を設定するだけです。

IdentityModels.cs ファイルに次のクラスを追加します。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a>キーの種類を使用するようにコンテキストクラスとユーザーマネージャーを変更する

IdentityModels.cs で、新しいカスタマイズされたクラスを使用するように**Applicationdbcontext**クラスの定義を変更し、強調表示されているコードに示されているように、キーの**int**を使用します。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

ThrowIfV1Schema パラメーターがコンストラクターで有効ではなくなりました。 ThrowIfV1Schema 値が渡されないようにコンストラクターを変更します。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

IdentityConfig.cs を開き、 **Applicationusermanger**クラスを変更して、データを保持するための新しいユーザーストアクラスとキーの**int**を使用するように変更します。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

Update 3 テンプレートでは、ApplicationSignInManager クラスを変更する必要があります。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a>キーの種類を使用するようにスタートアップ構成を変更する

Startup.Auth.cs で、下の強調表示されているように OnValidateIdentity コードを置き換えます。 GetUserIdCallback 定義により、文字列値が整数に解析されることに注意してください。

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

プロジェクトが**Getuserid**メソッドのジェネリック実装を認識しない場合は、ASP.NET Identity NuGet パッケージをバージョン2.1 に更新する必要がある場合があります。

ASP.NET Identity によって使用されるインフラストラクチャクラスに多数の変更が加えられました。 プロジェクトをコンパイルしようとすると、多数のエラーが発生します。 幸い、残りのエラーはすべて類似しています。 Id クラスはキーに整数を必要としますが、コントローラー (または Web フォーム) は文字列値を渡しています。 どちらの場合も、 **Getuserid&lt;int&gt;** を呼び出すことにより、文字列をと整数に変換する必要があります。 コンパイルからエラー一覧を処理するか、次の変更を行うことができます。

残りの変更は、作成するプロジェクトの種類と、Visual Studio にインストールした更新プログラムによって異なります。 関連するセクションに直接アクセスするには、次のリンクを使用します。

- [Update 2 の MVC では、キーの種類を渡すために AccountController を変更します。](#mvcupdate2)
- [Update 3 の MVC では、キーの種類を渡すように AccountController と ManageController を変更します。](#mvcupdate3)
- [Web フォーム Update 2 では、キーの種類を渡すようにアカウントページを変更します。](#webformsupdate2)
- [Update 3 で Web フォームを使用する場合は、キーの種類を渡すようにアカウントページを変更します。](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a>Update 2 の MVC では、キーの種類を渡すために AccountController を変更します。

AccountController.cs ファイルを開きます。 次のメソッドを変更する必要があります。

**ConfirmEmail**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

**関連付け**解除メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

**Manage (ManageUserViewModel)** メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

**Linklogincallback**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

**Removeaccountlist**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

**Haspassword**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

これで、[アプリケーションを実行](#run)し、新しいユーザーを登録できます。

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a>Update 3 の MVC では、キーの種類を渡すように AccountController と ManageController を変更します。

AccountController.cs ファイルを開きます。 次のメソッドを変更する必要があります。

**ConfirmEmail**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

**Sendcode**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

ManageController.cs ファイルを開きます。 次のメソッドを変更する必要があります。

**Index**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

**Removelogin**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

**AddPhoneNumber**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

**EnableTwoFactorAuthentication**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

**DisableTwoFactorAuthentication**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

**VerifyPhoneNumber**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

**RemovePhoneNumber**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

**ChangePassword**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

**SetPassword**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

**Managelogins**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

**Linklogincallback**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

**Haspassword**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

**HasPhoneNumber**メソッド

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

これで、[アプリケーションを実行](#run)し、新しいユーザーを登録できます。

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a>Web フォーム Update 2 では、キーの種類を渡すようにアカウントページを変更します。

Web フォーム Update 2 では、次のページを変更する必要があります。

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

これで、[アプリケーションを実行](#run)し、新しいユーザーを登録できます。

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a>Update 3 で Web フォームを使用する場合は、キーの種類を渡すようにアカウントページを変更します。

Update 3 で Web フォームを使用する場合は、次のページを変更する必要があります。

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

**VerifyPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

**AddPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

**ManagePassword.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

**ManageLogins.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

**TwoFactorAuthenticationSignIn.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a>アプリケーションを実行する

既定の Web アプリケーションテンプレートに必要なすべての変更が完了しました。 アプリケーションを実行し、新しいユーザーを登録します。 ユーザーを登録すると、AspNetUsers テーブルには整数の Id 列があることがわかります。

![新しい主キー](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

主キーが異なる ASP.NET Identity テーブルを既に作成している場合は、いくつかの追加の変更を行う必要があります。 可能であれば、既存のデータベースを削除するだけです。 Web アプリケーションを実行して新しいユーザーを追加すると、適切なデザインでデータベースが再作成されます。 削除できない場合は、code first の移行を実行してテーブルを変更します。 ただし、新しい整数の主キーは、データベースの SQL ID プロパティとしては設定されません。 Id 列は、手動で id として設定する必要があります。

<a id="other"></a>
## <a name="other-resources"></a>その他のリソース

- [ASP.NET Identity のカスタム ストレージ プロバイダーの概要](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [既存 Web サイトを SQL メンバーシップから ASP.NET Identity に移行する](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [メンバーシップとユーザープロファイルのユニバーサルプロバイダーデータを ASP.NET Identity に移行する](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- 主キーが変更された[サンプルアプリケーション](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK)

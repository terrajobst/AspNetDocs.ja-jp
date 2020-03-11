---
uid: identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
title: ASP.NET Identity 用カスタム記憶域プロバイダーの概要-ASP.NET 4.x
author: Rick-Anderson
description: ASP.NET Identity は拡張可能なシステムです。これを使用すると、独自の記憶域プロバイダーを作成し、アプリケーションにプラグインできます。
ms.author: riande
ms.date: 10/13/2014
ms.assetid: 681a9204-462e-4260-9a0b-19f0644d6ad7
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 21baedf6285b411f89627df9ca25d47a2a42e387
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472222"
---
# <a name="overview-of-custom-storage-providers-for-aspnet-identity"></a>ASP.NET Identity のカスタム ストレージ プロバイダーの概要

によって[Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET Identity は拡張可能なシステムで、アプリケーションを再実行することなく、独自の記憶域プロバイダーを作成してアプリケーションに組み込むことができます。 このトピックでは、ASP.NET Identity 用にカスタマイズされた記憶域プロバイダーを作成する方法について説明します。 独自の記憶域プロバイダーを作成するための重要な概念について説明しますが、カスタム記憶域プロバイダーを実装する手順については説明しません。
> 
> カスタムストレージプロバイダーを実装する例については、「[カスタム MySQL ASP.NET Identity ストレージプロバイダーの実装](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)」を参照してください。
> 
> このトピックは ASP.NET Identity 2.0 用に更新されました。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - Visual Studio 2013 Update 2
> - ASP.NET Identity 2

## <a name="introduction"></a>はじめに

既定では、ASP.NET Identity システムはユーザー情報を SQL Server データベースに格納し、Entity Framework Code First を使用してデータベースを作成します。 多くのアプリケーションでは、この方法が適しています。 ただし、Azure Table Storage などの別の種類の永続化メカニズムを使用するか、既定の実装とは異なる構造を持つデータベーステーブルが既に存在する可能性があります。 どちらの場合でも、ストレージ機構用にカスタマイズされたプロバイダーを作成し、そのプロバイダーをアプリケーションに組み込むことができます。

ASP.NET Identity は、多くの Visual Studio 2013 テンプレートに既定で含まれています。 ASP.NET Identity の更新プログラムを取得するには、 [Microsoft AspNet Identity EntityFramework NuGet パッケージ](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)を使用します。

このトピックには、次のセクションがあります。

- [アーキテクチャを理解する](#architecture)
- [格納されているデータを理解する](#data)
- [データアクセス層を作成する](#dal)
- [ユーザークラスをカスタマイズする](#user)
- [ユーザーストアをカスタマイズする](#userstore)
- [ロールクラスをカスタマイズする](#role)
- [ロールストアをカスタマイズする](#rolestore)
- [新しい記憶域プロバイダーを使用するようにアプリケーションを再構成する](#reconfigure)
- [カスタム記憶域プロバイダーのその他の実装](#other)

<a id="architecture"></a>
## <a name="understand-the-architecture"></a>アーキテクチャを理解する

ASP.NET Identity は、マネージャーとストアと呼ばれるクラスで構成されます。 マネージャーは、アプリケーション開発者が ASP.NET Identity システムでユーザーの作成などの操作を実行するために使用する、高レベルのクラスです。 ストアは、ユーザーやロールなどのエンティティがどのように永続化されるかを指定する下位レベルのクラスです。 ストアは永続化メカニズムと密接に結び付いていますが、管理者はストアから切り離されています。つまり、アプリケーション全体を中断することなく永続化メカニズムを置き換えることができます。

次の図は、web アプリケーションがマネージャーと対話する方法を示しています。また、データアクセス層との対話を格納します。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image1.png)

ASP.NET Identity 用にカスタマイズされた記憶域プロバイダーを作成するには、データソース、データアクセス層、およびこのデータアクセス層と対話するストアクラスを作成する必要があります。 同じマネージャー Api を使用してユーザーに対してデータ操作を実行できますが、データは別のストレージシステムに保存されるようになりました。

UserManager または RoleManager の新しいインスタンスを作成するときに、ユーザークラスの型を指定し、ストアクラスのインスタンスを引数として渡すため、マネージャークラスをカスタマイズする必要はありません。 この方法を使用すると、カスタマイズしたクラスを既存の構造に接続できます。 カスタマイズしたストアクラスで UserManager と RoleManager をインスタンス化する方法については、「[新しい記憶域プロバイダーを使用するようにアプリケーションを再構成](#reconfigure)する」を参照してください。

<a id="data"></a>
## <a name="understand-the-data-that-is-stored"></a>格納されているデータを理解する

カスタム記憶域プロバイダーを実装するには、ASP.NET Identity で使用されるデータの種類を理解し、アプリケーションに関連する機能を決定する必要があります。

| データ | 説明 |
| --- | --- |
| ユーザー | Web サイトの登録済みユーザー。 ユーザー Id とユーザー名が含まれます。 ユーザーが (Facebook などの外部サイトからの資格情報を使用せずに) サイトに固有の資格情報を使用してログインし、ユーザーの資格情報が変更されたかどうかを示すセキュリティスタンプを使用する場合は、ハッシュされたパスワードを含めることができます。 には、電子メールアドレス、電話番号、2要素認証が有効になっているかどうか、現在失敗したログインの数、アカウントがロックされているかどうかなども含まれます。 |
| ユーザー要求 | ユーザーの id を表す、ユーザーに関する一連のステートメント (または要求)。 では、ロールを使用した場合よりも多くのユーザー id を有効にすることができます。 |
| ユーザーログイン | ユーザーのログイン時に使用する外部認証プロバイダー (Facebook など) に関する情報。 |
| ロール | サイトの承認グループ。 ロール Id とロール名 ("Admin" や "Employee" など) が含まれます。 |

<a id="dal"></a>
## <a name="create-the-data-access-layer"></a>データアクセス層を作成する

このトピックでは、使用する永続化メカニズムについて理解していること、およびそのメカニズムのエンティティを作成する方法について理解していることを前提としています。 このトピックでは、リポジトリまたはデータアクセスクラスの作成方法の詳細については説明しません。代わりに、ASP.NET Identity を操作するときに行う必要がある設計上の決定について、いくつかの提案を提供します。

カスタマイズされたストアプロバイダーのリポジトリを設計する際には、さまざまな自由度があります。 アプリケーションで使用する機能に対してのみ、リポジトリを作成する必要があります。 たとえば、アプリケーションでロールを使用していない場合は、ロールまたはユーザーロールのストレージを作成する必要はありません。 テクノロジと既存のインフラストラクチャでは、ASP.NET Identity の既定の実装とは大きく異なる構造が必要になる場合があります。 データアクセス層では、リポジトリの構造を操作するためのロジックを提供します。

ASP.NET Identity 2.0 のデータリポジトリの MySQL 実装については、 [MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)を参照してください。

データアクセス層には、ASP.NET Identity からデータソースにデータを保存するためのロジックが用意されています。 カスタマイズした記憶域プロバイダーのデータアクセス層には、ユーザーとロールの情報を格納するための次のクラスが含まれている場合があります。

| &lt;クラス&gt; のすべてのオブジェクト | 説明 | 使用例 |
| --- | --- | --- |
| コンテキスト | 永続化メカニズムに接続してクエリを実行するための情報をカプセル化します。 このクラスは、データアクセス層の中心となります。 その他のデータクラスでは、操作を実行するために、このクラスのインスタンスが必要になります。 また、このクラスのインスタンスを使用して、ストアクラスを初期化します。 | [MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) |
| ユーザーストレージ | ユーザー情報 (ユーザー名やパスワードハッシュなど) を格納および取得します。 | [UserTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) |
| ロールストレージ | ロール名などのロール情報を格納および取得します。 | [RoleTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) |
| UserClaims ストレージ | ユーザー要求情報 (要求の種類や値など) を格納および取得します。 | [UserClaimsTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) |
| UserLogins ストレージ | ユーザーのログイン情報 (外部認証プロバイダーなど) を格納および取得します。 | [UserLoginsTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) |
| UserRole ストレージ | ユーザーが割り当てられているロールを格納して取得します。 | [UserRoleTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) |

ここでも、アプリケーションで使用するクラスを実装する必要があります。

データアクセスクラスでは、特定の永続化メカニズムに対してデータ操作を実行するコードを提供します。 たとえば、MySQL 実装では、UserTable クラスには、ユーザーデータベーステーブルに新しいレコードを挿入するメソッドが含まれています。 `_database` という名前の変数は、MySQLDatabase クラスのインスタンスです。

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample1.cs)]

データアクセスクラスを作成した後は、データアクセス層で特定のメソッドを呼び出すストアクラスを作成する必要があります。

<a id="user"></a>
## <a name="customize-the-user-class"></a>ユーザークラスをカスタマイズする

独自のストレージプロバイダーを実装する場合は、次のように、ユーザークラスを作成する必要があります。このクラスは、名前空間の[id](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)である[ユーザー](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser(v=vs.108).aspx)クラスに相当します。

次の図は、作成する必要があるユーザークラスと、このクラスで実装するインターフェイスを示しています。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image2.png)

[Iuser&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx)インターフェイスは、要求された操作の実行時に usermanager が呼び出しを試みるプロパティを定義します。 インターフェイスには、Id とユーザー名の2つのプロパティが含まれています。 [Iuser&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx)インターフェイスを使用すると、汎用**TKey**パラメーターを使用してユーザーのキーの型を指定できます。 Id プロパティの型は、TKey パラメーターの値と一致します。

Id フレームワークでは、キーに文字列値を使用する場合に、(ジェネリックパラメーターを指定せずに) [Iuser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.iuser(v=vs.108).aspx)インターフェイスも提供します。

ユーザークラスは IUser を実装し、web サイト上のユーザーの追加のプロパティまたはコンストラクターを含みます。 次の例は、キーに整数を使用するユーザークラスを示しています。 Id フィールドは、ジェネリックパラメーターの値と一致するように**int**に設定されます。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample2.cs)]

 完全な実装については、「[ユーザー (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs)」を参照してください。 

<a id="userstore"></a>
## <a name="customize-the-user-store"></a>ユーザーストアをカスタマイズする

また、ユーザーに対してすべてのデータ操作のメソッドを提供する UserStore クラスも作成します。 このクラスは、 [.Net framework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)名前空間の[Userstore&lt;tuser&gt;](https://msdn.microsoft.com/library/dn315446(v=vs.108).aspx)クラスに相当しています。 UserStore クラスでは、 [IUserStore&lt;TUser、TKey&gt;](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx) 、任意の省略可能なインターフェイスを実装します。 実装するオプションのインターフェイスは、アプリケーションで提供する機能に基づいて選択します。

次の図は、作成する必要がある UserStore クラスと関連するインターフェイスを示しています。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image3.png)

Visual Studio の既定のプロジェクトテンプレートには、オプションのインターフェイスの多くがユーザーストアに実装されていることを前提としたコードが含まれています。 カスタマイズされたユーザーストアで既定のテンプレートを使用している場合は、オプションのインターフェイスをユーザーストアに実装するか、実装していないインターフェイスでメソッドを呼び出さないようにテンプレートコードを変更する必要があります。

 単純なユーザーストアクラスの例を次に示します。 **Tuser**ジェネリックパラメーターは、ユーザークラスの型を受け取ります。このクラスは、通常、定義したユーザークラスです。 **TKey**ジェネリックパラメーターは、ユーザーキーの型を受け取ります。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample3.cs)]

 この例では、型のデータベースの*データベース*という名前のパラメーターを受け取るコンストラクターは、データアクセスクラスを渡す方法を示すことだけを目的としています。 たとえば、MySQL の実装では、このコンストラクターは MySQLDatabase 型のパラメーターを受け取ります。 

UserStore クラス内では、操作を実行するために作成したデータアクセスクラスを使用します。 たとえば、MySQL の実装では、UserStore クラスには、Userstore のインスタンスを使用して新しいレコードを挿入する CreateAsync メソッドがあります。 **Usertable**オブジェクトの**Insert**メソッドは、前のセクションで示したメソッドと同じです。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample4.cs)]

### <a name="interfaces-to-implement-when-customizing-user-store"></a>ユーザーストアをカスタマイズするときに実装するインターフェイス

次の図は、各インターフェイスで定義されている機能の詳細を示しています。 すべての省略可能なインターフェイスは、IUserStore から継承します。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image4.png)

- **IUserStore**  
  [IUserStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613278(v=vs.108).aspx)インターフェイスは、ユーザーストアに実装する必要がある唯一のインターフェイスです。 ユーザーの作成、更新、削除、および取得を行うためのメソッドを定義します。
- **IUserClaimStore**  
  [IUserClaimStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613265(v=vs.108).aspx)インターフェイスは、ユーザーの信頼性情報を有効にするためにユーザーストアに実装する必要があるメソッドを定義します。 これには、メソッドが含まれているか、ユーザー要求を追加、削除、取得します。
- **IUserLoginStore**  
  [IUserLoginStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613272(v=vs.108).aspx)は、外部認証プロバイダーを有効にするためにユーザーストアに実装する必要があるメソッドを定義します。 これには、ユーザーログインを追加、削除、取得するためのメソッド、およびログイン情報に基づいてユーザーを取得するためのメソッドが含まれています。
- **IUserRoleStore**  
  [IUserRoleStore&lt;TKey, TUser&gt;](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx)インターフェイスは、ユーザーをロールにマップするためにユーザーストアに実装する必要があるメソッドを定義します。 これには、ユーザーのロールを追加、削除、取得するメソッド、およびユーザーがロールに割り当てられているかどうかを確認するメソッドが含まれています。
- **IUserPasswordStore**  
  [IUserPasswordStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613273(v=vs.108).aspx)インターフェイスは、ハッシュされたパスワードを保持するためにユーザーストアに実装する必要があるメソッドを定義します。 ハッシュされたパスワードを取得および設定するためのメソッドと、ユーザーがパスワードを設定したかどうかを示すメソッドが含まれています。
- **IUserSecurityStampStore**  
  [IUserSecurityStampStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613277(v=vs.108).aspx)インターフェイスは、ユーザーのアカウント情報が変更されたかどうかを示すセキュリティスタンプを使用するために、ユーザーストアに実装する必要があるメソッドを定義します。 このスタンプは、ユーザーがパスワードを変更したとき、またはログインを追加または削除したときに更新されます。 セキュリティスタンプを取得および設定するためのメソッドが含まれています。
- **IUserTwoFactorStore**  
  [IUserTwoFactorStore&lt;tuser, TKey&gt;](https://msdn.microsoft.com/library/dn613279(v=vs.108).aspx)インターフェイスは、2要素認証を実装するために実装する必要があるメソッドを定義します。 これには、ユーザーに対して2要素認証を有効にするかどうかを取得および設定するためのメソッドが含まれています。
- **IUserPhoneNumberStore**  
  [IUserPhoneNumberStore&lt;tuser, TKey&gt;](https://msdn.microsoft.com/library/dn613275(v=vs.108).aspx)インターフェイスは、ユーザーの電話番号を格納するために実装する必要があるメソッドを定義します。 電話番号を取得して設定するためのメソッド、および電話番号を確認する方法が含まれています。
- **IUserEmailStore**  
  [IUserEmailStore&lt;tuser, TKey&gt;](https://msdn.microsoft.com/library/dn613143(v=vs.108).aspx)インターフェイスは、ユーザーの電子メールアドレスを格納するために実装する必要があるメソッドを定義します。 このファイルには、電子メールアドレスを取得および設定するためのメソッドと、電子メールを確認するかどうかが含まれています。
- **IUserLockoutStore**  
  [IUserLockoutStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613271(v=vs.108).aspx)インターフェイスは、アカウントのロックに関する情報を格納するために実装する必要があるメソッドを定義します。 これには、失敗したアクセス試行の現在の数を取得し、アカウントをロックできるかどうかを取得および設定するメソッド、ロックアウト終了日の取得と設定、失敗した試行の数の増加、および失敗した試行回数のリセットを行うメソッドが含まれています。
- **IQueryableUserStore**  
  [Iqueryableuserstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613267(v=vs.108).aspx)インターフェイスは、クエリ可能なユーザーストアを提供するために実装する必要があるメンバーを定義します。 これには、クエリ可能なユーザーを保持するプロパティが含まれています。

  アプリケーションで必要なインターフェイスを実装します。次に示すように、IUserClaimStore、IUserLoginStore、IUserRoleStore、IUserPasswordStore、IUserSecurityStampStore の各インターフェイスがあります。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample5.cs)]

(すべてのインターフェイスを含む) 完全な実装については、「 [Userstore (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs)」を参照してください。

### <a name="identityuserclaim-identityuserlogin-and-identityuserrole"></a>ユーザー Id、ユーザー名、およびユーザー名

Microsoft の Identity. EntityFramework 名前空間[には、](https://msdn.microsoft.com/library/dn613250(v=vs.108).aspx)[ユーザー id クラス](https://msdn.microsoft.com/library/dn613251(v=vs.108).aspx)の[実装が含まれています](https://msdn.microsoft.com/library/dn613252(v=vs.108).aspx)。 これらの機能を使用している場合は、これらのクラスの独自のバージョンを作成し、アプリケーションのプロパティを定義することができます。 ただし、基本的な操作 (ユーザーの要求の追加や削除など) を実行するときに、これらのエンティティをメモリに読み込まない方が効率的な場合もあります。 代わりに、バックエンドストアクラスは、データソースでこれらの操作を直接実行できます。 たとえば、GetClaimsAsync () メソッドは、FindByUserId (ユーザーを呼び出すことができます。Id) そのテーブルに対してクエリを直接実行し、クレームの一覧を返すメソッド。

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample6.cs)]

<a id="role"></a>
## <a name="customize-the-role-class"></a>ロールクラスをカスタマイズする

独自のストレージプロバイダーを実装する場合は、ロールクラスを作成する必要があります。これは、次のように、名前空間が指定されている[id](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx)クラスの id に[相当します](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityrole(v=vs.108).aspx)。

次の図は、作成する必要があるユーザーロールクラスと、このクラスで実装するインターフェイスを示しています。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image5.png)

[Irole&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx)インターフェイスは、要求された操作の実行時に RoleManager が呼び出すプロパティを定義します。 インターフェイスには、Id と名前の2つのプロパティが含まれています。 [Irole&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx)インターフェイスを使用すると、汎用の**tkey**パラメーターを使用してロールのキーの型を指定できます。 Id プロパティの型は、TKey パラメーターの値と一致します。

また、Id フレームワークは、キーに文字列値を使用する場合に、 [Irole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.irole(v=vs.108).aspx)インターフェイス (ジェネリックパラメーターなし) も提供します。

次の例では、キーに整数を使用する、identity Role クラスを示しています。 Id フィールドは、ジェネリックパラメーターの値と一致するように int に設定されます。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample7.cs)]

 完全な実装については、「identity [role (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs)」を参照してください。 

<a id="rolestore"></a>
## <a name="customize-the-role-store"></a>ロールストアをカスタマイズする

また、ロールに対するすべてのデータ操作のメソッドを提供する RoleStore クラスも作成します。 このクラスは、&gt;名前空間の[Rolestore&lt;TRole](https://msdn.microsoft.com/library/dn468181(v=vs.108).aspx)クラスに相当しています。 RoleStore クラスでは、 [Irolestore&lt;trole、tkey&gt;](https://msdn.microsoft.com/library/dn613266(v=vs.108).aspx)を実装し、必要に応じて、 [Iqueryablerolestore&lt;trole、tkey&gt;](https://msdn.microsoft.com/library/dn613262(v=vs.108).aspx)インターフェイスを実装します。

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image6.png)

次の例は、ロールストアクラスを示しています。 TRole ジェネリックパラメーターは、ロールクラスの型を受け取ります。通常は、定義したユーザーロールクラスです。 TKey ジェネリックパラメーターは、ロールキーの型を受け取ります。 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample8.cs)]

- **IRoleStore&lt;TRole&gt;**  
  [Irolestore](https://msdn.microsoft.com/library/dn468195.aspx)インターフェイスは、ロールストアクラスに実装するメソッドを定義します。 これには、ロールを作成、更新、削除、および取得するためのメソッドが含まれています。
- **RoleStore&lt;TRole&gt;**  
  RoleStore をカスタマイズするには、IRoleStore インターフェイスを実装するクラスを作成します。 システムでロールを使用する場合にのみ、このクラスを実装する必要があります。 型のデータベースの*データベース*という名前のパラメーターを受け取るコンストラクターは、データアクセスクラスを渡す方法を示すことだけを目的としています。 たとえば、MySQL の実装では、このコンストラクターは MySQLDatabase 型のパラメーターを受け取ります。  
  
  完全な実装については、「 [Rolestore (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) 」を参照してください。

<a id="reconfigure"></a>
## <a name="reconfigure-application-to-use-new-storage-provider"></a>新しい記憶域プロバイダーを使用するようにアプリケーションを再構成する

新しい記憶域プロバイダーが実装されました。 ここで、この記憶域プロバイダーを使用するようにアプリケーションを構成する必要があります。 既定のストレージプロバイダーがプロジェクトに含まれていた場合は、既定のプロバイダーを削除し、プロバイダーに置き換える必要があります。

### <a name="replace-default-storage-provider-in-mvc-project"></a>MVC プロジェクトの既定のストレージプロバイダーを置き換える

1. **[NuGet パッケージの管理]** ウィンドウで、 **Microsoft ASP.NET id entityframework**パッケージをアンインストールします。 このパッケージは、インストールされている Id. EntityFramework パッケージで検索できます。  
    ![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image7.png) Entity Framework もアンインストールするかどうかを確認するメッセージが表示されます。 アプリケーションの他の部分で必要とされない場合は、アンインストールできます。
2. [モデル] フォルダーの IdentityModels.cs ファイルで、 **Applicationuser**および**applicationdbcontext**クラスを削除またはコメントアウトします。 MVC アプリケーションでは、IdentityModels.cs ファイル全体を削除できます。 Web フォームアプリケーションでは、2つのクラスを削除しますが、IdentityModels.cs ファイルにもあるヘルパークラスを保持していることを確認してください。
3. ストレージプロバイダーが別のプロジェクトに存在する場合は、web アプリケーションに参照を追加します。
4. `using Microsoft.AspNet.Identity.EntityFramework;` へのすべての参照を、ストレージプロバイダーの名前空間の using ステートメントに置き換えます。
5. **Startup.Auth.cs**クラスで、適切なコンテキストの1つのインスタンスを使用するように**ConfigureAuth**メソッドを変更します。 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample9.cs?highlight=3)]
6. アプリ\_の [開始] フォルダーで、 **IdentityConfig.cs**を開きます。 ApplicationUserManager クラスで、**作成**方法を変更して、カスタマイズしたユーザーストアを使用するユーザーマネージャーを返します。 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample10.cs?highlight=3)]
7. **Applicationuser**へのすべての参照を、**ユーザー**に置き換えます。
8. 既定のプロジェクトには、IUser インターフェイスで定義されていないユーザークラスのメンバーが含まれています。(Email、PasswordHash、Generateuseridentity Async など)。 ユーザークラスにこれらのメンバーが含まれていない場合は、これらのメンバーを実装するか、これらのメンバーを使用するコードを変更する必要があります。
9. RoleManager のインスタンスを作成した場合は、新しい RoleStore クラスを使用するようにそのコードを変更します。  

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample11.cs)]
10. 既定のプロジェクトは、キーの文字列値を持つユーザークラス用に設計されています。 ユーザークラスのキーの型 (整数など) が異なる場合は、その型を使用するようにプロジェクトを変更する必要があります。 「 [ASP.NET Identity のユーザーの主キーの変更](change-primary-key-for-users-in-aspnet-identity.md)」を参照してください。
11. 必要に応じて、接続文字列を web.config ファイルに追加します。

<a id="other"></a>
## <a name="other-resources"></a>その他のリソース

- ブログ:[ASP.NET Identity の実装](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- チュートリアルと GIT コード:[Simple. Data Asp.Net Id プロバイダー](http://designcoderelease.blogspot.co.uk/2015/03/simpledata-aspnet-identity-provider.html)
- チュートリアル:[基本的な id アカウントを設定し、外部 DB でポイント](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)する。 [@xivSolutions](https://twitter.com/xivSolutions)。
- チュートリアル[:カスタム MySQL ASP.NET Identity ストレージプロバイダーの実装](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- [Softfluent](http://www.softfluent.com/)による[Codefluent エンティティ](http://blog.codefluententities.com/2014/04/30/asp-net-identity-v2-and-codefluent-entities/)
- [Azure Table Storage](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/) James randall)。
- Azure Table Storage:[AspNet. TableStorage](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage) [@stuartleeks](https://twitter.com/stuartleeks)します。
- [CouchDB/Cloudant by Daniel Wertheim。](https://github.com/danielwertheim/mycouch.aspnet.identity)
- エラスティック Searc[h:Bombsquad AB によって](https://github.com/bmbsqd/elastic-identity) エラスティック Id。
- Jonathan Sheely Jonathan Sheely による[MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) 。
- [N](https://github.com/milesibastos/NHibernate.AspNet.Identity) Io ミル Esi Bastos によって Id が識別されます。
- [@tourismgeek](https://twitter.com/tourismgeek)による[RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) 。
- [RavenDB](https://github.com/ILMServices/RavenDB.AspNet.Identity) [ilmservices](http://www.ilmservice.com/)によって識別されます。
- Cache[Redis. AspNet. Identity](https://github.com/aminjam/Redis.AspNet.Identity)
- "Database first" ユーザーストアの EF コードを生成する T4 テンプレート:[AspNet. EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)

---
uid: web-forms/overview/older-versions-security/roles/creating-and-managing-roles-vb
title: ロールの作成と管理 (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、ロールフレームワークを構成するために必要な手順について説明します。 ここでは、ロールを作成および削除するための web ページを作成します。
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 83af9f5f-9a00-4f83-8afc-e98bdd49014e
msc.legacyurl: /web-forms/overview/older-versions-security/roles/creating-and-managing-roles-vb
msc.type: authoredcontent
ms.openlocfilehash: 825e2afb750925637d308b7ceb35e1b02b708c1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586267"
---
# <a name="creating-and-managing-roles-vb"></a>ロールを作成し、管理する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.09.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial09_CreatingRoles_vb.pdf)

> このチュートリアルでは、ロールフレームワークを構成するために必要な手順について説明します。 ここでは、ロールを作成および削除するための web ページを作成します。

## <a name="introduction"></a>はじめに

<a id="_msoanchor_1"> </a>[*ユーザーベースの承認*](../membership/user-based-authorization-vb.md)に関するチュートリアルでは、URL 承認を使用して、ページのセットから特定のユーザーを制限する方法について説明しました。また、訪問しているユーザーに基づいて ASP.NET ページの機能を調整するための宣言型およびプログラム的な手法についても説明しました。 ただし、ユーザーごとにページアクセスまたは機能に対するアクセス許可を付与すると、ユーザーアカウントが多数存在する場合や、ユーザーの特権が頻繁に変更された場合に、メンテナンスが困難になることがあります。 ユーザーが特定のタスクを実行するための承認を取得したり、許可を失ったりするたびに、管理者は適切な URL 承認規則、宣言型マークアップ、およびコードを更新する必要があります。

これは通常、ユーザーをグループまたは*ロール*に分類し、ロールごとにアクセス許可を適用するのに役立ちます。 たとえば、ほとんどの web アプリケーションには、管理ユーザー専用に予約されている特定のページまたはタスクのセットがあります。 *ユーザーベースの承認*のチュートリアルで学習した手法を使用して、適切な URL 承認規則、宣言型マークアップ、およびコードを追加して、指定したユーザーアカウントが管理タスクを実行できるようにします。 ただし、新しい管理者が追加された場合、または既存の管理者が自分の管理権限を取り消す必要がある場合は、構成ファイルと web ページを戻って更新する必要があります。 ただし、ロールを使用すると、Administrators というロールを作成し、それらの信頼されたユーザーを管理者ロールに割り当てることができます。 次に、適切な URL 承認規則、宣言型マークアップ、およびコードを追加して、管理者ロールがさまざまな管理タスクを実行できるようにします。 このインフラストラクチャが整備されていれば、新しい管理者をサイトに追加したり、既存の管理者を削除したりするだけで、管理者ロールのユーザーを追加したり削除したりすることができます。 構成、宣言型のマークアップ、またはコードの変更は必要ありません。

ASP.NET には、ロールを定義し、それらをユーザーアカウントに関連付けるためのロールフレームワークが用意されています。 ロールフレームワークを使用すると、ロールの作成と削除、ロールに対するユーザーの追加または削除、特定のロールに属するユーザーのセットの特定、およびユーザーが特定のロールに属しているかどうかの確認を行うことができます。 ロールフレームワークを構成したら、URL 承認規則によってロールごとのページへのアクセスを制限し、現在ログオンしているユーザーのロールに基づいてページの追加情報や機能を表示または非表示にすることができます。

このチュートリアルでは、ロールフレームワークを構成するために必要な手順について説明します。 ここでは、ロールを作成および削除するための web ページを作成します。 <a id="_msoanchor_2"> </a>[*ユーザーへのロールの割り当て*](assigning-roles-to-users-vb.md)に関するチュートリアルでは、ロールのユーザーを追加および削除する方法について説明します。 ロールベースの<a id="_msoanchor_3"> </a>[*承認*](role-based-authorization-vb.md)のチュートリアルでは、ロールごとのページへのアクセスを制限する方法に加えて、訪問ユーザーのロールに応じてページの機能を調整する方法についても説明します。 では、始めましょう。

## <a name="step-1-adding-new-aspnet-pages"></a>手順 1: 新しい ASP.NET ページを追加する

このチュートリアルと次の2つでは、さまざまなロールに関連する関数と機能を調べます。 これらのチュートリアル全体で検討したトピックを実装するには、一連の ASP.NET ページが必要です。 これらのページを作成し、サイトマップを更新してみましょう。

まず、`Roles`という名前のプロジェクトに新しいフォルダーを作成します。 次に、4つの新しい ASP.NET ページを `Roles` フォルダーに追加し、各ページを `Site.master` マスターページとリンクします。 ページに名前を指定します。

- `ManageRoles.aspx`
- `UsersAndRoles.aspx`
- `CreateUserWizardWithRoles.aspx`
- `RoleBasedAuthorization.aspx`

この時点で、プロジェクトのソリューションエクスプローラーは、図1に示すスクリーンショットのようになります。

[![4 つの新しいページが Roles フォルダーに追加されました](creating-and-managing-roles-vb/_static/image2.png)](creating-and-managing-roles-vb/_static/image1.png)

**図 1**: `Roles` フォルダーに4つの新しいページが追加されました ([クリックしてフルサイズの画像を表示](creating-and-managing-roles-vb/_static/image3.png))

各ページには、この時点で2つのコンテンツコントロールが含まれている必要があります。1つは、`MainContent` と `LoginContent`の各マスターページの ContentPlaceHolders です。

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample1.aspx)]

`LoginContent` ContentPlaceHolder の既定のマークアップによって、ユーザーが認証されているかどうかに応じて、サイトへのログオンまたはログオフを行うためのリンクが表示されることを思い出してください。 ただし、ASP.NET ページの `Content2` コンテンツコントロールの存在は、マスターページの既定のマークアップよりも優先されます。 <a id="_msoanchor_4"> </a> [ *「フォーム認証チュートリアルの概要*](../introduction/an-overview-of-forms-authentication-vb.md)」で説明したように、既定のマークアップのオーバーライドは、ログイン関連のオプションを左の列に表示しないページで役立ちます。

ただし、この4つのページでは、`LoginContent` ContentPlaceHolder のマスターページの既定のマークアップを表示します。 そのため、`Content2` コンテンツコントロールの宣言型マークアップを削除します。 その後、4ページの各マークアップには、コンテンツコントロールを1つだけ含める必要があります。

最後に、サイトマップ (`Web.sitemap`) を更新して、これらの新しい web ページを追加してみましょう。 メンバーシップのチュートリアル用に追加した `<siteMapNode>` の後に、次の XML を追加します。

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample2.xml)]

サイトマップが更新されたら、ブラウザーを使用してサイトにアクセスします。 図2に示すように、左側のナビゲーションには、ロールのチュートリアルの項目が含まれています。

[![4 つの新しいページが Roles フォルダーに追加されました](creating-and-managing-roles-vb/_static/image5.png)](creating-and-managing-roles-vb/_static/image4.png)

**図 2**: `Roles` フォルダーに4つの新しいページが追加されました ([クリックしてフルサイズの画像を表示](creating-and-managing-roles-vb/_static/image6.png))

## <a name="step-2-specifying-and-configuring-the-roles-framework-provider"></a>手順 2: Roles Framework プロバイダーの指定と構成

メンバーシップフレームワークと同様に、ロールフレームワークはプロバイダーモデルの上に構築されます。 <a id="_msoanchor_5"> </a>[*セキュリティの基本と ASP.NET のサポート*](../introduction/security-basics-and-asp-net-support-vb.md)のチュートリアルで説明したように、.NET Framework には、 [`AuthorizationStoreRoleProvider`](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx)、 [`WindowsTokenRoleProvider`](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx)、および[`SqlRoleProvider`](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)の3つの組み込みのロールプロバイダーが付属しています。 このチュートリアルシリーズでは、ロールストアとして Microsoft SQL Server データベースを使用する `SqlRoleProvider`について説明します。

の下には、ロールフレームワークと `SqlRoleProvider` が含まれており、メンバーシップフレームワークや `SqlMembershipProvider`と同じように動作します。 .NET Framework には、ロールフレームワークの API として機能する `Roles` クラスが含まれています。 `Roles` クラスには、`CreateRole`、`DeleteRole`、`GetAllRoles`、`AddUserToRole`、`IsUserInRole`などの共有メソッドがあります。 これらのメソッドのいずれかが呼び出されると、`Roles` クラスによって、構成されたプロバイダーへの呼び出しがデリゲートされます。 `SqlRoleProvider` は、応答でロール固有のテーブル (`aspnet_Roles` と `aspnet_UsersInRoles`) と連携します。

アプリケーションで `SqlRoleProvider` プロバイダーを使用するには、ストアとして使用するデータベースを指定する必要があります。 `SqlRoleProvider` では、指定されたロールストアに特定のデータベーステーブル、ビュー、およびストアドプロシージャが含まれている必要があります。 これらの必要なデータベースオブジェクトは、 [`aspnet_regsql.exe` ツール](https://msdn.microsoft.com/library/ms229862.aspx)を使用して追加できます。 この時点で、`SqlRoleProvider`に必要なスキーマを持つデータベースが既に存在します。 「SQL Server の<a id="_msoanchor_6"> </a>[*メンバーシップスキーマの作成」* ](../membership/creating-the-membership-schema-in-sql-server-vb.md)チュートリアルに戻り、`SecurityTutorials.mdf` という名前のデータベースを作成し、`aspnet_regsql.exe` を使用してアプリケーションサービスを追加しました。これには、`SqlRoleProvider`に必要なデータベースオブジェクトが含まれていました。 そのため、ロールのサポートを有効にし、`SecurityTutorials.mdf` データベースでロールストアとして `SqlRoleProvider` を使用するようにロールフレームワークに指示するだけです。

ロールフレームワークは、アプリケーションの `Web.config` ファイル内の `<roleManager>` 要素を使用して構成されます。 既定では、ロールのサポートは無効になっています。 有効にするには、次のように[`<roleManager>`](https://msdn.microsoft.com/library/ms164660.aspx)要素の `enabled` 属性を `true` に設定する必要があります。

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample3.xml)]

既定では、すべての web アプリケーションに `SqlRoleProvider`型の `AspNetSqlRoleProvider` という名前のロールプロバイダーがあります。 この既定のプロバイダーは `machine.config` (`%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`にあります) に登録されています。

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample4.xml)]

プロバイダーの `connectionStringName` 属性は、使用するロールストアを指定します。 `AspNetSqlRoleProvider` プロバイダーは、この属性を `LocalSqlServer`に設定します。これは、既定では `machine.config` とポイントで `App_Data` という名前の `aspnet.mdf`フォルダー内の SQL Server 2005 Express Edition データベースにも定義されます。

そのため、アプリケーションの `Web.config` ファイルでプロバイダー情報を指定せずにロールフレームワークを有効にするだけであれば、アプリケーションは既定の登録済みロールプロバイダーである `AspNetSqlRoleProvider`を使用します。 `~/App_Data/aspnet.mdf` データベースが存在しない場合は、ASP.NET ランタイムによって自動的に作成され、アプリケーションサービススキーマが追加されます。 ただし、`aspnet.mdf` データベースは使用しません。ここでは、既に作成した `SecurityTutorials.mdf` データベースを使用して、アプリケーションサービススキーマをに追加します。 この変更は、次の2つの方法のいずれかで行うことができます。

- <strong>`Web.config`</strong>で、<strong>`LocalSqlServer`</strong><strong>接続文字列名</strong><strong>の値を指定</strong>し<strong>ます。</strong> `Web.config`の `LocalSqlServer` 接続文字列名の値を上書きすることで、既定の登録済みロールプロバイダー (`AspNetSqlRoleProvider`) を使用して、`SecurityTutorials.mdf` データベースと正しく連携させることができます。 この手法の詳細については、 [Scott Guthrie](https://weblogs.asp.net/scottgu/)のブログ記事「 [SQL Server 2000 または SQL Server 2005 を使用するように ASP.NET 2.0 アプリケーションサービスを構成する](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)」を参照してください。
- <strong>`SqlRoleProvider`</strong><strong>種類の新しい登録済みプロバイダーを追加</strong>し、<strong>`SecurityTutorials.mdf`</strong>データベース<strong>を指すようにその`connectionStringName`設定を</strong><strong>構成し</strong><strong>ます。</strong> これは、 <a id="_msoanchor_7"> </a> [*SQL Server チュートリアルでメンバーシップスキーマを作成*](../membership/creating-the-membership-schema-in-sql-server-vb.md)するために推奨されているアプローチであり、このチュートリアルで使用するアプローチです。

次のロールの構成マークアップを `Web.config` ファイルに追加します。 このマークアップは、という名前の新しいプロバイダーを登録 `SecurityTutorialsSqlRoleProvider.`

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample5.xml)]

上のマークアップでは、(`<roleManager>` 要素の `defaultProvider` 属性を使用して) 既定のプロバイダーとして `SecurityTutorialsSqlRoleProvider` が定義されています。 また、`SecurityTutorialsSqlRoleProvider`の `applicationName` 設定を `SecurityTutorials`に設定します。これは、メンバーシッププロバイダー (`SecurityTutorialsSqlMembershipProvider`) によって使用されるのと同じ `applicationName` 設定です。 ここには示されていませんが、`SqlRoleProvider` の[`<add>` 要素](https://msdn.microsoft.com/library/ms164662.aspx)には、データベースのタイムアウト期間を秒単位で指定するための `commandTimeout` 属性が含まれている場合もあります。 既定値は、30 です。

この構成マークアップを使用すると、アプリケーション内でロール機能の使用を開始する準備が整います。

> [!NOTE]
> 上記の構成マークアップは、`<roleManager>` 要素の `enabled` 属性と `defaultProvider` 属性の使用方法を示しています。 ロールフレームワークがユーザーごとにロール情報を関連付ける方法に影響する属性は他にも多数あります。 これらの設定については<a id="_msoanchor_8"> </a>、[*ロールベースの承認*](role-based-authorization-vb.md)に関するチュートリアルで確認します。

## <a name="step-3-examining-the-roles-api"></a>手順 3: Roles API を調べる

ロールフレームワークの機能は[`Roles` クラス](https://msdn.microsoft.com/library/system.web.security.roles.aspx)を介して公開されます。このクラスには、ロールベースの操作を実行するための13個の共有メソッドが含まれています。 手順 4. と 6. でロールを作成および削除することを検討している場合は、システムにロールを追加または削除する[`CreateRole`](https://msdn.microsoft.com/library/system.web.security.roles.createrole.aspx)および[`DeleteRole`](https://msdn.microsoft.com/library/system.web.security.roles.deleterole.aspx)メソッドを使用します。

システム内のすべてのロールの一覧を取得するには、 [`GetAllRoles` メソッド](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx)を使用します (手順 5. を参照)。 [`RoleExists` メソッド](https://msdn.microsoft.com/library/system.web.security.roles.roleexists.aspx)は、指定されたロールが存在するかどうかを示すブール値を返します。

次のチュートリアルでは、ユーザーをロールに関連付ける方法について説明します。 `Roles` クラスの[`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx)、 [`AddUserToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.addusertoroles.aspx)、 [`AddUsersToRole`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstorole.aspx)、および[`AddUsersToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstoroles.aspx)の各メソッドは、1人以上のユーザーを1つ以上のロールに追加します。 ロールからユーザーを削除するには、 [`RemoveUserFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)、 [`RemoveUserFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromroles.aspx)、 [`RemoveUsersFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromrole.aspx)、または[`RemoveUsersFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromroles.aspx)メソッドを使用します。

<a id="_msoanchor_9"> </a>[*ロールベースの承認*](role-based-authorization-vb.md)のチュートリアルでは、現在ログインしているユーザーのロールに基づいて機能をプログラムで表示または非表示にする方法について説明します。 これを実現するには、ロールクラスの[`FindUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.findusersinrole.aspx)、 [`GetRolesForUser`](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx)、 [`GetUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx)、または[`IsUserInRole`](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)メソッドを使用します。

> [!NOTE]
> これらのメソッドのいずれかが呼び出されるたびに、`Roles` クラスによって、構成されたプロバイダーへの呼び出しがデリゲートされることに注意してください。 この場合は、呼び出しが `SqlRoleProvider`に送信されていることを意味します。 `SqlRoleProvider` は、呼び出されたメソッドに基づいて適切なデータベース操作を実行します。 たとえば、コード `Roles.CreateRole("Administrators")` は `aspnet_Roles_CreateRole` ストアドプロシージャを実行し `SqlRoleProvider` します。これにより、管理者という名前の `aspnet_Roles` テーブルに新しいレコードが挿入されます。

このチュートリアルの残りの部分では、`Roles` クラスの `CreateRole`、`GetAllRoles`、および `DeleteRole` の各メソッドを使用して、システムのロールを管理する方法について見ていきます。

## <a name="step-4-creating-new-roles"></a>手順 4: 新しいロールの作成

ロールはユーザーを任意にグループ化する手段を提供します。通常、このグループ化は、承認規則を適用するためのより便利な方法として使用されます。 ただし、承認メカニズムとしてロールを使用するには、まず、アプリケーションにどのロールが存在するかを定義する必要があります。 残念ながら、ASP.NET には CreateRoleWizard コントロールは含まれていません。 新しいロールを追加するには、適切なユーザーインターフェイスを作成し、ロール API を自分で呼び出す必要があります。 すばらしいのは、これは非常に簡単な方法です。

> [!NOTE]
> CreateRoleWizard Web コントロールはありませんが、 [ASP.NET Web サイト管理ツール](https://msdn.microsoft.com/library/ms228053.aspx)があります。これは、web アプリケーションの構成の表示と管理を支援するように設計されたローカル ASP.NET アプリケーションです。 ただし、2つの理由から、ASP.NET Web サイト管理ツールの大きなファンではありません。 まず、少しのバグが発生し、ユーザーエクスペリエンスが必要になることがあります。 次に、ASP.NET Web サイト管理ツールは、ローカルでのみ機能するように設計されています。つまり、ライブサイトでロールをリモート管理する必要がある場合は、独自のロール管理 Web ページを作成する必要があります。 このチュートリアルと次の2つの理由により、ASP.NET Web サイト管理ツールを使用するのではなく、web ページで必要なロール管理ツールを構築することに重点を置いています。

`Roles` フォルダーの [`ManageRoles.aspx`] ページを開き、テキストボックスとボタン Web コントロールをページに追加します。 TextBox コントロールの `ID` プロパティを `RoleName` に設定し、ボタンの `ID` と `Text` プロパティをそれぞれ `CreateRoleButton` に設定して、ロールを作成します。 この時点で、ページの宣言型マークアップは次のようになります。

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample6.aspx)]

次に、デザイナーの [`CreateRoleButton`] ボタンコントロールをダブルクリックして、`Click` イベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample7.vb)]

上記のコードでは、最初に、[`RoleName`] ボックスに入力したトリミングされたロール名を `newRoleName` 変数に割り当てます。 次に、`Roles` クラスの `RoleExists` メソッドを呼び出して、ロール `newRoleName` がシステムに既に存在するかどうかを確認します。 ロールが存在しない場合は、`CreateRole` メソッドの呼び出しを使用して作成されます。 `CreateRole` メソッドに、システムに既に存在するロール名が渡されると、`ProviderException` 例外がスローされます。 このため、このコードでは、`CreateRole`を呼び出す前に、ロールがシステムに存在していないことを最初に確認します。 `Click` イベントハンドラーは、`RoleName` テキストボックスの `Text` プロパティをクリアすることによって終了します。

> [!NOTE]
> ユーザーが [`RoleName`] ボックスに値を入力しないとどうなるか疑問に思うかもしれません。 `CreateRole` メソッドに渡された値が `Nothing` または空の文字列の場合は、例外が発生します。 同様に、ロール名にコンマが含まれている場合は、例外が発生します。 そのため、ユーザーがロールを入力し、それにコンマが含まれていないことを確認するために、ページに検証コントロールが含まれている必要があります。 閲覧者のための演習を残しておきます。

管理者という名前のロールを作成してみましょう。 ブラウザーを使用して `ManageRoles.aspx` ページにアクセスし、テキストボックスに管理者を入力し (図3を参照)、[ロールの作成] ボタンをクリックします。

[管理者ロールを作成 ![には](creating-and-managing-roles-vb/_static/image8.png)](creating-and-managing-roles-vb/_static/image7.png)

**図 3**: 管理者ロールを作成[する (クリックすると、フルサイズの画像が表示](creating-and-managing-roles-vb/_static/image9.png)されます)

どうしたらよいでしょうか。 ポストバックが発生しますが、ロールが実際にシステムに追加されたことを示す視覚的な手掛かりはありません。 ここでは、手順 5. でこのページを更新して、視覚的なフィードバックを含めます。 ただし現時点では、ロールが作成されたことを確認するには、`SecurityTutorials.mdf` データベースに移動し、`aspnet_Roles` テーブルのデータを表示します。 図4に示すように、`aspnet_Roles` テーブルには、追加された管理者ロールのレコードが含まれています。

[aspnet_Roles テーブルに管理者の行がある ![](creating-and-managing-roles-vb/_static/image11.png)](creating-and-managing-roles-vb/_static/image10.png)

**図 4**: `aspnet_Roles` テーブルに管理者用の行がある ([クリックすると、フルサイズの画像が表示](creating-and-managing-roles-vb/_static/image12.png)されます)

## <a name="step-5-displaying-the-roles-in-the-system"></a>手順 5: システムでのロールの表示

`ManageRoles.aspx` ページを拡張して、システム内の現在のロールの一覧を追加してみましょう。 これを行うには、GridView コントロールをページに追加し、その `ID` プロパティを `RoleList`に設定します。 次に、次のコードを使用して、`DisplayRolesInGrid` という名前のページの分離コードクラスにメソッドを追加します。

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample8.vb)]

`Roles` クラスの `GetAllRoles` メソッドは、システム内のすべてのロールを文字列の配列として返します。 この文字列配列は、GridView にバインドされます。 ページが最初に読み込まれたときにロールの一覧を GridView にバインドするには、ページの `Page_Load` イベントハンドラーから `DisplayRolesInGrid` メソッドを呼び出す必要があります。 次のコードは、ページが最初にアクセスされたときにこのメソッドを呼び出しますが、後続のポストバックでは呼び出されません。

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample9.vb)]

このコードを配置したら、ブラウザーを使用してページにアクセスします。 図5に示すように、"Item" というラベルが付いた1列のグリッドが表示されます。 グリッドには、手順 4. で追加した管理者ロールの行が含まれています。

[GridView によってロールが1つの列に表示される ![](creating-and-managing-roles-vb/_static/image14.png)](creating-and-managing-roles-vb/_static/image13.png)

**図 5**: GridView によってロールが1つの列に表示される ([クリックすると、フルサイズの画像が表示](creating-and-managing-roles-vb/_static/image15.png)されます)

Gridview の [`AutoGenerateColumns`] プロパティが True (既定値) に設定されているため、gridview では、[Item] というラベルの付いた列のみが表示されます。これにより、GridView は、`DataSource`の各プロパティに対して自動的に列を作成します。 配列には、配列内の要素を表す1つのプロパティがあります。したがって、GridView の単一の列です。

GridView を使用してデータを表示する場合は、GridView によって暗黙的に生成されるのではなく、列を明示的に定義します。 列を明示的に定義することにより、データの書式設定、列の再配置、およびその他の一般的なタスクをより簡単に実行できるようになります。 そのため、GridView の宣言型マークアップを更新して、その列が明示的に定義されるようにしましょう。

まず、GridView の `AutoGenerateColumns` プロパティを False に設定します。 次に、グリッドに TemplateField を追加し、その `HeaderText` プロパティを Roles に設定し、配列の内容が表示されるように `ItemTemplate` を構成します。 これを行うには、`RoleNameLabel` という名前のラベル Web コントロールを `ItemTemplate` に追加し、その `Text` プロパティをにバインド `Container.DataItem.`

これらのプロパティと `ItemTemplate`の内容は、宣言によって、または GridView の [フィールド] ダイアログボックスとテンプレートの編集インターフェイスを使用して設定できます。 [フィールド] ダイアログボックスに移動するには、GridView のスマートタグの [列の編集] リンクをクリックします。 次に、[フィールドの自動生成] チェックボックスをオフにして `AutoGenerateColumns` プロパティを False に設定し、GridView に TemplateField を追加して、その `HeaderText` プロパティを Role に設定します。 `ItemTemplate`の内容を定義するには、GridView のスマートタグから [テンプレートの編集] オプションを選択します。 Label Web コントロールを `ItemTemplate`にドラッグし、その `ID` プロパティを `RoleNameLabel`に設定し、その `Text` プロパティが `Container.DataItem`にバインドされるようにデータバインド設定を構成します。

使用する方法に関係なく、GridView の結果の宣言型マークアップは、完了すると次のようになります。

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample10.aspx)]

> [!NOTE]
> 配列の内容は、`<%# Container.DataItem %>`データバインド構文を使用して表示されます。 GridView にバインドされた配列の内容を表示するときにこの構文を使用する理由の詳細については、このチュートリアルでは説明しません。 詳細については、「[データ Web コントロールへのスカラー配列のバインド](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)」を参照してください。

現時点では、`RoleList` GridView は、ページが最初にアクセスされたときにのみロールの一覧にバインドされます。 新しいロールが追加されるたびにグリッドを更新する必要があります。 これを実現するには、新しいロールが作成された場合に `DisplayRolesInGrid` メソッドを呼び出すように、`CreateRoleButton` ボタンの `Click` イベントハンドラーを更新します。

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample11.vb)]

これで、ユーザーが新しいロールを追加すると、`RoleList` GridView によってポストバック時に追加されたロールが表示され、ロールが正常に作成されたことを視覚的にフィードバックできます。 これを説明するには、ブラウザーを使用して `ManageRoles.aspx` のページにアクセスし、スーパーバイザーという名前のロールを追加します。 [Create Role] \ (ロールの作成 \) ボタンをクリックすると、ポストバックが議論され、新しいロールであるスーパーバイザーに加えて、管理者と共にグリッドが更新されます。

[スーパーバイザーロールが追加され ![](creating-and-managing-roles-vb/_static/image17.png)](creating-and-managing-roles-vb/_static/image16.png)

**図 6**: スーパーバイザーロールが追加されました ([クリックすると、フルサイズの画像が表示](creating-and-managing-roles-vb/_static/image18.png)されます)

## <a name="step-6-deleting-roles"></a>手順 6: 役割を削除する

この時点で、ユーザーは `ManageRoles.aspx` ページから新しいロールを作成し、すべての既存のロールを表示できます。 ユーザーがロールを削除できるようにしましょう。 `Roles.DeleteRole` メソッドには、次の2つのオーバーロードがあります。

- [`DeleteRole(roleName)`](https://msdn.microsoft.com/library/ek4sywc0.aspx) -ロール*roleName*を削除します。 ロールに1つ以上のメンバーが含まれている場合は、例外がスローされます。
- [`DeleteRole(roleName, throwOnPopulatedRole)`](https://msdn.microsoft.com/library/38h6wf59.aspx) -ロール*roleName*を削除します。 *ThrowOnPopulateRole*が `True`場合、ロールに1つ以上のメンバーが含まれていると、例外がスローされます。 *ThrowOnPopulateRole*が `False`場合、メンバーが含まれているかどうかにかかわらず、ロールが削除されます。 内部的には、`DeleteRole(roleName)` メソッドは `DeleteRole(roleName, True)`を呼び出します。

`DeleteRole` メソッドは、 *rolename*が `Nothing` または空の文字列の場合、または*rolename*にコンマが含まれている場合にも例外をスローします。 *RoleName*がシステムに存在しない場合、`DeleteRole` は、例外を発生させることなく、サイレントモードで失敗します。

クリックすると選択したロールを削除する [削除] ボタンを含めるように、`ManageRoles.aspx` の GridView を増やしてみましょう。 まず、[フィールド] ダイアログボックスに移動し、[CommandField] オプションの下にある [削除] ボタンを追加して、GridView に Delete ボタンを追加します。 [削除] ボタンを左端の列にして、その `DeleteText` プロパティを [ロールの削除] に設定します。

[RoleList GridView に Delete ボタンを追加 ![には](creating-and-managing-roles-vb/_static/image20.png)](creating-and-managing-roles-vb/_static/image19.png)

**図 7**: `RoleList` GridView に Delete ボタンを追加する ([クリックすると、フルサイズの画像が表示](creating-and-managing-roles-vb/_static/image21.png)されます)

[削除] ボタンを追加した後、GridView の宣言型マークアップは次のようになります。

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample12.aspx)]

次に、GridView の `RowDeleting` イベントのイベントハンドラーを作成します。 これは、[ロールの削除] ボタンをクリックしたときにポストバック時に発生するイベントです。 イベント ハンドラーに次のコードを追加します。

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample13.vb)]

このコードは、[ロールの削除] ボタンがクリックされた行の `RoleNameLabel` Web コントロールをプログラムで参照することによって開始します。 次に、`Roles.DeleteRole` メソッドが呼び出され、`RoleNameLabel` と `False`の `Text` を渡して、ロールに関連付けられているユーザーがいないかどうかに関係なく、ロールを削除します。 最後に、削除したロールがグリッドに表示されなくなるように、`RoleList` GridView が更新されます。

> [!NOTE]
> [ロールの削除] ボタンでは、ロールを削除する前に、ユーザーからの確認を行う必要はありません。 アクションを確認する最も簡単な方法の1つは、クライアント側の [確認] ダイアログボックスを使用することです。 この手法の詳細については、「[削除時にクライアント側の確認を追加](https://asp.net/learn/data-access/tutorial-42-vb.aspx)する」を参照してください。

## <a name="summary"></a>要約

多くの web アプリケーションには、特定のクラスのユーザーのみが使用できる特定の承認規則またはページレベルの機能があります。 たとえば、管理者のみがアクセスできる web ページのセットがある場合があります。 ユーザーごとにこれらの承認規則を定義するのではなく、ロールに基づいて規則を定義する方が便利な場合がよくあります。 つまり、Scott と Jisun ユーザーに管理 web ページへのアクセスを明示的に許可するのではなく、管理者ロールのメンバーにこれらのページへのアクセスを許可したうえで、ユーザーに属しているユーザーとして Scott と Jisun を示すという方法があります。管理者ロール。

ロールフレームワークを使用すると、ロールの作成と管理を簡単に行うことができます。 このチュートリアルでは、Microsoft SQL Server データベースをロールストアとして使用する、`SqlRoleProvider`を使用するようにロールフレームワークを構成する方法について説明します。 また、システム内の既存のロールを一覧表示する web ページを作成し、新しいロールを作成したり、既存のロールを削除したりできるようにしました。 以降のチュートリアルでは、ユーザーをロールに割り当てる方法と、ロールベースの承認を適用する方法を説明します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET 2.0 のメンバーシップ、ロール、およびプロファイルを調べています](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [方法: ASP.NET 2.0 でロールマネージャーを使用する](https://msdn.microsoft.com/library/ms998314.aspx)
- [ロールプロバイダー](https://msdn.microsoft.com/library/aa478950.aspx)
- [独自の Web サイト管理ツールのロール](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [`<roleManager>` 要素の技術ドキュメント](https://msdn.microsoft.com/library/ms164660.aspx)
- [メンバーシップ Api とロールマネージャー Api の使用](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/membership.aspx)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者には、Alicja Maziarz、Suchi Erjee、および Teresa Murphy が含まれています。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](role-based-authorization-cs.md)
> [次へ](assigning-roles-to-users-vb.md)

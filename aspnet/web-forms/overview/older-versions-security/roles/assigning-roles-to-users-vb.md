---
uid: web-forms/overview/older-versions-security/roles/assigning-roles-to-users-vb
title: ユーザーへのロールの割り当て (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、ユーザーがどのロールに属しているかを管理するのに役立つ2つの ASP.NET ページを作成します。 最初のページには、表示する機能が含まれています...
ms.author: riande
ms.date: 03/24/2008
ms.assetid: fd208ee9-69cc-4467-9783-b4e039bdd1d3
msc.legacyurl: /web-forms/overview/older-versions-security/roles/assigning-roles-to-users-vb
msc.type: authoredcontent
ms.openlocfilehash: b53df4494eb0faef7c5e4547c2bf95e5fb071298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507280"
---
# <a name="assigning-roles-to-users-vb"></a>ユーザーにロールを割り当てる (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.10.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial10_AssigningRoles_vb.pdf)

> このチュートリアルでは、ユーザーがどのロールに属しているかを管理するのに役立つ2つの ASP.NET ページを作成します。 最初のページには、特定のロールに属しているユーザー、特定のユーザーが属するロール、特定のロールから特定のユーザーを割り当てたり削除したりする機能が含まれます。 2番目のページでは、CreateUserWizard コントロールを拡張して、新しく作成されたユーザーが所属するロールを指定する手順が含まれるようにします。 これは、管理者が新しいユーザーアカウントを作成できる場合に便利です。

## <a name="introduction"></a>はじめに

<a id="_msoanchor_1"> </a>[前のチュートリアル](creating-and-managing-roles-vb.md)では、ロールフレームワークと `SqlRoleProvider`を検証しています。`Roles` クラスを使用して、ロールを作成、取得、および削除する方法を説明しました。 ロールの作成と削除に加えて、ロールのユーザーを割り当てたり、削除したりできる必要があります。 残念ながら、ASP.NET には、どのロールに属しているかを管理するための Web コントロールは付属していません。 代わりに、これらの関連付けを管理するには、独自の ASP.NET ページを作成する必要があります。 ユーザーをロールに追加したり削除したりするのは非常に簡単です。 `Roles` クラスには、1つまたは複数のロールに1人以上のユーザーを追加するためのメソッドが多数含まれています。

このチュートリアルでは、ユーザーがどのロールに属しているかを管理するのに役立つ2つの ASP.NET ページを作成します。 最初のページには、特定のロールに属しているユーザー、特定のユーザーが属するロール、特定のロールから特定のユーザーを割り当てたり削除したりする機能が含まれます。 2番目のページでは、CreateUserWizard コントロールを拡張して、新しく作成されたユーザーが所属するロールを指定する手順が含まれるようにします。 これは、管理者が新しいユーザーアカウントを作成できる場合に便利です。

作業開始

## <a name="listing-what-users-belong-to-what-roles"></a>ユーザーがどのロールに属しているかを一覧表示する

このチュートリアルの最初のビジネスの順序は、ユーザーをロールに割り当てることができる web ページを作成することです。 ユーザーをロールに割り当てる方法については、まず、ユーザーがどのロールに属しているかを判断する方法について重点的に説明します。 この情報を表示するには、"ロール別" または "ユーザー別" の2つの方法があります。 ユーザーがロールを選択して、そのロールに属しているすべてのユーザー ("ロール" 表示) を表示できるようにするか、ユーザーに割り当てられたロールをユーザーに表示するようにビジターに要求することができます ("ユーザー" 表示)。

"ロール別" ビューは、ビジターが特定のロールに属しているユーザーのセットを知りたい場合に便利です。"ユーザーごと" のビューは、ビジターが特定のユーザーのロールを知る必要がある場合に最適です。 ページに "ロール別" と "ユーザー別" の両方のインターフェイスが含まれていることを見てみましょう。

まず、"ユーザー" インターフェイスを作成します。 このインターフェイスは、ドロップダウンリストとチェックボックスの一覧で構成されます。 ドロップダウンリストには、システム内の一連のユーザーが表示されます。チェックボックスをオンにすると、ロールが列挙されます。 ドロップダウンリストからユーザーを選択すると、ユーザーが属するロールがチェックされます。 ページにアクセスするユーザーは、チェックボックスをオンまたはオフにして、選択したユーザーを対応するロールから追加または削除することができます。

> [!NOTE]
> ドロップダウンリストを使用してユーザーアカウントを一覧表示することは、数百のユーザーアカウントが存在する可能性のある web サイトには適していません。 ドロップダウンリストは、ユーザーが比較的短いオプションの一覧から1つの項目を選択できるように設計されています。 リスト項目の数が増えるにつれて、すぐに扱いにくくなります。 多くのユーザーアカウントを持つ可能性のある web サイトを構築する場合は、ページング可能な GridView や、文字を選択するようにビジターに要求するように設定されたフィルター可能なインターフェイスなど、代替のユーザーインターフェイスの使用を検討してください。ユーザー名が選択した文字で始まるユーザーを表示します。

## <a name="step-1-building-the-by-user-user-interface"></a>手順 1: "ユーザー" ユーザーインターフェイスを作成する

[`UsersAndRoles.aspx`] ページを開きます。 ページの上部で、`ActionStatus` という名前のラベル Web コントロールを追加し、その `Text` プロパティをオフにします。 このラベルを使用して、実行された操作に関するフィードバックを提供します。 "ユーザー Tito は管理者ロールに追加されました"、"ユーザー Jisun はスーパーバイザーロールから削除されました。" などのメッセージが表示されます。 これらのメッセージを目立たせるために、ラベルの `CssClass` プロパティを "Important" に設定します。

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample1.aspx)]

次に、次の CSS クラス定義を `Styles.css` スタイルシートに追加します。

[!code-css[Main](assigning-roles-to-users-vb/samples/sample2.css)]

この CSS 定義は、大きな赤いフォントを使用してラベルを表示するようにブラウザーに指示します。 図1は、Visual Studio デザイナーを使用したこの効果を示しています。

[ラベルの CssClass プロパティを ![と、大きな赤いフォントになります。](assigning-roles-to-users-vb/_static/image2.png)](assigning-roles-to-users-vb/_static/image1.png)

**図 1**: ラベルの `CssClass` プロパティによって大きなフォントが生成される ([クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image3.png)されます)

次に、DropDownList をページに追加し、その `ID` プロパティを `UserList`に設定し、その `AutoPostBack` プロパティを True に設定します。 この DropDownList を使用して、システム内のすべてのユーザーが一覧表示されます。 この DropDownList は、MembershipUser オブジェクトのコレクションにバインドされます。 DropDownList で MembershipUser オブジェクトの UserName プロパティを表示し、それをリスト項目の値として使用するため、DropDownList の `DataTextField` と `DataValueField` のプロパティを "UserName" に設定します。

DropDownList の下に、`UsersRoleList`という名前のリピータを追加します。 このリピータには、システム内のすべてのロールが一連のチェックボックスとして一覧表示されます。 次の宣言型マークアップを使用して、リピータの `ItemTemplate` を定義します。

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample3.aspx)]

`ItemTemplate` マークアップには、`RoleCheckBox`という1つのチェックボックス Web コントロールが含まれています。 チェックボックスの `AutoPostBack` プロパティは True に設定され、`Text` プロパティは `Container.DataItem`にバインドされます。 Databinding 構文が単に `Container.DataItem` のは、ロールフレームワークがロール名のリストを文字列配列として返すためです。この文字列配列は、リピータにバインドされます。 データ Web コントロールにバインドされた配列の内容を表示するためにこの構文を使用する理由の詳細については、このチュートリアルでは説明しません。 詳細については、「[データ Web コントロールへのスカラー配列のバインド](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)」を参照してください。

この時点で、"ユーザー別" インターフェイスの宣言型マークアップは次のようになります。

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample4.aspx)]

これで、ユーザーアカウントのセットを DropDownList および一連のロールにバインドするコードを作成する準備ができました。 ページの分離コードクラスで、次のコードを使用して、`BindUsersToUserList` という名前のメソッドと、別の名前付き `BindRolesList`を追加します。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample5.vb)]

`BindUsersToUserList` メソッドは、 [`Membership.GetAllUsers` メソッド](https://msdn.microsoft.com/library/dy8swhya.aspx)を使用して、システム内のすべてのユーザーアカウントを取得します。 これにより、 [`MembershipUser` インスタンス](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)のコレクションである[`MembershipUserCollection` オブジェクト](https://msdn.microsoft.com/library/system.web.security.membershipusercollection.aspx)が返されます。 このコレクションは `UserList` DropDownList にバインドされます。 コレクションを構成する `MembershipUser` インスタンスには、`UserName`、`Email`、`CreationDate`、`IsOnline`などのさまざまなプロパティが含まれています。 DropDownList に `UserName` プロパティの値を表示するように指示するには、`UserList` DropDownList の `DataTextField` プロパティと `DataValueField` プロパティが "UserName" に設定されていることを確認します。

> [!NOTE]
> `Membership.GetAllUsers` メソッドには、2つのオーバーロードがあります。1つは入力パラメーターを受け取り、すべてのユーザーを返します。もう1つは、ページインデックスとページサイズの整数値を受け取り、指定されたユーザーのサブセットのみを返します。 ページング可能なユーザーインターフェイス要素に大量のユーザーアカウントが表示されている場合は、2番目のオーバーロードを使用して、すべてのユーザーアカウントではなくユーザーアカウントの正確なサブセットだけを返すため、ユーザーをより効率的にページングできます。

`BindRolesToList` メソッドは、`Roles` クラスの[`GetAllRoles` メソッド](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx)を呼び出すことによって開始されます。このメソッドは、システム内のロールを格納する文字列配列を返します。 その後、この文字列配列はリピータにバインドされます。

最後に、ページが最初に読み込まれるときに、これらの2つのメソッドを呼び出す必要があります。 `Page_Load` イベント ハンドラーに次のコードを追加します。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample6.vb)]

このコードが用意されているので、ブラウザーを使用してページにアクセスします。画面は図2のようになります。 すべてのユーザーアカウントがドロップダウンリストに入力され、その下に各ロールがチェックボックスとして表示されます。 DropDownList とチェックボックスの `AutoPostBack` のプロパティを True に設定すると、選択したユーザーを変更したり、ロールを確認またはオフにしたりするとポストバックが発生します。 ただし、これらのアクションを処理するコードを記述していないため、アクションは実行されません。 これらのタスクについては、次の2つのセクションで説明します。

[![ページにユーザーとロールが表示されます。](assigning-roles-to-users-vb/_static/image5.png)](assigning-roles-to-users-vb/_static/image4.png)

**図 2**: ページにユーザーとロールが表示される ([クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image6.png)されます)

### <a name="checking-the-roles-the-selected-user-belongs-to"></a>選択したユーザーが属しているロールを確認しています

ページが最初に読み込まれるとき、またはユーザーがドロップダウンリストから新しいユーザーを選択するたびに、選択したユーザーがそのロールに属している場合にのみ、特定のロールチェックボックスがオンになるように、`UsersRoleList`のチェックボックスを更新する必要があります。 これを実現するには、次のコードを使用して、`CheckRolesForSelectedUser` という名前のメソッドを作成します。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample7.vb)]

上記のコードは、選択したユーザーを特定することによって開始されます。 次に、Roles クラスの[`GetRolesForUser(userName)` メソッド](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx)を使用して、指定されたユーザーのロールセットを文字列配列として返します。 次に、リピータの項目が列挙され、各項目の `RoleCheckBox` チェックボックスがプログラムによって参照されます。 チェックボックスがオンになっているのは、対応するロールが `selectedUsersRoles` string 配列内に含まれている場合のみです。

> [!NOTE]
> ASP.NET バージョン2.0 を使用している場合、`Linq.Enumerable.Contains(Of String)(...)` 構文はコンパイルされません。 `Contains(Of String)` メソッドは、ASP.NET 3.5 の新しい[LINQ ライブラリ](http://en.wikipedia.org/wiki/Language_Integrated_Query)の一部です。 ASP.NET バージョン2.0 をまだ使用している場合は、代わりに[`Array.IndexOf(Of String)` メソッド](https://msdn.microsoft.com/library/eha9t187.aspx)を使用します。

`CheckRolesForSelectedUser` メソッドは、ページが最初に読み込まれたときと、`UserList` DropDownList の選択されたインデックスが変更されたときの2つの場合に呼び出される必要があります。 したがって、`Page_Load` イベントハンドラーからこのメソッドを呼び出します (`BindUsersToUserList` と `BindRolesToList`を呼び出した後)。 また、DropDownList の `SelectedIndexChanged` イベントのイベントハンドラーを作成し、そこからこのメソッドを呼び出します。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample8.vb)]

このコードを配置すると、ブラウザーでページをテストできます。 ただし、`UsersAndRoles.aspx` のページには現在、ユーザーをロールに割り当てる機能がないため、ロールを持つユーザーはいません。 ここでは、ユーザーをロールに割り当てるためのインターフェイスを作成します。このコードが動作することを確認し、後で実行することを確認します。または、この機能を今すぐテストするために、`aspnet_UsersInRoles` テーブルにレコードを挿入してユーザーを手動でロールに追加することもできます。

### <a name="assigning-and-removing-users-from-roles"></a>ロールへのユーザーの割り当てと削除

ビジターが `UsersRoleList` リピータのチェックボックスをオンまたはオフにしたときに、対応するロールから選択したユーザーを追加または削除する必要があります。 現在、チェックボックスの `AutoPostBack` プロパティは True に設定されています。これにより、Repeater のチェックボックスがオンまたはオフになるたびにポストバックが発生します。 つまり、CheckBox の `CheckChanged` イベントのイベントハンドラーを作成する必要があります。 このチェックボックスは Repeater コントロールにあるため、イベントハンドラーの組み込みを手動で追加する必要があります。 まず、次のように、コードビハインドクラスに `Protected` メソッドとしてイベントハンドラーを追加します。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample9.vb)]

このイベントハンドラーのコードをすぐに記述するために、を返します。 では、最初にイベント処理の組み込みを完了してみましょう。 リピータの `ItemTemplate`内のチェックボックスで、`OnCheckedChanged="RoleCheckBox_CheckChanged"`を追加します。 この構文は、`RoleCheckBox_CheckChanged` イベントハンドラーを `RoleCheckBox`の `CheckedChanged` イベントに配線します。

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample10.aspx)]

最後に、`RoleCheckBox_CheckChanged` イベントハンドラーを完成させます。 この CheckBox インスタンスは、`Text` と `Checked` のプロパティを使用してチェックされたロールまたはチェック解除されたロールを示すので、イベントを発生させた CheckBox コントロールを参照することから始める必要があります。 この情報を選択したユーザーのユーザー名と共に使用して、`Roles` クラスの[`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx)または[`RemoveUserFromRole` メソッド](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)を使用して、ロールのユーザーを追加または削除します。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample11.vb)]

上のコードは、イベントを発生させたチェックボックスをプログラムによって参照することから始まります。これは、`sender` 入力パラメーターを通じて利用できます。 チェックボックスをオンにすると、選択したユーザーが指定したロールに追加されます。それ以外の場合は、ロールから削除されます。 どちらの場合も、`ActionStatus` ラベルには、実行されたアクションの概要を示したメッセージが表示されます。

ブラウザーでこのページをテストしてみましょう。 [ユーザー Tito] を選択してから、[管理者] ロールと [スーパーバイザー] ロールの両方に Tito を追加します。

[![Tito が Administrators ロールと監修者ロールに追加されました](assigning-roles-to-users-vb/_static/image8.png)](assigning-roles-to-users-vb/_static/image7.png)

**図 3**: [管理者] と [スーパーバイザー] のロールに Tito が追加されました ([クリックしてフルサイズの画像を表示し](assigning-roles-to-users-vb/_static/image9.png)ます)

次に、ドロップダウンリストから [ユーザー] を選択します。 ポストバックが存在し、リピータのチェックボックスが `CheckRolesForSelectedUser`によって更新されます。 まだロールに属していないため、2つのチェックボックスはオフになっています。 次に、監督者ロールにを追加します。

[![が監修者ロールに追加されました](assigning-roles-to-users-vb/_static/image11.png)](assigning-roles-to-users-vb/_static/image10.png)

**図 4**: スーパーバイザーロールに追加されました ([クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image12.png)されます)

`CheckRolesForSelectedUser` メソッドの機能をさらに確認するには、Tito またはをクリックしたユーザー以外のユーザーを選択します。 チェックボックスがどのロールにも属していないことを示すチェックボックスが自動的にオフになっていることに注意してください。 Tito に戻ります。 [管理者] チェックボックスと [スーパーバイザー] チェックボックスの両方をオンにする必要があります。

## <a name="step-2-building-the-by-roles-user-interface"></a>手順 2: "ロールによる" ユーザーインターフェイスの構築

この時点で、"ユーザー" インターフェイスが完成し、"ロール別" インターフェイスに取り組む準備が整いました。 "ロール別" インターフェイスは、ドロップダウンリストからロールを選択するようにユーザーに要求し、GridView でそのロールに属するユーザーのセットを表示します。

`UsersAndRoles.aspx page`に別の DropDownList コントロールを追加します。 Repeater コントロールの下に配置し、`RoleList`という名前を設定して、その `AutoPostBack` プロパティを True に設定します。 その下に、GridView を追加し、`RolesUserList`という名前を付けることができます。 この GridView には、選択したロールに属しているユーザーが一覧表示されます。 GridView の `AutoGenerateColumns` プロパティを False に設定し、グリッドの `Columns` コレクションに TemplateField を追加し、その `HeaderText` プロパティを "Users" に設定します。 TemplateField の `ItemTemplate` を定義して、`UserNameLabel`という名前のラベルの `Text` プロパティに `Container.DataItem` データバインド式の値が表示されるようにします。

GridView を追加して構成すると、"ロール別" インターフェイスの宣言型マークアップは次のようになります。

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample12.aspx)]

`RoleList` DropDownList にシステムの一連のロールを設定する必要があります。 これを実現するには、`BindRolesToList` メソッドを更新して、`Roles.GetAllRoles` メソッドによって返された文字列配列を `RolesList` DropDownList (および `UsersRoleList` リピータ) にバインドするようにします。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample13.vb)]

`BindRolesToList` メソッドの最後の2行が追加され、一連のロールを `RoleList` DropDownList コントロールにバインドするようになりました。 図5に、ブラウザーで表示した場合の最終的な結果を示します。このドロップダウンリストには、システムのロールが設定されています。

[ロールが RoleList DropDownList に表示さ ![](assigning-roles-to-users-vb/_static/image14.png)](assigning-roles-to-users-vb/_static/image13.png)

**図 5**: ロールが `RoleList` DropDownList に表示される ([クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image15.png)されます)

### <a name="displaying-the-users-that-belong-to-the-selected-role"></a>選択したロールに属するユーザーを表示する

ページが最初に読み込まれたとき、または `RoleList` DropDownList から新しいロールが選択されたときに、GridView でそのロールに属しているユーザーの一覧を表示する必要があります。 次のコードを使用して、`DisplayUsersBelongingToRole` という名前のメソッドを作成します。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample14.vb)]

このメソッドは、選択したロールを `RoleList` DropDownList から取得することによって開始します。 次に、 [`Roles.GetUsersInRole(roleName)` メソッド](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx)を使用して、そのロールに属するユーザーのユーザー名の文字列配列を取得します。 この配列は `RolesUserList` GridView にバインドされます。

このメソッドは、ページが最初に読み込まれたときと `RoleList` DropDownList で選択したロールが変更されたときの2つの状況で呼び出す必要があります。 したがって、`CheckRolesForSelectedUser`の呼び出しの後にこのメソッドが呼び出されるように、`Page_Load` イベントハンドラーを更新します。 次に、`RoleList`の `SelectedIndexChanged` イベントのイベントハンドラーを作成し、そこからこのメソッドを呼び出します。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample15.vb)]

このコードを配置すると、`RolesUserList` GridView には、選択したロールに属しているユーザーが表示されます。 図6に示すように、監修者ロールは2つのメンバーで構成されています。

[GridView に ![、選択したロールに属しているユーザーが一覧表示されます。](assigning-roles-to-users-vb/_static/image17.png)](assigning-roles-to-users-vb/_static/image16.png)

**図 6**: GridView には、選択したロールに属しているユーザーが一覧表示されます ([クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image18.png)されます)

### <a name="removing-users-from-the-selected-role"></a>選択したロールからユーザーを削除しています

`RolesUserList` GridView を拡張して、[削除] ボタンの列が含まれるようにしましょう。 特定のユーザーの [削除] ボタンをクリックすると、そのユーザーがそのロールから削除されます。

まず、GridView に [削除] ボタンフィールドを追加します。 このフィールドを一番左に表示されるようにして、その `DeleteText` プロパティを "Delete" (既定値) から "Remove" に変更します。

[![追加します。](assigning-roles-to-users-vb/_static/image20.png)](assigning-roles-to-users-vb/_static/image19.png)

**図 7**: GridView に [削除] ボタンを追加する ([クリックすると、フルサイズのイメージが表示](assigning-roles-to-users-vb/_static/image21.png)されます)

[Remove] ボタンをクリックすると、ポストバック ensues がクリックされ、GridView の `RowDeleting` イベントが発生します。 このイベントのイベントハンドラーを作成し、選択したロールからユーザーを削除するコードを記述する必要があります。 イベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample16.vb)]

このコードは、選択したロール名を決定することによって開始されます。 次に、削除するユーザーのユーザー名を決定するために [削除] ボタンがクリックされた行から、プログラムによって `UserNameLabel` コントロールを参照します。 次に、`Roles.RemoveUserFromRole` メソッドの呼び出しを使用して、ユーザーをロールから削除します。 `RolesUserList` GridView が更新され、`ActionStatus` Label コントロールを使用してメッセージが表示されます。

> [!NOTE]
> [削除] ボタンをクリックしても、ロールからユーザーを削除する前に、ユーザーからの確認は必要ありません。 いくつかのレベルのユーザー確認を追加するように依頼します。 アクションを確認する最も簡単な方法の1つは、クライアント側の [確認] ダイアログボックスを使用することです。 この手法の詳細については、「[削除時にクライアント側の確認を追加](https://asp.net/learn/data-access/tutorial-42-vb.aspx)する」を参照してください。

図8は、ユーザー Tito が監修者グループから削除された後のページを示しています。

[![悲しい、Tito は上司ではなくなりました。](assigning-roles-to-users-vb/_static/image23.png)](assigning-roles-to-users-vb/_static/image22.png)

**図 8**: 悲しい。 Tito は上司ではなくなりました ([クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image24.png)されます)

### <a name="adding-new-users-to-the-selected-role"></a>選択したロールに新しいユーザーを追加しています

選択したロールからユーザーを削除するだけでなく、このページのビジターは、選択したロールにユーザーを追加することもできます。 選択したロールにユーザーを追加するための最適なインターフェイスは、予想されるユーザーアカウントの数によって異なります。 Web サイトのユーザーアカウントが数十以下である場合は、DropDownList を使用できます。 数千人のユーザーアカウントがある場合は、ユーザーがアカウントを使用してページを表示したり、特定のアカウントを検索したり、他の方法でユーザーアカウントをフィルター処理したりすることを許可するユーザーインターフェイスを含めることができます。

このページでは、システム内のユーザーアカウントの数に関係なく機能する非常にシンプルなインターフェイスを使用します。 ここでは、テキストボックスを使用して、選択したロールに追加するユーザーのユーザー名を入力するようにビジターに要求します。 その名前のユーザーが存在しない場合、またはユーザーが既にロールのメンバーである場合、`ActionStatus` ラベルにメッセージが表示されます。 ただし、ユーザーが存在し、ロールのメンバーでない場合は、ロールに追加してグリッドを更新します。

GridView の下にテキストボックスとボタンを追加します。 テキストボックスの `ID` を `UserNameToAddToRole` に設定し、ボタンの `ID` および `Text` プロパティを `AddUserToRoleButton` に設定し、[ユーザーをロールに追加] をそれぞれ設定します。

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample17.aspx)]

次に、`AddUserToRoleButton` の `Click` イベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample18.vb)]

`Click` イベントハンドラーのコードの大部分は、さまざまな検証チェックを実行します。 これにより、ビジターが [`UserNameToAddToRole`] ボックスにユーザー名を入力したこと、ユーザーがシステムに存在すること、および選択したロールに属していないことが確認されます。 これらのチェックのいずれかが失敗すると、適切なメッセージが `ActionStatus` に表示され、イベントハンドラーが終了します。 すべてのチェックに合格した場合、ユーザーは `Roles.AddUserToRole` メソッドを使用してロールに追加されます。 その後、テキストボックスの `Text` プロパティがクリアされ、GridView が更新され、`ActionStatus` ラベルに、指定したユーザーが選択したロールに正常に追加されたことを示すメッセージが表示されます。

> [!NOTE]
> 指定されたユーザーがまだ選択されたロールに属していないことを確認するには、 [`Roles.IsUserInRole(userName, roleName)` メソッド](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)を使用します。このメソッドは、 *userName*が*roleName*のメンバーであるかどうかを示すブール値を返します。 このメソッドは、ロールベースの承認<a id="_msoanchor_2"></a>を確認するときに、[次のチュートリアル](role-based-authorization-vb.md)でもう一度使用します。

ブラウザーを使用してページを参照し、`RoleList` DropDownList からスーパーバイザーロールを選択します。 無効なユーザー名を入力してみてください。ユーザーがシステムに存在しないことを示すメッセージが表示されます。

[![存在しないユーザーをロールに追加することはできません](assigning-roles-to-users-vb/_static/image26.png)](assigning-roles-to-users-vb/_static/image25.png)

**図 9**: 存在しないユーザーをロールに追加することはできません ([クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image27.png)される)

次に、有効なユーザーを追加してみます。 先に進んで、"上司" ロールに追加します。

[![Tito はもう一度上司になります。](assigning-roles-to-users-vb/_static/image29.png)](assigning-roles-to-users-vb/_static/image28.png)

**図 10**: もう一度スーパーバイザーになる tito  ([クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image30.png)される)

## <a name="step-3-cross-updating-the-by-user-and-by-role-interfaces"></a>手順 3: "ユーザー" および "ロール別" のインターフェイスをクロス更新する

`UsersAndRoles.aspx` のページには、ユーザーとロールを管理するための2つの異なるインターフェイスが用意されています。 現時点では、これら2つのインターフェイスは相互に独立して動作するため、1つのインターフェイスで行われた変更がすぐには反映されない可能性があります。 たとえば、ページへの訪問者が `RoleList` DropDownList からスーパーバイザーロールを選択したとします。これは、メンバーとして表示されます。 次に、ビジターは `UserList` DropDownList から Tito を選択します。これにより、`UsersRoleList` リピータの [管理者] チェックボックスと [スーパーバイザー] チェックボックスがオンになります。 その後、訪問者がリピータからスーパーバイザーロールをオフにすると、スーパーバイザーロールから Tito が削除されますが、この変更は "ロールごと" のインターフェイスには反映されません。 GridView は、スーパーバイザーロールのメンバーであるとしても表示されます。

この問題を解決するには、`UsersRoleList` リピータからロールがオンまたはオフになったときに、GridView を更新する必要があります。 同様に、ユーザーが削除されるか、ロールに "by role" インターフェイスから追加されるたびに、リピータを更新する必要があります。

"ユーザー" インターフェイスのリピータは、`CheckRolesForSelectedUser` メソッドを呼び出すことによって更新されます。 "ロール別" インターフェイスは `RolesUserList` GridView の `RowDeleting` イベントハンドラーと、`AddUserToRoleButton` ボタンの `Click` イベントハンドラーで変更できます。 そのため、これらの各メソッドから `CheckRolesForSelectedUser` メソッドを呼び出す必要があります。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample19.vb)]

同様に、"by role" インターフェイスの GridView は、`DisplayUsersBelongingToRole` メソッドを呼び出すことによって更新され、"user" インターフェイスが `RoleCheckBox_CheckChanged` イベントハンドラーによって変更されます。 したがって、このイベントハンドラーから `DisplayUsersBelongingToRole` メソッドを呼び出す必要があります。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample20.vb)]

これらの軽微なコード変更により、"by user" インターフェイスと "role" インターフェイスが正常にクロス更新されるようになりました。 これを確認するには、ブラウザーを使用してページにアクセスし、[`UserList`] と [`RoleList`] の各リストから [Tito] と [スーパーバイザー] をそれぞれ選択します。 "ユーザー" インターフェイスでリピータから Tito のスーパーバイザーロールをオフにすると、"by role" インターフェイスの GridView から Tito が自動的に削除されることに注意してください。 "ロール別" インターフェイスからスーパーバイザーロールに Tito を追加すると、"ユーザー" インターフェイスのスーパーバイザーチェックボックスが自動的に再チェックされます。

## <a name="step-4-customizing-the-createuserwizard-to-include-a-specify-roles-step"></a>手順 4: "ロールの指定" 手順を含むように CreateUserWizard をカスタマイズする

<a id="_msoanchor_3"> </a>「[*ユーザーアカウントの作成*](../membership/creating-user-accounts-vb.md)」チュートリアルでは、CreateUserWizard Web コントロールを使用して、新しいユーザーアカウントを作成するためのインターフェイスを提供する方法を説明しました。 CreateUserWizard コントロールは、次の2つの方法のいずれかで使用できます。

- 訪問者がサイトで独自のユーザーアカウントを作成するための手段として、
- 管理者が新しいアカウントを作成するための手段として

最初のユースケースでは、ビジターはサイトに入力し、CreateUserWizard に入力して、サイトに登録するための情報を入力します。 2番目のケースでは、管理者が別のユーザーの新しいアカウントを作成します。

他のユーザーの管理者によってアカウントが作成されている場合は、新しいユーザーアカウントが属するロールを管理者が指定できるようにすると便利な場合があります。 <a id="_msoanchor_4"> </a> [ *追加のユーザー情報*の格納に関する](../membership/storing-additional-user-information-vb.md)チュートリアルでは、`WizardSteps`を追加して CreateUserWizard をカスタマイズする方法を説明しました。 新しいユーザーのロールを指定するために、CreateUserWizard に追加の手順を追加する方法を見てみましょう。

`CreateUserWizardWithRoles.aspx` ページを開き、`RegisterUserWithRoles`という名前の CreateUserWizard コントロールを追加します。 コントロールの `ContinueDestinationPageUrl` プロパティを "~/Default.aspx" に設定します。 ここでの考え方は、管理者がこの CreateUserWizard コントロールを使用して新しいユーザーアカウントを作成することであるため、コントロールの `LoginCreatedUser` プロパティを False に設定するということです。 この `LoginCreatedUser` プロパティは、ビジターが作成されたユーザーとして自動的にログオンするかどうかを指定します。既定値は True です。 管理者が新しいアカウントを作成するときに、サインインしたままにしておきたいので、False に設定します。

次に、[`WizardSteps`の追加と削除] を選択します。CreateUserWizard のスマートタグからオプションを選択し、新しい `WizardStep`を追加して、`ID` を `SpecifyRolesStep`に設定します。 "新しいアカウントにサインアップする" 手順の後、"Complete" 手順の前に、`SpecifyRolesStep WizardStep` を移動します。 `WizardStep`の `Title` プロパティを "Roles" を指定し、その `StepType` プロパティを `Step`に、その `AllowReturn` プロパティを False に設定します。

[![追加します。](assigning-roles-to-users-vb/_static/image32.png)](assigning-roles-to-users-vb/_static/image31.png)

**図 11**: [ロールの指定 `WizardStep`] を CreateUserWizard に追加する ([クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image33.png)されます)

この変更を行った後、CreateUserWizard の宣言型マークアップは次のようになります。

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample21.aspx)]

[ロールの指定] `WizardStep`で、`RoleList.` という名前の CheckBoxList を追加します。この CheckBoxList には、使用可能なロールが一覧表示され、ページにアクセスしたユーザーは、新しく作成されたユーザーが属するロールを確認できます。

ここでは、2つのコーディングタスクを行います。最初に、`RoleList` CheckBoxList にシステムのロールを設定する必要があります。次に、ユーザーが "ロールの指定" 手順から "完了" 手順に移動したときに、作成したユーザーを選択したロールに追加する必要があります。 `Page_Load` イベントハンドラーの最初のタスクを実行できます。 次のコードは、ページに最初にアクセスしたときに、`RoleList` チェックボックスをプログラムによって参照し、システム内のロールをバインドします。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample22.vb)]

上記のコードはよく知られています。 「 <a id="_msoanchor_5"> </a> [*追加のユーザー情報*の*格納*](../membership/storing-additional-user-information-vb.md) 」チュートリアルでは、2つの `FindControl` ステートメントを使用して、カスタム `WizardStep`内から Web コントロールを参照します。 ロールを CheckBoxList にバインドするコードは、このチュートリアルの前半で作成したものです。

2番目のプログラミングタスクを実行するには、"ロールの指定" 手順が完了したことを把握しておく必要があります。 CreateUserWizard には `ActiveStepChanged` イベントがあることを思い出してください。これは、ビジターがあるステップから別のステップに移動するたびに発生します。 ここで、ユーザーが "Complete" 手順に到達したかどうかを確認できます。その場合は、選択したロールにユーザーを追加する必要があります。

`ActiveStepChanged` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample23.vb)]

ユーザーが "Completed" 手順に到達した場合は、イベントハンドラーによって `RoleList` CheckBoxList の項目が列挙され、先ほど作成したユーザーが選択したロールに割り当てられます。

ブラウザーを使用してこのページにアクセスします。 CreateUserWizard の最初の手順は、新しいユーザーのユーザー名、パスワード、電子メール、その他の重要な情報の入力を求める標準の "新しいアカウントにサインアップする" 手順です。 情報を入力して、Wanda という名前の新しいユーザーを作成します。

[Wanda という名前の新しいユーザーを作成 ![には](assigning-roles-to-users-vb/_static/image35.png)](assigning-roles-to-users-vb/_static/image34.png)

**図 12**: Wanda という名前の新しいユーザーを作成[する (クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image36.png)される)

[Create User] \ (ユーザーの作成 \) ボタンをクリックします。 CreateUserWizard は、内部で `Membership.CreateUser` メソッドを呼び出し、新しいユーザーアカウントを作成した後、次の「ロールの指定」に進みます。 ここでは、システムの役割について説明します。 [スーパーバイザー] チェックボックスをオンにし、[次へ] をクリックします。

[Wanda をスーパーバイザーロールのメンバーにする ![](assigning-roles-to-users-vb/_static/image38.png)](assigning-roles-to-users-vb/_static/image37.png)

**図 13**: Wanda をスーパーバイザーロールのメンバーにする ([クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image39.png)されます)

[次へ] をクリックするとポストバックが実行され、`ActiveStep` が "Complete" 手順に更新されます。 `ActiveStepChanged` イベントハンドラーでは、最近作成されたユーザーアカウントがスーパーバイザーロールに割り当てられます。 これを確認するには、`UsersAndRoles.aspx` ページに戻り、`RoleList` DropDownList から [スーパーバイザー] を選択します。 図14に示すように、上司は、Wanda、Tito、およびの3人のユーザーで構成されています。

[Wanda、Tito、は全員が監督 ![](assigning-roles-to-users-vb/_static/image41.png)](assigning-roles-to-users-vb/_static/image40.png)

**図 14**: すべてのスーパーバイザーが表示されます ([クリックすると、フルサイズの画像が表示](assigning-roles-to-users-vb/_static/image42.png)されます)

## <a name="summary"></a>まとめ

ロールフレームワークには、特定のユーザーのロールに関する情報を取得するメソッドと、指定したロールに属するユーザーを決定するためのメソッドが用意されています。 さらに、1人以上のユーザーを1つ以上のロールに追加したり、削除したりするための方法がいくつかあります。 このチュートリアルでは、`AddUserToRole` と `RemoveUserFromRole`の2つの方法に焦点を絞っています。 1つのロールに複数のユーザーを追加し、1人のユーザーに複数のロールを割り当てるように設計された追加のバリエーションがあります。

このチュートリアルでは、新しく作成したユーザーのロールを指定する `WizardStep` を含むように、CreateUserWizard コントロールを拡張する方法についても説明しました。 このような手順は、管理者が新しいユーザーのユーザーアカウントを作成するプロセスを効率化するのに役立ちます。

この時点で、ロールを作成および削除する方法と、ロールにユーザーを追加および削除する方法を説明しました。 しかし、ロールベースの承認の適用についてはまだ説明していません。 <a id="_msoanchor_6"> </a>[次のチュートリアル](role-based-authorization-vb.md)では、ロールごとに URL 承認規則を定義すると共に、現在ログインしているユーザーのロールに基づいてページレベルの機能を制限する方法について説明します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET Web サイト管理ツールの概要](https://msdn.microsoft.com/library/ms228053.aspx)
- [ASP を調べています。NET のメンバーシップ、ロール、およびプロファイル](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [独自の Web サイト管理ツールのロール](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Teresa Murphy でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](creating-and-managing-roles-vb.md)
> [次へ](role-based-authorization-vb.md)

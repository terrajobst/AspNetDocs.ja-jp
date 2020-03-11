---
uid: web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-vb
title: ユーザーアカウントのロック解除と承認 (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、管理者がユーザーのロックアウトと承認済みの状態を管理するための web ページを構築する方法について説明します。 また、新しいユーザーを承認する方法についても説明します。
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 041854a5-ea8c-4de0-82f1-121ba6cb2893
msc.legacyurl: /web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-vb
msc.type: authoredcontent
ms.openlocfilehash: 4a7474676b8f502c583e226678de2b275e0ea3c7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517732"
---
# <a name="unlocking-and-approving-user-accounts-vb"></a>ユーザー アカウントをロック解除し、承認する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.14.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial14_UnlockAndApprove_vb.pdf)

> このチュートリアルでは、管理者がユーザーのロックアウトと承認済みの状態を管理するための web ページを構築する方法について説明します。 また、電子メールアドレスを確認した後にのみ、新しいユーザーを承認する方法についても説明します。

## <a name="introduction"></a>はじめに

ユーザー名、パスワード、および電子メールと共に、各ユーザーアカウントには、ユーザーがサイトにログインできるかどうかを指定する2つの状態フィールドがあります。ロックアウトされ、承認されています。 指定した分数内に無効な資格情報が指定した回数だけ提供された場合、ユーザーは自動的にロックアウトされます (既定の設定では、10分以内にログイン試行が5回失敗した後にユーザーがロックを解除します)。 承認済みの状態は、新しいユーザーがサイトにログオンする前に何らかのアクションを実行する必要がある場合に役立ちます。 たとえば、ユーザーは、最初に電子メールアドレスを確認するか、ログインする前に管理者によって承認される必要があります。

ロックアウトされたユーザーまたは未承認のユーザーがログインできないため、これらの状態をリセットする方法は自然なものになります。 ASP.NET には、ユーザーのロックアウトおよび承認済みの状態を管理するための組み込み機能や Web コントロールは含まれていません。これらの決定はサイトごとに処理する必要があるためです。 サイトによっては、すべての新しいユーザーアカウントが自動的に承認される場合があります (既定の動作)。 管理者が新しいアカウントを承認したり、サインアップ時に指定された電子メールアドレスに送信されたリンクにアクセスするまでユーザーを承認したりすることはできません。 同様に、一部のサイトでは、管理者が状態をリセットするまでユーザーがロックアウトされる場合がありますが、他のサイトでは、アカウントのロックを解除するためにアクセスできる URL を使用して、ロックアウトされたユーザーに電子メールが送信されます。

このチュートリアルでは、管理者がユーザーのロックアウトと承認済みの状態を管理するための web ページを構築する方法について説明します。 また、電子メールアドレスを確認した後にのみ、新しいユーザーを承認する方法についても説明します。

## <a name="step-1-managing-users-locked-out-and-approved-statuses"></a>手順 1:ユーザーのロックアウト状態と承認済み状態の管理

<a id="Tutorial12"> </a> [ *「多くのチュートリアルから1つのユーザーアカウントを選択するインターフェイスを構築する*](building-an-interface-to-select-one-user-account-from-many-vb.md)」では、ページ分割された GridView で各ユーザーアカウントを一覧表示するページを作成しています。 グリッドには、各ユーザーの名前と電子メール、承認およびロックアウトされた状態、現在オンラインになっているかどうか、およびユーザーに関するコメントが表示されます。 ユーザーの承認済みとロックアウト状態を管理するために、このグリッドを編集可能にすることができます。 ユーザーの承認済みの状態を変更するには、まず、管理者がユーザーアカウントを検索し、対応する GridView 行を編集して、[承認済み] チェックボックスをオンまたはオフにします。 または、別の ASP.NET ページを使用して、承認された状態とロックアウトされた状態を管理することもできます。

このチュートリアルでは、`ManageUsers.aspx` と `UserInformation.aspx`の2つの ASP.NET ページを使用します。 ここでの考え方は、`ManageUsers.aspx` はシステム内のユーザーアカウントを一覧表示しているのに対し、`UserInformation.aspx` では、管理者は特定のユーザーの承認済みおよびロックアウト状態を管理できます。 最初のビジネスの順序は、`ManageUsers.aspx` の GridView を拡張して、リンクの列として表示されるハイパーリンクフィールドを含めることです。 各リンクは `UserInformation.aspx?user=UserName`を指すようにします。 *UserName*は編集するユーザーの名前です。

> [!NOTE]
> 「 <a id="Tutorial13"> </a>[*パスワードの回復と変更*](recovering-and-changing-passwords-vb.md)」チュートリアルのコードをダウンロードした場合は、[`ManageUsers.aspx`] ページに "管理" リンクのセットが既に含まれており、[`UserInformation.aspx`] ページに、選択したユーザーのパスワードを変更するためのインターフェイスが用意されていることがわかります。 このチュートリアルに関連付けられているコードでは、この機能をレプリケートしないことにしました。これは、メンバーシップ API を回避し、SQL Server データベースを直接操作してユーザーのパスワードを変更することによって動作したためです。 このチュートリアルは、最初から `UserInformation.aspx` ページから開始します。

### <a name="adding-manage-links-to-theuseraccountsgridview"></a>`UserAccounts`GridView に "管理" リンクを追加する

[`ManageUsers.aspx`] ページを開き、[ハイパーリンク] フィールドを `UserAccounts` GridView に追加します。 [ハイパーリンク] フィールドの [`Text`] プロパティを "Manage" に設定し、その `DataNavigateUrlFields` と `DataNavigateUrlFormatString` のプロパティを `UserName` および "UserInformation .aspx? user ={0}" にそれぞれ設定します。 これらの設定は、すべてのハイパーリンクに "Manage" というテキストが表示されるように hyperlink フィールドを構成しますが、各リンクは、適切な*ユーザー名*の値を querystring に渡します。

[ハイパーリンク] フィールドを GridView に追加した後、ブラウザーを使用して `ManageUsers.aspx` ページを表示します。 図1に示すように、各 GridView 行には "Manage" リンクが含まれるようになりました。 の [管理] リンクは `UserInformation.aspx?user=Bruce`をポイントしますが、Dave の [管理] リンクを `UserInformation.aspx?user=Dave`します。

[ハイパーリンクフィールドに ![を追加すると、](unlocking-and-approving-user-accounts-vb/_static/image2.png)](unlocking-and-approving-user-accounts-vb/_static/image1.png)

**図 1**:[ハイパーリンク] フィールドには、ユーザーアカウントごとに "管理" リンクが追加されます ([クリックすると、フルサイズの画像が表示](unlocking-and-approving-user-accounts-vb/_static/image3.png)されます)。

ここでは、`UserInformation.aspx` ページのユーザーインターフェイスとコードを作成しますが、まず、ユーザーのロックアウト状態と承認済みの状態をプログラムで変更する方法について説明します。 [`MembershipUser` クラス](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)には、[`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx) プロパティと[`IsApproved` プロパティ](https://msdn.microsoft.com/library/system.web.security.membershipuser.isapproved.aspx)があります。 `IsLockedOut` プロパティは読み取り専用です。 プログラムによってユーザーをロックアウトするメカニズムはありません。ユーザーのロックを解除するには、`MembershipUser` クラスの[`UnlockUser` メソッド](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)を使用します。 `IsApproved` プロパティは読み取りと書き込みが可能です。 このプロパティに対する変更を保存するには、`Membership` クラスの[`UpdateUser` メソッド](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)を呼び出して、変更された `MembershipUser` オブジェクトを渡します。

`IsApproved` プロパティは読み取りと書き込みが可能であるため、CheckBox コントロールは、このプロパティを構成するための最適なユーザーインターフェイス要素として使用されることがあります。 ただし、管理者がユーザーをロックアウトすることはできず、ユーザーのロックを解除することはできないので、`IsLockedOut` プロパティではチェックボックスは機能しません。 `IsLockedOut` プロパティの適切なユーザーインターフェイスはボタンです。クリックすると、ユーザーアカウントのロックが解除されます。 このボタンは、ユーザーがロックアウトされている場合にのみ有効にする必要があります。

### <a name="creating-theuserinformationaspxpage"></a>`UserInformation.aspx`ページの作成

これで、`UserInformation.aspx`にユーザーインターフェイスを実装する準備が整いました。 このページを開き、次の Web コントロールを追加します。

- ハイパーリンクコントロール。クリックすると、管理者が [`ManageUsers.aspx`] ページに戻ります。
- 選択したユーザーの名前を表示するためのラベル Web コントロール。 このラベルの `ID` を `UserNameLabel` に設定し、Text プロパティをクリアします。
- `IsApproved`という名前の CheckBox コントロール。 `AutoPostBack` プロパティを `True`に設定します。
- ユーザーの最後のロックアウト日を表示するためのラベルコントロール。 このラベルに `LastLockedOutDateLabel` という名前を付け、その `Text` プロパティをオフにします。
- ユーザーのロックを解除するためのボタン。 このボタン `UnlockUserButton` という名前を指定し、その `Text` プロパティを "Unlock User" に設定します。
- "ユーザーの承認された状態は更新されました。" などのステータスメッセージを表示するためのラベルコントロール。 このコントロールに `StatusMessage`という名前を設定し、その `Text` プロパティをオフにして、その `CssClass` プロパティを `Important`に設定します。 (`Important` CSS クラスは、`Styles.css` スタイルシートファイルで定義されています。これにより、対応するテキストが大きな赤いフォントで表示されます)。

これらのコントロールを追加した後、Visual Studio のデザインビューは、図2のスクリーンショットのようになります。

[UserInformation .aspx 用のユーザーインターフェイスを作成 ![には](unlocking-and-approving-user-accounts-vb/_static/image5.png)](unlocking-and-approving-user-accounts-vb/_static/image4.png)

**図 2**:`UserInformation.aspx` 用のユーザーインターフェイスを作成[します (クリックすると、フルサイズの画像が表示](unlocking-and-approving-user-accounts-vb/_static/image6.png)されます)

ユーザーインターフェイスが完成したら、次に、選択したユーザーの情報に基づいて `IsApproved` チェックボックスとその他のコントロールを設定します。 ページの `Load` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample1.vb)]

上記のコードは、最初にページにアクセスし、次のポストバックではないことを確認することから始まります。 次に、`user` querystring フィールドを通じて渡されたユーザー名を読み取り、`Membership.GetUser(username)` メソッドを使用してそのユーザーアカウントに関する情報を取得します。 Querystring でユーザー名が指定されなかった場合、または指定されたユーザーが見つからなかった場合は、管理者が `ManageUsers.aspx` ページに戻されます。

`MembershipUser` オブジェクトの `UserName` 値が `UserNameLabel` に表示され、`IsApproved` プロパティ値に基づいて `IsApproved` チェックボックスがオンになります。

`MembershipUser` オブジェクトの[`LastLockoutDate` プロパティ](https://msdn.microsoft.com/library/system.web.security.membershipuser.lastlockoutdate.aspx)は、ユーザーが最後にロックアウトされた日時を示す `DateTime` 値を返します。ユーザーがロックアウトされていない場合、返される値はメンバーシッププロバイダーによって異なります。 新しいアカウントを作成すると、`SqlMembershipProvider` によって `aspnet_Membership` テーブルの `LastLockoutDate` フィールドが `1754-01-01 12:00:00 AM`に設定されます。 上のコードでは、`LastLockoutDate` プロパティが2000年の前に発生した場合、`LastLockoutDateLabel` に空の文字列が表示されます。それ以外の場合は、`LastLockoutDate` プロパティの日付部分がラベルに表示されます。 `UnlockUserButton`の `Enabled` プロパティは、ユーザーのロックアウト状態に設定されます。つまり、このボタンは、ユーザーがロックアウトされている場合にのみ有効になります。

ブラウザーを使用して `UserInformation.aspx` のページをテストしてみましょう。 もちろん、`ManageUsers.aspx` で開始し、管理するユーザーアカウントを選択する必要があります。 `UserInformation.aspx`に到着すると、[`IsApproved`] チェックボックスは、ユーザーが承認されている場合にのみチェックされることに注意してください。 ユーザーがロックアウトされている場合は、最後のロックアウト日が表示されます。 [ユーザーのロック解除] ボタンは、ユーザーが現在ロックアウトされている場合にのみ有効になります。`IsApproved` チェックボックスをオンまたはオフにして [ユーザーのロック解除] ボタンをクリックすると、ポストバックが発生しますが、これらのイベントのイベントハンドラーをまだ作成していないため、ユーザーアカウントに変更は加えられません。

Visual Studio に戻り、`IsApproved` CheckBox の `CheckedChanged` イベントと、`UnlockUser` ボタンの `Click` イベントのイベントハンドラーを作成します。 `CheckedChanged` イベントハンドラーで、ユーザーの `IsApproved` プロパティをチェックボックスの `Checked` プロパティに設定し、`Membership.UpdateUser`の呼び出しを使用して変更を保存します。 `Click` イベントハンドラーでは、`MembershipUser` オブジェクトの `UnlockUser` メソッドを呼び出すだけです。 両方のイベントハンドラーで、`StatusMessage` ラベルに適切なメッセージを表示します。

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample2.vb)]

### <a name="testing-theuserinformationaspxpage"></a>`UserInformation.aspx`ページのテスト

これらのイベントハンドラーを使用して、ページを再実行し、ユーザーを未承認にします。 図3に示すように、ページには、ユーザーの `IsApproved` プロパティが正常に変更されたことを示す簡単なメッセージが表示されます。

[Chris が承認されていない ![](unlocking-and-approving-user-accounts-vb/_static/image8.png)](unlocking-and-approving-user-accounts-vb/_static/image7.png)

**図 3**:Chris が未承認になりました ([クリックすると、フルサイズの画像が表示](unlocking-and-approving-user-accounts-vb/_static/image9.png)されます)

次に、ログアウトして、アカウントが承認されていないユーザーとしてログインします。 ユーザーは承認されていないため、ログインできません。 既定では、ログイン制御は、理由に関係なく、ユーザーがログインできない場合、同じメッセージを表示します。 ただし、 <a id="Tutorial6"> </a>[*メンバーシップユーザーストアに対するユーザー資格情報の検証*](../membership/validating-user-credentials-against-the-membership-user-store-vb.md)に関するチュートリアルでは、より適切なメッセージを表示するように、ログインコントロールを拡張する方法を検討しました。 図4に示すように、Chris には、アカウントがまだ承認されていないためにログインできないことを示すメッセージが表示されています。

[アカウントが承認されていないため、Chris がログインできない ![](unlocking-and-approving-user-accounts-vb/_static/image11.png)](unlocking-and-approving-user-accounts-vb/_static/image10.png)

**図 4**:アカウントが承認されていないため、Chris はログインできません ([クリックすると、フルサイズの画像が表示](unlocking-and-approving-user-accounts-vb/_static/image12.png)されます)

ロックアウトされた機能をテストするには、承認されたユーザーとしてログインを試みますが、正しくないパスワードを使用します。 ユーザーのアカウントがロックアウトされるまで、必要な回数だけこのプロセスを繰り返します。ロックアウトされたアカウントからログインしようとすると、カスタムメッセージを表示するように Login コントロールも更新されました。 ログインページで次のメッセージが表示されると、アカウントがロックアウトされていることがわかります。"無効なログイン試行回数が多すぎるため、アカウントがロックアウトされました。 アカウントのロックを解除するには、管理者にお問い合わせください。 "

`ManageUsers.aspx` ページに戻り、ロックアウトされたユーザーの [管理] リンクをクリックします。 図5に示すように、[ユーザーのロック解除] ボタンが有効になっている `LastLockedOutDateLabel` に値が表示されます。 ユーザーアカウントのロックを解除するには、[ユーザーのロック解除] ボタンをクリックします。 ユーザーのロックを解除すると、再度ログインできるようになります。

[![Dave がシステムからロックアウトされました](unlocking-and-approving-user-accounts-vb/_static/image14.png)](unlocking-and-approving-user-accounts-vb/_static/image13.png)

**図 5**:Dave がシステムからロックアウトされました ([クリックすると、フルサイズの画像が表示](unlocking-and-approving-user-accounts-vb/_static/image15.png)されます)

## <a name="step-2-specifying-new-users-approved-status"></a>手順 2:新しいユーザーの承認済み状態の指定

承認済みの状態は、新しいユーザーがサイトのユーザー固有の機能にログインしてアクセスできるようにするために、何らかのアクションを実行する必要がある場合に便利です。 たとえば、プライベート web サイトを実行していて、ログインページとサインアップページを除くすべてのページが、認証されたユーザーのみがアクセスできるようにすることができます。 しかし、ユーザーが web サイトに到達し、サインアップページを検索して、アカウントを作成した場合はどうなるでしょうか。 この問題を回避するには、サインアップページを `Administration` フォルダーに移動し、管理者が各アカウントを手動で作成する必要があります。 または、すべてのユーザーにサインアップを許可し、管理者がユーザーアカウントを承認するまでサイトアクセスを禁止することもできます。

既定では、CreateUserWizard コントロールは新しいアカウントを承認します。 この動作は、コントロールの[`DisableCreatedUser` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)を使用して構成できます。 新しいユーザーアカウントを承認しないようにするには、このプロパティを `True` に設定します。

> [!NOTE]
> 既定では、CreateUserWizard コントロールは新しいユーザーアカウントに自動的にログオンします。 この動作は、コントロールの[`LoginCreatedUser` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)によって決まります。 未承認のユーザーがサイトにログインできないため、`DisableCreatedUser` が `True` 場合、`LoginCreatedUser` プロパティの値に関係なく、新しいユーザーアカウントはサイトにログインしません。

`Membership.CreateUser` メソッドを使用してプログラムによって新しいユーザーアカウントを作成する場合、未承認のユーザーアカウントを作成するには、新しいユーザーの `IsApproved` プロパティ値を入力パラメーターとして受け取るオーバーロードのいずれかを使用します。

## <a name="step-3-approving-users-by-verifying-their-email-address"></a>手順 3:電子メールアドレスを確認してユーザーを承認する

ユーザーアカウントをサポートする多くの web サイトは、登録時に指定した電子メールアドレスを確認するまで、新しいユーザーを承認しません。 この検証プロセスは、ボット、スパム送信者、およびその他の neer を阻止するためによく使用されます。これは、一意で検証された電子メールアドレスが必要であり、サインアッププロセスに追加の手順が追加されるためです。 このモデルでは、新しいユーザーがサインアップすると、確認ページへのリンクを含む電子メールメッセージが送信されます。 このリンクにアクセスすることで、ユーザーは電子メールを受信したことがわかっているので、指定された電子メールアドレスが有効であることが証明されます。 検証ページは、ユーザーを承認する役割を担います。 これは自動的に発生し、このページに到達したユーザーを承認するか、ユーザーが[CAPTCHA](http://en.wikipedia.org/wiki/Captcha)などの追加情報を提供した後にのみ承認されます。

このワークフローに対応するには、最初にアカウント作成ページを更新して、新しいユーザーが承認されないようにする必要があります。 `Membership` フォルダーの [`EnhancedCreateUserWizard.aspx`] ページを開き、CreateUserWizard コントロールの `DisableCreatedUser` プロパティを [`True`] に設定します。

次に、新しいユーザーに電子メールを送信するように CreateUserWizard コントロールを構成し、アカウントを確認する方法を説明します。 特に、`Verification.aspx` ページ (まだ作成していません) へのリンクを電子メールに含め、新しいユーザーの `UserId` を querystring で渡します。 `Verification.aspx` ページでは、指定されたユーザーを検索し、承認済みとしてマークします。

### <a name="sending-a-verification-email-to-new-users"></a>新しいユーザーに確認メールを送信する

CreateUserWizard コントロールから電子メールを送信するには、その `MailDefinition` プロパティを適切に構成します。 <a id="Tutorial13"> </a>[前のチュートリアル](recovering-and-changing-passwords-vb.md)で説明したように、ChangePassword および passwordrecovery コントロールには、CreateUserWizard コントロールのと同じ方法で動作する[`MailDefinition` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx)が含まれています。

> [!NOTE]
> `MailDefinition` プロパティを使用するには、`Web.config`でメール配信オプションを指定する必要があります。 詳細については、「 [ASP.NET での電子メールの送信」](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)を参照してください。

まず、`EmailTemplates` フォルダーに `CreateUserWizard.txt` という名前の新しい電子メールテンプレートを作成します。 テンプレートには、次のテキストを使用します。

[!code-aspx[Main](unlocking-and-approving-user-accounts-vb/samples/sample3.aspx)]

`MailDefinition`の `BodyFileName` プロパティを "~/EmailTemplates/CreateUserWizard.txt" に設定し、その `Subject` プロパティを [My Web サイトへようこそ] に設定します。 アカウントをアクティブ化してください。 "

`CreateUserWizard.txt` 電子メールテンプレートには、`<%VerificationUrl%>` プレースホルダーが含まれていることに注意してください。 ここで、`Verification.aspx` ページの URL が配置されます。 CreateUserWizard は、`<%UserName%>` と `<%Password%>` のプレースホルダーを新しいアカウントのユーザー名とパスワードに自動的に置き換えますが、組み込みの `<%VerificationUrl%>` プレースホルダーはありません。 適切な検証 URL に手動で置き換える必要があります。

これを実現するには、CreateUserWizard の[`SendingMail` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.sendingmail.aspx)のイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample4.vb)]

`SendingMail` イベントは、`CreatedUser` イベントの後に発生します。つまり、上記のイベントハンドラーが実行されたときに、新しいユーザーアカウントが既に作成されていることを意味します。 新しいユーザーの `UserId` 値にアクセスするには、`Membership.GetUser` メソッドを呼び出し、CreateUserWizard コントロールに入力した `UserName` を渡します。 次に、検証 URL が形成されます。 ステートメント `Request.Url.GetLeftPart(UriPartial.Authority)` は、URL の `http://yourserver.com` の部分を返します。`Request.ApplicationPath` は、アプリケーションがルートとするパスを返します。 検証 URL が `Verification.aspx?ID=userId`として定義されます。 この2つの文字列は、完全な URL を形成するために連結されます。 最後に、電子メールメッセージの本文 (`e.Message.Body`) には、すべての `<%VerificationUrl%>` が完全な URL で置き換えられます。

実質的な効果は、新しいユーザーが未承認であることです。つまり、サイトにログインすることはできません。 さらに、確認 URL へのリンクを含む電子メールが自動的に送信されます (図6を参照)。

[新しいユーザーが、確認 URL へのリンクを含む電子メールを受信 ![](unlocking-and-approving-user-accounts-vb/_static/image17.png)](unlocking-and-approving-user-accounts-vb/_static/image16.png)

**図 6**:新しいユーザーは、確認 URL へのリンクを含む電子メールを受信します ([クリックすると、フルサイズの画像が表示](unlocking-and-approving-user-accounts-vb/_static/image18.png)されます)

> [!NOTE]
> CreateUserWizard コントロールの既定の CreateUserWizard ステップでは、ユーザーにアカウントが作成されたことを知らせるメッセージが表示され、[続行] ボタンが表示されます。 このボタンをクリックすると、ユーザーはコントロールの `ContinueDestinationPageUrl` プロパティによって指定された URL に移動します。 `EnhancedCreateUserWizard.aspx` の CreateUserWizard は、新しいユーザーを `~/Membership/AdditionalUserInfo.aspx`に送信するように構成されています。これにより、ユーザーは自分の故郷、ホームページの URL、署名を求められます。 この情報は、ログオンしているユーザーのみが追加できるため、このプロパティを更新して、ユーザーをサイトのホームページ (`~/Default.aspx`) に戻すことができます。 さらに、[`EnhancedCreateUserWizard.aspx`] ページまたは CreateUserWizard 手順は、確認メールが送信されたことをユーザーに通知するように拡張する必要があります。また、そのアカウントは、この電子メールの指示に従うまでライセンス認証されません。 これらの変更は、読者のための演習として残しておきます。

### <a name="creating-the-verification-page"></a>検証ページの作成

最後に、`Verification.aspx` ページを作成します。 このページをルートフォルダーに追加し、`Site.master` マスターページに関連付けます。 前に説明したコンテンツページのほとんどがサイトに追加されたので、コンテンツページがマスターページの既定のコンテンツを使用するように、`LoginContent` ContentPlaceHolder を参照するコンテンツコントロールを削除します。

[`Verification.aspx`] ページに [ラベル] Web コントロールを追加し、その `ID` を `StatusMessage` に設定して、[text] プロパティをオフにします。 次に、`Page_Load` イベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample5.vb)]

上記のコードの大部分では、querystring によって指定された UserId が存在すること、有効な `Guid` 値であること、および既存のユーザーアカウントを参照していることを確認します。 これらすべてのチェックに合格すると、ユーザーアカウントは承認されます。それ以外の場合は、適切なステータスメッセージが表示されます。

図7は、ブラウザーを使用してアクセスしたときの `Verification.aspx` ページを示しています。

[新しいユーザーのアカウントが承認された ![](unlocking-and-approving-user-accounts-vb/_static/image20.png)](unlocking-and-approving-user-accounts-vb/_static/image19.png)

**図 7**:新しいユーザーのアカウントが承認されました ([クリックすると、フルサイズの画像が表示](unlocking-and-approving-user-accounts-vb/_static/image21.png)されます)

## <a name="summary"></a>まとめ

すべてのメンバーシップユーザーアカウントには、ユーザーがサイトにログインできるかどうかを決定する2つの状態があります。 `IsLockedOut` と `IsApproved`です。 ユーザーがログインするには、これらのプロパティの両方を `True` する必要があります。

ユーザーのロックアウト状態はセキュリティ対策として使用されます。これは、ブルートフォース方式によって、ハッカーがサイトに侵入する可能性を低減するためです。 具体的には、一定の時間内に無効なログイン試行回数があると、ユーザーはロックアウトされます。 これらの境界は、`Web.config`のメンバーシッププロバイダー設定を使用して構成できます。

承認済みの状態は、一部のアクションが発生するまで、新しいユーザーがログインできないようにする手段としてよく使用されます。 サイトでは、最初に管理者が新しいアカウントを承認する必要があります。または、手順3で見たように、電子メールアドレスを確認してください。

プログラミングを楽しんでください。

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](recovering-and-changing-passwords-vb.md)

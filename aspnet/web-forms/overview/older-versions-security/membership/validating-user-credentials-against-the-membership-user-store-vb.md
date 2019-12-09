---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
title: メンバーシップユーザーストアに対してユーザー資格情報を検証する (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、プログラムによる方法とログイン制御の両方を使用して、メンバーシップユーザーストアに対してユーザーの資格情報を検証する方法について説明します。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 17772912-b47b-4557-9ce9-80f22df642f7
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
msc.type: authoredcontent
ms.openlocfilehash: 37574e4cdc86f518d01d12da58cc2862bc77d463
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74643209"
---
# <a name="validating-user-credentials-against-the-membership-user-store-vb"></a>メンバーシップ ユーザー ストアに対してユーザー資格情報を確認する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_VB.zip)または[PDF のダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_vb.pdf)

> このチュートリアルでは、プログラムによる方法とログイン制御の両方を使用して、メンバーシップユーザーストアに対してユーザーの資格情報を検証する方法について説明します。 また、ログインコントロールの外観と動作をカスタマイズする方法についても説明します。

## <a name="introduction"></a>はじめに

前の<a id="Tutorial05"> </a>[チュートリアル](creating-user-accounts-vb.md)では、メンバーシップフレームワークで新しいユーザーアカウントを作成する方法について説明しました。 まず、プログラムで `Membership` クラスの `CreateUser` メソッドを使用してユーザーアカウントを作成し、次に CreateUserWizard Web コントロールを使用して検証しました。 ただし、ログインページでは、指定された資格情報が、ハードコーディングされたユーザー名とパスワードの組み合わせに対して現在検証されています。 メンバーシップフレームワークのユーザーストアに対して資格情報を検証するために、ログインページのロジックを更新する必要があります。

ユーザーアカウントの作成と同様に、資格情報はプログラムによって、または宣言によって検証できます。 メンバーシップ API には、ユーザーストアに対してユーザーの資格情報をプログラムによって検証するためのメソッドが含まれています。 と ASP.NET には、ログイン Web コントロールが付属しています。これにより、ユーザー名とパスワードのテキストボックスとログインするボタンを含むユーザーインターフェイスがレンダリングされます。

このチュートリアルでは、プログラムによる方法とログイン制御の両方を使用して、メンバーシップユーザーストアに対してユーザーの資格情報を検証する方法について説明します。 また、ログインコントロールの外観と動作をカスタマイズする方法についても説明します。 では、始めましょう。

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>手順 1: メンバーシップユーザーストアに対して資格情報を検証する

フォーム認証を使用する web サイトの場合、ユーザーはログインページにアクセスして資格情報を入力することで、web サイトにログオンします。 これらの資格情報は、ユーザーストアと比較されます。 有効な場合、ユーザーにはフォーム認証チケットが付与されます。これは、ビジターの id と信頼性を示すセキュリティトークンです。

メンバーシップフレームワークに対してユーザーを検証するには、`Membership` クラスの[`ValidateUser` メソッド](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)を使用します。 `ValidateUser` メソッドは、`username` と `password` の2つの入力パラメーターを受け取り、資格情報が有効であるかどうかを示すブール値を返します。 前のチュートリアルで調べた `CreateUser` メソッドと同様に、`ValidateUser` メソッドは、構成されたメンバーシッププロバイダーに実際の検証を委任します。

`SqlMembershipProvider` は、指定されたユーザーのパスワードを `aspnet_Membership_GetPasswordWithFormat` ストアドプロシージャを使用して取得することによって、指定された資格情報を検証します。 `SqlMembershipProvider` には、クリア、暗号化、またはハッシュされた3つの形式のいずれかを使用してユーザーのパスワードが格納されていることを思い出してください。 `aspnet_Membership_GetPasswordWithFormat` ストアドプロシージャは、パスワードを未加工の形式で返します。 暗号化またはハッシュされたパスワードの場合、`SqlMembershipProvider` は `ValidateUser` メソッドに渡された `password` 値を、それと等価な暗号化またはハッシュされた状態に変換し、データベースから返された値と比較します。 データベースに格納されているパスワードが、ユーザーが入力した書式設定されたパスワードと一致する場合、資格情報は有効です。

メンバーシップフレームワークのユーザーストアに対して指定された資格情報を検証するように、ログインページ (~/`Login.aspx`) を更新してみましょう。 このログインページは、 <a id="Tutorial02"> </a> [ *「フォーム認証の概要」* ](../introduction/an-overview-of-forms-authentication-vb.md)チュートリアルで作成したもので、[ユーザー名] と [パスワード] の2つのテキストボックス、[覚えてください] チェックボックス、[ログイン] ボタン (図1を参照) を使用してインターフェイスを作成しています。 このコードは、入力された資格情報を、ユーザー名とパスワードのペア (Scott/password、Jisun/password、および Sam/password) のハードコーディングされたリストと照合して検証します。 <a id="Tutorial03"> </a>[*フォーム認証構成と高度なトピック*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)のチュートリアルでは、フォーム認証チケットの `UserData` プロパティに追加情報を格納するために、ログインページのコードを更新しました。

[ログインページのインターフェイスに、2つのテキストボックス、CheckBoxList、およびボタンが含まれている ![](validating-user-credentials-against-the-membership-user-store-vb/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image1.png)

**図 1**: ログインページのインターフェイスには、2つのテキストボックス、CheckBoxList、ボタンが含まれています ([クリックすると、フルサイズの画像が表示](validating-user-credentials-against-the-membership-user-store-vb/_static/image3.png)されます)

ログインページのユーザーインターフェイスは変更されませんが、ログインボタンの `Click` イベントハンドラーを、メンバーシップフレームワークのユーザーストアに対してユーザーを検証するコードに置き換える必要があります。 イベントハンドラーを次のように更新します。

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample1.vb)]

このコードは非常に単純です。 まず、`Membership.ValidateUser` メソッドを呼び出して、指定されたユーザー名とパスワードを渡します。 このメソッドが True を返す場合、ユーザーは `FormsAuthentication` クラスの RedirectFromLoginPage メソッドを使用してサイトにサインインします。 ( <a id="Tutorial02"> </a> [ *「フォーム認証の概要*](../introduction/an-overview-of-forms-authentication-vb.md)」チュートリアルで説明したように、`FormsAuthentication.RedirectFromLoginPage` はフォーム認証チケットを作成し、ユーザーを適切なページにリダイレクトします)。ただし、資格情報が無効な場合は、ユーザー名またはパスワードが間違っていることを知らせる `InvalidCredentialsMessage` ラベルが表示されます。

必要な作業は以上です。

ログインページが想定どおりに動作することをテストするには、前のチュートリアルで作成したユーザーアカウントのいずれかでログインを試みます。 または、まだアカウントを作成していない場合は、[`~/Membership/CreatingUserAccounts.aspx`] ページからアカウントを作成します。

> [!NOTE]
> ユーザーが資格情報を入力し、ログインページフォームを送信すると、パスワードを含む資格情報がインターネット経由で*プレーンテキスト*で web サーバーに送信されます。 つまり、ハッカーがネットワークトラフィックをスニッフィングすると、ユーザー名とパスワードが表示されます。 これを回避するには、 [SSL (Secure Socket layer)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)を使用してネットワークトラフィックを暗号化することが不可欠です。 これにより、資格情報 (ページ全体の HTML マークアップ) が web サーバーによって受信されるまでブラウザーを離れた時点から暗号化されるようになります。

### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>メンバーシップフレームワークが無効なログイン試行を処理する方法

ビジターがログインページに到達し、資格情報を送信すると、ブラウザーはログインページに HTTP 要求を行います。 資格情報が有効な場合、HTTP 応答には、cookie 内の認証チケットが含まれます。 したがって、ハッカーがサイトに侵入しようとすると、有効なユーザー名とパスワードで推測されたパスワードを使用して、ログインページに HTTP 要求を徹底的に送信するプログラムが作成される可能性があります。 パスワードの推定値が正しい場合、ログインページは認証チケットクッキーを返します。これは、プログラムが有効なユーザー名とパスワードの組み合わせで偶然していることを認識しています。 ブルートフォース攻撃によって、このようなプログラムは、特にパスワードが脆弱な場合に、ユーザーのパスワードを遭遇ことができる可能性があります。

このようなブルートフォース攻撃を防ぐために、特定の期間内にログイン試行が何回も失敗した場合に、メンバーシップフレームワークによってユーザーがロックアウトされます。 正確なパラメーターは、次の2つのメンバーシッププロバイダーの構成設定を使用して構成できます。

- `maxInvalidPasswordAttempts`-アカウントがロックアウトされるまでにユーザーが使用できる無効なパスワードの試行回数を指定します。既定値は5です。
- `passwordAttemptWindow`-指定した回数の無効なログイン試行によってアカウントがロックアウトされる期間を分単位で示します。既定値は10です。

ユーザーがロックアウトされている場合は、管理者が自分のアカウントのロックを解除するまでログインできません。 ユーザーがロックアウトされると、`ValidateUser` メソッドは、有効な資格情報が指定されている場合でも、*常に*`False`を返します。 この動作によって、ハッカーがブルートフォース方式を使用してサイトに侵入する可能性が低くなりますが、パスワードを忘れた場合、または誤って入力された日付が間違っていた場合は、有効なユーザーがロックアウトされる可能性があります。

残念ながら、ユーザーアカウントのロックを解除するための組み込みツールはありません。 アカウントのロックを解除するには、データベースを直接変更して、適切なユーザーアカウントの `aspnet_Membership` テーブルの [`IsLockedOut`] フィールドを変更するか、ロックアウトされたアカウントのロック解除オプションを含む web ベースのインターフェイスを作成します。 この後のチュートリアルでは、一般的なユーザーアカウントとロールに関連するタスクを実行するための管理インターフェイスの作成について説明します。

> [!NOTE]
> `ValidateUser` メソッドの欠点の1つは、指定された資格情報が無効な場合に、その理由を説明するものではないということです。 ユーザーストアに一致するユーザー名とパスワードのペアがないか、ユーザーがまだ承認されていないか、ユーザーがロックアウトされているため、資格情報が無効になっている可能性があります。手順 4. では、ログイン試行が失敗したときに、より詳細なメッセージをユーザーに表示する方法を説明します。

## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>手順 2: ログイン Web コントロールを使用して資格情報を収集する

[ログイン Web コントロール](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)は、 <a id="Tutorial02"> </a> [ *「フォーム認証の概要」* ](../introduction/an-overview-of-forms-authentication-vb.md)チュートリアルで作成したものとよく似た既定のユーザーインターフェイスをレンダリングします。 ログインコントロールを使用すると、ユーザーの資格情報を収集するためのインターフェイスを作成する作業が保存されます。 さらに、ログインコントロールは、(送信された資格情報が有効であることを前提として) ユーザーに自動的にサインインするため、コードを記述する必要がなくなります。

`Login.aspx`を更新して、手動で作成したインターフェイスとコードをログインコントロールに置き換えてみましょう。 まず、`Login.aspx`の既存のマークアップとコードを削除します。 完全に削除することも、単にコメントアウトすることもできます。宣言型マークアップをコメントアウトするには、`<%--` と `--%>` 区切り記号で囲みます。 これらの区切り記号を手動で入力することも、図2に示すように、コメントアウトするテキストを選択してから、ツールバーの [選択した行をコメントアウトする] アイコンをクリックすることもできます。 同様に、[選択した行をコメントアウトする] アイコンを使用して、分離コードクラスで選択されているコードをコメントアウトすることもできます。

[![既存の宣言型マークアップと login.aspx のソースコードをコメントアウトします。](validating-user-credentials-against-the-membership-user-store-vb/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image4.png)

**図 2**: Login.aspx の既存の宣言型マークアップとソースコードをコメントアウト[する (クリックしてフルサイズのイメージを表示する](validating-user-credentials-against-the-membership-user-store-vb/_static/image6.png))

> [!NOTE]
> Visual Studio 2005 で宣言マークアップを表示する場合、[選択した行をコメントアウトする] アイコンは使用できません。 Visual Studio 2008 を使用していない場合は、`<%--` と `--%>` 区切り記号を手動で追加する必要があります。

次に、ツールボックスからログインコントロールをページにドラッグし、その `ID` プロパティを `myLogin`に設定します。 この時点で、画面は図3のようになります。 Login コントロールの既定のインターフェイスには、[ユーザー名とパスワード]、[次回に記憶する] チェックボックス、[ログイン] ボタンのテキストボックスコントロールが含まれていることに注意してください。 2つのテキストボックスには、`RequiredFieldValidator` コントロールもあります。

[ログインコントロールをページに追加 ![には](validating-user-credentials-against-the-membership-user-store-vb/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image7.png)

**図 3**: ログインコントロールをページに追加する ([クリックすると、フルサイズの画像が表示](validating-user-credentials-against-the-membership-user-store-vb/_static/image9.png)されます)

これで完了です。 ログインコントロールの [ログイン] ボタンをクリックすると、ポストバックが発生し、ログインコントロールは、入力したユーザー名とパスワードを渡して `Membership.ValidateUser` メソッドを呼び出します。 資格情報が無効な場合、ログインコントロールには、そのようなメッセージが表示されます。 ただし、資格情報が有効な場合、ログイン制御によってフォーム認証チケットが作成され、ユーザーが適切なページにリダイレクトされます。

ログイン制御では、次の4つの要素を使用して、ログインが成功したときにユーザーをリダイレクトするための適切なページを決定します。

- フォーム認証構成の `loginUrl` 設定によって定義されたログインページにログイン制御があるかどうか。この設定の既定値は `Login.aspx`
- `ReturnUrl` querystring パラメーターの存在
- ログインコントロールの[`DestinationUrl` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx)の値
- フォーム認証構成設定で指定された `defaultUrl` 値。この設定の既定値は default.aspx です。

図4は、ログインコントロールがこれら4つのパラメーターを使用して、適切なページの決定に到達する方法を示しています。

[ログインコントロールをページに追加 ![には](validating-user-credentials-against-the-membership-user-store-vb/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image10.png)

**図 4**: ログインコントロールをページに追加する ([クリックすると、フルサイズの画像が表示](validating-user-credentials-against-the-membership-user-store-vb/_static/image12.png)されます)

ブラウザーを使用してサイトにアクセスし、メンバーシップフレームワークの既存のユーザーとしてログインして、ログイン制御をテストしてみましょう。

ログインコントロールの表示インターフェイスは、高度な構成が可能です。 外観に影響を与えるプロパティがいくつかあります。さらに、ユーザーインターフェイス要素のレイアウトを正確に制御するために、ログインコントロールをテンプレートに変換することができます。 この手順の残りの部分では、外観とレイアウトをカスタマイズする方法について説明します。

### <a name="customizing-the-login-controls-appearance"></a>ログインコントロールの外観のカスタマイズ

ログインコントロールの既定のプロパティ設定では、ユーザーインターフェイスが表示されます。これには、ユーザー名とパスワードの入力、[次回に保存] チェックボックス、[ログイン] ボタンがあります。 これらの要素の外観は、すべて Login コントロールの多くのプロパティを使用して構成できます。 さらに、新しいユーザーアカウントを作成するためのページへのリンクなどの追加のユーザーインターフェイス要素は、プロパティまたは2を設定することによって追加できます。

ログインコントロールの外観をさしに少し時間をかけてみましょう。 [`Login.aspx`] ページには [ログイン] と表示されているページの上部に既にテキストがあるため、ログインコントロールのタイトルは余分です。 そのため、ログインコントロールのタイトルを削除するには、 [`TitleText` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx)の値をオフにします。

[ユーザー名] と [パスワード]: 2 つのテキストボックスコントロールの左側にあるラベルは、それぞれ[`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx)および[`PasswordLabelText` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)を使用してカスタマイズできます。 ユーザー名: ラベルを「ユーザー名:」に変更してみましょう。 ラベルとテキストボックスのスタイルは、それぞれ[`LabelStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx)と[`TextBoxStyle` のプロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)を使用して構成できます。

[次回に保存] チェックボックスの Text プロパティは、Login コントロールの[`RememberMeText` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx)を使用して設定できます。既定のチェック状態は、 [`RememberMeSet` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx)(既定値は False) を使用して構成できます。 [次の時間を記憶する] チェックボックスが既定でオンになるように、[`RememberMeSet`] プロパティを [True] に設定します。

ログインコントロールには、ユーザーインターフェイスコントロールのレイアウトを調整するための2つのプロパティが用意されています。 [`TextLayout` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx)は、ユーザー名: とパスワード: ラベルが対応するテキストボックスの左側に表示されるかどうかを示します (既定)。それ以外の場合は、その上に表示されます。 [`Orientation` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx)は、ユーザー名とパスワードの入力が垂直方向 (もう一方の方) または水平方向のどちらに配置されているかを示します。 これら2つのプロパティは既定値に設定したままにしておきますが、結果として得られる効果を確認するには、これら2つのプロパティを既定値以外の値に設定することをお勧めします。

> [!NOTE]
> 次のセクション「ログインコントロールのレイアウトの構成」では、テンプレートを使用してレイアウトコントロールのユーザーインターフェイス要素の正確なレイアウトを定義する方法を見ていきます。

[`CreateUserText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx)と[`CreateUserUrl` のプロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx)を未登録に設定して、ログインコントロールのプロパティ設定をラップしますか? アカウントを作成します。 とはそれぞれ `~/Membership/CreatingUserAccounts.aspx`ます。 これにより、 <a id="Tutorial05"> </a>[前のチュートリアル](creating-user-accounts-vb.md)で作成したページを指すログインコントロールのインターフェイスへのハイパーリンクが追加されます。 ログインコントロールの[`HelpPageText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx)と[`HelpPageUrl` のプロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx)と[`PasswordRecoveryText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx)および[`PasswordRecoveryUrl` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx)は同じように動作し、ヘルプページへのリンクとパスワードの回復ページが表示されます。

これらのプロパティの変更を行った後、ログインコントロールの宣言型のマークアップと外観は、図5に示すようになります。

[ログインコントロールのプロパティの値を ![して、その外観を決定します](validating-user-credentials-against-the-membership-user-store-vb/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image13.png)

**図 5**: ログインコントロールのプロパティの値によって外観が決まります ([クリックすると、フルサイズの画像が表示](validating-user-credentials-against-the-membership-user-store-vb/_static/image15.png)されます)

### <a name="configuring-the-login-controls-layout"></a>ログインコントロールのレイアウトの構成

ログイン Web コントロールの既定のユーザーインターフェイスは、HTML `<table>`でインターフェイスをレイアウトします。 しかし、レンダリングされた出力をより細かく制御する必要がある場合はどうでしょうか。 場合によっては、`<table>` を一連の `<div>` タグに置き換える必要があります。 または、アプリケーションで認証に追加の資格情報が必要な場合はどうすればよいでしょうか。 たとえば、多くの金融 web サイトでは、ユーザー名とパスワードだけでなく、個人識別番号 (PIN)、またはその他の識別情報も指定する必要があります。 理由にかかわらず、ログインコントロールをテンプレートに変換することができます。この場合、インターフェイスの宣言型マークアップを明示的に定義できます。

追加の資格情報を収集するためにログインコントロールを更新するには、次の2つの操作を行う必要があります。

1. 追加の資格情報を収集するための Web コントロールを含めるように、ログインコントロールのインターフェイスを更新します。
2. ログインコントロールの内部認証ロジックをオーバーライドして、ユーザー名とパスワードが有効で、追加の資格情報が有効である場合にのみユーザーが認証されるようにします。

最初のタスクを実行するには、ログインコントロールをテンプレートに変換し、必要な Web コントロールを追加する必要があります。 2番目のタスクと同様に、コントロールの[`Authenticate` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)のイベントハンドラーを作成することによって、ログインコントロールの認証ロジックを置き換えることができます。

ログインコントロールを更新して、ユーザーにユーザー名、パスワード、および電子メールアドレスを要求し、指定された電子メールアドレスがファイルの電子メールアドレスと一致する場合にのみ、ユーザーを認証するようにしてみましょう。 まず、ログインコントロールのインターフェイスをテンプレートに変換する必要があります。 ログインコントロールのスマートタグから、[テンプレートに変換] オプションを選択します。

[ログインコントロールをテンプレートに変換 ![には](validating-user-credentials-against-the-membership-user-store-vb/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image16.png)

**図 6**: ログインコントロールをテンプレートに変換する ([クリックすると、フルサイズの画像が表示](validating-user-credentials-against-the-membership-user-store-vb/_static/image18.png)されます)

> [!NOTE]
> ログインコントロールをテンプレート前のバージョンに戻すには、コントロールのスマートタグから [リセット] リンクをクリックします。

ログインコントロールをテンプレートに変換すると、ユーザーインターフェイスを定義する HTML 要素および Web コントロールを使用して、コントロールの宣言マークアップに `LayoutTemplate` が追加されます。 図7に示すように、コントロールをテンプレートに変換すると、テンプレートを使用するときに、これらのプロパティ値は無視されるため、`TitleText`、`CreateUserUrl`などのプロパティウィンドウから多数のプロパティが削除されます。

[ログインコントロールがテンプレートに変換されるときに使用できるプロパティを ![減らす](validating-user-credentials-against-the-membership-user-store-vb/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image19.png)

**図 7**: ログインコントロールがテンプレートに変換されたときに使用できるプロパティが減る ([クリックすると、フルサイズの画像が表示](validating-user-credentials-against-the-membership-user-store-vb/_static/image21.png)されます)

`LayoutTemplate` の HTML マークアップは、必要に応じて変更することができます。 同様に、新しい Web コントロールをテンプレートに追加してもかまいません。 ただし、ログイン制御のコア Web コントロールをテンプレートに残し、割り当てられた `ID` 値を保持することが重要です。 特に、`UserName` または `Password` のテキストボックス、[`RememberMe`] チェックボックス、[`LoginButton`] ボタン、`FailureText` ラベル、または `RequiredFieldValidator` コントロールを削除したり、名前を変更したりしないでください。

訪問者の電子メールアドレスを収集するには、テンプレートにテキストボックスを追加する必要があります。 `Password` テキストボックスを含むテーブル行 (`<tr>`) と、[次回保存] チェックボックスを保持するテーブル行の間に、次の宣言型マークアップを追加します。

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample2.aspx)]

`Email` テキストボックスを追加した後、ブラウザーを使用してページにアクセスします。 図8に示すように、ログインコントロールのユーザーインターフェイスには、3番目のテキストボックスが含まれています。

[ログインコントロールにユーザーの電子メールアドレスのテキストボックスが含まれるようになった ![](validating-user-credentials-against-the-membership-user-store-vb/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image22.png)

**図 8**: ログインコントロールにユーザーの電子メールアドレスのテキストボックスが含まれるようになりました ([クリックすると、フルサイズの画像が表示](validating-user-credentials-against-the-membership-user-store-vb/_static/image24.png)されます)

この時点で、ログインコントロールは、まだ `Membership.ValidateUser` メソッドを使用して、指定された資格情報を検証しています。 また、`Email` テキストボックスに入力した値は、ユーザーがログインできるかどうかには影響しません。 手順3では、ユーザー名とパスワードが有効であり、指定された電子メールアドレスがファイルの電子メールアドレスと一致する場合にのみ、資格情報が有効と見なされるように、ログインコントロールの認証ロジックを上書きする方法について説明します。

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>手順 3: ログインコントロールの認証ロジックを変更する

ビジターが資格情報を入力し、[ログイン] ボタンをクリックすると、ポストバック ensues とログイン制御が、その認証ワークフローを通じて進行します。 ワークフローは、 [`LoggingIn` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx)を発生させて開始します。 このイベントに関連付けられているすべてのイベントハンドラーは、`e.Cancel` プロパティを `True`に設定することによって、ログイン操作をキャンセルできます。

ログイン操作が取り消されていない場合、ワークフローは[`Authenticate` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)を発生させて進行します。 `Authenticate` イベントのイベントハンドラーがある場合は、指定された資格情報が有効かどうかを判断する役割があります。 イベントハンドラーが指定されていない場合、ログイン制御は `Membership.ValidateUser` メソッドを使用して資格情報の有効性を判断します。

指定された資格情報が有効な場合は、フォーム認証チケットが作成され、 [`LoggedIn` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx)が発生し、ユーザーが適切なページにリダイレクトされます。 ただし、資格情報が無効と見なされた場合、 [`LoginError` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx)が発生し、ユーザーに資格情報が無効であることを知らせるメッセージが表示されます。 既定では、エラーが発生した場合、ログイン制御は単に `FailureText` Label コントロールの Text プロパティをエラーメッセージに設定します (ログイン試行は成功しませんでした)。 もう一度やり直してください。) ただし、ログインコントロールの[`FailureAction` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx)が `RedirectToLoginPage`に設定されている場合、ログインコントロールは、querystring パラメーター `loginfailure=1` を追加するログインページに `Response.Redirect` を発行します (これにより、ログイン制御によってエラーメッセージが表示されます)。

図9に、認証ワークフローのフローチャートを提供します。

[ログインコントロールの認証ワークフローを ![する](validating-user-credentials-against-the-membership-user-store-vb/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image25.png)

**図 9**: ログインコントロールの認証ワークフロー ([クリックすると、フルサイズの画像が表示](validating-user-credentials-against-the-membership-user-store-vb/_static/image27.png)されます)

> [!NOTE]
> `FailureAction`の `RedirectToLogin` ページ オプションを使用する場合は、次のシナリオを考慮してください。 現在、`Site.master` マスターページには、匿名ユーザーがアクセスしたときに、左側の列に "Hello" というテキストが表示されていますが、そのテキストをログインコントロールに置き換えることを考えています。 これにより、匿名ユーザーは、ログインページに直接アクセスする必要がなく、サイトの任意のページからログインできるようになります。 ただし、マスターページによって表示されるログイン制御を使用してユーザーがログインできなかった場合は、ログインページ (`Login.aspx`) にリダイレクトすることをお勧めします。これは、マスターページに追加されていない新しいアカウントを作成したり、紛失したパスワードを取得したりするためのリンクなど、追加の指示やリンクなどの

### <a name="creating-theauthenticateevent-handler"></a>`Authenticate`イベントハンドラーの作成

カスタム認証ロジックをプラグインするには、ログインコントロールの `Authenticate` イベントのイベントハンドラーを作成する必要があります。 `Authenticate` イベントのイベントハンドラーを作成すると、次のイベントハンドラー定義が生成されます。

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample3.vb)]

ご覧のように、`Authenticate` イベントハンドラーには、 [`AuthenticateEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx)型のオブジェクトが2番目の入力パラメーターとして渡されます。 `AuthenticateEventArgs` クラスには、指定された資格情報が有効かどうかを指定するために使用される `Authenticated` という名前のブール型プロパティが含まれています。 次に、指定された資格情報が有効かどうかを判断し、それに応じて `e.Authenticate` プロパティを設定するコードをここに記述します。

### <a name="determining-and-validating-the-supplied-credentials"></a>指定された資格情報の確認と検証

ログインコントロールの[`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx)と`Password` の[プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx)を使用して、ユーザーが入力したユーザー名とパスワードの資格情報を確認します。 追加の Web コントロール (前の手順で追加した `Email` TextBox など) に入力された値を確認するには、`LoginControlID.FindControl`(" *`controlID`* ") を使用して、`ID` プロパティが *`controlID`* と等しいテンプレート内の web コントロールへのプログラムによる参照を取得します。 たとえば、`Email` テキストボックスへの参照を取得するには、次のコードを使用します。

`Dim EmailTextBox As TextBox = CType(myLogin.FindControl("Email"), TextBox)`

ユーザーの資格情報を検証するには、次の2つの作業を行う必要があります。

1. 指定されたユーザー名とパスワードが有効であることを確認してください
2. 入力した電子メールアドレスが、ログインしようとしているユーザーのファイルの電子メールアドレスと一致していることを確認します

最初のチェックを実行するには、手順1で示したのと同様に `Membership.ValidateUser` メソッドを使用するだけです。 2番目のチェックでは、ユーザーの電子メールアドレスを確認し、テキストボックスコントロールに入力した電子メールアドレスと比較できるようにする必要があります。 特定のユーザーに関する情報を取得するには、`Membership` クラスの[`GetUser` メソッド](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)を使用します。

`GetUser` メソッドには、多くのオーバーロードがあります。 パラメーターを渡さずに使用した場合は、現在ログインしているユーザーに関する情報が返されます。 特定のユーザーに関する情報を取得するには、を呼び出し `GetUser` ユーザー名を渡します。 どちらの場合も、`GetUser` は、`UserName`、`Email`、`IsApproved`、`IsOnline`などのプロパティを持つ[`MembershipUser` オブジェクト](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)を返します。

次のコードでは、これら2つのチェックを実装しています。 両方が渡された場合、`e.Authenticate` は `True`に設定されます。それ以外の場合は `False`が割り当てられます。

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample4.vb)]

このコードを使用して、有効なユーザーとしてログインし、正しいユーザー名、パスワード、および電子メールアドレスを入力します。 もう一度試してみてください。ただし、今回は意図的に無効な電子メールアドレスを使用しています (図10を参照)。 最後に、存在しないユーザー名を使用して、3回目にします。 最初のケースでは、サイトに正常にログオンする必要がありますが、最後の2つのケースでは、ログインコントロールの無効な資格情報メッセージが表示されます。

[無効な電子メールアドレスを指定したときにログインできない ![Tito](validating-user-credentials-against-the-membership-user-store-vb/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image28.png)

**図 10**: 無効な電子メールアドレスを指定するときにログインできない ([クリックしてフルサイズの画像を表示する](validating-user-credentials-against-the-membership-user-store-vb/_static/image30.png))

> [!NOTE]
> 手順1の「メンバーシップフレームワークが無効なログイン試行を処理する方法」セクションで説明したように、`Membership.ValidateUser` メソッドが呼び出され、無効な資格情報が渡されると、無効なログイン試行を追跡し、指定された時間枠内に無効な試行回数を超えた場合にユーザーをロックアウトします。 カスタム認証ロジックによって `ValidateUser` メソッドが呼び出されるため、有効なユーザー名のパスワードが正しくないと、無効なログイン試行カウンターが増加しますが、ユーザー名とパスワードが有効であっても、電子メールアドレスが正しくない場合は、このカウンターはインクリメントされません。 ハッカーがユーザー名とパスワードを知ることはほとんどなく、ブルートフォース手法を使用してユーザーの電子メールアドレスを決定する必要があるため、この動作は適切です。

## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>手順 4: ログインコントロールの無効な資格情報メッセージを改善する

ユーザーが無効な資格情報でログオンしようとすると、ログインの試行が失敗したことを示すメッセージが表示されます。 特に、コントロールには[`FailureText` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx)によって指定されたメッセージが表示されます。このプロパティには、ログイン試行の既定値が正しくありませんでした。 やり直してください。

ユーザーの資格情報が無効になる理由は数多くあります。

- ユーザー名が存在しない可能性があります
- ユーザー名は存在しますが、パスワードが無効です
- ユーザー名とパスワードは有効ですが、ユーザーはまだ承認されていません
- ユーザー名とパスワードは有効ですが、ユーザーがロックアウトされています (指定された期間内の無効なログイン試行回数を超えたことが原因である可能性があります)。

また、カスタム認証ロジックを使用する場合もあります。 たとえば、手順 3. で記述したコードでは、ユーザー名とパスワードは有効ですが、電子メールアドレスが正しくない可能性があります。

資格情報が無効である理由に関係なく、ログインコントロールでも同じエラーメッセージが表示されます。 このフィードバックがないと、アカウントがまだ承認されていないユーザーや、ロックアウトされているユーザーが混乱する可能性があります。ただし、少しの作業で、ログインコントロールにより適切なメッセージが表示されるようにすることができます。

ユーザーが無効な資格情報でログインしようとすると、ログイン制御によってその `LoginError` イベントが発生します。 このイベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample5.vb)]

上記のコードは、ログインコントロールの `FailureText` プロパティを既定値に設定することによって開始されます (ログイン試行は成功しませんでした。 もう一度やり直してください。) 次に、指定されたユーザー名が既存のユーザーアカウントにマップされているかどうかを確認します。 その場合は、生成された `MembershipUser` オブジェクトの `IsLockedOut` と `IsApproved` プロパティを調べて、アカウントがロックアウトされているか、まだ承認されていないかを判断します。 どちらの場合も、`FailureText` プロパティは対応する値に更新されます。

このコードをテストするには、既存のユーザーとしてログインを意図的に試みますが、正しくないパスワードを使用します。 この処理は10分間の行で5回実行され、アカウントはロックアウトされます。図11に示すように、後続のログイン試行は (正しいパスワードを使用しても) 常に失敗しますが、無効なログイン試行回数が多すぎるため、アカウントがロックアウトされたことがわかりやすく表示されるようになりました。 アカウントのロックを解除するには、管理者に連絡してください。

[無効なログイン試行回数が多すぎて、ロックアウトされた ![Tito](validating-user-credentials-against-the-membership-user-store-vb/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image31.png)

**図 11**: Tito は無効なログイン試行回数が多すぎて、ロックアウトされています ([クリックすると、フルサイズの画像が表示](validating-user-credentials-against-the-membership-user-store-vb/_static/image33.png)されます)

## <a name="summary"></a>要約

このチュートリアルの前に、ログインページでは、指定された資格情報を、ハードコーディングされたユーザー名とパスワードの組み合わせに対して検証しました。 このチュートリアルでは、メンバーシップフレームワークに対して資格情報を検証するためにページを更新しました。 手順 1. では、`Membership.ValidateUser` メソッドをプログラムで使用する方法を説明しました。 手順2では、手動で作成したユーザーインターフェイスとコードをログインコントロールに置き換えました。

Login コントロールは、標準のログインユーザーインターフェイスをレンダリングし、メンバーシップフレームワークに対してユーザーの資格情報を自動的に検証します。 さらに、有効な資格情報がある場合、ログイン制御はフォーム認証を介してユーザーにサインインします。 簡単に言うと、完全に機能するログインユーザーエクスペリエンスは、ログインコントロールをページにドラッグするだけで利用できます。追加の宣言型マークアップやコードは必要ありません。 さらに、ログイン制御は高度なカスタマイズが可能で、レンダリングされたユーザーインターフェイスと認証ロジックの両方を細かく制御できます。

この時点で、web サイトの訪問者は、新しいユーザーアカウントを作成してサイトにログインできますが、認証されたユーザーに基づいてページへのアクセスを制限することを検討しています。 現在、認証または匿名のすべてのユーザーは、サイトの任意のページを表示できます。 ユーザーごとにサイトのページへのアクセスを制御することに加えて、ユーザーに依存する機能を持つ特定のページがある場合があります。 次のチュートリアルでは、ログインしているユーザーに基づいて、アクセスとページ内の機能を制限する方法について説明します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ロックアウトされたユーザーと承認されていないユーザーにカスタムメッセージを表示する](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [ASP.NET 2.0 のメンバーシップ、ロール、およびプロファイルを調べています](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [方法: ASP.NET ログインページを作成する](https://msdn.microsoft.com/library/ms178331.aspx)
- [ログイン制御の技術ドキュメント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [ログインコントロールの使用](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Teresa Murphy と Michael Olivero でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](creating-user-accounts-vb.md)
> [次へ](user-based-authorization-vb.md)

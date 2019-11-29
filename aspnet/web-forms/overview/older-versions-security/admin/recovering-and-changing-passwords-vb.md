---
uid: web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-vb
title: パスワードの回復と変更 (VB) |Microsoft Docs
author: rick-anderson
description: ASP.NET には、パスワードの回復と変更を支援する2つの Web コントロールが含まれています。 PasswordRecovery コントロールを使用すると、ビジターが紛失した pa を回復できます...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: f9adcb5d-6d70-4885-a3bf-ed95efb4da1a
msc.legacyurl: /web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ed1df9455af94a86ce59ecc06c55846a4880596
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618763"
---
# <a name="recovering-and-changing-passwords-vb"></a>パスワードを復元し、変更する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.13.zip)または[PDF のダウンロード](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial13_ChangingPasswords_vb.pdf)

> ASP.NET には、パスワードの回復と変更を支援する2つの Web コントロールが含まれています。 PasswordRecovery コントロールを使用すると、ビジターが紛失したパスワードを回復することができます。 ChangePassword コントロールを使用すると、ユーザーは自分のパスワードを更新できます。 このチュートリアルシリーズ全体で見てきた他のログイン関連 Web コントロールと同様に、PasswordRecovery と ChangePassword コントロールは、ユーザーのパスワードをリセットまたは変更するための背後でメンバーシップフレームワークと連携します。

## <a name="introduction"></a>はじめに

銀行、公益事業、電話会社、電子メールアカウント、およびパーソナライズされた web ポータルの web サイトでは、ほとんどのユーザーと同じように、多数のパスワードを覚えておく必要があります。 多くの資格情報を使用すると、ユーザーがパスワードを忘れてしまうことは珍しくありません。 このことを考慮するために、ユーザーアカウントを提供する web サイトには、ユーザーがパスワードを回復する方法を含める必要があります。 通常、このプロセスでは、新しいランダムなパスワードを生成し、ファイルのユーザーの電子メールアドレスに電子メールで送信します。 新しいパスワードを受け取った場合、ほとんどのユーザーはサイトに戻り、ランダムに生成されたパスワードを、より覚えやすいものに変更します。

ASP.NET には、パスワードの回復と変更を支援する2つの Web コントロールが含まれています。 PasswordRecovery コントロールを使用すると、ビジターが紛失したパスワードを回復することができます。 ChangePassword コントロールを使用すると、ユーザーは自分のパスワードを更新できます。 このチュートリアルシリーズ全体で見てきた他のログイン関連 Web コントロールと同様に、PasswordRecovery と ChangePassword コントロールは、ユーザーのパスワードをリセットまたは変更するための背後でメンバーシップフレームワークと連携します。

このチュートリアルでは、これら2つのコントロールを使用する方法について説明します。 また、`MembershipUser` クラスの `ChangePassword` メソッドと `ResetPassword` メソッドを使用して、ユーザーのパスワードをプログラムで変更およびリセットする方法についても説明します。

## <a name="step-1-helping-users-recover-lost-passwords"></a>手順 1: ユーザーが紛失したパスワードを回復できるようにする

ユーザーアカウントをサポートするすべての web サイトは、忘れたパスワードを回復するためのメカニズムをユーザーに提供する必要があります。 ASP.NET にこのような機能を実装することは、PasswordRecovery Web コントロールに感謝します。 PasswordRecovery コントロールは、ユーザーにユーザー名の入力を求めるインターフェイスをレンダリングし、必要に応じて、セキュリティの質問に対する回答を表示します。 その後、ユーザーにパスワードを電子メールで入力します。

> [!NOTE]
> 電子メールメッセージは、プレーンテキストでネットワーク経由で送信されるため、電子メールでユーザーのパスワードを送信することにはセキュリティ上のリスクが伴います。

PasswordRecovery コントロールは、次の3つのビューで構成されます。

- **Username** -ビジターにユーザー名の入力を求めます。 これは最初のビューです。
- **質問**-ユーザーのユーザー名とセキュリティの質問をテキストとして表示し、ユーザーがセキュリティの質問に答えを入力するためのテキストボックスを表示します。
- **成功**-パスワードが電子メールで送信されたことをユーザーに通知するメッセージを表示します。

PasswordRecovery コントロールによって実行されるビューとアクションは、次のメンバーシップ構成設定によって異なります。

- `RequiresQuestionAndAnswer`
- `EnablePasswordRetrieval`
- `EnablePasswordReset`

メンバーシップフレームワークの `RequiresQuestionAndAnswer` 設定は、ユーザーがアカウントの登録時にセキュリティの質問と回答を指定する必要があるかどうかを示します。 「 <a id="_msoanchor_1"> </a>[*ユーザーアカウントの作成*](../membership/creating-user-accounts-vb.md)」チュートリアルで説明したように、`RequiresQuestionAndAnswer` が True (既定値) の場合、CreateUserWizard のインターフェイスには、新しいユーザーのセキュリティの質問と回答のテキストボックスコントロールが含まれています。`RequiresQuestionAndAnswer` が False の場合、そのような情報は収集されません。 同様に `RequiresQuestionAndAnswer` が True の場合、ユーザーがユーザー名を入力した後に、PasswordRecovery コントロールによって質問ビューが表示されます。パスワードは、ユーザーが正しいセキュリティの回答を入力した場合にのみ回復されます。 ただし `RequiresQuestionAndAnswer` が False の場合、PasswordRecovery コントロールはユーザー名ビューから [成功] ビューに直接移動します。

ユーザーが自分のユーザー名、または自分のユーザー名とセキュリティの回答を入力した後、`RequiresQuestionAndAnswer` が True の場合は、PasswordRecovery によってユーザーのパスワードが電子メールで送られます。 `EnablePasswordRetrieval` オプションが True に設定されている場合、ユーザーは現在のパスワードを電子メールで送信します。 False に設定されていて `EnablePasswordReset` が True に設定されている場合は、PasswordRecovery コントロールによってユーザーに対して新しいランダムなパスワードが生成され、このパスワードに新しいパスワードが電子メールで送られます。 `EnablePasswordRetrieval` と `EnablePasswordReset` の両方が False の場合、PasswordRecovery コントロールは例外をスローします。

> [!NOTE]
> `SqlMembershipProvider` は、クリア、ハッシュ (既定)、または暗号化された3つの形式のいずれかでユーザーのパスワードを格納していることを思い出してください。 使用されるストレージメカニズムは、メンバーシップの構成設定によって異なります。デモアプリケーションでは、ハッシュされたパスワード形式を使用します。 ハッシュされたパスワード形式を使用する場合は、`EnablePasswordRetrieval` オプションを False に設定する必要があります。これは、システムが、データベースに格納されているハッシュされたバージョンからユーザーの実際のパスワードを特定できないためです。

図1は、PasswordRecovery のインターフェイスと動作がメンバーシップの構成によってどのように影響を受けるかを示しています。

[RequiresQuestionAndAnswer、Enablepasswordretrieval、Enablepasswordretrieval が PasswordRecovery コントロールの外観と動作に影響を与える ![](recovering-and-changing-passwords-vb/_static/image2.png)](recovering-and-changing-passwords-vb/_static/image1.png)

**図 1**: `RequiresQuestionAndAnswer`、`EnablePasswordRetrieval`、および `EnablePasswordReset` は、passwordrecovery コントロールの外観と動作に影響を及ぼします ([クリックすると、フルサイズの画像が表示](recovering-and-changing-passwords-vb/_static/image3.png)されます)。

> [!NOTE]
> SQL Server チュートリアル<a id="_msoanchor_2"> </a>[*でメンバーシップスキーマを作成*](../membership/creating-the-membership-schema-in-sql-server-vb.md)するには、`RequiresQuestionAndAnswer` を true に設定してメンバーシッププロバイダーを構成し、False に `EnablePasswordRetrieval` し、を true に `EnablePasswordReset` します。

### <a name="using-the-passwordrecovery-control"></a>PasswordRecovery コントロールの使用

ASP.NET ページで PasswordRecovery コントロールを使用する方法を見てみましょう。 `RecoverPassword.aspx` を開き、[ツールボックス] から PasswordRecovery コントロールをデザイナーにドラッグアンドドロップします。`ID` を `RecoverPwd`に設定します。 Login および CreateUserWizard Web コントロールと同様に、PasswordRecovery コントロールのビューには、ラベル、テキストボックス、ボタン、および検証コントロールを含む、豊富な複合インターフェイスが表示されます。 ビューの外観をカスタマイズするには、コントロールのスタイルプロパティを使用するか、ビューをテンプレートに変換します。 これは関心のある読者のための演習として残されています。

ユーザーがこのページにアクセスすると、自分のユーザー名を入力し、[送信] ボタンをクリックします。 メンバーシップの構成設定で [`RequiresQuestionAndAnswer`] プロパティを True に設定しているので、PasswordRecovery コントロールでは質問ビューが表示されます。 ユーザーが適切なセキュリティの回答を入力して [送信] をクリックすると、PasswordRecovery コントロールはユーザーのパスワードをランダムに生成されたパスワードに更新し、このパスワードをファイルの電子メールアドレスに電子メールで送信します。 1行のコードを記述しなくても、すべてのことが可能でした。

このページをテストする前に、構成の最終的な構成要素が1つあります。 `Web.config`でメール配信の設定を指定する必要があります。 PasswordRecovery コントロールは、これらの設定に基づいて電子メールを送信します。

メール配信の構成は、 [`<system.net>` 要素](https://msdn.microsoft.com/library/6484zdc1.aspx)の[`<mailSettings>` 要素](https://msdn.microsoft.com/library/w355a94k.aspx)によって指定されます。 [`<smtp>` 要素](https://msdn.microsoft.com/library/ms164240.aspx)を使用して、配信方法と既定の差出人アドレスを指定します。 次のマークアップは、ポート25で `smtp.example.com` という名前のネットワーク SMTP サーバーと、ユーザー名とパスワードのユーザー名/パスワードの資格情報を使用するように、メールの設定を構成します。

> [!NOTE]
> `<system.net>` は、ルート `<configuration>` 要素の子要素であり、`<system.web>`の兄弟です。 したがって、`<system.web>` 要素内に `<system.net>` 要素を配置しないでください。代わりに、同じレベルに配置します。

[!code-xml[Main](recovering-and-changing-passwords-vb/samples/sample1.xml)]

ネットワーク上の SMTP サーバーを使用するだけでなく、送信する電子メールメッセージが格納されるピックアップディレクトリを指定することもできます。

SMTP 設定を構成したら、ブラウザーを使用して `RecoverPassword.aspx` のページにアクセスします。 まず、ユーザーストアに存在しないユーザー名を入力してください。 図2に示すように、PasswordRecovery コントロールには、ユーザー情報にアクセスできなかったことを示すメッセージが表示されます。 メッセージのテキストは、コントロールの[`UserNameFailureText` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.usernamefailuretext.aspx)を使用してカスタマイズできます。

[無効なユーザー名が入力された場合にエラーメッセージが表示される ![](recovering-and-changing-passwords-vb/_static/image5.png)](recovering-and-changing-passwords-vb/_static/image4.png)

**図 2**: 無効なユーザー名が入力された場合にエラーメッセージが表示される ([クリックしてフルサイズの画像を表示](recovering-and-changing-passwords-vb/_static/image6.png))

ここで、ユーザー名を入力します。 システム内のアカウントのユーザー名を使用して、アクセスできる電子メールアドレスと、そのセキュリティの回答を確認します。 ユーザー名を入力して [送信] をクリックすると、PasswordRecovery コントロールにその質問ビューが表示されます。 ユーザー名ビューの場合と同様に、間違った回答を入力すると、PasswordRecovery コントロールでエラーメッセージが表示されます (図3を参照)。 このエラーメッセージをカスタマイズするには、 [`QuestionFailureText` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.questionfailuretext.aspx)を使用します。

[ユーザーが無効なセキュリティの回答を入力すると、エラーメッセージが表示される ![](recovering-and-changing-passwords-vb/_static/image8.png)](recovering-and-changing-passwords-vb/_static/image7.png)

**図 3**: ユーザーが無効なセキュリティの回答を入力した場合にエラーメッセージが表示される ([クリックすると、フルサイズの画像が表示](recovering-and-changing-passwords-vb/_static/image9.png)されます)

最後に、正しいセキュリティの回答を入力し、[送信] をクリックします。 バックグラウンドでは、PasswordRecovery コントロールによってランダムなパスワードが生成され、ユーザーアカウントに割り当てられ、新しいパスワードをユーザーに通知する電子メールが送信されます (図4を参照)。その後、[成功] ビューが表示されます。

[ユーザーに新しいパスワードを使用して電子メールを送信 ![](recovering-and-changing-passwords-vb/_static/image11.png)](recovering-and-changing-passwords-vb/_static/image10.png)

**図 4**: ユーザーに新しいパスワードを使用して電子メールが送信される ([クリックすると、フルサイズの画像が表示](recovering-and-changing-passwords-vb/_static/image12.png)されます)

### <a name="customizing-the-email"></a>電子メールのカスタマイズ

PasswordRecovery コントロールによって送信された既定の電子メールは、代わりに退屈です (図4を参照)。 メッセージは、`<smtp>` 要素の `from` 属性で指定されたアカウントから、サブジェクトパスワードとプレーンテキストの本文で送信されます。

サイトに戻り、次の情報を使用してログインしてください。

ユーザー*名: ユーザー名*

パスワード:*パスワード*

このメッセージは、PasswordRecovery コントロールの[`SendingMail` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.sendingmail.aspx)のイベントハンドラーを通じて、または[`MailDefinition` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.maildefinition.aspx)を使用して宣言によってカスタマイズできます。 これら両方のオプションを見てみましょう。

`SendingMail` イベントは、電子メールメッセージが送信される直前に発生し、電子メールメッセージをプログラムによって調整する最後の機会になります。 このイベントが発生すると、イベントハンドラーには[`MailMessageEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.mailmessageeventargs.aspx)型のオブジェクトが渡され、`Message` プロパティには、送信される電子メールへの参照が含まれます。

`SendingMail` イベントのイベントハンドラーを作成し、次のコードを追加します。このコードは、プログラムを使用して `webmaster@example.com` を CC リストに追加します。

[!code-vb[Main](recovering-and-changing-passwords-vb/samples/sample2.vb)]

また、宣言的な方法で電子メールメッセージを構成することもできます。 PasswordRecovery の `MailDefinition` プロパティは、 [`MailDefinition`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.aspx)型のオブジェクトです。 `MailDefinition` クラスは、`From`、`CC`、`Priority`、`Subject`、`IsBodyHtml`、`BodyFileName`など、電子メール関連のプロパティのホストを提供します。 まず、[`Subject`][プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.subject.aspx)に、パスワードがリセットされたなど、既定 (パスワード) で使用されているものよりもわかりやすい値を設定します。

電子メールメッセージの本文をカスタマイズするには、本文の内容を含む別の電子メールテンプレートファイルを作成する必要があります。 まず、`EmailTemplates`という名前の web サイトに新しいフォルダーを作成します。 次に、`PasswordRecovery.txt` という名前のこのフォルダーに新しいテキストファイルを追加し、次の内容を追加します。

[!code-aspx[Main](recovering-and-changing-passwords-vb/samples/sample3.aspx)]

プレースホルダー `<%UserName%>` と `<%Password%>`を使用することに注意してください。 PasswordRecovery コントロールは、電子メールを送信する前に、これら2つのプレースホルダーをユーザーのユーザー名と回復したパスワードに自動的に置き換えます。

最後に、`MailDefinition`の[`BodyFileName` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx)を、先ほど作成した電子メールテンプレート (`~/EmailTemplates/PasswordRecovery.txt`) にポイントします。

これらの変更を行った後、[`RecoverPassword.aspx`] ページに戻って、ユーザー名とセキュリティの回答を入力します。 図5に示すような電子メールが届きます。 `webmaster@example.com` が CC に設定されており、件名と本文が更新されていることに注意してください。

[件名、本文、および CC の一覧が更新された ![](recovering-and-changing-passwords-vb/_static/image14.png)](recovering-and-changing-passwords-vb/_static/image13.png)

**図 5**: 件名、本文、および CC の一覧が更新されました ([クリックすると、フルサイズの画像が表示](recovering-and-changing-passwords-vb/_static/image15.png)されます)

HTML 形式の電子メールセットを[`IsBodyHtml`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.isbodyhtml.aspx) True に送信するには (既定値は False)、電子メールテンプレートを更新して html を含めます。

`MailDefinition` プロパティは、PasswordRecovery クラスに固有のものではありません。 手順 2. で説明したように、ChangePassword コントロールには `MailDefinition` プロパティも用意されています。 さらに、CreateUserWizard コントロールには、新しいユーザーに自動的にようこそ電子メールメッセージを送信するように構成できるプロパティが含まれています。

> [!NOTE]
> 現在、`RecoverPassword.aspx` ページに到達するための左側のナビゲーションにリンクはありません。 ユーザーは、サイトに正常にログオンできなかった場合にのみ、このページにアクセスすることを目的としています。 そのため、[`Login.aspx`] ページを更新して、[`RecoverPassword.aspx`] ページへのリンクを追加します。

### <a name="programmatically-resetting-a-users-password"></a>プログラムによるユーザーのパスワードのリセット

ユーザーのパスワードをリセットすると、PasswordRecovery コントロールは `MembershipUser` オブジェクトの[`ResetPassword` メソッド](https://msdn.microsoft.com/library/system.web.security.membershipuser.resetpassword.aspx)を呼び出します。 このメソッドには、次の2つのオーバーロードがあります。

- **[`ResetPassword`](https://msdn.microsoft.com/library/d94bdzz2.aspx)** -ユーザーのパスワードをリセットします。 `RequiresQuestionAndAnswer` が False の場合は、このオーバーロードを使用します。
- **[`ResetPassword(securityAnswer)`](https://msdn.microsoft.com/library/d90zte4w.aspx)** -指定した*securityanswer*が正しい場合にのみ、ユーザーのパスワードをリセットします。 `RequiresQuestionAndAnswer` が True の場合は、このオーバーロードを使用します。

どちらのオーバーロードも、ランダムに生成された新しいパスワードを返します。

メンバーシップフレームワークの他のメソッドと同様に、`ResetPassword` メソッドは構成されたプロバイダーにデリゲートします。 `SqlMembershipProvider` は、ユーザーのユーザー名、新しいパスワード、および指定されたパスワードの解答を他のフィールドに渡して、`aspnet_Membership_ResetPassword` ストアドプロシージャを呼び出します。 このストアドプロシージャにより、パスワードの解答が確実に一致し、ユーザーのパスワードが更新されます。

低レベルの実装に関する注意事項をいくつか次に示します。

- ロックアウトされたユーザーは、自分のパスワードをリセットできません。 ただし、未承認のユーザーがいる可能性があります。 ロックアウトと承認された状態については、「 <a id="_msoanchor_3"> </a>[*ユーザーアカウントのロック解除と承認*](unlocking-and-approving-user-accounts-vb.md)」チュートリアルで詳細に説明します。
- パスワードの解答が正しくない場合、ユーザーのパスワードの解答試行回数が増加します。 指定された期間内に指定された無効なセキュリティ回答の試行回数が発生した場合、ユーザーはロックアウトされます。

### <a name="a-word-on-how-the-random-passwords-are-generated"></a>ランダムなパスワードが生成される方法に関する単語

図4および5の電子メールメッセージに表示されるランダムに生成されたパスワードは、メンバーシップクラスの[`GeneratePassword` メソッド](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)によって作成されます。 このメソッドは、2つの整数入力のパラメーター*長*と*numberOfNonAlphanumericCharacters*を受け取り、少なくとも*numberOfNonAlphanumericCharacters*の数字以外の文字を含む*長さ*が長い文字列を返します。 このメソッドがメンバーシップクラスまたはログイン関連の Web コントロール内から呼び出された場合、これら2つのパラメーターの値は、メンバーシップ構成の `MinRequiredPasswordLength` と `MinRequiredNonalphanumericCharacters` プロパティによって決定されます。これらの値はそれぞれ7と1に設定されます。

`GeneratePassword` メソッドは、暗号強度の高い乱数ジェネレーターを使用して、選択されているランダム文字にバイアスがないことを確認します。 さらに、ランダムな文字列またはパスワードを生成する必要がある場合は、`GeneratePassword` が `Public`ます。つまり、ASP.NET アプリケーションから直接使用できます。

> [!NOTE]
> `SqlMembershipProvider` クラスでは、常に14文字以上のランダムなパスワードが生成されます。そのため、`MinRequiredPasswordLength` が14文字未満の場合、その値は無視されます。

## <a name="step-2-changing-passwords"></a>手順 2: パスワードの変更

ランダムに生成されたパスワードは覚えにくいものです。 図4に示すパスワードを考えてみます。 `WWGUZv(f2yM:Bd`を参照してください。 メモリへのコミットを試行してください。 言うまでもありませんが、この種のランダムに生成されたパスワードをユーザーに送信した後は、より覚えやすいパスワードに変更する必要があります。

パスワードを変更するためのインターフェイスをユーザーに対して作成するには、ChangePassword コントロールを使用します。 PasswordRecovery コントロールと同様に、ChangePassword コントロールは、パスワードの変更と成功の2つのビューで構成されます。 パスワードの変更ビューでは、ユーザーは古いパスワードと新しいパスワードを入力するように求められます。 正しい古いパスワードと、最小文字数と英数字以外の文字の要件を満たす新しいパスワードを指定すると、ChangePassword コントロールによってユーザーのパスワードが更新され、[成功] ビューが表示されます。

> [!NOTE]
> ChangePassword コントロールは、`MembershipUser` オブジェクトの[`ChangePassword` メソッド](https://msdn.microsoft.com/library/system.web.security.membershipuser.changepassword.aspx)を呼び出すことによって、ユーザーのパスワードを変更します。 ChangePassword メソッドは、 *oldpassword*と*newPassword*という2つの `String` 入力パラメーターを受け取り、指定された*oldpassword*が正しいことを前提として、ユーザーのアカウントを*newPassword*で更新します。

[`ChangePassword.aspx`] ページを開き、[ChangePassword] コントロールをページに追加して `ChangePwd`名前を付けます。 この時点で、デザインビューにパスワードの変更ビューが表示されます (図6を参照)。 PasswordRecovery コントロールと同様に、コントロールのスマートタグを使用してビューを切り替えることができます。 さらに、これらのビューの外観は、さまざまなスタイルプロパティまたはテンプレートに変換することによってカスタマイズできます。

[![ChangePassword コントロールをページに追加するには](recovering-and-changing-passwords-vb/_static/image17.png)](recovering-and-changing-passwords-vb/_static/image16.png)

**図 6**: ChangePassword コントロールをページに追加する ([クリックすると、フルサイズの画像が表示](recovering-and-changing-passwords-vb/_static/image18.png)されます)

ChangePassword コントロールでは、現在ログインしているユーザーのパスワード、*または*別の指定されたユーザーのパスワードを更新できます。 図6に示すように、既定のパスワードの変更ビューでは、3つのテキストボックスコントロールが表示されます。1つは古いパスワード用で、もう1つは新しいパスワード用です。 この既定のインターフェイスは、現在ログオンしているユーザーのパスワードを更新するために使用されます。

ChangePassword コントロールを使用して別のユーザーのパスワードを更新するには、コントロールの[`DisplayUserName` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.changepassword.displayusername.aspx)を True に設定します。 このようにすると、ページに4番目のテキストボックスが追加され、パスワードを変更するユーザーのユーザー名の入力を求められます。

`DisplayUserName` を True に設定すると、ログアウトしたユーザーがログインしなくてもパスワードを変更できるようにする場合に便利です。 個人的には、パスワードの変更を許可する前に、ユーザーにログインを要求しても問題はありません。 そのため、`DisplayUserName` は False (既定値) のままにしておきます。 ただし、この決定を行う際、基本的に、匿名ユーザーがこのページにアクセスできないようにしています。 匿名ユーザーが `ChangePassword.aspx`にアクセスするのを拒否するように、サイトの URL 承認規則を更新します。 URL 承認規則の構文でメモリを更新する必要がある場合は、 <a id="_msoanchor_4"> </a>[*ユーザーベースの承認*](../membership/user-based-authorization-vb.md)に関するチュートリアルを参照してください。

> [!NOTE]
> `DisplayUserName` プロパティは、管理者が他のユーザーのパスワードを変更できるようにするのに便利な場合があります。 ただし、`DisplayUserName` が True に設定されている場合でも、正しい古いパスワードを認識して入力する必要があります。 手順3で管理者がユーザーのパスワードを変更できるようにするための手法について説明します。

ブラウザーを使用して `ChangePassword.aspx` のページにアクセスし、パスワードを変更します。 メンバーシップの構成で指定されているパスワードの長さと英数字以外の文字の要件を満たしていない新しいパスワードを入力すると、エラーメッセージが表示されることに注意してください (図7を参照)。

[![ChangePassword コントロールをページに追加するには](recovering-and-changing-passwords-vb/_static/image20.png)](recovering-and-changing-passwords-vb/_static/image19.png)

**図 7**: ChangePassword コントロールをページに追加する ([クリックすると、フルサイズの画像が表示](recovering-and-changing-passwords-vb/_static/image21.png)されます)

正しい古いパスワードと有効な新しいパスワードを入力すると、ログオンしたユーザーのパスワードが変更され、[成功] ビューが表示されます。

### <a name="sending-a-confirmation-email"></a>確認メールの送信

既定では、ChangePassword コントロールは、パスワードが更新されたばかりのユーザーに電子メールメッセージを送信しません。 電子メールを送信する場合は、コントロールの `MailDefinition` プロパティを構成するだけです。 新しいパスワードを含む HTML 形式の電子メールがユーザーに送信されるように、ChangePassword コントロールを構成してみましょう。

まず、`ChangePassword.htm`という名前の `EmailTemplates` フォルダーに新しいファイルを作成します。 次のマークアップを追加します。

[!code-html[Main](recovering-and-changing-passwords-vb/samples/sample4.html)]

次に、ChangePassword コントロールの `MailDefinition` プロパティの `BodyFileName`、`IsBodyHtml`、および `Subject` プロパティを ~/EmailTemplates/ChangePassword.htm、True に設定します。パスワードはそれぞれ変更されています。

これらの変更を行った後、ページを再入力して、もう一度パスワードを変更します。 このとき、ChangePassword コントロールは、カスタマイズされた HTML 形式の電子メールをファイルのユーザーの電子メールアドレスに送信します (図8を参照)。

[パスワードが変更されたことをユーザーに通知する電子メールメッセージを ![する](recovering-and-changing-passwords-vb/_static/image23.png)](recovering-and-changing-passwords-vb/_static/image22.png)

**図 8**: 電子メールメッセージによって、パスワードが変更されたことがユーザーに通知される ([クリックすると、フルサイズの画像が表示](recovering-and-changing-passwords-vb/_static/image24.png)されます)

## <a name="step-3-allowing-administrators-to-change-users-passwords"></a>手順 3: 管理者がユーザーのパスワードを変更できるようにする

ユーザーアカウントをサポートするアプリケーションの一般的な機能は、管理ユーザーが他のユーザーのパスワードを変更できるようにする機能です。 場合によっては、ユーザーが自分のパスワードを変更する機能がないため、この機能が必要になることがあります。 このような場合、ユーザーが忘れたパスワードを回復する唯一の方法は、管理者が新しいパスワードを割り当てることです。 ただし、PasswordRecovery と ChangePassword コントロールでは、管理ユーザーがユーザーのパスワードを変更する必要があります。ユーザーはこの操作を行うことができるためです。

しかし、クライアントが他のユーザーのパスワードを変更できるようにする必要がある場合はどうでしょうか。 残念ながら、この機能の追加には少しの作業が必要になる場合があります。 ユーザーのパスワードを変更するには、古いパスワードと新しいパスワードの両方を `MembershipUser` オブジェクトの `ChangePassword` 方法に指定する必要がありますが、管理者は変更するためにユーザーのパスワードを知らなければなりません。

回避策の1つとして、まずユーザーのパスワードをリセットし、次のようなコードを使用して新しいパスワードに変更します。

[!code-vb[Main](recovering-and-changing-passwords-vb/samples/sample5.vb)]

このコードでは、まず*ユーザー名*に関する情報を取得します。これは、管理者が変更するパスワードを持つユーザーです。 次に、`ResetPassword` メソッドが呼び出されます。これにより、とユーザーに新しいランダムなパスワードが割り当てられます。 このランダムに生成されたパスワードは、メソッドによって返され、`resetPwd`変数に格納されます。 これで、ユーザーのパスワードがわかったので、`ChangePassword`を呼び出すことで変更できます。

問題は、`RequiresQuestionAndAnswer` が False になるようにメンバーシップシステムの構成が設定されている場合にのみ、このコードが機能することです。 `RequiresQuestionAndAnswer` が True の場合、アプリケーションの場合と同じように、`ResetPassword` メソッドにセキュリティの解答を渡す必要があります。そうしないと、例外がスローされます。

メンバーシップフレームワークがセキュリティの質問と回答を要求するように構成されているにもかかわらず、管理者がユーザーのパスワードを変更できることをクライアントが主張する場合は、次の3つの方法があります。

- 空中を捨てて、このことを行うことができないことをクライアントに通知します。
- `RequiresQuestionAndAnswer` を False に設定します。 これにより、安全性の低いアプリケーションが生成されます。 不正ユーザーが別のユーザーの電子メールの受信トレイにアクセスしたとします。 侵害されたユーザーが、昼食にアクセスしたり、ワークステーションをロックしたりしなかったか、公共のターミナルからメールにアクセスした可能性があり、サインアウトしていない可能性があります。どちらの場合も、不正ユーザーは `RecoverPassword.aspx` のページにアクセスして、ユーザーのユーザー名を入力できます。 その後、システムは、回復されたパスワードを、セキュリティの回答を求めるメッセージを表示せずに電子メールで送信します。
- メンバーシップフレームワークによって作成された抽象化レイヤーをバイパスし、SQL Server データベースを直接操作します。 メンバーシップスキーマには、ユーザーのパスワードを設定する `aspnet_Membership_SetPassword` という名前のストアドプロシージャが含まれており、そのタスクを実行するためにセキュリティの答えや古いパスワードは必要ありません。

これらのオプションはどれも特に魅力的なものではありませんが、開発者の生活がどのように行われるかということがあります。

3番目のアプローチを実装し、`Membership` と `MembershipUser` クラスをバイパスし、`SecurityTutorials` データベースに対して直接操作するコードを記述しました。

> [!NOTE]
> データベースを直接操作することにより、メンバーシップフレームワークによって提供されるカプセル化が砕かれます。 この決定により、`SqlMembershipProvider`に結び付け、コードの移植性が低下します。 さらに、メンバーシップスキーマが変更された場合、ASP.NET の将来のバージョンでは、このコードが期待どおりに動作しないことがあります。 この方法は回避策であり、ほとんどの回避策と同様に、ベストプラクティスの例ではありません。

コードにはいくつかの魅力的ビットがあり、非常に時間がかかります。 このため、このチュートリアルを詳しく見ていくことは避けたいと思います。 詳細については、このチュートリアルのコードをダウンロードし、`~/Administration/ManageUsers.aspx` のページを参照してください。 <a id="_msoanchor_5"> </a>[前のチュートリアル](building-an-interface-to-select-one-user-account-from-many-vb.md)で作成したこのページには、各ユーザーの一覧が表示されています。 GridView を更新して、`UserInformation.aspx` ページへのリンクを含め、選択したユーザーのユーザー名を querystring で渡しました。 [`UserInformation.aspx`] ページには、選択したユーザーとパスワードを変更するためのテキストボックスに関する情報が表示されます (図9を参照)。

新しいパスワードを入力し、2番目のテキストボックスで確認し、[ユーザーの更新] ボタンをクリックすると、ポストバック ensues と `aspnet_Membership_SetPassword` ストアドプロシージャが呼び出され、ユーザーのパスワードが更新されます。 この機能に関心を持っている読者は、コードについて理解を深め、パスワードが変更されたユーザーに電子メールを送信するように機能を拡張することをお勧めします。

[管理者がユーザーのパスワードを変更する ![](recovering-and-changing-passwords-vb/_static/image26.png)](recovering-and-changing-passwords-vb/_static/image25.png)

**図 9**: 管理者がユーザーのパスワードを変更[する (クリックすると、フルサイズの画像が表示](recovering-and-changing-passwords-vb/_static/image27.png)されます)

> [!NOTE]
> 現在、`UserInformation.aspx` ページは、パスワードをクリアまたはハッシュ形式で格納するようにメンバーシップフレームワークが構成されている場合にのみ機能します。 新しいパスワードを暗号化するためのコードは不足していますが、この機能を追加するように招待されています。 必要なコードを追加する方法は、デコンパイラのようなを使用して、.NET Framework 内のメソッドのソース[コードを調べる](http://www.aisto.com/roeder/dotnet/)ことです。まず、`SqlMembershipProvider` クラスの `ChangePassword` メソッドを調べます。 これは、パスワードのハッシュを作成するためのコードを記述するために使用した手法です。

## <a name="summary"></a>要約

ASP.NET には、ユーザーがパスワードを管理するのに役立つ2つのコントロールが用意されています。 PasswordRecovery コントロールは、パスワードを忘れたユーザーに役立ちます。 メンバーシップフレームワークの構成によっては、ユーザーは既存のパスワードまたはランダムに生成された新しいパスワードを電子メールで送信することになります。 ChangePassword コントロールを使用すると、ユーザーは自分のパスワードを更新できます。

Login および CreateUserWizard コントロールと同様に、PasswordRecovery と ChangePassword コントロールは、宣言型マークアップやコード行を記述しなくても、豊富なユーザーインターフェイスを表示します。 既定のユーザーインターフェイスがニーズを満たさない場合は、さまざまなスタイルのプロパティを使用してカスタマイズできます。 もう1つの方法として、コントロールのインターフェイスをテンプレートに変換して、さらに細かく制御することもできます。 バックグラウンドでは、これらのコントロールは Membership API を使用して、`MembershipUser` オブジェクトの `ResetPassword` と `ChangePassword` メソッドを呼び出します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ChangePassword コントロールのクイックスタート](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/changepassword.aspx)
- [PasswordRecovery コントロールのクイックスタート](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/passwordrecovery.aspx)
- [ASP.NET で電子メールを送信しています](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`System.Net.Mail` Faq](http://www.systemnetmail.com/)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者には、Michael Emmings と Suchi Erjee が含まれています。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](building-an-interface-to-select-one-user-account-from-many-vb.md)
> [次へ](unlocking-and-approving-user-accounts-vb.md)

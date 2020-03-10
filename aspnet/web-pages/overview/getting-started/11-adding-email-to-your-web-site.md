---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: ASP.NET Web ページ (Razor) サイトから電子メールを送信する |Microsoft Docs
author: Rick-Anderson
description: この章では、web サイトから自動電子メールメッセージを送信する方法について説明します。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 23e9717329525fb5a0ed505c9dc94505d4f9dbbe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515326"
---
# <a name="sending-email-from-an-aspnet-web-pages-razor-site"></a>ASP.NET Web ページ (Razor) サイトからの電子メールの送信

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ASP.NET Web ページ (Razor) を使用するときに web サイトから電子メールメッセージを送信する方法について説明します。
> 
> ここでは、次の内容について学習します。
> 
> - Web サイトから電子メールメッセージを送信する方法。
> - 電子メールメッセージにファイルを添付する方法。
> 
> この記事で導入された ASP.NET 機能は次のとおりです。
> 
> - `WebMail` ヘルパー。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 3
>   
> 
> このチュートリアルは ASP.NET Web ページ2でも動作します。

<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a>Web サイトから電子メールメッセージを送信する

Web サイトから電子メールを送信する必要がある理由はさまざまです。 ユーザーに確認メッセージを送信したり、ユーザーが自分で通知を送信したりすることがあります (たとえば、新しいユーザーが登録されている場合など)。`WebMail` ヘルパーを使用すると、簡単に電子メールを送信できます。

`WebMail` helper を使用するには、SMTP サーバーにアクセスできる必要があります。 (SMTP は*Simple Mail Transfer Protocol*を表します)。SMTP サーバーは、電子メールの送信側である受信者のサーバー &#8212;にメッセージを転送する電子メールサーバーです。 Web サイトのホスティングプロバイダーを使用する場合は、電子メールで設定されている可能性があります。また、SMTP サーバー名を通知できます。 企業ネットワーク内で作業している場合は、通常、管理者または IT 部門が、使用可能な SMTP サーバーに関する情報を提供することができます。 自宅で作業している場合は、SMTP サーバーの名前を知らせることができる通常の電子メールプロバイダーを使用してテストすることさえできます。 通常、次のものが必要です。

- SMTP サーバーの名前。
- ポート番号。 これは、ほぼ常に25です。 ただし、ISP では、ポート587を使用することが必要になる場合があります。 電子メールに secure sockets layer (SSL) を使用している場合は、別のポートが必要になることがあります。 電子メールプロバイダーに確認してください。
- 資格情報 (ユーザー名、パスワード)。

この手順では、2つのページを作成します。 最初のページには、テクニカルサポートフォームに入力しているかのように、ユーザーが説明を入力できるフォームがあります。 最初のページでは、2番目のページに情報を送信します。 2番目のページでは、code はユーザーの情報を抽出し、電子メールメッセージを送信します。 また、問題レポートが受信されたことを確認するメッセージも表示されます。

![[画像]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> この例を簡単にするために、コードは、使用するページで `WebMail` ヘルパー権限を初期化します。 ただし、実際の web サイトの場合は、このような初期化コードをグローバルファイルに配置することをお勧めします。これにより、web サイト内のすべてのファイルの `WebMail` ヘルパーが初期化されます。 詳細については、「 [ASP.NET Web ページのサイト全体の動作をカスタマイズする](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)」を参照してください。

1. 新しい web サイトを作成します。
2. *Emailrequest. cshtml*という名前の新しいページを追加し、次のマークアップを追加します。 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    Form 要素の `action` 属性が*ProcessRequest*に設定されていることに注意してください。 これは、現在のページに戻るのではなく、そのページにフォームが送信されることを意味します。
3. *ProcessRequest*という名前の新しいページを web サイトに追加し、次のコードとマークアップを追加します。   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    このコードでは、ページに送信されたフォームフィールドの値を取得します。 次に、`WebMail` ヘルパーの `Send` メソッドを呼び出して、電子メールメッセージを作成して送信します。 この場合、使用する値は、フォームから送信された値と連結するテキストで構成されます。

    このページのコードは `try/catch` ブロック内にあります。 何らかの理由で電子メールの送信が機能しない場合 (設定が正しくない場合など)、`catch` ブロック内のコードが実行され、発生したエラーに `errorMessage` 変数が設定されます。 (`try/catch` ブロックまたは `<text>` タグの詳細については、「 [Razor 構文を使用した ASP.NET Web ページプログラミングの概要](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors)」を参照してください)。

    ページの本文では、`errorMessage` 変数が空 (既定値) の場合、電子メールメッセージが送信されたことを示すメッセージがユーザーに表示されます。 `errorMessage` 変数が true に設定されている場合、メッセージの送信で問題が発生したことを示すメッセージがユーザーに表示されます。

    エラーメッセージが表示されるページの部分には、追加のテスト (`if(debuggingFlag)`) があります。 これは、電子メールの送信に問題がある場合に true に設定できる変数です。 `debuggingFlag` が true で、電子メールの送信で問題が発生した場合は、電子メールメッセージを送信しようとしたときに報告されたすべての ASP.NET を示す追加のエラーメッセージが表示されます。 公正な警告ですが、電子メールメッセージを送信できないときに ASP.NET が報告するエラーメッセージは一般にすることができます。 たとえば、ASP.NET が SMTP サーバーに接続できない場合 (たとえば、サーバー名にエラーが発生したため)、エラーは `Failure sending mail`になります。

    > [!NOTE] 
    > 
    > **重要**例外オブジェクト (コード内の`ex`) からエラーメッセージを受け取った場合、そのメッセージをユーザーに定期的に渡すこと*は避けて*ください。 多くの場合、例外オブジェクトには、ユーザーに表示されない情報や、セキュリティ上の脆弱性が含まれている可能性があります。 このコードには、エラーメッセージを表示するスイッチとして使用される変数 `debuggingFlag` が含まれています。また、変数が既定で false に設定されているのはなぜですか。 電子メールの送信に問題があり、デバッグが必要な場合に*のみ*、この変数を true に設定する必要があります (したがって、エラーメッセージが表示されます)。 問題を修正したら、`debuggingFlag` を false に戻します。

    コード内の次の電子メール関連の設定を変更します。

   - `your-SMTP-host` に、アクセス権のある SMTP サーバーの名前を設定します。
   - `your-user-name-here` を、SMTP サーバーアカウントのユーザー名に設定します。
   - `your-account-password` を SMTP サーバーアカウントのパスワードに設定します。
   - `your-email-address-here` を独自の電子メールアドレスに設定します。 これは、メッセージの送信元の電子メールアドレスです。 (一部の電子メールプロバイダーでは、別の `From` アドレスを指定することはできず、`From` アドレスとしてユーザー名が使用されます)。

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a>電子メール設定の構成
     > 
     > 場合によっては、SMTP サーバーやポート番号などに適切な設定があることを確認してください。 いくつかのヒントをご紹介します。
     > 
     > - SMTP サーバー名は、多くの場合 `smtp.provider.com` や `smtp.provider.net`のようなものです。 ただし、サイトをホスティングプロバイダーに発行する場合、その時点での SMTP サーバー名が `localhost`可能性があります。 これは、を発行し、サイトがプロバイダーのサーバーで実行されている場合に、電子メールサーバーがアプリケーションの観点からローカルである可能性があるためです。 このようにサーバー名を変更すると、公開プロセスの一部として SMTP サーバー名を変更する必要があることがあります。
     > - ポート番号は通常25です。 ただし、一部のプロバイダーでは、ポート587またはその他のポートを使用する必要があります。
     > - 適切な資格情報を使用していることを確認します。 サイトをホスティングプロバイダーに発行した場合は、プロバイダーが特別に指定した資格情報を電子メール用に使用します。 これらは、発行に使用する資格情報とは異なる場合があります。
     > - 場合によっては、資格情報をまったく必要としません。 個人用 ISP を使用して電子メールを送信している場合は、電子メールプロバイダーによって既に資格情報が知られている可能性があります。 発行後、ローカルコンピューターでテストする場合とは異なる資格情報を使用することが必要になる場合があります。
     > - 電子メールプロバイダーが暗号化を使用する場合は、`WebMail.EnableSsl` を `true`に設定する必要があります。
4. ブラウザーで*Emailrequest. cshtml*ページを実行します。 (実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。
5. 名前と問題の説明を入力し、 **[送信]** ボタンをクリックします。 *ProcessRequest*ページにリダイレクトされます。このページで、メッセージを確認し、電子メールメッセージを送信します。 

    ![[画像]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a>電子メールを使用したファイルの送信

また、電子メールメッセージに添付されているファイルを送信することもできます。 この手順では、テキストファイルと2つの HTML ページを作成します。 このテキストファイルを電子メールの添付ファイルとして使用します。

1. Web サイトに新しいテキストファイルを追加し、「 *myfile.txt*」という名前を入力します。
2. 次のテキストをコピーし、ファイルに貼り付けます。 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. *Sendfile. cshtml*という名前のページを作成し、次のマークアップを追加します。 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. *Processfile. cshtml*という名前のページを作成し、次のマークアップを追加します。 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. 例のコードで、次の電子メール関連の設定を変更します。

    - `your-SMTP-host` に、アクセス権のある SMTP サーバーの名前を設定します。
    - `your-user-name-here` を、SMTP サーバーアカウントのユーザー名に設定します。
    - `your-email-address-here` を独自の電子メールアドレスに設定します。 これは、メッセージの送信元の電子メールアドレスです。
    - `your-account-password` を SMTP サーバーアカウントのパスワードに設定します。
    - `target-email-address-here` を独自の電子メールアドレスに設定します。 (前と同様に、通常は他のユーザーに電子メールを送信しますが、テストの場合は自分で送信できます)。
6. ブラウザーで*Sendfile. cshtml*ページを実行します。
7. 名前、件名、添付するテキストファイルの名前 (*myfile.txt*) を入力します。
8. `Submit` ボタンをクリックします。 前と同様に、 *Processfile. cshtml*ページにリダイレクトされます。このページでは、メッセージを確認し、添付ファイルを含む電子メールメッセージを送信します。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

- [ASP.NET Web ページ (Razor) トラブルシューティング ガイド](https://go.microsoft.com/fwlink/?LinkId=253001)
- [簡易メール転送プロトコル](https://msdn.microsoft.com/library/aa480435.aspx)
- [ASP.NET Web ページのサイト全体の動作のカスタマイズ](https://go.microsoft.com/fwlink/?LinkId=202906)

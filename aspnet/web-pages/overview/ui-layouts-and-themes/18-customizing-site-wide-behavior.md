---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: ASP.NET Web ページ (Razor) サイトのサイト全体の動作をカスタマイズする |Microsoft Docs
author: Rick-Anderson
description: この章では、ページだけではなく、web サイト全体またはフォルダー全体に対して設定を行う方法について説明します。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: f05e05f725d9209bce283ce18659ae5efe4de2ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515248"
---
# <a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a>ASP.NET Web ページ (Razor) サイトのサイト全体の動作のカスタマイズ

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ASP.NET Web ページ (Razor) web サイトのページに対してサイト側の設定を行う方法について説明します。
> 
> ここでは、次の内容について学習します。
> 
> - サイト内のすべてのページに対して値 (グローバル値またはヘルパー設定) を設定できるコードを実行する方法。
> - フォルダー内のすべてのページの値を設定できるコードを実行する方法。
> - ページが読み込まれる前と後にコードを実行する方法について説明します。
> - 中央のエラーページにエラーを送信する方法。
> - フォルダー内のすべてのページに認証を追加する方法
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 2
> - WebMatrix 3
> - ASP.NET Web ヘルパーライブラリ (NuGet パッケージ)
>   
> 
> このチュートリアルでは、ASP.NET Web ヘルパーライブラリを使用できない点を除いて、ASP.NET Web ページ3と Visual Studio 2013 (または Web 用の Visual Studio Express 2013) でも動作します。

<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a>ASP.NET Web ページの Web サイトのスタートアップコードを追加する

ASP.NET Web ページに記述するコードの大部分では、そのページに必要なすべてのコードを個別のページに含めることができます。 たとえば、ページが電子メールメッセージを送信する場合、その操作のすべてのコードを1ページにまとめることができます。 これには、電子メールの送信 (SMTP サーバーの場合) および電子メールメッセージの送信の設定を初期化するコードを含めることができます。

ただし、状況によっては、サイトのページが実行される前にコードを実行することが必要になる場合があります。 これは、サイト内の任意の場所 (*グローバル値*と呼ばれます) で使用できる値を設定する場合に便利です。たとえば、一部のヘルパーでは、電子メールの設定やアカウントキーなどの値を指定する必要があります。 これらの設定をグローバル値に保持すると便利な場合があります。

これを行うには、サイトのルートに *\_該当*という名前のページを作成します。 このページが存在する場合は、サイトのページが最初に要求されたときに実行されます。 そのため、グローバル値を設定するコードを実行することをお勧めします。 ( *\_該当*にはアンダースコアプレフィックスが付いているため、ユーザーが直接要求した場合でも、ASP.NET はページをブラウザーに送信しません。)

次の図は、 *\_該当*ページの動作を示しています。 ページに対して要求が送信され、それがサイト内のいずれかのページの最初の要求である場合、ASP.NET は最初に、 *\_該当*ページが存在するかどうかを確認します。 その場合は、 *\_該当*ページ内のすべてのコードが実行され、要求されたページが実行されます。

![[画像]](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a>Web サイトのグローバル値を設定する

1. WebMatrix web サイトのルートフォルダーに、 *\_該当*という名前のファイルを作成します。 ファイルは、サイトのルートにある必要があります。
2. 既存のコンテンツを次の内容に置き換えます。 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    このコードは `AppState` ディクショナリに値を格納します。このディクショナリは、サイト内のすべてのページで自動的に使用できます。 *\_該当*ファイルにマークアップがないことに注意してください。 このページでコードが実行され、最初に要求されたページにリダイレクトされます。

    > [!NOTE]
    > *\_該当*ファイルにコードを配置する場合は注意してください。 *\_該当*ファイルのコードでエラーが発生した場合、web サイトは開始されません。
3. ルートフォルダーに、 *AppName. cshtml*という名前の新しいページを作成します。
4. 既定のマークアップとコードを次のコードに置き換えます。 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    このコードは、 *\_該当*ページで設定した `AppState` オブジェクトから値を抽出します。
5. ブラウザーで*AppName*ページを実行します。 (実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。ページにグローバル値が表示されます。 

    ![[画像]](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a>ヘルパーの値の設定

*\_該当*ファイルは、サイトで使用するヘルパーの値を設定し、初期化することをお勧めします。 一般的な例としては、`WebMail` ヘルパーの電子メール設定と、`ReCaptcha` ヘルパーの秘密キーと公開キーがあります。 このような場合は、 *\_該当*で値を1回設定すると、サイト内のすべてのページに対して既に設定されています。

この手順では、`WebMail` 設定をグローバルに設定する方法について説明します。 (`WebMail` ヘルパーの使用方法の詳細については、「 [ASP.NET Web ページサイトへの電子メールの追加](../getting-started/11-adding-email-to-your-web-site.md)」を参照してください)。

1. 「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだ追加していない場合)。
2. *\_該当*ファイルをまだ持っていない場合は、web サイトのルートフォルダーに *\_該当*という名前のファイルを作成します。
3. 次の `WebMail` 設定を *\_該当*ファイルに追加します。 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    コード内の次の電子メール関連の設定を変更します。

   - `your-SMTP-host` に、アクセス権のある SMTP サーバーの名前を設定します。
   - `your-user-name-here` を、SMTP サーバーアカウントのユーザー名に設定します。
   - `your-account-password` を SMTP サーバーアカウントのパスワードに設定します。
   - `your-email-address-here` を独自の電子メールアドレスに設定します。 これは、メッセージの送信元の電子メールアドレスです。 (一部の電子メールプロバイダーでは、別の `From` アドレスを指定することはできず、`From` アドレスとしてユーザー名が使用されます)。

     SMTP 設定の詳細については、「 [ASP.NET Web ページ (razor) トラブルシューティングガイド](https://go.microsoft.com/fwlink/?LinkId=253001)」の「 [ASP.NET Web ページ (razor) サイトから](https://go.microsoft.com/fwlink/?LinkID=202899)電子メールを送信する」と「電子[メールの送信に関する問題](https://go.microsoft.com/fwlink/?LinkId=253001#email)」の「電子メール[設定の構成](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings)」を参照してください。
4. *\_該当*ファイルを保存して閉じます。
5. Web サイトのルートフォルダーに、 *Testemail. cshtml*という名前の新しいページを作成します。
6. 既存のコンテンツを次の内容に置き換えます。 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. ブラウザーで*Testemail. cshtml*ページを実行します。
8. フィールドに電子メールメッセージを送信するように入力し、 **[送信]** をクリックします。
9. メールを確認して、メッセージが表示されていることを確認してください。

この例の重要な部分は、通常は変更しない設定 (SMTP サーバーの名前や電子メールの資格情報など) が *\_該当*ファイルに設定されていることです。 このようにして、電子メールを送信する各ページで再度設定する必要はありません。 (何らかの理由で、これらの設定を変更する必要がある場合は、ページで個別に設定できます)。このページでは、通常、電子メールメッセージの受信者や本文など、毎回変更される値のみを設定します。

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a>フォルダー内のファイルの前後にコードを実行する

*\_該当*を使用して、サイト内のページの前にコードを記述するのと同様に、特定のフォルダー内の任意のページが実行される前 (および後) に実行されるコードを記述することができます。 これは、フォルダー内のすべてのページに対して同じレイアウトページを設定する場合や、フォルダー内のページを実行する前にユーザーがログインしていることを確認する場合などに便利です。

特定のフォルダーのページでは、 *\_PageStart. cshtml*という名前のファイルにコードを作成できます。 次の図は、 *\_PageStart. cshtml*ページがどのように動作するかを示しています。 ページに対して要求が送信されると、ASP.NET は最初に、 *\_該当*ページを確認し、それを実行します。 次に、ASP.NET ページがあるか *\_* どうかを確認し、存在する場合はそれを実行します。 次に、要求されたページを実行します。

*\_PageStart. cshtml*ページ内で、`RunPage` メソッドを含めることで、要求されたページの実行を処理する場所を指定できます。 これにより、要求されたページが実行される前にコードを実行してから、後で再度実行できます。 `RunPage`を指定しない場合は、 *\_pagestart*すべてのコードが実行され、要求されたページが自動的に実行されます。

![[画像]](18-customizing-site-wide-behavior/_static/image3.jpg)

ASP.NET を使用すると *\_PageStart. cshtml*ファイルの階層を作成できます。 サイトのルートと任意のサブフォルダーに、 *\_PageStart. cshtml*ファイルを配置できます。 ページが要求されると、最上位レベル (サイトルートに最も近い) の *\_PageStart. cshtml*ファイルが実行され、その後、次のサブフォルダーにある *\_pagestart. cshtml*ファイルが実行されます。その後、要求されたページを含むフォルダーに要求が到達するまで、サブフォルダーの構造が下になります。 適用可能なすべての *\_PageStart. cshtml*ファイルが実行されると、要求されたページが実行されます。

たとえば、次のような *\_PageStart. cshtml*ファイルと*既定の cshtml*ファイルの組み合わせがあるとします。

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

*/Myfolderを*実行すると、次のように表示されます。

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a>フォルダー内のすべてのページに対して初期化コードを実行する

*PageStart. cshtml*ファイルを\_には、1つのフォルダー内のすべてのファイルに対して同じレイアウトページを初期化することをお勧めします。

1. ルートフォルダーに、 *Initpages*という名前の新しいフォルダーを作成します。
2. Web サイトの*Initpages*フォルダーで、 *\_pagestart. cshtml*という名前のファイルを作成し、既定のマークアップとコードを次のコードに置き換えます。 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. Web サイトのルートで、 *Shared*という名前のフォルダーを作成します。
4. *共有*フォルダーで *\_Layout1*という名前のファイルを作成し、既定のマークアップとコードを次のコードに置き換えます。 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. *Initpages*フォルダーで、 *Content1*という名前のファイルを作成し、既存のコンテンツを次の内容に置き換えます。 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. *Initpages*フォルダーで、 *Content2*という名前の別のファイルを作成し、既定のマークアップを次のように置き換えます。 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. ブラウザーで*Content1*を実行します。 

    ![[画像]](18-customizing-site-wide-behavior/_static/image4.jpg)

    *Content1*ページを実行すると、 *\_pagestart. cshtml*ファイルが `Layout` 設定され、`PageData["MyBackground"]` も色に設定されます。 *Content1*では、レイアウトと色が適用されます。
8. ブラウザーで*Content2*を表示します。 

    レイアウトは同じです。どちらのページも、 *\_PageStart. cshtml*で初期化されたのと同じレイアウトページと色を使用するためです。

## <a name="using-_pagestartcshtml-to-handle-errors"></a>\_PageStart. cshtml を使用してエラーを処理する

*\_PageStart. cshtml*ファイルのもう1つの使用方法は、フォルダー内の任意の*cshtml*ページで発生する可能性があるプログラミングエラー (例外) を処理する方法を作成することです。 この例では、これを行う1つの方法を示します。

1. ルートフォルダーに、 *Initcatch*という名前のフォルダーを作成します。
2. Web サイトの*Initcatch*フォルダーで、 *\_pagestart. cshtml*という名前のファイルを作成し、既存のマークアップとコードを次のコードに置き換えます。 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    このコードでは、`try` ブロック内で `RunPage` メソッドを呼び出すことによって、要求されたページを明示的に実行しようとしています。 要求されたページで何らかのプログラミングエラーが発生した場合は、`catch` ブロック内のコードが実行されます。 この場合、コードはページ (*エラー cshtml*) にリダイレクトし、URL の一部としてエラーが発生したファイルの名前を渡します。 (ページはすぐに作成します)。
3. Web サイトの*Initcatch*フォルダーで、 *Exception. cshtml*という名前のファイルを作成し、既存のマークアップとコードを次のコードに置き換えます。 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    この例では、このページで行っていることは、存在しないデータベースファイルを開こうとすると意図的にエラーになります。
4. ルートフォルダーで、「 *Error. cshtml* 」という名前のファイルを作成し、既存のマークアップとコードを次のコードに置き換えます。 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    このページでは、式 `@Request["source"]` が URL から値を取得して表示します。
5. ツールバーの **[保存]** をクリックします。
6. ブラウザーで*例外を*実行します。 

    ![[画像]](18-customizing-site-wide-behavior/_static/image5.jpg)

    *例外*が発生したため、 *\_pagestart. Cshtml*ページが*エラーの cshtml*ファイルにリダイレクトされ、メッセージが表示されます。

    例外の詳細については、「 [Razor 構文を使用した ASP.NET Web ページプログラミングの概要](https://go.microsoft.com/fwlink/?LinkID=251587)」を参照してください。

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-_pagestartcshtml-to-restrict-folder-access"></a>\_PageStart. cshtml を使用してフォルダーアクセスを制限する

また、 *\_PageStart. cshtml*ファイルを使用して、フォルダー内のすべてのファイルへのアクセスを制限することもできます。

1. WebMatrix で、 **[テンプレートからのサイト]** オプションを使用して新しい web サイトを作成します。
2. 使用可能なテンプレートから、 **[スターターサイト]** を選択します。
3. ルートフォルダーに、認証*Atedcontent*という名前のフォルダーを作成します。
4. [認証*Atedcontent* ] フォルダーで、 *\_pagestart. cshtml*という名前のファイルを作成し、既存のマークアップとコードを次のコードに置き換えます。 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    このコードは、フォルダー内のすべてのファイルがキャッシュされるのを防ぐことから始まります。 (これは、パブリックコンピューターのようなシナリオで、1人のユーザーのキャッシュされたページを次のユーザーが使用できないようにする場合に必要です)。次に、ユーザーがフォルダー内のページを表示する前に、サイトにサインインしているかどうかを確認します。 ユーザーがサインインしていない場合、コードはログインページにリダイレクトされます。 ログインページでは、`ReturnUrl`という名前のクエリ文字列値を指定した場合に、最初に要求されたページにユーザーを返すことができます。
5. "/" という名前の認証の*コンテンツ*フォルダーに新しいページを作成*します。*
6. 既定のマークアップを次のように置き換えます。  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. ブラウザーで、[ *Cshtml]* を実行します。 このコードにより、ログインページにリダイレクトされます。 ログインする前に登録する必要があります。 登録してログインすると、ページに移動してその内容を表示できます。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

[Razor 構文を使用した ASP.NET Web ページプログラミングの概要](https://go.microsoft.com/fwlink/?LinkID=251587)

---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET Web ページ (Razor) トラブルシューティングガイド |Microsoft Docs
author: Rick-Anderson
description: この記事では、ASP.NET Web ページ (Razor) といくつかの提案された解決策を使用する場合に発生する可能性がある問題について説明します。 ソフトウェアバージョン ASP.NET Web Pag...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: fc03767c16f46c1e282d24ee3a7df2409a7c38bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473380"
---
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a>ASP.NET Web Pages (Razor) トラブルシューティング ガイド (英語)

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ASP.NET Web ページ (Razor) といくつかの提案された解決策を使用する場合に発生する可能性がある問題について説明します。
> 
> ## <a name="software-versions"></a>ソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 3
>   
> 
> このチュートリアルは ASP.NET Web ページ2および ASP.NET Web ページ1.0 でも動作します。

このトピックには、次のセクションが含まれます。

- [実行中のページに関する問題](#Issues_Running_.cshtml_Pages)
- [Razor コードに関する問題](#IssuesWithRazorCode)
- [セキュリティとメンバーシップに関する問題](#membership)
- [電子メールの送信に関する問題](#email)
- [その他のリソース](#AdditionalResources)

一般的な質問については、「 [ASP.NET Web ページ (Razor)](https://go.microsoft.com/fwlink/?LinkId=253000)に関する FAQ」を参照してください。

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a>実行中のページに関する問題

さまざまな問題により、 *cshtml*および*vbhtml*ページが正常に実行されない可能性があります。 ここでは、一般的なエラーメッセージと考えられる原因を示します。

### <a name="http-error-403---forbidden-access-is-denied"></a>HTTP エラー 403-許可されていません: アクセスが拒否されました

*指定した資格情報を使用して、このディレクトリまたはページを表示するアクセス許可がありません。*

このエラーは、サーバーで正しいバージョンの .NET Framework が実行されていない場合に発生する可能性があります。 サーバー (ローカルまたはリモート) を実行しているコンピューターに、少なくとも .NET Framework 4 がインストールされていることを確認します。 また、アプリケーション自体が適切なバージョンを実行するように構成されていることを確認します。

WebMatrix での作業中にこの問題がローカルに表示される場合は、**サイト**ワークスペースをクリックし、treeview で **[設定]** をクリックします。 **[.NET Framework バージョンの選択**] ボックスの一覧で、 **[.Net 4 (統合)]** を選択します。 このバージョンが既に設定されている場合は、管理者として WebMatrix を実行してみてください。

Web サイトのルートに少なくとも1つの*cshtml*ファイルがあることを確認します。

Web サーバーがリモートサーバー上にあるときにこのエラーが表示される場合は、サーバー管理者に問い合わせてください。 サーバーに .NET Framework 4 以降がインストールされていることを確認します。 また、そのバージョンの the.NET Framework を使用するように構成されたアプリケーションプールでアプリケーションが実行されていることを確認します。

サーバーを制御している場合は、正しいバージョンの .NET Framework が実行されていることを確認してください。 `aspnet_regiis -iru` のコマンドを実行して、インストールの修復を試みることもできます。 (たとえば、.NET Framework をインストールした後に IIS をインストールした場合、IIS は ASP.NET ページを実行するように正しく構成されません)。詳細については、「 [ASP.NET IIS Registration Tool (Aspnet\_iis 登録ツール)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)」を参照してください。

### <a name="http-error-40314---forbidden"></a>HTTP エラー 403.14-許可されていません

*Web サーバーは、このディレクトリの内容を一覧表示しないように構成されています。*

このエラー*は、保護*されているリソース (web.config ファイルなど) を要求した場合、または保護されているフォルダー ( *app\_データ*や*アプリ\_コード*など) にある場合に発生する可能性があります。

### <a name="http-error-40417---not-found"></a>HTTP エラー 404.17-見つかりません

*要求されたコンテンツはスクリプトであり、静的ファイルハンドラーによって処理されません。*

このエラーは、サーバーが .NET Framework 4 以降を使用するように正しく構成されていないために、`@{ }` ブロックのコードを認識しない場合に発生する可能性があります。 前の「 *HTTP エラー 403-許可されていません: アクセスが拒否されまし*た」の説明を参照してください。

### <a name="http-error-4047---not-found"></a>HTTP エラー 404.7-見つかりません

*要求フィルターモジュールは、ファイル拡張子を拒否するように構成されています*

このエラーは、サーバーで*cshtml*または*vbhtml*拡張子が明示的にブロックされている場合に発生する可能性があります。 この問題が発生するのは、拡張子が含まれていない Url は機能しますが、拡張子が*cshtml*または*vbhtml*の url は機能しないということです。 解決策として、サイトの*web.config*ファイルにある拡張機能を再度有効にすることが考えられます。 次の例は、拡張子を有効にする方法を示し*ています*。

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a>HTTP エラー 404.8-見つかりません

*要求フィルターモジュールは、hiddenSegment セクションを含む URL 内のパスを拒否するように構成されています。*

このエラー*は、保護*されているリソース (web.config ファイルなど) を要求した場合、または保護されているフォルダー ( *app\_データ*や*アプリ\_コード*など) にある場合に発生する可能性があります。

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a>この種類のページは提供されていません ('/' アプリケーションのサーバーエラー)

HTTP エラー404.17 については、前述の説明を参照してください。

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a>Razor コードに関する問題

### <a name="the-name-class-does-not-exist-in-the-current-context"></a>名前 '*class*' は現在のコンテキストに存在しません

多くの場合、このエラーが表示される理由は、`class` がヘルパーを参照するが、ヘルパーがインストールされていないことです。 たとえば、ヘルパーを使用しようとしても、NuGet からパッケージをインストールしていない場合は、このエラーが表示されます。 WebMatrix のギャラリーを使用して、ヘルパーを検索してインストールします。

ヘルパーがインストールされていても、ページがそれを認識しない場合は、`using` ステートメントをコードに追加してみてください。 `using` ステートメントで、ヘルパーを含む名前空間を参照します。 たとえば、ASP.NET Web ヘルパーパッケージに含まれる基本的なヘルパーは、`System.Web.Helpers` 名前空間にあります。 ヘルパーを使用するページの先頭に、次の行を追加します。

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a>セキュリティとメンバーシップに関する問題

ASP.NET Web ページ (Razor) で組み込みのセキュリティ (メンバーシップ) システムを使用している場合は、次の問題が発生する可能性があります。

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a>このメソッドを呼び出すには、"ExtendedMembershipProvider" プロパティが "" のインスタンスである必要があります。

このエラーは、`AspNetSqlMembershipProvider` クラスが構成されていないことを示している可能性があります。 (症状として、サイトはローカルで正常に動作しますが、ホスティングプロバイダーのサーバーに公開すると、このエラーがスローされます)。この問題の解決策の1つは、サイトの*web.config*ファイルに次の内容を追加して単純なメンバーシップを明示的に有効にすることです。

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a>電子メールの送信に関する問題

電子メールの送信に問題があると、デバッグが困難になることがあります。 最初の問題は、SMTP サーバーに接続できないことです。 接続に成功した場合、ASP.NET はメッセージを SMTP サーバーに渡します。 ただし、メッセージ自体には、SMTP サーバーから送信されないという問題があります。

アプリケーションが電子メールを正常に送信できない場合は、次のことを試してください。

- SMTP サーバー名は、多くの場合 `smtp.provider.com` や `smtp.provider.net`のようなものです。 ただし、サイトをホスティングプロバイダーに発行する場合、その時点での SMTP サーバー名が `localhost`可能性があります。 この状況は、発行後にサイトがプロバイダーのサーバーで実行されている場合に発生します。そのため、SMTP サーバーは、アプリケーションの観点からローカルに配置されている可能性があります。 このようにサーバー名を変更すると、発行プロセスの一部として SMTP サーバー名を変更する必要があるということが考えられます。
- ポート番号は通常25です。 ただし、一部のプロバイダーでは、ポート587またはその他のポートを使用する必要があります。 使用するポート番号を SMTP サーバーの所有者に確認してください。
- 適切な資格情報を使用していることを確認します。 サイトをホスティングプロバイダーに発行した場合は、プロバイダーが特別に指定した資格情報を電子メール用に使用します。 これらの資格情報は、発行に使用する資格情報とは異なる場合があります。
- 場合によっては、資格情報をまったく必要としません。 個人用 ISP を使用して電子メールを送信している場合は、電子メールプロバイダーによって既に資格情報が知られている可能性があります。 発行後、ローカルコンピューターでテストする場合とは異なる資格情報を使用することが必要になる場合があります。
- 電子メールプロバイダーが暗号化を使用する場合は、`WebMail.EnableSsl` を `true`に設定します。

電子メールの送信中にエラーが発生した場合は、標準の ASP.NET エラーメッセージが表示されることがあります。これは次のようになります。

![電子メールに問題があるときに ASP.NET エラーメッセージを表示する](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

次の例に示すように、`try-catch` ブロックを使用して、電子メールの送信に関する問題をデバッグすることもできます。 `try-catch` ブロックを使用する場合、ASP.NET では標準エラーメッセージは表示されません。 代わりに、ブロックの `catch` 部分でエラーをキャプチャできます。

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

`your-SMTP-server-name`の適切な値に置き換えます。 このように表示されるエラーメッセージには、次のようなものがあります。

- *メールの送信に失敗します。*

    または

    *接続されたパーティが一定期間内に適切に応答しなかったか、接続されたホストが応答に失敗したために確立された接続に失敗したため、接続に失敗しました*

    このエラーは通常、アプリケーションが SMTP サーバーに接続できなかったことを示します。 サーバー名とポート番号を確認します。
- *メールボックスを使用できません。サーバーの応答: 5.1.0 &lt;someuser@invaliddomain&gt; 送信者が拒否しました: 送信者ドメインが無効です*

    このメッセージは、`From` アドレスが正しくないか、または存在しないことを示している可能性があります。
- *指定された文字列は、電子メールアドレスに必要な形式ではありません。*

    このエラーは、`To` または `From` プロパティの値が電子メールアドレスとして認識されないことを示している可能性があります。 (ASP.NET のように、電子メールアドレスが有効であることを確認することはできません。 *name@domain.com* のように、正しい形式である必要があります)。

> [!NOTE]
> ページをライブサイトに発行する前に、エラー (`@errorMessage`) を表示するマークアップを削除します。 サーバーから取得したエラーメッセージをユーザーに表示させることはお勧めしません。

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>その他のリソース

[ASP.NET Web ページ (Razor) のよくあるご質問](https://go.microsoft.com/fwlink/?LinkId=253000)

ASP.NET web サイトの[WebMatrix と ASP.NET Web ページ](https://forums.asp.net/1224.aspx/1?WebMatrix)フォーラム

---
uid: mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
title: ASP.NET MVC と Web Pages の XSRF/CSRF 防止 |Microsoft Docs
author: Rick-Anderson
description: クロスサイト要求偽造 (XSRF または CSRF とも呼ばれます) は、悪意のある web サイトが interacti に影響する可能性がある web ホストアプリケーションに対する攻撃です。
ms.author: riande
ms.date: 03/14/2013
ms.assetid: aadc5fa4-8215-4fc7-afd5-bcd2ef879728
msc.legacyurl: /mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
msc.type: authoredcontent
ms.openlocfilehash: 6fcfcda5b95e5844f7d357ac0cbb6d1fd2e215ac
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445778"
---
# <a name="xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages"></a>ASP.NET MVC と Web ページの XSRF/CSRF 防止

[Rick Anderson]((https://twitter.com/RickAndMSFT))

> クロスサイト要求偽造 (XSRF または CSRF とも呼ばれます) は、web でホストされるアプリケーションに対する攻撃であり、悪意のある web サイトが、クライアントブラウザーとそのブラウザーによって信頼されている web サイトとの間の対話に影響を与える可能性があります。 Web ブラウザーは web サイトへのすべての要求で認証トークンを自動的に送信するため、これらの攻撃が可能になります。 標準的な例として、ASP などの認証 cookie があります。NET のフォーム認証チケット。 ただし、永続的な認証メカニズム (Windows 認証、基本など) を使用する web サイトは、これらの攻撃の対象にすることができます。
> 
> XSRF 攻撃はフィッシング攻撃とは異なります。 フィッシング攻撃では、被害者との対話が必要です。 フィッシング攻撃では、悪意のある web サイトがターゲット web サイトを模倣し、攻撃者に機密情報を提供することはできません。 XSRF 攻撃では、多くの場合、標的からの相互作用は必要ありません。 攻撃者は、ブラウザーによって、関連するすべての cookie が送信先の web サイトに自動的に送信されます。
> 
> 詳細については、 [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page)(owasp) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))を参照してください。

## <a name="anatomy-of-an-attack"></a>攻撃の構造

XSRF 攻撃を実行するには、いくつかのオンラインバンキングトランザクションを実行する必要があるユーザーを考えてみます。 このユーザーは、最初に WoodgroveBank.com にアクセスしてログインします。この時点で、応答ヘッダーには自分の認証クッキーが含まれます。

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample1.cmd)]

認証 cookie はセッション cookie であるため、ブラウザープロセスが終了すると、ブラウザーによって自動的にクリアされます。 ただし、その時点までは、ブラウザーには、WoodgroveBank.com に対する各要求に cookie が自動的に含まれます。 これで、ユーザーは $1000 を別のアカウントに転送するようになりました。そのため、銀行のサイトにフォームを入力すると、ブラウザーはこの要求をサーバーに対して行います。

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample2.cmd)]

この操作は副作用がある (金額トランザクションを開始する) ため、この操作を開始するために、銀行のサイトで HTTP POST の要求が選択されています。 サーバーは、要求から認証トークンを読み取り、現在のユーザーのアカウント番号を検索し、十分な資金が存在することを確認してから、対象のアカウントにトランザクションを開始します。

オンラインバンキングを完了すると、ユーザーが銀行のサイトから移動し、web 上の他の場所にアクセスします。 これらのサイトのいずれか– fabrikam.com – &lt;iframe&gt;内に埋め込まれたページに次のマークアップを含めます。

[!code-html[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample3.html)]

これにより、ブラウザーは次の要求を行います。

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample4.cmd)]

攻撃者は、ユーザーがターゲット web サイトに有効な認証トークンを持っている可能性があるという事実を悪用しています。また、Javascript の小さなスニペットを使用して、ブラウザーがターゲットサイトへの HTTP POST を自動的に行うようにしています。 認証トークンがまだ有効である場合、銀行のサイトでは、攻撃者が選択したアカウントへの $250 の転送を開始します。

### <a name="ineffective-mitigations"></a>効率的でない軽減策

上記のシナリオでは、WoodgroveBank.com が SSL 経由でアクセスされ、SSL のみの認証クッキーが攻撃を阻止するのに十分ではないという事実に注意してください。 攻撃者は &lt;フォーム&gt; 要素で[URI スキーム](http://en.wikipedia.org/wiki/URI_scheme)(https) を指定できます。また、これらの cookie が目的のターゲットの URI スキームと一致する限り、ブラウザーは引き続きターゲットサイトに unexpired cookie を送信します。

信頼されたサイトのみにアクセスしても安全なオンラインに保つことができるので、ユーザーは信頼されていないサイトにアクセスしないようにする必要があります。 これには真実がありますが、残念ながらこのアドバイスは常に実用的であるとは限りません。 ユーザーは、ローカルニュースサイト ConsolidatedMessenger を "信頼" している可能性があります。 ConsolidatedMessenger.com を使用してそのサイトにアクセスしますが、そのサイトには、fabrikam.com で実行されていたものと同じコードスニペットを注入できる XSS 脆弱性があります。

受信要求にドメインを参照する[Referer ヘッダー](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14)があることを確認できます。 これにより、サードパーティのドメインから知らないうちに送信された要求を停止します。 ただし、プライバシー上の理由からブラウザーの Referer ヘッダーを無効にするユーザーもいれば、攻撃者が特定の安全でないソフトウェアがインストールされている場合は、そのヘッダーを偽装することがあります。 [Referer ヘッダー](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14)の検証は、XSRF 攻撃を防ぐための安全な方法とは見なされません。

## <a name="web-stack-runtime-xsrf-mitigations"></a>Web Stack Runtime XSRF の緩和

ASP.NET Web Stack ランタイムは、[シンクロナイザートークンパターン](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#synchronizer-token-pattern)のバリエーションを使用して、XSRF 攻撃に対する防御を行います。 シンクロナイザートークンパターンの一般的な形式では、2つの XSRF トークンが (認証トークンに加えて) 各 HTTP POST と共にサーバーに送信されます。1つは cookie として、もう1つはフォーム値です。 ASP.NET ランタイムによって生成されるトークン値は、攻撃者によって決定的または予測可能ではありません。 トークンが送信されると、サーバーでは、両方のトークンが比較チェックに合格した場合にのみ、要求を続行できます。

XSRF 要求確認*セッショントークン*は、HTTP クッキーとして格納され、現在、ペイロードに次の情報が含まれています。

- ランダムな128ビット識別子で構成されるセキュリティトークン。   
 次の図は、Internet Explorer の F12 開発者ツールで表示される XSRF request 確認セッショントークンを示しています (これは現在の実装であり、変更される可能性があります)。

![](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/_static/image1.png)

*フィールドトークン*は `<input type="hidden" />` として格納され、ペイロードに次の情報が含まれます。

- ログインしているユーザーのユーザー名 (認証されている場合)。
- [Iアンチ Forgeryadditionaldataprovider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)によって提供される追加データ。

XSRF トークンのペイロードは暗号化および署名されるので、ツールを使用してトークンを確認するときにユーザー名を表示することはできません。 Web アプリケーションが ASP.NET 4.0 をターゲットにしている場合、暗号化サービスは、 [MachineKey. Encode](https://msdn.microsoft.com/library/system.web.security.machinekey.encode.aspx)ルーチンによって提供されます。 Web アプリケーションが ASP.NET 4.5 以降を対象としている場合、暗号化サービスは、パフォーマンス、拡張性、およびセキュリティを向上させるために、 [MachineKey. Protect](https://msdn.microsoft.com/library/system.web.security.machinekey.protect(v=vs.110))ルーチンによって提供されます。 詳細については、次のブログ投稿を参照してください。

- [ASP.NET 4.5, pt. 1 での暗号化の強化](https://blogs.msdn.com/b/webdev/archive/2012/10/22/cryptographic-improvements-in-asp-net-4-5-pt-1.aspx)
- [ASP.NET 4.5、pt. 2 での暗号化の強化](https://blogs.msdn.com/b/webdev/archive/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2.aspx)
- [ASP.NET 4.5、pt. 3 での暗号化の強化](https://blogs.msdn.com/b/webdev/archive/2012/10/24/cryptographic-improvements-in-asp-net-4-5-pt-3.aspx)

## <a name="generating-the-tokens"></a>トークンの生成

XSRF トークンを生成するには、Razor ページから MVC ビューまたは @AntiForgery.GetHtml() から[@Html.AntiForgeryToken](https://msdn.microsoft.com/library/dd470175.aspx)メソッドを呼び出します。 ランタイムは、次の手順を実行します。

1. 現在の HTTP 要求に XSRF セッショントークン (XSRF cookie \_\_RequestVerificationToken) が既に含まれている場合は、セキュリティトークンがそこから抽出されます。 HTTP 要求に XSRF セッショントークンが含まれていない場合、またはセキュリティトークンの抽出に失敗した場合は、新しいランダムな XSRF トークンが生成されます。
2. 上記の手順 (1) からのセキュリティトークンと、現在ログインしているユーザーの id を使用して、XSRF フィールドトークンが生成されます。 (ユーザー id を決定する方法の詳細については、以下の「 **[特別なサポートを使用するシナリオ](#_Scenarios_with_special)** 」を参照してください)。さらに、 [Iアンチ Forgeryadditionaldataprovider](https://msdn.microsoft.com/library/jj158328(v=vs.111).aspx)が構成されている場合、ランタイムはその[getadditionaldata](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.getadditionaldata(v=vs.111).aspx)メソッドを呼び出し、返された文字列をフィールドトークンに含めます。 (詳細については、「 **[構成と拡張機能](#_Configuration_and_extensibility)** 」を参照してください)。
3. 手順 (1) で新しい XSRF トークンが生成された場合、それを含む新しいセッショントークンが作成され、送信 HTTP cookies コレクションに追加されます。 手順 (2) のフィールドトークンは `<input type="hidden" />` 要素にラップされ、この HTML マークアップは `Html.AntiForgeryToken()` または `AntiForgery.GetHtml()`の戻り値になります。

## <a name="validating-the-tokens"></a>トークンの検証

受信した XSRF トークンを検証するために、開発者は自分の MVC アクションまたはコントローラーに[Validateアンチ Forgerytoken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(VS.108).aspx)属性を含めるか、または自分の Razor ページから `@AntiForgery.Validate()` を呼び出します。 ランタイムは、次の手順を実行します。

1. 受信セッショントークンとフィールドトークンが読み取られ、それぞれから抽出された XSRF トークンが読み取られます。 XSRF トークンは、生成ルーチンのステップごとに同一である必要があります (2)。
2. 現在のユーザーが認証されている場合、ユーザー名はフィールドトークンに格納されているユーザー名と比較されます。 ユーザー名が一致している必要があります。
3. [Iアンチ Forgeryadditionaldataprovider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)が構成されている場合、ランタイムは*validateadditionaldata*メソッドを呼び出します。 メソッドはブール値*true*を返す必要があります。

検証が成功した場合、要求は続行できます。 検証が失敗した場合、フレームワークは*Httpantiforgeryexception*をスローします。

## <a name="failure-conditions"></a>エラー条件

ASP.NET Web Stack Runtime v2 以降、検証中にスローされる*Httpantiforgeryexception*には、問題の原因に関する詳細情報が含まれています。 現在定義されているエラー条件は次のとおりです。

- セッショントークンまたはフォームトークンが要求に存在しません。
- セッショントークンまたはフォームトークンを読み取ることができません。 この原因として最も可能性が高いのは、一致しないバージョンの ASP.NET Web Stack ランタイムを実行しているファーム、または web.config の &lt;machineKey&gt; 要素がコンピューター間で異なるファームです。 Fiddler などのツールを使用して、XSRF トークンを使用して改ざんすることで、この例外を強制的に適用することができます。
- セッショントークンとフィールドトークンがスワップされました。
- セッショントークンとフィールドトークンに、一致しないセキュリティトークンが含まれています。
- フィールドトークン内に埋め込まれているユーザー名が、現在ログインしているユーザーのユーザー名と一致しません。
- *[Iアンチ Forgeryadditionaldataprovider. ValidateAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.validateadditionaldata(v=vs.111).aspx)* メソッドは*false*を返しました。

また、XSRF 施設では、トークンの生成または検証中に追加のチェックを実行することもできます。これらのチェック中にエラーが発生すると、例外がスローされる可能性があります。 詳細については、 [WIF/ACS/要求ベースの認証](#_WIF_ACS)と **[構成と拡張](#_Configuration_and_extensibility)** に関するセクションを参照してください。

<a id="_Scenarios_with_special"></a>

## <a name="scenarios-with-special-support"></a>特別なサポートがあるシナリオ

### <a name="anonymous-authentication"></a>匿名認証

XSRF システムには、匿名ユーザーの特別なサポートが含まれています *。* ここで、"anonymous" は、"anonymous" プロパティが*false*を返すユーザーとして定義されています。 シナリオには、ログインページへの XSRF 保護の提供 (ユーザーが認証される前) と、アプリケーションが*IIdentity*以外のメカニズムを使用してユーザーを識別するカスタム認証スキームが含まれます。

これらのシナリオをサポートするには、セッションとフィールドトークンが、ランダムに生成された128ビットの不透明な識別子であるセキュリティトークンによって結合されていることを思い出してください。 このセキュリティトークンは、サイトを移動するときに個々のユーザーのセッションを追跡するために使用されます。これにより、匿名識別子の目的が効果的に提供されます。 上記で説明した生成ルーチンと検証ルーチンのユーザー名の代わりに、空の文字列が使用されます。

<a id="_WIF_ACS"></a>

### <a name="wif--acs--claims-based-authentication"></a>WIF/ACS/要求ベースの認証

通常、.NET Framework に組み込まれている*IIdentity*クラスには、特定のアプリケーション内の特定のユーザーを一意に識別するのに十分な*IIdentity.Name*のプロパティがあります。 たとえば、 *FormsIdentity.Name*はメンバーシップデータベースに格納されているユーザー名 (そのデータベースに依存するすべてのアプリケーションに対して一意である) を返し、 *WindowsIdentity.Name*はユーザーのドメイン修飾 id を返します。 これらのシステムは認証のみを行います。また、アプリケーションに対してユーザーを*識別*します。

一方、クレームベースの認証では、必ずしも特定のユーザーを識別する必要はありません。 代わりに、 *ClaimsPrincipal*と*ClaimsIdentity*の種類は*クレーム*インスタンスのセットに関連付けられています。この場合、個々の要求は "18 歳以上の年齢" や "管理者" などになります。 ユーザーは必ずしも特定されていないため、ランタイムはこの特定のユーザーの一意の識別子として*ClaimsIdentity.Name*プロパティを使用できません。 チームは実際の例を見てきました。 *ClaimsIdentity.Name*は*null*を返し、フレンドリ (表示) 名を返します。それ以外の場合は、ユーザーの一意の識別子として使用するのに適していない文字列を返します。

信頼性情報ベースの認証を使用する多くのデプロイでは、特に[Azure Access Control Service](https://msdn.microsoft.com/library/windowsazure/gg429786.aspx) (ACS) を使用します。 ACS を使用すると、開発者は個々の*id プロバイダー* (ADFS、Microsoft アカウントプロバイダー、yahoo! などの OpenID プロバイダーなど) を構成し、id プロバイダーは*名前識別子*を返すことができます。 これらの名前識別子には、電子メールアドレスのような個人を特定できる情報 (PII) を含めることができます。また、個人の個人識別子 (PPID) のように匿名化することもできます。 タプル (id プロバイダー、名前識別子) は、サイトを参照している間、特定のユーザーに適切な追跡トークンとして十分に機能します。そのため、ASP.NET Web Stack ランタイムは、を生成するときに、ユーザー名の代わりにタプルを使用できます。XSRF のフィールドトークンを検証しています。 Id プロバイダーと名前識別子の特定の Uri は次のとおりです。

- `http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider`
- `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`

(詳細については、この[ACS ドキュメントページ](https://msdn.microsoft.com/library/windowsazure/gg185971.aspx)を参照してください。)

トークンを生成または検証するときに、ASP.NET Web スタックランタイムは実行時に次の型にバインドします。

- `Microsoft.IdentityModel.Claims.IClaimsIdentity, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35` (WIF SDK の場合)
- `System.Security.Claims.ClaimsIdentity` (.NET 4.5 の場合)。

これらの型が存在し、現在のユーザーの*IIIIdentity*がこれらの型のいずれかを実装しているかサブクラスを実装している場合、XSRF ファシリティは、トークンを生成および検証するときに、ユーザー名の代わりに (id プロバイダー、名前識別子) タプルを使用します。 このようなタプルが存在しない場合、要求は失敗し、開発者に対して、使用中の特定の要求ベースの認証メカニズムを理解するように XSRF システムを構成する方法を説明するエラーが表示されます。 詳細については、「 **[構成と拡張機能](#_Configuration_and_extensibility)** 」を参照してください。

### <a name="oauth--openid-authentication"></a>OAuth/OpenID 認証

最後に、XSRF 機能は、OAuth または OpenID 認証を使用するアプリケーションに対して特別なサポートを行います。 このサポートはヒューリスティックに基づいています。現在の*IIdentity.Name*が http://または https://で始まる場合は、既定の stringcomparison.ordinalignorecase comparer ではなく序数の比較子を使用して、ユーザー名の比較が行われます。

<a id="_Configuration_and_extensibility"></a>

## <a name="configuration-and-extensibility"></a>構成と拡張性

場合によっては、開発者が XSRF の生成と検証の動作を厳密に制御する必要があります。 たとえば、MVC と Web ページのヘルパーの既定の動作である HTTP cookie を応答に自動的に追加することは望ましくありません。開発者は、トークンを他の場所に保存することをお勧めします。 これを支援するために、次の2つの Api が存在します。

`AntiForgery.GetTokens(string oldCookieToken, out string newCookieToken, out string formToken);`  
`AntiForgery.Validate(string cookieToken, string formToken);`

*Gettokens*メソッドは、既存の XSRF 要求確認セッショントークン (null) を入力として受け取り、新しい XSRF request 検証セッショントークンとフィールドトークンを出力として生成します。 トークンは、装飾のない単なる不透明な文字列です。インスタンスの*Formtoken*値は、&lt;入力&gt; タグにラップされません。 *Newcookietoken*値は null にすることができます。このエラーが発生した場合は、 *Oldcookietoken*値が引き続き有効であり、新しい応答クッキーを設定する必要はありません。 *Gettokens*の呼び出し元は、必要な応答クッキーを保持したり、必要なマークアップを生成したりします。*Gettokens*メソッド自体は、応答を副作用として変更しません。 *Validate*メソッドは、受信セッションとフィールドトークンを受け取り、前述の検証ロジックを実行します。

### <a name="antiforgeryconfig"></a>アンチ Forgeryconfig

開発者は、アプリケーション\_の起動から、XSRF システムを構成できます。 構成はプログラムによって行います。 次に、静的な*アンチ Forgeryconfig*型のプロパティについて説明します。 クレームを使用するほとんどのユーザーは、UniqueClaimTypeIdentifier プロパティを設定します。

| **Property** | **説明** |
| --- | --- |
| **AdditionalDataProvider** | トークンの生成中に追加データを提供し、トークンの検証中に追加のデータを使用する[Iアンチ Forgeryadditionaldataprovider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 。 既定値は*null*です。 詳細については、「 [Iアンチ Forgeryadditionaldataprovider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 」セクションを参照してください。 |
| **CookieName** | XSRF のセッショントークンを格納するために使用される HTTP クッキーの名前を提供する文字列。 この値が設定されていない場合、アプリケーションの展開された仮想パスに基づいて、名前が自動的に生成されます。 既定値は*null*です。 |
| **RequireSsl** | SSL で保護されたチャネル経由で XSRF トークンを送信する必要があるかどうかを指定するブール値。 この値が*true*の場合、自動的に生成される cookie には "secure" フラグが設定され、SSL 経由で送信されていない要求内から呼び出された場合、XSRF api はスローします。 既定値は *false* です。 |
| **SuppressIdentityHeuristicChecks** | XSRF システムで、要求ベースの id のサポートを非アクティブ化するかどうかを指定するブール値。 この値が*true*の場合、 *IIdentity.Name*はユーザーごとの一意の識別子として使用するのが適切であると想定し、WIF/ACS/で説明されているように、特殊なケースの*IClaimsIdentity*または*ClClaimsIdentity*を試行しません。 [要求ベースの認証](#_WIF_ACS)セクション。 既定値は `false`です。 |
| **UniqueClaimTypeIdentifier** | 一意のユーザーごとの識別子としての使用に適した要求の種類を示す文字列。 この値が設定されていて、現在の*IIdentity*がクレームベースの場合、システムは*UniqueClaimTypeIdentifier*によって指定された種類の要求を抽出しようとします。また、対応する値は、ユーザーのユーザー名の代わりに使用されます。フィールドトークンを生成しています。 要求の種類が見つからない場合、システムは要求に失敗します。 既定値は*null*です。これは、ユーザーのユーザー名の代わりに、前に説明したように、システムが (id プロバイダー、名前識別子) タプルを使用する必要があることを示します。 |

<a id="_IAntiForgeryAdditionalDataProvider"></a>

### <a name="iantiforgeryadditionaldataprovider"></a>Iアンチ Forgeryadditionaldataprovider

*[Iアンチ Forgeryadditionaldataprovider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)* 型を使用すると、開発者は、各トークンの追加データをラウンドトリップさせることで、XSRF システムの動作を拡張できます。 *Getadditionaldata*メソッドは、フィールドトークンが生成されるたびに呼び出され、戻り値は生成されたトークン内に埋め込まれます。 実装者は、タイムスタンプ、nonce、またはこのメソッドからのその他の値を返すことができます。

同様に、 *Validateadditionaldata*メソッドは、フィールドトークンが検証されるたびに呼び出され、トークン内に埋め込まれた "追加データ" 文字列がメソッドに渡されます。 検証ルーチンは、(トークンの作成時に現在の時刻をチェックすることによって) タイムアウトを実装したり、nonce チェックルーチンやその他の必要なロジックを実装したりすることができます。

## <a name="design-decisions-and-security-considerations"></a>設計上の決定とセキュリティに関する考慮事項

セッションとフィールドトークンをリンクするセキュリティトークンは、匿名/認証されていないユーザーを XSRF 攻撃から保護する場合にのみ、技術的には必要です。 ユーザーが認証されると、認証トークン自体 (cookie の形式で送信された可能性があります) をシンクロナイザートークンペアの半分として使用できるようになります。 ただし、認証されていないユーザーによるログインページの保護には有効なシナリオがあります。また、認証されたユーザーであっても、常にセキュリティトークンを生成して検証することによって、XSRF の対策ロジックがより簡単になりました。 また、攻撃者によってフィールドトークンが侵害される可能性がある場合に、追加の保護も提供します。これにより、セッショントークンが攻撃者にとって別のハードルになる可能性があります。

複数のアプリケーションが1つのドメインでホストされている場合、開発者は注意を払う必要があります。 たとえば、 *example1.cloudapp.net*と*example2.cloudapp.net*は異なるホストですが、 *cloudapp.net ドメイン\** のすべてのホスト間には暗黙の信頼関係があります。 この暗黙的な信頼関係[により、信頼できない可能性のあるホストが互いの cookie に影響を与えることが](http://stackoverflow.com/questions/9636857/how-can-asp-net-or-asp-net-mvc-be-protected-from-related-domain-cookie-attacks)あります (AJAX 要求を管理する同じオリジンポリシーは、必ずしも HTTP クッキーに適用されるわけではありません)。 ASP.NET Web Stack ランタイムでは、ユーザー名がフィールドトークンに埋め込まれるという点が軽減されます。したがって、悪意のあるサブドメインがセッショントークンを上書きできる場合でも、ユーザーに有効なフィールドトークンを生成することはできません。 ただし、このような環境でホストされている場合、組み込みの XSRF ルーチンは、セッションハイジャックやログイン XSRF を防ぐことはできません。

現在、XSRF ルーチンは[クリックジャッキング](https://www.owasp.org/index.php/Clickjacking)を防御するものではありません。 クリックジャッキングに対して自身を防御する必要があるアプリケーションは、各応答で X フレームオプション: sameorigin ヘッダーを送信することによって簡単に行うことができます。 このヘッダーは、最近のすべてのブラウザーでサポートされています。 詳細については、 [IE ブログ](https://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx)、 [SDL ブログ](https://blogs.msdn.com/b/sdl/archive/2009/02/05/clickjacking-defense-in-ie8.aspx)、 [owasp](https://www.owasp.org/index.php/Clickjacking)を参照してください。 ASP.NET Web スタックランタイムは、今後のリリースで、MVC と Web ページの XSRF ヘルパーが自動的にこのヘッダーを設定し、アプリケーションがこの攻撃に対して自動的に保護されるようにします。

Web 開発者は、サイトが XSS 攻撃に対して脆弱でないことを継続的に確認する必要があります。 XSS 攻撃は非常に強力であり、悪用が成功すると、XSRF 攻撃に対して ASP.NET Web Stack Runtime 防御も破壊されます。

## <a name="acknowledgment"></a>認識

[@LeviBroderick](https://twitter.com/LeviBroderick)、ASP.NET のセキュリティコードの大部分をこの情報の大部分に書いています。

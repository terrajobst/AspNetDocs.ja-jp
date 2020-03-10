---
uid: whitepapers/aspnet4/breaking-changes
title: ASP.NET 4 つの重大な変更 |Microsoft Docs
author: rick-anderson
description: このドキュメントでは、... を使用して作成されたアプリケーションに影響する可能性がある .NET Framework バージョン4リリースに加えられた変更について説明します。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d601c540-f86b-4feb-890c-20c806b3da6c
msc.legacyurl: /whitepapers/aspnet4/breaking-changes
msc.type: content
ms.openlocfilehash: 8ccad3b40a723c92a3164de082e1f94577141008
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439510"
---
# <a name="aspnet-4-breaking-changes"></a>ASP.NET 4 の破壊的変更

> このドキュメントでは、ASP.NET 4 Beta 1 と Beta 2 のリリースを含む、以前のリリースを使用して作成されたアプリケーションに影響を与える可能性がある .NET Framework バージョン4リリースに加えられた変更について説明します。
> 
> [このホワイトペーパーをダウンロードする](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_Breaking_Changes.pdf)

<a id="0.1__Toc256768952"></a><a id="0.1__Toc256770056"></a>

## <a name="contents"></a>内容

[Web.config ファイルの ControlRenderingCompatibilityVersion 設定](#0.1__Toc256770141 "_Toc256770141")  
[ClientIDMode の変更](#0.1__Toc256770142 "_Toc256770142")  
[HtmlEncode と UrlEncode で単一引用符をエンコードするようになりました](#0.1__Toc256770143 "_Toc256770143")  
[ASP.NET Page (.aspx) パーサーは厳密に](#0.1__Toc256770144 "_Toc256770144")  
[ブラウザー定義ファイルが更新されました](#0.1__Toc256770145 "_Toc256770145")  
[ルート Web 構成ファイルから削除された system.web](#0.1__Toc256770146 "_Toc256770146")  
[ASP.NET 要求の検証](#0.1__Toc256770147 "_Toc256770147")  
[既定のハッシュアルゴリズムが HMACSHA256 されるようになりました](#0.1__Toc256770148 "_Toc256770148")  
[新しい ASP.NET 4 ルート構成に関連する構成エラー](#0.1__Toc256770149 "_Toc256770149")  
[ASP.NET 4 子アプリケーションが ASP.NET 2.0 または ASP.NET 3.5 アプリケーションで開始できない](#0.1__Toc256770150 "_Toc256770150")  
[SharePoint がインストールされているコンピューターで ASP.NET 4 Web サイトを起動できない](#0.1__Toc256770151 "_Toc256770151")  
[HttpRequest プロパティに PathInfo の値が含まれなくなりました](#0.1__Toc256770152 "_Toc256770152")  
[ASP.NET 2.0 アプリケーションで、eurl axd を参照する HttpException エラーが生成される場合がある](#0.1__Toc256770153 "_Toc256770153")  
[IIS 7 または IIS 7.5 統合モードの既定のドキュメントでは、イベントハンドラーが生成されない場合がある](#0.1__Toc256770154 "_Toc256770154")  
[ASP.NET コードアクセスセキュリティ (CAS) の実装に対する変更](#0.1__Toc256770155 "_Toc256770155")  
[MembershipUser 名前空間のその他の型は移動されました](#0.1__Toc256770156 "_Toc256770156")  
[HTTP ヘッダー \* 変化する出力キャッシュの変更](#0.1__Toc256770157 "_Toc256770157")  
[Passport の system.web. Security の種類は廃止されています](#0.1__Toc256770158 "_Toc256770158")  
[PopOutImageUrl プロパティは、ASP.NET 4 でイメージをレンダリングできません。](#0.1__Toc256770159 "_Toc256770159")  
[StaticPopOutImageUrl と DynamicPopOutImageUrl は、パスに円記号が含まれている場合、イメージをレンダリングできません。](#0.1__Toc256770160 "_Toc256770160")  
[免責事項](#0.1__Toc256770161 "_Toc256770161")

<a id="0.1__ControlRenderingCompatibilityVersio"></a><a id="0.1__Toc245724853"></a><a id="0.1__Toc255587630"></a><a id="0.1__Toc256770141"></a>

## <a name="controlrenderingcompatibilityversion-setting-in-the-webconfig-file"></a>Web.config ファイルの ControlRenderingCompatibilityVersion 設定

.NET Framework バージョン4では、マークアップのレンダリング方法をより正確に指定できるように、ASP.NET コントロールが変更されています。 以前のバージョンの .NET Framework では、一部のコントロールは無効にする方法がなかったマークアップを生成しました。 既定では、ASP.NET 4 この種類のマークアップは生成されなくなりました。

Visual Studio 2010 を使用して ASP.NET 2.0 または ASP.NET 3.5 からアプリケーションをアップグレードすると、レガシレンダリングを保持する設定が `Web.config` ファイルに自動的に追加されます。 ただし、IIS のアプリケーション プールを変更して .NET Framework 4 をターゲットにするようにアプリケーションをアップグレードする場合、ASP.NET では新しい表示モードが既定で使用されます。 新しい表示モードを無効にするには、`Web.config` ファイルに次の設定を追加します。

[!code-xml[Main](breaking-changes/samples/sample1.xml)]

新しい動作によってもたらされる主な表示変更は次のとおりです。

- **Image**コントロールと**ImageButton**コントロールでは、`border="0"` 属性がレンダリングされなくなりました。
- **Basevalidator**クラスとそれから派生した検証コントロールは、既定で赤いテキストを表示しなくなります。
- **HtmlForm**コントロールでは、 **name**属性は表示されません。
- **テーブル**コントロールは、`border="0"` 属性をレンダリングしなくなりました。
- ユーザー入力向けに設計されていないコントロール (たとえば、**ラベル**コントロール) では、 **Enabled**プロパティが**false**に設定されている場合 (または、コンテナーコントロールからこの設定を継承している場合)、`disabled="disabled"` 属性がレンダリングされなくなりました。

<a id="0.1__Toc245724854"></a><a id="0.1__Toc255587631"></a><a id="0.1__Toc256770142"></a>

## <a name="clientidmode-changes"></a>ClientIDMode の変更

ASP.NET 4 の**Clientidmode**設定を使用すると、ASP.NET が HTML 要素の**id**属性を生成する方法を指定できます。 以前のバージョンの ASP.NET では、既定の動作は、 **Clientidmode**の**autoid**設定と同じでした。 ただし、既定の設定が**予測可能**になりました。

Visual Studio 2010 を使用してアプリケーションを ASP.NET 2.0 または ASP.NET 3.5 からアップグレードする場合、ツールは、以前のバージョンの .NET Framework の動作を保持する設定を `Web.config` ファイルに自動的に追加します。 ただし、IIS のアプリケーション プールを変更して .NET Framework 4 をターゲットにするようにアプリケーションをアップグレードする場合、ASP.NET では新しいモードが既定で使用されます。 新しいクライアント ID モードを無効にするには、`Web.config` ファイルに次の設定を追加します。

[!code-xml[Main](breaking-changes/samples/sample2.xml)]

<a id="0.1__Toc245724855"></a><a id="0.1__Toc255587632"></a><a id="0.1__Toc256770143"></a>

## <a name="htmlencode-and-urlencode-now-encode-single-quotation-marks"></a>HtmlEncode と UrlEncode で単一引用符をエンコードするようになりました

ASP.NET 4 では、 **HttpUtility**クラスと**設定**クラスの**HtmlEncode**メソッドと**UrlEncode**メソッドが、次のように単一引用符文字 (') をエンコードするように更新されています。

- **HtmlEncode**メソッドは、単一引用符のインスタンスをとしてエンコードします。
- **UrlEncode**メソッドは、単一引用符のインスタンスを %27 としてエンコードします。

<a id="0.1__Toc255587633"></a><a id="0.1__Toc256770144"></a><a id="0.1__Toc245724856"></a>

## <a name="aspnet-page-aspx-parser-is-stricter"></a>ASP.NET Page (.aspx) パーサーは厳密に

ASP.NET ページ (`.aspx` ファイル) とユーザーコントロール (`.ascx` ファイル) のページパーサーは、ASP.NET 4 では厳密なものであり、無効なマークアップのインスタンスをさらに拒否します。 たとえば、次の2つのスニペットは、ASP.NET の以前のリリースでは正常に解析されますが、ASP.NET 4 でパーサーエラーが発生するようになりました。

[!code-aspx[Main](breaking-changes/samples/sample3.aspx)]

**HiddenField**タグの末尾に無効なセミコロンがあることに注意してください。

[!code-aspx[Main](breaking-changes/samples/sample4.aspx)]

**CssClass**属性で実行されている、閉じていない**スタイル**属性に注意してください。

<a id="0.1__Toc255587634"></a><a id="0.1__Toc256770145"></a>

## <a name="browser-definition-files-updated"></a>ブラウザー定義ファイルが更新されました

ブラウザー定義ファイルは、新しいブラウザーとデバイスや、更新されたブラウザーとデバイスに関する情報を含むように、更新されました。 Netscape Navigator などの古いブラウザーとデバイスは削除され、Google Chrome や Apple iPhone などの新しいブラウザーとデバイスが追加されました。

削除されたブラウザー定義の 1 つを継承するカスタム ブラウザー定義がご利用のアプリケーションに含まれている場合は、エラーが表示されます。 たとえば、`App_Browsers` フォルダーに IE2 browser 定義から継承するブラウザー定義が含まれている場合、次のような構成エラーメッセージが表示されます。

- ID ' IE2 ' のブラウザーまたはゲートウェイ要素が見つかりません。

> [!NOTE]
> **Httpbrowsercapabilities**オブジェクト (ページの**Request. Browser**プロパティによって公開されます) は、ブラウザー定義ファイルによって制御されます。 したがって、ASP.NET 4 のこのオブジェクトのプロパティにアクセスすることによって返される情報は、以前のバージョンの ASP.NET で返された情報とは異なる場合があります。

次のフォルダーからブラウザー定義ファイルをコピーすることで、古いブラウザー定義ファイルに戻すことができます。

[!code-console[Main](breaking-changes/samples/sample5.cmd)]

ASP.NET 4 の対応する `\CONFIG\Browsers` フォルダーにファイルをコピーします。 ファイルをコピーしたら、Aspnet\_のコマンドラインツールを実行します。

<a id="0.1__Toc255587635"></a><a id="0.1__Toc256770146"></a>

## <a name="systemwebmobiledll-removed-from-root-web-configuration-file"></a>ルート Web 構成ファイルから削除された system.web

以前のバージョンの ASP.NET では、の下にある **[アセンブリ]** セクションのルート `Web.config` ファイルにアセンブリへの参照が含まれていました。 パフォーマンスを向上させるために、このアセンブリへの参照は削除されました。

ASP.NET アセンブリは、この4に含まれていますが、非推奨とされます。 System.web アセンブリの型を使用する場合は、このアセンブリへの参照をルート `Web.config` ファイル、またはアプリケーション `Web.config` ファイルに追加しますが、 たとえば、(非推奨) ASP.NET モバイルコントロールのいずれかを使用する場合は、`Web.config` ファイルにアセンブリへの参照を追加する必要があります。

<a id="0.1__Toc245724857"></a><a id="0.1__Toc255587636"></a><a id="0.1__Toc256770147"></a>

## <a name="aspnet-request-validation"></a>ASP.NET 要求の検証

ASP.NET の要求検証機能は、クロスサイトスクリプティング (XSS) 攻撃に対して一定レベルの既定の保護を提供します。 以前のバージョンの ASP.NET では、要求の検証は既定で有効になっていました。 ただし、ASP.NET ページ (`.aspx` ファイルとそのクラスファイル) のみに適用され、それらのページが実行されている場合にのみ適用されます。

ASP.NET 4 では、要求の検証は、HTTP 要求の**BeginRequest**フェーズの前に有効にされているため、既定ではすべての要求に対して有効になっています。 その結果、要求の検証は、.aspx ページ要求だけでなく、すべての ASP.NET リソースに対する要求に適用されます。 これには、Web サービス呼び出しやカスタム HTTP ハンドラーなどの要求が含まれます。 要求の検証は、カスタム HTTP モジュールが HTTP 要求の内容を読み取っている場合にもアクティブになります。

その結果、以前にエラーがトリガーされなかった要求に対して、要求の検証エラーが発生する可能性があります。 ASP.NET 2.0 要求の検証機能の動作に戻すには、`Web.config` ファイルに次の設定を追加します。

[!code-xml[Main](breaking-changes/samples/sample6.xml)]

ただし、既存のハンドラー、モジュール、またはその他のカスタムコードが安全でない可能性のある HTTP 入力にアクセスするかどうかを判断するために、要求の検証エラーを分析することをお勧めします。

<a id="0.1__Toc245724858"></a><a id="0.1__Toc255587637"></a><a id="0.1__Toc256770148"></a>

## <a name="default-hashing-algorithm-is-now-hmacsha256"></a>既定のハッシュアルゴリズムが HMACSHA256 されるようになりました

ASP.NET では、暗号化とハッシュ アルゴリズムの両方を使用して、フォーム認証 Cookie やビュー ステートなどのデータをセキュリティで保護します。 既定では、ASP.NET 4 では、cookie とビューステートのハッシュ操作に HMACSHA256 アルゴリズムが使用されるようになりました。 以前のバージョンの ASP.NET では、古い HMACSHA1 アルゴリズムが使用されていました。

フォーム認証 cookie などのデータが across.NET Framework バージョンで動作する必要がある混合 ASP.NET 2.0/ASP. NET 4 環境を実行すると、アプリケーションが影響を受ける可能性があります。 古い HMACSHA1 アルゴリズムを使用するように ASP.NET 4 Web アプリケーションを構成するには、`Web.config` ファイルに次の設定を追加します。

[!code-xml[Main](breaking-changes/samples/sample7.xml)]

<a id="0.1__Toc245724859"></a><a id="0.1__Toc255587638"></a><a id="0.1__Toc256770149"></a>

## <a name="configuration-errors-related-to-new-aspnet-4-root-configuration"></a>新しい ASP.NET 4 ルート構成に関連する構成エラー

.NET Framework 4 (および ASP.NET 4) のルート構成ファイル (`machine.config` ファイルとルート `Web.config` ファイル) が更新され、ASP.NET 3.5 に含まれる定型構成情報の大部分がアプリケーション `Web.config` ファイルに含まれるようになりました。 IIS 7 および iis 7.5 の管理された構成システムは複雑であるため、ASP.NET 4、IIS 7、IIS 7.5 の下で ASP.NET 3.5 アプリケーションを実行すると、ASP.NET または IIS の構成エラーが発生する可能性があります。

実際には、Visual Studio 2010 の project upgrade tools を使用して、ASP.NET 3.5 アプリケーションを ASP.NET 4 にアップグレードすることをお勧めします。 Visual Studio 2010 では、ASP.NET 3.5 アプリケーションの `Web.config` ファイルが ASP.NET 4 の適切な設定を含むように自動的に変更されます。

ただし、.NET Framework 4 を使用して ASP.NET 3.5 アプリケーションを再コンパイルせずに実行するシナリオはサポートされています。 この場合、.NET Framework 4 および IIS 7 または IIS 7.5 でアプリケーションを実行する前に、アプリケーションの `Web.config` ファイルを手動で変更しなければならないことがあります。

次の2つのセクションでは、ソフトウェアのさまざまな組み合わせに対して行う必要がある変更について説明します。

**Windows Vista SP1 または Windows Server 2008 SP1。修正プログラム KB958854 と SP2 のどちらもインストールされていません。** この構成では、IIS 7 構成システムは、アプリケーションレベルの `Web.config` ファイルを ASP.NET 2.0 `machine.config` ファイルと比較することによって、アプリケーションの管理された構成を誤ってマージします。 このため、IIS 7 の検証エラーを発生させないようにするには、.NET Framework 3.5 以降のアプリケーションレベルの `Web.config` ファイルで、 **system.web. extensions**構成セクションの定義 (要素) が必要です。

ただし、Visual Studio 2008 で導入された元の定型構成セクションの定義と正確に一致しない、手動で変更されたアプリケーションレベルの `Web.config` ファイルエントリは、ASP.NET 構成エラーが発生します。 (Visual Studio 2008 によって生成される既定の構成エントリは正常に動作します)。一般的な問題としては、手動で変更された `Web.config` ファイルは、さまざまな構成セクションの定義にある**Allowdefinition**および**requirepermission**の構成属性を除外することです。 これにより、アプリケーションレベルの `Web.config` ファイルの省略された構成セクションと、ASP.NET 4 `machine.config` ファイルの完全な定義が一致しません。 その結果、実行時に、ASP.NET 4 構成システムによって構成エラーがスローされます。

**Windows Vista SP2、Windows Server 2008 SP2、Windows 7、Windows Server 2008 R2、および Windows Vista SP1 および Windows Server 2008 SP1 (修正プログラム KB958854 がインストールされている場合)。**

このシナリオでは、IIS 7 と IIS 7.5 のネイティブ構成システムは、マネージ構成セクションハンドラーに定義されている**type**属性に対してテキスト比較を実行するため、構成エラーが返されます。 Visual Studio 2008 および Visual Studio 2008 SP1 によって生成されるすべての `Web.config` ファイルは、システムの型文字列に "3.5" が含まれているため**です。 web.config** (および関連) 構成セクションハンドラー、および ASP.NET 4 `machine.config` ファイルは同じ構成セクションハンドラーの**type**属性に "4.0" があるため、visual Studio 2008 または visual studio 2008 SP1 で生成されるアプリケーションでは、iis 7 および iis 7.5 での構成の検証は常に失敗します。

<a id="0.1__Toc251910248"></a>

### <a name="resolving-these-issues"></a>これらの問題の解決

最初のシナリオの回避策は、Visual Studio 2008 によって自動的に生成された `Web.config` ファイルの定型構成テキストを含めることによって、アプリケーションレベルの `Web.config` ファイルを更新することです。

最初のシナリオの代替の回避策としては、Vista または Windows Server 2008 用の Service Pack 2 をコンピューターにインストールするか、KB958854 ([https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)) をインストールして、IIS 構成システムの不適切な構成-マージ動作を修正します。 ただし、これらのアクションのいずれかを実行すると、2番目のシナリオで説明されている問題のために、アプリケーションで構成エラーが発生する可能性があります。

2番目のシナリオの回避策は、アプリケーションレベルの `Web.config` ファイルから、すべての**system.web. extensions**構成セクション定義と構成セクショングループ定義を削除またはコメントアウトすることです。 これらの定義は、通常、アプリケーションレベルの `Web.config` ファイルの先頭にあり、 **Configsections**要素とその子によって識別できます。

どちらのシナリオでも、**システムの codedom**セクションを手動で削除することをお勧めします。ただし、これは必須ではありません。

<a id="0.1__Toc252995490"></a><a id="0.1__Toc255587639"></a><a id="0.1__Toc256770150"></a><a id="0.1__Toc245724860"></a>

## <a name="aspnet-4-child-applications-fail-to-start-when-under-aspnet-20-or-aspnet-35-applications"></a>ASP.NET 4 子アプリケーションが ASP.NET 2.0 または ASP.NET 3.5 アプリケーションで開始できない

旧バージョンの ASP.NET を実行する子アプリケーションとして構成されている ASP.NET 4 アプリケーションは、構成エラーまたはコンパイル エラーにより起動しない場合があります。 次の例は、影響を受けるアプリケーションのディレクトリ構造を示しています。

`/parentwebapp` (ASP.NET 2.0 または ASP.NET 3.5 を使用するように構成されています)  
`/childwebapp` (ASP.NET 4 を使用するように構成されています)

`childwebapp` フォルダー内のアプリケーションは、IIS 7 または IIS 7.5 で開始できず、構成エラーが報告されます。 エラーテキストには、次のようなメッセージが表示されます。

- `The requested page cannot be accessed because the related configuration data for the page is invalid.`

- `The configuration section 'configSections' cannot be read because it is missing a section declaration.`

IIS 6 では、`childwebapp` フォルダー内のアプリケーションも起動に失敗しますが、別のエラーが報告されます。 たとえば、エラーテキストには次のような状態があります。

- `The value for the 'compilerVersion' attribute in the provider options must be 'v4.0' or later if you are compiling for version 4.0 or later of the .NET Framework. To compile this Web application for version 3.5 or earlier of the .NET Framework, remove the 'targetFramework' attribute from the element of the Web.config file`

これらのシナリオが発生するのは、`parentwebapp` フォルダー内の親アプリケーションからの構成情報が、`childwebapp` フォルダー内の子 web アプリケーションによって使用される最終的にマージされた構成設定を決定する構成情報の階層に含まれているためです。 ASP.NET 4 Web アプリケーションが IIS 7 (または IIS 7.5) で実行されているか、IIS 6 で実行されているかによって、IIS 構成システムまたは ASP.NET 4 コンパイルシステムのいずれかでエラーが返されます。

この問題を解決し、子 ASP.NET 4 アプリケーションを動作させるために従う必要がある手順は、ASP.NET 4 アプリケーションが IIS 6 または iis 7 (または IIS 7.5) のどちらで実行されているかによって異なります。

### <a name="step-1-iis-7-or-iis-75-only"></a>手順 1 (IIS 7 または IIS 7.5 のみ)

この手順は、Windows Vista、Windows Server 2008、Windows 7、および Windows Server 2008 R2 を含む IIS 7 または IIS 7.5 を実行するオペレーティングシステムにのみ必要です。

親アプリケーション (ASP.NET 2.0 または ASP.NET 3.5 を実行するアプリケーション) の `Web.config` ファイル内の**Configsections**定義を the.NET Framework 2.0 のルート `Web.config` ファイルに移動します。 IIS 7 および IIS 7.5 のネイティブ構成システムは、構成ファイルの階層をマージするときに**Configsections**要素をスキャンします。 親 Web アプリケーションの `Web.config` ファイルからルート `Web.config` ファイルに**Configsections**定義を移動すると、子 ASP.NET 4 アプリケーションに対して行われる構成マージプロセスの要素が実質的に非表示になります。

32ビットのオペレーティングシステム、または32ビットのアプリケーションプールでは、ASP.NET 2.0 と ASP.NET 3.5 のルート `Web.config` ファイルは通常、次のフォルダーにあります。

`C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG`

64ビットのオペレーティングシステム、または64ビットのアプリケーションプールでは、ASP.NET 2.0 と ASP.NET 3.5 のルート `Web.config` ファイルは通常、次のフォルダーにあります。

`C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG`

64ビットコンピューターで32ビットと64ビットの両方の Web アプリケーションを実行する場合は、32ビットシステムと64ビットシステムの両方のルート `Web.config` ファイルに**Configsections**要素を移動する必要があります。

ルート `Web.config` ファイルに**Configsections**要素を配置するときに、**構成**要素の直後にセクションを貼り付けます。 次の例では、要素の移動が終了したときに、ルート `Web.config` ファイルの先頭部分がどのように表示されるかを示します。

> [!NOTE]
> 次の例では、読みやすくするために行がラップされています。

[!code-xml[Main](breaking-changes/samples/sample8.xml)]

### <a name="step-2-all-versions-of-iis"></a>手順 2 (IIS のすべてのバージョン)

ASP.NET 4 子 Web アプリケーションが IIS 6 または iis 7 (または IIS 7.5) のどちらで実行されている場合でも、この手順は必須です。

ASP.NET 2 または ASP.NET 3.5 を実行している親 Web アプリケーションの `Web.config` ファイルで、構成エントリが親 Web アプリケーションにのみ適用されることを明示的に指定する**location**タグを (IIS と ASP.NET 構成システムの両方に) 追加します。 次の例は、追加する**location**要素の構文を示しています。

[!code-xml[Main](breaking-changes/samples/sample9.xml)]

次の例は、 **appSettings**セクションで始まり、 **system.webserver**セクションで終わるすべての構成セクションをラップするために**location**タグを使用する方法を示しています。

[!code-xml[Main](breaking-changes/samples/sample10.xml)]

手順 1. と手順 2. を完了すると、子 ASP.NET 4 Web アプリケーションはエラーなしで開始されます。

<a id="0.1__Toc252995491"></a><a id="0.1__Toc255587640"></a><a id="0.1__Toc256770151"></a>

## <a name="aspnet-4-web-sites-fail-to-start-on-computers-where-sharepoint-is-installed"></a>SharePoint がインストールされているコンピューターで ASP.NET 4 Web サイトを起動できない

SharePoint を実行する web サーバーには、SharePoint Web サイトのルート (たとえば、既定の Web サイトの `c:\inetpub\wwwroot\web.config`) に配置される `Web.config` ファイルがあります。 この `Web.config` ファイルでは、SharePoint によって、WSS\_最小という名前のカスタム部分信頼レベルが設定されます。

この種類の SharePoint Web サイトの子として配置されている ASP.NET 4 Web サイトを実行しようとすると、次のエラーが表示されます。

`Could not find permission set named 'ASP.NET'.`

このエラーは、ASP.NET 4 コードアクセスセキュリティ (CAS) インフラストラクチャが ASP.NET という名前のアクセス許可セットを検索するために発生します。 ただし、WSS\_最小限で参照される部分信頼構成ファイルには、その名前のアクセス許可セットが含まれていません。

現在、ASP.NET と互換性のあるバージョンの SharePoint は使用できません。 そのため、SharePoint Web サイトの下の子サイトとして ASP.NET 4 Web サイトを実行しようとしないでください。

<a id="0.1__Toc255587641"></a><a id="0.1__Toc256770152"></a>

## <a name="the-httprequestfilepath-property-no-longer-includes-pathinfo-values"></a>HttpRequest プロパティに PathInfo の値が含まれなくなりました

以前のバージョンの ASP.NET では、ファイルパス関連のさまざまなプロパティから返される値に**Pathinfo**値が含まれていました。これには、 **AppRelativeCurrentExecutionFilePath**、 **httprequest などが** **あります。** ASP.NET 4 では、これらのプロパティの戻り値に**Pathinfo**値が含まれなくなりました。 代わりに、 **pathinfo**情報は、 **HttpRequest**情報で入手できます。 たとえば、次のような URL フラグメントがあるとします。

`/testapp/Action.mvc/SomeAction`

以前のバージョンの ASP.NET では、 **HttpRequest**プロパティの値は次のとおりです。

**HttpRequest. FilePath**: `/testapp/Action.mvc/SomeAction`

**HttpRequest info**: (空)

ASP.NET 4 では、 **HttpRequest**プロパティは次の値を持ちます。

**HttpRequest. FilePath**: `/testapp/Action.mvc`

**HttpRequest info**: `SomeAction`

<a id="0.1__Toc252995493"></a><a id="0.1__Toc255587642"></a><a id="0.1__Toc256770153"></a><a id="0.1__Toc245724861"></a>

## <a name="aspnet-20-applications-might-generate-httpexception-errors-that-reference-eurlaxd"></a>ASP.NET 2.0 アプリケーションで、eurl axd を参照する HttpException エラーが生成される場合がある

ASP.NET 4 を IIS 6 で有効にした後、(Windows Server 2003 または Windows Server 2003 R2 の) IIS 6 で実行された ASP.NET 2.0 アプリケーションで次のようなエラーが発生する可能性があります。

`System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.`

このエラーは、Web サイトが ASP.NET 4 を使用するように構成されていることが ASP.NET によって検出された場合に発生します。これにより、ASP.NET 4 のネイティブコンポーネントは拡張子 URL を ASP.NET のマネージ部分に渡して処理を続行します。 ただし、ASP.NET 4 Web サイトの下にある仮想ディレクトリが ASP.NET 2.0 を使用するように構成されている場合、この方法で拡張子 URL を処理すると、文字列 "eurl. axd" を含む URL が変更されます。 この変更された URL は、ASP.NET 2.0 アプリケーションに送信されます。 ASP.NET 2.0 は、"eurl. axd" 形式を認識できません。 したがって、ASP.NET 2.0 は `eurl.axd` という名前のファイルを検索して実行しようとします。 このようなファイルが存在しないため、要求は**Httpexception**例外で失敗します。

この問題を回避するには、次のいずれかのオプションを使用します。

### <a name="option-1"></a>方法 1

Web サイトを実行するために ASP.NET 4 が必要ない場合は、代わりに ASP.NET 2.0 を使用するようにサイトを再マップします。

### <a name="option-2"></a>方法 2

Web サイトを実行するために ASP.NET 4 が必要な場合は、ASP.NET 2.0 にマップされている別の Web サイトに、子の ASP.NET 2.0 仮想ディレクトリを移動します。

### <a name="option-3"></a>オプション3

Web サイトを ASP.NET 2.0 に再マップしたり、仮想ディレクトリの場所を変更したりするのが実用的でない場合は、ASP.NET 4 の拡張子 URL 処理を明示的に無効にします。 次の手順に従います。

1. Windows レジストリで、次のノードを開きます。

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0`

1. **Enableextensionlessurls**という名前の新しい**DWORD**値を作成します。
2. **Enableextensionurl**を0に設定します。 これにより、拡張子 URL の動作が無効になります。
3. レジストリ値を保存し、レジストリエディターを閉じます。
4. **Iisreset**コマンドラインツールを実行します。これにより、IIS によって新しいレジストリ値が読み取られます。

> [!NOTE]
> **Enableextension拡張子**url を1に設定すると、url の動作が有効になります。 これは、値が指定されていない場合の既定の設定です。

<a id="0.1__Toc252995494"></a><a id="0.1__Toc255587643"></a><a id="0.1__Toc256770154"></a><a id="0.1__Toc245724862"></a>

## <a name="event-handlers-might-not-be-not-raised-in-a-default-document-in-iis-7-or-iis-75-integrated-mode"></a>IIS 7 または IIS 7.5 統合モードの既定のドキュメントでは、イベントハンドラーが生成されない場合がある

ASP.NET 4 には、拡張子 URL が既定のドキュメントに解決されるときに HTML**フォーム**要素の**action**属性がどのように表示されるかを変更する変更が含まれています。 既定のドキュメントを解決する拡張子 URL の例として[http://contoso.com/](http://contoso.com/)があり、その結果、 [http://contoso.com/Default.aspx](http://contoso.com/Default.aspx)要求が発生します。

ASP.NET 4 では、既定のドキュメントがマップされている拡張子 URL に対して要求が行われたときに、HTML**フォーム**要素の**action**属性値が空の文字列として表示されるようになりました。 たとえば、ASP.NET の以前のリリースでは、 [http://contoso.com](http://contoso.com)の要求によって `Default.aspx`要求が発生します。 このドキュメントでは、開始**フォーム**タグは次の例のようにレンダリングされます。

`<form action="Default.aspx" />`

ASP.NET 4 では、 [http://contoso.com](http://contoso.com)の要求によっても `Default.aspx`要求が発生します。 ただし、次の例のように、ASP.NET は HTML を開始する**フォーム**タグをレンダリングするようになりました。

`<form action="" />`

**Action**属性がどのように表示されるかによって、IIS と ASP.NET によってフォームの投稿が処理される方法が微妙に変わる可能性があります。 **Action**属性が空の文字列の場合、IIS **defaultdocumentmodule**オブジェクトは `Default.aspx`する子要求を作成します。 ほとんどの条件下では、この子要求はアプリケーションコードに対して透過的であり、`Default.aspx` ページは正常に実行されます。

ただし、マネージド コードと IIS 7 または IIS 7.5 統合モードとの間のやり取りによって、マネージド .aspx ページが子要求中に正常に動作を停止することがあります。 次の条件が発生すると、`Default.aspx` ドキュメントへの子要求によってエラーまたは予期しない動作が発生します。

1. .Aspx ページは、 **form**要素の**action**属性が "" に設定されているブラウザーに送信されます。
2. フォームは ASP.NET にポストバックされます。
3. マネージ HTTP モジュールは、エンティティ本体の一部を読み取ります。 たとえば、モジュールは、**要求の形式**または**要求**を読み取ります。 Params です。 これにより、POST 要求のエンティティ本体がマネージド メモリに読み込まれます。 その結果、エンティティ本体は、IIS 7 または IIS 7.5 統合モードで実行されているネイティブ コード モジュールから使用できなくなります。
4. IIS **Defaultdocumentmodule**オブジェクトが最終的に実行され、`Default.aspx` ドキュメントへの子要求を作成します。 ただし、エンティティ本体はマネージド コードの一部によって既に読み取られているため、子要求に対する送信に使用できるエンティティ本体はありません。
5. HTTP パイプラインが子要求に対して実行されると、ハンドラー実行フェーズ中に `.aspx` ファイルのハンドラーが実行されます。
6. エンティティ本体がないため、フォーム変数とビューステートは存在しません。そのため、.aspx ページハンドラーでは、発生するイベント (存在する場合) を判断するための情報は使用できません。 その結果、影響を受ける .aspx ページのポストバック イベント ハンドラーは実行されません。

この動作を回避するには、次の方法を使用します。

- 既定のドキュメント要求中に要求のエンティティ本体にアクセスしている HTTP モジュールを特定し、それをマネージ要求に対してのみ実行するように構成できるかどうかを判断します。 IIS 7 と IIS 7.5 の統合モードでは、次の属性をモジュールの**system.webserver/modules**エントリに追加することで、マネージ要求に対してのみ実行するように HTTP モジュールをマークできます。

- `precondition="managedHandler"`

- この設定により、IIS 7 および IIS 7.5 が管理されていない要求として判断した要求のモジュールが無効になります。 既定のドキュメント要求の場合、最初の要求は拡張子 URL になります。 そのため、初期要求の処理中に、マネージハンドラーの事前条件でマークされているマネージモジュールは実行されません。 その結果、マネージモジュールはエンティティ本体を誤って読み取ることがなく、エンティティ本体は引き続き使用でき、子要求および既定のドキュメントに渡されます。

- 問題のある HTTP モジュールをすべての要求に対して実行する必要がある場合 (静的ファイルの場合は、 **Defaultdocumentmodule**オブジェクトに解決される拡張子 url、マネージ要求の場合など) は、ページの**HtmlForm**コントロールの**Action**プロパティを空でない文字列に明示的に設定して、影響を受ける .aspx ページを変更します。 たとえば、既定のドキュメントが `Default.aspx`場合は、ページのコードを変更して、 **HtmlForm**コントロールの**Action**プロパティを明示的に "default.aspx" に設定します。

<a id="0.1__Toc255587644"></a><a id="0.1__Toc256770155"></a>

## <a name="changes-to-the-aspnet-code-access-security-cas-implementation"></a>ASP.NET コードアクセスセキュリティ (CAS) の実装に対する変更

ASP.NET 2.0、および3.5 で追加された ASP.NET 機能の拡張により、.NET Framework 1.1 および2.0 コードアクセスセキュリティ (CAS) モデルを使用します。 ただし、ASP.NET 4 での CAS の実装は大幅に見直されました。 その結果、グローバルアセンブリキャッシュ (GAC) で実行されている信頼されたコードに依存する部分信頼 ASP.NET アプリケーションは、さまざまなセキュリティ例外で失敗する可能性があります。 コンピューターの CAS ポリシーに対する広範な変更に依存する部分信頼アプリケーションも、セキュリティ例外で失敗する場合があります。

次の例に示すように、 **trust** configuration 要素の new **legacyCasModel**属性を使用して、部分信頼 ASP.NET 4 アプリケーションを ASP.NET 1.1 および2.0 の動作に戻すことができます。

`<trust level= "Medium" legacyCasModel="true" />`

従来の CAS モデルに戻すと、次の古い CAS 動作が有効になります。

- コンピューターの CAS ポリシーは受け入れられます。
- 1つのアプリケーションドメインに複数の異なるアクセス許可セットを指定できます。
- ASP.NET または他の .NET Framework コードだけがスタック上にある場合に呼び出される GAC のアセンブリには、明示的なアクセス許可アサーションは必要ありません。

.NET Framework 4 では、1つのシナリオを元に戻すことはできません。非 Web 部分信頼アプリケーションでは、system.web および system.servicemodel の特定の Api を呼び出すことができなくなりました。 以前のバージョンの .NET Framework では、非 Web 部分信頼アプリケーションに**Aspnethostingpermission**アクセス許可を明示的に付与することができました。 これらのアプリケーションは、 **HttpUtility、** 名前空間の **\*** 型、およびメンバーシップ、ロール、およびプロファイルに関連する型を使用できます。 非 Web 部分信頼アプリケーションからこれらの型を呼び出すことは、.NET Framework 4 ではサポートされなくなりました。

> [!NOTE]
> **HttpUtility**クラスの**HtmlEncode**および**htmldecode**機能は、新しい .NET Framework 4 **System webutility.htmldecode**クラスに移動されました。 それが使用されていた唯一の ASP.NET 機能であった場合は、代わりに新しい**webutility.htmldecode**クラスを使用するようにアプリケーションのコードを変更します。

ASP.NET 4 の既定の CAS 実装に加えられた変更の概要を次に示します。

- ASP.NET アプリケーションドメインが同種のアプリケーションドメインになりました。 アプリケーションドメインで使用できるのは、部分信頼と完全信頼の許可セットだけです。
- ASP.NET の部分信頼付与セットは、エンタープライズレベル、マシンレベル、またはユーザーレベルの CAS ポリシーからは独立しています。
- 3\.5 および 3.5 SP1 に同梱されている ASP.NET アセンブリは、.NET Framework 4 つの透過性モデルを使用するように変換されています。
- ASP.NET **Aspnethostingpermission**属性の使用が大幅に減少しました。 この属性のほとんどのインスタンスは、パブリック ASP.NET Api から削除されています。
- ASP.NET ビルドプロバイダーによって作成された動的にコンパイルされたアセンブリは、アセンブリを透過的として明示的にマークするように更新されました。
- すべての ASP.NET アセンブリは、APTCA 属性が Web ホスティング環境でのみ受け入れられるようにマークされるようになりました。 ClickOnce などの部分的に信頼されていない Web ホスティング環境では、ASP.NET アセンブリを呼び出すことができません。

新しい ASP.NET 4 コードアクセスセキュリティモデルの詳細については、MSDN Web サイトの「 [ASP.NET アプリケーションでのコードアクセスセキュリティの使用](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx)」を参照してください。

<a id="0.1__Toc256770156"></a><a id="0.1__Toc245724863"></a><a id="0.1__Toc252995496"></a><a id="0.1__Toc255587645"></a><a id="0.1__Toc245724864"></a>

## <a name="membershipuser-and-other-types-in-the-systemwebsecurity-namespace-have-been-moved"></a>MembershipUser 名前空間のその他の型は移動されました

ASP.NET のメンバーシップで使用される一部の型は、`System.Web.dll` から新しいアセンブリに移動されました。 これらのタイプは、クライアントのタイプと拡張 .NET Framework SKU のタイプとの間のアーキテクチャ層の依存関係を解決するために移動しました。

Web サイトプロジェクトには、これらの型を移動した結果として問題はありません。これは、ASP.NET コンパイルシステムによって既定で使用される参照アセンブリの一覧に、アプリケーションが追加されたためです。 以前のバージョンの ASP.NET を使用して作成された Web サイトプロジェクトを Visual Studio 2010 で開くことによって ASP.NET 4 にアップグレードした場合、プロジェクトはエラーなしでコンパイルされます。

同様に、以前のバージョンの ASP.NET で作成された Web アプリケーションプロジェクトを Visual Studio 2010 で開くことによって ASP.NET 4 にアップグレードすると、アップグレードプロセスによってプロジェクトにへの参照が追加されます。 そのため、アップグレードされた Web アプリケーションプロジェクトもエラーなしでコンパイルされます。

以前のバージョンの ASP.NET を使用して作成されたコンパイル済み (バイナリ) ファイルは、メンバーシップの種類が別のアセンブリに移動された場合でも、ASP.NET 4 ではエラーなしでも実行されます。 型の転送情報が ASP.NET 4 バージョンの `System.Web.dll` に追加され、これらの型のランタイム参照が型の新しい場所に自動的にルーティングされるようになりました。

ただし、特定のメンバーシップの種類を使用し、以前のバージョンの ASP.NET からアップグレードされたクラスライブラリは、ASP.NET 4 プロジェクトで使用するとコンパイルに失敗します。 たとえば、クラスライブラリプロジェクトのコンパイルに失敗し、次のようなエラーが報告される場合があります。

- `The type 'System.Web.Security.MembershipUser' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`

- `The type name 'MembershipUser' could not be found. This type has been forwarded to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'. Consider adding a reference to that assembly.`

この問題を回避するには、クラスライブラリプロジェクトの参照を system.servicemodel に追加します。

次の一覧は、`System.Web.dll` から system.servicemodel に移動された*web.config*の種類を示しています。

- *System.web. Membershipcreatestatus.success*
- *CreateUserException を構成します。*
- *System.web. System.web.security.membershippasswordexception*
- *System.web. Security. メンバーシップ Passwordformat*
- *System.web. MembershipProvider*
- *System.web. Security. メンバーシップ Providercollection*
- *System.web. MembershipUser*
- *System.web. Security. メンバーシップ Usercollection*
- *System.web. MembershipValidatePasswordEventHandler*
- *System.web. ValidatePasswordEventArgs*
- *System.web. RoleProvider*
- <a id="0.1_a"></a>*System.web. Configuration. メンバーシップパスワードモード*

<a id="0.1__Toc256770157"></a>

## <a name="output-caching-changes-to-vary--http-header"></a>HTTP ヘッダー \* 変化する出力キャッシュの変更

ASP.NET 1.0 では、バグによって、出力として `Location="ServerAndClient"` 指定されたキャッシュされたページが、応答で `Vary:*` HTTP ヘッダーを出力するように設定されました。 その結果、クライアント ブラウザーに対して、ローカルにページをキャッシュしないように指示がなされていました。

ASP.NET 1.1 では、 **SetOmitVaryStar**メソッドが追加されました。これを呼び出すと、`Vary:*` ヘッダーを非表示にすることができます。 出力された HTTP ヘッダーを変更すると、その時点で重大な変更と見なされたため、このメソッドが選択されました。 ただし、開発者は ASP.NET の動作と混同されており、バグレポートは、開発者が既存の**SetOmitVaryStar**の動作を認識しないことを示唆しています。

ASP.NET 4 では、根本原因を修正するための決定が行われました。 `Vary:*` HTTP ヘッダーは、次のディレクティブを指定する応答からは出力されなくなりました。

`<%@OutputCache Location="ServerAndClient" %>`

その結果、`Vary:*` ヘッダーを非表示にするために**SetOmitVaryStar**は不要になりました。

ページの **@ OutputCache**ディレクティブで `Location="ServerAndClient"` を指定するアプリケーションでは、 **Location**属性の値の名前によって暗黙的に指定される動作が表示されます。つまり、 **SetOmitVaryStar**メソッドを呼び出すことなく、ブラウザーでページをキャッシュできるようになります。

アプリケーションのページで `Vary:*`を生成する必要がある場合は、次の例のように**Appendheader**メソッドを呼び出します。

`HttpResponse.AppendHeader("Vary","*");`

または、[出力キャッシュの**場所**] 属性の値を "Server" に変更することもできます。

<a id="0.1__Toc255587646"></a><a id="0.1__Toc256770158"></a>

## <a name="systemwebsecurity-types-for-passport-are-obsolete"></a>Passport の system.web. Security の種類は廃止されています

Passport (現在は LiveID) の変更により、ASP.NET 2.0 に組み込まれている Passport サポートは廃止され、数年間サポートされなくなりました。 その結果、ObsoleteAttribute の Passport に関連する5つの型が、現在は属性で**マークされています**。

<a id="0.1__The_MenuItem.PopOutImageUrl_Propert"></a><a id="0.1__Toc256770159"></a>

## <a name="the-menuitempopoutimageurl-property-fails-to-render-an-image-in-aspnet-4"></a>PopOutImageUrl プロパティは、ASP.NET 4 でイメージをレンダリングできません。

ASP.NET 3.5 では、 *PopOutImageUrl*プロパティを使用して、メニュー項目に表示されるイメージの URL を指定して、メニュー項目に動的サブメニューがあることを示すことができます。 次の例は、ASP.NET 3.5 のマークアップでこのプロパティを指定する方法を示しています。

[!code-aspx[Main](breaking-changes/samples/sample11.aspx)]

ASP.NET 4 でのデザイン変更の結果、 *MenuItem*クラスに対してプロパティが設定されている場合、 *PopOutImageUrl*の出力は表示されません。 代わりに、 *StaticPopOutImageUrl*プロパティまたは*DynamicPopOutImageUrl*プロパティのいずれかを使用して、*メニュー*コントロールに直接イメージ URL を指定する必要があります。 静的メニューを使用する場合、 *StaticPopOutImageUrl*プロパティは、次の例に示すように、静的メニュー項目にサブメニューがあることを示すために表示されるイメージの URL を指定します。

[!code-aspx[Main](breaking-changes/samples/sample12.aspx)]

動的メニューで作業している場合は、 *DynamicPopOutImageUrl*プロパティを使用して、動的メニュー項目にサブメニューがあることを示すイメージの URL を指定します。 次の例は前の例と似ていますが、動的メニューの*DynamicPopOutImageUrl*プロパティを設定する方法を示しています。

[!code-aspx[Main](breaking-changes/samples/sample13.aspx)]

*DynamicPopOutImageUrl*プロパティが設定されておらず、 *DynamicEnableDefaultPopOutImage*プロパティが*false*に設定されている場合、イメージは表示されません。 同様に、 *StaticPopOutImageUrl*プロパティが設定されておらず、 *StaticEnableDefaultPopOutImage*プロパティが*false*に設定されている場合、イメージは表示されません。

これらのプロパティのパスを設定するときは、円記号 (\)の代わりにスラッシュ (/) を使用します。 詳細については、「StaticPopOutImageUrl and DynamicPopOutImageUrl」を参照してください。このドキュメントの他の場所に[パスが含まれている場合は、画像をレンダリングできませ](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu。 StaticPopOutImageUrl_and_Menu。")ん。

<a id="0.1__Menu.StaticPopOutImageUrl_and_Menu."></a><a id="0.1__Toc256770160"></a>

## <a name="menustaticpopoutimageurl-and-menudynamicpopoutimageurl-fail-to-render-images-when-paths-contain-backslashes"></a>StaticPopOutImageUrl と DynamicPopOutImageUrl は、パスに円記号が含まれている場合、イメージをレンダリングできません。

ASP.NET 4 では、 *StaticPopOutImageUrl*プロパティと*DynamicPopOutImageUrl*プロパティを使用して指定したイメージは、パスに backlashes (\)が含まれている場合はレンダリングされません。 これは、以前のバージョンの ASP.NET から変更されています。

次の*メニュー*コントロールマークアップの例では、円記号を含むパスを使用して、 *StaticPopOutImageUrl*プロパティが設定されています。 ASP.NET 4 では、プロパティで指定されたイメージはレンダリングされません。

[!code-aspx[Main](breaking-changes/samples/sample14.aspx)]

この問題を解決するには、 *StaticPopOutImageUrl*プロパティと*DynamicPopOutImageUrl*プロパティで指定されているパス値を、スラッシュ (/) を使用するように変更します。 次の例は、この変更を示しています。

[!code-aspx[Main](breaking-changes/samples/sample15.aspx)]

以前のバージョンの ASP.NET から ASP.NET 4 に移行されたアプリケーションも影響を受ける可能性があります。これは、 *PopOutImageUrl*プロパティが変更されているためです。 詳細については、このドキュメントの別の場所にある[ASP.NET 4 で、PopOutImageUrl プロパティが画像を表示](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem。 PopOutImageUrl_Propert")できないことを確認してください。

<a id="0.1__Toc224729061"></a><a id="0.1__Toc255587647"></a><a id="0.1__Toc256770161"></a>

## <a name="disclaimer"></a>免責事項

このドキュメントは暫定版であり、ここで説明するソフトウェアの最終的な商業リリースより前に大幅に変更される可能性があります。

このドキュメントに含まれる情報は、取り上げている問題についての、公開時点における Microsoft Corporation の見解を表します。 Microsoft は変化する市場状況に対応する必要があるため、これを Microsoft による確約と解釈しないでください。Microsoft は、記載されている情報の公開後の正確さを保証できません。

このホワイト ペーパーは、情報提供のみを目的としています。 マイクロソフトは、このドキュメント内の情報に関して、明示的、暗黙的、または法的ないかなる保証も行いません。

お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用を願います。 このソフトウェアおよびマニュアルのいかなる部分も、米国 Microsoft Corporation の書面による許諾を受けることなく、その目的を問わず、どのような形態であっても、複製または譲渡することは禁じられています。ここでいう形態とは、複写や記録など、電子的な、または物理的なすべての手段を含みます。

Microsoft は、このマニュアルに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。 別途マイクロソフトのライセンス契約上に明示の規定がない限り、このドキュメントはこれらの特許、商標、著作権、またはその他の無体財産権に関する権利をお客様に許諾するものではありません。

特に明記されていない限り、ここに記載されている会社、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人名、場所、およびイベントは架空のものであり、実在する企業、組織、製品、ドメイン名、電子メールとは一切関係ありません。アドレス、ロゴ、人物、場所、またはイベントが想定されているか、または推測する必要があります。

© 2010 Microsoft Corporation. All rights reserved.

Microsoft および Windows は、米国および他の国における Microsoft Corporation の登録商標または商標です。

本ドキュメントで説明する実際の製造元および製品名は、それぞれの所有者の商標である場合があります。

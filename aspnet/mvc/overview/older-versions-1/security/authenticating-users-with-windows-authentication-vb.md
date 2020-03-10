---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: Windows 認証を使用してユーザーを認証する (VB) |Microsoft Docs
author: microsoft
description: MVC アプリケーションのコンテキストで Windows 認証を使用する方法について説明します。 アプリケーションの web co で Windows 認証を有効にする方法について説明します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: aa64b1f9ef6461a81611ca066310dca2d545baa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506242"
---
# <a name="authenticating-users-with-windows-authentication-vb"></a>Windows 認証でユーザーを認証する (VB)

[Microsoft](https://github.com/microsoft)

> MVC アプリケーションのコンテキストで Windows 認証を使用する方法について説明します。 アプリケーションの web 構成ファイル内で Windows 認証を有効にする方法と、IIS で認証を構成する方法について説明します。 最後に、[承認] 属性を使用して、特定の Windows ユーザーまたはグループに対するコントローラーアクションへのアクセスを制限する方法について説明します。

このチュートリアルの目的は、MVC アプリケーションのビューをパスワードで保護するためにインターネットインフォメーションサービスに組み込まれているセキュリティ機能を活用する方法を説明することです。 特定の windows ユーザーまたは特定の Windows グループのメンバーであるユーザーのみがコントローラーアクションを呼び出せるようにする方法について説明します。

社内の社内 web サイト (イントラネットサイト) を構築していて、ユーザーが web サイトにアクセスするときに標準の Windows ユーザー名とパスワードを使用できるようにする場合は、Windows 認証を使用するのが理にかなっています。 外部に接続する web サイト (インターネット web サイト) を構築する場合は、代わりにフォーム認証を使用することを検討してください。

#### <a name="enabling-windows-authentication"></a>Windows 認証を有効にする

新しい ASP.NET MVC アプリケーションを作成する場合、Windows 認証は既定では有効になっていません。 フォーム認証は、MVC アプリケーションに対して有効になっている既定の認証の種類です。 MVC アプリケーションの web 構成 (web.config) ファイルを変更して、Windows 認証を有効にする必要があります。 &lt;authentication&gt; セクションを見つけて、次のようなフォーム認証ではなく Windows を使用するように変更します。

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

Windows 認証を有効にすると、web サーバーはユーザーの認証を担当します。 通常、ASP.NET MVC アプリケーションを作成してデプロイするときに使用する web サーバーには2種類あります。

まず、MVC アプリケーションを開発するときに、Visual Studio に付属の ASP.NET Development Web サーバーを使用します。 既定では、ASP.NET Development Web サーバーは、Windows へのログインに使用したすべてのアカウントについて、現在の Windows アカウントのコンテキストですべてのページを実行します。

ASP.NET Development Web サーバーは、NTLM 認証もサポートしています。 NTLM 認証を有効にするには、[ソリューションエクスプローラー] ウィンドウでプロジェクトの名前を右クリックし、[プロパティ] を選択します。 次に、[Web] タブを選択し、[NTLM] チェックボックスをオンにします (図1を参照)。

**図 1: ASP.NET Development Web サーバーの NTLM 認証を有効にする**

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

実稼働 web アプリケーションの場合は、IIS を web サーバーとして使用します。 IIS は次のようないくつかの種類の認証をサポートしています。

- 基本認証-HTTP 1.0 プロトコルの一部として定義されます。 インターネット経由でユーザー名とパスワードをクリアテキスト (Base64 エンコード) で送信します。 -Digest 認証–パスワード自体ではなく、パスワードのハッシュをインターネット経由で送信します。 -統合 Windows (NTLM) 認証– windows を使用してイントラネット環境で使用する最適な認証の種類。 -証明書認証–クライアント側の証明書を使用した認証を有効にします。 証明書は Windows ユーザーアカウントにマップされます。

> [!NOTE] 
> 
> これらのさまざまな種類の認証の詳細については、「 [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)」を参照してください。

インターネットインフォメーションサービス Manager を使用して、特定の種類の認証を有効にすることができます。 すべての種類の認証は、すべてのオペレーティングシステムで使用できるわけではないことに注意してください。 さらに、Windows Vista で IIS 7.0 を使用している場合は、インターネットインフォメーションサービス Manager に表示する前に、さまざまな種類の Windows 認証を有効にする必要があります。 [**コントロールパネル]、[プログラム]、[プログラムと機能] の順に開き、[Windows の機能の有効化または無効化**] を開き、[インターネットインフォメーションサービス] ノードを展開します (図2を参照)。

**図 2-Windows IIS 機能の有効化**

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

インターネットインフォメーションサービスを使用すると、さまざまな種類の認証を有効または無効にすることができます。 たとえば、図3は、IIS 7.0 を使用する場合に、匿名認証を無効にし、統合 Windows (NTLM) 認証を有効にする方法を示しています。

**図 3-統合 Windows 認証の有効化**

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Windows ユーザーとグループの承認

Windows 認証を有効にした後、&lt;承認&gt; 属性を使用して、コントローラーまたはコントローラーアクションへのアクセスを制御できます。 この属性は、MVC コントローラー全体または特定のコントローラーアクションに適用できます。

たとえば、リスト1のホームコントローラーでは、Index ()、企業秘密 ()、StephenSecrets () という3つのアクションが公開されています。 すべてのユーザーが Index () アクションを呼び出すことができます。 ただし、会社のシークレット () アクションを呼び出すことができるのは、Windows ローカルマネージャーグループのメンバーだけです。 最後に、Stephen (Redmond ドメイン内) という名前の Windows ドメインユーザーのみが StephenSecrets () アクションを呼び出すことができます。

**リスト1– Controllers\HomeController.vb**

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> Windows ユーザーアカウント制御 (UAC) のため、Windows Vista または Windows Server 2008 を使用する場合、ローカルの Administrators グループの動作は他のグループとは異なります。 &lt;承認&gt; 属性は、コンピューターの UAC 設定を変更しない限り、ローカルの Administrators グループのメンバーを正しく認識しません。

適切なアクセス許可がない状態でコントローラーアクションを呼び出そうとすると、有効になっている認証の種類によって、正確に発生します。 既定では、ASP.NET 開発サーバーを使用すると、空白のページが表示されます。 ページには、401の**承認されていない**HTTP 応答ステータスが提供されます。

一方、匿名認証を無効にし、基本認証を有効にした状態で IIS を使用している場合は、保護されたページを要求するたびにログインダイアログプロンプトが表示されます (図4を参照)。

**図4–基本認証のログインダイアログ**

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a>まとめ

このチュートリアルでは、ASP.NET MVC アプリケーションのコンテキストで Windows 認証を使用する方法について説明しました。 アプリケーションの web 構成ファイル内で Windows 認証を有効にする方法と、IIS で認証を構成する方法について学習しました。 最後に、&lt;承認&gt; 属性を使用して、特定の Windows ユーザーまたはグループに対するコントローラーアクションへのアクセスを制限する方法を学習しました。

> [!div class="step-by-step"]
> [前へ](authenticating-users-with-forms-authentication-vb.md)
> [次へ](preventing-javascript-injection-attacks-vb.md)

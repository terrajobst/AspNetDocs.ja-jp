---
uid: whitepapers/overview
title: ホワイトペーパー |Microsoft Docs
author: rick-anderson
description: このページでは、ASP.NET のインストールと構成に役立つホワイトペーパーを紹介し、安全で高速かつ柔軟な ASP.NET アプリケーションの作成を支援します。
ms.author: riande
ms.date: 11/15/2011
ms.assetid: d5e79470-01f2-4d65-8077-11c3e10a6784
msc.legacyurl: /whitepapers
msc.type: content
ms.openlocfilehash: 1a3a9fe5d685d4b38efe666fc88ff57016482ada
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520588"
---
# <a name="whitepapers"></a>ホワイトペーパー

> このページでは、ASP.NET のインストールと構成に役立つホワイトペーパーを紹介し、安全で高速かつ柔軟な ASP.NET アプリケーションの作成を支援します。
> 
> - [ASP.NET 4](#aspnet4)
> - [ASP.NET のセキュリティホワイトペーパー](#security)
> - [インストールとセットアップに関するホワイトペーパー](#setup)
> - [SQL Server ホワイトペーパー](#sql)
> - [一般的なホワイトペーパー](#general)

<a id="aspnet4"></a>
## <a name="aspnet-4"></a>ASP.NET 4

ASP.NET 4 および Visual Studio 2010 に関連する情報。

[ASP.NET MVC 4 リリースノート](mvc4-beta-release-notes.md "mvc4-リリースノート")

このドキュメントでは、ASP.NET MVC 4 Developer Preview for Visual Studio 2010 で導入された新機能と機能強化に加え、インストールに関する注意事項と既知の問題について説明します。

[ASP.NET MVC 3 リリースノート](mvc3-release-notes.md "mvc3-リリースノート")

このドキュメントでは、ASP.NET MVC 3 で導入された新機能と機能強化に加え、インストールに関する注意事項と既知の問題について説明します。

[ASP.NET 4 と Visual Studio 2010 Web 開発の概要](aspnet4/index.md "aspnet4")

ASP.NET の多くの魅力的な変更は .NET Framework バージョン4で公開されています。 このドキュメントでは、今後のリリースに含まれる多くの新機能の概要を示します。

[ASP.NET 4 Beta 2 の重大な変更](aspnet4/breaking-changes.md "重大な変更")

このドキュメントでは、以前のリリース (ASP.NET 4 beta 1 リリースを含む) を使用して作成されたアプリケーションに影響する可能性がある .NET Framework version 4 beta 2 リリース (つまり、ASP.NET 4 Beta 2 リリース) に加えられた変更について説明します。

[ASP.NET MVC 2 の新機能](what-is-new-in-aspnet-mvc.md "aspnet mvc の新機能")

このドキュメントでは、ASP.NET MVC 2 で導入された新機能と機能強化について説明します。

[ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードする](aspnet-mvc2-upgrade-notes.md "aspnet-mvc2")

ASP.NET MVC 2 は、同じサーバーに ASP.NET MVC 1.0 とサイドバイサイドでインストールできます。 これにより、アプリケーション開発者は、ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードするタイミングを柔軟に選択できます。 このドキュメントでは、ついて説明を手動でアップグレードする方法と、ビジュアルでウィザードを使用する方法の両方を説明します。

<a id="security"></a>
## <a name="aspnet-security-whitepapers"></a>ASP.NET のセキュリティホワイトペーパー

セキュリティはインターネットアプリケーションの重要な要素であり、これらのホワイトペーパーでは、secure ASP.NET アプリケーションを設計および実装する方法について説明します。

[セキュリティのための ASP.NET 2.0 アプリケーションのインストルメント化](https://msdn.microsoft.com/library/ms998325.aspx)

ここでは、カスタムの正常性監視イベントを使用して、セキュリティ関連のイベントと操作を追跡する ASP.NET アプリケーションをインストルメント化する方法について説明します。 ASP.NET バージョン2.0 は、さまざまな標準のインストルメンテーションを含む正常性の監視を提供します...

[ASP.NET 2.0 のセキュリティ展開の確認を実行する](https://msdn.microsoft.com/library/ms998367.aspx)

この方法では、ASP.NET 2.0 アプリケーションのセキュリティ展開の確認を実行し、不適切な構成設定によって発生する潜在的なセキュリティ脆弱性を特定する方法について説明します。 レビュープロセスの大部分は、

[ASP.NET 2.0 のロールに ADAM を使用する](https://msdn.microsoft.com/library/ms998331.aspx)

ここでは、Active Directory Application Mode (ADAM) を使用して ASP.NET ロールを格納する ASP.NET Web サイトを開発する方法について説明します。 ここでは、ADAM および Authorization Manager (AzMan) ポリシーストアの構成方法、新しいロールを作成する方法、および

[ASP.NET 2.0 で承認マネージャー (AzMan) を使用する](https://msdn.microsoft.com/library/ms998336.aspx)

ここでは、ASP.NET role manager API と共に Authorization Manager (AzMan) を使用してロールを管理する方法、ユーザーロールのメンバーシップを確認する方法、および AzMan ポリシーストアに対して特定の操作を実行するロールを承認する方法について説明します。 操作方法

[ASP.NET 2.0 のメンバーシップを使用する](https://msdn.microsoft.com/library/ms998347.aspx)

この方法では、ASP.NET バージョン2.0 アプリケーションのメンバーシップ機能を使用する方法を示します。 ここでは、2つの異なるメンバーシッププロバイダーを使用する方法を示します。 ActiveDirectoryMembershipProvider と SqlMembershipProvider です。 メンバーシップ機能...

[ASP.NET 2.0 でのロールマネージャーの使用](https://msdn.microsoft.com/library/ms998314.aspx)

ここでは、ASP.NET 2.0 ロールマネージャーの使用方法について説明します。 ロールマネージャーを使用すると、アプリケーションでロールを管理し、ロールベースの承認を実行するタスクを簡単に行うことができます。 ここでは、さまざまなロールプロバイダーを構成して、

[ASP.NET 2.0 で Windows 認証を使用する](https://msdn.microsoft.com/library/ms998358.aspx)

ここでは、ASP.NET Web アプリケーションで Windows 認証を構成して使用する方法について説明します。 Windows 認証は、ユーザーが Windows ドメインの一部である場合に推奨される方法です。 この方法では、既存の id ストアを使用できます...

[マネージコードのセキュリティコードレビューを実行する (ベースラインアクティビティ)](https://msdn.microsoft.com/library/ms998364.aspx)

ここでは、セキュリティコードレビューを実行する方法について説明します。 このモジュールは、アクティビティに関連する手順と、結果を分析する方法を示しています。 ここでは、"セキュリティの質問リスト: マネージコード (.NET Framework 2.0)" を使用する方法について説明します。

[ASP.NET 2.0 のセキュリティ展開の確認を実行する](https://msdn.microsoft.com/library/ms998367.aspx)

この方法では、ASP.NET 2.0 アプリケーションのセキュリティ展開の確認を実行し、不適切な構成設定によって発生する潜在的なセキュリティ脆弱性を特定する方法について説明します。 レビュープロセスの大部分は、

[Windows 2000 の Kerberos 委任を実装する](https://msdn.microsoft.com/library/aa302400.aspx)

Kerberos 委任を使用すると、アプリケーションの複数の物理層で認証済み id をフローし、下流の認証と承認をサポートできます。 ここでは、この作業を行うために必要な構成手順について説明します。

[ASP.NET 2.0 での偽装と委任の使用](https://msdn.microsoft.com/library/ms998351.aspx)

ここでは、ASP.NET 2.0 アプリケーションで偽装を使用する方法とタイミングについて説明します。 既定では、権限借用は無効になっており、ASP.NET Web アプリケーションのプロセス id を使用してリソースにアクセスできます。 ただし、...

[デザイン時に Web アプリケーションの脅威モデルを作成する](https://msdn.microsoft.com/library/ms978527.aspx)

ここでは、Web アプリケーションの脅威モデルを作成する方法について説明します。 脅威のモデル化アクティビティは、セキュリティ設計のモデル化に役立ちます。これにより、潜在的なセキュリティ設計の欠陥と脆弱性を、投資する前に公開できます。

### <a name="forms-authentication"></a>フォーム認証

[ASP.NET 2.0 でフォーム認証を保護する](https://msdn.microsoft.com/library/ms998310.aspx)

ここでは、ASP.NET 2.0 アプリケーションでフォーム認証を安全に構成し、使用する方法を示します。 考慮すべき主な要素は、認証チケットを適切に保護し、ユーザー id ストアとそのストアへのアクセスをセキュリティで保護することです。 ...

[ASP.NET 2.0 の Active Directory でフォーム認証を使用する](https://msdn.microsoft.com/library/ms998360.aspx)

ここでは、ActiveDirectoryMembershipProvider を使用して、Microsoft® Active Directory® Directory サービスでフォーム認証を使用する方法について説明します。 プロバイダーを構成し、ユーザーを作成および認証する方法について説明します。

[ASP.NET 2.0 の複数のドメインで Active Directory でフォーム認証を使用する](https://msdn.microsoft.com/library/ms998345.aspx)

ここでは、ActiveDirectoryMembershipProvider を使用して、Microsoft® Active Directory® Directory サービスでフォーム認証を使用する方法について説明します。 プロバイダーを構成し、ユーザーを作成および認証する方法について説明します。

[ASP.NET 2.0 の SQL Server でフォーム認証を使用する](https://msdn.microsoft.com/library/ms998317.aspx)

ここでは、SQL Server メンバーシッププロバイダーでフォーム認証を使用する方法について説明します。 SQL Server を使用したフォーム認証は、アプリケーションのユーザーが Windows ドメインの一部ではなく、その結果として、最も適用される場合があり,...

[ASP.NET 1.1 でフォーム認証を使用して GenericPrincipal オブジェクトを作成する](https://msdn.microsoft.com/library/aa302399.aspx)

ここでは、フォーム認証を使用して GenericPrincipal オブジェクトと FormsIdentity オブジェクトを作成および処理する方法について説明します。

[ASP.NET 1.1 の Active Directory でフォーム認証を使用する](https://msdn.microsoft.com/library/aa302397.aspx)

この記事では、Active Directory 資格情報ストアに対してフォーム認証を実装する方法について説明します。

[ASP.NET 1.1 の SQL Server でフォーム認証を使用する](https://msdn.microsoft.com/library/aa302398.aspx)

ここでは、SQL Server 資格情報ストアに対してフォーム認証を実装する方法について説明します。 また、データベースにパスワードダイジェストを格納する方法についても説明します。

### <a name="user-input-data-validation"></a>ユーザー入力データの検証

[要求の検証 - スクリプト攻撃の防止](request-validation.md "要求-検証")

このホワイトペーパーでは、ASP.NET の要求検証機能について説明します。既定では、アプリケーションは、エンコードされていない HTML コンテンツをサーバーに送信できません。 この要求の検証機能は、アプリケーションが実行されたときに無効にすることができます...

[ASP.NET でクロスサイトスクリプティングを防止する](https://msdn.microsoft.com/library/ms998274.aspx)

ここでは、適切な入力検証手法を使用し、出力をエンコードすることで、クロスサイトスクリプト攻撃から ASP.NET アプリケーションを保護する方法について説明します。 また、で使用できるその他のさまざまな保護メカニズムについても説明します。

[ASP.NET で SQL インジェクションから保護する](https://msdn.microsoft.com/library/ms998271.aspx)

この方法では、SQL インジェクション攻撃から ASP.NET アプリケーションを保護するためのさまざまな方法を紹介します。 SQL インジェクションは、アプリケーションが入力を使用して動的 SQL ステートメントを作成するとき、またはストアドプロシージャを使用して...

[正規表現を使用して ASP.NET の入力を制限する](https://msdn.microsoft.com/library/ms998267.aspx)

この方法では、ASP.NET アプリケーション内で正規表現を使用して、信頼されていない入力を制限する方法を示します。 正規表現は、名前、住所、電話番号、その他のユーザー情報などのテキストフィールドを検証するのに適した方法です。 使用できる...

### <a name="code-access-security"></a>コード アクセス セキュリティ

[ASP.NET 2.0 でコードアクセスセキュリティを使用する](https://msdn.microsoft.com/library/ms998326.aspx)

ここでは、アプリケーションに適切な信頼レベルを選択する方法と、カスタムの ASP.NET コードアクセスセキュリティポリシーファイルを作成してカスタムの信頼レベルを定義する方法について説明します。 さまざまなコードアクセスセキュリティ信頼を使用できます...

[カスタム暗号化アクセス許可を作成する](https://msdn.microsoft.com/library/aa302362.aspx)

ここでは、Win32® Data Protection API (DPAPI) によって提供されるアンマネージ暗号化機能へのプログラムによるアクセスを制御するための、カスタムコードアクセスセキュリティのアクセス許可を作成する方法について説明します。 このカスタムアクセス許可は、管理されている DPAPI ラッパーで使用します...

[コードアクセスセキュリティポリシーを使用してアセンブリを制限する](https://msdn.microsoft.com/library/aa302361.aspx)

管理者は、コードアクセスセキュリティポリシーを構成して、.NET Framework コード (アセンブリ) の操作を制限することができます。 この方法では、コードアクセスセキュリティポリシーを構成して、ファイル i/o を実行するアセンブリの機能を制限し、...

### <a name="communications-security"></a>通信のセキュリティ

[Web サーバーで SSL を設定する](https://msdn.microsoft.com/library/aa302411.aspx)

クライアントアプリケーションからの https 接続をサポートするために、Web サーバーが SSL 用に構成されている必要があります。 ここでは、Web サーバーで SSL を構成する方法について説明します。

[クライアント証明書の設定](https://msdn.microsoft.com/library/aa302412.aspx)

IIS は、クライアント証明書の認証をサポートしています。 ここでは、クライアント証明書を要求するように Web アプリケーションを構成する方法について説明します。 また、クライアントコンピューターに証明書をインストールし、Web アプリケーションを呼び出すときに証明書を使用する方法についても説明します。

[IPSec を使用してポートと認証をフィルター処理する](https://msdn.microsoft.com/library/aa302366.aspx)

インターネットプロトコルセキュリティ (IPSec) は、サービスではなく、IP ベースのネットワークトラフィックに対して暗号化、整合性、および認証サービスを提供するプロトコルです。 IPSec ではサーバー間の保護が提供されるため、IPSec を使用して内部の脅威に対抗することができます。

[IPSec を使用して、2つのサーバー間のセキュリティで保護された通信を提供する](https://msdn.microsoft.com/library/aa302413.aspx)

IPSec は、2つのサーバー間に暗号化されたチャネルを作成することを可能にする Windows 2000 によって提供されるテクノロジです。 IPSec は、IP トラフィックをフィルター処理し、サーバーを認証するために使用できます。 ここでは、セキュリティで保護された (暗号化された) を提供するように IPSec を構成する方法について説明します。

[SSL を使用して SQL Server との通信をセキュリティで保護する](https://msdn.microsoft.com/library/aa302414.aspx)

アプリケーションでは、SQL Server データベースサーバーとの間でやり取りされるデータをセキュリティで保護できることが重要です。 SQL Server では、SSL を使用して暗号化されたチャネルを作成できます。 ここでは、データベースサーバーに証明書をインストールする方法について説明します。

[ASP.NET 1.1 からのクライアント証明書を使用して Web サービスを呼び出す](https://msdn.microsoft.com/library/aa302408.aspx)

ここでは、ASP.NET Web アプリケーションまたは Windows フォームアプリケーションからの認証用にクライアント証明書を Web サービスに渡す方法について説明します。 クライアント証明書は、ローカルコンピューターストアまたはユーザーストアのいずれかにインストールできます。 もし...

[ASP.NET 1.1 から SSL を使用して Web サービスを呼び出す](https://msdn.microsoft.com/library/aa302409.aspx)

Secure Sockets Layer (SSL) 暗号化を使用すると、Web サービスとの間で送受信されるメッセージの整合性と機密性を保証できます。 ここでは、Web サービスで SSL を使用する方法について説明します。

### <a name="cryptography"></a>Cryptography

[.NET 1.1 で DPAPI ライブラリを作成する](https://msdn.microsoft.com/library/aa302402.aspx)

ここでは、データを暗号化するアプリケーション (データベース接続文字列、アカウントの資格情報など) に DPAPI 機能を公開するマネージクラスライブラリを作成する方法について説明します。

[.NET 1.1 で暗号化ライブラリを作成する](https://msdn.microsoft.com/library/aa302405.aspx)

ここでは、アプリケーションの暗号化機能を提供するマネージクラスライブラリを作成する方法について説明します。 これにより、アプリケーションで暗号化アルゴリズムを選択できるようになります。 サポートされているアルゴリズムには、DES、Triple DES、RC2、Rijndael があります。

[暗号化された接続文字列をレジストリに格納する ASP.NET 1.1](https://msdn.microsoft.com/library/aa302406.aspx)

アプリケーションでは、接続文字列やアカウントの資格情報などの暗号化されたデータを Windows レジストリに格納することができます。 ここでは、暗号化された文字列をレジストリに格納および取得する方法について説明します。

[ASP.NET 1.1 から DPAPI (マシンストア) を使用する](https://msdn.microsoft.com/library/aa302403.aspx)

ここでは、ASP.NET Web アプリケーションまたは Web サービスから DPAPI を使用して機密データを暗号化する方法について説明します。

[Enterprise Services で ASP.NET 1.1 から DPAPI (ユーザーストア) を使用する](https://msdn.microsoft.com/library/aa302404.aspx)

ここでは、ASP.NET Web アプリケーションまたはサービスから DPAPI を使用して機密データを暗号化する方法について説明します。 ここでは、ユーザーストアで DPAPI を使用する方法について説明します。この場合、アウトプロセスの Enterprise Services コンポーネントを使用する必要があります。

<a id="setup"></a>
## <a name="installation-and-setup-whitepapers"></a>インストールとセットアップに関するホワイトペーパー

これらのホワイトペーパーでは、サーバーに ASP.NET をインストールして構成する手順について説明しています。

[ASP.NET 2.0 アプリケーションのサービスアカウントを作成する](https://msdn.microsoft.com/library/ms998297.aspx)

ここでは、ASP.NET Web アプリケーションを実行するために、カスタムの最小特権サービスアカウントを作成および構成する方法について説明します。 既定では、Microsoft Windows Server 2003 および IIS 6.0 の ASP.NET アプリケーションは、組み込みのネットワークサービスを使用して実行されます。

[ASP.NET 2.0 で複数のアプリケーションをホストするときのセキュリティを強化する](https://msdn.microsoft.com/library/aa480478.aspx)

ここでは、Web ホスティング環境で、複数のアプリケーションを相互に分離する方法と共有システムリソースから分離する方法について説明します。 ホスト環境は、インターネットサービスプロバイダー (ISP) によって提供される Web サーバーであり、複数の...

[ASP.NET 2.0 での中程度の信頼の使用](https://msdn.microsoft.com/library/ms998341.aspx)

ここでは、中程度の信頼で実行されるように ASP.NET Web アプリケーションを構成する方法について説明します。 同じサーバー上で複数のアプリケーションをホストする場合は、コードアクセスセキュリティと中程度の信頼レベルを使用して、アプリケーションの分離を実現できます。 設定

[Network Service アカウントを使用して ASP.NET 2.0 のリソースにアクセスする](https://msdn.microsoft.com/library/ms998320.aspx)

この方法では、NT AUTHORITY\Network Service コンピューターアカウントを使用してローカルリソースとネットワークリソースにアクセスする方法を説明します。 既定では、Windows Server 2003 では、ASP.NET アプリケーションはこのアカウントの id を使用して実行されます。 最小限の特権を持つ...

[ASP.NET 2.0 でのプロトコル遷移と制約付き委任の使用](https://msdn.microsoft.com/library/ms998355.aspx)

ここでは、プロトコル遷移と制約付き委任を構成して使用し、元の呼び出し元の偽装中に ASP.NET アプリケーションがネットワークリソースにアクセスできるようにする方法について説明します。 Microsoft® Windows®2000オペレーティングシステム...

[ASP.NET で .NET Framework 1.0 と 1.1 を並行して実行する](side-by-side-with-10.md "1\.0 とサイドバイサイド")

このホワイトペーパーでは、.NET 1.0 と .NET 1.1 の両方をコンピューターにインストールする方法について説明します。これにより、ASP.NET Web アプリケーションをいずれかのバージョンのフレームワークで実行できるようになります。

[ASP.NET の IIS ディレクトリのアクセス拒否](denied-access-to-iis-directories.md "iis ディレクトリへのアクセスが拒否されました")

このホワイトペーパーでは、ASP.NET アプリケーションに対する要求で " *DirectoryName*ディレクトリへのアクセスが拒否されました" というエラーが返された場合の対処方法について説明します。 ディレクトリの変更の監視を開始できませんでした。 "

[IIS 6.0 で ASP.NET 1.1 を実行する](aspnet-and-iis6.md "aspnet および iis6")

Windows Server 2003 には IIS 6.0 と ASP.NET 1.1 の両方が含まれていますが、これらのコンポーネントは既定で無効になっています。 このホワイトペーパーでは、IIS 6.0 と ASP.NET 1.1 を有効にする方法について説明し、最適な構成を実現するためにいくつかの構成設定を推奨します。

[IE のセキュリティ更新プログラムを適用した後の "サーバーアプリケーションが使用できません" エラーの修正](ms03-32-issue.md "ms03-32-問題")

このホワイトペーパーでは、Windows XP Professional で実行されている ASP.NET 1.0 アプリケーションに影響する Internet Explorer の MS03-32 セキュリティ更新プログラムに関する問題を修正する修正プログラムについて説明します。

[ASP.NET 1.1 を実行するカスタムアカウントを作成する](https://msdn.microsoft.com/library/aa302396.aspx)

ASP.NET Web アプリケーションは、通常、組み込みの ASPNET アカウントを使用して実行されます。 場合によっては、代わりにカスタムアカウントを使用することもできます。 この記事では、ASP.NET Web アプリケーションを実行するために最小限の特権を持つローカルアカウントを作成する方法について説明します。 ...

### <a name="configuration"></a>構成

[ASP.NET 2.0 でのマシンキーの構成](https://msdn.microsoft.com/library/ms998288.aspx)

ここでは、web.config ファイルの &lt;machineKey&gt; 要素について説明し、&lt;machineKey&gt; 要素を構成して、ViewState、フォーム認証チケット、およびロールクッキーの改ざんによる校正と暗号化を制御する方法を示します。 ViewState が署名されています...

[DPAPI を使用して ASP.NET 2.0 の構成セクションを暗号化する](https://msdn.microsoft.com/library/ms998280.aspx)

この方法では、Windows データ保護アプリケーションプログラミングインターフェイス (DPAPI) で保護されている構成プロバイダーと Aspnet\_iis 登録ツールツールを使用して、構成ファイルのセクションを暗号化する方法を示します。 Aspnet\_iis 登録ツールツールを使用して、...

[RSA を使用して ASP.NET 2.0 の構成セクションを暗号化する](https://msdn.microsoft.com/library/ms998283.aspx)

この方法では、RSA 保護された構成プロバイダーおよび Aspnet\_iis 登録ツールツールを使用して、構成ファイルのセクションを暗号化する方法を示します。 Aspnet\_iis 登録ツールツールを使用して、接続文字列などの機密データを暗号化できます。

[ASP.NET 2.0 での偽装と委任の使用](https://msdn.microsoft.com/library/ms998351.aspx)

ここでは、ASP.NET 2.0 アプリケーションで偽装を使用する方法とタイミングについて説明します。 既定では、権限借用は無効になっており、ASP.NET Web アプリケーションのプロセス id を使用してリソースにアクセスできます。 ただし、...

<a id="sql"></a>
## <a name="sql-server-whitepapers"></a>SQL Server ホワイトペーパー

ASP.NET はさまざまなデータベースで動作しますが、これらのホワイトペーパーは、特に ASP.NET アプリケーションを SQL Server に接続することを目的としています。

[ASP.NET 2.0 で SQL 認証を使用して SQL Server に接続する](https://msdn.microsoft.com/library/ms998300.aspx)

ここでは、データベースアクセス認証でネイティブ SQL 認証を使用する場合に、ASP.NET アプリケーションを Microsoft® SQL Server™に安全に接続する方法について説明します。 Windows 認証は、SQL Server に接続するために推奨される方法です。

[ASP.NET 2.0 で Windows 認証を使用して SQL Server に接続する](https://msdn.microsoft.com/library/ms998292.aspx)

この方法では、ASP.NET バージョン2.0 アプリケーションから Windows サービスアカウントを使用して SQL Server 2000 に接続する方法について説明します。 可能な限り、SQL 認証ではなく Windows 認証を使用してください。

[SSL を使用して SQL Server 2000 との通信をセキュリティで保護する](https://msdn.microsoft.com/library/aa302414.aspx)

アプリケーションでは、SQL Server データベースサーバーとの間でやり取りされるデータをセキュリティで保護できることが重要です。 SQL Server では、SSL を使用して暗号化されたチャネルを作成できます。 ここでは、データベースサーバーに証明書をインストールする方法について説明し,...

<a id="general"></a>
## <a name="general-whitepapers"></a>一般的なホワイトペーパー

次のケーススタディでは、従来のホスティング環境から Microsoft Azure に Microsoft .NET コミュニティ web サイトを移行するために使用されたプロセスについて説明します。

[Microsoft の ASP.NET および IIS.NET コミュニティ Web サイトを Microsoft Azure に移行する](https://go.microsoft.com/fwlink/?LinkId=400656)

これらのホワイトペーパーでは、ASP.NET に関するさまざまなトピックを取り上げています。

[ASP.NET 2.0 での正常性監視の使用](https://msdn.microsoft.com/library/ms998306.aspx)

ここでは、正常性監視を使用して、アプリケーションにカスタムイベントをインストルメント化する方法について説明します。 カスタムの正常性監視イベントを作成するには、WebBaseEvent から派生するクラスを作成し、&lt;healthMonitoring&gt; を構成します。

[修正プログラム管理の実装](https://msdn.microsoft.com/library/aa302364.aspx)

この方法では、1台または複数のサーバーを最新の状態に保つ方法など、修正プログラムの管理について説明します。 Microsoft からダウンロードできるツールを除き、追加のソフトウェアは必要ありません。 操作とセキュリティポリシーでは、修正プログラムの管理を採用する必要があります...

[Silverlight 3 SDK での Silverlight の ASP.NET サーバーコントロール](https://go.microsoft.com/fwlink/?LinkId=153377)

Silverlight 用の ASP.NET サーバーコントロール ("ASP.NET Silverlight コントロール") は、ASP.NET MediaPlayer および Silverlight コントロールですが、silverlight SDK for Silverlight バージョン3では削除されています。 このドキュメントでは、これらの ASP.NET を扱った開発者向けのガイダンスを提供します。

[高パフォーマンスの Web アプリケーションの構築](https://devexpress.com/act)

ASP.NET Ajax ライブラリの新機能を使用して、高パフォーマンスの Web アプリケーションを構築する方法について説明します。

---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: フォーム認証を使用してユーザーを認証する (VB) |Microsoft Docs
author: microsoft
description: '[承認] 属性を使用して、MVC アプリケーションの特定のページをパスワードで保護する方法について説明します。 Web サイトの管理を使用する方法についても説明します。'
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: a2c2140631d59a7f8b21aa73613a92ea5c7a91d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498934"
---
# <a name="authenticating-users-with-forms-authentication-vb"></a>フォーム認証でユーザーを認証する (VB)

[Microsoft](https://github.com/microsoft)

> [承認] 属性を使用して、MVC アプリケーションの特定のページをパスワードで保護する方法について説明します。 Web サイト管理ツールを使用して、ユーザーとロールを作成および管理する方法について説明します。 また、ユーザーアカウントとロール情報を格納する場所を構成する方法についても説明します。

このチュートリアルの目的は、フォーム認証を使用して、ASP.NET MVC アプリケーションのビューをパスワードで保護する方法を説明することです。 Web サイト管理ツールを使用して、ユーザーとロールを作成する方法について説明します。 また、承認されていないユーザーがコントローラーアクションを呼び出さないようにする方法についても説明します。 最後に、ユーザー名とパスワードが格納される場所を構成する方法について説明します。

#### <a name="using-the-web-site-administration-tool"></a>Web サイト管理ツールの使用

他の作業を行う前に、まずユーザーとロールをいくつか作成する必要があります。 新しいユーザーとロールを作成する最も簡単な方法は、Visual Studio 2008 Web サイト管理ツールを利用することです。 このツールを起動するには、メニューオプション**プロジェクトの [ASP.NET Configuration**] を選択します。 または、[ソリューションエクスプローラー] ウィンドウの上部に表示される、ハンマーの (少し恐ろしい) アイコンをクリックして、Web サイト管理ツールを起動することもできます (図1を参照)。

**図 1: Web サイト管理ツールの起動**

![clip_image002[4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

Web サイト管理ツールで、セキュリティ タブを選択して新しいユーザーとロールを作成します。 **ユーザーの作成** リンクをクリックして、Stephen という名前の新しいユーザーを作成します (図2を参照)。 Stephen ユーザーに必要なパスワード (たとえば、 *secret*) を入力します。

**図2–新しいユーザーの作成**

![clip_image004[4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

新しいロールを作成するには、最初にロールを有効にし、1つ以上のロールを定義します。 **[ロールの有効化]** リンクをクリックして、ロールを有効にします。 次に、 **[ロールの作成または管理]** リンクをクリックして、*管理者*という名前のロールを作成します (図3を参照)。

**図3–新しいロールを作成する**

![clip_image006[4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

最後に、[ユーザーの作成] リンクをクリックし、[ユーザーの作成時に管理者を選択する] をクリックして、"ユーザー名" という名前の新しいユーザーを作成し、管理者ロールに関連付けます (図4を参照)。

**図4–ロールへのユーザーの追加**

![clip_image008[4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

すべてが完了したら、2つの新しいユーザーを Stephen として作成する必要があります。 また、Administrators という名前の新しいロールも必要です。 Stephen が管理者ロールのメンバーであり、かつ、そのメンバーがではありません。

#### <a name="requiring-authorization"></a>承認が必要

ユーザーが [承認] 属性をアクションに追加することによってコントローラーアクションを呼び出す前に、ユーザーの認証を要求することができます。 [承認] 属性を個々のコントローラーアクションに適用することも、この属性をコントローラークラス全体に適用することもできます。

たとえば、リスト1のコントローラーは、企業秘密 () という名前のアクションを公開します。 このアクションは [承認] 属性で修飾されているため、ユーザーが認証されていない限り、このアクションを呼び出すことはできません。

**リスト1– Controllers\HomeController.vb**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

ブラウザーのアドレスバーに/Home/CompanySecrets URL を入力して会社のシークレット () アクションを呼び出すと、認証されたユーザーではない場合、ログインビューに自動的にリダイレクトされます (図5を参照)。

**図 5-ログインビュー**

![clip_image010[4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

ログインビューを使用して、ユーザー名とパスワードを入力できます。 登録済みのユーザーでない場合は、 **[登録]** リンクをクリックしてレジスタビューに移動できます (図6を参照)。 新しいユーザーアカウントを作成するには、[登録] ビューを使用します。

**図6–レジスタビュー**

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

ログインに成功すると、会社のシークレットビューが表示されます (図7を参照)。 既定では、ブラウザーウィンドウを閉じるまでログインしたままになります。

**図 7-会社の機密情報の表示**

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>ユーザー名またはユーザーロールによる承認

[承認] 属性を使用して、コントローラーアクションへのアクセスを特定のユーザーセットまたは特定のユーザーロールのセットに制限することができます。 たとえば、リスト2の変更されたホームコントローラーには、StephenSecrets () と [アドミニストレーターシークレット ()] という2つの新しいアクションが含まれています。

**リスト2– Controllers\HomeController.vb**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

ユーザー名 Stephen を持つユーザーのみが StephenSecrets () アクションを呼び出すことができます。 他のすべてのユーザーは、ログインビューにリダイレクトされます。 Users プロパティは、ユーザーアカウント名のコンマ区切りの一覧を受け取ります。

管理者のシークレット () アクションを呼び出すことができるのは、Administrators ロールのユーザーだけです。 たとえば、ユーザーが管理者グループのメンバーである場合、管理者のシークレット () アクションを呼び出すことができます。 他のすべてのユーザーは、ログインビューにリダイレクトされます。 Roles プロパティは、ロール名のコンマ区切りリストを受け入れます。

#### <a name="configuring-authentication"></a>認証の構成

この時点で、ユーザーアカウントとロール情報が保存されている場所について疑問に思うかもしれません。 既定では、情報は、MVC アプリケーションの App\_Data フォルダーにある ASPNETDB.MDF という名前の (RANU) SQL Express データベースに格納されます。 このデータベースは、メンバーシップの使用を開始すると、ASP.NET フレームワークによって自動的に生成されます。

ソリューションエクスプローラーウィンドウで ASPNETDB.MDF データベースを表示するには、まずメニューオプションプロジェクト [すべてのファイルを表示] を選択する必要があります。

アプリケーションを開発する場合は、既定の SQL Express データベースを使用するのが適切です。 ただし、ほとんどの場合、実稼働アプリケーションで既定の ASPNETDB.MDF データベースを使用する必要はありません。 その場合は、次の2つの手順を実行して、ユーザーアカウント情報の保存場所を変更できます。

1. 実稼働データベースにアプリケーションサービスデータベースオブジェクトを追加する-実稼働データベースを指すようにアプリケーションの接続文字列を変更する

最初の手順では、必要なすべてのデータベースオブジェクト (テーブルとストアドプロシージャ) を実稼働データベースに追加します。 これらのオブジェクトを新しいデータベースに追加する最も簡単な方法は、ASP.NET SQL Server セットアップウィザードを利用することです (図8を参照)。 このツールを起動するには、Microsoft Visual Studio 2008 プログラムグループから Visual Studio 2008 コマンドプロンプトを開き、コマンドプロンプトから次のコマンドを実行します。

aspnet\_regsql

**図 8-ASP.NET SQL Server セットアップウィザード**

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

ASP.NET SQL Server セットアップウィザードでは、ネットワーク上の SQL Server データベースを選択し、ASP.NET アプリケーションサービスに必要なすべてのデータベースオブジェクトをインストールすることができます。 データベースサーバーがローカルコンピューターに配置されている必要はありません。

> [!NOTE]
> ASP.NET SQL Server セットアップウィザードを使用しない場合は、次のフォルダーにアプリケーションサービスデータベースオブジェクトを追加するための SQL スクリプトを見つけることができます。
> 
> 
> C:\Windows\Microsoft.NET\Framework\v2.0.50727

必要なデータベースオブジェクトを作成した後、MVC アプリケーションで使用されるデータベース接続を変更する必要があります。 Web 構成 (web.config) ファイル内の ApplicationServices 接続文字列を変更して、実稼働データベースをポイントするようにします。 たとえば、リスト3の変更された接続は、MyProductionDB という名前のデータベースを指しています (元の ApplicationServices 接続文字列はコメントアウトされています)。

**リスト3– web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>データベースのアクセス許可の構成

統合セキュリティを使用してデータベースに接続する場合は、正しい Windows ユーザーアカウントをログインとしてデータベースに追加する必要があります。 正しいアカウントは、web サーバーとして ASP.NET 開発サーバーまたはインターネットインフォメーションサービスのどちらを使用しているかによって異なります。 正しいユーザーアカウントは、使用しているオペレーティングシステムにも依存します。

ASP.NET 開発サーバー (Visual Studio で使用される既定の web サーバー) を使用している場合、アプリケーションは Windows ユーザーアカウントのコンテキスト内で実行されます。 その場合は、Windows ユーザーアカウントをデータベースサーバーログインとして追加する必要があります。

または、インターネットインフォメーションサービスを使用する場合は、ASPNET アカウントまたは NT AUTHORITY/NETWORK サービスアカウントをデータベースサーバーログインとして追加する必要があります。 Windows XP を使用している場合は、ASPNET アカウントをログインとしてデータベースに追加します。 Windows Vista や Windows Server 2008 など、より新しいオペレーティングシステムを使用している場合は、データベースログインとして NT AUTHORITY/NETWORK SERVICE アカウントを追加します。

Microsoft SQL Server Management Studio を使用して、新しいユーザーアカウントをデータベースに追加できます (図9を参照)。

**図9–新しい Microsoft SQL Server ログインを作成する**

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

必要なログインを作成した後、適切なデータベースロールを持つデータベースユーザーにログインをマップする必要があります。 ログインをダブルクリックし、[ユーザーマッピング] タブを選択します。1つまたは複数のアプリケーションサービスデータベースロールを選択します。 たとえば、ユーザーを認証するには、aspnet\_メンバーシップ\_BasicAccess データベースロールを有効にする必要があります。 新しいユーザーを作成するには、aspnet\_メンバーシップ\_FullAccess データベースロールを有効にする必要があります (図10を参照)。

**図 10-アプリケーションサービスデータベースロールの追加**

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a>まとめ

このチュートリアルでは、ASP.NET MVC アプリケーションを構築するときにフォーム認証を使用する方法について学習しました。 まず、Web サイト管理ツールを利用して、新しいユーザーとロールを作成する方法を学習しました。 次に、[承認] 属性を使用して、承認されていないユーザーがコントローラーアクションを呼び出さないようにする方法を学習しました。 最後に、ユーザーとロールの情報を運用データベースに格納するように MVC アプリケーションを構成する方法について学習しました。

> [!div class="step-by-step"]
> [前へ](preventing-javascript-injection-attacks-cs.md)
> [次へ](authenticating-users-with-windows-authentication-vb.md)

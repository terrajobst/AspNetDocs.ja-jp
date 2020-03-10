---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
title: 運用 Web サイトのユーザーとロール (C#) |Microsoft Docs
author: rick-anderson
description: ASP.NET Web サイト管理ツール (WSAT) は、メンバーシップとロールの設定を構成するための web ベースのユーザーインターフェイスと、作成、編集、...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: dbc54313-5d05-4285-98b3-726edea6d0c9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
msc.type: authoredcontent
ms.openlocfilehash: c47bd2c1661f129dd8856916de04b8ba459fbfec
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441220"
---
# <a name="users-and-roles-on-the-production-website-c"></a>運用 Web サイトのユーザーとロール (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_cs.pdf)

> ASP.NET Web サイト管理ツール (WSAT) には、メンバーシップとロールの設定を構成したり、ユーザーとロールを作成、編集、および削除したりするための web ベースのユーザーインターフェイスが用意されています。 残念ながら、WSAT は localhost からアクセスした場合にのみ機能します。つまり、ブラウザーを使用して運用 web サイトの管理ツールにアクセスすることはできません。 実は、運用環境でユーザーとロールを管理するための回避策があるということです。 このチュートリアルでは、これらの回避策とその他の方法について見ていきます。

## <a name="introduction"></a>はじめに

ASP.NET 2.0 では、いくつかの*アプリケーションサービス*が導入されました。これは、web アプリケーションに追加できるビルディングブロックサービスのスイートです。 [*アプリケーションサービスチュートリアルを使用した web サイトの構成*](configuring-a-website-that-uses-application-services-cs.md)に関するドキュメントの「Book review」 Web サイトに、メンバーシップと役割のサービスを追加しました。 メンバーシップサービスは、ユーザーアカウントの作成と管理を容易にします。Roles サービスは、ユーザーをグループに分類するための API を提供します。 書籍レビューサイトには、Scott、Jisun、および Alice という3つのユーザーアカウントと、管理者ロールに Scott と Jisun を持つ1つのロール Admin があります。

ASP.NET のアプリケーションサービスは、特定の実装に関連付けられていません。 代わりに、特定の*プロバイダー*を使用するようにアプリケーションサービスに指示します。このプロバイダーは、特定のテクノロジを使用してサービスを実装します。 Books review web アプリケーションは、メンバーシップサービスとロールサービスの `SqlMembershipProvider` と `SqlRoleProvider` プロバイダーを使用するように構成されています。 これらの2つのプロバイダーは、ユーザーアカウントとロール情報を SQL Server データベースに格納します。これは、web ホスティング会社でホストされているインターネットベースの web アプリケーションで最もよく使用されるプロバイダーです。

メンバーシップサービスとロールサービスを使用する開発者にとっての一般的な課題は、運用環境でのユーザーとロールの管理です。 運用 web サイトからユーザーアカウントを削除したり、新しいロールを追加したり、既存のユーザーを既存のロールに追加したりするにはどうすればよいですか。 このチュートリアルでは、運用 web サイトでユーザーとロールを管理するためのさまざまな手法について説明します。

## <a name="using-the-aspnet-web-site-administration-tool"></a>ASP.NET Web サイト管理ツールの使用

ASP.NET には、ユーザーアカウントとロールの作成と管理、およびユーザーとロールベースの承認規則の指定を簡単に行うことができる[Web サイト管理ツール](https://msdn.microsoft.com/library/yy40ytx0.aspx)(WSAT) が含まれています。 WSAT を使用するには、ソリューションエクスプローラーの [ASP.NET 構成] アイコンをクリックするか、Web サイトまたは [プロジェクト] メニューにアクセスして、ASP.NET 構成オプションを選択します。 どちらの方法でも web ブラウザーが起動され、次のようなアドレスで WSAT が参照されます。 `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`

WSAT は、次の3つのセクションに分かれています。

- **セキュリティ**-ユーザー、ロール、および承認規則を管理します。
- **Applicationconfiguration** -ここから &lt;appSettings&gt; と SMTP の設定を管理します。 また、アプリケーションをオフラインにして、ここからデバッグとトレースの設定を管理したり、既定のカスタムエラーページを指定したりすることもできます。
- **Providerconfiguration** -アプリケーションサービスによって使用されるプロバイダーを構成します。

セキュリティセクション (**図 1**を参照) には、新しいユーザーの作成、ユーザーの管理、ロールの作成と管理、およびアクセス規則の作成と管理を行うためのリンクが含まれています。 ここから、システムに新しいロールを追加したり、既存のユーザーを削除したり、特定のユーザーアカウントのロールを追加または削除したりできます。

[![](users-and-roles-on-the-production-website-cs/_static/image2.png)](users-and-roles-on-the-production-website-cs/_static/image1.png)

**図 1**: WSAT セキュリティセクションには、ユーザーと役割を管理するためのオプションが含まれています。  
([クリックすると、フルサイズの画像が表示](users-and-roles-on-the-production-website-cs/_static/image3.png)される)

残念ながら、WSAT にはローカルでしかアクセスできません。 リモート運用 web サイトの WSAT にアクセスすることはできません。`www.yoursite.com/asp.netwebadminfiles/default.aspx` にアクセスすると、"404 が見つかりません" という応答が返されます。 WSAT を強化するコードでは、.NET Framework の `Membership` クラスと `Roles` クラスを使用して、ユーザーとロールの作成、編集、および削除を行います。 これらのクラスは、web アプリケーションの構成情報を参照して、使用するプロバイダーを決定します。「アプリケーションサービスを[*使用した web サイトの構成*」チュートリアル](configuring-a-website-that-uses-application-services-cs.md)に戻り、`SqlMembershipProvider` と `SqlRoleProvider` プロバイダーを使用するように Book review web サイトを設定しました。 これにより、`<membership>` セクションと `<roleManager>` セクションが `Web.config`に追加されます。

[!code-xml[Main](users-and-roles-on-the-production-website-cs/samples/sample1.xml)]

`<membership>` セクションと `<roleManager>` セクションでは、それぞれ `type` 属性の `SqlMembershipProvider` および `SqlRoleProvider` プロバイダーが参照されていることに注意してください。 これらのプロバイダーは、指定された SQL Server データベースにユーザーとロールの情報を格納します。 これらのプロバイダーによって使用されるデータベースは、`~/ConfigSections/databaseConnectionStrings.config` ファイルで定義されている `connectionStringName` 属性 `ReviewsConnectionString`によって指定されます。 開発環境の `databaseConnectionStrings.config` ファイルには開発データベースへの接続文字列が含まれているのに対し、運用環境の `databaseConnectionStrings.config` ファイルには運用データベースへの接続文字列が含まれていることに注意してください。

簡単に言うと、WSAT は開発環境を通じてローカルにアクセスする必要があり、これは `databaseConnectionStrings.config` ファイルに指定されているデータベース内のユーザーとロールの情報で機能します。 そのため、開発環境で `databaseConnectionStrings.config` ファイル内の接続文字列情報を変更した場合は、WSAT をローカルで使用して、運用環境のユーザーとロールを管理できます。

この機能を説明するために、開発環境で Visual Studio の `databaseConnectionStrings.config` ファイルを開き、開発データベースの接続文字列を実稼働データベースの接続文字列に置き換えます。 次に、WSAT を起動し、[セキュリティ] タブにアクセスして、"password!" という名前の Sam という名前の新しいユーザーを追加します。 (引用符を除く)。 **図 2**は、このアカウントを作成するときの WSAT 画面を示しています。

[![](users-and-roles-on-the-production-website-cs/_static/image5.png)](users-and-roles-on-the-production-website-cs/_static/image4.png)

**図 2**: 運用環境で Sam という名前の新しいユーザーを作成する  
([クリックすると、フルサイズの画像が表示](users-and-roles-on-the-production-website-cs/_static/image6.png)される)

実稼働データベースサーバーを指すように `databaseConnectionStrings.config` の接続文字列を変更したので、Sam が運用環境のユーザーとして追加されました。 これを確認するには、`databaseConnectionStrings.config` ファイルの接続文字列を開発データベースに戻し、開発環境の [`Login.aspx`] ページに移動します。 Sam としてサインインします (**図 3**を参照)。

[![](users-and-roles-on-the-production-website-cs/_static/image8.png)](users-and-roles-on-the-production-website-cs/_static/image7.png)

**図 3**: 開発環境で Sam としてサインインできない  
([クリックすると、フルサイズの画像が表示](users-and-roles-on-the-production-website-cs/_static/image9.png)される)

開発環境で Sam としてサインインすることはできません。これは、ユーザーアカウント情報がローカルデータベースに存在しないためです。 代わりに、が運用データベースに追加されました。 これを確認するには、開発データベースと運用データベースの両方で `aspnet_Users` テーブルの内容を表示します。 開発環境では、Scott、Jisun、および Alice のユーザーに対して記録されるレコードは3つだけです。 ただし、実稼働データベースの `aspnet_Users` テーブルには、Scott、Jisun、Alice、および Sam という4つのレコードがあります。 その結果、Sam は、開発環境ではなく、運用環境の web サイトからサインインできます。

[![](users-and-roles-on-the-production-website-cs/_static/image11.png)](users-and-roles-on-the-production-website-cs/_static/image10.png)

**図 4**: Sam が運用 Web サイトにサインインできる  
([クリックすると、フルサイズの画像が表示](users-and-roles-on-the-production-website-cs/_static/image12.png)される)

> [!NOTE]
> WSAT の操作が完了したら、`databaseConnectionStrings.config` ファイル内の接続文字列を開発データベースの接続文字列に戻すことを忘れないでください。それ以外の場合は、開発環境でサイトをテストするときに実稼働データを操作します。 また、ここで説明した手法を使用すると、WSAT を使用してユーザーとロールをリモートで管理できるようになります。他の WSAT 構成オプション (アクセス規則、SMTP 設定、デバッグとトレースの設定など) を変更した場合は、`Web.config` ファイルを変更してください。 そのため、設定に加えられた変更は、運用環境ではなく、開発環境に適用されます。

## <a name="creating-custom-user-and-role-management-web-pages"></a>カスタムユーザーおよびロール管理 Web ページの作成

WSAT は、ユーザーとロールを管理するためのすぐに使用できるシステムを提供しますが、ローカルでのみ起動できます。また、運用環境でユーザーとロールを管理するために、接続文字列情報を変更する必要があります。 ユーザーアカウントをサポートするほとんどの web サイトには、管理者がサイト内のページからユーザーと役割を管理できるようにする、多数のユーザーおよび役割の管理 web ページも含まれています。 このような web ベースの管理ページを使用すると、ユーザーとロールの管理が非常に簡単になります。また、WSAT を起動するために Visual Studio を使用するために、または技術的な背景にアクセスすることのできない管理者や管理者がいるサイトにとっては重要です。

ASP.NET には、さまざまなログイン関連の Web コントロールが組み込まれており、これらの web ページの多くはドラッグアンドドロップ操作で簡単に実装できます。 たとえば、管理者用のページを作成して、CreateUserWizard コントロールをページにドラッグし、いくつかのプロパティを設定することによって、新しいユーザーアカウントを作成できます。 実際、**図 2**に示す WSAT でユーザーを作成するためのページには、ページに追加できるのと同じ CreateUserWizard コントロールが使用されています。 さらに、メンバーシップと役割サービスの機能は、.NET Framework の `Membership` クラスと `Roles` クラスを使用してプログラムで利用できます。 これらのクラスを使用すると、ユーザーとロールの作成、編集、削除を行うコードを記述したり、ユーザーをロールに追加または削除したり、ロールのユーザーを特定したり、他のユーザーやロールに関連するタスクを実行したりできます。

「 [*アプリケーションサービスを使用した web サイトの構成*」チュートリアル](configuring-a-website-that-uses-application-services-cs.md)では、`CreateAccount.aspx`という名前の `Admin` フォルダーにページを追加しました。 このページを使用すると、管理者は新しいユーザーアカウントをサイトに追加し、新しく作成されたユーザーが管理者ロールに存在するかどうかを指定できます (**図 5**を参照)。

[![](users-and-roles-on-the-production-website-cs/_static/image14.png)](users-and-roles-on-the-production-website-cs/_static/image13.png)

**図 5**: 管理者が新しいユーザーアカウントを作成する  
([クリックすると、フルサイズの画像が表示](users-and-roles-on-the-production-website-cs/_static/image15.png)される)

詳細については、「ユーザーと役割の管理」のページを参照してください。 `Membership` および `Roles` クラスとログイン関連の ASP.NET Web コントロールの使用方法に関する詳細な手順については、「 [Web サイトのセキュリティ](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)に関するチュートリアル」を参照してください。 ここでは、新しいアカウントを作成したり、ロールを作成および管理したり、ユーザーをロールに割り当てたり、その他の一般的な管理タスクを行うための web ページを構築する方法についても説明します。

運用 web サイトに WSAT のような機能を実装するには、WSAT の機能を実装する独自の一連の web ページをいつでも作成できます。 作業を開始するには、`%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`のフォルダーにある WSAT ソースコードを確認してください。 別の方法として、Dan Clem の WSAT 代替手段を使用することもできます。この方法では、[独自の Web サイト管理ツールをロール](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)します。 Dan は、WSAT のようなカスタムツールを構築するプロセスを通じて、アプリケーションのダウンロード用ソースコード (でC#は) をインクルードし、ホストされた web サイトにカスタム WSAT を追加するための詳細な手順を示します。

## <a name="summary"></a>まとめ

ASP.NET Web サイト管理ツール (WSAT) は、メンバーシップとロールアプリケーションサービスと共に使用して、web サイトのユーザーとロールの情報を管理できます。 残念ながら、WSAT はローカルでのみアクセスでき、運用 web サイトからはアクセスできません。 ただし、運用データベースを指すように開発環境の接続文字列を変更することにより、WSAT を使用して運用 web サイトのユーザーとロールを管理できます。

WSAT アプローチでは、ユーザーとロールをすばやく簡単に管理できますが、Visual Studio から WSAT を起動し、接続文字列情報を一時的に変更することが必要になります。 WSAT は、実稼働環境でユーザーとロールを簡単に管理する方法を提供しますが、煩雑で、Visual Studio や WSAT を持っていない、または使い慣れていない、複数の管理者や管理者がいる web サイトでは適切に機能しません。 このような理由から、ユーザーアカウントをサポートするほとんどの web サイトには、一連の管理 web ページが含まれています。 このような一連の web ページにより、WSAT が不要になり、どのコンピューターからでもさまざまな管理ユーザーが使用できるようになります。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP を調べています。NET のメンバーシップ、ロール、およびプロファイル](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [独自の Web サイト管理ツールをロールする](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [Web サイト管理ツールの概要](https://msdn.microsoft.com/library/yy40ytx0.aspx)
- [Web サイトのセキュリティに関するチュートリアル](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [前へ](precompiling-your-website-cs.md)
> [次へ](asp-net-hosting-options-vb.md)

---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET が IIS ディレクトリへのアクセスを拒否されました |Microsoft Docs
author: rick-anderson
description: このホワイトペーパーでは、ASP.NET アプリケーションに対する要求で "DirectoryName ディレクトリへのアクセスが拒否されました" というエラーが返された場合の対処方法について説明します。 失敗した...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: a3a53aa88abbe1bcaaea7d691406800c8f9b988b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518572"
---
# <a name="aspnet-denied-access-to-iis-directories"></a>ASP.NET の IIS ディレクトリのアクセス拒否

> このホワイトペーパーでは、ASP.NET アプリケーションに対する要求で " *DirectoryName*ディレクトリへのアクセスが拒否されました" というエラーが返された場合の対処方法について説明します。 ディレクトリの変更の監視を開始できませんでした。 "
> 
> ASP.NET 1.0 と ASP.NET 1.1 に適用されます。

ASP.NET V1 RTM は、ローカルコンピューターで "ASPNET" アカウントとして登録されている、より低い特権の windows アカウントを使用して実行されるようになりました。

一部のロックされたシステムでは、このアカウントは、既定では、web サイトのコンテンツディレクトリ、アプリケーションルートディレクトリ、または web サイトのルートディレクトリに対する読み取りセキュリティアクセス権を持っていない可能性があります。 この場合、特定の web アプリケーションからページを要求すると、次のエラーが表示されます。

![](denied-access-to-iis-directories/_static/image1.jpg)

この問題を解決するには、適切なディレクトリのセキュリティアクセス許可を変更する必要があります。

具体的には、ASP.NET は、web サイトのルート (たとえば、c:\inetpub\wwwroot や IIS で構成した別のサイトディレクトリ) の ASPNET アカウントの読み取り、実行、およびリストアクセスを必要とします。構成ファイルの変更を監視するために使用します。 アプリケーションルートは、IIS 管理ツール (inetmgr.exe) のアプリケーション仮想ディレクトリに関連付けられているフォルダーパスに対応します。

たとえば、wwwroot フォルダーの下にある次のアプリケーション階層を考えてみます。

`C:\inetpub\wwwroot\myapp\default.aspx`

この例では、ASPNET アカウントで、myapp ディレクトリと wwwroot ディレクトリの両方のコンテンツに対して、上記で定義した読み取りアクセス許可が必要です。 ルートフォルダーに継承された単一の ACL は、入れ子になっている場合に、両方のディレクトリに対して必要に応じて使用することもできます。

ディレクトリにアクセス許可を追加するには、次の手順を実行します。

- Windows エクスプローラーを使用して、ディレクトリに移動します。
- ディレクトリフォルダーを右クリックし、[プロパティ] を選択します。
- プロパティダイアログの [セキュリティ] タブに移動します。
- [追加] ボタンをクリックし、コンピューター名の後に ASPNET アカウント名を入力します。 たとえば、"webdev" という名前のコンピューターでは、「Webdev\ ASPNET」と入力し、[OK] をクリックします。
- ASPNET アカウントに [読み取り &amp; 実行]、[フォルダーの内容の一覧表示]、[読み取り] チェックボックスがオンになっていることを確認します。
- [OK] をクリックしてダイアログを閉じ、変更を保存します。

![](denied-access-to-iis-directories/_static/image2.jpg)

必要に応じて、これらの変更は、Windows に付属しているスクリプトまたは "cacls.exe" ツールを使用して自動化できます。 ASPNET アカウントの詳細については、 [FAQ ドキュメント](https://go.microsoft.com/fwlink/?LinkId=5828)を参照してください。

特定の web アプリケーションが特定のフォルダーまたはファイルに対する書き込みアクセス許可または変更アクセス許可を持っている場合は、同じ手順に従って、[書き込み] または [変更] チェックボックスをオンにすることで、この操作を許可できます。

すべてのユーザーまたはユーザーグループにこれらのディレクトリへの読み取りアクセスを許可するコンピューター (既定の構成) では、問題は発生せず、上記の手順は必要ありません。

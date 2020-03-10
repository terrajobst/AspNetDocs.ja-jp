---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: パスワードおよびその他の機密データを ASP.NET および Azure App Service に展開する-ASP.NET 4.x
author: Rick-Anderson
description: このチュートリアルでは、セキュリティで保護された情報をコードで安全に格納し、アクセスする方法について説明します。 最も重要な点は、パスワードやその他のものを保存しないことです。
ms.author: riande
ms.date: 05/21/2015
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 8356a90611f791779cc4ff4730038d82cd76242f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472144"
---
# <a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a>ASP.NET と Azure App Service にパスワードやその他の機密データを配置するためのベスト プラクティス

[Rick Anderson](https://twitter.com/RickAndMSFT)

> このチュートリアルでは、セキュリティで保護された情報をコードで安全に格納し、アクセスする方法について説明します。 最も重要な点は、パスワードやその他の機密データをソースコードに保存しないようにし、開発およびテストモードでは運用シークレットを使用しないことです。
> 
> このサンプルコードは、単純な Web ジョブコンソールアプリと、データベース接続文字列 password、Twilio、Google、および SendGrid のセキュリティで保護されたキーにアクセスする必要がある ASP.NET MVC アプリです。
> 
> オンプレミスの設定と PHP についても説明します。

- [開発環境でのパスワードの使用](#pwd)
- [開発環境での接続文字列の使用](#con)
- [Web ジョブコンソールアプリ](#wj)
- [Azure へのシークレットのデプロイ](#da)
- [オンプレミスと PHP の注意事項](#not)
- [その他のリソース](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a>開発環境でのパスワードの使用

チュートリアルでは、多くの場合、ソースコードに機密データが表示されます。機密データをソースコードに保存しないように注意する必要があります。 たとえば、my [ASP.NET MVC 5 app WITH SMS および email 2FA](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)チュートリアルでは、web.config ファイルで次のことを示して*い*ます。

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

Web.config*ファイルは*ソースコードであるため、これらのシークレットをそのファイルに格納することはできません。 幸いにも、`<appSettings>` 要素には、機密性の高いアプリ構成設定を含む外部ファイルを指定するための `file` 属性があります。 外部ファイルがソースツリーにチェックインされていない限り、すべてのシークレットを外部ファイルに移動できます。 たとえば、次のマークアップでは、 *Appsettingssecrets .config*ファイルにすべてのアプリシークレットが含まれています。

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

外部ファイルのマークアップ (このサンプルでは*Appsettingssecrets .config* ) は、 *web.config ファイルで*見つかったマークアップと同じです。

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

ASP.NET ランタイムは、外部ファイルの内容を &lt;appSettings&gt; 要素のマークアップとマージします。 指定したファイルが見つからない場合、このファイル属性は無視されます。

> [!WARNING]
> セキュリティ-*シークレットの .config*ファイルをプロジェクトに追加したり、ソース管理にチェックインしたりしないでください。 既定では、Visual Studio は `Build Action` を `Content`に設定します。これは、ファイルが配置されることを意味します。 詳細については[、「プロジェクトフォルダー内のすべてのファイルが配置されない理由](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment)」を参照してください。 *シークレットの .config*ファイルには任意の拡張機能を使用できますが、構成ファイルは IIS によって処理されないため、そのままにしておくことをお勧めし*ます*。 また、 *Appsettingssecrets .config*ファイル*は、web.config ファイルから*の2つのディレクトリレベルであるため、ソリューションディレクトリから完全に除外されます。 ソリューションディレクトリの外にファイルを移動することによって、&quot;git で \*を追加し &quot; によってリポジトリに追加されません。

<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a>開発環境での接続文字列の使用

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)を使用する新しい ASP.NET プロジェクトが Visual Studio によって作成されます。 LocalDB は、開発環境専用に作成されました。 パスワードは必要ありません。そのため、シークレットがソースコードにチェックインされないようにするために何もする必要はありません。 一部の開発チームでは、パスワードを必要とする SQL Server (またはその他の DBMS) の完全バージョンを使用しています。

`configSource` 属性を使用して、`<connectionStrings>` マークアップ全体を置き換えることができます。 マークアップをマージする `<appSettings>` `file` 属性とは異なり、`configSource` 属性によってマークアップが置換されます。 次のマークアップは、web.config ファイルの `configSource` 属性を示して*い*ます。

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> 上に示した `configSource` 属性を使用して接続文字列を外部ファイルに移動し、Visual Studio で新しい web サイトを作成する場合、データベースを使用していることを検出することはできません。また、Visual Studio から Azure に発行するときにデータベースを構成するオプションもありません。 `configSource` 属性を使用している場合は、PowerShell を使用して web サイトとデータベースを作成および配置できます。また、発行前にポータルで web サイトとデータベースを作成することもできます。 [New-AzureWebsitewithDB](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)スクリプトは、新しい web サイトとデータベースを作成します。

> [!WARNING]
> セキュリティ- *Appsettingssecrets .config*ファイルとは異なり、外部接続文字列ファイルはルートの*web.config*ファイルと同じディレクトリに存在する必要があるため、ソースリポジトリにチェックインしないようにするための予防措置を講じる必要があります。

> [!NOTE]
> **シークレットファイルのセキュリティ警告:** ベストプラクティスとして、テストと開発では運用シークレットを使用しないことをお勧めします。 テストまたは開発で実稼働パスワードを使用すると、これらの機密情報をリークします。

<a id="wj"></a>
## <a name="webjobs-console-apps"></a>Web ジョブコンソールアプリ

コンソールアプリで使用される*app.config*ファイルは相対パスをサポートしていませんが、絶対パスはサポートしています。 絶対パスを使用して、お使いのプロジェクトディレクトリからシークレットを移動できます。 次のマークアップは、 *C:\secrets\AppSettingsSecrets.config*ファイルのシークレットと、 *app.config*ファイル内の機微なデータを示しています。

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a>Azure へシークレットを展開

Web アプリを Azure にデプロイすると、 *Appsettingssecrets .config*ファイルはデプロイされません (これが必要です)。 [Azure 管理ポータル](https://azure.microsoft.com/services/management-portal/)にアクセスし、手動で設定して、次の操作を行うことができます。

1. [https://portal.azure.com](https://portal.azure.com)にアクセスし、Azure の資格情報でサインインします。
2. [**参照 &gt; Web Apps**] をクリックし、Web アプリの名前をクリックします。
3. **すべての設定 &gt; アプリケーション設定** をクリックします。

**アプリケーション設定**と**接続文字列**の値は、 *web.config ファイルの*同じ設定よりも優先されます。 この例では、これらの設定を Azure にデプロイしませんでしたが、これらのキーが web.config ファイルにある場合、ポータルに表示される設定が優先さ*れます。*

ベストプラクティスとして、 [DevOps ワークフロー](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md)に従って[Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (または[Chef](http://www.opscode.com/chef/)や[パペット](http://puppetlabs.com/puppet/what-is-puppet)などの他のフレームワーク) を使用して、Azure でこれらの値を自動的に設定することをお勧めします。 次の PowerShell スクリプトでは、 [export-clixml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk)を使用して暗号化されたシークレットをディスクにエクスポートします。

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

上記のスクリプトでは、' Name ' は、'&quot;FB\_AppSecret&quot; や "TwitterSecret" などの秘密キーの名前です。 スクリプトによって作成された ". credential" ファイルをブラウザーに表示できます。 次のスニペットは、各資格情報ファイルをテストし、名前付き web アプリのシークレットを設定します。

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> セキュリティ-PowerShell スクリプトにパスワードやその他のシークレットを含めないでください。これにより、PowerShell スクリプトを使用して機微なデータをデプロイする目的が損なわれます。 [Get Credential](https://technet.microsoft.com/library/hh849815.aspx)コマンドレットは、パスワードを取得するための安全なメカニズムを提供します。 UI プロンプトを使用すると、パスワードのリークを防ぐことができます。

### <a name="deploying-db-connection-strings"></a>DB 接続文字列の展開

DB 接続文字列は、アプリ設定と同様に処理されます。 Visual Studio から web アプリをデプロイすると、接続文字列が構成されます。 これは、ポータルで確認できます。 接続文字列の設定方法としては、PowerShell を使用することをお勧めします。 PowerShell スクリプトの例として、は web サイトとデータベースを作成し、web サイトの接続文字列を設定します。 [Azure スクリプトライブラリ](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)から[New-AzureWebsitewithDB](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)をダウンロードします。

<a id="not"></a>
## <a name="notes-for-php"></a>PHP における考慮事項

**アプリ設定**と**接続文字列**の両方のキーと値のペアは Azure App Service の環境変数に格納されるため、WEB アプリフレームワーク (PHP など) を使用する開発者は、これらの値を簡単に取得できます。 「Stefan の[Windows Azure websites: アプリケーション文字列と接続文字列の機能](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)」ブログ記事で、アプリ設定と接続文字列を読み取るための PHP スニペットを示します。

## <a name="notes-for-on-premises-servers"></a>オンプレミス サーバーにおける考慮事項

オンプレミスの web サーバーにデプロイする場合は、[構成ファイルの構成セクションを暗号化](https://msdn.microsoft.com/library/ff647398.aspx)することで、シークレットをセキュリティで保護することができます。 別の方法として、Azure Websites に推奨される同じアプローチを使用できます。構成ファイルで開発設定を保持し、運用設定に環境変数の値を使用します。 ただし、この場合は、Azure Websites で自動化されている機能のアプリケーションコードを作成する必要があります。環境変数から設定を取得し、構成ファイルの設定の代わりにこれらの値を使用するか、構成ファイルの設定を使用します。環境変数が見つかりません。

<a id="addRes"></a>
## <a name="additional-resources"></a>その他のリソース

Web アプリとデータベースを作成する PowerShell スクリプトの例については、接続文字列とアプリの設定を設定し、 [Azure スクリプトライブラリ](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)から[New-AzureWebsitewithDB](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)をダウンロードします。 

「Stefan の[Windows Azure websites: アプリケーション文字列と接続文字列](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)のしくみ」を参照してください。

Dorrans ( [@blowdart](https://twitter.com/blowdart) ) と Carlos Farre のレビューに感謝します。

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
# <a name="aspnet-denied-access-to-iis-directories"></a><span data-ttu-id="745e1-104">ASP.NET の IIS ディレクトリのアクセス拒否</span><span class="sxs-lookup"><span data-stu-id="745e1-104">ASP.NET Denied Access to IIS Directories</span></span>

> <span data-ttu-id="745e1-105">このホワイトペーパーでは、ASP.NET アプリケーションに対する要求で " *DirectoryName*ディレクトリへのアクセスが拒否されました" というエラーが返された場合の対処方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="745e1-105">This whitepaper describes what you must do if a request to your ASP.NET application returns the error, "Denied Access to *DirectoryName* directory.</span></span> <span data-ttu-id="745e1-106">ディレクトリの変更の監視を開始できませんでした。 "</span><span class="sxs-lookup"><span data-stu-id="745e1-106">Failed to start monitoring directory changes."</span></span>
> 
> <span data-ttu-id="745e1-107">ASP.NET 1.0 と ASP.NET 1.1 に適用されます。</span><span class="sxs-lookup"><span data-stu-id="745e1-107">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="745e1-108">ASP.NET V1 RTM は、ローカルコンピューターで "ASPNET" アカウントとして登録されている、より低い特権の windows アカウントを使用して実行されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="745e1-108">ASP.NET V1 RTM now runs using a less privileged windows account - registered as the "ASPNET" account on a local machine.</span></span>

<span data-ttu-id="745e1-109">一部のロックされたシステムでは、このアカウントは、既定では、web サイトのコンテンツディレクトリ、アプリケーションルートディレクトリ、または web サイトのルートディレクトリに対する読み取りセキュリティアクセス権を持っていない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="745e1-109">On some locked down systems, this account may not by default have read security access to a website's content directories, the application root directory, or the web site root directory.</span></span> <span data-ttu-id="745e1-110">この場合、特定の web アプリケーションからページを要求すると、次のエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="745e1-110">In this case you will receive the following error when requesting pages from a given web application:</span></span>

![](denied-access-to-iis-directories/_static/image1.jpg)

<span data-ttu-id="745e1-111">この問題を解決するには、適切なディレクトリのセキュリティアクセス許可を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="745e1-111">To fix this you will need to change the security permissions on the appropriate directories.</span></span>

<span data-ttu-id="745e1-112">具体的には、ASP.NET は、web サイトのルート (たとえば、c:\inetpub\wwwroot や IIS で構成した別のサイトディレクトリ) の ASPNET アカウントの読み取り、実行、およびリストアクセスを必要とします。構成ファイルの変更を監視するために使用します。</span><span class="sxs-lookup"><span data-stu-id="745e1-112">Specifically, ASP.NET requires read, execute, and list access for the ASPNET account for the web site root (for example: c:\inetpub\wwwroot or any alternative site directory you may have configured in IIS), the content directory and the application root directory in order to monitor for configuration file changes.</span></span> <span data-ttu-id="745e1-113">アプリケーションルートは、IIS 管理ツール (inetmgr.exe) のアプリケーション仮想ディレクトリに関連付けられているフォルダーパスに対応します。</span><span class="sxs-lookup"><span data-stu-id="745e1-113">The application root corresponds to the folder path associated with the application virtual directory in the IIS Administration tool (inetmgr).</span></span>

<span data-ttu-id="745e1-114">たとえば、wwwroot フォルダーの下にある次のアプリケーション階層を考えてみます。</span><span class="sxs-lookup"><span data-stu-id="745e1-114">For example, consider the following application hierarchy under the wwwroot folder.</span></span>

`C:\inetpub\wwwroot\myapp\default.aspx`

<span data-ttu-id="745e1-115">この例では、ASPNET アカウントで、myapp ディレクトリと wwwroot ディレクトリの両方のコンテンツに対して、上記で定義した読み取りアクセス許可が必要です。</span><span class="sxs-lookup"><span data-stu-id="745e1-115">For this example, the ASPNET account needs the read permissions defined above for content in both the myapp and the wwwroot directory.</span></span> <span data-ttu-id="745e1-116">ルートフォルダーに継承された単一の ACL は、入れ子になっている場合に、両方のディレクトリに対して必要に応じて使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="745e1-116">A single inherited ACL on the root folder can also be optionally used for both directories if they're nested.</span></span>

<span data-ttu-id="745e1-117">ディレクトリにアクセス許可を追加するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="745e1-117">To add permissions to a directory, perform the following steps:</span></span>

- <span data-ttu-id="745e1-118">Windows エクスプローラーを使用して、ディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="745e1-118">Using the Windows explorer, navigate to the directory</span></span>
- <span data-ttu-id="745e1-119">ディレクトリフォルダーを右クリックし、[プロパティ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="745e1-119">Right click on the directory folder and choose "Properties"</span></span>
- <span data-ttu-id="745e1-120">プロパティダイアログの [セキュリティ] タブに移動します。</span><span class="sxs-lookup"><span data-stu-id="745e1-120">Navigate to the "Security" tab on the property dialog</span></span>
- <span data-ttu-id="745e1-121">[追加] ボタンをクリックし、コンピューター名の後に ASPNET アカウント名を入力します。</span><span class="sxs-lookup"><span data-stu-id="745e1-121">Click the "Add" button and enter the machine name followed by the ASPNET account name.</span></span> <span data-ttu-id="745e1-122">たとえば、"webdev" という名前のコンピューターでは、「Webdev\ ASPNET」と入力し、[OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="745e1-122">For example, on a machine named "webdev", you would enter webdev\ASPNET and hit "OK".</span></span>
- <span data-ttu-id="745e1-123">ASPNET アカウントに [読み取り &amp; 実行]、[フォルダーの内容の一覧表示]、[読み取り] チェックボックスがオンになっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="745e1-123">Ensure that the ASPNET account has the "Read &amp; Execute", "List Folder Contents", and "Read" checkboxes checked.</span></span>
- <span data-ttu-id="745e1-124">[OK] をクリックしてダイアログを閉じ、変更を保存します。</span><span class="sxs-lookup"><span data-stu-id="745e1-124">Hit OK to dismiss the dialog and save the changes.</span></span>

![](denied-access-to-iis-directories/_static/image2.jpg)

<span data-ttu-id="745e1-125">必要に応じて、これらの変更は、Windows に付属しているスクリプトまたは "cacls.exe" ツールを使用して自動化できます。</span><span class="sxs-lookup"><span data-stu-id="745e1-125">If desired, these changes can be automated using scripts or the "cacls.exe" tool that ships with Windows.</span></span> <span data-ttu-id="745e1-126">ASPNET アカウントの詳細については、 [FAQ ドキュメント](https://go.microsoft.com/fwlink/?LinkId=5828)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="745e1-126">For more information on the ASPNET account, please see the [FAQ document](https://go.microsoft.com/fwlink/?LinkId=5828).</span></span>

<span data-ttu-id="745e1-127">特定の web アプリケーションが特定のフォルダーまたはファイルに対する書き込みアクセス許可または変更アクセス許可を持っている場合は、同じ手順に従って、[書き込み] または [変更] チェックボックスをオンにすることで、この操作を許可できます。</span><span class="sxs-lookup"><span data-stu-id="745e1-127">If a given web application relies on having write or modify permissions to a particular folder or file, this can be granted by following the same procedure and checking the "Write" and/or "Modify" checkboxes.</span></span>

<span data-ttu-id="745e1-128">すべてのユーザーまたはユーザーグループにこれらのディレクトリへの読み取りアクセスを許可するコンピューター (既定の構成) では、問題は発生せず、上記の手順は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="745e1-128">On machines that allow Everyone or the Users group read access to these directories (which is the default configuration), no issues will be encountered and the above steps will not be required.</span></span>

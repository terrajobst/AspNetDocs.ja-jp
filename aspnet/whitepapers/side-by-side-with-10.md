---
uid: whitepapers/side-by-side-with-10
title: ASP.NET .NET Framework 1.0 と 1.1 | のサイドバイサイド実行Microsoft Docs
author: rick-anderson
description: このホワイトペーパーでは、.NET 1.0 と .NET 1.1 の両方をコンピューターにインストールする方法について説明します。これにより、ASP.NET Web アプリケーションをいずれかのバージョンの fram で実行できるようになります。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513832"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a>ASP.NET で .NET Framework 1.0 と 1.1 を並行して実行する

> このホワイトペーパーでは、.NET 1.0 と .NET 1.1 の両方をコンピューターにインストールする方法について説明します。これにより、ASP.NET Web アプリケーションをいずれかのバージョンのフレームワークで実行できるようになります。
> 
> ASP.NET 1.0 と ASP.NET 1.1 に適用されます。

ASP.NET では、アプリケーションは同じコンピューターにインストールされているときにサイドバイサイドで実行されますが、異なるバージョンの .NET Framework を使用します。 次のトピックでは、ASP.NET アプリケーションを side-by-side 実行用に構成する方法について説明し、詳細な手順を示します。

- [インストール中に .NET Framework バージョン1.0 への Web アプリケーションのマッピングを維持する](#1)
- [Web アプリケーションを特定のバージョンの .NET Framework にマップする](#2)
- [Web サイトが使用している .NET Framework のバージョンを確認する](#3)

従来、コンピューターでコンポーネントまたはアプリケーションが更新されると、古いバージョンが削除され、新しいバージョンに置き換えられます。 新しいバージョンが以前のバージョンと互換性がない場合は、通常、コンポーネントまたはアプリケーションを使用する他のアプリケーションが中断されます。 .NET Framework は、side-by-side 実行のサポートを提供します。これにより、複数のバージョンのアセンブリまたはアプリケーションを同じコンピューターに同時にインストールできます。 複数のバージョンを同時にインストールできるため、マネージアプリケーションでは、別のバージョンを使用するアプリケーションに影響を与えずに、使用するバージョンを選択できます。

既定では .NET Framework バージョン1.1 のインストール時に、.NET Framework の最新バージョンを使用するように既存のすべての ASP.NET アプリケーションが自動的に再構成されます。 ASP.NET アプリケーションで既定 .NET Framework 1.1 に設定しない場合は、[ここ](#1)をクリックして、インストール中にこれを回避する方法を確認してください。

Web サーバーを .NET Framework 1.1 に更新し、1つまたは複数の Web アプリケーションで .NET Framework 1.0 を実行する場合は、インターネットインフォメーションサービス (IIS) スクリプトマップを更新する必要があります。 スクリプトマッピングは、特定の Web アプリケーションの .aspx ファイル拡張子を .NET Framework のバージョンにマップするメカニズムです。 [ここ](#2)をクリックして、Web アプリケーションを特定のバージョンの .NET Framework にマップする方法を確認してください。

インターネットインフォメーションマネージャーまたは ASP.NET IIS 登録ツール (Aspnet\_iis 登録ツール) を使用して、特定の Web アプリケーションを実行している .NET Framework バージョンを見つけることができます。 Web サイトが使用している .NET Framework のバージョンを確認するには、[ここ](#3)をクリックしてください。

.NET Framework 1.1 に移行する際の1つのインポートの考慮事項は、.NET Framework の各バージョンが独自の machine.config ファイルを使用することです。 このため、Web 管理者が machine.config ファイルに変更を加えた場合は、それらの変更を .NET Framework 1.1 の machine.config ファイルに移行する必要があります。

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a>インストール中に .NET Framework 1.0 への Web アプリケーションのマッピングを維持する

既定では、既存のすべての ASP.NET アプリケーションは、新しいバージョンの .NET Framework を使用するために、インストール時に自動的に再構成されます。 新しいバージョンの .NET Framework を使用すると、アプリケーションは、新しいリリースに含まれる機能強化や新機能を最大限に活用できます。 同時に、更新するアプリケーションをきめ細かく制御する必要がある Web 管理者は、.NET Framework のインストール中に、既存のすべての ASP.NET アプリケーションの自動再マップを防ぐことができます。

ASP.NET アプリケーション全体を新しいバージョンの .NET Framework に自動的に再マップしないようにするために、Web 管理者は Dotnetfx.exe セットアッププログラムと共に/noaspupgrade コマンドラインオプションを使用できます。

**ASP.NET アプリケーションの新しいバージョンへの再マップの合計を回避するには**

1. **[スタート]** に移動します。
2. **[実行]** をクリックします。
3. 「**cmd**」と入力します。
4. **[OK]** をクリックします。  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. コマンドプロンプトで、次の行を入力して .NET Framework のインストールを開始します: **dotnetfx.exe/c: "install/noaspupgrade?** .  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. Microsoft .NET Framework 1.1 セットアップで [**はい]** をクリックします。 .NET Framework 1.1 のセットアッププロセスが開始されます。  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a>Web アプリケーションを特定のバージョンの .NET Framework にマップする

.NET Framework の各バージョンには、ASP.NET IIS Registration Tool (Aspnet\_iis 登録ツール) のバージョンが含まれています。 このツールを使用すると、管理者は、.NET Framework の特定のバージョンで Web アプリケーションを実行するように指定できます。 これは、Web アプリケーションを .NET Framework のバージョンにマッピングすることと呼ばれます。 管理者は、Web アプリケーションに関連付けられる .NET Framework のバージョンに対応する Aspnet\_iis 登録ツールを選択する必要があります。 たとえば、Web サイトで .NET Framework 1.1 を使用することを指定する管理者は、.NET Framework 1.1 に付属する Aspnet\_iis 登録ツールを使用する必要があります。

バージョン1.0 の Aspnet\_iis 登録ツールは次の場所にあります。

- C:\windows\ microsoft.net \framework\\**v v1.0.3705**iis 登録ツール\_

Aspnet\_iis 登録ツールのバージョン1、1は次の場所にあります。

- C:\windows\ microsoft.net \framework\\**v 1.1.4322**iis 登録ツール\_

Aspnet\_iis 登録ツールには、Web アプリケーションをマッピングするスクリプトの2つのオプションがあります。

- **-s**は、パスとその子ディレクトリ内のスクリプトマップを設定します。
- **-sn**パス内のスクリプトマップのみを設定します。

パスは、Web アプリケーションの IIS メタデータパスを定義します。これは、W3SVC/ROOT/{WebSiteNumber}/{Application\_Name} の形式で定義されています。 たとえば、既定の Web サイトの下にあるポータルと呼ばれる Web アプリケーションの場合、メタベースのパスは W3SVC/1/ROOT/Portal です。

![](side-by-side-with-10/_static/image4.gif)

また、メタベースエディターというツールを使用して、メタベースパスを取得することもできます。 このツールは、Microsoft サポートサイトの[https://support.microsoft.com/default.aspx?scid=kb; en-us; 232068](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)からダウンロードできます。

- Aspnet\_iis 登録ツール-s W3SVC/1/ROOT/Portal を実行して、ポータルの IIS スクリプトマップとそのサブアプリケーションを更新します。  
  
    ![](side-by-side-with-10/_static/image5.gif)

- Aspnet\_iis 登録ツール-sn W3SVC/1/ROOT/Portal を実行して、ポータルのサブディレクトリ内のアプリケーションに影響を与えずに、ポータルの IIS スクリプトマップを更新します。  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a>Web アプリケーションで使用している .NET Framework のバージョンを確認する

管理者は、インターネット Service Manager を使用して、Web サイトを実行している .NET Framework のバージョンを見つけることができます。 オペレーティングシステムのバージョンが異なると、インターネット Service Manager が異なる方法で起動します。 Service manager を起動するには、次の手順に従います。

**インターネット Service Manager を開始するには**

1. **[スタート]** に移動します。
2. **[実行]** をクリックします。
3. 「 **Inetmgr.exe**」と入力します。  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. インターネット Service Manager から、確認する .NET Framework のバージョンを持つ Web アプリケーションを選択します。  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. Web アプリケーションを右クリックし、[プロパティ] をクリックし**ます。**  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. [プロパティ] ウィンドウで、[構成] を選択し**ます。**  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. アプリケーションマッピングテーブルから **.aspx**を選択し、 **[編集]** をクリックします。  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. **[実行可能ファイル]** テキストボックスで、スクロールしてバージョンディレクトリを確認します。 バージョンディレクトリが1.1.4322 の場合、アプリケーションは .NET Framework 1.1 にマップされます。 反対に、バージョンディレクトリが v v1.0.3705 の場合、アプリケーションは .NET Framework 1.0 にマップされます。  
  
    ![](side-by-side-with-10/_static/image12.gif)

---
uid: whitepapers/aspnet-and-iis6
title: IIS 6.0 で ASP.NET 1.1 を実行する |Microsoft Docs
author: rick-anderson
description: Windows Server 2003 には IIS 6.0 と ASP.NET 1.1 の両方が含まれていますが、これらのコンポーネントは既定で無効になっています。 このホワイトペーパーでは、IIS 6.0 を有効にする方法について説明します。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78419848"
---
# <a name="running-aspnet-11-with-iis-60"></a>IIS 6.0 で ASP.NET 1.1 を実行する

> Windows Server 2003 には IIS 6.0 と ASP.NET 1.1 の両方が含まれていますが、これらのコンポーネントは既定で無効になっています。 このホワイトペーパーでは、IIS 6.0 と ASP.NET 1.1 を有効にする方法について説明します。また、IIS と ASP.NET から最適なパフォーマンスを得るために、いくつかの構成設定を推奨しています。
> 
> ASP.NET 1.1 および IIS 6.0 に適用されます。

ASP.NET 1.1 は、Windows Server 2003 に付属しています。これには、インターネットインフォメーションサーバー (IIS) バージョン6.0 の最新バージョンも含まれています。 IIS 6.0 と ASP.NET 1.1 はシームレスに統合するように設計されており、ASP.NET は既定で新しい IIS 6.0 ワーカープロセスモデルに設定されています。

## <a name="aspnet-11-is-not-installed-by-default"></a>ASP.NET 1.1 は既定ではインストールされません

Microsoft のサーバーオペレーティングシステムの以前のバージョンとは異なり、インターネットインフォメーションサーバー (IIS) は既定では有効になっていません。とは ASP.NET 1.1 です。 IIS を有効にするには、次の2つのオプションがあります。

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a>IIS を有効にする、オプション #1-サーバーの構成ウィザード

Windows Server 2003 は、必要なモードでサーバーを適切に構成するために、新しい "サーバーの構成ウィザード" を提供します。

ウィザードを開始するには、ウィザードを実行するには、管理者としてログインする必要があります。開始 |プログラム |[管理ツール] を選択し、[サーバーの構成] を選択します。

選択すると、[サーバーの構成ウィザード] の開始画面が表示されます。

![](aspnet-and-iis6/_static/image1.jpg)

[次の &gt;] をクリックします。

![](aspnet-and-iis6/_static/image2.jpg)

[次の &gt;] をクリック

![](aspnet-and-iis6/_static/image3.jpg)

この画面では、[アプリケーションサーバー (IIS、ASP.NET)] を構成するオプションとして選択する必要があります。

[次の &gt;] をクリックします。

![](aspnet-and-iis6/_static/image4.jpg)

サーバーをアプリケーションサーバーとして構成するように選択すると、この画面が表示され、追加の機能をインストールするように求められます。 既定では、どちらのオプションも選択されていません。 ASP.NET を自動的に有効にするには、[ASP を有効にする] を選択する必要があります。NET '。

[次の &gt;] をクリックします。

![](aspnet-and-iis6/_static/image5.jpg)

この画面には、インストールするオプションが表示されます。

[次の &gt;] をクリックします。

![](aspnet-and-iis6/_static/image6.jpg)

この画面は、選択したオプションがインストールされている間に表示されます。 サービスのインストール中に他のダイアログボックスが表示されることは通常ありません。 また、Windows 2003 Server のインストール CD の場所を入力するように求められる場合もあります。

完了したら [次の &gt;] をクリックします。

![](aspnet-and-iis6/_static/image7.jpg)

[完了] をクリックします。 Windows Server 2003 は、IIS 6.0 と ASP.NET 1.1 をサポートするように構成されています。

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a>IIS を有効にする、オプション #2-IIS と ASP.NET を手動で構成する

[サーバーの構成ウィザード] を使用しない場合は、必要に応じて、コントロールパネルの [プログラムの追加と削除] を使用して IIS 6.0 および ASP.NET 1.1 をインストールします。

まず、コントロールパネルを開きます。

![](aspnet-and-iis6/_static/image8.jpg)

次に、[windows コンポーネントの追加と削除] をクリックして、[Windows コンポーネントウィザード] を開きます。

![](aspnet-and-iis6/_static/image9.jpg)

[アプリケーションサーバー] を選択してオンにし、[詳細] をクリックします。 ;

![](aspnet-and-iis6/_static/image10.jpg)

ASP.NET をインストールするには、[ASP] をオンにします。NET '。

[OK] をクリックして、Windows コンポーネントウィザードに戻ります。 Windows コンポーネントウィザードの [次の &gt;] をクリックして、のインストールを開始します。

![](aspnet-and-iis6/_static/image11.jpg)

サービスのインストール中に他のダイアログボックスが表示されることは通常ありません。 また、Windows 2003 Server のインストール CD の場所を入力するように求められる場合もあります。

インストールが完了すると、Windows コンポーネントウィザードの最後の画面が表示されます。

![](aspnet-and-iis6/_static/image12.jpg)

IIS 6.0 と ASP.NET 1.1 が構成され、使用できるようになりました。

## <a name="recommended-settings"></a>推奨される設定

IIS 6.0 で ASP.NET 1.1 を実行する場合、ASP.NET から最適なパフォーマンスを得るために推奨される構成設定がいくつかあります。

- ワーカープロセスのメモリ制限の構成
- ワーカープロセスのリサイクルの構成

### <a name="configuring-worker-process-memory-limits"></a>ワーカープロセスのメモリ制限の構成

既定では、iis 6.0 では、IIS で使用できるメモリの量に制限は設定されません。 ASP.NET のキャッシュ機能はメモリの制限に依存しているため、キャッシュはメモリから未使用の項目を事前に削除できます。

IIS 6.0 のメモリリサイクル機能を構成することをお勧めします。 これを構成するにはインターネットインフォメーションサービスマネージャーを開きます (Start |プログラム |管理ツール |インターネットインフォメーションサービス)。 開いたら、[アプリケーションプール] フォルダーを展開します。

各アプリケーションプールについて、次のことを行います。

![](aspnet-and-iis6/_static/image13.jpg)

1. アプリケーションプール (' DefaultAppPool ' など) を右クリックし、[プロパティ] を選択します。

![](aspnet-and-iis6/_static/image14.jpg)

2. 次に、[最大使用メモリ (mb 単位)] をクリックして、メモリのリサイクルを有効にします。 値は、サーバー上の物理メモリ (仮想メモリではない) の容量を超えないようにする必要があります。つまり、物理メモリの60% です。つまり、512 MB の物理メモリがあるサーバーでは、310を選択します。 また、2 GB のアドレス空間を使用する場合は、最大800MB を超えないようにすることをお勧めします。 サーバーのメモリアドレス空間が 3 GB の場合、ワーカープロセスの最大メモリ制限は、1, 800MB のようになります。

![](aspnet-and-iis6/_static/image15.jpg)

[適用] をクリックし、[OK] をクリックして、[プロパティ] ダイアログボックスを閉じます。 使用可能なすべてのアプリケーションプールに対してこの手順を繰り返します。

### <a name="configuring-worker-recycling"></a>ワーカーのリサイクルの構成

既定では、IIS 6.0 は、29時間ごとにワーカープロセスをリサイクルするように構成されています。 これは ASP.NET を実行しているアプリケーションに対しては少し積極的であり、ワーカープロセスの自動リサイクルは無効にすることをお勧めします。

ワーカープロセスの自動リサイクルを無効にするには、最初にインターネットインフォメーションサービスマネージャーを開きます (Start |プログラム |管理ツール |インターネットインフォメーションサービス)。 開いたら、[アプリケーションプール] フォルダーを展開します。

![](aspnet-and-iis6/_static/image16.jpg)

各アプリケーションプールについて、次のことを行います。

1. アプリケーションプール (' DefaultAppPool ' など) を右クリックし、[プロパティ] を選択します。

![](aspnet-and-iis6/_static/image17.jpg)

2. [ワーカープロセスのリサイクル (分単位)] をオフにします:

![](aspnet-and-iis6/_static/image18.jpg)

[適用] をクリックし、[OK] をクリックして、[プロパティ] ダイアログボックスを閉じます。 使用可能なすべてのアプリケーションプールに対してこの手順を繰り返します。

## <a name="granting-write-access-to-the-file-system"></a>ファイルシステムへの書き込みアクセス権の付与

アプリケーションがファイルシステムへの書き込みアクセスを必要とし、NTFS を使用している場合は、ASP.NET アクセスを許可するフォルダーまたはファイルの Access Control リスト (ACL) を変更する必要があります。

たとえば、c:\inetpub\wwwroot 最初に開いているエクスプローラーに ASP.NET 書き込みアクセス権を付与するには、次のディレクトリに移動します。

![](aspnet-and-iis6/_static/image19.jpg)

次に、ディレクトリ ("wwwroot" など) を右クリックし、[プロパティ] を選択します。 [プロパティ] ダイアログが開いたら、[セキュリティ] タブを選択します。

![](aspnet-and-iis6/_static/image20.jpg)

C:\inetpub\wwwroot\ ディレクトリは、特別な IIS 6.0 グループ ' IIS\_WPG ' に既に読み取り &amp; 実行、フォルダーの内容の一覧表示、および読み取りアクセス許可が既に付与されているディレクトリです。 ただし、書き込みアクセス許可を付与するには、[書き込み] の [許可] チェックボックスをオンにする必要があります。

![](aspnet-and-iis6/_static/image21.jpg)

IIS 6.0 は、このフォルダーに対する書き込みアクセス許可を持つようになりました。 他のフォルダーに対する書き込みアクセス許可を付与するには、次の手順に従います。既に存在していない場合は、IIS\_WPG グループを追加する必要があることに注意してください。

> [!CAUTION]
> IIS\_WPG に書き込みアクセス許可を付与すると、すべての ASP.NET アプリケーションがこのディレクトリに書き込むことができます。

## <a name="supporting-integrated-authentication-with-sql-server"></a>SQL Server による統合認証のサポート

統合認証を使用すると、SQL Server は Windows NT 認証を利用して SQL Server ログオンアカウントを検証できます。 これにより、ユーザーは標準の SQL Server ログオンプロセスをバイパスできます。 この方法では、ネットワークユーザーは、Windows NT ネットワークセキュリティプロセスからユーザーとパスワードの情報を取得 SQL Server ため、個別のログオン id またはパスワードを指定しなくても、SQL Server データベースにアクセスできます。

アプリケーションの接続文字列内に資格情報が格納されることはないため、ASP.NET アプリケーションに対して統合認証を選択することをお勧めします。 代わりに、SQL への接続に使用される接続文字列は次のようになります。

`"server=localhost; database=Northwind;Trusted_Connection=true"`

この接続文字列は、SQL Server にアクセスしようとしているアプリケーションの Windows 資格情報を使用するように SQL Server に指示します。 ASP.NET/IIS 6 の場合、これは IIS\_WPG グループのアカウントになります。

SQL Server と ASP.NET 間の統合認証を有効にするには、まず、SQL Server が統合認証または混合モード認証用に構成されていることを確認する必要があります。このことを判断するには、DBA に確認してください。 これら2つのモードのいずれかを使用して SQL Server 場合は、統合認証を使用できます。

SQL Server Enterprise マネージャーを開きます (Start |プログラム |Microsoft SQL Server |Enterprise Manager) で、適切なサーバーを選択し、[セキュリティ] フォルダーを展開します。

![](aspnet-and-iis6/_static/image22.jpg)

' BUILTINT\IIS\_WPG ' グループが表示されていない場合は、[ログイン] を右クリックし、[新しい Login '] を選択します。

![](aspnet-and-iis6/_static/image23.jpg)

' Name: ' テキストボックスで、「[Server/Domain Name] \ IIS\_WPG」と入力するか、省略記号ボタンをクリックして Windows NT ユーザー/グループピッカーを開きます。

![](aspnet-and-iis6/_static/image24.jpg)

現在のコンピューターの IIS\_WPG グループを選択して [追加] をクリックし、[OK] をクリックしてピッカーを閉じます。

次に、既定のデータベースと、データベースにアクセスするための権限も設定する必要があります。 既定のデータベースを設定するには、ドロップダウンリストから次のように選択します。たとえば、Northwind が選択されています。

![](aspnet-and-iis6/_static/image25.jpg)

次に、[データベースアクセス] タブをクリックします。

![](aspnet-and-iis6/_static/image26.jpg)

アクセスを許可するすべてのデータベースについて、[許可] チェックボックスをオンにします。 また、データベースロールを選択する必要があります。 db\_所有者を確認すると、選択したデータベースを管理および使用するために必要なすべての権限がログインに与えられます。

[OK] をクリックして、プロパティダイアログを閉じます。 ASP.NET アプリケーションは、統合 SQL Server 認証をサポートするように構成されました。

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a>IIS 6.0 ネイティブモードで ASP.NET 1.0 を実行しない

Iis 6.0 の ASP.NET 1.0 は、IIS 5 互換モードでのみサポートされています。

ASP.NET 1.0 を IIS 5.0 互換モードで実行するように構成するにはインターネットサービスマネージャーを開き、[Web サイト] を右クリックし、[プロパティ] を選択します。

![](aspnet-and-iis6/_static/image27.jpg)

[サービス] タブに切り替えて、確認します。IIS 5.0 分離モードで WWW サービスを実行します。

![](aspnet-and-iis6/_static/image28.jpg)

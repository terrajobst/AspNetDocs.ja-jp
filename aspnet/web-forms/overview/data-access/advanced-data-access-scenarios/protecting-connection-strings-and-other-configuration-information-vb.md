---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-vb
title: 接続文字列とその他の構成情報を保護する (VB) |Microsoft Docs
author: rick-anderson
description: ASP.NET アプリケーションは、通常、構成情報を web.config ファイルに格納します。 この情報の一部は機密情報であり、保護を保証します。 Def...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: cd17dbe1-c5e1-4be8-ad3d-57233d52cef1
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-vb
msc.type: authoredcontent
ms.openlocfilehash: 070e1dccb80ef9af21ea621357c5b23e2ada6f9f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421000"
---
# <a name="protecting-connection-strings-and-other-configuration-information-vb"></a>接続文字列とその他の構成情報を保護する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_73_VB.zip)または[PDF のダウンロード](protecting-connection-strings-and-other-configuration-information-vb/_static/datatutorial73vb1.pdf)

> ASP.NET アプリケーションは、通常、構成情報を web.config ファイルに格納します。 この情報の一部は機密情報であり、保護を保証します。 既定では、このファイルは Web サイトの訪問者には提供されませんが、管理者またはハッカーが Web サーバーのファイルシステムにアクセスして、ファイルの内容を表示する場合があります。 このチュートリアルでは、ASP.NET 2.0 を使用して、web.config ファイルのセクションを暗号化することで機密情報を保護できることについて説明します。

## <a name="introduction"></a>はじめに

ASP.NET アプリケーションの構成情報は、通常、`Web.config`という名前の XML ファイルに格納されます。 これらのチュートリアルでは、`Web.config` をいくつかの方法で更新しました。 たとえば、[最初のチュートリアル](../introduction/creating-a-data-access-layer-vb.md)で `Northwind` 型指定されたデータセットを作成する場合、接続文字列情報は `<connectionStrings>` セクションの `Web.config` に自動的に追加されます。 後で、[マスターページとサイトナビゲーション](../introduction/master-pages-and-site-navigation-vb.md)チュートリアルで `Web.config`手動で更新し、プロジェクトのすべての ASP.NET ページで `DataWebControls` テーマを使用する必要があることを示す `<pages>` 要素を追加しました。

`Web.config` には接続文字列などの機密データが含まれている場合があるため、`Web.config` の内容は、承認されていないユーザーに対して安全かつ非表示にしておくことが重要です。 既定では、`.config` 拡張子を持つファイルに対する HTTP 要求は、ASP.NET エンジンによって処理されます。このエンジンは、図1に示すように、*この種類のページが提供*されていないメッセージを返します。 これは、ブラウザーのアドレスバーに http://www.YourServer.com/Web.config を入力するだけで、`Web.config` ファイルの内容を閲覧できないことを意味します。

[ブラウザーを使用して web.config にアクセス ![と、この種類のページはメッセージを表示しません](protecting-connection-strings-and-other-configuration-information-vb/_static/image2.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image1.png)

**図 1**: ブラウザーを介して `Web.config` にアクセスすると、この種類のページはメッセージを表示しません ([クリックすると、フルサイズの画像が表示](protecting-connection-strings-and-other-configuration-information-vb/_static/image3.png)されます)

しかし、攻撃者が `Web.config` ファイルの内容を見ることができる他の悪用を見つけることができる場合はどうでしょうか。 攻撃者がこの情報を使用すると、`Web.config`内の機密情報をさらに保護するための手順を実行できます。 幸い、`Web.config` のほとんどのセクションには機密情報が含まれていません。 ASP.NET ページで使用されている既定のテーマの名前がわかっていれば、攻撃者がどのような問題を perpetrate ことがありますか。

ただし、特定の `Web.config` セクションには、接続文字列、ユーザー名、パスワード、サーバー名、暗号化キーなどの機密情報が含まれています。 この情報は、通常、次の `Web.config` のセクションにあります。

- `<appSettings>`
- `<connectionStrings>`
- `<identity>`
- `<sessionState>`

このチュートリアルでは、このような機密構成情報を保護する手法について説明します。 ここで説明するように、.NET Framework バージョン2.0 には、選択した構成セクションを簡単に暗号化および復号化する保護された構成システムが含まれています。

> [!NOTE]
> このチュートリアルでは、ASP.NET アプリケーションからデータベースに接続するための Microsoft の推奨事項について説明します。 接続文字列を暗号化するだけでなく、セキュリティで保護された方法でデータベースに接続することで、システムを強化することができます。

## <a name="step-1-exploring-aspnet-20-s-protected-configuration-options"></a>手順 1: ASP.NET 2.0 s で保護されている構成オプションを探索する

ASP.NET 2.0 には、構成情報の暗号化と復号化を行うための保護された構成システムが含まれています。 これには、構成情報をプログラムで暗号化または復号化するために使用できる .NET Framework のメソッドが含まれます。 保護された構成システムでは、[プロバイダーモデル](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)を使用します。これにより、開発者は、使用する暗号化実装を選択できます。

.NET Framework には、次の2つの保護された構成プロバイダーが付属しています。

- [`RSAProtectedConfigurationProvider`](https://msdn.microsoft.com/library/system.configuration.rsaprotectedconfigurationprovider.aspx) -暗号化と復号化に非対称[RSA アルゴリズム](http://en.wikipedia.org/wiki/Rsa)を使用します。
- [`DPAPIProtectedConfigurationProvider`](https://msdn.microsoft.com/system.configuration.dpapiprotectedconfigurationprovider.aspx) -Windows[データ保護 API (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx)を使用して暗号化と復号化を行います。

保護された構成システムはプロバイダーの設計パターンを実装するため、独自の保護された構成プロバイダーを作成してアプリケーションに組み込むことができます。 このプロセスの詳細について[は、「保護された構成プロバイダーの実装](https://msdn.microsoft.com/library/wfc2t3az(VS.80).aspx)」を参照してください。

RSA プロバイダーと DPAPI プロバイダーは、暗号化と復号化のルーチンにキーを使用します。これらのキーは、コンピューターレベルまたはユーザーレベルで格納できます。 コンピューターレベルのキーは、web アプリケーションが独自の専用サーバーで実行される場合や、暗号化された情報を共有する必要があるサーバー上に複数のアプリケーションが存在する場合に最適です。 共有ホスティング環境では、ユーザーレベルのキーはより安全なオプションです。同じサーバー上の他のアプリケーションが、アプリケーションの保護された構成セクションの暗号化を解除できないようにする必要があります。

このチュートリアルでは、DPAPI プロバイダーとコンピューターレベルのキーを使用します。 具体的には、`Web.config`の `<connectionStrings>` セクションの暗号化について説明します。ただし、保護された構成システムを使用して、ほとんどの `Web.config` セクションを暗号化できます。 ユーザーレベルのキーを使用する方法、または RSA プロバイダーを使用する方法については、このチュートリアルの最後にある「参考資料」セクションのリソースを参照してください。

> [!NOTE]
> `RSAProtectedConfigurationProvider` プロバイダーと `DPAPIProtectedConfigurationProvider` プロバイダーは、それぞれ `RsaProtectedConfigurationProvider` および `DataProtectionConfigurationProvider`のプロバイダー名を使用して `machine.config` ファイルに登録されます。 構成情報を暗号化または復号化する場合は、実際の型名 (`RSAProtectedConfigurationProvider` および `DPAPIProtectedConfigurationProvider`) ではなく、適切なプロバイダー名 (`RsaProtectedConfigurationProvider` または `DataProtectionConfigurationProvider`) を指定する必要があります。 `$WINDOWS$\Microsoft.NET\Framework\version\CONFIG` フォルダーに `machine.config` ファイルがあります。

## <a name="step-2-programmatically-encrypting-and-decrypting-configuration-sections"></a>手順 2: プログラムによる構成セクションの暗号化と復号化

数行のコードを使用して、指定されたプロバイダーを使用して特定の構成セクションを暗号化または復号化することができます。 このコードは、後で説明するように、プログラムによって適切な構成セクションを参照し、`ProtectSection` または `UnprotectSection` メソッドを呼び出してから、`Save` メソッドを呼び出して変更を保持する必要があります。 さらに、.NET Framework には、構成情報の暗号化と復号化を行うための便利なコマンドラインユーティリティが含まれています。 このコマンドラインユーティリティについては、手順 3. で説明します。

プログラムによって構成情報を保護する方法を説明するために、「`Web.config`の `<connectionStrings>` セクションの暗号化と復号化を行うためのボタンを含む ASP.NET ページを作成します。

まず、`AdvancedDAL` フォルダーの [`EncryptingConfigSections.aspx`] ページを開きます。 TextBox コントロールをツールボックスからデザイナーにドラッグし、その `ID` プロパティを `WebConfigContents`に、その `TextMode` プロパティを `MultiLine`に、`Width` プロパティと `Rows` プロパティをそれぞれ95% および15に設定します。 このテキストボックスコントロールには `Web.config` の内容が表示され、コンテンツが暗号化されているかどうかをすばやく確認できます。 もちろん、実際のアプリケーションでは、`Web.config`の内容を表示しないようにする必要があります。

テキストボックスの下に、`EncryptConnStrings` と `DecryptConnStrings`という名前の2つのボタンコントロールを追加します。 接続文字列を暗号化し、接続文字列の暗号化を解除するように Text プロパティを設定します。

この時点で、画面は図2のようになります。

[テキストボックスと2つのボタン Web コントロールをページに追加 ![には](protecting-connection-strings-and-other-configuration-information-vb/_static/image5.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image4.png)

**図 2**: テキストボックスと2つのボタン Web コントロールをページに追加する ([クリックすると、フルサイズの画像が表示](protecting-connection-strings-and-other-configuration-information-vb/_static/image6.png)されます)

次に、ページが最初に読み込まれたときに `WebConfigContents` テキストボックスに `Web.config` の内容を読み込んで表示するコードを記述する必要があります。 ページ s 分離コードクラスに次のコードを追加します。 このコードは `DisplayWebConfig` という名前のメソッドを追加し、`Page.IsPostBack` が `False`されたときに `Page_Load` イベントハンドラーから呼び出します。

[!code-vb[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample1.vb)]

`DisplayWebConfig` メソッドは、 [`File` クラス](https://msdn.microsoft.com/library/system.io.file.aspx)を使用してアプリケーションの `Web.config` ファイルを開き、 [`StreamReader` クラス](https://msdn.microsoft.com/library/system.io.streamreader.aspx)を使用してその内容を文字列に読み取り、 [`Path` クラス](https://msdn.microsoft.com/library/system.io.path.aspx)を使用して、`Web.config` ファイルへの物理パスを生成します。 これら3つのクラスはすべて、 [`System.IO` 名前空間](https://msdn.microsoft.com/library/system.io.aspx)にあります。 そのため、分離コードクラスの先頭に `Imports``System.IO` ステートメントを追加するか、または、これらのクラス名の前にというプレフィックスを付ける必要があり `System.IO.`

次に、2つのボタンコントロール `Click` イベントのイベントハンドラーを追加し、DPAPI プロバイダーでコンピューターレベルのキーを使用して `<connectionStrings>` セクションを暗号化および復号化するために必要なコードを追加する必要があります。 デザイナーで、各ボタンをダブルクリックして、分離コードクラスに `Click` イベントハンドラーを追加し、次のコードを追加します。

[!code-vb[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample2.vb)]

2つのイベントハンドラーで使用されるコードはほぼ同じです。 どちらも、まず、 [`WebConfigurationManager` クラス](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.aspx)s [`OpenWebConfiguration` メソッド](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.openwebconfiguration.aspx)を使用して、現在のアプリケーションの `Web.config` ファイルに関する情報を取得します。 このメソッドは、指定された仮想パスの web 構成ファイルを返します。 次に、`Web.config` file s `<connectionStrings>` セクションに[`Configuration` クラス](https://msdn.microsoft.com/library/system.configuration.configuration.aspx)s [`GetSection(sectionName)` メソッド](https://msdn.microsoft.com/library/system.configuration.configuration.getsection.aspx)を使用してアクセスします。このメソッドは[`ConfigurationSection`](https://msdn.microsoft.com/library/system.configuration.configurationsection.aspx)オブジェクトを返します。

`ConfigurationSection` オブジェクトには、構成セクションに関する追加の情報と機能を提供する[`SectionInformation` プロパティ](https://msdn.microsoft.com/library/system.configuration.configurationsection.sectioninformation.aspx)が含まれています。 上記のコードに示すように、構成セクションが暗号化されているかどうかを確認するには、`SectionInformation` プロパティ s `IsProtected` プロパティを確認します。 さらに、セクションは、`SectionInformation` プロパティ s `ProtectSection(provider)` と `UnprotectSection` メソッドを使用して暗号化または復号化できます。

`ProtectSection(provider)` メソッドは、暗号化時に使用する保護された構成プロバイダーの名前を指定する文字列を入力として受け入れます。 `EncryptConnString` ボタン s イベントハンドラーで、DataProtectionConfigurationProvider を `ProtectSection(provider)` メソッドに渡して、DPAPI プロバイダーが使用されるようにします。 `UnprotectSection` メソッドは、構成セクションの暗号化に使用されたプロバイダーを特定できます。そのため、入力パラメーターは必要ありません。

`ProtectSection(provider)` または `UnprotectSection` メソッドを呼び出した後、`Configuration` オブジェクト s [`Save` メソッド](https://msdn.microsoft.com/library/system.configuration.configuration.save.aspx)を呼び出して変更を保持する必要があります。 構成情報が暗号化または暗号化解除され、変更が保存されたら、`DisplayWebConfig` を呼び出して、更新された `Web.config` の内容をテキストボックスコントロールに読み込みます。

上記のコードを入力したら、ブラウザーを使用して `EncryptingConfigSections.aspx` のページにアクセスしてテストします。 最初に、`<connectionStrings>` セクションがプレーンテキストで表示されている `Web.config` の内容を一覧表示するページが表示されます (図3を参照)。

[テキストボックスと2つのボタン Web コントロールをページに追加 ![には](protecting-connection-strings-and-other-configuration-information-vb/_static/image8.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image7.png)

**図 3**: テキストボックスと2つのボタン Web コントロールをページに追加する ([クリックすると、フルサイズの画像が表示](protecting-connection-strings-and-other-configuration-information-vb/_static/image9.png)されます)

次に、[接続文字列の暗号化] ボタンをクリックします。 要求の検証が有効になっている場合は、`WebConfigContents` テキストボックスからポストバックされたマークアップによって `HttpRequestValidationException`が生成されます。このメッセージには、危険性のある `Request.Form` 値がクライアントから検出されたことが示されます。 ASP.NET 2.0 で既定で有効になっている要求の検証では、エンコードされていない HTML を含むポストバックは禁止されており、スクリプトインジェクション攻撃を防ぐことができるように設計されています。 このチェックは、ページレベルまたはアプリケーションレベルで無効にすることができます。 このページで無効にするには、`ValidateRequest` 設定を `@Page` ディレクティブの `False` に設定します。 `@Page` ディレクティブは、ページの宣言型マークアップの先頭にあります。

[!code-aspx[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample3.aspx)]

要求の検証、その目的、ページおよびアプリケーションレベルでの無効化方法、HTML エンコードマークアップの方法の詳細については、「[要求の検証-スクリプト攻撃の防止](../../../../whitepapers/request-validation.md)」を参照してください。

ページの要求の検証を無効にした後、[接続文字列の暗号化] ボタンをもう一度クリックしてください。 ポストバック時に、構成ファイルにアクセスし、その `<connectionStrings>` セクションを DPAPI プロバイダーを使用して暗号化します。 次に、テキストボックスが更新され、新しい `Web.config` の内容が表示されます。 図4に示すように、`<connectionStrings>` 情報は現在暗号化されています。

[[接続文字列の暗号化] ボタンをクリック ![と &lt;connectionString&gt; セクションが暗号化されます](protecting-connection-strings-and-other-configuration-information-vb/_static/image11.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image10.png)

**図 4**: [接続文字列の暗号化] ボタンをクリックすると `<connectionString>` セクションが暗号化される ([クリックしてフルサイズの画像を表示する](protecting-connection-strings-and-other-configuration-information-vb/_static/image12.png))

コンピューターで生成された暗号化された `<connectionStrings>` セクションは次のとおりです。ただし、`<CipherData>` 要素の内容の一部は簡潔にするために削除されています。

[!code-xml[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample4.xml)]

> [!NOTE]
> `<connectionStrings>` 要素は、暗号化 (`DataProtectionConfigurationProvider`) を実行するために使用するプロバイダーを指定します。 この情報は、[接続文字列の復号化] ボタンをクリックしたときに `UnprotectSection` メソッドによって使用されます。

接続文字列情報が `Web.config` からアクセスされると、コードによって、SqlDataSource コントロールから、または型指定されたデータセットの Tableadapter から自動生成されたコードのいずれかによって、自動的に暗号化が解除されます。 つまり、暗号化された `<connectionString>` セクションの暗号化を解除するために、余分なコードやロジックを追加する必要はありません。 このデモを実行するには、この時点で前のチュートリアルのいずれかを参照してください。たとえば、基本的なレポートのセクション (`~/BasicReporting/SimpleDisplay.aspx`) の簡易表示チュートリアルを参照してください。 図5に示すように、このチュートリアルは想定どおりに動作し、暗号化された接続文字列情報が ASP.NET ページによって自動的に暗号化解除されることを示しています。

[データアクセス層によって接続文字列情報の暗号化が自動的に解除 ![](protecting-connection-strings-and-other-configuration-information-vb/_static/image14.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image13.png)

**図 5**: データアクセス層によって接続文字列情報の暗号化が自動的に解除される ([クリックすると、フルサイズの画像が表示](protecting-connection-strings-and-other-configuration-information-vb/_static/image15.png)されます)

`<connectionStrings>` セクションをプレーンテキスト形式に戻すには、[接続文字列の復号化] ボタンをクリックします。 ポストバック時に、`Web.config` の接続文字列がプレーンテキストで表示されます。 この時点で、このページに初めてアクセスしたときのように画面が表示されます (図3を参照)。

## <a name="step-3-encrypting-configuration-sections-usingaspnet_regiisexe"></a>手順 3:`aspnet_regiis.exe` を使用した構成セクションの暗号化

.NET Framework には、`$WINDOWS$\Microsoft.NET\Framework\version\` フォルダーにさまざまなコマンドラインツールが含まれています。 たとえば、 [Sql キャッシュの依存関係の使用](../caching-data/using-sql-cache-dependencies-vb.md)に関するチュートリアルでは、sql キャッシュの依存関係に必要なインフラストラクチャを追加するために `aspnet_regsql.exe` コマンドラインツールを使用する方法について説明しました。 このフォルダーにあるもう1つの便利なコマンドラインツールは、 [ASP.NET IIS 登録ツール (`aspnet_regiis.exe`)](https://msdn.microsoft.com/library/k6h9cz8h(VS.80).aspx)です。 その名前が示すように、ASP.NET IIS 登録ツールは主に ASP.NET 2.0 アプリケーションを Microsoft の professional グレード Web server (IIS) に登録するために使用されます。 ASP.NET IIS 登録ツールは、IIS 関連の機能に加えて、`Web.config`の指定された構成セクションの暗号化または暗号化解除にも使用できます。

次のステートメントは、`aspnet_regiis.exe` コマンドラインツールを使用して構成セクションを暗号化するために使用される一般的な構文を示しています。

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample5.cmd)]

*section*は暗号化する構成セクション (connectionStrings など)、*物理\_ディレクトリ*は web アプリケーションのルートディレクトリへの完全な物理パス、 *provider*は使用する保護された構成プロバイダーの名前 (dataprotectionconfigurationprovider など) です。 または、web アプリケーションが IIS に登録されている場合は、次の構文を使用して、物理パスの代わりに仮想パスを入力できます。

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample6.cmd)]

次の `aspnet_regiis.exe` 例では、DPAPI プロバイダーとコンピューターレベルのキーを使用して、`<connectionStrings>` セクションを暗号化します。

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample7.cmd)]

同様に、`aspnet_regiis.exe` コマンドラインツールを使用して、構成セクションの暗号化を解除することもできます。 `-pef` スイッチを使用する代わりに、`-pdf` (または `-pe`ではなく `-pd`) を使用します。 また、復号化するときにプロバイダー名は不要であることに注意してください。

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample8.cmd)]

> [!NOTE]
> コンピューターに固有のキーを使用する DPAPI プロバイダーを使用しているため、web ページが提供されているのと同じコンピューターから `aspnet_regiis.exe` を実行する必要があります。 たとえば、このコマンドラインプログラムをローカルの開発用コンピューターから実行してから、暗号化された Web.config ファイルを実稼働サーバーにアップロードした場合、実稼働サーバーでは、暗号化されてから接続文字列情報を復号化することはできません。開発用コンピューターに固有のキーを使用します。 Rsa プロバイダーには、RSA キーを別のコンピューターにエクスポートできるため、このような制限はありません。

## <a name="understanding-database-authentication-options"></a>データベース認証オプションについて

アプリケーションで `SELECT`、`INSERT`、`UPDATE`、または `DELETE` のクエリを Microsoft SQL Server データベースに発行する前に、まずデータベースで要求元を識別する必要があります。 このプロセスは*認証*と呼ばれ、SQL Server は次の2つの認証方法を提供します。

- **Windows 認証**-アプリケーションが実行されているプロセスを使用して、データベースとの通信を行います。 Visual Studio 2005 s ASP.NET 開発サーバーで ASP.NET アプリケーションを実行する場合、ASP.NET アプリケーションは、現在ログオンしているユーザーの id を前提としています。 Microsoft Internet Information Server (IIS) の ASP.NET アプリケーションでは、ASP.NET アプリケーションは通常、`domainName``\MachineName` または `domainName``\NETWORK SERVICE`の id を想定していますが、これはカスタマイズすることもできます。
- **SQL 認証**-ユーザー ID とパスワードの値は、認証の資格情報として指定されます。 SQL 認証では、ユーザー ID とパスワードが接続文字列で指定されます。

Windows 認証は、セキュリティが強化されているため、SQL 認証よりも優先されます。 Windows 認証では、接続文字列はユーザー名とパスワードから解放され、web サーバーとデータベースサーバーが2つの異なるコンピューターに存在する場合、資格情報はネットワーク経由でプレーンテキストで送信されません。 ただし、SQL 認証では、認証資格情報は接続文字列にハードコーディングされ、web サーバーからデータベースサーバーにプレーンテキストで送信されます。

これらのチュートリアルでは、Windows 認証を使用しました。 接続文字列を調べることによって、どの認証モードが使用されているかを知ることができます。 チュートリアル用の接続文字列は、次のようになりました `Web.config`。

`Data Source=.\SQLEXPRESS; AttachDbFilename=|DataDirectory|\NORTHWND.MDF; Integrated Security=True; User Instance=True`

Integrated Security = True であり、ユーザー名とパスワードがない場合は、Windows 認証が使用されていることを示します。 一部の接続文字列では、"信頼された接続 = Yes" または "Integrated Security = SSPI" という用語が統合セキュリティ = True の代わりに使用されますが、3つすべてが Windows 認証を使用することを示します。

次の例は、SQL 認証を使用する接続文字列を示しています。 接続文字列内に埋め込まれている資格情報を確認します。

`Server=serverName; Database=Northwind; uid=userID; pwd=password`

たとえば、攻撃者がアプリケーションの `Web.config` ファイルを表示できるとします。 SQL 認証を使用してインターネット経由でアクセス可能なデータベースに接続する場合、攻撃者はこの接続文字列を使用して、SQL Management Studio または独自の web サイトの ASP.NET ページからデータベースに接続できます。 この脅威を軽減するために、保護された構成システムを使用して `Web.config` の接続文字列情報を暗号化します。

> [!NOTE]
> SQL Server で使用できるさまざまな種類の認証の詳細については、「[セキュリティで保護された ASP.NET アプリケーションの構築: 認証、承認、セキュリティで保護された通信](https://msdn.microsoft.com/library/aa302392.aspx)」を参照してください。 Windows と SQL の認証構文の違いを示す接続文字列の例については、 [ConnectionStrings.com](http://www.connectionstrings.com/)を参照してください。

## <a name="summary"></a>まとめ

既定では、ASP.NET アプリケーションの `.config` 拡張子を持つファイルには、ブラウザーからアクセスすることはできません。 これらの種類のファイルには、データベース接続文字列、ユーザー名とパスワードなどの機密情報が含まれている可能性があるため、返されません。 .NET 2.0 の保護された構成システムは、指定された構成セクションを暗号化できるようにすることで、機密情報をさらに保護するのに役立ちます。 保護された構成プロバイダーには、RSA アルゴリズムを使用するものと、Windows Data Protection API (DPAPI) を使用するものの2つがあります。

このチュートリアルでは、DPAPI プロバイダーを使用して構成設定を暗号化および復号化する方法について説明しました。 これは、手順 2. で説明したようにプログラムによって行うことも、手順 3. で説明した `aspnet_regiis.exe` コマンドラインツールを使用して行うこともできます。 ユーザーレベルのキーを使用する方法、または RSA プロバイダーを使用する方法の詳細については、「参考資料」セクションを参照してください。

プログラミングを楽しんでください。

## <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [Secure ASP.NET アプリケーションの構築: 認証、承認、セキュリティで保護された通信](https://msdn.microsoft.com/library/aa302392.aspx)
- [ASP.NET 2.0 アプリケーションの構成情報の暗号化](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [ASP.NET 2.0 での `Web.config` 値の暗号化](https://weblogs.asp.net/scottgu/archive/2006/01/09/434893.aspx)
- [方法: DPAPI を使用して ASP.NET 2.0 の構成セクションを暗号化する](https://msdn.microsoft.com/library/ms998280.aspx)
- [方法: RSA を使用して ASP.NET 2.0 の構成セクションを暗号化する](https://msdn.microsoft.com/library/ms998283.aspx)
- [.NET 2.0 の構成 API](http://www.odetocode.com/Articles/418.aspx)
- [Windows データ保護](https://msdn.microsoft.com/library/ms995355.aspx)

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は[ *、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 mitchell@4GuysFromRolla.comでアクセスでき[ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは[http://ScottOnWriting.NET](http://ScottOnWriting.NET)にあります。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Teresa Murphy と Randy/Midt でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、mitchell@4GuysFromRolla.comの行を削除[します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb.md)
> [次へ](debugging-stored-procedures-vb.md)

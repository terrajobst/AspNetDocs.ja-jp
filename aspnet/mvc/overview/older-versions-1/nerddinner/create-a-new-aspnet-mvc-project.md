---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 新しい ASP.NET MVC プロジェクトを作成する |Microsoft Docs
author: microsoft
description: 手順 1. では、基本的なユーザーのアプリケーション構造を配置する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469240"
---
# <a name="create-a-new-aspnet-mvc-project"></a>新しい ASP.NET MVC プロジェクトを作成する

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法について説明する無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順1です。
> 
> 手順 1. では、基本的なユーザーのアプリケーション構造を配置する方法を示します。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-1-file-gtnew-project"></a>手順 1: ファイル&gt;新しいプロジェクトを作成する

次に、Visual Studio 2008 または無料の Visual Web Developer 2008 Express のいずれかで、[**ファイル]&gt;[新しいプロジェクト**] メニュー項目を選択して、このアプリケーションを開始します。

[新しいプロジェクト] ダイアログが表示されます。 新しい ASP.NET MVC アプリケーションを作成するには、ダイアログの左側にある [Web] ノードを選択し、右側の [ASP.NET MVC Web アプリケーション] プロジェクトテンプレートを選択します。

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*重要: ASP.NET MVC をダウンロードしてインストールしたことを確認してください。そうしないと、[新しいプロジェクト] ダイアログに表示されません。まだインストールしていない場合は、 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)の V2 を使用できます (ASP.NET MVC は、"Web Platform-&gt;framework and runtime" セクション内で利用できます)。*

作成する新しいプロジェクトに "are Dディナー" という名前を指定し、[ok] ボタンをクリックして作成します。

[Ok] をクリックすると、Visual Studio によって追加のダイアログが表示され、必要に応じて新しいアプリケーションの単体テストプロジェクトも作成するように求められます。 この単体テストプロジェクトを使用すると、アプリケーションの機能と動作を確認する自動テストを作成できます (このチュートリアルで後ほど説明します)。

![](create-a-new-aspnet-mvc-project/_static/image2.png)

このダイアログの [テストフレームワーク] ドロップダウンには、コンピューターにインストールされている使用可能なすべての ASP.NET MVC 単体テストプロジェクトテンプレートが表示されます。 NUnit、MBUnit、XUnit のバージョンをダウンロードできます。 組み込みの Visual Studio 単体テストフレームワークもサポートされています。

*注: Visual Studio 単体テストフレームワークは、Visual Studio 2008 Professional 以降のバージョンでのみ使用できます。VS 2008 Standard Edition または Visual Web Developer 2008 Express を使用している場合は、このダイアログを表示するために、ASP.NET MVC の NUnit、MBUnit、または XUnit 拡張機能をダウンロードしてインストールする必要があります。テストフレームワークがインストールされていない場合、ダイアログは表示されません。*

ここでは、作成したテストプロジェクトに対して既定の "" を使用する "という名前を使用し、" Visual Studio 単体テスト "フレームワークオプションを使用します。 [Ok] ボタンをクリックすると、Visual Studio によって、2つのプロジェクト (web アプリケーション用と単体テスト用) を含むソリューションが作成されます。

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>各ディレクトリ構造の検証

Visual Studio で新しい ASP.NET MVC アプリケーションを作成すると、次のような多数のファイルとディレクトリがプロジェクトに自動的に追加されます。

![](create-a-new-aspnet-mvc-project/_static/image4.png)

既定では、ASP.NET MVC プロジェクトには、次の6つの最上位レベルのディレクトリがあります。

| **ディレクトリ** | **目的** |
| --- | --- |
| **/コントローラー** | URL 要求を処理するコントローラークラスを配置する場所 |
| **/Models** | データを表現および操作するクラスを配置する場所 |
| **/Views** | 出力のレンダリングを担当する UI テンプレートファイルを配置する場所 |
| **/Scripts** | JavaScript ライブラリファイルとスクリプト (.js) を配置する場所 |
| **/コンテンツ** | CSS およびイメージファイル、およびその他の非動的/非 JavaScript コンテンツを配置する場所 |
| **/アプリ\_データ** | 読み取り/書き込みの対象となるデータファイルを保存する場所。 |

ASP.NET MVC では、この構造は必要ありません。 実際、大規模なアプリケーションで作業している開発者は、通常、アプリケーションを複数のプロジェクトに分割して管理しやすくしています (たとえば、データモデルクラスは、多くの場合、web アプリケーションとは別のクラスライブラリプロジェクトにあります)。 ただし、既定のプロジェクト構造には、アプリケーションの問題をクリーンな状態に保つために使用できる、既定のディレクトリ規則が用意されています。

コントローラーディレクトリを展開すると、Visual Studio によって、HomeController と AccountController という2つのコントローラークラスが既定でプロジェクトに追加されていることがわかります。

![](create-a-new-aspnet-mvc-project/_static/image5.png)

ビューディレクトリを展開すると、3つのサブディレクトリ (/Home、/Account、/Shared) が検出されます。また、その中にはいくつかのテンプレートファイルも既定でプロジェクトに追加されています。

![](create-a-new-aspnet-mvc-project/_static/image6.png)

/コンテンツディレクトリとスクリプトディレクトリを展開すると、サイト上のすべての HTML のスタイルを設定するために使用される .css ファイルと、アプリケーション内で ASP.NET AJAX および jQuery サポートを有効にできる JavaScript ライブラリが見つかります。

![](create-a-new-aspnet-mvc-project/_static/image7.png)

このテストプロジェクトを展開すると、コントローラークラスの単体テストを含む2つのクラスが見つかります。

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Visual Studio によって追加されたこれらの既定のファイルには、作業中のアプリケーション (ホームページ、about ページ、アカウントのログイン/ログアウト/登録ページ) の基本構造と、ハンドルされないエラーページ (すべてのワイヤード (有線) と機能があります) が用意されています。

### <a name="running-the-nerddinner-application"></a>アプリケーションの実行

プロジェクトを実行するには、[デバッグ]、[デバッグの開始]、また&gt;は [デバッグ] の順に選択 **&gt;** し、[デバッグ**なしで開始**] メニュー項目を選択します

![](create-a-new-aspnet-mvc-project/_static/image9.png)

これにより、Visual Studio に付属する組み込みの ASP.NET Web サーバーが起動し、アプリケーションが実行されます。

![](create-a-new-aspnet-mvc-project/_static/image10.png)

次に示すのは、新しいプロジェクト (URL: "/") の実行時のホームページです。

![](create-a-new-aspnet-mvc-project/_static/image11.png)

[バージョン情報] タブをクリックすると、about ページ (URL: "/Home/About") が表示されます。

![](create-a-new-aspnet-mvc-project/_static/image12.png)

右上にある [ログオン] リンクをクリックすると、ログインページ (URL: "/アカウント/ログオン") に移動します。

![](create-a-new-aspnet-mvc-project/_static/image13.png)

ログインアカウントがない場合は、[登録] リンク (URL: "/Account/register") をクリックして作成できます。

![](create-a-new-aspnet-mvc-project/_static/image14.png)

上記の home、about、および logout/register 機能を実装するコードは、新しいプロジェクトを作成したときに既定で追加されました。 アプリケーションの出発点として使用します。

### <a name="testing-the-nerddinner-application"></a>アプリケーションのテスト

Professional Edition 以降のバージョンの Visual Studio 2008 を使用している場合は、Visual Studio 内で組み込みの単体テスト IDE サポートを使用してプロジェクトをテストすることができます。

![](create-a-new-aspnet-mvc-project/_static/image15.png)

上記のオプションのいずれかを選択すると、IDE 内の [テスト結果] ウィンドウが開き、組み込みの機能について説明する新しいプロジェクトに含まれている27の単体テストに合格/不合格の状態が表示されます。

![](create-a-new-aspnet-mvc-project/_static/image16.png)

このチュートリアルの後半では、自動化されたテストについて詳しく説明し、実装するアプリケーション機能をカバーする追加の単体テストを追加します。

### <a name="next-step"></a>次の手順

これで、基本的なアプリケーション構造が完成しました。 次[に、アプリケーションデータを格納するデータベースを作成](create-a-database.md)しましょう。

> [!div class="step-by-step"]
> [前へ](introducing-the-nerddinner-tutorial.md)
> [次へ](create-a-database.md)

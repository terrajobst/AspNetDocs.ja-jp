---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4.7 Web フォームと Visual Studio 2017 でのはじめにMicrosoft Docs
author: Erikre
description: このステップバイステップチュートリアルシリーズでは、ASP.NET 4.7 Microsoft Visual Studio とを使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615451"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a>ASP.NET 4.5 Web フォームと Visual Studio 2017 でのはじめに

[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。

このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio 2017 を使用して ASP.NET Web フォームアプリケーションを構築する方法について説明します。 

## <a name="introduction"></a>はじめに

このチュートリアルシリーズでは、Visual Studio 2017 と ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを作成する手順について説明します。 **Wingtip Toys**という名前のアプリケーションを作成します。これは、簡素化されたストア web サイトで、オンラインでアイテムを販売します。 シリーズの中で、新しい ASP.NET 4.5 の機能が強調表示されています。

### <a name="target-audience"></a>対象ユーザー

ASP.NET Web フォームを初めて使用する開発者は、このチュートリアルシリーズの対象ユーザーです。

次の領域には、いくつかの知識が必要です。

- オブジェクト指向プログラミング (OOP) と言語
- Web 開発 (HTML、CSS、JavaScript)
- リレーショナルデータベース
- n 層アーキテクチャ

これらの領域を確認するには、次の内容を確認することを検討してください。

- [Visual C# 入門](https://msdn.microsoft.com/library/a72418yk.aspx)
- [Web 開発](https://msdn.microsoft.com/beginner/bb308760.aspx)、 [HTML、CSS、JavaScript、SQL、PHP、JQuery](http://w3schools.com/)
- [リレーショナルデータベース](http://en.wikipedia.org/wiki/Relational_database)
- [多層アーキテクチャ](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a>アプリケーションの機能

このシリーズでは、次のような ASP.NET Web フォーム機能を紹介します。

- Web アプリケーションプロジェクト (Web サイトプロジェクトではない)
- Web フォーム
- マスターページ、構成
- ブートストラップ
- Entity Framework Code First、LocalDB
- 要求の検証
- 厳密に型指定されたデータコントロール
- モデル バインド
- データの注釈
- 値プロバイダー
- SSL と OAuth
- ASP.NET Identity、構成、および承認
- 控えめに検証
- ルーティング
- ASP.NET エラー処理

### <a name="application-scenarios-and-tasks"></a>アプリケーションのシナリオとタスク

チュートリアルシリーズのタスクは次のとおりです。

- 新しいプロジェクトの作成、確認、および実行
- データベース構造の作成
- データベースの初期化とシード処理
- スタイル、グラフィックス、およびマスターページを使用した UI のカスタマイズ
- ページおよびナビゲーションの追加
- メニューの詳細と製品データを表示する
- ショッピングカートの作成
- SSL および OAuth サポートの追加
- 支払い方法の追加
- 管理者ロールとユーザーをアプリケーションに含める
- 特定のページおよびフォルダーへのアクセスを制限する
- Web アプリケーションへのファイルのアップロード
- 入力検証の実装
- Web アプリケーションのルートを登録しています
- エラー処理とエラーログの実装

## <a name="overview"></a>の概要

このチュートリアルシリーズは、プログラミングの概念に習熟している方を対象としていますが、ASP.NET Web フォームが新しく追加されました。 ASP.NET の Web フォームを既に使い慣れている場合でも、このシリーズでは、ASP.NET 4.5 の新機能について学習できます。 プログラミングの概念と ASP.NET の Web フォームに慣れていない読者には、ASP.NET Web サイトの[はじめに](../../../index.md)セクションに記載されている追加の web フォームチュートリアルを参照してください。

このチュートリアルシリーズで提供されている ASP.NET 4.5 には、次の機能が含まれています。

- [多くの ASP.NET フレームワーク](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add)(web フォーム、MVC、web API) をサポートするプロジェクトを作成するための簡単な UI です。
- [ブートストラップ](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)、レイアウト、テーマ、および応答性のデザインフレームワーク。
- [ASP.NET Identity](../../../../identity/index.md)、すべての ASP.NET フレームワークで同じように動作し、IIS 以外の web ホスティングソフトウェアで動作する新しい ASP.NET メンバーシップシステムです。
- [Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx)

  Entity Framework の更新により、次のことが可能になります。
  - 厳密に型指定されたオブジェクトとしてデータを取得および操作する
  - データへの非同期アクセス
  - 一時的な接続エラーの処理
  - ログ SQL ステートメント

ASP.NET 4.5 の完全な機能一覧については、 [Visual Studio 2013 リリースノートの ASP.NET and Web Tools](../../../../visual-studio/overview/2013/release-notes.md)を参照してください。

### <a name="the-wingtip-toys-sample-application"></a>Wingtip Toys サンプルアプリケーション

次のスクリーンショットは、このチュートリアルシリーズで作成する ASP.NET Web フォームアプリケーションのものです。 Visual Studio でアプリケーションを実行すると、次の web ホームページが表示されます。

![Wingtip Toys-既定のページ](introduction-and-overview/_static/image1.png)

新しいユーザーとして登録することも、既存のユーザーとしてサインインすることもできます。 上部のナビゲーションには、データベースから製品カテゴリと製品へのリンクがあります。

**[製品]** を選択すると、利用可能なすべての製品が表示されます。 

![Wingtip Toys-製品](introduction-and-overview/_static/image2.png)

特定の製品を選択すると、製品の詳細が表示されます。

![Wingtip Toys-製品の詳細](introduction-and-overview/_static/image3.png)

ユーザーは、Web フォームテンプレートの既定の機能を使用して、登録とサインインを行うことができます。 このチュートリアルでは、既存の Gmail アカウントを使用してサインインする方法についても説明します。 また、管理者としてサインインして、データベースの製品を追加および削除することもできます。

![Wingtip Toys-サインイン](introduction-and-overview/_static/image4.png)

ユーザーとしてサインインすると、ショッピングカートに製品を追加して、PayPal でチェックアウトできます。 このサンプルアプリケーションは、PayPal の開発者サンドボックスで動作するように設計されています。 実際の金額トランザクションは発生しません。

![Wingtip Toys-ショッピングカート](introduction-and-overview/_static/image5.png)

PayPal は、お客様のアカウント、注文、支払い情報を確認します。

![Wingtip Toys-PayPal](introduction-and-overview/_static/image6.png)

PayPal から戻った後、注文を確認して完了することができます。

![Wingtip Toys-注文レビュー](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a>必要条件

開始する前に、次のソフトウェアがコンピューターにインストールされていることを確認してください。

- [Microsoft Visual Studio 2017 または Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/)。

.NET Framework は自動的にインストールされます。

このチュートリアルシリーズでは、Microsoft Visual Studio Community 2017 を使用します。 このチュートリアルシリーズを完了するには、または Microsoft Visual Studio 2017 を使用できます。

Visual Studio については、次の点に注意してください。

* このチュートリアルシリーズでは、Microsoft Visual Studio 2017 と Microsoft Visual Studio Community 2017 を*Visual Studio*と呼びます。

* Visual Studio 2017 は、既にインストールされている古いバージョンの横にインストールされます。 以前のバージョンで作成されたサイトは Visual Studio 2017 で開くことができ、以前のバージョンでは引き続き開くことができます。

* Visual Studio を初めて起動したときは、 *Web 開発*設定を選択したと見なされます。 詳細については、「[方法: Web 開発環境の設定を選択する](https://msdn.microsoft.com/library/ff521558.aspx)」を参照してください。

前提条件をインストールしたら、このチュートリアルシリーズで紹介する Web プロジェクトの作成を開始できます。

## <a name="download-the-sample-application"></a>サンプルアプリケーションをダウンロードする

 完成したサンプルアプリケーションは、MSDN サンプルサイトからいつでもダウンロードできます。

C# [ASP.NET 4.5 Web フォームと Visual Studio 2013-Wingtip Toys () を使用したはじめに](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 

 このダウンロードには次の項目があります。

- *ウィングヒント toys*フォルダー内のサンプルアプリケーション。
- このサンプルアプリケーションを作成するために使用されるリソースは、*ウィング? toys*フォルダー内の*ウィングヒントの toys-Assets*フォルダーにあります。

ダウンロードは *.zip*ファイルです。 このチュートリアルシリーズで作成した完成したプロジェクトを表示するに*C#* は、.zip ファイル内のフォルダーを見つけて選択します。 Visual Studio C#プロジェクトを操作するために使用するフォルダーにフォルダーを保存します。 既定では、Visual Studio 2017 projects フォルダーは次のとおりです。

<strong>C:\Users&#92;</strong>  <strong><em>&lt;ユーザー名&gt;</em></strong>

フォルダーの***C#*** 名前を「***ウィング? toys***」に変更します。

> [!NOTE]
> 既にプロジェクトフォルダーにウィング? *toys*という名前のフォルダーがある場合は、フォルダーの*C#* 名前を「ウィング? *toys*」に変更する前に、既存のフォルダーの名前を一時的に変更します。

完成したプロジェクトを実行するには、*ウィングヒントの toys*フォルダーを開き、*ウィングヒントの toys. .sln*ファイルをダブルクリックします。 Visual Studio 2017 によってプロジェクトが開きます。 次に、**ソリューションエクスプローラー**で*default.aspx*ファイルを右クリックし、 **[ブラウザーで表示]** を選択します。

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a>ASP.NET の Web フォームクイズでコンテンツを確認する

チュートリアルシリーズを完了したら、クイズを使用して知識をテストし、主要な概念を補強します。 各質問には、説明と追加のガイダンスへのリンクが記載されています。

* [ASP.NET Web フォームのクイズ](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a>チュートリアルのサポートとコメント

質問やコメントについては、 [ASP.NET 4.5 Web フォームおよび Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) サンプルページのはじめにに記載されている Q とセクションを使用します。

このチュートリアルシリーズのコメントは歓迎されます。 このチュートリアルシリーズを更新すると、修正や改善の提案についてすべての取り組みが行われます。

エラーが発生した場合は、対応するエラーメッセージが混乱する可能性があり、修正方法についての適切な説明はありません。 ヘルプを表示するには、 [ASP.NET フォーラム](https://forums.asp.net/)を確認してください。 もう1つの優れたソースは、 [ASP.NET 4.5 Web フォームと Visual Studio 2013 Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) サンプルページのはじめにの Q と A セクションです。 

> [!div class="step-by-step"]
> [次へ](create-the-project.md)

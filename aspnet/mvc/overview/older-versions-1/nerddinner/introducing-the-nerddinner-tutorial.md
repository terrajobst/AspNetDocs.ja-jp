---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: このチュートリアルの概要 |Microsoft Docs
author: shanselman
description: 新しいフレームワークを学習する最善の方法は、それを使用して何かを構築することです。 このチュートリアルでは、ASP.NE を使用して小規模で、完成したアプリケーションを作成する方法について説明します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468934"
---
# <a name="introducing-the-nerddinner-tutorial"></a>NerdDinner チュートリアルの紹介

[Scott マン Selman](https://github.com/shanselman)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 新しいフレームワークを学習する最善の方法は、それを使用して何かを構築することです。 このチュートリアルでは、ASP.NET MVC 1 を使用して小規模で、完成したアプリケーションを作成する方法について説明し、その背後にある主要な概念をいくつか紹介します。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-tutorial"></a>のチュートリアル

新しいフレームワークを学習する最善の方法は、それを使用して何かを構築することです。 このチュートリアルでは、ASP.NET MVC を使用して小規模で、完成したアプリケーションを構築する方法について説明し、その背後にある主要な概念をいくつか紹介します。

ビルドしようとしているアプリケーションは、"実行中" と呼ばれます。 ディナー online を簡単に検索して整理するには、次のような簡単な方法があります。

![](introducing-the-nerddinner-tutorial/_static/image1.png)

ユーザーは、ディナーを作成、編集、削除することができます。 アプリケーション全体で一貫性のある検証とビジネスルールのセットを適用します。

![](introducing-the-nerddinner-tutorial/_static/image2.png)

訪問者は、AJAX ベースのマップを使用して、近い将来に保持されているディナーを検索できます。

![](introducing-the-nerddinner-tutorial/_static/image3.png)

ディナーをクリックすると、詳細ページが表示され、詳細を確認できます。

![](introducing-the-nerddinner-tutorial/_static/image4.png)

夕食に参加したい場合は、次のようにして、サイトにログインまたは登録できます。

![](introducing-the-nerddinner-tutorial/_static/image5.png)

次に、AJAX ベースの RSVP リンクをクリックして、イベントに参加できます。

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>ディナー Dディナーの実装

ここでは、Visual Studio 内でファイル&gt;[新しいプロジェクト] コマンドを使用して新しい ASP.NET MVC プロジェクトを作成することにより、このアプリケーションを開始します。 次に、機能と機能を段階的に追加します。 ここでは、次のことについて説明します。

1. [新しい ASP.NET MVC プロジェクトを作成する方法](create-a-new-aspnet-mvc-project.md)
2. [データベースを作成する方法](create-a-database.md)
3. [ビジネスルール検証を使用してモデルを構築する方法](build-a-model-with-business-rule-validations.md)
4. [リスト/詳細 UI を実装するためにコントローラーとビューを使用する方法](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [CRUD (作成、読み取り、更新、削除) データフォームエントリのサポートを提供する方法](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [ViewData を使用して、ビューモデルクラスを実装する方法](use-viewdata-and-implement-viewmodel-classes.md)
7. [マスターページとパーシャルを使用して UI を再利用する方法](re-use-ui-using-master-pages-and-partials.md)
8. [効率的なデータページングを実装する方法](implement-efficient-data-paging.md)
9. [認証と承認を使用してアプリケーションをセキュリティで保護する方法](secure-applications-using-authentication-and-authorization.md)
10. [AJAX を使用して動的更新を配信する方法](use-ajax-to-deliver-dynamic-updates.md)
11. [AJAX を使用してマッピングシナリオを実装する方法](use-ajax-to-implement-mapping-scenarios.md)
12. [自動単体テストを有効にする方法](enable-automated-unit-testing.md)

この章のチュートリアルの各手順を実行することで、最初から自分で作成した自分のコピーを作成できます。 または、ソースコードの完全なバージョンを、 [GitHub の「で](https://github.com/AspNetMVPSamples/NerdDinner)は、こちらからダウンロードできます。 このチュートリアルをオフラインで読む場合は、必要に応じて、[このチュートリアルの無料 PDF バージョンをダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)することもできます。

Visual Studio 2008 または無料の Visual Web Developer 2008 Express を使用して、アプリケーションをビルドできます。 SQL Server またはデータベースの空き SQL Server Express を使用できます。

の V2 を使用して、ASP.NET MVC、Visual Web Developer 2008 Express、SQL Server Express (すべて無料) をインストールでき[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)

### <a name="now-lets-get-started"></a>では、始めましょう。

これで、次は、引き締めをロールアップしてコードを記述しました。

まず、Visual Studio 内でファイル&gt;新しいプロジェクトを使用して、このアプリケーションを作成します。

> [!div class="step-by-step"]
> [Next](create-a-new-aspnet-mvc-project.md)

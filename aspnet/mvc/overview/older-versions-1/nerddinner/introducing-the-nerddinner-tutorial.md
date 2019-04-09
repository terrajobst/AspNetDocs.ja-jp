---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: NerdDinner チュートリアルの紹介 |Microsoft Docs
author: shanselman
description: 新しいフレームワークを学習する最善の方法では、何らかの処理を構築します。 このチュートリアル ASP.NE を使用して、サイズは小さいが完了すると、アプリケーションを構築する方法について説明しています.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: ebd49295ea165ba4ef1a25398cff7dddcfa54f11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59392197"
---
# <a name="introducing-the-nerddinner-tutorial"></a>NerdDinner チュートリアルの紹介

[Scott Hanselman](https://github.com/shanselman)による

[PDF をダウンロードします。](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 新しいフレームワークを学習する最善の方法では、何らかの処理を構築します。 このチュートリアルでは、小さなをビルドしても、ASP.NET MVC 1 を使用してアプリケーションを実行する方法について説明し、その背後にある主要な概念の一部が導入されています。
> 
> 次のことをお勧め ASP.NET MVC 3 を使用している場合、 [MVC 3 の開始と取得](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)または[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)チュートリアル。


## <a name="nerddinner-tutorial"></a>NerdDinner チュートリアル

新しいフレームワークを学習する最善の方法では、何らかの処理を構築します。 このチュートリアルでは、小さなをビルドしても、ASP.NET MVC を使用してアプリケーションを実行する方法について説明し、その背後にある主要な概念の一部が導入されています。

アプリケーションをビルドするには、"NerdDinner"が呼び出されます。 NerdDinner では、ユーザーの検索し、整理の dinners をオンラインに簡単な方法を提供します。

![](introducing-the-nerddinner-tutorial/_static/image1.png)

NerdDinner では、登録済みユーザーを作成、編集、および dinners を削除できるようにします。 アプリケーション全体で一貫性のある一連の検証とビジネス ルールを適用します。

![](introducing-the-nerddinner-tutorial/_static/image2.png)

訪問者は、AJAX ベースのマップを使用して、近くに保持されている次回の dinners を検索できます。

![](introducing-the-nerddinner-tutorial/_static/image3.png)

クリックすると、dinner は持ち運ぶ詳細ページに学ぶことができる詳細については。

![](introducing-the-nerddinner-tutorial/_static/image4.png)

Dinner への参加に興味を持つ場合は、ログインまたはサイトに登録できます。

![](introducing-the-nerddinner-tutorial/_static/image5.png)

イベントに出席する RSVP の AJAX ベースのリンクをクリックしています。

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>NerdDinner を実装します。

ファイル-を使用して、NerdDinner アプリケーションを開始しようとして&gt;Visual Studio 内で新しい ASP.NET MVC プロジェクトを作成する新しいプロジェクト コマンド。 私たちの機能と機能増分追加します。 その過程について説明します。

1. [新しい ASP.NET MVC プロジェクトを作成する方法](create-a-new-aspnet-mvc-project.md)
2. [データベースを作成する方法](create-a-database.md)
3. [ビジネス ルール検証でモデルを構築する方法](build-a-model-with-business-rule-validations.md)
4. [コント ローラーとビューを使用して、リスティング/詳細 UI を実装する方法](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [CRUD を提供する方法 (作成、読み取り、更新、削除) データ フォーム エントリ サポート](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [ViewData を使用し、ViewModel クラスを実装する方法](use-viewdata-and-implement-viewmodel-classes.md)
7. [マスター ページおよびパーシャルを使用して UI を再利用する方法](re-use-ui-using-master-pages-and-partials.md)
8. [効率的なデータ ページングを実装する方法](implement-efficient-data-paging.md)
9. [認証と承認を使用してアプリケーションをセキュリティで保護する方法](secure-applications-using-authentication-and-authorization.md)
10. [AJAX を使用して、動的な更新プログラムを配信する方法](use-ajax-to-deliver-dynamic-updates.md)
11. [AJAX を使用して、マッピングのシナリオを実装する方法](use-ajax-to-implement-mapping-scenarios.md)
12. [自動化された単体テストを有効にする方法](enable-automated-unit-testing.md)

NerdDinner の独自のコピーを構築する各を実行して最初から手順チュートリアルの「します。 または、ここで、ソース コードの完成版をダウンロードできます。[GitHub で NerdDinner](https://github.com/AspNetMVPSamples/NerdDinner)します。 また、必要に応じて[このチュートリアルの無料 PDF 版をダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)オフライン チュートリアルを読みたい場合。

Visual Studio 2008 または、無料の Visual Web Developer 2008 Express のいずれかを使用するには、アプリケーションをビルドします。 データベースの SQL Server または無料の SQL Server Express のいずれかを使用することができます。

ASP.NET MVC、Visual Web Developer 2008 Express、および SQL Server Express (すべて無料) の V2 を使用してをインストールすることができます、 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)

### <a name="now-lets-get-started"></a>今すぐ開始しましょう.

NerdDinner が、ここで説明した、これで、とりかかりましょうをいくつかのコードを記述しましょう。

まず、ファイルを使用して&gt;NerdDinner アプリケーションを作成する Visual Studio 内で新しいプロジェクト。

> [!div class="step-by-step"]
> [次へ](create-a-new-aspnet-mvc-project.md)

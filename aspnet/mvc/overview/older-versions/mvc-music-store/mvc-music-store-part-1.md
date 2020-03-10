---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: 'パート 1: 概要とファイル > 新しいプロジェクト |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート1では、概要とファイル > 新しいプロジェクトについて説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451282"
---
# <a name="part-1-overview-and-file-new-project"></a>パート 1: 概要とファイル > 新しいプロジェクト

( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。  
>   
> MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。  
>   
> このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート1では、概要とファイル&gt;新しいプロジェクトについて説明します。

## <a name="overview"></a>概要

MVC Music Store は、ASP.NET MVC と Visual Web Developer を使用して Web 開発を行う方法を紹介したチュートリアルアプリケーションです。 開始に時間がかかります。初心者レベルの web 開発エクスペリエンスは問題ありません。

ビルドするアプリケーションは、単純なミュージックストアです。 アプリケーションには、買い物、チェックアウト、管理という3つの主要な部分があります。

![](mvc-music-store-part-1/_static/image1.jpg)

閲覧者はジャンルでアルバムを参照できます。

![](mvc-music-store-part-1/_static/image2.jpg)

1つのアルバムを表示し、カートに追加することができます。

![](mvc-music-store-part-1/_static/image3.jpg)

カートをレビューして、不要になったアイテムを削除することができます。

![](mvc-music-store-part-1/_static/image4.jpg)

チェックアウトに進むと、ユーザーアカウントにログインまたは登録するように求められます。

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

アカウントを作成した後は、出荷と支払いに関する情報を入力して注文を完了できます。 簡潔にするために、すばらしいプロモーションを実行しています。プロモーションコードを "無料" で入力すると、すべて無料で利用できます。

![](mvc-music-store-part-1/_static/image5.jpg)

順序を付けると、簡単な確認画面が表示されます。

![](mvc-music-store-part-1/_static/image6.jpg)

顧客向けのページだけでなく、管理者がアルバムの作成、編集、削除を行うことができるアルバムの一覧を示す管理者セクションも作成します。

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a>1. ファイル&gt; 新しいプロジェクト

### <a name="installing-the-software"></a>ソフトウェアのインストール

このチュートリアルを開始するには、無料の Visual Web Developer 2010 Express (無料) を使用して新しい ASP.NET MVC 3 プロジェクトを作成し、機能を段階的に追加して、完全に機能するアプリケーションを作成します。 この過程で、データベースへのアクセス、フォームのポストのシナリオ、データの検証、一貫性のあるページレイアウトのためのマスターページの使用、ページの更新と検証に AJAX を使用する、ユーザーログインなどについて説明します。

ステップバイステップで進めることができます。または、完成したアプリケーションを[MVC-Music-ストア](https://github.com/evilDave/MVC-Music-Store)からダウンロードすることもできます。

Visual Studio 2010 SP1 または Visual Web Developer 2010 Express SP1 (Visual Studio 2010 の無料版) のいずれかを使用して、アプリケーションをビルドできます。 データベースをホストするために SQL Server Compact (または無料) を使用します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。

- [Visual Studio Web Developer Express SP1 の前提条件]
- [ASP.NET MVC 3 Tools Update]
- [SQL Server Compact 4.0]-ランタイムとツールの両方のサポートを含む

### <a name="creating-a-new-aspnet-mvc-3-project"></a>新しい ASP.NET MVC 3 プロジェクトを作成する

まず、Visual Web Developer の [ファイル] メニューから [新しいプロジェクト] を選択します。 [新しいプロジェクト] ダイアログが表示されます。

![](mvc-music-store-part-1/_static/image5.png)

左側の [Visual C#&gt; web テンプレート] グループを選択し、中央の列で "ASP.NET MVC 3 web アプリケーション" テンプレートを選択します。 プロジェクトに MvcMusicStore という名前を指定し、[OK] をクリックします。

![](mvc-music-store-part-1/_static/image8.jpg)

これにより、プロジェクトの MVC 固有の設定を行うためのセカンダリダイアログが表示されます。 次のように選択します。

プロジェクトテンプレート-[空を選択]

ビューエンジン-Razor の選択

HTML5 セマンティックマークアップの使用-チェック済み

設定が次のようになっていることを確認し、[OK] をクリックします。

![](mvc-music-store-part-1/_static/image9.jpg)

これにより、プロジェクトが作成されます。 ここでは、アプリケーションに追加されたフォルダーを右側のソリューションエクスプローラーに見てみましょう。

![](mvc-music-store-part-1/_static/image10.jpg)

空の MVC 3 テンプレートは完全に空ではないため、基本的なフォルダー構造が追加されます。

![](mvc-music-store-part-1/_static/image6.png)

ASP.NET MVC では、フォルダー名に対していくつかの基本的な名前付け規則を使用します。

| **フォルダー** | **目的** |
| --- | --- |
| **/コントローラー** | コントローラーは、ブラウザーからの入力に応答し、その処理を決定し、ユーザーに応答を返します。 |
| **/Views** | ビューは UI テンプレートを保持します |
| **/Models** | データの保持と操作を行うモデル |
| **/コンテンツ** | このフォルダーには、イメージ、CSS、およびその他の静的コンテンツが保持されます。 |
| **/Scripts** | このフォルダーには、JavaScript ファイルが保持します |

これらのフォルダーは、空の ASP.NET MVC アプリケーションにも含まれています。 ASP.NET MVC フレームワークでは、既定では "構成に基づく規約" アプローチが使用され、フォルダーの名前付け規則に基づいて既定の仮定がいくつか行われているためです。 たとえば、コントローラーは既定で Views フォルダー内のビューを検索しますが、コードで明示的に指定する必要はありません。 既定の規則に従うと、記述する必要のあるコードの量が減り、他の開発者がプロジェクトを理解しやすくなります。 これらの規則については、アプリケーションを作成するときに説明します。

> [!div class="step-by-step"]
> [Next](mvc-music-store-part-2.md)

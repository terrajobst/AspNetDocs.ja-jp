---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: ASP.NET Web ページ (Razor) サイトでのヘルパーのインストール |Microsoft Docs
author: Rick-Anderson
description: この記事では、ASP.NET Web ページ (Razor) web サイトにヘルパーをインストールする方法について説明します。 ヘルパーは、コードとマークアップを含む再利用可能なコンポーネントです...
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518644"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a>ASP.NET Web ページ (Razor) サイトへのヘルパーのインストール

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ASP.NET Web ページ (Razor) web サイトにヘルパーをインストールする方法について説明します。 *ヘルパー*は、煩雑または複雑なタスクを実行するためのコードとマークアップを含む再利用可能なコンポーネントです。
> 
> ここでは、次の内容について学習します。
> 
> - WebMatrix 3 を使用して作成された web サイトにヘルパーをインストールする方法について説明します。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - WebMatrix 3

## <a name="overview-of-helpers"></a>ヘルパーの概要

Web ページで頻繁に実行するタスクには、多くのコードが必要になる場合や、追加の知識が必要な場合があります。 たとえば、データのグラフを表示します。ページに Twitter の "フォロー" ボタンを配置するweb サイトから電子メールを送信しています。イメージのトリミングまたはサイズ変更サイトで PayPal を使用します。 このような作業を簡単に行うために、ASP.NET Web ページで*ヘルパー*を使用できます。 ヘルパーは、サイト用にインストールするコンポーネントであり、1行または2行の Razor コードだけを使用して一般的なタスクを実行できます。

ASP.NET Web ページには、いくつかのヘルパーが組み込まれています。 ただし、NuGet パッケージマネージャーを使用して提供されているパッケージ (アドイン) では、多くのヘルパーを利用できます。 NuGet を使用すると、インストールするパッケージを選択して、インストールのすべての詳細を処理できます。

## <a name="installing-a-helper-in-webmatrix-3"></a>WebMatrix でのヘルパーのインストール3

1. WebMatrix 3 では、 **[NuGet]** ボタンをクリックします。

    ![WebMatrix の [NuGet ギャラリー] ダイアログボックス](installing-helpers/_static/image1.png)
2. NuGet パッケージマネージャーが起動し、使用可能なパッケージが表示されます。 検索ボックスに、インストールするヘルパーのキーワードを入力します。

    ![WebMatrix の [NuGet ギャラリー] ダイアログボックス](installing-helpers/_static/image2.png)
3. パッケージを選択し、 **[インストール]** をクリックします。 パッケージをインストールするかどうかを確認するメッセージが表示されたら [**はい]** をクリックし、条項に同意することを示します。

     初めてヘルパーをインストールした場合は、NuGet によって、ヘルパーを構成するコード用のフォルダーが web サイトに作成されます。
4. ヘルパーをアンインストールするには、 **[ギャラリー]** ボタンをクリックし、 **[インストール済み]** タブをクリックして、アンインストールするパッケージを選択します。

## <a name="installing-the-twitter-helper"></a>Twitter ヘルパーのインストール

最新バージョンの Twitter API は、NuGet を使用してインストールする Twitter ヘルパーと互換性がありません。 プロジェクトに Twitter ヘルパーを設定する方法については、「WebMatrix を使用した[Twitter ヘルパー](twitter-helper.md) 」を参照してください。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

[ASP.NET Web ページ2の概要-プログラミングの基礎](../getting-started/introducing-razor-syntax-c.md)

[WebMatrix を使用した Twitter ヘルパー](twitter-helper.md)

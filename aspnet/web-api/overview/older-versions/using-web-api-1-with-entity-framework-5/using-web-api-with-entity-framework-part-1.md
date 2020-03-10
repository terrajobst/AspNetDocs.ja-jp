---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 'パート 1: 概要とプロジェクトの作成 |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447934"
---
# <a name="part-1-overview-and-creating-the-project"></a>パート 1: 概要とプロジェクトの作成

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

Entity Framework は、オブジェクト/リレーショナルマッピングフレームワークです。 コード内のドメインオブジェクトをリレーショナルデータベースのエンティティにマップします。 ほとんどの場合、データベース層について心配する必要はありません。これは、Entity Framework によって処理されるためです。 コードはオブジェクトを操作し、変更はデータベースに保存されます。

## <a name="about-the-tutorial"></a>チュートリアルについて

このチュートリアルでは、単純なストアアプリケーションを作成します。 アプリケーションには主に2つの部分があります。 通常のユーザーは、製品を表示して注文を作成できます。

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

管理者は、製品の作成、削除、または編集を行うことができます。

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a>学習内容

ここでは次の内容について学習します。

- ASP.NET Web API で Entity Framework を使用する方法について説明します。
- ノックアウトを使用して動的クライアント UI を作成する方法。
- Web API でフォーム認証を使用してユーザーを認証する方法。

このチュートリアルは自己完結していますが、まず次のチュートリアルを読むことをお勧めします。

- [ASP.NET Web API の入門ページ](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [CRUD 操作をサポートする Web API の作成](../creating-a-web-api-that-supports-crud-operations.md)

[ASP.NET MVC](../../../../mvc/index.md)に関する知識も役に立ちます。

## <a name="overview"></a>概要

大まかに言えば、アプリケーションのアーキテクチャは次のようになります。

- ASP.NET MVC では、クライアントの HTML ページが生成されます。
- ASP.NET Web API は、データ (製品と注文) に対して CRUD 操作を公開します。
- Entity Framework は、 C# Web API によって使用されるモデルをデータベースエンティティに変換します。

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

次の図は、アプリケーションのさまざまな層でドメインオブジェクトがどのように表されるかを示しています。データベース層、オブジェクトモデル、最後にワイヤ形式を使用します。これは、HTTP 経由でクライアントにデータを送信するために使用されます。

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a>Visual Studio プロジェクトを作成する

チュートリアルプロジェクトは、Visual Web Developer Express または Visual Studio の完全バージョンのいずれかを使用して作成できます。

**スタート**ページで、 **[新しいプロジェクト]** をクリックします。

**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。 **[ビジュアルC# ]** で **[Web]** を選択します。 プロジェクトテンプレートの一覧で、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。 プロジェクトに "ProductStore" という名前を指定し、[ **OK]** をクリックします。

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

**[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** を選択し、 **[OK]** をクリックします。

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

"インターネットアプリケーション" テンプレートは、フォーム認証をサポートする ASP.NET MVC アプリケーションを作成します。 ここでアプリケーションを実行すると、既にいくつかの機能があります。

- 新しいユーザーは、右上隅にある [登録] リンクをクリックすることで登録できます。
- 登録されたユーザーは、[ログイン] リンクをクリックしてログインできます。

メンバーシップ情報は、自動的に作成されるデータベースに保持されます。 ASP.NET MVC でのフォーム認証の詳細については、「[チュートリアル: ASP.NET mvc でのフォーム認証の使用](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)」を参照してください。

## <a name="update-the-css-file"></a>CSS ファイルを更新する

この手順は表面的なものですが、前のスクリーンショットのようにページがレンダリングされるようになります。

ソリューションエクスプローラーで、[コンテンツ] フォルダーを展開し、[サイト .css] という名前のファイルを開きます。 次の CSS スタイルを追加します。

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [Next](using-web-api-with-entity-framework-part-2.md)

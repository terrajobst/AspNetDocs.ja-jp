---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: 'パート 4: 管理者ビューの追加 |Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600014"
---
# <a name="part-4-adding-an-admin-view"></a>パート 4: 管理ビューの追加

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a>管理ビューの追加

次に、クライアント側に切り替え、管理コントローラーのデータを使用できるページを追加します。 このページでは、ユーザーが AJAX 要求をコントローラーに送信することによって、製品の作成、編集、または削除を行うことができます。

ソリューションエクスプローラーで、Controllers フォルダーを展開し、HomeController.cs という名前のファイルを開きます。 このファイルには、MVC コントローラーが含まれています。 `Admin`という名前のメソッドを追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

**HttpRouteUrl**メソッドは、web API への URI を作成し、後でこのをビューバッグに格納します。

次に、`Admin` アクションメソッド内にテキストカーソルを置き、右クリックして **[ビューの追加]** を選択します。 **[ビューの追加]** ダイアログが表示されます。

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

**[ビューの追加]** ダイアログで、ビューに "Admin" という名前を指定します。 **[厳密に型指定されたビューを作成する]** チェックボックスをオンにします。 **モデルクラス** で、Product (productstore) を選択します。 その他のオプションはすべて既定値のままにしておきます。

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

**[追加]** をクリックすると、Views/Home の下に Admin. cshtml という名前のファイルが追加されます。 このファイルを開き、次の HTML を追加します。 この HTML はページの構造を定義しますが、機能はまだ接続されていません。

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a>管理ページへのリンクを作成する

ソリューションエクスプローラーで、Views フォルダーを展開し、共有フォルダーを展開します。 \_Layout. cshtml という名前のファイルを開きます。 Id が "menu" である**ul**要素と、管理ビューのアクションリンクを探します。

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> サンプルプロジェクトでは、"ここにロゴを入力してください" という文字列を置き換えるなど、いくつかの外観の変更が加えられました。 これらは、アプリケーションの機能には影響しません。 プロジェクトをダウンロードし、ファイルを比較することができます。

アプリケーションを実行し、ホームページの上部に表示される [Admin] \ (管理者 \) リンクをクリックします。 管理者ページは次のようになります。

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

現在、このページでは何も実行されません。 次のセクションでは、ノックアウトを使用して動的 UI を作成します。

## <a name="add-authorization"></a>承認の追加

現在、管理者ページには、サイトにアクセスするすべてのユーザーがアクセスできます。 これを変更して、管理者にアクセス許可を制限してみましょう。

まず、"管理者" ロールと管理者ユーザーを追加します。 ソリューションエクスプローラーで、[フィルター] フォルダーを展開し、InitializeSimpleMembershipAttribute.cs という名前のファイルを開きます。 `SimpleMembershipInitializer` コンストラクターを見つけます。 **InitializeDatabaseConnection**の呼び出しの後に、次のコードを追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

これは、"管理者" ロールを追加し、ロールのユーザーを作成するための簡単な方法です。

ソリューションエクスプローラーで、Controllers フォルダーを展開し、HomeController.cs ファイルを開きます。 `Admin` メソッドに**承認**属性を追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

AdminController.cs ファイルを開き、`AdminController` クラス全体に**承認**属性を追加します。

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> MVC と Web API は両方とも、異なる名前空間の**承認**属性を定義します。 MVC は、system.web. **authorizeattribute**を使用しますが、web API**では、system.web. web.config を**使用します。

管理者のみが管理ページを表示できるようになりました。 また、管理コントローラーに HTTP 要求を送信する場合は、要求に認証クッキーが含まれている必要があります。 それ以外の場合、サーバーは HTTP 401 (未承認) の応答を送信します。 GET 要求を `http://localhost:*port*/api/admin`に送信することで、これを Fiddler で確認できます。

> [!div class="step-by-step"]
> [前へ](using-web-api-with-entity-framework-part-3.md)
> [次へ](using-web-api-with-entity-framework-part-5.md)

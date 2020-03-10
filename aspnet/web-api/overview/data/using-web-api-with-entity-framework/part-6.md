---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: JavaScript クライアントを作成する |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504724"
---
# <a name="create-the-javascript-client"></a>JavaScript クライアントの作成

[Mike Wasson](https://github.com/MikeWasson)

[完成したプロジェクトのダウンロード](https://github.com/MikeWasson/BookService)

このセクションでは、HTML、JavaScript、および[ノックアウト](http://knockoutjs.com/)ライブラリを使用して、アプリケーション用のクライアントを作成します。 クライアントアプリを段階的に構築します。

- 書籍の一覧を表示します。
- 書籍の詳細を表示しています。
- 新しい書籍を追加します。

ノックアウトライブラリは、モデルビュービューモデル (MVVM) パターンを使用します。

- この**モデル**は、ビジネスドメイン内のデータ (ここでは books と authors) のサーバー側表現です。
- **ビュー**はプレゼンテーション層 (HTML) です。
- **ビューモデル**は、モデルを保持する JavaScript オブジェクトです。 ビューモデルは、UI のコード抽象化です。 HTML 表現に関する情報はありません。 代わりに、書籍&quot;の一覧 &quot;など、ビューの抽象的な機能を表します。

ビューは、ビューモデルにデータバインドされています。 ビューモデルの更新は、自動的にビューに反映されます。 ビューモデルでは、ボタンのクリックなど、ビューからイベントを取得することもできます。

![](part-6/_static/image1.png)

この方法を使用すると、コードを書き直さずにバインドを変更できるため、アプリのレイアウトと UI を簡単に変更できます。 たとえば、項目の一覧を `<ul>`として表示し、後でテーブルに変更することができます。

## <a name="add-the-knockout-library"></a>ノックアウトライブラリを追加する

Visual Studio で、 **[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択します。 次に、 **[パッケージ マネージャー コンソール]** を選択します。 [パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。

[!code-console[Main](part-6/samples/sample1.cmd)]

このコマンドは、[スクリプト] フォルダーにノックアウトファイルを追加します。

## <a name="create-the-view-model"></a>ビューモデルを作成する

App.config という名前の JavaScript ファイルを Scripts フォルダーに追加します。 (ソリューションエクスプローラーで、Scripts フォルダーを右クリックし、 **[追加]** 、 **[JavaScript ファイル]** の順に選択します)。次のコードを貼り付けます。

[!code-javascript[Main](part-6/samples/sample2.js)]

ノックアウトでは、`observable` クラスによってデータバインディングが有効になります。 観測可能な変更の内容が監視対象となると、データにバインドされたすべてのコントロールに対して、自身の更新が可能になるように通知されます。 (`observableArray` クラスは、*観測*可能な配列バージョンです)。まず、ビューモデルには2つの observable があります。

- `books` は、本の一覧を保持します。
- AJAX 呼び出しが失敗した場合、`error` にはエラーメッセージが表示されます。

`getAllBooks` メソッドは、AJAX 呼び出しを行って書籍の一覧を取得します。 次に、結果を `books` 配列にプッシュします。

`ko.applyBindings` メソッドは、ノックアウトライブラリの一部です。 ビューモデルをパラメーターとして受け取り、データバインディングを設定します。

## <a name="add-a-script-bundle"></a>スクリプトバンドルを追加する

バンドルは ASP.NET 4.5 の機能であり、複数のファイルを簡単に1つのファイルに結合したりバンドルしたりすることができます。 バンドルを使用すると、サーバーへの要求の数が減り、ページの読み込み時間が短縮されます。

File App\_Start/BundleConfig を開きます。 RegisterBundles メソッドに次のコードを追加します。

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> [前へ](part-5.md)
> [次へ](part-7.md)

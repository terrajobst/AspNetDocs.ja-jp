---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Web API と ASP.NET Web フォームの使用-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x 用の ASP.NET Forms アプリケーションに Web API を追加するためのコード手順を説明したチュートリアル
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448534"
---
# <a name="using-web-api-with-aspnet-web-forms"></a>ASP.NET Web フォームでの Web API の使用

[Mike Wasson](https://github.com/MikeWasson)

このチュートリアルでは、ASP.NET 4.x の従来の ASP.NET Web フォームアプリケーションに Web API を追加する手順について説明します。 

## <a name="overview"></a>概要

ASP.NET Web API は ASP.NET MVC でパッケージ化されていますが、従来の ASP.NET Web フォームアプリケーションに Web API を簡単に追加できます。

Web フォームアプリケーションで Web API を使用するには、次の2つの主要な手順を実行します。

- **ApiController**クラスから派生した Web API コントローラーを追加します。
- ルートテーブルを**アプリケーション\_の開始**メソッドに追加します。

## <a name="create-a-web-forms-project"></a>Web フォームプロジェクトを作成する

Visual Studio を起動し、**スタート**ページで **[新しいプロジェクト]** を選択します。 または、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。 **[ビジュアルC# ]** で **[Web]** を選択します。 プロジェクトテンプレートの一覧で、 **[ASP.NET Web フォームアプリケーション]** を選択します。 プロジェクトの名前を入力し、[ **OK]** をクリックします。

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>モデルとコントローラーを作成する

このチュートリアルでは、[はじめに](tutorial-your-first-web-api.md)チュートリアルと同じモデルとコントローラークラスを使用します。

まず、モデルクラスを追加します。 **ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[クラスの追加]** を選択します。 クラスに Product という名前を指定し、次の実装を追加します。

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

次に、Web API コントローラーをプロジェクトに追加します。*コントローラー*は、web API の HTTP 要求を処理するオブジェクトです。

**Solution Explorer** で、プロジェクト名を右クリックします。 **[新しい項目の追加]** を選択します。

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

**[インストールされたテンプレート]** で **[ C#ビジュアル]** を展開し、 **[Web]** を選択します。 次に、テンプレートの一覧から **[WEB API コントローラークラス]** を選択します。 コントローラーに "製品コントローラー" という名前を指定し、 **[追加]** をクリックします。

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

**新しい項目の追加**ウィザードでは、ProductsController.cs という名前のファイルが作成されます。 ウィザードに含まれているメソッドを削除し、次のメソッドを追加します。

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

このコントローラーのコードの詳細については、[はじめに](tutorial-your-first-web-api.md)チュートリアルを参照してください。

## <a name="add-routing-information"></a>ルーティング情報の追加

次に、URI ルートを追加します。これにより、フォーム &quot;/api/&quot; の Uri がコントローラーにルーティングされるようになります。

**ソリューションエクスプローラー**で、[global.asax] をダブルクリックして、分離コードファイル Global.asax.cs を開きます。 次の**using ステートメントを**追加します。

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

次に、 **Application\_Start**メソッドに次のコードを追加します。

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

ルーティングテーブルの詳細については、「 [ASP.NET Web API でのルーティング](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)」を参照してください。

## <a name="add-client-side-ajax"></a>クライアント側 AJAX の追加

これで、クライアントがアクセスできる web API を作成する必要があります。 次に、jQuery を使用して API を呼び出す HTML ページを追加します。

マスターページ (たとえば、「 *master*」) に `ID="HeadContent"`の `ContentPlaceHolder` が含まれていることを確認します。

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

Default.aspx ファイルを開きます。 次に示すように、メインコンテンツセクションにある定型テキストを置き換えます。

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

次に、`HeaderContent` セクションで jQuery ソースファイルへの参照を追加します。

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

注:**ソリューションエクスプローラー**からコードエディターウィンドウにファイルをドラッグアンドドロップすることで、スクリプト参照を簡単に追加できます。

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

JQuery script タグの下に、次のスクリプトブロックを追加します。

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

ドキュメントが読み込まれると、このスクリプトは、&quot;api/products&quot;に AJAX 要求を行います。 要求は、JSON 形式で製品の一覧を返します。 このスクリプトにより、製品情報が HTML テーブルに追加されます。

アプリケーションを実行すると、次のようになります。

![](using-web-api-with-aspnet-web-forms/_static/image5.png)

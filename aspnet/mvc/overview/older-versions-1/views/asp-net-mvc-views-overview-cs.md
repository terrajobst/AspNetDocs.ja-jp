---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
title: ASP.NET MVC ビューの概要C#() |Microsoft Docs
author: StephenWalther
description: ASP.NET MVC ビューとは何ですか。また、HTML ページとどのような違いがありますか。 このチュートリアルでは、Stephen Walther がビューを紹介し、その方法を示します。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 152ab1e5-aec2-4ea7-b8cc-27a24dd9acb8
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: b3f44aa9654a2a718381eaf9c856ca3e15ed1e27
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485854"
---
# <a name="aspnet-mvc-views-overview-c"></a>ASP.NET MVC ビュー概要 (C#)

[Stephen Walther](https://github.com/StephenWalther)

> ASP.NET MVC ビューとは何ですか。また、HTML ページとどのような違いがありますか。 このチュートリアルでは、Stephen Walther を使用してビューを作成し、ビュー内でビューデータと HTML ヘルパーを活用する方法を紹介します。

このチュートリアルの目的は、MVC ビューの ASP.NET、データの表示、および HTML ヘルパーの概要を説明することです。 このチュートリアルの最後に、新しいビューを作成する方法、コントローラーからビューにデータを渡す方法、HTML ヘルパーを使用してビューのコンテンツを生成する方法について理解しておく必要があります。

## <a name="understanding-views"></a>ビューについて

ASP.NET ページまたは Active Server ページの場合、ASP.NET MVC には、ページに直接対応するものは含まれません。 ASP.NET MVC アプリケーションでは、ブラウザーのアドレスバーに入力する URL 内のパスに対応するページがディスク上にありません。 ASP.NET MVC アプリケーションのページに最も近いのは、*ビュー*と呼ばれるものです。

ASP.NET MVC アプリケーションでは、入力方向のブラウザー要求がコントローラーアクションにマップされます。 コントローラーアクションはビューを返すことがあります。 ただし、コントローラーアクションでは、他の種類のアクション (別のコントローラーアクションへのリダイレクトなど) が実行される場合があります。

リスト1には、HomeController という名前のシンプルなコントローラーが含まれています。 HomeController は、Index () と Details () という2つのコントローラーアクションを公開します。

**リスト 1-HomeController.cs**

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample1.cs)]

ブラウザーのアドレスバーに次の URL を入力して、最初のアクション (Index () アクション) を呼び出すことができます。

/Home/Index

このアドレスをブラウザーに入力することで、2番目のアクションである Details () アクションを呼び出すことができます。

/Home/Details

Index () アクションを実行すると、ビューが返されます。 作成するほとんどの操作では、ビューが返されます。 ただし、アクションは他の種類のアクション結果を返すことができます。 たとえば、Details () アクションは、着信要求を Index () アクションにリダイレクトする RedirectToActionResult を返します。

Index () アクションには、次の1行のコードが含まれています。

View();

次のコード行では、web サーバー上の次のパスにあるビューが返されます。

\Views\Home\Index.aspx

ビューへのパスは、コントローラーの名前とコントローラーアクションの名前から推測されます。

必要に応じて、ビューを明示的に指定することもできます。 次のコード行では、Fred という名前のビューが返されます。

View( Fred );

このコード行を実行すると、次のパスからビューが返されます。

\Views\Home\Fred.aspx

> [!NOTE] 
> 
> ASP.NET MVC アプリケーションの単体テストを作成する予定の場合は、ビュー名について明示することをお勧めします。 これにより、単体テストを作成して、必要なビューがコントローラーアクションによって返されたことを確認できます。

## <a name="adding-content-to-a-view"></a>ビューへのコンテンツの追加

ビューは、スクリプトを含めることができる標準 (X) の HTML ドキュメントです。 スクリプトを使用して、動的なコンテンツをビューに追加します。

たとえば、リスト2のビューには、現在の日付と時刻が表示されます。

**リスト 2-\Views\Home\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample2.aspx)]

リスト2の HTML ページの本文には、次のスクリプトが含まれていることに注意してください。

&lt;% Response. 書き込み (DateTime. Now);%&gt;

スクリプトの区切り記号 &lt;% および%&gt; を使用して、スクリプトの先頭と末尾にマークを付けます。 このスクリプトは、「 C#」で記述されています。 ブラウザーにコンテンツを表示するために、Write () メソッドを呼び出して現在の日付と時刻を表示します。 スクリプトの区切り記号 &lt;% および%&gt; を使用して、1つまたは複数のステートメントを実行できます。

Response. Write () を呼び出すと、Microsoft から、Response () メソッドを呼び出すためのショートカットが提供されます。 リスト3のビューでは、応答の呼び出し () のショートカットとして、区切り記号 &lt;% = および%&gt; を使用します。

**リスト 3-Views\Home\Index2.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample3.aspx)]

任意の .NET 言語を使用して、動的なコンテンツをビューに生成できます。 通常は、Visual Basic .NET またはC#を使用して、コントローラーとビューを作成します。

## <a name="using-html-helpers-to-generate-view-content"></a>HTML ヘルパーを使用したビューコンテンツの生成

ビューにコンテンツを簡単に追加できるようにするために、 *HTML ヘルパー*と呼ばれるものを利用できます。 通常、HTML ヘルパーは、文字列を生成するメソッドです。 HTML ヘルパーを使用すると、テキストボックス、リンク、ドロップダウンリスト、リストボックスなどの標準の HTML 要素を生成できます。

たとえば、リスト4のビューでは、3つの HTML ヘルパー (BeginForm ()、TextBox ()、および Password () ヘルパー) を利用して、ログインフォームを生成します (図1を参照)。

**リスト 4--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample4.aspx)]

[[新しいプロジェクト] ダイアログボックスの ![](asp-net-mvc-views-overview-cs/_static/image1.jpg)](asp-net-mvc-views-overview-cs/_static/image1.png)

**図 01**: 標準のログインフォーム ([クリックすると、フルサイズの画像が表示](asp-net-mvc-views-overview-cs/_static/image2.png)される)

すべての HTML ヘルパーメソッドは、ビューの Html プロパティで呼び出されます。 たとえば、TextBox () メソッドを呼び出すことによってテキストボックスをレンダリングします。

Html の TextBox () ヘルパーと .Html () ヘルパーの両方を呼び出すときは、スクリプトの区切り記号 &lt;% = および%&gt; を使用することに注意してください。 これらのヘルパーは単に文字列を返します。 文字列をブラウザーに表示するには、Response. Write () を呼び出す必要があります。

HTML ヘルパーメソッドの使用は省略可能です。 記述する必要のある HTML およびスクリプトの量を減らすことで、作業が簡単になります。 リスト5のビューでは、HTML ヘルパーを使用せずに、リスト4のビューとまったく同じ形式がレンダリングされます。

**リスト 5--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample5.aspx)]

独自の HTML ヘルパーを作成することもできます。 たとえば、データベースレコードのセットを HTML テーブルに自動的に表示する GridView () ヘルパーメソッドを作成できます。 このトピックでは、**カスタム HTML ヘルパーの作成**について説明します。

## <a name="using-view-data-to-pass-data-to-a-view"></a>ビューデータを使用してビューにデータを渡す

ビューデータを使用して、コントローラーからビューにデータを渡します。 メールを通じて送信するパッケージのようなデータを表示してみてください。 コントローラーからビューに渡されるすべてのデータは、このパッケージを使用して送信する必要があります。 たとえば、リスト6のコントローラーは、データを表示するメッセージを追加します。

**リスト 6-ProductController.cs**

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample6.cs)]

Controller ViewData プロパティは、名前と値のペアのコレクションを表します。 リスト6では、Index () メソッドは、Hello World! という値を持つメッセージという名前のビューデータコレクションに項目を追加します。 Index () メソッドによってビューが返されると、ビューデータは自動的にビューに渡されます。

リスト7のビューでは、ビューデータからメッセージが取得され、ブラウザーに表示されます。

**リスト 7--\Views\Product\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample7.aspx)]

このビューでは、メッセージを表示するときに html. Encode () HTML ヘルパーメソッドが利用されていることに注意してください。 Html. Encode () HTML ヘルパーは、&lt; や &gt; などの特殊文字を、web ページに安全に表示できる文字にエンコードします。 ユーザーが web サイトに送信するコンテンツをレンダリングするときは常に、JavaScript インジェクション攻撃を防ぐためにコンテンツをエンコードする必要があります。

(ProductController に自分でメッセージを作成したので、実際にはメッセージをエンコードする必要はありません。 ただし、ビュー内のビューデータから取得したコンテンツを表示するときは、常に Html の Encode () メソッドを呼び出すことをお勧めします。

リスト7では、ビューデータを利用して、コントローラーからビューに単純な文字列メッセージを渡していました。 また、ビューデータを使用して、データベースレコードのコレクションなど、他の種類のデータをコントローラーからビューに渡すこともできます。 たとえば、Products データベーステーブルの内容をビューに表示する場合は、データベースレコードのコレクションをビューデータに渡すことになります。

また、厳密に型指定されたビューデータをコントローラーからビューに渡すこともできます。 このトピックでは、厳密に**型指定されたビューのデータとビューについ**て説明します。

## <a name="summary"></a>まとめ

このチュートリアルでは、MVC ビューの ASP.NET、データの表示、および HTML ヘルパーについて簡単に説明しました。 最初のセクションでは、新しいビューをプロジェクトに追加する方法について学習しました。 特定のコントローラーからビューを呼び出すには、適切なフォルダーにビューを追加する必要があることを学びました。 次に、HTML ヘルパーのトピックについて説明しました。 HTML ヘルパーを使用して、標準の HTML コンテンツを簡単に生成する方法について学習しました。 最後に、ビューデータを利用して、コントローラーからビューにデータを渡す方法について学習しました。

> [!div class="step-by-step"]
> [Next](creating-custom-html-helpers-cs.md)

---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: HTML エディターコントロールを使用操作方法には (C#) |Microsoft Docs
author: microsoft
description: HTMLEditor は、ツールバーのボタンを使用して HTML コンテンツを簡単に作成および編集できるようにする ASP.NET AJAX コントロールです。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: cb7d75b59b1361abeb6d3c38ad6e42e34d6e3f7b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78466606"
---
# <a name="how-do-i-use-the-html-editor-control-c"></a>HTML エディターコントロールを使用操作方法には (C#)

[Microsoft](https://github.com/microsoft)

> HTMLEditor は、ツールバーのボタンを使用して HTML コンテンツを簡単に作成および編集できるようにする ASP.NET AJAX コントロールです。

このチュートリアルの目的は、AJAX Control Toolkit に含まれている HTML エディターコントロールの概要を説明することです。 HTML エディターには、フォントサイズの変更、フォントの選択、背景色の変更、前景色の変更、リンクの追加、イメージの追加、テキストの配置の変更、および切り取り、コピー、貼り付けの操作 (図1を参照) を行うためのオプションが含まれています。

[HTML エディターの ![](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)

**図 01**: HTML エディター ([クリックすると、フルサイズの画像が表示](how-do-i-use-the-html-editor-control-cs/_static/image2.png)されます)

HTML エディターを使用すると、デザインモードでコンテンツを入力したり、HTML を直接入力したりできます。 HTML コンテンツをプレビューするオプションも用意されています (図2を参照)。

[![デザイン、HTML、およびプレビューボタン](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)

**図 02**: デザイン、HTML、およびプレビューのボタン ([クリックしてフルサイズのイメージを表示](how-do-i-use-the-html-editor-control-cs/_static/image4.png))

このチュートリアルでは、HTML エディターを表示する方法、HTML エディターに表示されるツールバーボタンをカスタマイズする方法、クロスサイトスクリプト攻撃を回避する方法について説明します。

## <a name="displaying-the-html-editor"></a>HTML エディターを表示する

ASP.NET ページで HTML エディターを使用するには、まず、ScriptManager コントロールをページに追加する必要があります。 ScriptManager コントロールは、Visual Studio/Visual Web Developer Express ツールボックスの [AJAX 拡張] タブの下にあります。

ScriptManager コントロールは、ページ上の他のコントロールの前に、ページの一番上に配置する必要があります。 たとえば、開いているサーバー側の &lt;フォーム&gt; タグのすぐ下に配置できます。

HTML エディターコントロールは、他の AJAX コントロールツールキットコントロールと共にツールボックスに配置されます。 これは、エディターコントロールと呼ばれます (図3を参照)。

[HTML エディターコントロールの ![](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)

**図 03**: HTML エディターコントロール ([クリックしてフルサイズのイメージを表示する](how-do-i-use-the-html-editor-control-cs/_static/image6.png))

HTML エディターをページにドラッグした後は、プロパティシートでそのプロパティを設定できます。 たとえば、通常は Width プロパティと Height プロパティを設定します。 リスト1には、HTML エディターを含む ASP.NET ページのソースが含まれています。

**リスト 1-SimpleEditor .aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

リスト1のページには、HTML エディターコントロール、ボタンコントロール、およびリテラルコントロールが含まれています。 このボタンをクリックすると、HTML エディターの内容がリテラルコントロールに表示されます (図4を参照)。

[HTML エディターを使用してフォームを送信 ![には](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)

**図 04**: HTML エディターを使用してフォームを送信[する (クリックすると、フルサイズの画像が表示](how-do-i-use-the-html-editor-control-cs/_static/image8.png)されます)

Html エディターのコンテンツプロパティは、html エディターに入力された HTML コンテンツを取得するために使用されます。 この HTML コンテンツには JavaScript を含めることができることに注意してください。 次のセクションでは、JavaScript インジェクション攻撃を防ぐ方法について説明します。

## <a name="customizing-the-html-editor-toolbar"></a>HTML エディターツールバーのカスタマイズ

エディターに表示されるボタンを正確にカスタマイズできます。 たとえば、ユーザーが html エディターを HTML モードに切り替えられないようにするには、[HTML] タブを削除します。 または、[フォントサイズ] ドロップダウンリストを削除して、ユーザーがフォーラムのメッセージの投稿で極端に大きいテキストを作成できないようにすることもできます (図5を参照)。

[カスタマイズされた HTML エディターの ![](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)

**図 05**: カスタマイズされた HTML エディター ([クリックしてフルサイズのイメージを表示する](how-do-i-use-the-html-editor-control-cs/_static/image10.png))

ツールバーのボタンをカスタマイズするには、基本エディタークラスから新しい HTML エディターを派生させます。 たとえば、リスト2のカスタムエディターには、太字と斜体のツールバーボタンのみが含まれています。 その他のツールバーボタンはすべて削除されました。 さらに、エディターの下部から [HTML] タブが削除されています (ただし、[デザイン] タブと [プレビュー] タブはまだ表示されています)。

**リスト 2-アプリ\_Code/customeditorcs**

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

クラスが自動的にコンパイルされるように、リスト2のクラスをアプリ\_コードフォルダーに追加する必要があります。 アプリ\_コードフォルダーが web サイトに存在しない場合は、単にフォルダーを追加できます。

カスタムエディターを作成した後は、通常の HTML エディターを追加するのと同じ方法で、ASP.NET ページに追加できます (リスト3を参照)。

**リスト 3-ShowCustomEditor .aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>クロスサイトスクリプティング (XSS) 攻撃の回避

ユーザーからの入力を受け入れ、web サイトでその入力を再表示すると、web サイトがクロスサイトスクリプティング (XSS) 攻撃につながる可能性があります。 理論的には、悪意のあるハッカーが、入力が再提示されたときに実行される JavaScript コードを送信する可能性があります。 JavaScript を使用すると、ユーザーのパスワードやその他の機密情報を盗むことができます。

通常、web ページに表示する前に、ユーザーから取得した入力を HTML エンコードすることによって、XSS 攻撃を防ぐことができます。 ただし、html エディターの出力を html エンコードすると、スクリプト&gt; のタグ &lt;エンコードされるだけでなく、すべての HTML タグもエンコードされます。 つまり、フォントの種類、フォントサイズ、背景色など、すべての書式設定が失われる可能性があります。

パスワード、クレジットカード番号、社会保障番号など、ユーザーから機密情報を収集する場合は、HTML エディターを使用してユーザーから取得したエンコードされていないコンテンツを表示しないようにする必要があります。 Html エディターは、html コンテンツを再表示しない場合、または HTML コンテンツが信頼できるパーティによって web サイトに送信されている場合にのみ使用してください。

たとえば、ブログアプリケーションを作成する場合を考えてみましょう。 このような状況では、ブログの投稿を作成するときに HTML エディターを使用するのが理にかなっています。 ブログ投稿を送信するのは自分だけで、おそらく悪意のある JavaScript を送信することはできません。 ただし、匿名ユーザーにコメントの投稿を許可する場合、HTML エディターを使用することは意味がありません。 パスワードなどの機密情報をユーザーが送信する状況に特に注意する必要があります。 悪意のあるユーザーが、パスワードを盗むための適切な JavaScript を含むコメントを投稿する可能性があります。

## <a name="summary"></a>まとめ

このチュートリアルでは、AJAX Control Toolkit に含まれている HTML エディターコントロールの概要を簡単に説明しました。 HTML エディターを使用して、ユーザーからのリッチコンテンツを受け入れ、コンテンツをサーバーに送信する方法を学習しました。 また、HTML エディターによって表示されるツールバーボタンをカスタマイズする方法についても説明しました。 最後に、HTML エディターを使用して悪意のある入力を受け入れるときのクロスサイトスクリプト攻撃を回避する方法を学習しました。

> [!div class="step-by-step"]
> [Next](how-do-i-use-the-html-editor-control-vb.md)

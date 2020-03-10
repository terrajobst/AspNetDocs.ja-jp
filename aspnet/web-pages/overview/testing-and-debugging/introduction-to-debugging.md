---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: ASP.NET Web ページ (Razor) サイトのデバッグの概要 |Microsoft Docs
author: Rick-Anderson
description: デバッグは、コードページ内のエラーを検出して修正するプロセスです。 この章では、デバッグと率のために使用できるツールと手法について説明します。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: ae7d871e56326610c043dc20fe6e0919e1b4ac89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506458"
---
# <a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a>デバッグ ASP.NET Web ページ (Razor) サイトの概要

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ASP.NET Web ページ (Razor) web サイトでページをデバッグするさまざまな方法について説明します。 デバッグは、コードページ内のエラーを検出して修正するプロセスです。
>
> **学習内容:**
>
> - ページの分析とデバッグに役立つ情報を表示する方法について説明します。
> - Visual Studio でデバッグツールを使用する方法について説明します。
>
>
> この記事で導入された ASP.NET 機能を次に示します。
>
> - `ServerInfo` ヘルパー。
> - `ObjectInfo` ヘルパー。
>
>
> ## <a name="software-versions"></a>ソフトウェアのバージョン
>
>
> - ASP.NET Web ページ (Razor) 3
> - Visual Studio 2013
>
>
> このチュートリアルは ASP.NET Web ページ2でも動作します。 WebMatrix 3 を使用することはできますが、統合デバッガーはサポートされていません。

コードのエラーや問題をトラブルシューティングするための重要な側面は、これらの問題を最初に回避することです。 これを行うには、エラーの原因となる可能性があるコードのセクションを `try/catch` ブロックに配置します。 詳細については、「 [Razor 構文を使用した ASP.NET Web プログラミングの概要](https://go.microsoft.com/fwlink/?LinkId=202890)」のエラー処理に関するセクションを参照してください。

`ServerInfo` helper は、ページをホストする web サーバー環境に関する情報の概要を提供する診断ツールです。 また、ブラウザーがページを要求したときに送信される HTTP 要求情報も表示されます。 `ServerInfo` ヘルパーには、現在のユーザー id、要求を行ったブラウザーの種類などが表示されます。 この種の情報は、一般的な問題のトラブルシューティングに役立ちます。

1. *Serverinfo. cshtml*という名前の新しい web ページを作成します。
2. ページの最後で、終了 `</body>` タグの直前に `@ServerInfo.GetHtml()`を追加します。

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    `ServerInfo` コードは、ページの任意の場所に追加できます。 ただし、末尾に追加すると、他のページコンテンツとは別に出力が保持されるため、読みやすくなります。

    > [!NOTE]
    >
    > **重要**Web ページを実稼働サーバーに移動する前に、web ページから診断コードを削除する必要があります。 これは、`ServerInfo` ヘルパーに適用されます。また、この記事では、ページへのコードの追加を含むその他の診断手法にも当てはまります。 この種の情報が悪意のあるユーザーにとって役立つ可能性があるため、web サイトの訪問者にサーバー名、ユーザー名、サーバー上のパスなどの情報が表示されないようにする必要があります。
3. ページを保存し、ブラウザーで実行します。

    ![デバッグ-1](introduction-to-debugging/_static/image1.jpg)

    `ServerInfo` ヘルパーは、次の4つのテーブルの情報をページに表示します。

   - サーバーの構成。 このセクションでは、ホストしている web サーバーに関する情報を提供します。これには、コンピューター名、実行している ASP.NET のバージョン、ドメイン名、サーバー時間などが含まれます。
   - ASP.NET サーバー変数。 このセクションでは、多くの HTTP プロトコルの詳細 (HTTP 変数と呼ばれます) と、各 web ページ要求に含まれる値について詳しく説明します。
   - HTTP ランタイム情報。 このセクションでは、web ページが実行されている Microsoft .NET Framework のバージョン、パス、キャッシュに関する詳細などについて詳しく説明します。 ( [Razor 構文を使用した ASP.NET Web プログラミングの概要につい](https://go.microsoft.com/fwlink/?LinkId=202890)て学習したように、Razor 構文を使用する ASP.NET Web ページは、Microsoft の ASP.NET Web サーバーテクノロジを基盤としています。これは、.NET Framework と呼ばれる広範なソフトウェア開発ライブラリに基づいて構築されています)。
   - 環境変数。 このセクションでは、web サーバー上のすべてのローカル環境変数とその値の一覧を示します。

     すべてのサーバーと要求情報の詳細については、この記事では説明しませんが、`ServerInfo` ヘルパーが多くの診断情報を返すことを確認できます。 `ServerInfo` 返される値の詳細については、MSDN web サイトの Microsoft TechNet web サイトおよび[IIS サーバー変数](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)の「認識された[環境変数](https://technet.microsoft.com/library/dd560744(WS.10).aspx)」を参照してください。

## <a name="embedding-output-expressions-to-display-page-values"></a>ページ値を表示するための出力式の埋め込み

コード内で何が起こっているかを確認するもう1つの方法は、出力式をページに埋め込むことです。 ご存じのように、`@myVariable` や `@(subTotal * 12)` などの値をページに追加して、変数の値を直接出力できます。 デバッグ用には、コード内の戦略的なポイントでこれらの出力式を配置できます。 これにより、ページの実行時に、キー変数の値または計算結果を確認できます。 デバッグが完了したら、式を削除するか、コメントアウトすることができます。この手順は、ページのデバッグを支援するために、埋め込み式を使用する一般的な方法を示しています。

1. *Outputexpression. cshtml*という名前の新しい WebMatrix ページを作成します。
2. ページの内容を次の内容に置き換えます。

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    この例では、`switch` ステートメントを使用して `weekday` 変数の値を確認し、その曜日に応じて別の出力メッセージを表示します。 この例では、最初のコードブロック内の `if` ブロックは、現在の曜日の値に1日を加算することによって、曜日を任意に変更します。 これは、図を示すために導入されたエラーです。
3. ページを保存し、ブラウザーで実行します。

    このページには、曜日が正しくないことを示したメッセージが表示されます。 曜日にかかわらず、1日後にメッセージが表示されます。 この例では、メッセージが無効になっている理由 (コードが意図的に誤った日付値を設定しているため) がわかっていますが、実際には、コード内のどこが間違っているかを把握するのが難しい場合があります。 デバッグするには、`weekday`などの主要なオブジェクトと変数の値に何が起こっているかを調べる必要があります。
4. コード内のコメントに示されている2つの場所に示されているように `@weekday` を挿入して、出力式を追加します。 これらの出力式では、コード実行のその時点の変数の値が表示されます。

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. ブラウザーでページを保存して実行します。

    このページには、最初に週の実際の曜日、次に1日後に更新された曜日が表示されます。その後、`switch` ステートメントから結果として得られるメッセージが表示されます。 HTML `<p>` タグを出力に追加していないため、2つの変数式 (`@weekday`) からの出力には、その日の間にスペースがありません。式はテスト専用です。

    ![デバッグ-2](introduction-to-debugging/_static/image2.jpg)

    ここで、エラーの場所を確認できます。 コードに最初に `weekday` 変数を表示すると、正しい日が表示されます。 2回目に表示すると、コードの `if` ブロックの後に、その日が1つずつオフになります。 これは、weekday 変数の1番目と2番目の外観の間に何らかの問題が発生したことを把握しています。 これが実際のバグである場合、この種のアプローチは、問題の原因となっているコードの場所を絞り込むのに役立ちます。
6. 追加した2つの出力式を削除し、曜日を変更するコードを削除して、ページ内のコードを修正します。 コードの残りの完全なブロックは、次の例のようになります。

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. ブラウザーでページを実行します。 今回は、実際の曜日に対して正しいメッセージが表示されます。

## <a name="using-the-objectinfo-helper-to-display-object-values"></a>ObjectInfo ヘルパーを使用したオブジェクト値の表示

`ObjectInfo` ヘルパーには、渡された各オブジェクトの型と値が表示されます。 これを使用すると、前の例の出力式の場合と同様に、コード内の変数とオブジェクトの値を表示できます。さらに、オブジェクトに関するデータ型情報を確認することもできます。

1. 先ほど作成した*Outputexpression. cshtml*という名前のファイルを開きます。
2. ページ内のすべてのコードを次のコードブロックに置き換えます。

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. ブラウザーでページを保存して実行します。

    ![デバッグ-4](introduction-to-debugging/_static/image3.jpg)

    この例では、`ObjectInfo` ヘルパーは次の2つの項目を表示します。

   - 型。 最初の変数の場合、型は `DayOfWeek`になります。 2番目の変数の場合、型は `String`になります。
   - 値。 この場合、ページにあいさつ変数の値が既に表示されているので、変数を `ObjectInfo`に渡すと、値が再び表示されます。

     より複雑なオブジェクトの場合、`ObjectInfo` ヘルパーは、基本的&#8212;により多くの情報を表示できます。また、オブジェクトのすべてのプロパティの型と値を表示できます。

## <a name="using-debugging-tools-in-visual-studio"></a>Visual Studio でのデバッグツールの使用

より包括的なデバッグエクスペリエンスを実現するには、 [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)を使用します。 Visual Studio では、検査する行のコードにブレークポイントを設定できます。

![ブレークポイントの設定](introduction-to-debugging/_static/image1.png)

Web サイトをテストすると、実行中のコードがブレークポイントで停止します。

![リーチブレークポイント](introduction-to-debugging/_static/image2.png)

変数の現在の値を確認し、コードを1行ずつステップ実行することができます。

![値の表示](introduction-to-debugging/_static/image3.png)

Visual Studio で統合デバッガーを使用して ASP.NET Razor ページをデバッグする方法の詳細については、「 [Visual Studio を使用したプログラミング ASP.NET Web ページ (Razor)](https://go.microsoft.com/fwlink/?LinkId=205854)」を参照してください。

## <a name="additional-resources"></a>その他のリソース

- [Visual Studio を使用したプログラミング ASP.NET Web ページ (Razor)](https://go.microsoft.com/fwlink/?LinkId=205854)
- [IIS サーバー変数](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)(MSDN)
- 認識された[環境変数](https://technet.microsoft.com/library/dd560744(WS.10).aspx)(TechNet)

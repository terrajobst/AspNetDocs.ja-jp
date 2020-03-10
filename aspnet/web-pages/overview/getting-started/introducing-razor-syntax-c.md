---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Razor 構文 (C#) を使用して ASP.NET Web プログラミングの概要 |Microsoft Docs
author: Rick-Anderson
description: この章では、Razor 構文を使用した ASP.NET Web ページによるプログラミングの概要について説明します。 ASP.NET は、動的な web pa を実行するための Microsoft のテクノロジです...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521206"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a>Razor 構文 (C#) を使用して ASP.NET Web プログラミングの概要

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、Razor 構文を使ったASP.NET Web ページにおけるプログラミングの概要を解説します。 ASP.NETは、Webサーバーで動的な Web ページを運用するためのマイクロソフトの技術です。 この記事を使用して C# のプログラミング言語での焦点を当てます。
> 
> **学習内容**:
> 
> - Razor構文を使ったASP.NET Webページのプログラミングをはじめるための上位8つのプログラミング Tips
> - 必要とする基本的なプログラミング概念
> - ASP.NETサーバーコードとRazor構文に関する全体像
>   
> 
> ## <a name="software-versions"></a>ソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 3
>   
> 
> このチュートリアルは ASP.NET Web ページ2でも動作します。

## <a name="the-top-8-programming-tips"></a>8 つのプログラミング Tips

このセクションでは、Razor 構文を使用して ASP.NET サーバーコードの記述を開始するときに理解しておく必要があるいくつかのヒントを示します。

> [!NOTE]
> Razor 構文は C# プログラミング言語に基づいており、ASP.NET Web Pages を最もよく使用されている言語です。 ただし、Razor 構文は Visual Basic の言語をサポートしています。また、Visual Basic でも実行できます。 詳細については、付録[Visual Basic の言語と構文](https://go.microsoft.com/fwlink/?LinkId=202908)を参照してください。

これらのプログラミング手法のほとんどの詳細については、この記事の後半で説明します。

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. @ 文字を使用してコードをページに追加します。

`@` 文字は、インライン式、単一のステートメントブロック、および複数ステートメントのブロックを開始します。

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

ブラウザーでページを実行すると、次のようなステートメントが表示されます。

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> **HTML エンコード**
> 
> 前の例のように `@` 文字を使用してページにコンテンツを表示すると、ASP.NET は出力を HTML エンコードします。 これにより、予約された HTML 文字 (`<`、`>` や `&`など) が、HTML タグまたはエンティティとして解釈されるのではなく、web ページに文字として表示されるようにするコードに置き換えられます。 HTML エンコードを使用しないと、サーバーコードからの出力が正しく表示されず、ページがセキュリティ上のリスクにさらされる可能性があります。
> 
> タグをマークアップとしてレンダリングする HTML マークアップを出力することが目的である場合 (たとえば、段落や `<em></em>` テキストを強調するための `<p></p>`)、この記事で後述する「[コードブロック内のテキスト、マークアップ、およびコードの結合](#BM_CombiningTextMarkupAndCode)」セクションを参照してください。
> 
> HTML エンコードの詳細については、「[フォームの操作](https://go.microsoft.com/fwlink/?LinkId=202892)」を参照してください。

### <a name="2-you-enclose-code-blocks-in-braces"></a>2. コードブロックを中かっこで囲みます

*コードブロック*には、1つまたは複数のコードステートメントが含まれ、中かっこで囲まれています。

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

結果がブラウザーに表示されます。

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a>3. ブロック内では、各コードステートメントをセミコロンで終了します。

コードブロックの中では、それぞれの完結するコード文はセミコロンで終わらせます。 インライン式は、セミコロンで終わりません。

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a>4. 変数を使用して値を格納する

文字列、数値、日付など、*変数*に値を格納することができます。新しい変数を作成するには、`var` キーワードを使用します。 `@`を使用して、変数の値をページに直接挿入できます。

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

結果がブラウザーに表示されます。

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. リテラル文字列値を二重引用符で囲みます。

*文字列*は、テキストとして扱われる文字のシーケンスです。 文字列を指定するには、ダブル クォーテーション記号で囲みます。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

表示する文字列に円記号 (`\`) または二重引用符 (`"`) が含まれている場合は、`@` 演算子を先頭に付けた*逐語的文字列リテラル*を使用します。 (でC#は、逐語的文字列リテラルを使用しない限り、\ 文字は特別な意味を持ちます)。

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

二重引用符を埋め込むには、逐語的文字列リテラルを使用して、引用符を繰り返します。

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

ページで両方の例を使用した結果を次に示します。

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> `@` 文字が、でC#逐語的文字列リテラルをマークし、ASP.NET ページのコードをマークするために使用されていることに注意してください。

### <a name="6-code-is-case-sensitive"></a>6. コードで大文字と小文字を区別する

でC#は、キーワード (`var`、`true`、`if`など) と変数名は大文字と小文字が区別されます。 次のコード行では、`lastName` と `LastName.` の2つの異なる変数を作成しています。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

変数を `var lastName = "Smith";` として宣言し、その変数を `@LastName`としてページ内で参照しようとすると、`"Smith"`ではなく `"Jones"` 値が取得されます。

> [!NOTE]
> Visual Basic では、キーワードと変数の大文字と小文字は区別され*ません*。

### <a name="7-much-of-your-coding-involves-objects"></a>7. コーディングの多くがオブジェクトを含む

*オブジェクト*は、ページ、テキストボックス、ファイル、 &#8212;画像、web 要求、電子メールメッセージ、顧客レコード (データベース行) などを使用してプログラミングできることを表します。オブジェクトには、その特性を説明するプロパティがあります。 &#8212;また、テキストボックスオブジェクトの読み取りまたは変更には、`Text` プロパティがあります。また、要求オブジェクトには `Url` プロパティがあり、電子メールメッセージには `From` プロパティがあり、顧客オブジェクトには `FirstName` プロパティがあります。 オブジェクトには、実行できる&quot; &quot;動詞であるメソッドもあります。 例としては、ファイルオブジェクトの `Save` メソッド、イメージオブジェクトの `Rotate` メソッド、電子メールオブジェクトの `Send` メソッドなどがあります。

多くの場合、`Request` オブジェクトを使用します。このオブジェクトは、ページ上のテキストボックス (フォームフィールド) の値、要求を行ったブラウザーの種類、ページの URL、ユーザー id などの情報を提供します。次の例は、`Request` オブジェクトのプロパティにアクセスする方法と、`Request` オブジェクトの `MapPath` メソッドを呼び出す方法を示しています。これにより、サーバー上のページの絶対パスが得られます。

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

結果がブラウザーに表示されます。

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. 決定を行うコードを記述できます。

動的 web ページの重要な機能は、条件に基づいて何を行うかを決定できることです。 これを行う最も一般的な方法は、`if` ステートメント (および省略可能な `else` ステートメント) を使用することです。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

ステートメント `if(IsPost)` は、`if(IsPost == true)`を簡単に記述する方法です。 `if` ステートメントと共に、条件のテスト、コードブロックの繰り返しなど、さまざまな方法があります。これについては、この記事の後半で説明します。

ブラウザーに表示される結果 ( **[送信]** をクリックした後):

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a>HTTP GET メソッドと POST メソッド、および IsPost プロパティ
> 
> Web ページ (HTTP) に使用されるプロトコルでは、サーバーへの要求を行うために使用されるメソッド (動詞) の数が制限されています。 最も一般的な2つの方法は、ページの読み取りに使用される GET と、ページの送信に使用される POST です。 一般に、ユーザーが初めてページを要求したときは、GET を使用してページが要求されます。 ユーザーがフォームに入力し、[送信] ボタンをクリックすると、ブラウザーはサーバーに POST 要求を行います。
> 
> Web プログラミングでは、ページの処理方法を把握できるように、ページが GET として要求されているのか、または投稿として要求されているのかを知ることが役に立つことがよくあります。 ASP.NET Web ページでは、`IsPost` プロパティを使用して、要求が GET または POST のどちらであるかを確認できます。 要求が POST の場合、`IsPost` プロパティは true を返し、フォームのテキストボックスの値を読み取るなどの操作を実行できます。 多くの例では、`IsPost`の値に応じて、ページを異なる方法で処理する方法を示しています。

## <a name="a-simple-code-example"></a>単純なコード例

この手順では、基本的なプログラミング手法を示すページを作成する方法について説明します。 この例では、ユーザーが2つの数値を入力できるページを作成し、それらを追加して結果を表示します。

1. エディターで、新しいファイルを作成し、「 *Addnumbers. cshtml*」という名前を付けます。
2. 次のコードとマークアップをページにコピーして、ページに既に存在するものを置き換えます。  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    ここでは、次の点に注意してください。

    - `@` 文字は、ページ内の最初のコードブロックを開始し、ページの下部付近に埋め込まれている `totalMessage` 変数の前にあります。
    - ページの上部にあるブロックは、中かっこで囲まれています。
    - 先頭のブロックでは、すべての行の末尾にセミコロンが付きます。
    - 変数 `total`、`num1`、`num2`、および `totalMessage` には、いくつかの数値と文字列が格納されます。
    - `totalMessage` 変数に代入されたリテラル文字列値は、二重引用符で囲まれています。
    - コードでは大文字と小文字が区別されるため、`totalMessage` 変数がページの下部付近で使用されている場合、その名前は一番上の変数と正確に一致している必要があります。
    - 式 `num1.AsInt() + num2.AsInt()` は、オブジェクトとメソッドを操作する方法を示しています。 各変数の `AsInt` メソッドは、ユーザーが入力した文字列を数値 (整数) に変換して、算術演算を実行できるようにします。
    - `<form>` タグには、`method="post"` 属性が含まれています。 これにより、ユーザーが **[追加]** をクリックしたときに、HTTP POST メソッドを使用してページがサーバーに送信されることを指定します。 ページが送信されると、`if(IsPost)` テストが true と評価され、条件コードが実行されて、数値を加算した結果が表示されます。
3. ページを保存し、ブラウザーで実行します。 (実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。2つの整数を入力し、 **[追加]** ボタンをクリックします。 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a>基本的なプログラミングの概念

この記事では、ASP.NET web プログラミングの概要について説明します。 これは完全な検査ではなく、最も頻繁に使用するプログラミングの概念を簡単に説明します。 それでも、ASP.NET Web ページの使用を開始するために必要なほとんどすべてのことが説明されています。

しかし、まず少し技術的な背景です。

### <a name="the-razor-syntax-server-code-and-aspnet"></a>Razor 構文、サーバーコード、および ASP.NET

Razor 構文は、web ページにサーバーベースのコードを埋め込むための単純なプログラミング構文です。 Razor 構文を使用する web ページでは、クライアントコンテンツとサーバーコードという2種類のコンテンツがあります。 クライアントコンテンツは、HTML マークアップ (要素)、CSS などのスタイル情報、JavaScript などのクライアントスクリプト、プレーンテキストなど、web ページで使用するものです。

Razor 構文を使用すると、このクライアントコンテンツにサーバーコードを追加できます。 ページにサーバーコードがある場合、サーバーはそのコードを最初に実行してから、ブラウザーにページを送信します。 サーバー上で実行することにより、このコードでは、サーバーベースのデータベースへのアクセスなど、クライアントコンテンツのみを使用することにより複雑なタスクを実行できます。 ほとんどの場合、サーバーコードは動的にクライアント&#8212;コンテンツを作成できます。これにより、HTML マークアップやその他のコンテンツをその場で生成し、そのページに含まれる静的な html と共にブラウザーに送信できます。 ブラウザーの観点からは、サーバーコードによって生成されるクライアントコンテンツは、他のクライアントコンテンツと同じではありません。 既に説明したように、必要なサーバーコードは非常に単純です。

Razor 構文を含む web ページの ASP.NET には、特殊なファイル拡張子 (*cshtml*または*vbhtml*) があります。 サーバーはこれらの拡張機能を認識し、Razor 構文でマークされているコードを実行してから、ブラウザーにページを送信します。

### <a name="where-does-aspnet-fit-in"></a>ASP.NET はどこにありますか。

Razor 構文は、ASP.NET と呼ばれる Microsoft のテクノロジに基づいています。このテクノロジは、Microsoft .NET フレームワークに基づいています。 The.NET Framework は、ほぼすべての種類のコンピューターアプリケーションを開発するための、Microsoft の大きな包括的なプログラミングフレームワークです。 ASP.NET は、web アプリケーションの作成専用に設計された .NET Framework の一部です。 開発者は ASP.NET を使用して、世界中の最大規模で最大規模の web サイトを作成しました。 (サイトの URL の一部としてファイル名拡張子 *.aspx*が表示されると、サイトが ASP.NET を使用して書き込まれたことがわかります)。

Razor 構文は、ASP.NET のすべての機能を提供しますが、初心者であり、専門家の方が生産性を向上させる簡単な構文を使用します。 この構文は簡単に使用できますが、ASP.NET と .NET Framework との家族の関係は、web サイトがより高度なものになったときに、より大きなフレームワークの機能を利用できることを意味します。

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> **クラスとインスタンス**
> 
> ASP.NET サーバーコードは、クラスの概念に基づいて構築されたオブジェクトを使用します。 クラスは、オブジェクトの定義またはテンプレートです。 たとえば、アプリケーションには、顧客オブジェクトが必要とするプロパティとメソッドを定義する `Customer` クラスが含まれている場合があります。
> 
> アプリケーションが実際の顧客情報を処理する必要がある場合は、customer オブジェクトのインスタンス *(または*インスタンス) を作成します。 個々の顧客は、`Customer` クラスの個別のインスタンスです。 すべてのインスタンスは同じプロパティとメソッドをサポートしますが、各顧客オブジェクトが一意であるため、各インスタンスのプロパティ値は通常異なります。 1つの customer オブジェクトでは、`LastName` プロパティが "Smith" である場合があります。別の customer オブジェクトでは、`LastName` プロパティが "Jones" である場合があります。
> 
> 同様に、サイト内の個々の web ページは、`Page` クラスのインスタンスである `Page` オブジェクトです。 ページ上のボタンは、`Button` クラスのインスタンスである `Button` のオブジェクトです。 各インスタンスには独自の特性がありますが、これらはすべて、オブジェクトのクラス定義で指定されている内容に基づいています。

## <a name="basic-syntax"></a>基本構文

前に、ASP.NET Web ページページを作成する方法の基本的な例と、HTML マークアップにサーバーコードを追加する方法について説明しました。 ここでは、プログラミング言語の規則である Razor 構文&#8212;を使用して、ASP.NET サーバーコードを記述する方法の基本について説明します。

(特に C、C++、C#、Visual Basic、または JavaScript を使用した) 場合のプログラミング経験豊富な場合は、ここで読んだの多くが使い慣れたになります。 場合によっては、ファイル内のマークアップにサーバーコードを追加する方法についてのみ理解しておく必要が*あります。*

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a>コードブロック内のテキスト、マークアップ、およびコードの結合

サーバーコードブロックでは、多くの場合、テキストまたはマークアップ (またはその両方) をページに出力します。 サーバーコードブロックにコード以外のテキストが含まれていて、そのテキストをそのように表示する必要がある場合、ASP.NET はそのテキストをコードから区別できる必要があります。 これにはいくつかの方法があります。

- テキストを `<p></p>` や `<em></em>`などの HTML 要素で囲みます。   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    HTML 要素には、テキスト、追加の HTML 要素、およびサーバーコード式を含めることができます。 ASP.NET が HTML の開始タグ (`<p>`など) を参照すると、要素とそのコンテンツを含むすべてのものがブラウザーに表示されます。これにより、サーバーコード式が解決されます。
- `@:` 演算子または `<text>` 要素を使用します。 `@:` は、プレーンテキストまたは一致しない HTML タグを含む1行のコンテンツを出力します。`<text>` 要素は、出力に複数の行を囲みます。 これらのオプションは、HTML 要素を出力の一部としてレンダリングしない場合に便利です。  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    複数行のテキストまたは一致しない HTML タグを出力する場合は、各行の前に `@:`を挿入するか、`<text>` 要素でその行を囲むことができます。 `@:` 演算子と同様、`<text>` タグはテキストコンテンツを識別するために ASP.NET によって使用され、ページ出力には表示されません。

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    最初の例では、前の例を繰り返しますが、1組の `<text>` タグを使用して、レンダリングするテキストを囲みます。 2番目の例では、`<text>` タグと `</text>` タグは3つの行を囲みます。これらの行には、非包含テキストと一致しない HTML タグ (`<br />`) と、サーバーコードおよび一致した HTML タグがあります。 繰り返しになりますが、各行の前に `@:` 演算子を使用することもできます。どちらの方法でも動作します。

    > [!NOTE]
    > HTML 要素を使用して、このセクション&#8212;に示すようにテキストを出力する場合、`@:` 演算子、 &#8212;または `<text>` 要素 ASP.NET は、出力を html エンコードしません。 (前述のように、ASP.NET は、このセクションに記載されている特殊なケースを除き、`@`の前にあるサーバーコード式とサーバーコードブロックの出力をエンコードします)。

### <a name="whitespace"></a>空白文字

ステートメント内の余分なスペース (および文字列リテラルの外部) は、ステートメントに影響しません。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

ステートメント内の改行は、ステートメントには影響しません。また、ステートメントをラップして読みやすくすることもできます。 次の 2 つのステートメントでは同じ結果が得られます。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

ただし、文字列リテラルの途中では、行をラップすることはできません。 次の例は機能しません。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

上のコードのように、折り返される長い文字列を複数の行に結合するには、2つのオプションがあります。 連結演算子 (`+`) を使用できます。これについては、この記事の後半で説明します。 この記事で既に説明したように、`@` 文字を使用して逐語的文字列リテラルを作成することもできます。 逐語的文字列リテラルは、次のように行を越えて分割できます。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a>コード (およびマークアップ) のコメント

コメントを使用すると、自分や他のユーザーにメモを残すことができます。 また、実行するのではなく、ページ内に保持する必要のあるコードまたはマークアップを無効 (*コメントアウト*) することもできます。

Razor コードと HTML マークアップには、それぞれ異なるコメント構文があります。 すべての Razor コードと同様に、ページがブラウザーに送信される前に、Razor コメントがサーバー上で処理され、削除されます。 したがって、Razor コメントの構文を使用すると、ファイルを編集するときに表示できるコメントをコード (またはマークアップにも) に含めることができますが、ユーザーにはページソース内であっても表示されません。

ASP.NET Razor コメントの場合は、`@*` でコメントを開始し、`*@`で終了します。 コメントは、1行または複数行にすることができます。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

コードブロック内のコメントは次のようになります。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

次に示すのは、コードの行をコメントアウトして実行しないようにするコードのブロックです。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

コードブロック内では、Razor コメント構文を使用する代わりに、使用しているプログラミング言語のコメント構文を使用できC#ます。次に例を示します。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

でC#は、単一行のコメントの前に `//` 文字が付きます。複数行のコメントは `/*` で始まり、`*/`で終わります。 (Razor コメントの場合とC#同様に、コメントはブラウザーに表示されません)。

ご存知のように、マークアップでは、HTML コメントを作成できます。

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

HTML コメントは `<!--` 文字で始まり `-->`で終わります。 HTML コメントを使用すると、テキストだけでなく、ページに保持してもレンダリングしたくない HTML マークアップを囲むことができます。 この HTML コメントは、タグの内容全体と、タグに含まれるテキストを非表示にします。

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

Razor コメントとは異なり、HTML コメントはページに表示*され*、ユーザーはページソースを表示して表示できます。

Razor には、のC#入れ子になったブロックに関する制限があります。 詳細について[はC# 、「名前付き変数と入れ子になったブロックの生成](http://aspnetwebstack.codeplex.com/workitem/1914)」を参照してください。

## <a name="variables"></a>変数:

変数は、データを格納するために使用する名前付きオブジェクトです。 変数には任意の名前を指定できますが、名前の先頭には英字を使用する必要があり、空白や予約文字を含めることはできません。

### <a name="variables-and-data-types"></a>変数とデータ型

変数には、変数に格納されているデータの種類を示す特定のデータ型を指定できます。 文字列値 (&quot;Hello world&quot;など) を格納する文字列変数、整数値 (3 や79など) を格納する整数変数、および日付値をさまざまな形式で格納する日付変数 (4/12/2012 や2009など) を指定できます。 他にもさまざまなデータ型を使用できます。

ただし、通常は変数の型を指定する必要はありません。 ほとんどの場合、ASP.NET は変数のデータがどのように使用されているかに基づいて型を特定できます。 (場合によっては、型を指定する必要があります。これが当てはまる例があります)。

変数を宣言するには、`var` キーワードを使用するか (型を指定しない場合)、または型の名前を使用します。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

次の例は、web ページでの変数の一般的な使用例を示しています。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

前の例を1つのページで組み合わせると、次のような画面がブラウザーに表示されます。

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>データ型の変換とテスト

ASP.NET は通常、データ型を自動的に判断することができますが、できないことがあります。 そのため、明示的な変換を実行して ASP.NET を解決することが必要になる場合があります。 型を変換する必要がない場合でも、使用している可能性のあるデータの種類を確認するためにテストすると便利な場合があります。

最も一般的なケースは、文字列を別の型 (整数や日付など) に変換する必要がある場合です。 次の例は、文字列を数値に変換する必要がある一般的なケースを示しています。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

規則として、ユーザーの入力は文字列として取得されます。 数字を入力するように求められていても、数字を入力した場合でも、ユーザー入力を送信してコードで読み取ると、データは文字列形式になります。 したがって、文字列を数値に変換する必要があります。 この例では、変換せずに値に対して算術演算を実行しようとすると、ASP.NET は2つの文字列を追加できないため、次のエラーが発生します。

*型 ' string ' を ' int ' に暗黙的に変換することはできません。*

値を整数に変換するには、`AsInt` メソッドを呼び出します。 変換が成功した場合は、数値を追加できます。

次の表に、変数の一般的な変換メソッドとテストメソッドの一覧を示します。

:::row:::
    :::column:::
    <strong>方法</strong>
    :::column-end:::
    :::column:::
    <strong>説明</strong>
    :::column-end:::
    :::column:::
    <strong>例</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    整数 ("593" など) を表す文字列を整数に変換します。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    &quot;true&quot; のような文字列または false&quot; &quot;ブール型に変換します。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    &quot;1.3&quot; または &quot;7.439&quot; などの10進数値を持つ文字列を浮動小数点数に変換します。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    &quot;1.3&quot; または &quot;7.439&quot; などの10進数値を持つ文字列を10進数に変換します。 (ASP.NET では、10進数は浮動小数点数よりも正確です)。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    日付と時刻の値を表す文字列を ASP.NET `DateTime` 型に変換します。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    その他のデータ型を文字列に変換します。
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>オペレーター

演算子は、式で実行するコマンドの種類を ASP.NET に指示するキーワードまたは文字です。 C#言語 (およびそれに基づく Razor 構文) では、多くの演算子がサポートされていますが、最初に知っておく必要があるのはいくつかの操作だけです。 次の表は、最も一般的な演算子をまとめたものです。

:::row:::
    :::column:::
    <strong>[オペレーター]</strong>
    :::column-end:::
    :::column:::
    <strong>説明</strong>
    :::column-end:::
    :::column:::
    <strong>使用例</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+` `-` `*` `/`
    :::column-end:::
    :::column:::
    数値式で使用される算術演算子。
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    代入。 ステートメントの右辺の値を左側のオブジェクトに代入します。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    等値。 値が等しい場合は `true` を返します。 (`=` 演算子と `==` 演算子の違いに注意してください)。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    非等値。 値が等しくない場合は `true` を返します。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    小なり、大なり、小なり、または等しい、より大きい、または等しい。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    連結。文字列を結合するために使用されます。 ASP.NET は、式のデータ型に基づいて、この演算子と加算演算子の違いを認識します。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+=` `-=`
    :::column-end:::
    :::column:::
    インクリメント演算子とデクリメント演算子。変数から 1 (それぞれ) を加算して減算します。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    .Dot. オブジェクトとそのプロパティおよびメソッドを区別するために使用されます。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    内側. 式をグループ化し、パラメーターをメソッドに渡すために使用されます。
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    カッコ. 配列またはコレクションの値にアクセスするために使用されます。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    じゃない。 `true` 値を `false` に戻します。逆も同様です。 通常、`false` をテストするための簡単な方法として使用されます (つまり、`true`ではありません)。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&&` `||`
    :::column-end:::
    :::column:::
    論理 AND および OR。条件を相互にリンクするために使用されます。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a>コードでのファイルとフォルダーのパスの操作

多くの場合、コードでファイルとフォルダーのパスを操作します。 開発用コンピューターに表示される web サイトの物理フォルダー構造の例を次に示します。

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

Url とパスに関する重要な詳細情報を次に示します。

- URL は、ドメイン名 (`http://www.example.com`) またはサーバー名 (`http://localhost`、`http://mycomputer`) のいずれかで始まります。
- URL は、ホストコンピューターの物理パスに対応します。 たとえば、`http://myserver` は、サーバー上の*C:\websites\mywebsite*フォルダーに対応している可能性があります。
- 仮想パスは、完全パスを指定しなくてもコード内のパスを表す短縮形です。 これには、ドメイン名またはサーバー名の後の URL の部分が含まれます。 仮想パスを使用すると、パスを更新しなくてもコードを別のドメインまたはサーバーに移動できます。

相違点を理解するための例を次に示します。

| 完全な URL | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| サーバー名 | *my企業サーバー* |
| [仮想パス] | */humanresources/CompanyPolicy.htm* |
| 物理パス | *C:\mywebsites\humanresources\CompanyPolicy.htm* |

仮想ルートは/です。 C: ドライブのルートと同じです。 (仮想フォルダーパスは常にスラッシュを使用します)。フォルダーの仮想パスは、物理フォルダーと同じ名前である必要はありません。エイリアスにすることができます。 (実稼働サーバーでは、仮想パスが正確な物理パスと一致することはほとんどありません)。

コード内でファイルやフォルダーを操作するときに、使用しているオブジェクトに応じて、物理パスと仮想パスを参照することが必要になる場合があります。 ASP.NET には、コード内のファイルとフォルダーのパスを操作するためのツールが用意されています。 `Server.MapPath` メソッド、`~` 演算子、および `Href` メソッドです。

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a>仮想パスから物理パスへの変換: サーバーの MapPath メソッド

`Server.MapPath` メソッドは、仮想パス (C:\WebSites\MyWebSiteFolder\default.cshtml など *)* を絶対物理パス (たとえば、) に変換します。 この方法は、完全な物理パスが必要な場合にいつでも使用できます。 一般的な例として、web サーバー上のテキストファイルまたはイメージファイルを読み取ったり書き込んだりする場合があります。

通常、ホストサイトのサーバー上にあるサイトの絶対物理パスがわからないため、この方法では、既知のパス (仮想パス) をサーバー上の対応するパスに変換できます。 ファイルまたはフォルダーへの仮想パスをメソッドに渡し、物理パスを返します。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>仮想ルートの参照: ~ 演算子と Href メソッド

*Cshtml*ファイルまたは*vbhtml*ファイルでは、`~` 演算子を使用して仮想ルートパスを参照できます。 これは、サイト内でページを移動することができ、他のページに含まれているすべてのリンクが破損しないため、非常に便利です。 また、web サイトを別の場所に移動した場合にも便利です。 次に例をいくつか示します。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

Web サイトが `http://myserver/myapp`場合は、ページの実行時に ASP.NET がこれらのパスを処理する方法を次に示します。

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

(実際には、これらのパスは変数の値としては表示されませんが、ASP.NET はそのようなパスを扱います)。

次のように、サーバーコード (上記) とマークアップの両方で `~` 演算子を使用できます。

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

マークアップでは、`~` 演算子を使用して、イメージファイル、その他の web ページ、CSS ファイルなどのリソースへのパスを作成します。 ページが実行されると、ASP.NET はページ (コードとマークアップの両方) を参照し、適切なパスへのすべての `~` 参照を解決します。

## <a name="conditional-logic-and-loops"></a>条件付きロジックとループ

ASP.NET server code を使用すると、条件に基づいてタスクを実行し、ステートメントを特定の回数 (ループを実行するコード) に繰り返すコードを記述することができます。

### <a name="testing-conditions"></a>テスト条件

単純な条件をテストするには、`if` ステートメントを使用します。これは、指定したテストに基づいて true または false を返します。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

`if` キーワードはブロックを開始します。 実際のテスト (条件) はかっこ内にあり、true または false を返します。 テストが true の場合に実行されるステートメントは、中かっこで囲まれます。 `if` ステートメントには、条件が false の場合に実行するステートメントを指定する `else` ブロックを含めることができます。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

`else if` ブロックを使用して複数の条件を追加できます。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

この例では、if ブロックの最初の条件が true でない場合、`else if` 条件がチェックされます。 この条件が満たされると、`else if` ブロック内のステートメントが実行されます。 条件が満たされていない場合は、`else` ブロック内のステートメントが実行されます。 任意の数の else if ブロックを追加して、他のすべての&quot; 条件 &quot;として `else` ブロックで閉じることができます。

多数の条件をテストするには、`switch` ブロックを使用します。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

テストする値は、かっこで囲まれています (例では `weekday` 変数)。 個々のテストでは、コロン (:) で終わる `case` ステートメントが使用されます。 `case` ステートメントの値がテスト値と一致する場合は、そのケースブロック内のコードが実行されます。 各 case ステートメントを終了するには、`break` ステートメントを使用します。 (各 `case` ブロックに break を含め忘れた場合、次の `case` ステートメントのコードも実行されます)。`switch` ブロックには、多くの場合、&quot; &quot;の最後のケースとして `default` ステートメントが含まれています。それ以外の場合は、他のいずれのケースも true ではありません。

ブラウザーに表示された最後の2つの条件ブロックの結果:

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a>ループコード

多くの場合、同じステートメントを繰り返し実行する必要があります。 これを行うには、ループを使用します。 たとえば、多くの場合、データのコレクション内の各項目に対して同じステートメントを実行します。 ループする回数が正確にわかっている場合は、`for` ループを使用できます。 この種類のループは、カウントアップまたはカウントする場合に特に役立ちます。

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

ループは `for` キーワードで始まり、その後に3つのステートメントがかっこで囲まれ、それぞれがセミコロンで終了します。

- かっこ内では、最初のステートメント (`var i=10;`) によってカウンターが作成され、10に初期化されます。 カウンターに名前を付ける必要はあり&#8212;ません `i` 任意の変数を使用できます。 `for` ループが実行されると、カウンターが自動的にインクリメントされます。
- 2番目のステートメント (`i < 21;`) では、カウントする条件を設定します。 このケースでは、最大20にまで移動します (つまり、カウンターが21未満である間は継続します)。
- 3番目のステートメント (`i++`) では、インクリメント演算子を使用します。これは、ループが実行されるたびにカウンターに1が追加されることを指定するだけです。

中かっこ内には、ループの反復ごとに実行されるコードが含まれています。 マークアップは、毎回新しい段落 (`<p>` 要素) を作成し、出力に行を追加して `i` (カウンター) の値を表示します。 このページを実行すると、この例では、出力を表示する11行を作成し、アイテム番号を示す各行にテキストを入力します。

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

コレクションまたは配列を使用して作業している場合は、多くの場合、`foreach` ループを使用します。 コレクションは、類似したオブジェクトのグループであり、`foreach` ループを使用すると、コレクション内の各項目に対してタスクを実行できます。 この種類のループは、`for` ループとは異なり、カウンターをインクリメントしたり制限を設定したりする必要がないため、コレクションに便利です。 代わりに、`foreach` ループコードは、完了するまでコレクションを処理します。

たとえば、次のコードは、`Request.ServerVariables` コレクション内の項目を返します。これは、web サーバーに関する情報を格納するオブジェクトです。 `foreac` h ループを使用して、HTML の箇条書きに新しい `<li>` 要素を作成することによって各項目の名前を表示します。

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

`foreach` キーワードの後に、コレクション内の1つの項目 (例では `var item`) を表す変数を宣言し、続いて `in` キーワードを入力した後、ループするコレクションを指定します。 `foreach` ループの本体では、前に宣言した変数を使用して現在の項目にアクセスできます。

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

より汎用的なループを作成するには、`while` ステートメントを使用します。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

`while` ループは、`while` キーワードで始まり、その後に、ループの継続時間 (ここでは `countNum` が50未満である限り) を指定します。次に、繰り返します。 ループは通常、カウントに使用される変数またはオブジェクトをインクリメント (加算) またはデクリメント (減算) します。 この例では、`+=` 演算子は、ループが実行されるたびに `countNum` に1を加算します。 (カウントダウンするループ内で変数をデクリメントするには、デクリメント演算子 `-=`) を使用します。

## <a name="objects-and-collections"></a>オブジェクトとコレクション

ASP.NET web サイトのほぼすべてのものは、web ページ自体を含むオブジェクトです。 このセクションでは、コード内で頻繁に使用するいくつかの重要なオブジェクトについて説明します。

### <a name="page-objects"></a>Page オブジェクト

ASP.NET の最も基本的なオブジェクトはページです。 ページオブジェクトのプロパティには、修飾されたオブジェクトを使用せずに直接アクセスできます。 次のコードは、ページの `Request` オブジェクトを使用して、ページのファイルパスを取得します。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

現在の page オブジェクトのプロパティとメソッドを参照していることを明確にするために、必要に応じて `this` キーワードを使用して、コード内のページオブジェクトを表すことができます。 次に示すのは、上記のコード例です。ページを表すために `this` が追加されています。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

`Page` オブジェクトのプロパティを使用して、次のような大量の情報を取得できます。

- [https://login.microsoftonline.com/consumers/](`Request`) 既に説明したように、これは現在の要求に関する情報のコレクションです。要求を行ったブラウザーの種類、ページの URL、ユーザー id などが含まれます。
- [https://login.microsoftonline.com/consumers/](`Response`) これは、サーバーコードの実行が終了したときにブラウザーに送信される応答 (ページ) に関する情報のコレクションです。 たとえば、このプロパティを使用して、応答に情報を書き込むことができます。 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a>コレクションオブジェクト (配列とディクショナリ)

*コレクション*は、データベースの `Customer` オブジェクトのコレクションなど、同じ種類のオブジェクトのグループです。 ASP.NET には、`Request.Files` コレクションのような多くの組み込みコレクションが含まれています。

多くの場合、コレクション内のデータを操作します。 2つの一般的なコレクション型は、*配列*と*ディクショナリ*です。 配列は、類似した項目のコレクションを格納するが、各項目を保持するための個別の変数を作成しない場合に便利です。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

配列を使用して、`string`、`int`、`DateTime`などの特定のデータ型を宣言します。 変数に配列を含めることができることを示すには、宣言に角かっこを追加します (`string[]` や `int[]`など)。 配列内の項目には、その位置 (インデックス) を使用するか、`foreach` ステートメントを使用してアクセスできます。 配列インデックスは 0 &#8212;から始まります。つまり、最初の項目の位置は0、2番目の項目は1の位置にあります。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

配列内の項目の数を確認するには、その `Length` プロパティを取得します。 配列内の特定の項目の位置を取得するには (配列を検索する場合)、`Array.IndexOf` メソッドを使用します。 また、配列の内容 (`Array.Reverse` メソッド) の反転やコンテンツ (`Array.Sort` メソッド) の並べ替えなどを行うこともできます。

ブラウザーに表示される文字列配列コードの出力を次に示します。

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

ディクショナリはキーと値のペアのコレクションであり、キー (または名前) を指定して、対応する値を設定または取得します。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

ディクショナリを作成するには、`new` キーワードを使用して、新しい辞書オブジェクトを作成していることを示します。 `var` キーワードを使用して、変数に辞書を割り当てることができます。 ディクショナリ内の項目のデータ型は、山かっこ (`< >`) を使用して指定します。 宣言の最後に、かっこのペアを追加する必要があります。これは、実際には新しいディクショナリを作成するメソッドであるためです。

ディクショナリに項目を追加するには、ディクショナリ変数 (この場合は`myScores`) の `Add` メソッドを呼び出して、キーと値を指定します。 また、次の例のように、角かっこを使用してキーを指定し、単純な割り当てを行うこともできます。

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

ディクショナリから値を取得するには、キーを角かっこで囲んで指定します。

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a>パラメーターを使用したメソッドの呼び出し

この記事の前半で説明したように、を使用してプログラミングするオブジェクトには、メソッドを含めることができます。 たとえば、`Database` オブジェクトには、`Database.Connect` メソッドがある場合があります。 多くのメソッドには、1つまたは複数のパラメーターもあります。 *パラメーター*は、メソッドがタスクを完了できるようにメソッドに渡す値です。 たとえば、`Request.MapPath` メソッドの宣言を見て、次の3つのパラメーターを取得します。

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

(行は、読みやすくするために折り返されています。 改行は、引用符で囲まれた文字列内を除き、ほぼすべての場所に配置することができます)。

このメソッドは、指定された仮想パスに対応するサーバー上の物理パスを返します。 メソッドの3つのパラメーターは、`virtualPath`、`baseVirtualDir`、および `allowCrossAppMapping`です。 (宣言では、パラメーターが、受け入れられるデータのデータ型と共に一覧表示されていることに注意してください)。このメソッドを呼び出す場合は、3つのすべてのパラメーターの値を指定する必要があります。

Razor 構文には、メソッドにパラメーターを渡す方法として、*位置指定*パラメーターと*名前付きパラメーター*の2つのオプションが用意されています。 位置指定パラメーターを使用してメソッドを呼び出すには、メソッド宣言で指定された厳密な順序でパラメーターを渡します。 (通常、この順序については、メソッドのドキュメントを参照してください)。順序に従う必要があります。また、必要に応じて&#8212;パラメーターを省略することはできません。値のない位置指定パラメーターには、空の文字列 (`""`) または `null` を渡します。

次の例では、web サイトに*scripts*という名前のフォルダーがあることを前提としています。 このコードは `Request.MapPath` メソッドを呼び出し、3つのパラメーターの値を正しい順序で渡します。 次に、結果としてマップされたパスが表示されます。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

メソッドに多数のパラメーターがある場合は、名前付きパラメーターを使用してコードを読みやすくすることができます。 名前付きパラメーターを使用してメソッドを呼び出すには、パラメーター名の後にコロン (:) を指定し、その後に値を指定します。 名前付きパラメーターの利点は、任意の順序で渡すことができることです。 (欠点は、メソッドの呼び出しがコンパクトではないことです)。

次の例では、上記と同じメソッドを呼び出しますが、名前付きパラメーターを使用して値を指定します。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

ご覧のように、パラメーターは異なる順序で渡されます。 ただし、前の例とこの例を実行すると、同じ値が返されます。

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a>エラーの処理

### <a name="try-catch-statements"></a>Try-catch ステートメント

多くの場合、コントロール以外の理由で失敗する可能性のあるステートメントがコードに含まれています。 次に例を示します。

- コードでファイルを作成またはアクセスしようとすると、すべてのエラーが発生する可能性があります。 必要なファイルが存在しない可能性があります。ロックされているか、コードにアクセス許可がない可能性があります。
- 同様に、コードがデータベース内のレコードを更新しようとすると、アクセス許可の問題が発生し、データベースへの接続が切断され、保存するデータが無効になっている可能性があります。

プログラミング用語では、これらの状況は*例外*と呼ばれます。 コードで例外が発生した場合、ユーザーにとって非常に面倒なエラーメッセージが生成されます (スローされます)。

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

コードで例外が発生する可能性があり、この種類のエラーメッセージが表示されないようにするには、`try/catch` ステートメントを使用します。 `try` ステートメントでは、チェックしているコードを実行します。 1つ以上の `catch` ステートメントでは、発生した可能性のある特定のエラー (特定の種類の例外) を検索できます。 予測しているエラーを検索するために必要な数の `catch` ステートメントを含めることができます。

> [!NOTE]
> `try/catch` ステートメントでは `Response.Redirect` メソッドを使用しないことをお勧めします。これは、ページで例外が発生する可能性があるためです。

次の例は、最初の要求でテキストファイルを作成し、ユーザーがファイルを開くためのボタンを表示するページを示しています。 この例では、例外が発生するように、不適切なファイル名を意図的に使用しています。 このコードには `catch` 2 つの例外のステートメントが含まれています。 `FileNotFoundException`は、ファイル名が正しくない場合に発生します。また、ASP.NET がフォルダーを検索できない場合に発生する `DirectoryNotFoundException`です。 (例では、すべてが正常に動作するときに実行方法を確認するために、ステートメントのコメントを解除できます)。

コードで例外が処理されなかった場合は、前のスクリーンショットのようなエラーページが表示されます。 ただし、`try/catch` セクションは、ユーザーがこれらの種類のエラーを表示できないようにするのに役立ちます。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a>その他のリソース

**Visual Basic を使用したプログラミング**

[付録: Visual Basic の言語と構文](https://go.microsoft.com/fwlink/?LinkId=202908)

**リファレンス ドキュメント**

[ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)

[C#言語](https://msdn.microsoft.com/library/kx37x362.aspx)

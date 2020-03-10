---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Razor 構文を使用した ASP.NET Web プログラミングの概要 (Visual Basic) |Microsoft Docs
author: Rick-Anderson
description: この付録概要 ASP.NET Web ページを使用したプログラミングの Visual Basic で Razor 構文を使用します。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 2be57655b8c9b76b94e1d9a7ae5fbee27545a0a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422662"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a>Razor 構文 (Visual Basic) を使用した ASP.NET Web プログラミングの概要 (英語)

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、Razor 構文と Visual Basic を使用した ASP.NET Web ページによるプログラミングの概要について説明します。 ASP.NETは、Webサーバーで動的な Web ページを運用するためのマイクロソフトの技術です。
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

Razor 構文を使用する ASP.NET Web ページを使用するほとんどの例は C# を使用します。 ただし、Razor 構文も Visual Basic をサポートしています。 Visual Basic で ASP.NET web ページをプログラミングするには、拡張子が*vbhtml*の web ページを作成し、Visual Basic コードを追加します。 この記事では、ASP.NET の Web ページを作成するための Visual Basic 言語と構文の使用方法の概要について説明します。

> [!NOTE]
> Microsoft WebMatrix の既定の web サイトテンプレート (**ケーキ屋さん**、**フォトギャラリー**、および**スターターサイト**など) は、および Visual Basic C#バージョンで使用できます。 Visual Basic テンプレートを NuGet パッケージとしてインストールできます。 Web サイトテンプレートは、サイトのルートフォルダーに*Microsoft templates*という名前のフォルダーにインストールされます。

## <a name="the-top-8-programming-tips"></a>8 つのプログラミング Tips

このセクションでは、Razor 構文を使用して ASP.NET サーバーコードの記述を開始するときに理解しておく必要があるいくつかのヒントを示します。

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. @ 文字を使用してコードをページに追加します。

`@` 文字は、インライン式、単一ステートメントブロック、および複数ステートメントブロックを開始します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

結果がブラウザーに表示されます。

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **HTML エンコード**
> 
> 前の例のように `@` 文字を使用してページにコンテンツを表示すると、ASP.NET は出力を HTML エンコードします。 これにより、予約された HTML 文字 (`<`、`>` や `&`など) が、HTML タグまたはエンティティとして解釈されるのではなく、web ページに文字として表示されるようにするコードに置き換えられます。 HTML エンコードを使用しないと、サーバーコードからの出力が正しく表示されず、ページがセキュリティ上のリスクにさらされる可能性があります。
> 
> タグをマークアップとしてレンダリングする HTML マークアップを出力することが目的である場合 (たとえば、段落や `<em></em>` テキストを強調するための `<p></p>`)、この記事で後述する「[コードブロック内のテキスト、マークアップ、およびコードの結合](#BM_CombiningTextMarkupAndCode)」セクションを参照してください。
> 
> Html エンコードの詳細については、 [ASP.NET Web ページサイトでの Html フォームの操作](https://go.microsoft.com/fwlink/?LinkId=202892)」を参照してください。

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a>2. コードブロックをコードで囲みます...終了コード

コードブロックには1つ以上のコードステートメントが含まれており、キーワード `Code` と `End Code`で囲まれています。 開始 `Code` キーワードは、`@` 文字&#8212;の直後に配置することはできません。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

結果がブラウザーに表示されます。

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a>3. ブロック内では、各コードステートメントを改行で終了します。

Visual Basic コードブロックでは、各ステートメントは改行で終了します。 (この記事の後半では、必要に応じて長いコードステートメントを複数の行にラップする方法を説明しています)。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a>4. 変数を使用して値を格納する

文字列、数値、日付など、*変数*に値を格納することができます。新しい変数を作成するには、`Dim` キーワードを使用します。 `@`を使用して、変数の値をページに直接挿入できます。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

結果がブラウザーに表示されます。

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. リテラル文字列値を二重引用符で囲みます。

*文字列*は、テキストとして扱われる文字のシーケンスです。 文字列を指定するには、ダブル クォーテーション記号で囲みます。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

文字列値の中に二重引用符を埋め込むには、2つの二重引用符文字を挿入します。 ページ出力に二重引用符文字を1回だけ表示する場合は、引用符で囲まれた文字列内の `""` として入力します。2回表示する場合は、引用符で囲まれた文字列内の `""""` として入力します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

結果がブラウザーに表示されます。

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a>6. Visual Basic コードでは大文字と小文字が区別されない

Visual Basic 言語では大文字と小文字が区別されません。 プログラミングキーワード (`Dim`、`If`、`True`など) と変数名 (`myString`、`subTotal`など) は、どのような場合でも記述できます。

次のコード行では、小文字の名前を使用して `lastname` 変数に値を代入し、大文字の名前を使用して変数の値をページに出力します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

結果がブラウザーに表示されます。

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a>7. コーディングの多くは、オブジェクトの操作を行います。

オブジェクトは、ページ、テキストボックス、ファイル、 &#8212;画像、web 要求、電子メールメッセージ、顧客レコード (データベース行) などを使用してプログラミングできることを表します。オブジェクトにはプロパティ&#8212;があり、テキストボックスオブジェクトには `Text` プロパティがあり、要求オブジェクトにはプロパティが `Url`、電子メールメッセージには `From` プロパティがあり、customer オブジェクトには `FirstName` プロパティがあります。 オブジェクトには、実行できる&quot; &quot;動詞であるメソッドもあります。 例としては、ファイルオブジェクトの `Save` メソッド、イメージオブジェクトの `Rotate` メソッド、電子メールオブジェクトの `Send` メソッドなどがあります。

多くの場合、`Request` オブジェクトを使用します。これにより、ページ上のフォームフィールドの値 (テキストボックスなど)、要求を行ったブラウザーの種類、ページの URL、ユーザー id などの情報が得られます。この例では、`Request` オブジェクトのプロパティにアクセスする方法と、`Request` オブジェクトの `MapPath` メソッドを呼び出す方法を示します。これにより、サーバー上のページの絶対パスが得られます。

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

結果がブラウザーに表示されます。

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. 決定を行うコードを記述できます。

動的 web ページの重要な機能は、条件に基づいて何を行うかを決定できることです。 これを行う最も一般的な方法は、`If` ステートメント (および省略可能な `Else` ステートメント) を使用することです。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

ステートメント `If IsPost` は、`If IsPost = True`を簡単に記述する方法です。 `If` ステートメントと共に、条件のテスト、コードブロックの繰り返しなど、さまざまな方法があります。これについては、この記事の後半で説明します。

ブラウザーに表示される結果 ( **[送信]** をクリックした後):

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **HTTP GET メソッドと POST メソッド、および IsPost プロパティ**
> 
> Web ページ (HTTP) に使用されるプロトコルでは、サーバーへの要求を行うために使用されるメソッド (&quot;動詞&quot;) の数が制限されています。 最も一般的な2つの方法は、ページの読み取りに使用される GET と、ページの送信に使用される POST です。 一般に、ユーザーが初めてページを要求したときは、GET を使用してページが要求されます。 ユーザーがフォームに入力して **[送信]** をクリックすると、ブラウザーはサーバーに POST 要求を行います。
> 
> Web プログラミングでは、ページの処理方法を把握できるように、ページが GET として要求されているのか、または投稿として要求されているのかを知ることが役に立つことがよくあります。 ASP.NET Web ページでは、`IsPost` プロパティを使用して、要求が GET または POST のどちらであるかを確認できます。 要求が POST の場合、`IsPost` プロパティは true を返し、フォームのテキストボックスの値を読み取るなどの操作を実行できます。 多くの例では、`IsPost`の値に応じて、ページを異なる方法で処理する方法を示しています。

## <a name="a-simple-code-example"></a>単純なコード例

この手順では、基本的なプログラミング手法を示すページを作成する方法について説明します。 この例では、ユーザーが2つの数値を入力できるページを作成し、それらを追加して結果を表示します。

1. エディターで、新しいファイルを作成し、「 *Addnumbers. vbhtml*」という名前を付けます。
2. 次のコードとマークアップをページにコピーして、ページに既に存在するものを置き換えます。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    ここでは、次の点に注意してください。

    - `@` 文字は、ページ内の最初のコードブロックを開始し、最後の近くに埋め込まれた `totalMessage` 変数の前に置かれます。
    - ページの上部にあるブロックは `Code...End Code`で囲まれています。
    - 変数 `total`、`num1`、`num2`、および `totalMessage` には、いくつかの数値と文字列が格納されます。
    - `totalMessage` 変数に代入されたリテラル文字列値は、二重引用符で囲まれています。
    - Visual Basic コードでは大文字と小文字が区別されないため、ページの下部付近で `totalMessage` 変数が使用されている場合、その名前はページの先頭にある変数宣言のスペルと一致している必要があります。 大文字と小文字は区別されません。
    - 式 `num1.AsInt()` + `num2.AsInt()` オブジェクトとメソッドの操作方法を示しています。 各変数の `AsInt` メソッドは、ユーザーが入力した文字列を、追加できる整数 (整数) に変換します。
    - `<form>` タグには、`method="post"` 属性が含まれています。 これにより、ユーザーが **[追加]** をクリックしたときに、HTTP POST メソッドを使用してページがサーバーに送信されることを指定します。 ページが送信されると、コード `If IsPost` が true に評価され、条件コードが実行されて、数値を加算した結果が表示されます。
3. ページを保存し、ブラウザーで実行します。 (実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。2つの整数を入力し、 **[追加]** ボタンをクリックします。

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a>Visual Basic 言語と構文

前に、ASP.NET web ページを作成する方法の基本的な例と、HTML マークアップにサーバーコードを追加する方法について説明しました。 ここでは、Visual Basic を使用して、プログラミング言語の規則である Razor 構文&#8212;を使用して ASP.NET サーバーコードを記述する方法の基本について説明します。

(特に C、C++、C#、Visual Basic、または JavaScript を使用した) 場合のプログラミング経験豊富な場合は、ここで読んだの多くが使い慣れたになります。 場合によっては、WebMatrix コードを*vbhtml*ファイルのマークアップに追加する方法についてのみ理解する必要があります。

### <a id="BM_CombiningTextMarkupAndCode"></a>コードブロック内のテキスト、マークアップ、およびコードの結合

サーバーコードブロックでは、多くの場合、テキストとマークアップをページに出力します。 サーバーコードブロックにコード以外のテキストが含まれていて、そのテキストをそのように表示する必要がある場合、ASP.NET はそのテキストをコードから区別できる必要があります。 これにはいくつかの方法があります。

- テキストは、`<p></p>` や `<em></em>`などの HTML ブロック要素で囲みます。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    HTML 要素には、テキスト、追加の HTML 要素、およびサーバーコード式を含めることができます。 ASP.NET が HTML の開始タグ (`<p>`など) を認識すると、要素とその内容をすべてブラウザーに表示します (サーバーコード式を解決します)。

- `@:` 演算子または `<text>` 要素を使用します。 `@:` は、プレーンテキストまたは一致しない HTML タグを含む1行のコンテンツを出力します。`<text>` 要素は、出力に複数の行を囲みます。 これらのオプションは、HTML 要素を出力の一部としてレンダリングしない場合に便利です。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    次の例では、前の例を繰り返しますが、1組の `<text>` タグを使用して、表示するテキストを囲みます。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    次の例では、`<text>` タグと `</text>` タグによって3つの行が囲まれています。これらの行には、非包含テキストと一致しない HTML タグ (`<br />`) と、サーバーコードおよび一致した HTML タグがあります。 繰り返しになりますが、各行の前に `@:` 演算子を使用することもできます。どちらの方法でも動作します。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > HTML 要素を使用して、このセクション&#8212;に示すようにテキストを出力する場合、`@:` 演算子、 &#8212;または `<text>` 要素 ASP.NET は、出力を html エンコードしません。 (前述のように、ASP.NET は、このセクションに記載されている特殊なケースを除き、`@`の前にあるサーバーコード式とサーバーコードブロックの出力をエンコードします)。

### <a name="whitespace"></a>空白文字

ステートメント内の余分なスペース (および文字列リテラルの外部) は、ステートメントに影響しません。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a>長いステートメントを複数行に分割する

長いコードステートメントを複数の行に分割するには、各コード行の後にアンダースコア文字 `_` (Visual Basic は*継続文字*と呼ばれます) を使用します。 ステートメントを次の行に分割するには、行の末尾でスペースと継続文字を追加します。 次の行でステートメントを続行します。 ステートメントは、読みやすさを向上させるために必要な数の行にラップすることができます。 次の 2 つのステートメントでは同じ結果が得られます。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

ただし、文字列リテラルの途中では、行をラップすることはできません。 次の例は機能しません。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

上のコードのように、折り返される長い文字列を複数の行に結合するには、*連結演算子*(`&`) を使用する必要があります。これについては、この記事の後半で説明します。

### <a name="code-comments"></a>コードコメント

コメントを使用すると、自分や他のユーザーにメモを残すことができます。 Razor 構文のコメントの先頭には `@*` が付き、`*@`で終わります。

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

コードブロック内では、Razor 構文コメントを使用することも、通常の Visual Basic コメント文字を使用することもできます。これは、各行の先頭に単一引用符 (`'`) を付けたものです。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a>変数:

変数は、データを格納するために使用する名前付きオブジェクトです。 変数には任意の名前を指定できますが、名前の先頭には英字を使用する必要があり、空白や予約文字を含めることはできません。 Visual Basic で、前に説明したように、変数名の文字の大文字と小文字は関係ありません。

### <a name="variables-and-data-types"></a>変数とデータ型

変数には、変数に格納されているデータの種類を示す特定のデータ型を指定できます。 文字列値 (&quot;Hello world&quot;など) を格納する文字列変数、整数値 (3 や79など) を格納する整数変数、および日付値をさまざまな形式で格納する日付変数 (4/12/2012 や2009など) を指定できます。 他にもさまざまなデータ型を使用できます。

ただし、変数の型を指定する必要はありません。 ほとんどの場合、ASP.NET は変数のデータがどのように使用されているかに基づいて型を調べることができます。 (場合によっては、型を指定する必要があります。これが当てはまる例があります)。

型を指定せずに変数を宣言するには、`Dim` と変数名 (たとえば、`Dim myVar`) を使用します。 型の変数を宣言するには、`Dim` を使用し、変数名の後に `As` を指定してから、型名 (たとえば、`Dim myVar As String`) を指定します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

次の例は、web ページの変数を使用するインライン式を示しています。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

結果がブラウザーに表示されます。

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>データ型の変換とテスト

ASP.NET は通常、データ型を自動的に判断することができますが、できないことがあります。 そのため、明示的な変換を実行して ASP.NET を解決することが必要になる場合があります。 型を変換する必要がない場合でも、使用している可能性のあるデータの種類を確認するためにテストすると便利な場合があります。

最も一般的なケースは、文字列を別の型 (整数や日付など) に変換する必要がある場合です。 次の例は、文字列を数値に変換する必要がある一般的なケースを示しています。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

規則として、ユーザーの入力は文字列として取得されます。 数値を入力するように求められていても、数字を入力した場合でも、ユーザー入力が送信され、コードで読み取られた場合でも、データは文字列形式になります。 したがって、文字列を数値に変換する必要があります。 この例では、変換せずに値に対して算術演算を実行しようとすると、ASP.NET は2つの文字列を追加できないため、次のエラーが発生します。

`Cannot implicitly convert type 'string' to 'int'.`

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
        整数 (&quot;593&quot;など) を表す文字列を整数に変換します。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>オペレーター

演算子は、式で実行するコマンドの種類を ASP.NET に指示するキーワードまたは文字です。 Visual Basic は多くの演算子をサポートしていますが、ASP.NET web ページの開発を開始するには、いくつかのことを理解している必要があります。 次の表は、最も一般的な演算子をまとめたものです。

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
        `+ - * /`
    :::column-end:::
    :::column:::
        数値式で使用される算術演算子。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        代入と等値。 コンテキストによっては、ステートメントの右側の値が左側のオブジェクトに割り当てられるか、値が等しいかどうかがチェックされます。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        非等値。 値が等しくない場合は `True` を返します。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        より小さい、より大きい、より小さい、または等しい。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        連結。文字列を結合するために使用されます。
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        インクリメント演算子とデクリメント演算子。変数から 1 (それぞれ) を加算して減算します。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        内側. 式をグループ化したり、メソッドにパラメーターを渡したり、配列やコレクションのメンバーにアクセスしたりするために使用します。
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        じゃない。 True の値を false に、またはその逆を反転します。 通常、`False` をテストするための簡単な方法として使用されます (つまり、`True`ではありません)。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        論理 AND および OR。条件を相互にリンクするために使用されます。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

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

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>仮想ルートの参照: ~ 演算子と Href メソッド

*Cshtml*ファイルまたは*vbhtml*ファイルでは、`~` 演算子を使用して仮想ルートパスを参照できます。 これは、サイト内でページを移動することができ、他のページに含まれているすべてのリンクが破損しないため、非常に便利です。 また、web サイトを別の場所に移動した場合にも便利です。 次に例をいくつか示します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

Web サイトが `http://myserver/myapp`場合は、ページの実行時に ASP.NET がこれらのパスを処理する方法を次に示します。

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

(実際には、これらのパスは変数の値としては表示されませんが、ASP.NET はそのようなパスを扱います)。

次のように、サーバーコード (上記) とマークアップの両方で `~` 演算子を使用できます。

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

マークアップでは、`~` 演算子を使用して、イメージファイル、その他の web ページ、CSS ファイルなどのリソースへのパスを作成します。 ページが実行されると、ASP.NET はページ (コードとマークアップの両方) を参照し、適切なパスへのすべての `~` 参照を解決します。

## <a name="conditional-logic-and-loops"></a>条件付きロジックとループ

ASP.NET server code を使用すると、条件に基づいてタスクを実行し、特定の回数 (ループを実行するコード) でステートメントを繰り返すコードを記述することができます。

### <a name="testing-conditions"></a>テスト条件

単純な条件をテストするには、`If...Then` ステートメントを使用します。これにより、指定したテストに基づいて `True` または `False` が返されます。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

`If` キーワードはブロックを開始します。 実際のテスト (条件) は `If` キーワードに従い、true または false を返します。 `If` ステートメントが `Then`で終了します。 テストが true の場合に実行されるステートメントは、`If` と `End If`で囲まれます。 `If` ステートメントには、条件が false の場合に実行するステートメントを指定する `Else` ブロックを含めることができます。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

`If` ステートメントでコードブロックが開始された場合、通常の `Code...End Code` ステートメントを使用してブロックを含める必要はありません。 ブロックに `@` を追加するだけで、それが機能します。 この方法は、`If` と、`For`、`For Each`、`Do While`などのコードブロックが後に続く他の Visual Basic プログラミングキーワードにも使用できます。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

1つ以上の `ElseIf` ブロックを使用して、複数の条件を追加できます。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

この例では、`If` ブロックの最初の条件が true でない場合、`ElseIf` 条件がチェックされます。 この条件が満たされると、`ElseIf` ブロック内のステートメントが実行されます。 条件が満たされていない場合は、`Else` ブロック内のステートメントが実行されます。 任意の数の `ElseIf` ブロックを追加して、他のすべての条件を&quot; &quot;として、`Else` ブロックで閉じることができます。

多数の条件をテストするには、`Select Case` ブロックを使用します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

テストする値はかっこで囲まれています (例では、曜日変数)。 個々のテストでは、値を一覧表示する `Case` ステートメントが使用されます。 `Case` ステートメントの値がテスト値と一致する場合は、その `Case` ブロック内のコードが実行されます。

ブラウザーに表示された最後の2つの条件ブロックの結果:

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a>ループコード

多くの場合、同じステートメントを繰り返し実行する必要があります。 これを行うには、ループを使用します。 たとえば、多くの場合、データのコレクション内の各項目に対して同じステートメントを実行します。 ループする回数が正確にわかっている場合は、`For` ループを使用できます。 この種類のループは、カウントアップまたはカウントする場合に特に役立ちます。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

ループは `For` キーワードで始まり、その後に3つの要素が続きます。

- `For` ステートメントの直後に、カウンター変数を宣言し (`Dim`を使用する必要はありません)、`i = 10 to 20`のように範囲を指定します。 これは、変数 `i` が10にカウントされ、20 (を含む) に達するまで続行されることを意味します。
- `For` と `Next` ステートメントの間には、ブロックの内容があります。 これには、各ループで実行される1つ以上のコードステートメントを含めることができます。
- `Next i` ステートメントは、ループを終了します。 カウンターをインクリメントし、ループの次の反復処理を開始します。

`For` と `Next` の行の間のコード行には、ループの各反復処理で実行されるコードが含まれています。 マークアップは、毎回新しい段落 (`<p>` 要素) を作成し、出力に行を追加して i (カウンター) の値を表示します。 このページを実行すると、この例では、出力を表示する11行を作成し、アイテム番号を示す各行にテキストを入力します。

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

コレクションまたは配列を使用して作業している場合は、多くの場合、`For Each` ループを使用します。 コレクションは、類似したオブジェクトのグループであり、`For Each` ループを使用すると、コレクション内の各項目に対してタスクを実行できます。 この種類のループは、`For` ループとは異なり、カウンターをインクリメントしたり制限を設定したりする必要がないため、コレクションに便利です。 代わりに、`For Each` ループコードは、完了するまでコレクションを処理します。

この例では、`Request.ServerVariables` コレクション内の項目 (web サーバーに関する情報を含む) が返されます。 `For Each` ループを使用して、HTML の箇条書きに新しい `<li>` 要素を作成することによって各項目の名前を表示します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

`For Each` キーワードの後に、コレクション内の単一の項目 (例では `myItem`) を表す変数が続き、その後に `In` キーワードが続き、その後にループするコレクションが続きます。 `For Each` ループの本体では、前に宣言した変数を使用して現在の項目にアクセスできます。

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

より汎用的なループを作成するには、`Do While` ステートメントを使用します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

このループは `Do While` キーワードで始まり、その後に条件が続き、その後に繰り返しブロックが続きます。 ループは通常、カウントに使用される変数またはオブジェクトをインクリメント (加算) またはデクリメント (減算) します。 この例では、`+=` 演算子は、ループが実行されるたびに変数の値に1を加算します。 (カウントダウンするループ内で変数をデクリメントするには、デクリメント演算子 `-=`を使用します)。

## <a name="objects-and-collections"></a>オブジェクトとコレクション

ASP.NET web サイトのほぼすべてのものは、web ページ自体を含むオブジェクトです。 このセクションでは、コード内で頻繁に使用するいくつかの重要なオブジェクトについて説明します。

### <a name="page-objects"></a>Page オブジェクト

ASP.NET の最も基本的なオブジェクトはページです。 ページオブジェクトのプロパティには、修飾されたオブジェクトを使用せずに直接アクセスできます。 次のコードは、ページの `Request` オブジェクトを使用して、ページのファイルパスを取得します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

`Page` オブジェクトのプロパティを使用して、次のような大量の情報を取得できます。

- [https://login.microsoftonline.com/consumers/](`Request`) 既に説明したように、これは現在の要求に関する情報のコレクションです。要求を行ったブラウザーの種類、ページの URL、ユーザー id などが含まれます。
- [https://login.microsoftonline.com/consumers/](`Response`) これは、サーバーコードの実行が終了したときにブラウザーに送信される応答 (ページ) に関する情報のコレクションです。 たとえば、このプロパティを使用して、応答に情報を書き込むことができます。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a>コレクションオブジェクト (配列とディクショナリ)

コレクションは、データベースの `Customer` オブジェクトのコレクションなど、同じ種類のオブジェクトのグループです。 ASP.NET には、`Request.Files` コレクションのような多くの組み込みコレクションが含まれています。

多くの場合、コレクション内のデータを操作します。 2つの一般的なコレクション型は、*配列*と*ディクショナリ*です。 配列は、類似した項目のコレクションを格納するが、各項目を保持するための個別の変数を作成しない場合に便利です。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

配列を使用して、`String`、`Integer`、`DateTime`などの特定のデータ型を宣言します。 変数に配列を含めることができることを示すには、宣言の変数名にかっこを追加します (`Dim myVar() As String`など)。 配列内の項目には、その位置 (インデックス) を使用するか、`For Each` ステートメントを使用してアクセスできます。 配列インデックスは 0 &#8212;から始まります。つまり、最初の項目の位置は0、2番目の項目は1の位置にあります。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

配列内の項目の数を確認するには、その `Length` プロパティを取得します。 配列内の特定の項目の位置を取得する (つまり、配列を検索する) には、`Array.IndexOf` メソッドを使用します。 また、配列の内容 (`Array.Reverse` メソッド) の反転やコンテンツ (`Array.Sort` メソッド) の並べ替えなどを行うこともできます。

ブラウザーに表示される文字列配列コードの出力を次に示します。

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

ディクショナリはキーと値のペアのコレクションであり、キー (または名前) を指定して、対応する値を設定または取得します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

ディクショナリを作成するには、`New` キーワードを使用して、新しい `Dictionary` オブジェクトを作成していることを示します。 `Dim` キーワードを使用して、変数に辞書を割り当てることができます。 ディクショナリ内の項目のデータ型を示すには、かっこ (`( )`) を使用します。 宣言の最後に、別のかっこのペアを追加する必要があります。これは、実際には新しいディクショナリを作成するメソッドであるためです。

ディクショナリに項目を追加するには、ディクショナリ変数 (この場合は`myScores`) の `Add` メソッドを呼び出して、キーと値を指定します。 また、次の例のように、かっこを使用してキーを指定し、単純な割り当てを行うこともできます。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

ディクショナリから値を取得するには、キーをかっこで囲んで指定します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a>パラメーターを使用したメソッドの呼び出し

この記事で既に説明したように、プログラムで使用するオブジェクトにはメソッドがあります。 たとえば、`Database` オブジェクトには、`Database.Connect` メソッドがある場合があります。 多くのメソッドには、1つまたは複数のパラメーターもあります。 *パラメーター*は、メソッドがタスクを完了できるようにメソッドに渡す値です。 たとえば、`Request.MapPath` メソッドの宣言を見て、次の3つのパラメーターを取得します。

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

このメソッドは、指定された仮想パスに対応するサーバー上の物理パスを返します。 メソッドの3つのパラメーターは、`virtualPath`、`baseVirtualDir`、および `allowCrossAppMapping`です。 (宣言では、パラメーターが、受け入れられるデータのデータ型と共に一覧表示されていることに注意してください)。このメソッドを呼び出す場合は、3つのすべてのパラメーターの値を指定する必要があります。

Razor 構文で Visual Basic を使用する場合、メソッドにパラメーターを渡す方法として、*位置指定*パラメーターと*名前付きパラメーター*の2つのオプションがあります。 位置指定パラメーターを使用してメソッドを呼び出すには、メソッド宣言で指定された厳密な順序でパラメーターを渡します。 (通常、この順序については、メソッドのドキュメントを参照してください)。順序に従う必要があります。また、必要に応じて&#8212;パラメーターを省略することはできません。値のない位置指定パラメーターには、空の文字列 (`""`) または null を渡します。

次の例では、web サイトに*scripts*という名前のフォルダーがあることを前提としています。 このコードは `Request.MapPath` メソッドを呼び出し、3つのパラメーターの値を正しい順序で渡します。 次に、結果としてマップされたパスが表示されます。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

メソッドに多くのパラメーターがある場合は、名前付きパラメーターを使用して、コードをすっきりさせて読みやすくすることができます。 名前付きパラメーターを使用してメソッドを呼び出すには、パラメーター名の後に `:=` を指定し、値を指定します。 名前付きパラメーターの利点は、必要な順序で追加できることです。 (欠点は、メソッドの呼び出しがコンパクトではないことです)。

次の例では、上記と同じメソッドを呼び出しますが、名前付きパラメーターを使用して値を指定します。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

ご覧のように、パラメーターは異なる順序で渡されます。 ただし、前の例とこの例を実行すると、同じ値が返されます。

## <a name="handling-errors"></a>エラーの処理

### <a name="try-catch-statements"></a>Try-catch ステートメント

多くの場合、コントロール以外の理由で失敗する可能性のあるステートメントがコードに含まれています。 次に例を示します。

- コードでファイルのオープン、作成、読み取り、または書き込みを行おうとすると、すべてのエラーが発生する可能性があります。 必要なファイルが存在しない可能性があります。ロックされているか、コードにアクセス許可がない可能性があります。
- 同様に、コードがデータベース内のレコードを更新しようとすると、アクセス許可の問題が発生し、データベースへの接続が切断され、保存するデータが無効になっている可能性があります。

プログラミング用語では、これらの状況は*例外*と呼ばれます。 コードで例外が発生した場合は、ユーザーにとって非常に面倒なエラーメッセージが生成 (スロー) されます。

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

コードで例外が発生する可能性があり、この種類のエラーメッセージが表示されないようにするには、`Try/Catch` ステートメントを使用します。 `Try` ステートメントでは、チェックしているコードを実行します。 1つ以上の `Catch` ステートメントでは、発生した可能性のある特定のエラー (特定の種類の例外) を検索できます。 予測しているエラーを検索するために必要な数の `Catch` ステートメントを含めることができます。

> [!NOTE]
> `Try/Catch` ステートメントでは `Response.Redirect` メソッドを使用しないことをお勧めします。これは、ページで例外が発生する可能性があるためです。

次の例は、最初の要求でテキストファイルを作成し、ユーザーがファイルを開くためのボタンを表示するページを示しています。 この例では、例外が発生するように、不適切なファイル名を意図的に使用しています。 このコードには `Catch` 2 つの例外のステートメントが含まれています。 `FileNotFoundException`は、ファイル名が正しくない場合に発生します。また、ASP.NET がフォルダーを検索できない場合に発生する `DirectoryNotFoundException`です。 (例では、すべてが正常に動作するときに実行方法を確認するために、ステートメントのコメントを解除できます)。

コードで例外が処理されなかった場合は、前のスクリーンショットのようなエラーページが表示されます。 ただし、`Try/Catch` セクションは、ユーザーがこれらの種類のエラーを表示できないようにするのに役立ちます。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a>その他のリソース

### <a name="reference-documentation"></a>リファレンス ドキュメント

- [ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)
- [Visual Basic 言語](https://msdn.microsoft.com/library/2x7h1hfk.aspx)

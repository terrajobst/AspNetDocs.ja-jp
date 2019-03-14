---
uid: web-pages/overview/ui-layouts-and-themes/9-working-with-images
title: ASP.NET Web Pages (Razor) サイトに画像の操作 |Microsoft Docs
author: Rick-Anderson
description: この章は、追加、表示、およびイメージを操作する方法を示します (サイズ変更、反転、およびウォーターマークの追加)、web サイトにします。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 778c4e58-4372-4d25-bab9-aec4a8d8e38d
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/9-working-with-images
msc.type: authoredcontent
ms.openlocfilehash: 7536f71eb9afce9d7c8bb7e4d6326d280658c27b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056039"
---
<a name="working-with-images-in-an-aspnet-web-pages-razor-site"></a>ASP.NET Web Pages (Razor) サイトに画像の操作
====================
によって[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、追加、表示、およびイメージを操作する方法を示します (サイズ変更、反転、およびウォーターマークの追加) ASP.NET Web Pages (Razor) の web サイトにします。
> 
> 学習内容。
> 
> - ページにイメージを動的に追加する方法。
> - ユーザーがイメージをアップロードできるようにする方法。
> - イメージのサイズを変更する方法。
> - 反転やイメージを回転させる方法。
> - ウォーターマーク イメージを追加する方法。
> - ウォーターマークとしてイメージを使用する方法。
> 
> この記事で導入された機能のプログラミング、ASP.NET を次に示します。
> 
> - `WebImage`ヘルパー。
> - `Path`オブジェクトで、パスとファイル名を操作できるメソッドを提供します。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されるソフトウェアのバージョン
> 
> 
> - ASP.NET Web Pages (Razor) 2
> - WebMatrix 2
>   
> 
> このチュートリアルは、WebMatrix 3 でも機能します。


<a id="Adding_an_Image"></a>
## <a name="adding-an-image-to-a-web-page-dynamically"></a>Web ページにイメージを動的に追加します。

Web サイトの開発中は、web サイトに、個々 のページにイメージを追加することができます。 ユーザーのプロファイル写真を追加するなどのタスクに役立つのイメージをアップロードすることもできます。

HTML を使用する場合は、サイト、イメージが既に使用可能なページに表示する、`<img>`このような要素。

[!code-html[Main](9-working-with-images/samples/sample1.html)]

イメージを動的に表示できるようにする必要がありますが、場合によっては、&#8212;ページが実行されるまで表示するイメージの内容は、わかりません。

このセクションの手順では、ユーザーがイメージ名の一覧からイメージ ファイル名を指定する実行時にイメージを表示する方法を示します。 イメージの名前をドロップダウン リストから選択して、ページを送信すると、選択したイメージが表示されます。

![[イメージ]](9-working-with-images/_static/image1.jpg "ch9images 1.jpg")

1. WebMatrix で、新しい web サイトを作成します。
2. という名前の新しいページを追加*DynamicImage.cshtml*します。
3. Web サイトのルート フォルダーに新しいフォルダーを追加し、名前*イメージ*します。
4. 次の 4 つのイメージを追加、*イメージ*作成したフォルダーです。 (すべてのイメージには、便利なはあるがそれらをページに適合する必要があります)。イメージの名前を変更*Photo1.jpg*、 *Photo2.jpg*、 *Photo3.jpg*、および*Photo4.jpg*します。 (使用しない*Photo4.jpg*このプロシージャが使用しますが、記事の後半)。
5. 4 つのイメージは読み取り専用にマークしていないことを確認します。
6. 次のように、ページで、既存のコンテンツを置き換えます。

    [!code-cshtml[Main](9-working-with-images/samples/sample2.cshtml)]

    ページの本文がドロップダウン リスト (、`<select>`要素) という`photoChoice`します。 リストが 3 つのオプション、および`value`各リストのオプションの属性に格納されているイメージの 1 つの名前を持つ、*イメージ*フォルダー。 リストでのようなフレンドリ名を選択します。 ユーザーは、基本的に、&quot;写真 1&quot;、し、渡しますが、 *.jpg*ページが送信されたときに、ファイル名。

    コードから取得できます (つまり、イメージ ファイル名) のユーザーの選択リストを読み取って`Request["photoChoice"]`します。 まず、かどうか、選択範囲があるすべての参照してください。 発生した場合は、イメージのフォルダーの名前と、ユーザーのイメージ ファイル名で構成されるイメージのパスを構築します。 (パスを作成しようとしたでは nothing を使用する必要があるかどうか`Request["photoChoice"]`エラーが発生したとします)。これは、結果、このような相対パス。

    *images/Photo1.jpg*

    パスがという名前の変数に格納されている`imagePath`ページの後半で必要です。

    本文にも、`<img>`選択ユーザー イメージを表示するために使用する要素。 `src`静的要素の表示を行う場合と、ファイル名または URL に属性が設定されていません。 代わりに設定されている`@imagePath`、つまりコードで設定したパスからその値を取得します。

    初めてページが実行されるはありません、表示するイメージ、ユーザーには、何も選択されていないためです。 これは通常からといって、`src`属性は空にして、イメージが赤いとして表示&quot;x&quot; (または任意のイメージが見つからない場合に、ブラウザーを表示します)。 これを防ぐためには、配置する、`<img>`内の要素、`if`ブロックをテストするかどうか、`imagePath`変数が含まれるものです。 ユーザーが、選択を行った場合`imagePath`パスが含まれています。 場合は、ユーザーがイメージを選択していないか、これが初めてである場合は、ページが表示されます、`<img>`要素は表示もされません。
7. ファイルを保存し、ブラウザーでページを実行します。 (内でページが選択されていることを確認、**ファイル**ワークスペースを実行する前にします)。
8. ドロップダウン リストからイメージを選択してクリックして**サンプル イメージ**します。 さまざまな選択肢に異なるイメージが表示されることを確認します。

<a id="Uploading_an_Image"></a>
## <a name="uploading-an-image"></a>イメージのアップロード

前の例は、イメージを動的に表示する方法を示しましたが、web サイトに存在したイメージのみで機能しました。 この手順では、ユーザーがページに表示されるイメージをアップロードできるようにする方法を示します。 ASP.NET を使用して、実行時にイメージを操作することができます、`WebImage`ヘルパーで、作成、操作、および画像を保存できるメソッドがあります。 `WebImage`ヘルパーはすべて、一般的な web のイメージ ファイルの種類などをサポートしている *.jpg*、 *.png*、および *.bmp*します。 この記事では、全体で使用する *.jpg*が、イメージはイメージの種類のいずれかで使用できます。

![[イメージ]](9-working-with-images/_static/image2.jpg "ch9images 2.jpg")

1. 新しいページを追加し、名前*UploadImage.cshtml*します。
2. 次のように、ページで、既存のコンテンツを置き換えます。 

    [!code-cshtml[Main](9-working-with-images/samples/sample3.cshtml)]

    テキストの本文には、`<input type="file">`要素で、アップロードするファイルを選択できます。 クリックすると**送信**フォームと、選択ファイルを送信します。

    使用して、アップロードされたイメージを取得する、`WebImage`ヘルパーで、あらゆる種類のイメージを操作するための便利なメソッドを持ちます。 具体的を使用する`WebImage.GetImageFromRequest`(ある場合) にアップロードされたイメージを取得し、という名前の変数に格納する`photo`します。

    この例では作業の多くは、取得およびファイルとパス名を設定する必要があります。 問題は、ユーザーがアップロードされたイメージの名前 (および名のみ) を取得しのイメージを格納しようしている新しいパスを作成することです。 ユーザーは、同じ名前を持つ複数のイメージをアップロード可能性のある可能性があります、ため少し余分なコードを使用する一意の名前を作成し、ユーザーが既存の写真を上書きしないことを確認します。

    イメージを実際にアップロードされた場合 (テスト`if (photo != null)`)、イメージから、イメージの名前を取得する`FileName`プロパティ。 ユーザーは、イメージをアップロードする際`FileName`ユーザーのコンピューターからのパスを含む、ユーザーの元名が含まれています。 次のようになります。

    *C:\Users\Joe\Pictures\SamplePhoto1.jpg*

    ただし、すべてのパス情報をしたくない&#8212;する実際のファイル名 (*SamplePhoto1.jpg*)。 パスからのファイルだけを除去するを使用して、`Path.GetFileName`メソッドは、次のようにします。

    [!code-csharp[Main](9-working-with-images/samples/sample4.cs)]

    新しい一意のファイル名は、元の名前に GUID を追加することで作成します。 (詳細については、Guid は、次を参照してください[について Guid](#SB_AboutGUIDs)この記事で後述します。)。イメージの保存に使用できる完全なパスを構築します。 ファイルのパスは、新しいファイル名、フォルダー (イメージ)、および現在の web サイトの場所の構成します。

    > [!NOTE]
    > コード内のファイルを保存するために、*イメージ*フォルダー、アプリケーション必要がある読み取り/書き込みフォルダーのアクセスを許可します。 開発用コンピューターにこれは通常、問題ありません。 ただし、ホスティング プロバイダーの web サーバーにサイトを発行するときは、これらのアクセス許可を明示的に設定する必要があります。 ホスティング プロバイダーのサーバーでこのコードを実行し、エラーが発生する場合は、これらのアクセス許可を設定する方法を確認するホスティング プロバイダーを確認します。

    最後に、保存を渡すへのパス、`Save`のメソッド、`WebImage`ヘルパー。 これは、新しい名前でアップロードされたイメージを格納します。 ファイルの次のようなメソッド:`photo.Save(@"~\" + imagePath)`します。 完全なパスに追加`@"~\"`、現在の web サイトの場所であります。 (については、`~`演算子を参照してください[Web プログラミングを使用して ASP.NET Razor 構文の概要](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths))。

    前の例のように、ページの本文に含まれる、`<img>`イメージを表示する要素。 場合`imagePath`が設定されている、`<img>`要素を表示し、その`src`属性に設定されて、`imagePath`値。
3. ブラウザーでページを実行します。
4. イメージをアップロードし、ページに表示されるかどうかを確認します。
5. サイトで、開く、*イメージ*フォルダー。 次のようにファイルの名前の新しいファイルが追加されたことを参照してください。 

    *45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto.png*

    これは、名前にプレフィックス付きの GUID でアップロードしたイメージです。 (独自のファイルが別の GUID を持つし、おそらく名前は異なる点が*MyPhoto.png*)。

> [!TIP] 
> 
> <a id="SB_AboutGUIDs"></a>
> ### <a name="about-guids"></a>Guid の詳細について
> 
> GUID (グローバルに一意の ID) は、このような形式で表示される、通常は識別子:`936DA01F-9ABD-4d9d-80C7-02AF85C822A8`します。 数字と文字 (A ~ F) から、GUID ごとに異なりますが、8-4-4-4-12 文字のグループの使用パターンに従うすべて。 (技術的には、GUID は 16 バイト/128 ビット数) です。GUID が必要なときは、GUID を生成する特殊なコードを呼び出すことができます。 Guid の背後にある考え方は膨大な数のサイズの違いの差 (3.4 × 10<sup>38</sup>) し、生成するためのアルゴリズム、結果の数は仮想的に保証の種類のいずれかを指定します。 したがって Guid は、同じ名前を 2 回使用しないことを保証する必要があるときに、モ ノの名前を生成する優れた方法です。 短所は、名前がコードでのみ使用されるときに使用される傾向があるので、Guid はユーザー フレンドリ、特にはありません。 もちろん、です。


<a id="Resizing_an_Image"></a>
## <a name="resizing-an-image"></a>イメージのサイズ変更

Web サイトがユーザーからのイメージを受け入れる場合表示、保存したりする前に、イメージのサイズを変更する可能性があります。 もう一度使用することができます、`WebImage`このヘルパー。

この手順では、サムネイルを作成し、web サイトで、サムネイルと元のイメージを保存するアップロードされたイメージのサイズを変更する方法を示します。 ページのサムネイルを表示し、ハイパーリンクを使用すると、フルサイズのイメージにユーザーをリダイレクトします。

![[イメージ]](9-working-with-images/_static/image3.jpg "ch9images 3.jpg")

1. という名前の新しいページを追加*Thumbnail.cshtml*します。
2. *イメージ*フォルダー、という名前のサブフォルダーを作成する*thumbs*します。
3. 次のように、ページで、既存のコンテンツを置き換えます。 

    [!code-cshtml[Main](9-working-with-images/samples/sample5.cshtml)]

    このコードは、前の例のコードに似ています。 違いは、2 回、1 回は、通常、このコードは、イメージを保存します。 画像のサムネイルのコピーを作成した後に 1 回です。 まず、アップロードされたイメージを取得し、保存、*イメージ*フォルダー。 サムネイル イメージの新しいパスを作成します。 実際には、サムネイルを作成するを呼び出す、`WebImage`ヘルパーの`Resize`60 によって 60 ピクセル イメージを作成するメソッド。 例では、縦横比を保持する方法と、イメージから (この場合、新しいサイズが実際には、画像を拡大) は拡大されるようにする方法を示します。 サイズを変更したイメージを保存し、 *thumbs*サブフォルダーです。

    同一のマークアップの末尾には、使用する`<img>`、動的な要素`src`条件付きでイメージを表示する前の例で見た属性。 この場合、サムネイルを表示します。 使用することも、`<a>`大きなバージョンのイメージへのハイパーリンクを作成する要素。 同様、`src`の属性、`<img>`設定、要素、`href`の属性、`<a>`要素内のあらゆるものを動的に`imagePath`します。 パスを URL として操作できることを確認に合格する`imagePath`を`Html.AttributeEncode`メソッドで、パス内の予約文字を URL で [ok] の文字に変換します。
4. ブラウザーでページを実行します。
5. 写真をアップロードし、サムネイルが表示されていることを確認します。
6. サムネイルをクリックして、フルサイズの画像を参照してください。
7. *イメージ*と*イメージ/thumbs*、新しいファイルが追加されたことに注意してください。

<a id="Rotating_and_Flipping"></a>
## <a name="rotating-and-flipping-an-image"></a>回転とイメージの回転

`WebImage`ヘルパーすることもできます反転と回転イメージ。 この手順では、サーバーからイメージを取得し、イメージを上下 (垂直方向に) 反転し、保存して、ページに、反転されたイメージを表示する方法を示します。 この例で、サーバーに既にあるファイルを使用しているだけです (*Photo2.jpg*)。 実際のアプリケーションでは、前の例で行ったように、動的に取得する名前を持つイメージを反転させるは可能性があります。

![[イメージ]](9-working-with-images/_static/image4.jpg "ch9images 4.jpg")

1. という名前の新しいページを追加*FlipImage.cshtml*します。
2. 次のように、ページで、既存のコンテンツを置き換えます。 

    [!code-cshtml[Main](9-working-with-images/samples/sample6.cshtml)]

    コードを使用して、`WebImage`サーバーからイメージを取得するヘルパー。 前の例で、イメージを保存するために使用される同じ手法を使用するイメージへのパスを作成してを使用して、イメージを作成するときにそのパスを渡す`WebImage`:

    [!code-javascript[Main](9-working-with-images/samples/sample7.js)]

    イメージが見つかった場合は、新しいパスとファイル名を前の例で行ったようを構築します。 イメージを反転させるを呼び出す、`FlipVertical`メソッド、およびし、もう一度画像を保存します。

    使用して、イメージが再度表示ページで、`<img>`を持つ要素、`src`属性に設定`imagePath`します。
3. ブラウザーでページを実行します。 画像が*Photo2.jpg*上下に表示されます。
4. ページを更新するか、もう一度確認して、イメージ反転右側にあるをもう一度ページを要求します。

イメージを回転させるを呼び出す代わりに点を除いて、同じコードを使用して、`FlipVertical`または`FlipHorizontal`、呼び出す`RotateLeft`または`RotateRight`します。

<a id="Adding_a_Watermark"></a>
## <a name="adding-a-watermark-to-an-image"></a>ウォーターマークは、イメージへの追加

イメージを web サイトに追加する場合は、保存したり、ページ上に表示する前に、イメージに透かしを追加することができます。 ユーザーは、イメージに著作権情報を追加したり、そのビジネス名を提供する多くの場合、透かしを使用します。

![[イメージ]](9-working-with-images/_static/image5.jpg "ch9images 5.jpg")

1. という名前の新しいページを追加*Watermark.cshtml*します。
2. 次のように、ページで、既存のコンテンツを置き換えます。 

    [!code-cshtml[Main](9-working-with-images/samples/sample8.cshtml)]

    このコードは、コードのように、 *FlipImage.cshtml*前のページ (使用時間がこれが、 *Photo3.jpg*ファイル)。 呼び出すウォーターマークを追加する、`WebImage`ヘルパーの`AddTextWatermark`メソッド、イメージを保存する前にします。 呼び出しで`AddTextWatermark`、テキストを渡す&quot;マイ透かし&quot;、黄色、フォントの色を設定および arial フォント ファミリを設定します。 (ここでは、表示されませんが、`WebImage`ヘルパーでは不透明度、フォント ファミリとフォント サイズ、および透かしテキストの位置を指定することもできます)。イメージを保存すると、読み取り専用にする必要がありますできません。

    使用してページにイメージを表示する前に見たよう、 `<img>` src 属性を持つ要素を設定`@imagePath`します。
3. ブラウザーでページを実行します。 画像の右下隅にあるテキスト"My Watermark"に注意してください。

<a id="Using_an_Image_as_a_Watermark"></a>
## <a name="using-an-image-as-a-watermark"></a>ウォーターマークとしてイメージを使用します。

透かしのテキストではなく、別のイメージを使用できます。 ユーザーは、透かしとして会社のロゴなどのイメージを使用することがあります。 または著作権情報のテキストではなくウォーターマーク イメージを使用します。

![[イメージ]](9-working-with-images/_static/image6.jpg "ch9images 6.jpg")

1. という名前の新しいページを追加*ImageWatermark.cshtml*します。
2. イメージの追加、*イメージ*フォルダー、ロゴとして使用し、イメージの名前を変更できます*MyCompanyLogo.jpg*します。 このイメージは、表示されていることが明確に 80 ピクセル、高さ 20 ピクセルに設定されている場合、イメージを使用する必要があります。
3. 次のように、ページで、既存のコンテンツを置き換えます。 

    [!code-cshtml[Main](9-working-with-images/samples/sample9.cshtml)]

    これは、前の例のコードのもう 1 つのバリエーションです。 この場合は、呼び出す`AddImageWatermark`ウォーターマークのイメージをターゲット イメージに追加する (*Photo3.jpg*) イメージを保存する前にします。 呼び出すと`AddImageWatermark`、80 ピクセルを 20 ピクセル、高さ、幅を設定します。 *MyCompanyLogo.jpg*イメージは水平方向に中央に配置され、ターゲット画像の下部にある垂直方向に整列します。 不透明度が 100% に設定されているし、10 ピクセルの余白が設定されます。 ウォーターマーク イメージがターゲットのイメージよりも大きい場合は、何も起こりません。 ウォーターマーク イメージが対象のイメージより大きい、ゼロに透かしの画像の埋め込みを設定すると、透かしは無視されます。

    使用してイメージを表示する前に、として、`<img>`要素と動的な`src`属性。
4. ブラウザーでページを実行します。 メイン イメージの下部にあるウォーターマークの画像が表示されることに注意してください。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース


[ASP.NET Web ページ サイトでファイルの使用](https://go.microsoft.com/fwlink/?LinkId=202896)

[ASP.NET Web ページの Razor 構文を使用したプログラミングの概要](https://go.microsoft.com/fwlink/?LinkID=251587)
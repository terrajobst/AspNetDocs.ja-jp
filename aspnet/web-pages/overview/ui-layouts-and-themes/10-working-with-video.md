---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: ASP.NET Web ページ (Razor) サイトでビデオを表示する |Microsoft Docs
author: Rick-Anderson
description: この章では、Razor 構文ページを使用して ASP.NET Web ページにビデオを表示する方法について説明します。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510382"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a>ASP.NET Web ページ (Razor) サイトでビデオを表示する

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ASP.NET Web ページ (Razor) web サイトでビデオ (メディア) プレーヤーを使用して、サイトに保存されているビデオをユーザーが表示できるようにする方法について説明します。 ASP.NET Web ページ Razor 構文では、Flash (*swf*)、Media Player ( *.wmv*)、および Silverlight ( *.xap*) のビデオを再生できます。
> 
> ここでは、次の内容について学習します。
> 
> - ビデオプレーヤーを選択する方法。
> - Web ページにビデオを追加する方法。
> - ビデオプレーヤーの属性を設定する方法。
> 
> この記事で紹介する ASP.NET Razor ページ機能を次に示します。
> 
> - `Video` ヘルパー。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 2
> - WebMatrix 2
>   
> 
> このチュートリアルでは、WebMatrix 3 も使用できます。

## <a name="introduction"></a>はじめに

サイトにビデオを表示することもできます。 これを行う1つの方法は、既にビデオがあるサイト (YouTube など) にリンクすることです。 これらのサイトからのビデオを自分のページに直接埋め込む場合は、通常、サイトから HTML マークアップを取得して、ページにコピーすることができます。 たとえば、次の例は YouTube ビデオを埋め込む方法を示しています。

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

自分の web サイトにあるビデオを (公共のビデオ共有サイトではなく) 再生する場合、このような埋め込みマークアップを使用して直接リンクすることはできません。 ただし、`Video` ヘルパーを使用してサイトからビデオを再生できます。このヘルパーは、メディアプレーヤーをページに直接レンダリングします。

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a>ビデオプレーヤーの選択

ビデオファイルには多くの形式があり、各形式には通常、別のプレーヤーが必要で、プレーヤーを構成する別の方法が必要です。 ASP.NET Razor ページでは、`Video` ヘルパーを使用して web ページでビデオを再生できます。 `Video` ヘルパーは、ビデオを web ページに埋め込むプロセスを簡略化します。これは、ビデオをページに追加するために通常使用される `object` と `embed` HTML 要素を自動的に生成するためです。

`Video` helper では、次のメディアプレーヤーがサポートされています。

- Adobe Flash
- Windows MediaPlayer
- Microsoft Silverlight

### <a name="the-flash-player"></a>Flash Player

`Video` ヘルパーの `Flash` プレーヤーを使用すると、web ページで Flash ビデオ (*swf*ファイル) を再生できます。 少なくとも、ビデオファイルへのパスを指定する必要があります。 パスだけを指定した場合、player は現在のバージョンの Flash で設定されている既定値を使用します。 一般的な既定の設定は次のとおりです。

- ビデオは、既定の幅と高さを使用して、背景色なしで表示されます。
- ビデオは、ページが読み込まれるときに自動的に再生されます。
- ビデオは、明示的に停止されるまで継続的にループされます。
- ビデオは、特定のサイズに合わせてビデオをトリミングするのではなく、すべてのビデオを表示するようにスケーリングされています。
- ビデオがウィンドウで再生されます。

### <a name="the-mediaplayer-player"></a>MediaPlayer プレーヤー

`Video` ヘルパーの `MediaPlayer` プレーヤーを使用すると、web ページで Windows Media ビデオ ( *.wmv*ファイル)、windows media audio ( *.wma*ファイル)、および mp3 ( *.mp3*ファイル) を再生できます。 再生するメディアファイルのパスを含める必要があります。その他のパラメーターはすべて省略可能です。 パスのみを指定した場合、windows media player では、次のように、現在のバージョンの MediaPlayer によって設定された既定の設定が使用されます。

- ビデオは、既定の幅と高さを使用して表示されます。
- ビデオは、ページが読み込まれるときに自動的に再生されます。
- ビデオは1回再生されます (ループしません)。
- プレーヤーには、ユーザーインターフェイスのすべてのコントロールが表示されます。
- ビデオがウィンドウで再生されます。

### <a name="the-silverlight-player"></a>Silverlight プレーヤー

`Video` ヘルパーの `Silverlight` プレーヤーを使用すると、Windows Media ビデオ ( *.wmv*ファイル)、Windows media Audio ( *.wma*ファイル)、mp3 ( *.mp3*ファイル) を再生できます。 Silverlight ベースのアプリケーションパッケージ ( *.xap*ファイル) を指すように path パラメーターを設定する必要があります。 また、幅と高さのパラメーターも設定する必要があります。 その他のパラメーターはすべて省略可能です。 Silverlight プレーヤーをビデオに使用する場合、必要なパラメーターのみを設定すると、Silverlight プレーヤーは背景色なしでビデオを表示します。

> [!NOTE]
> Silverlight をまだ理解していない場合、 *.xap*ファイルは圧縮されたファイルで*あり、.xaml*ファイル、アセンブリ内のマネージコード、およびオプションのリソースのレイアウト命令が含まれています。 Silverlight アプリケーションプロジェクトとして、Visual Studio で *.xap*ファイルを作成できます。

`Silverlight` video player は、windows media player 用に指定した設定と *.xap*ファイルで提供されている設定の両方を使用します。

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a>MIME の種類
> 
> ブラウザーがファイルをダウンロードすると、ファイルの種類が、表示されるドキュメントに指定されている MIME の種類と一致することが確認されます。 MIME の種類は、ファイルのコンテンツの種類またはメディアの種類です。 `Video` helper は、次の MIME の種類を使用します。
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a>Flash (swf) ビデオの再生

この手順では、*サンプルの swf*という名前の Flash ビデオを再生する方法について説明します。 この手順では、サイトに*Media*という名前のフォルダーがあり、そのフォルダーに*swf*ファイルがあることを前提としています。

1. 「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだ追加していない場合)。
2. Web サイトで、ページを追加し、 *FlashVideo*という名前を指定します。
3. 次のマークアップをページに追加します。 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. ブラウザーでページを実行します。 (実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。ページが表示され、ビデオが自動的に再生されます。 

    ![絵](10-working-with-video/_static/image1.jpg "ch08_video-1")

Flash ビデオの `quality` パラメーターは、`low`、`autolow`、`autohigh`、`medium`、`high`、および `best`に設定できます。

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

`scale` パラメーターを使用して、特定のサイズで再生するように Flash ビデオを変更することができます。これは、次のように設定できます。

- [https://login.microsoftonline.com/consumers/](`showall`) これにより、元の縦横比を維持しながらビデオ全体が表示されるようになります。 ただし、右端に境界線が表示される場合があります。
- [https://login.microsoftonline.com/consumers/](`noorder`) これにより、元の縦横比を維持しながらビデオが拡大縮小されますが、トリミングされる可能性があります。
- [https://login.microsoftonline.com/consumers/](`exactfit`) これにより、元の縦横比を維持せずにビデオ全体が表示されるようになりますが、歪みが発生する可能性があります。

`scale` パラメーターを指定しない場合、ビデオ全体が表示され、元の縦横比はトリミングされることなく維持されます。 次の例では、`scale` パラメーターを使用する方法を示します。

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

Flash player では、`windowMode`という名前のビデオモード設定がサポートされています。 これを `window`、`opaque`、および `transparent`に設定できます。 既定では、`windowMode` は `window`に設定されます。これにより、ビデオが web ページ上の別のウィンドウに表示されます。 `opaque` の設定は、web ページ上のビデオの背後にあるすべてを非表示にします。 `transparent` 設定を使用すると、ビデオの一部が透明であると想定して、web ページの背景をビデオに表示できます。

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a>MediaPlayer ( *.wmv*) ビデオの再生

次の手順は、 *media*フォルダーにある*サンプル .wmv*という名前のウィンドウメディアビデオを再生する方法を示しています。

1. 「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。
2. *MediaPlayerVideo*という名前の新しいページを作成します。
3. 次のマークアップをページに追加します。 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. ブラウザーでページを実行します。 ビデオが自動的に読み込まれ、再生されます。 

    ![絵](10-working-with-video/_static/image2.jpg "ch08_video-2")

`playCount` は、ビデオを自動的に再生する回数を示す整数に設定できます。

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

`uiMode` パラメーターを使用すると、ユーザーインターフェイスに表示されるコントロールを指定できます。 `uiMode` は、`invisible`、`none`、`mini`、または `full`に設定できます。 `uiMode` パラメーターを指定しない場合は、ビデオウィンドウに加えて、ステータスウィンドウ、シークバー、コントロールボタン、およびボリュームコントロールと共にビデオが表示されます。 プレーヤーを使用してオーディオファイルを再生する場合も、これらのコントロールが表示されます。 `uiMode` パラメーターを使用する方法の例を次に示します。

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

既定では、オーディオはビデオが再生されるときにオンになります。 オーディオをミュートするには、`mute` パラメーターを true に設定します。

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

`volume` パラメーターを 0 ~ 100 の値に設定することにより、MediaPlayer ビデオのオーディオレベルを制御できます。 既定値は 50 です。 次に例を示します。

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a>Silverlight ビデオの再生

この手順では、 *Media*という名前のフォルダーにある、Silverlight *.xap*ページに含まれているビデオを再生する方法について説明します。

1. 「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。
2. *SilverlightVideo*という名前の新しいページを作成します。
3. 次のマークアップをページに追加します。 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. ブラウザーでページを実行します。 

    ![絵](10-working-with-video/_static/image3.jpg "ch08_video-3")

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>その他のリソース

[Silverlight の概要](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)

[Flash オブジェクトと埋め込みタグ属性](http://kb2.adobe.com/cps/127/tn_12701.html)

[Windows Media Player 11 SDK PARAM タグ](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)

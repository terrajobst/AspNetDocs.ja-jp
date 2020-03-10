---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: ソーシャルネットワークを ASP.NET Web ページ (Razor) サイトに追加する |Microsoft Docs
author: Rick-Anderson
description: この章では、サイトをソーシャルネットワークサービスと統合する方法について説明します。 この章では、ユーザーに web サイトのブックマーク/リンクを許可する方法について説明します。
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 1637464b0473bba8133acbbf8918d92b4f552701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422956"
---
# <a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a>ASP.NET Web ページ (Razor) サイトへのソーシャルネットワークの追加

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、Facebook、Twitter、Reddit、Digg のソーシャルネットワークリンクを ASP.NET Web ページ (Razor) web サイトのページに追加する方法と、Twitter フィード、Xbox ゲーマーカード、Gravatar イメージを含める方法について説明します。
> 
> ここでは、次の内容について学習します。
> 
> - サイトのブックマーク/リンクをユーザーに許可する方法。
> - Twitter フィードを追加する方法。
> - Facebook の**ような**ボタンをページに追加する方法。
> - Gravatar.com イメージをレンダリングする方法。
> - Xbox ゲーマーカードをサイトに表示する方法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 2
> - ASP.NET Web Helper Library (NuGet パッケージ)
>   
> 
> このチュートリアルでは、ASP.NET Web Helper ライブラリを使用するパーツを除き、ASP.NET Web ページ3でも使用できます。

<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a>ソーシャルネットワークサイトでの Web サイトのリンク

サイトで何らかの問題が発生した場合は、多くの場合、友人と共有したいと考えています。 これを簡単にするには、ユーザーがクリックして Digg、Reddit、Facebook、Twitter などのサイトでページを共有できるようにするグリフ (アイコン) を表示します。

これらのグリフを表示するには、`LinkSharecode` ヘルパーをページに追加します。 ページにアクセスするユーザーは、個々のグリフをクリックできます。 そのソーシャルネットワークサイトのアカウントを持っている場合は、そのサイトのページへのリンクを投稿できます。

![画像 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. 「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだ追加していない場合)。- *listlinkshare. cshtml*という名前のページを作成し、次のマークアップを追加します。

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    この例では、`LinkShare` ヘルパーを実行すると、ページタイトルがパラメーターとして渡され、そのページタイトルがソーシャルネットワークサイトに渡されます。 ただし、任意の文字列を渡すことができます。 この例では、一覧に含めるソーシャルネットワークサイトも指定します。 サイトに関連するソーシャルネットワークサイトを指定できます。
2. ブラウザーで*Listlinkshare. cshtml*ページを実行します。 (実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。
3. サインアップしているいずれかのサイトのグリフをクリックします。 リンクを選択すると、選択したソーシャルネットワークサイトのページに移動し、リンクを共有することができます。 たとえば、Reddit リンクをクリックすると、Reddit web サイトの [`submit to reddit`] ページが表示されます。

     ![画像 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a>Twitter フィードの追加

Twitter API の現在のバージョンと互換性のある Twitter ヘルパーの使用方法については、「 [twitter ヘルパー](../ui-layouts-and-themes/twitter-helper.md)」を参照してください。 この例では、さまざまなページのコードを簡単に再利用できるように、独自のヘルパーを記述する方法を示します。

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a>&quot; ボタンなどの Facebook &quot;を表示する

場合によっては、ヘルパーに依存するのではなく、ソーシャルネットワークプロバイダーから直接コードを取得するのが最善の方法です。 これは特に、ソーシャルネットワークプロバイダーがヘルパーを更新するよりも迅速にオプションを更新する場合に当てはまります。

Facebook 機能 ([Like] ボタンなど) をサイトに追加するには、 [developers.facebook.com](https://developers.facebook.com/)サイトからコードスニペットを取得します。 Facebook サイトでは、自分のツールを使用して、サイトに関連するコードスニペットを生成します。

次の強調表示されたコードは、developers.facebook.com サイトの同様のボタンツールから取得したコードです。 独自のアプリ ID を指定する必要があります。

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a>Gravatar イメージのレンダリング

*Gravatar* (&quot;グローバルに認識されるアバター&quot;) は、アバター &#8212;として複数の web サイトで使用できるイメージで、ユーザーを表すイメージです。 たとえば、Gravatar は、フォーラムの投稿、ブログのコメントなどで個人を識別できます。 (独自の Gravatar は、[Gravatar] web サイトの[http://www.gravatar.com/](http://www.gravatar.com/)に登録できます)。Web サイトのユーザーの名前または電子メールアドレスの横に画像を表示する場合は、Gravatar ヘルパーを使用できます。

この例では、自分を表す1つの Gravatar を使用しています。 Gravatar を使用するもう1つの方法は、サイトに登録するときに、ユーザーが自分の Gravatar アドレスを指定できるようにすることです。 (ユーザーが[ASP.NET Web ページサイトにセキュリティとメンバーシップを追加](https://go.microsoft.com/fwlink/?LinkId=202904)する方法については、「」を参照してください)。その後、そのユーザーの情報を表示するときに、ユーザーの名前を表示する場所に Gravatar を追加するだけで済みます。

1. 「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。
2. *Gravatar*という名前の新しい web ページを作成します。
3. 次のマークアップをファイルに追加します。 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    `Gravatar.GetHtml` メソッドは、ページに Gravatar イメージを表示します。 イメージのサイズを変更するには、数値を2番目のパラメーターとして含めることができます。 既定のサイズは80です。 80未満の数値を設定すると、画像が小さくなります。 80より大きい数値を指定すると、イメージが大きくなります。
4. `Gravatar.GetHtml` メソッドで、`<Your Gravatar account here>` を Gravatar アカウントに使用する電子メールアドレスに置き換えます。 (Gravatar アカウントを持っていない場合は、他のユーザーの電子メールアドレスを使用できます)。
5. ブラウザーでページを実行します。 このページには、指定した電子メールアドレスの2つの Gravatar イメージが表示されます。 2番目のイメージは、最初のイメージよりも小さくなります。 

    ![画像4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a>Xbox ゲーマーカードを表示する

Microsoft Xbox ゲームをオンラインで再生すると、各ユーザーに一意の ID が与えられます。 統計は、ゲーマーカードの形式で各プレーヤーに対して保持されます。このカードには、評判、ゲーマースコア、および最近再生したゲームが表示されます。 Xbox ゲーマーの場合は、`GamerCard` ヘルパーを使用して、サイト内のページにゲーマーカードを表示できます。

1. 「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。
2. *Xboxgamer. cshtml*という名前の新しいページを作成し、次のマークアップを追加します。

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    `GamerCard.GetHtml` プロパティを使用して、表示するゲーマーカードのエイリアスを指定します。
3. ブラウザーでページを実行します。 このページには、指定した Xbox ゲーマーカードが表示されます。

    ![画像 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)

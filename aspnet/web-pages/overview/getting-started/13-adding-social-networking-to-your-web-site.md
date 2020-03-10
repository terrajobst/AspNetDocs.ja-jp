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
# <a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a><span data-ttu-id="f6ce9-104">ASP.NET Web ページ (Razor) サイトへのソーシャルネットワークの追加</span><span class="sxs-lookup"><span data-stu-id="f6ce9-104">Adding Social Networking to ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="f6ce9-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f6ce9-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f6ce9-106">この記事では、Facebook、Twitter、Reddit、Digg のソーシャルネットワークリンクを ASP.NET Web ページ (Razor) web サイトのページに追加する方法と、Twitter フィード、Xbox ゲーマーカード、Gravatar イメージを含める方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-106">This article explains how to add social networking links for Facebook, Twitter, Reddit, and Digg to pages in an ASP.NET Web Pages (Razor) website, and how to include Twitter feeds, Xbox gamer cards, and Gravatar images.</span></span>
> 
> <span data-ttu-id="f6ce9-107">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="f6ce9-108">サイトのブックマーク/リンクをユーザーに許可する方法。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-108">How to let people bookmark/link your site.</span></span>
> - <span data-ttu-id="f6ce9-109">Twitter フィードを追加する方法。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-109">How to add a Twitter feed.</span></span>
> - <span data-ttu-id="f6ce9-110">Facebook の**ような**ボタンをページに追加する方法。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-110">How to add a Facebook **Like** button to pages.</span></span>
> - <span data-ttu-id="f6ce9-111">Gravatar.com イメージをレンダリングする方法。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-111">How to render Gravatar.com images.</span></span>
> - <span data-ttu-id="f6ce9-112">Xbox ゲーマーカードをサイトに表示する方法。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-112">How to display an Xbox gamer card on your site.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f6ce9-113">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="f6ce9-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f6ce9-114">ASP.NET Web ページ (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="f6ce9-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="f6ce9-115">ASP.NET Web Helper Library (NuGet パッケージ)</span><span class="sxs-lookup"><span data-stu-id="f6ce9-115">ASP.NET Web Helper Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="f6ce9-116">このチュートリアルでは、ASP.NET Web Helper ライブラリを使用するパーツを除き、ASP.NET Web ページ3でも使用できます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-116">This tutorial also works with ASP.NET Web Pages 3, except for parts that use the ASP.NET Web Helper Library.</span></span>

<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a><span data-ttu-id="f6ce9-117">ソーシャルネットワークサイトでの Web サイトのリンク</span><span class="sxs-lookup"><span data-stu-id="f6ce9-117">Linking Your Website on Social Networking Sites</span></span>

<span data-ttu-id="f6ce9-118">サイトで何らかの問題が発生した場合は、多くの場合、友人と共有したいと考えています。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-118">If people like something on your site, they often want to share it with friends.</span></span> <span data-ttu-id="f6ce9-119">これを簡単にするには、ユーザーがクリックして Digg、Reddit、Facebook、Twitter などのサイトでページを共有できるようにするグリフ (アイコン) を表示します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-119">You can make this easy by displaying glyphs (icons) that people can click to share a page on Digg, Reddit, Facebook, Twitter, or similar sites.</span></span>

<span data-ttu-id="f6ce9-120">これらのグリフを表示するには、`LinkSharecode` ヘルパーをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-120">To display these glyphs, add the `LinkSharecode` helper to a page.</span></span> <span data-ttu-id="f6ce9-121">ページにアクセスするユーザーは、個々のグリフをクリックできます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-121">People who visit your page can click an individual glyph.</span></span> <span data-ttu-id="f6ce9-122">そのソーシャルネットワークサイトのアカウントを持っている場合は、そのサイトのページへのリンクを投稿できます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-122">If they have an account with that social networking site, they can then post a link to your page on that site.</span></span>

![画像 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. <span data-ttu-id="f6ce9-124">「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだ追加していない場合)。- *listlinkshare. cshtml*という名前のページを作成し、次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-124">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.- Create a page named *ListLinkShare.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    <span data-ttu-id="f6ce9-125">この例では、`LinkShare` ヘルパーを実行すると、ページタイトルがパラメーターとして渡され、そのページタイトルがソーシャルネットワークサイトに渡されます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-125">In this example, when the `LinkShare` helper runs, the page title is passed as a parameter, which in turn passes the page title to the social networking site.</span></span> <span data-ttu-id="f6ce9-126">ただし、任意の文字列を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-126">However, you could pass in any string you want.</span></span> <span data-ttu-id="f6ce9-127">この例では、一覧に含めるソーシャルネットワークサイトも指定します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-127">This example also specifies which social networking sites to include in the list.</span></span> <span data-ttu-id="f6ce9-128">サイトに関連するソーシャルネットワークサイトを指定できます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-128">You can specify the social networking sites that are relevant to your site.</span></span>
2. <span data-ttu-id="f6ce9-129">ブラウザーで*Listlinkshare. cshtml*ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-129">Run the *ListLinkShare.cshtml* page in a browser.</span></span> <span data-ttu-id="f6ce9-130">(実行する前に、 **[ファイル]** ワークスペースでページが選択されていることを確認してください)。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-130">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
3. <span data-ttu-id="f6ce9-131">サインアップしているいずれかのサイトのグリフをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-131">Click a glyph for one of the sites that you're signed up for.</span></span> <span data-ttu-id="f6ce9-132">リンクを選択すると、選択したソーシャルネットワークサイトのページに移動し、リンクを共有することができます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-132">The link takes you to the page on the selected social network site where you can share a link.</span></span> <span data-ttu-id="f6ce9-133">たとえば、Reddit リンクをクリックすると、Reddit web サイトの [`submit to reddit`] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-133">For example, if you click the Reddit link, you're taken to the `submit to reddit` page on the Reddit website.</span></span>

     ![画像 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a><span data-ttu-id="f6ce9-135">Twitter フィードの追加</span><span class="sxs-lookup"><span data-stu-id="f6ce9-135">Adding a Twitter Feed</span></span>

<span data-ttu-id="f6ce9-136">Twitter API の現在のバージョンと互換性のある Twitter ヘルパーの使用方法については、「 [twitter ヘルパー](../ui-layouts-and-themes/twitter-helper.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-136">For information about using a Twitter helper that is compatible with the current version of the Twitter API, see [Twitter helper](../ui-layouts-and-themes/twitter-helper.md).</span></span> <span data-ttu-id="f6ce9-137">この例では、さまざまなページのコードを簡単に再利用できるように、独自のヘルパーを記述する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-137">This example shows how to write your own helper so you can easily reuse the code from many pages.</span></span>

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a><span data-ttu-id="f6ce9-138">&quot; ボタンなどの Facebook &quot;を表示する</span><span class="sxs-lookup"><span data-stu-id="f6ce9-138">Displaying a Facebook &quot;Like&quot; Button</span></span>

<span data-ttu-id="f6ce9-139">場合によっては、ヘルパーに依存するのではなく、ソーシャルネットワークプロバイダーから直接コードを取得するのが最善の方法です。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-139">In some cases, your best option is to get the code directly from the social networking provider rather than relying on a helper.</span></span> <span data-ttu-id="f6ce9-140">これは特に、ソーシャルネットワークプロバイダーがヘルパーを更新するよりも迅速にオプションを更新する場合に当てはまります。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-140">This is especially true if the social network provider updates its options more quickly than the helper is updated.</span></span>

<span data-ttu-id="f6ce9-141">Facebook 機能 ([Like] ボタンなど) をサイトに追加するには、 [developers.facebook.com](https://developers.facebook.com/)サイトからコードスニペットを取得します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-141">To add Facebook features (such as the Like button) to your site, you can retrieve code snippets from the [developers.facebook.com](https://developers.facebook.com/) site.</span></span> <span data-ttu-id="f6ce9-142">Facebook サイトでは、自分のツールを使用して、サイトに関連するコードスニペットを生成します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-142">On the Facebook site, you use their tools to generate a code snippet that is relevant to your site.</span></span>

<span data-ttu-id="f6ce9-143">次の強調表示されたコードは、developers.facebook.com サイトの同様のボタンツールから取得したコードです。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-143">The following highlighted code is the code that was retrieved from the Like Button tool on the developers.facebook.com site.</span></span> <span data-ttu-id="f6ce9-144">独自のアプリ ID を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-144">You must provide your own app ID.</span></span>

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a><span data-ttu-id="f6ce9-145">Gravatar イメージのレンダリング</span><span class="sxs-lookup"><span data-stu-id="f6ce9-145">Rendering a Gravatar Image</span></span>

<span data-ttu-id="f6ce9-146">*Gravatar* (&quot;グローバルに認識されるアバター&quot;) は、アバター &#8212;として複数の web サイトで使用できるイメージで、ユーザーを表すイメージです。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-146">A *Gravatar* (a &quot;globally recognized avatar&quot;) is an image that can be used on multiple websites as your avatar &#8212; that is, an image that represents you.</span></span> <span data-ttu-id="f6ce9-147">たとえば、Gravatar は、フォーラムの投稿、ブログのコメントなどで個人を識別できます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-147">For example, a Gravatar can identify a person in a forum post, in a blog comment, and so on.</span></span> <span data-ttu-id="f6ce9-148">(独自の Gravatar は、[Gravatar] web サイトの[http://www.gravatar.com/](http://www.gravatar.com/)に登録できます)。Web サイトのユーザーの名前または電子メールアドレスの横に画像を表示する場合は、Gravatar ヘルパーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-148">(You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/).) If you want to display images next to people's names or email addresses on your website, you can use the Gravatar helper.</span></span>

<span data-ttu-id="f6ce9-149">この例では、自分を表す1つの Gravatar を使用しています。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-149">In this example, you're using a single Gravatar that represents yourself.</span></span> <span data-ttu-id="f6ce9-150">Gravatar を使用するもう1つの方法は、サイトに登録するときに、ユーザーが自分の Gravatar アドレスを指定できるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-150">Another way to use a Gravatar is to let people specify their Gravatar address when they register on your site.</span></span> <span data-ttu-id="f6ce9-151">(ユーザーが[ASP.NET Web ページサイトにセキュリティとメンバーシップを追加](https://go.microsoft.com/fwlink/?LinkId=202904)する方法については、「」を参照してください)。その後、そのユーザーの情報を表示するときに、ユーザーの名前を表示する場所に Gravatar を追加するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-151">(You can learn how to let people register in [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).) Then whenever you display information for that user, you can just add the Gravatar to where you display the user's name.</span></span>

1. <span data-ttu-id="f6ce9-152">「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-152">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="f6ce9-153">*Gravatar*という名前の新しい web ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-153">Create a new web page named *Gravatar.cshtml*.</span></span>
3. <span data-ttu-id="f6ce9-154">次のマークアップをファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-154">Add the following markup to the file:</span></span> 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    <span data-ttu-id="f6ce9-155">`Gravatar.GetHtml` メソッドは、ページに Gravatar イメージを表示します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-155">The `Gravatar.GetHtml` method displays the Gravatar image on the page.</span></span> <span data-ttu-id="f6ce9-156">イメージのサイズを変更するには、数値を2番目のパラメーターとして含めることができます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-156">To change the size of the image, you can include a number as a second parameter.</span></span> <span data-ttu-id="f6ce9-157">既定のサイズは80です。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-157">The default size is 80.</span></span> <span data-ttu-id="f6ce9-158">80未満の数値を設定すると、画像が小さくなります。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-158">Numbers less than 80 make the image smaller.</span></span> <span data-ttu-id="f6ce9-159">80より大きい数値を指定すると、イメージが大きくなります。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-159">Numbers greater than 80 make the image larger.</span></span>
4. <span data-ttu-id="f6ce9-160">`Gravatar.GetHtml` メソッドで、`<Your Gravatar account here>` を Gravatar アカウントに使用する電子メールアドレスに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-160">In the `Gravatar.GetHtml` methods, replace `<Your Gravatar account here>` with the email address that you use for your Gravatar account.</span></span> <span data-ttu-id="f6ce9-161">(Gravatar アカウントを持っていない場合は、他のユーザーの電子メールアドレスを使用できます)。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-161">(If you don't have a Gravatar account, you can use the email address of someone who does.)</span></span>
5. <span data-ttu-id="f6ce9-162">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-162">Run the page in your browser.</span></span> <span data-ttu-id="f6ce9-163">このページには、指定した電子メールアドレスの2つの Gravatar イメージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-163">The page displays two Gravatar images for the email address you specified.</span></span> <span data-ttu-id="f6ce9-164">2番目のイメージは、最初のイメージよりも小さくなります。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-164">The second image is smaller than the first.</span></span> 

    ![画像4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a><span data-ttu-id="f6ce9-166">Xbox ゲーマーカードを表示する</span><span class="sxs-lookup"><span data-stu-id="f6ce9-166">Displaying an Xbox Gamer Card</span></span>

<span data-ttu-id="f6ce9-167">Microsoft Xbox ゲームをオンラインで再生すると、各ユーザーに一意の ID が与えられます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-167">When people play Microsoft Xbox games online, each user has a unique ID.</span></span> <span data-ttu-id="f6ce9-168">統計は、ゲーマーカードの形式で各プレーヤーに対して保持されます。このカードには、評判、ゲーマースコア、および最近再生したゲームが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-168">Statistics are kept for each player in the form of a gamer card, which shows their reputation, gamer score, and recently played games.</span></span> <span data-ttu-id="f6ce9-169">Xbox ゲーマーの場合は、`GamerCard` ヘルパーを使用して、サイト内のページにゲーマーカードを表示できます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-169">If you're an Xbox gamer, you can show your gamer card on pages in your site by using the `GamerCard` helper.</span></span>

1. <span data-ttu-id="f6ce9-170">「 [ASP.NET Web ページサイトにヘルパーをインストール](https://go.microsoft.com/fwlink/?LinkId=252372)する」の説明に従って、ASP.NET Web ヘルパーライブラリを web サイトに追加します (まだインストールしていない場合)。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-170">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="f6ce9-171">*Xboxgamer. cshtml*という名前の新しいページを作成し、次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-171">Create a new page named *XboxGamer.cshtml* and add the following markup.</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    <span data-ttu-id="f6ce9-172">`GamerCard.GetHtml` プロパティを使用して、表示するゲーマーカードのエイリアスを指定します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-172">You use the `GamerCard.GetHtml` property to specify the alias for the gamer card to be displayed.</span></span>
3. <span data-ttu-id="f6ce9-173">ブラウザーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-173">Run the page in your browser.</span></span> <span data-ttu-id="f6ce9-174">このページには、指定した Xbox ゲーマーカードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f6ce9-174">The page displays the Xbox gamer card that you specified.</span></span>

    ![画像 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)

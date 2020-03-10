---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: 'パート 3: Views と Viewmodel |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート3では、ビューと Viewmodel について説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451132"
---
# <a name="part-3-views-and-viewmodels"></a>パート 3: Views と Viewmodel

( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。  
>   
> MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。  
>   
> このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート3では、ビューと Viewmodel について説明します。

ここまでで、コントローラーアクションから文字列を返していました。 これは、コントローラーがどのように動作するかを把握するのに便利な方法ですが、実際の web アプリケーションを構築する方法ではありません。 ここでは、サイトにアクセスするブラウザーに HTML を返す方が優れています。1つはテンプレートファイルを使用して、送信した HTML コンテンツを簡単にカスタマイズできるようにすることです。 このビューでは、まさにこのビューが実行されます。

## <a name="adding-a-view-template"></a>ビューテンプレートの追加

ビューテンプレートを使用するには、ActionResult を返すように HomeController Index メソッドを変更し、次のように View () を返すようにします。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

上記の変更は、文字列を返さずに、代わりに "ビュー" を使用して結果を返すことを示しています。

次に、適切なビューテンプレートをプロジェクトに追加します。 これを行うには、Index アクションメソッド内にテキストカーソルを置き、右クリックして [ビューの追加] を選択します。 [ビューの追加] ダイアログが表示されます。

![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)

[ビューの追加] ダイアログボックスを使用すると、ビューテンプレートファイルをすばやく簡単に生成できます。 既定では、[ビューの追加] ダイアログボックスに、作成するビューテンプレートの名前があらかじめ設定されているので、それを使用するアクションメソッドと一致します。 HomeController の Index () アクションメソッド内で [ビューの追加] コンテキストメニューを使用したので、上の [ビューの追加] ダイアログには、既定でビュー名として "Index" が設定されています。 このダイアログのオプションを変更する必要はありません。 [追加] ボタンをクリックしてください。

[追加] ボタンをクリックすると、Visual Web Developer によって \Views\Home ディレクトリに新しいインデックスの cshtml ビューテンプレートが作成され、まだ存在しない場合はフォルダーが作成されます。

![](mvc-music-store-part-3/_static/image2.png)

"Index. cshtml" ファイルの名前とフォルダーの場所は重要で、既定の ASP.NET MVC 名前付け規則に従います。 ディレクトリ名 \Views\Home は、HomeController という名前のコントローラーに一致します。 ビューテンプレート名 Index は、ビューを表示するコントローラーアクションメソッドに一致します。

ASP.NET MVC を使用すると、この名前付け規則を使用してビューを返すときに、ビューテンプレートの名前または場所を明示的に指定しなくても済むようになります。 HomeController 内に次のようなコードを記述すると、既定で \Views\Home\Index.cshtml view テンプレートがレンダリングされます。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

[ビューの追加] ダイアログボックスで [追加] ボタンをクリックした後、Visual Web Developer によって "Index. cshtml" ビューテンプレートが作成され、開かれました。 次に、インデックスの内容を示します。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

このビューでは Razor 構文が使用されています。これは、ASP.NET Web フォームと以前のバージョンの ASP.NET MVC で使用される Web フォームビューエンジンよりも簡潔です。 Web フォームビューエンジンは ASP.NET MVC 3 でも使用できますが、多くの開発者は、Razor ビューエンジンが ASP.NET MVC の開発に適していることを確認しています。

最初の3行は、ViewBag を使用してページタイトルを設定します。 この機能の詳細については、後で詳しく説明しますが、まずテキスト見出しのテキストを更新し、ページを表示してみましょう。 次に示すように、&lt;h2&gt; タグを更新して、"これはホームページです" と言います。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

アプリケーションを実行すると、新しいテキストがホームページに表示されることがわかります。

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a>一般的なサイト要素のレイアウトの使用

ほとんどの web サイトには、ナビゲーション、フッター、ロゴ画像、スタイルシート参照など、多くのページ間で共有されているコンテンツがあります。Razor ビューエンジンでは、/ビュー/共有フォルダー内に自動的に作成された \_Layout. cshtml という名前のページを使用して、管理が簡単になります。

![](mvc-music-store-part-3/_static/image4.png)

次に示す内容を表示するには、このフォルダーをダブルクリックします。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

個々のビューのコンテンツは @RenderBody() コマンドによって表示されます。また、の外部に表示されるすべての共通コンテンツは、\_Layout マークアップに追加できます。 MVC ミュージックストアには、サイト内のすべてのページのホームページと店舗領域へのリンクを含む共通ヘッダーを含めるようにします。そのため、その @RenderBody() ステートメントのすぐ上のテンプレートに追加します。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a>スタイルシートの更新

空のプロジェクトテンプレートには、検証メッセージを表示するために使用されるスタイルだけを含む非常に簡素化された CSS ファイルが含まれています。 このデザイナーでは、サイトのルックアンドフィールを定義するために追加の CSS とイメージを用意しているので、ここで追加します。

更新された CSS ファイルとイメージは、MvcMusicStore-Assets のコンテンツディレクトリに含まれています。このディレクトリは、 [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store)で入手できます。 次に示すように、Windows エクスプローラーで両方のファイルを選択し、Visual Web Developer のソリューションのコンテンツフォルダーにドロップします。

![](mvc-music-store-part-3/_static/image5.png)

既存のサイトの .css ファイルを上書きするかどうかを確認するメッセージが表示されます。 [はい] をクリックします。

![](mvc-music-store-part-3/_static/image6.png)

これで、アプリケーションのコンテンツフォルダーが次のように表示されるようになります。

![](mvc-music-store-part-3/_static/image7.png)

次に、アプリケーションを実行して、ホームページの変更内容を確認します。

![](mvc-music-store-part-3/_static/image8.png)

- 変更内容を確認してみましょう。ビューテンプレートは標準的な名前付け規則に従っているため、HomeController のインデックスアクションメソッドが見つかり、\Views\Home\Index.cshtmlView テンプレートが表示されています。
- ホームページには、\Views\Home\Index.cshtml view テンプレート内で定義されている簡単なウェルカムメッセージが表示されます。
- ホームページでは \_Layout テンプレートが使用されているため、ウェルカムメッセージは標準のサイト HTML レイアウト内に含まれています。

## <a name="using-a-model-to-pass-information-to-our-view"></a>モデルを使用してビューに情報を渡す

ハードコードされた HTML だけを表示するビューテンプレートでは、非常に興味深い web サイトを作成しません。 動的な web サイトを作成するには、代わりにコントローラーアクションからの情報をビューテンプレートに渡す必要があります。

モデルビューコントローラーパターンでは、モデルという用語は、アプリケーション内のデータを表すオブジェクトを指します。 多くの場合、モデルオブジェクトはデータベース内のテーブルに対応していますが、これは必要ありません。

ActionResult を返すコントローラーアクションメソッドは、モデルオブジェクトをビューに渡すことができます。 これにより、コントローラーは、応答を生成するために必要なすべての情報を完全にパッケージ化してから、この情報をビューテンプレートに渡して、適切な HTML 応答を生成するために使用できます。 これは動作を確認することで簡単に理解できるので、始めましょう。

まず、ストア内のジャンルとアルバムを表すモデルクラスをいくつか作成します。 まず、Genre クラスを作成してみましょう。 プロジェクト内の "モデル" フォルダーを右クリックし、[クラスの追加] オプションを選択して、ファイルに "Genre.cs" という名前を指定します。

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

次に、作成されたクラスに "パブリック文字列名" プロパティを追加します。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

*注: ご注意のために、{get; set;} という表記は、 C#の自動実装プロパティ機能を使用しています。これにより、バッキングフィールドを宣言しなくても、プロパティの利点を得ることができます。*

次に、同じ手順に従って、タイトルと Genre プロパティを持つアルバムクラス (Album.cs という名前の) を作成します。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

ここで、StoreController を変更して、モデルの動的な情報を表示するビューを使用できるようになりました。 -デモンストレーションの目的で、要求 ID に基づいてアルバムという名前を付けた場合は、次のビューのようにその情報を表示できます。

![](mvc-music-store-part-3/_static/image10.png)

まず、Store Details (ストアの詳細) アクションを変更することで、1つのアルバムの情報が表示されるようにします。 **StoreControllers**クラスの先頭に "using" ステートメントを追加して、MvcMusicStore 名前空間を含めます。そのため、アルバムクラスを使用するたびに MvcMusicStore を入力する必要はありません。 そのクラスの "using" セクションが次のように表示されます。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

次に、HomeController の Index メソッドで行ったように、文字列ではなく ActionResult を返すように Details controller アクションを更新します。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

これで、アルバムオブジェクトをビューに返すロジックを変更できるようになりました。 このチュートリアルの後半では、データベースからデータを取得しますが、ここでは "ダミーデータ" を使用して作業を開始します。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

*注: にC#慣れていない場合は、var を使用すると、アルバム変数が遅延バインディングされることを想定できます。これは適切ではありC#ません。コンパイラは、変数に割り当てられている内容に基づいて型の推論を使用して、アルバムの種類がアルバムであることを判別し、アルバムの種類としてローカルのアルバム変数をコンパイルします。そのため、コンパイル時のチェックと Visual Studio コードエディターのサポートが得られます。*

ここで、アルバムを使用して HTML 応答を生成するビューテンプレートを作成しましょう。 この作業を行う前に、[ビューの追加] ダイアログで新しく作成したアルバムクラスについて理解できるように、プロジェクトをビルドする必要があります。 プロジェクトをビルドするには、[⇨ Build MvcMusicStore のデバッグ] メニュー項目を選択します (追加のクレジットの場合は、Ctrl + Shift + B のショートカットを使用してプロジェクトをビルドします)。

![](mvc-music-store-part-3/_static/image11.png)

サポートクラスを設定したので、ビューテンプレートをビルドする準備ができました。 詳細メソッド内を右クリックし、[ビューの追加...] を選択します。コンテキストメニューから。

![](mvc-music-store-part-3/_static/image12.png)

HomeController の前に作成したのと同じように、新しいビューテンプレートを作成します。 StoreController から作成するため、既定では \Views\Store\Index.cshtml ファイルに生成されます。

以前とは異なり、[厳密に型指定されたビューを作成する] チェックボックスをオンにします。 次に、[データクラスの表示] ドロップダウンリストで "アルバム" クラスを選択します。 これにより、[ビューの追加] ダイアログボックスが表示され、使用するためにアルバムオブジェクトが渡されることを期待するビューテンプレートが作成されます。

![](mvc-music-store-part-3/_static/image13.png)

[追加] ボタンをクリックすると、次のコードを含む \Views\Store\Details.cshtml View テンプレートが作成されます。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

最初の行に注目してください。これは、このビューがアルバムクラスに厳密に型指定されていることを示します。 Razor ビューエンジンは、そのオブジェクトがアルバムオブジェクトに渡されたことを認識します。これにより、モデルプロパティに簡単にアクセスできるようになります。また、Visual Web Developer エディターで IntelliSense を利用することもできます。

&lt;h2&gt; タグを更新して、次のように、その行を変更することでアルバムの Title プロパティを表示できるようにします。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

@Model キーワードの後にピリオドを入力すると、IntelliSense がトリガーされることに注意してください。これは、アルバムクラスでサポートされるプロパティとメソッドを示しています。

ここで、プロジェクトを再実行し、/ストア/ページの URL にアクセスしてみましょう。 次のようなアルバムの詳細が表示されます。

![](mvc-music-store-part-3/_static/image14.png)

次に、ストアの参照アクションメソッドに対して同様の更新を行います。 メソッドを更新して ActionResult を返し、メソッドのロジックを変更して、新しい Genre オブジェクトを作成し、それをビューに返すようにします。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

Browse メソッドを右クリックし、[ビューの追加...] を選択します。コンテキストメニューから、厳密に型指定されたビューを追加して、Genre クラスに厳密に型指定されたを追加します。

![](mvc-music-store-part-3/_static/image15.png)

ビューコード (/Views/Store/Browse.cshtml) の &lt;h2&gt; 要素を更新して、ジャンル情報を表示します。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

次に、プロジェクトを再実行して、/ストアに移動してみましょう。Genre = Disco URL。 次のように、参照ページが表示されます。

![](mvc-music-store-part-3/_static/image16.png)

最後に、ストア**インデックス**のアクションメソッドとビューを少し複雑に更新して、ストア内のすべてのジャンルの一覧を表示してみましょう。 これを行うには、1つのジャンルだけではなく、モデルオブジェクトとしてジャンルのリストを使用します。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

ストアインデックスアクションメソッドを右クリックし、[前のビューを追加] を選択して、モデルクラスとして [ジャンル] を選択し、[追加] ボタンをクリックします。

![](mvc-music-store-part-3/_static/image17.png)

まず、@model 宣言を変更して、ビューが1つだけではなく複数の Genre オブジェクトを必要とすることを示します。 /ストアの最初の行を次のように変更します。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

これにより、複数の Genre オブジェクトを保持できるモデルオブジェクトを操作することを Razor ビューエンジンに通知します。 一般的なものであるため、IEnumerable&lt;Genre&gt;&lt;&gt; を使用しています。これは一般に、IEnumerable インターフェイスをサポートする任意のオブジェクト型に後でモデルの種類を変更できるためです。

次に、次の「完成したビューコード」に示されているように、モデル内の Genre オブジェクトをループ処理します。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

このコードを入力すると IntelliSense が完全にサポートされるので、「@Model」と入力すると、 種類が Genre の IEnumerable でサポートされているすべてのメソッドとプロパティが表示されます。

![](mvc-music-store-part-3/_static/image18.png)

"Foreach" ループ内では、Visual Web Developer は各項目の種類が Genre であることを認識しているため、ジャンルの種類ごとに IntelliSense が表示されます。

![](mvc-music-store-part-3/_static/image19.png)

次に、スキャフォールディング機能は Genre オブジェクトを調べ、それぞれに Name プロパティがあることを確認したので、ループ処理して出力します。また、個々の項目に対する編集、詳細、および削除のリンクも生成します。 この機能については、ストアマネージャーで後ほど説明しますが、ここでは単純なリストを使用します。

アプリケーションを実行して、[ストア] を参照すると、カウントとジャンルの一覧の両方が表示されていることがわかります。

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a>ページ間のリンクの追加

現在、ジャンルを一覧表示する/ストア URL では、ジャンル名が単にプレーンテキストとして一覧表示されます。 これを変更して、プレーンテキストではなく、ジャンル名を適切な/Store/browse URL にリンクさせます。これにより、"Disco" のような音楽のジャンルをクリックすると、"Disco" に移動します。 次のようなコードを使用して、これらのリンクを出力するように \Views\Store\Index.cshtml View テンプレートを更新することもできます **(これを入力しないでください)** 。

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

これは機能しますが、ハードコーディングされた文字列に依存しているため、後で問題が発生する可能性があります。 たとえば、コントローラーの名前を変更する場合は、コードを検索して、更新する必要があるリンクを探す必要があります。

別の方法として、HTML ヘルパーメソッドを利用することもできます。 ASP.NET MVC には、このようなさまざまな一般的なタスクを実行するために、ビューテンプレートコードから使用できる HTML ヘルパーメソッドが含まれています。 Html.actionlink () ヘルパーメソッドは特に便利であり、&gt; リンクの HTML &lt;を簡単に作成できます。また、URL パスが適切に URL エンコードされているかどうかなど、面倒な詳細も考慮します。

Html.actionlink () には、リンクに必要な量の情報を指定できるように、いくつかの異なるオーバーロードがあります。 最も単純なケースでは、クライアントでハイパーリンクがクリックされたときに、リンクテキストとアクションメソッドを指定するだけです。 たとえば、次の呼び出しを使用して、ストアの詳細ページの "/Store/" Index () メソッドにリンクすることができます。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

*注: この場合、現在のビューを表示しているのと同じコントローラー内の別のアクションにリンクするだけなので、コントローラー名を指定する必要はありませんでした。*

参照ページへのリンクではパラメーターを渡す必要があるので、次の3つのパラメーターを受け取る Html.actionlink メソッドの別のオーバーロードを使用します。

- 1. ジャンル名を表示するリンクテキスト
- 2. コントローラーアクション名 (参照)
- 3. ルートパラメーターの値。名前 (ジャンル) と値 (ジャンル名) の両方を指定します。

これらのリンクをまとめて、ストアインデックスビューへのリンクを次のように記述します。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

ここでプロジェクトをもう一度実行し、/Store/URL にアクセスすると、ジャンルの一覧が表示されます。 各ジャンルはハイパーリンクです。クリックすると、/Store/Browse? genre = *[genre]* URL に移動します。

![](mvc-music-store-part-3/_static/image3.jpg)

ジャンルリストの HTML は次のようになります。

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> [前へ](mvc-music-store-part-2.md)
> [次へ](mvc-music-store-part-4.md)

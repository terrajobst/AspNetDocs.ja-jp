---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: Visual Studio 2013 を使用した基本的な ASP.NET 4.5 Web フォームページの作成
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 5d13a51128eecd92a82cfd06054448582a348e11
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511078"
---
# <a name="using-visual-studio-2013-to-create-a-basic-aspnet-45-web-forms-page"></a>Visual Studio 2013 を使用した基本的な ASP.NET 4.5 Web フォームページの作成

[Erik Reitan](https://github.com/Erikre)

[!INCLUDE[](~/includes/rp.md)]

このチュートリアルでは、 [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)の web 開発環境の概要と、 [web 用 Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web)について説明します。 このチュートリアルでは、簡単な ASP.NET Web フォームページを作成し、新しいページを作成し、コントロールを追加し、コードを記述するための基本的な手法について説明します。

このチュートリアルでは、以下のタスクを行います。

- ファイルシステム Web フォームアプリケーションプロジェクトを作成する。
- Visual Studio について理解を深める。
- ASP.NET ページを作成しています。
- コントロールを追加しています。
- イベントハンドラーを追加しています。
- Visual Studio からのページの実行とテスト。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、以下が必要です。

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)または[Web 用 Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web)。 .NET Framework は自動的にインストールされます。 

    > [!NOTE] 
    > 
    > このチュートリアルシリーズでは、多くの場合、Web 用の Microsoft Visual Studio 2013 と Microsoft Visual Studio Express 2013 を Visual Studio と呼びます。  
    >   
    > Visual Studio を使用している場合、このチュートリアルでは、Visual Studio を初めて起動したときに設定の**Web 開発**コレクションが選択されていることを前提としています。 詳細については、「[方法: Web 開発環境の設定を選択する](https://msdn.microsoft.com/library/ff521558.aspx)」を参照してください。

## <a name="creating-a-web-application-project-and-a-page"></a>Web アプリケーションプロジェクトとページの作成

<a id="sectionToggle0"></a>

チュートリアルのこの部分では、Web アプリケーションプロジェクトを作成し、そこに新しいページを追加します。 また、HTML テキストを追加し、ブラウザーでページを実行します。

### <a name="to-create-a-web-application-project"></a>Web アプリケーションプロジェクトを作成するには

1. Microsoft Visual Studio を開きます。
2. **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。  
    ![ファイル メニュー](creating-a-basic-web-forms-page/_static/image1.png)

    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。
3. 左側にある [**テンプレート** -&gt; **Visual C#**  -&gt; **Web**テンプレート] グループを選択します。
4. 中央の列で **[ASP.NET Web アプリケーション]** を選択します。
5. プロジェクトに***Basicwebapp***という名前を指定し、 **[OK]** ボタンをクリックします。   
![[新しいプロジェクト] ダイアログ ボックス](creating-a-basic-web-forms-page/_static/image2.png)
6. 次に、 **[Web フォーム]** テンプレートを選択し、 **[OK]** ボタンをクリックしてプロジェクトを作成します。  
![[新しい ASP.NET プロジェクト] ダイアログ ボックス](creating-a-basic-web-forms-page/_static/image3.png)  

    Visual Studio によって、Web フォームテンプレートに基づく事前構築済みの機能を含む新しいプロジェクトが作成されます。 これは *、default.aspx ページ*、 *About .aspx*ページ、および*Contact .aspx*ページを提供するだけでなく、ユーザーが web サイトにログインできるように、ユーザーを登録して資格情報を保存するメンバーシップ機能も備えています。 新しいページが作成されると、既定では、Visual Studio によってページが**ソース**ビューに表示されます。このページでは、ページの HTML 要素を確認できます。 次の図は、 *Basicwebapp*という名前の新しい Web ページを作成した場合に**ソース**ビューに表示される内容を示しています。  
    ![ソース ビュー](creating-a-basic-web-forms-page/_static/image4.png)

### <a name="a-tour-of-the-visual-studio-web-development-environment"></a>Visual Studio Web 開発環境のツアー

ページを変更する前に、Visual Studio 開発環境について理解しておくと役に立ちます。 次の図は、Visual Studio で使用できるウィンドウとツール、および Web 用の Visual Studio Express を示しています。

> [!NOTE] 
> 
> この図は、既定のウィンドウとウィンドウの場所を示しています。 **[表示]** メニューを使用すると、他のウィンドウを表示したり、ユーザーの好みに合わせてウィンドウの位置を変更したりすることができます。 ウィンドウの配置が既に変更されている場合、表示される内容は図と一致しません。

 Visual Studio 環境

![Visual Studio 環境](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a>Web デザイナーについて理解する

上の図を確認し、テキストを次の一覧と照合します。これは、最も一般的に使用される windows およびツールを示しています。 (表示されているすべてのウィンドウとツールがここに記載されているわけではありませんが、前の図でマークされているもののみ)。

- ツールバー. テキストの書式設定、テキストの検索などを行うためのコマンドを提供します。 一部のツールバーは、 **[デザイン]** ビューで作業している場合にのみ使用できます。
- **ソリューションエクスプローラー**ウィンドウ。 Web アプリケーション内のファイルとフォルダーを表示します。
- ドキュメントウィンドウ。 タブ付きウィンドウで作業中のドキュメントを表示します。 タブをクリックして、ドキュメントを切り替えることができます。
- **プロパティ**ウィンドウ。 ページ、HTML 要素、コントロール、およびその他のオブジェクトの設定を変更できます。
- タブを表示します。 同じドキュメントのさまざまなビューを表示します。 **デザイン**ビューは、ほぼ WYSIWYG の編集サーフェイスです。 **ソース**ビューは、ページの HTML エディターです。 **分割**ビュードキュメントの**デザイン**ビューと**ソース**ビューの両方を表示します。 このチュートリアルの後半では、**デザイン**ビューと**ソース**ビューを使用します。 **デザイン**ビューで Web ページを開く場合は、 **[ツール]** メニューの **[オプション]** をクリックし、 **[HTML デザイナー]** ノードを選択し、 **[開始ページの開始]** オプションを変更します。
- **ツールボックス**。 ページにドラッグできるコントロールと HTML 要素を提供します。 **ツールボックス**要素は、共通の関数によってグループ化されます。
- 秒の**エクスプローラー**。 データベース接続を表示します。 サーバーエクスプローラー表示されていない場合は、[表示] メニューの [サーバーエクスプローラー] をクリックします。

### <a name="creating-a-new-aspnet-web-forms-page"></a>新しい ASP.NET Web フォームページの作成

**ASP.NET Web アプリケーション**プロジェクトテンプレートを使用して新しい Web フォームアプリケーションを作成すると、Visual Studio によって、 *default.aspx*という名前の ASP.NET ページ (Web フォームページ) とその他のいくつかのファイルとフォルダーが追加されます。 *Default.aspx*ページは、Web アプリケーションのホームページとして使用できます。 ただし、このチュートリアルでは、新しいページを作成して操作します。

### <a name="to-add-a-page-to-the-web-application"></a>Web アプリケーションにページを追加するには

1. *Default.aspx*ページを閉じます。 これを行うには、ファイル名が表示されているタブをクリックし、[閉じる] オプションをクリックします。
2. **ソリューションエクスプローラー**で、Web アプリケーション名 (このチュートリアルではアプリケーション名は**basicwebsite**) を右クリックし、[ -の**追加**] をクリックして &gt;**新しい項目**を追加します。   
**[新しい項目の追加]** ダイアログ ボックスが表示されます。
3. 左側の **[ C# Visual** -&gt; **Web**テンプレート] グループを選択します。 次に、中央の一覧から **[Web フォーム]** を選択し、 *firstwebpage ページ*にという名前を指定します。   
    ![[新しい項目の追加] ダイアログ ボックス](creating-a-basic-web-forms-page/_static/image6.png)
4. **[追加]** をクリックして、web ページをプロジェクトに追加します。  
新しいページが作成されて開きます。

### <a name="adding-html-to-the-page"></a>ページへの HTML の追加

チュートリアルのこの部分では、いくつかの静的テキストをページに追加します。

### <a name="to-add-text-to-the-page"></a>テキストをページに追加するには

1. ドキュメントウィンドウの下部にある **[デザイン]** タブをクリックして、**デザイン**ビューに切り替えます。

    デザインビューには、現在のページが WYSIWYG に似た方法で表示されます。 この時点では、ページにテキストやコントロールはありません。そのため、四角形の輪郭を示す破線を除き、ページは空白になります。 この四角形は、ページ上の**div**要素を表します。
2. 破線で囲まれた四角形の内側をクリックします。
3. 「 **Visual Web Developer へようこそ**」と入力し、 **enter**キーを2回押します。

    次の図は、 **[デザイン]** ビューで入力したテキストを示しています。

    ![デザインビューのようこそテキスト](creating-a-basic-web-forms-page/_static/image7.png "デザイン ビューの開始テキスト")
4. **ソース**ビューに切り替えます。

    **デザイン**ビューで入力したときに作成した HTML が**ソース**ビューに表示されます。  
    静的なテキスト](creating-a-basic-web-forms-page/_static/image8.png) を含む Web ページ ![

### <a name="running-the-page"></a>ページを実行しています

ページにコントロールを追加する前に、最初にコントロールを実行することができます。

### <a name="to-run-the-page"></a>ページを実行するには

1. **ソリューションエクスプローラー**で、[ *firstwebpage ページ*] を右クリックし、 **[スタートページとして設定]** を選択します。
2. CTRL キーを押し**ながら F5**キーを押して、ページを実行します。

    ページがブラウザーに表示されます。 作成したページのファイル名拡張子は *.aspx*ですが、現在は HTML ページと同じように実行されます。

    ブラウザーにページを表示するには、**ソリューションエクスプローラー**のページを右クリックし、 **[ブラウザーで表示]** を選択することもできます。
3. ブラウザーを閉じて、Web アプリケーションを停止します。

## <a name="adding-and-programming-controls"></a>コントロールの追加とプログラミング

<a id="sectionToggle1"></a>

次に、サーバーコントロールをページに追加します。 ボタン、ラベル、テキストボックス、その他の使い慣れたコントロールなどのサーバーコントロールは、Web フォームページの一般的なフォーム処理機能を提供します。 ただし、クライアントではなく、サーバー上で実行されるコードを使用してコントロールをプログラミングできます。

[ボタンコントロール、](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) [テキストボックス](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)コントロール、および[ラベル](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)コントロールをページに追加し、[ボタン](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)コントロールの[クリック](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)イベントを処理するコードを記述します。

### <a name="to-add-controls-to-the-page"></a>ページにコントロールを追加するには

1. **デザインビューに**切り替えるには、 **[デザイン]** タブをクリックします。
2. **[Visual Web Developer テキストへようこそ]** の末尾にカーソルを置き、 **enter**キーを5回押すと、 **[div]** 要素 ボックスにいくつかの領域が作成されます。
3. **ツールボックス**で、**標準**のグループがまだ展開されていない場合は展開します。  
表示するには、左側の **[ツールボックス]** ウィンドウを展開する必要があることに注意してください。
4. [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)コントロールをページにドラッグし、最初の行で **[Visual Web Developer へようこそ]** と表示されている **[div]** 要素 ボックスの中央にドロップします。
5. [ボタン](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)コントロールをページにドラッグし、[テキストボックス](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)コントロールの右側にドロップします。
6. [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)コントロールをページにドラッグし、[ボタン](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)コントロールの下の別の行にドロップします。
7. [テキストボックス](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)コントロールの上に挿入ポイントを置き、「**名前を入力**してください:」と入力します。

    この静的 HTML テキストは、 [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx)コントロールのキャプションです。 同じページに、静的な HTML コントロールとサーバーコントロールを混在させることができます。 次の図は、3つのコントロールが**デザイン**ビューにどのように表示されるかを示しています。

    ![デザインビューの3つのコントロール](creating-a-basic-web-forms-page/_static/image9.png "デザイン ビューの 3 つのコントロール")

### <a name="setting-control-properties"></a>コントロールのプロパティの設定

Visual Studio には、ページ上のコントロールのプロパティを設定するためのさまざまな方法が用意されています。 チュートリアルのこの部分では、**デザイン**ビューと**ソース**ビューの両方でプロパティを設定します。

### <a name="to-set-control-properties"></a>コントロールのプロパティを設定するには

1. 最初に、 **[表示]** メニューの [**その他のウィンドウ**を&gt;] をクリックして **[プロパティ**] ウィンドウを表示し、&gt;**プロパティウィンドウ** -ます。 または、 **F4**キーを選択して、 **[プロパティ]** ウィンドウを表示することもできます。
2. [ボタン](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)コントロールを選択し、 **[プロパティ]** ウィンドウで、 **[テキスト]** の値を **[表示名]** に設定します。 次の図に示すように、入力したテキストがデザイナーのボタンに表示されます。

    ![ボタンのテキストを設定する](creating-a-basic-web-forms-page/_static/image10.png "ボタン設定テキスト")
3. **ソース**ビューに切り替えます。

    **ソース**ビューサーバーコントロール用に Visual Studio によって作成された要素を含む、ページの HTML が表示されます。 コントロールは、HTML に似た構文を使用して宣言されます。ただし、タグには、プレフィックス**asp:** が使用され、 **runat =&quot;server&quot;** 属性が含まれる点が異なります。

    コントロールプロパティは属性として宣言されます。 たとえば、手順1で[ボタン](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)コントロールの[text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx)プロパティを設定した場合、実際には、コントロールのマークアップで**テキスト**属性を設定していました。

    > [!NOTE] 
    > 
    > すべてのコントロールは**フォーム**要素内にあり、 **runat =&quot;server&quot;** 属性も持っています。 **Runat =&quot;server&quot;** 属性と、コントロールタグの**asp:** prefix は、ページの実行時にサーバー上の ASP.NET によって処理されるようにコントロールをマークします。 &lt;の外部のコード**runat =&quot;server&quot;&gt;** および **&lt;script runat =&quot;server&quot;** 要素は変更されずにブラウザーに送信されます。そのため、ASP.NET コードは、開始タグに**runat = &gt;server&quot;** 属性が含まれている要素内に存在する必要があります。&quot;
4. 次に、 [Label](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)コントロールにプロパティを追加します。 **&lt;asp: label&gt;** タグの**asp: label**の直後に挿入ポイントを置き、 **space**キーを押します。

    ドロップダウンリストが表示され、[ラベル](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)コントロールに設定できる使用可能なプロパティの一覧が表示されます。 **IntelliSense**と呼ばれるこの機能を使用すると、ページ上のサーバーコントロール、HTML 要素、およびその他の項目の構文で**ソース**ビューを使用できます。 次の図は、[ラベル](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)コントロールの**IntelliSense**ドロップダウンリストを示しています。

    ![IntelliSense 属性](creating-a-basic-web-forms-page/_static/image11.png "IntelliSense 属性")
5. **[ForeColor]** を選択し、等号を入力します。

    IntelliSense では、色の一覧が表示されます。

    > [!NOTE] 
    > 
    > **IntelliSense**のドロップダウンリストは、コードを表示するときに**CTRL + J**キーを押すことでいつでも表示できます。
6. **[ラベル](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** コントロールのテキストの色を選択します。 白い背景に読み取るのに十分な暗い色を選択していることを確認します。

    **ForeColor**属性は、終わりの引用符を含め、選択した色で完成します。

### <a name="programming-the-button-control"></a>ボタンコントロールのプログラミング

このチュートリアルでは、ユーザーがテキストボックスに入力した名前を読み取り、[ラベル](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)コントロールに名前を表示するコードを記述します。

### <a name="add-a-default-button-event-handler"></a>既定のボタンイベントハンドラーを追加する

1. **デザイン**ビューに切り替えます。
2. [ボタン](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)コントロールをダブルクリックします。

    既定では、Visual Studio は分離コードファイルに切り替えて、[ボタン](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)コントロールの既定のイベント ( [click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)イベント) のスケルトンイベントハンドラーを作成します。 分離コードファイルは、(などのC#) サーバーコードから UI マークアップ (HTML など) を分離します。   
   カーソルがこのイベントハンドラー用に追加されたコードに配置されています。

    > [!NOTE] 
    > 
    > **デザイン**ビューでコントロールをダブルクリックすることは、イベントハンドラーを作成するいくつかの方法の1つです。
3. **Button1\_クリック**イベントハンドラーで、「 **Label1**の後にピリオド ( **.** )」と入力します。

    ラベルの**ID**の後にピリオド (**Label1**) を入力すると、次の図に示すように、Visual Studio では、[ラベル](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)コントロールに使用できるメンバーの一覧が表示されます。 メンバーは、通常、プロパティ、メソッド、またはイベントです。

    ![コードビューの IntelliSense](creating-a-basic-web-forms-page/_static/image12.png "コード ビューの IntelliSense")
4. 次のコード例に示すように、ボタンの**クリック**イベントハンドラーを完成させます。

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. **ソリューションエクスプローラー**で*firstwebpage ページ*を右クリックし、 **[マークアップの表示]** を選択して、HTML マークアップの**ソース**ビューの表示に戻ります。
6. **&lt;asp: Button&gt;** 要素までスクロールします。 **&lt;asp: Button&gt;** 要素には、 **[Onclick =&quot;Button1\_クリックして&quot;]** という属性があります。

    この属性は、ボタンの[click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)イベントを、前の手順でコード化したハンドラーメソッドにバインドします。

    イベントハンドラーメソッドには任意の名前を付けることができます。表示される名前は、Visual Studio によって作成された既定の名前です。 重要な点は、HTML の**OnClick**属性に使用される名前が、分離コードで定義されたメソッドの名前と一致する必要があることです。

### <a name="running-the-page"></a>ページを実行しています

これで、ページ上のサーバーコントロールをテストできるようになりました。

### <a name="to-run-the-page"></a>ページを実行するには

1. CTRL キーを押し**ながら F5**キーを押して、ブラウザーでページを実行します。 エラーが発生した場合は、上記の手順を再確認してください。
2. テキストボックスに名前を入力し、 **[表示名]** ボタンをクリックします。

    入力した名前が[ラベル](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)コントロールに表示されます。 このボタンをクリックすると、ページが Web サーバーにポストされます。 次に、ASP.NET はページを再作成し、コードを実行し (この場合は[ボタン](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)コントロールの[click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)イベントハンドラーが実行されます)、ブラウザーに新しいページを送信します。 ブラウザーでステータスバーを見ると、ボタンをクリックするたびに Web サーバーへのラウンドトリップが行われていることがわかります。
3. ブラウザーで、ページを右クリックし、 **[ソースの表示]** を選択して、実行中のページのソースを表示します。

    ページソースコードでは、サーバーコードなしで HTML が表示されます。 具体的には、**ソース**ビューで使用していた **&lt;asp:&gt;** の要素は表示されません。 ページを実行すると、ASP.NET によってサーバーコントロールが処理され、コントロールを表す機能を実行するページに HTML 要素がレンダリングされます。 たとえば、 **&lt;asp: Button&gt;** コントロールは、HTML **&lt;input type =&quot;submit&quot;&gt;** 要素としてレンダリングされます。
4. ブラウザーを閉じます。

## <a name="working-with-additional-controls"></a>追加のコントロールの操作

<a id="sectionToggle2"></a>

チュートリアルのこの部分では、[カレンダー](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)コントロールを操作します。このコントロールには、月に日付が表示されます。 [Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)コントロールは、使用していたボタン、テキストボックス、ラベルよりも複雑なコントロールで、サーバーコントロールのいくつかの機能を示しています。

このセクションでは、 [WebControls](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)コントロールをページに追加して、書式を設定します。

### <a name="to-add-a-calendar-control"></a>カレンダーコントロールを追加するには

1. Visual Studio で、 **[デザイン]** ビューに切り替えます。
2. **ツールボックス**の **[標準]** セクションで、[カレンダー](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)コントロールをページにドラッグし、他のコントロールを含む**div**要素の下にドロップします。

    カレンダーのスマートタグパネルが表示されます。 パネルには、選択したコントロールに対して最も一般的なタスクを簡単に実行できるようにするコマンドが表示されます。 次の図は、 **[デザイン]** ビューで表示される[カレンダー](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)コントロールを示しています。

    ![デザインビューの Calendar コントロール](creating-a-basic-web-forms-page/_static/image13.png "デザイン ビューの Calender コントロール")
3. スマートタグパネルで、 **[オートフォーマット]** を選択します。

    **[オートフォーマット]** ダイアログボックスが表示されます。このダイアログボックスでは、カレンダーの書式設定スキームを選択できます。 次の図は、[カレンダー](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)コントロールの **[オートフォーマット]** ダイアログボックスを示しています。

    ![[オートフォーマット] ダイアログボックス (カレンダーコントロール)](creating-a-basic-web-forms-page/_static/image14.png "[自動フォーマット] ダイアログ ボックス (Calender コントロール)")
4. **[スキームの選択]** の一覧から **[Simple]** を選択し、 **[OK]** をクリックします。
5. **ソース**ビューに切り替えます。

    **&lt;asp: Calendar&gt;** 要素が表示されます。 この要素は、前に作成した単純なコントロールの要素よりもはるかに長くなります。 また、さまざまな書式設定を表す **&lt;WeekEndDayStyle&gt;** などのサブ要素が含まれています。 次の図は、**ソース**ビューの[Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)コントロールを示しています。 (**ソース**ビューに表示される正確なマークアップは、図とは少し異なる場合があります)。

    ![ソースビューの Calendar コントロール](creating-a-basic-web-forms-page/_static/image15.png "ソース ビューの Calender コントロール")

### <a name="programming-the-calendar-control"></a>カレンダーコントロールのプログラミング

このセクションでは、現在選択されている日付を表示するように[Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)コントロールをプログラミングします。

### <a name="to-program-the-calendar-control"></a>カレンダーコントロールをプログラミングするには

1. **デザイン**ビューで、[カレンダー](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)コントロールをダブルクリックします。

    新しいイベントハンドラーが作成され、 *FirstWebPage.aspx.cs*という名前の分離コードファイルに表示されます。
2. 次のコードを使用して、 [Selectionchanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx)イベントハンドラーを完成させます。

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

    上のコードは、ラベルコントロールのテキストをカレンダーコントロールの選択された日付に設定します。

### <a name="running-the-page"></a>ページを実行しています

これで、カレンダーをテストできるようになりました。

### <a name="to-run-the-page"></a>ページを実行するには

1. CTRL キーを押し**ながら F5**キーを押して、ブラウザーでページを実行します。
2. カレンダーの日付をクリックします。

    クリックした日付が[ラベル](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)コントロールに表示されます。
3. ブラウザーで、ページのソースコードを表示します。

    [カレンダー](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx)コントロールは、各日が**td**要素として**テーブル**としてページにレンダリングされていることに注意してください。
4. ブラウザーを閉じます。

## <a name="next-steps"></a>次の手順

<a id="nextStepsToggle"></a>

このチュートリアルでは、Visual Studio ページデザイナーの基本的な機能について説明しました。 これで、Visual Studio で Web フォームページを作成および編集する方法を理解できたので、他の機能を調べることもできます。 たとえば、次のような操作を行うことができます。

- ASP.NET Web フォームの詳細については、 [ASP.NET 4.5 Web フォームおよび Visual Studio 2013 でのはじめに](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)チュートリアルシリーズの手順に関するページを参照してください。
- カスケードスタイルシート (CSS) の詳細については、こちらを参照してください。 詳細については、「 [CSS の使用の概要](https://msdn.microsoft.com/library/bb398931.aspx)」を参照してください。

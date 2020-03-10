---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: コード編集 ASP.NET の Web フォームを Visual Studio 2013 |Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 3473ad476fbbebc58e12586334b4600f57cf17ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513640"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a>Visual Studio 2013 で ASP.NET Web フォームのコードを編集する

[Erik Reitan](https://github.com/Erikre)

多くの ASP.NET Web フォーム ページでは、Visual Basic、C#、または別の言語でコードを記述します。 Visual Studio のコードエディターを使用すると、エラーを回避しながらコードをすばやく記述できます。 また、エディターは、再利用可能なコードを作成して、必要な作業量を減らすための手段を提供します。

このチュートリアルでは、Visual Studio コードエディターのさまざまな機能について説明します。

このチュートリアルでは、次の作業を行う方法について説明します。

- インラインのコードエラーを修正します。
- コードをリファクターして名前を変更します。
- 変数とオブジェクトの名前を変更します。
- コードスニペットを挿入します。

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

チュートリアルのこの部分では、Web アプリケーションプロジェクトを作成し、そこに新しいページを追加します。

### <a name="to-create-a-web-application-project"></a>Web アプリケーションプロジェクトを作成するには

1. Microsoft Visual Studio を開きます。
2. **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。  
    ![ファイル メニュー](code-editing-in-web-forms-pages/_static/image1.png)

    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。
3. 左側にある [**テンプレート** -&gt; **Visual C#**  -&gt; **Web**テンプレート] グループを選択します。
4. 中央の列で **[ASP.NET Web アプリケーション]** を選択します。
5. プロジェクトに***Basicwebapp***という名前を指定し、 **[OK]** ボタンをクリックします。   
![[新しいプロジェクト] ダイアログ ボックス](code-editing-in-web-forms-pages/_static/image2.png)
6. 次に、 **[Web フォーム]** テンプレートを選択し、 **[OK]** ボタンをクリックしてプロジェクトを作成します。  
![[新しい ASP.NET プロジェクト] ダイアログ ボックス](code-editing-in-web-forms-pages/_static/image3.png)  

    Visual Studio によって、Web フォームテンプレートに基づく事前構築済みの機能を含む新しいプロジェクトが作成されます。

## <a name="creating-a-new-aspnet-web-forms-page"></a>新しい ASP.NET Web フォームページの作成

**ASP.NET Web アプリケーション**プロジェクトテンプレートを使用して新しい Web フォームアプリケーションを作成すると、Visual Studio によって、 *default.aspx*という名前の ASP.NET ページ (Web フォームページ) とその他のいくつかのファイルとフォルダーが追加されます。 *Default.aspx*ページは、Web アプリケーションのホームページとして使用できます。 ただし、このチュートリアルでは、新しいページを作成して操作します。

### <a name="to-add-a-page-to-the-web-application"></a>Web アプリケーションにページを追加するには

1. **ソリューションエクスプローラー**で、Web アプリケーション名 (このチュートリアルではアプリケーション名は**basicwebsite**) を右クリックし、[ -の**追加**] をクリックして &gt;**新しい項目**を追加します。   
**[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. 左側の **[ C# Visual** -&gt; **Web**テンプレート] グループを選択します。 次に、中央の一覧から **[Web フォーム]** を選択し、 *firstwebpage ページ*にという名前を指定します。   
    ![[新しい項目の追加] ダイアログ ボックス](code-editing-in-web-forms-pages/_static/image4.png)
3. **[追加]** をクリックして、Web フォームページをプロジェクトに追加します。  
 新しいページが作成されて開きます。
4. 次に、この新しいページを既定のスタートアップページとして設定します。 **ソリューションエクスプローラー**で、 *firstwebpage*という名前の新しいページを右クリックし、 **[スタートページとして設定]** を選択します。 次回このアプリケーションを実行して進行状況をテストすると、ブラウザーにこの新しいページが自動的に表示されます。

## <a name="correcting-inline-coding-errors"></a>インラインコードエラーの修正

Visual Studio のコードエディターを使用すると、コードを記述するときにエラーを回避できます。また、エラーが発生した場合は、コードエディターを使用してエラーを修正することができます。 チュートリアルのこの部分では、エディターのエラー修正機能を示すコード行を記述します。

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a>Visual Studio で単純なコードエラーを修正するには

1. **デザイン**ビューで、空白のページをダブルクリックして、ページの**読み込み**イベントのハンドラーを作成します。   
   イベントハンドラーを使用するのは、コードを記述する場所としてのみです。
2. ハンドラー内で、エラーを含む次の行を入力し、 **enter キーを押します。**

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   **Enter キーを**押すと、コードエディターによって、問題のあるコード領域の下に緑と赤の下線が表示されます (通常は、波線 &quot;&quot; 線になります)。 緑の下線は警告を示します。 赤い下線は、修正する必要があるエラーを示しています。 

    `myStr` 上にマウスポインターを置くと、警告に関する情報を示すツールヒントが表示されます。 また、赤い枠線の上にマウスポインターを置くと、エラーメッセージが表示されます。

    次の図は、下線付きのコードを示しています。

    ![デザインビューのようこそテキスト](code-editing-in-web-forms-pages/_static/image5.png "デザイン ビューの開始テキスト")  
   このエラーは、行の末尾にセミコロン `;` を追加することで修正する必要があります。 警告は、`myStr` 変数をまだ使用していないことを通知するだけです。  

    > [!NOTE] 
    > 
    > Visual Studio で現在のコードの書式設定を表示するには、[**ツール** -&gt;**オプション]** を選択し &gt;**フォントと色**を -します。

## <a name="refactoring-and-renaming"></a>リファクタリングと名前の変更

リファクタリングとは、コードを再構築することによって、機能を維持しながら理解を深め、保守を容易にする、ソフトウェアの手法です。 単純な例として、イベントハンドラーにコードを記述してデータベースからデータを取得することがあります。 ページを開発する際には、複数の異なるハンドラーからデータにアクセスする必要があることがわかります。 したがって、ページにデータアクセスメソッドを作成し、ハンドラーにメソッドの呼び出しを挿入することによって、ページのコードをリファクターします。

コードエディターには、さまざまなリファクタリングタスクの実行に役立つツールが用意されています。 このチュートリアルでは、変数の名前の変更とメソッドの抽出という2つのリファクタリング手法を使用します。 その他のリファクタリングオプションとしては、フィールドのカプセル化、メソッドパラメーターへのローカル変数の昇格、およびメソッドパラメーターの管理などがあります。 これらのリファクタリングオプションを使用できるかどうかは、コード内の場所によって異なります。

### <a name="refactoring-code"></a>リファクタリング (コードを)

一般的なリファクタリングシナリオでは、メソッドなど、別のメンバー内にあるコードからメソッドを作成 (抽出) します。 これにより、元のメンバーのサイズが縮小され、抽出されたコードが再利用可能になります。

チュートリアルのこの部分では、単純なコードを記述し、そこからメソッドを抽出します。 リファクタリングはサポートされている C# の場合は、ため、プログラミング言語として C# を使用するページを作成します。

### <a name="to-extract-a-method-in-a-c-page"></a>C#ページ内のメソッドを抽出するには

1. **デザイン**ビューに切り替えます。
2. **ツールボックス**の **[標準]** タブで、[ボタン](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx)コントロールをページにドラッグします。
3. **ボタン**コントロールをダブルクリックして、[クリック](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx)イベントのハンドラーを作成し、次の強調表示されたコードを追加します。

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   このコードは、 **arraylist**オブジェクトを作成し、ループを使用して値を読み込み、別のループを使用して**arraylist**オブジェクトの内容を表示します。
4. CTRL キーを押し**ながら F5**キーを押してページを実行し、**ボタン**をクリックして、次の出力が表示されることを確認します。   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. コードエディターに戻り、イベントハンドラーで次の行を選択します。   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. 選択範囲を右クリックし、 **[リファクター]** 、 **[メソッドの抽出]** の順にクリックします。 

    **[メソッドの抽出]** ダイアログボックスが表示されます。
7. **[新しいメソッド名]** ボックスに「 **displayarray**」と入力し、 **[OK]** をクリックします。 

    コードエディターによって `DisplayArray`という名前の新しいメソッドが作成され、ループがもともと呼び出されていた**クリック**ハンドラーに新しいメソッドの呼び出しが配置されます。

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. CTRL キーを押し**ながら F5**キーを押してページを再度実行し、**ボタン**をクリックします。

    ページは、以前と同じように機能します。 `DisplayArray` メソッドは、ページクラスのどこからでも呼び出すことができるようになりました。

## <a name="renaming-variables"></a>変数名の変更

変数とオブジェクトを操作する場合は、コード内で既に参照されているときに名前を変更することもできます。 ただし、変数とオブジェクトの名前を変更すると、いずれかの参照の名前を変更しないとコードが破損する可能性があります。 そのため、リファクタリングを使用して名前の変更を行うことができます。

### <a name="to-use-refactoring-to-rename-a-variable"></a>リファクタリングを使用して変数の名前を変更するには

1. **Click**イベントハンドラーで、次の行を見つけます。

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. 変数名 `alist`を右クリックし、 **[リファクター]** 、 **[名前の変更]** の順に選択します。

    **[名前の変更]** ダイアログボックスが表示されます。
3. **[新しい名前]** ボックスに「 **ArrayList1** 」と入力し、 **[参照の変更のプレビュー]** チェックボックスがオンになっていることを確認します。 次に、 **[OK]** をクリックします

    **[変更のプレビュー]** ダイアログボックスが表示され、名前を変更しようとしている変数へのすべての参照を含むツリーが表示されます。
4. **[適用]** をクリックして、 **[変更のプレビュー]** ダイアログボックスを閉じます。

    選択したインスタンスを明示的に参照する変数の名前は変更されます。 ただし、次の行に `alist` 変数の名前は変更されないことに注意してください。

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    この行の `alist` 変数の名前は変更されません。これは、名前を変更した `alist` 変数と同じ値を表していないためです。 `DisplayArray` 宣言内の変数 `alist` は、そのメソッドのローカル変数です。 これは、リファクタリングを使用して変数名を変更することは、エディターで [検索と置換] アクションを実行することとは異なります。リファクタリングでは、変数の名前が、使用している変数のセマンティクスに関する情報で変更されます。

## <a name="inserting-snippets"></a>スニペットの挿入

多くの場合、Web フォームの開発者が頻繁に実行する必要があるコーディングタスクが多数あるため、コードエディターでは、スニペットのライブラリ、または記述済みのコードのブロックが提供されます。 これらのスニペットは、ページに挿入できます。

Visual Studio で使用する各言語には、コード スニペットを挿入する方法にはわずかな違いがあります。 スニペットの挿入の詳細については、「 [Visual Basic IntelliSense コードスニペット](https://msdn.microsoft.com/library/18yz4be4.aspx)」を参照してください。 ビジュアルC#にスニペットを挿入する方法の詳細については、「 [ C# visual コードスニペット](https://msdn.microsoft.com/library/z41h7fat.aspx)」を参照してください。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、Visual Studio 2010 コードエディターの基本的な機能について説明しました。コード内のエラーを修正し、コードをリファクタリングし、変数の名前を変更し、コードスニペットをコードに挿入します。 エディターのその他の機能を使用すると、アプリケーション開発を迅速かつ簡単に行うことができます。 たとえば、次の場合です。

- Intellisense のオプションの変更、コードスニペットの管理、オンラインでのコードスニペットの検索など、IntelliSense の機能の詳細について説明します。 詳細については、「 [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx)」を参照してください。
- 独自のコードスニペットを作成する方法について説明します。 詳細については、「 [IntelliSense コードスニペットの作成と使用](https://msdn.microsoft.com/library/ms165392.aspx)」を参照してください。
- スニペットのカスタマイズやトラブルシューティングなど、IntelliSense コードスニペットの Visual Basic 固有の機能について説明します。 詳細については、「 [Visual Basic IntelliSense コードスニペット](https://msdn.microsoft.com/library/18yz4be4.aspx)」を参照してください。
- 詳細については、C# は、リファクタリングとコード スニペットなど、IntelliSense の特定の機能。 詳細については、「 [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)」を参照してください。

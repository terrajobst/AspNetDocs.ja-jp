---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4 の新機能 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 は、適切に確立された設計パターンと ASP.NET の力を使用して、拡張性のある標準ベースの web アプリケーションを構築するためのフレームワークです。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433672"
---
# <a name="whats-new-in-aspnet-mvc-4"></a>ASP.NET MVC 4 の新機能

[Web キャンプチーム](https://twitter.com/webcamps)別

[Web キャンプトレーニングキットをダウンロードする](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4 は、適切に確立された設計パターンと ASP.NET と .NET framework の機能を使用して、スケーラブルで標準ベースの web アプリケーションを構築するためのフレームワークです。 この新しい4番目のバージョンのフレームワークは、モバイル web アプリケーションの開発をより簡単にすることに重点を置いています。

まず、新しい ASP.NET MVC 4 プロジェクトを作成するときに、モバイルアプリケーションプロジェクトテンプレートを使用して、モバイルデバイス専用のスタンドアロンアプリを作成できるようになりました。 さらに、ASP.NET MVC 4 は、jQuery の NuGet パッケージを通じて jQuery Mobile と統合されています。 jQuery Mobile は、Windows Phone、iPhone、Android など、一般的なすべてのモバイルデバイスプラットフォームと互換性のある web アプリを開発するための HTML5 ベースのフレームワークです。 ただし、特殊化が必要な場合は、ASP.NET MVC 4 を使用すると、デバイスごとに異なるビューを提供し、デバイス固有の最適化を行うこともできます。

このハンズオンラボでは、まず、ASP.NET MVC 4 &quot;Internet Application&quot; プロジェクトテンプレートを使用して、フォトギャラリーアプリケーションを作成します。 JQuery Mobile と ASP.NET MVC 4 の新機能を使用してアプリを段階的に強化し、さまざまなモバイルデバイスとデスクトップ web ブラウザーとの互換性を確保します。 また、コード生成用の新しいコードレシピと、ASP.NET MVC 4 によって、タスク&lt;ActionResult&gt; 戻り値の型をサポートすることで、非同期アクションメソッドを簡単に記述できるようになる方法についても説明します。

> [!NOTE]
> すべてのサンプルコードとスニペットは、 [Microsoft web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)で入手できる Web キャンプトレーニングキットに含まれています。 このラボに固有のプロジェクトは、 [「ASP.NET 4.5 の Web フォームの新機能](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)」から入手できます。

<a id="Objectives"></a>
### <a name="objectives"></a>目標

このハンズオンラボでは、次の方法を学習します。

- ASP.NET MVC プロジェクトテンプレートの機能強化を活用する (新しいモバイルアプリケーションプロジェクトテンプレートを含む)
- HTML5 ビューポート属性と CSS メディアクエリを使用してモバイルデバイスの表示を改善する
- JQuery Mobile を使用してプログレッシブ拡張を行い、タッチに最適化された web UI を作成する
- モバイル固有のビューを作成する
- アプリケーションのモバイルビューとデスクトップビューを切り替えるには、ビュースイッチャーコンポーネントを使用します。
- タスクサポートを使用して非同期コントローラーを作成する

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>前提条件

このラボを完了するには、次の項目が必要です。

- Web またはそれ以降[の2012を Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)します (付録 B をインストールする手順については、 [「付録 B](#AppendixB) 」を参照してください)。
- [ASP.NET MVC 4](../../../mvc4.md) (Microsoft Visual Studio 2012 インストールに含まれています)
- Windows Phone Emulator ( [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233)に含まれています)
- オプション- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) With**電気 Plum iPhone シミュレーター**拡張機能 (iphone シミュレーターで web アプリケーションを参照するために使用する演習3のみ)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>セットアップ

ラボドキュメント全体で、コードブロックを挿入するように指示されます。 便宜上、そのコードのほとんどは Visual Studio Code のスニペットとして提供されています。これを Visual Studio 内から使用すると、手動で追加する必要がなくなります。

コードスニペットをインストールするには:

1. Windows エクスプローラーウィンドウを開き、ラボの**Source\Setup**フォルダーを参照します。
2. このフォルダーにある**setup.exe**ファイルをダブルクリックして、Visual Studio のコードスニペットをインストールします。

Visual Studio Code のスニペットを使い慣れておらず、その使用方法を学習する場合は、このドキュメントの付録「[付録 a: コードスニペット](#AppendixA)&quot;の使用」 &quot;参照してください。

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>手順

このハンズオンラボには、次の演習が含まれています。

1. [新しい ASP.NET MVC 4 プロジェクトテンプレート](#Exercise1)
2. [フォトギャラリー Web アプリケーションの作成](#Exercise2)
3. [モバイルデバイスのサポートの追加](#Exercise3)
4. [非同期コントローラーの使用](#Exercise4)

> [!NOTE]
> 各演習には、演習を完了した後に取得する必要があるソリューションを含む**終了**フォルダーが付属しています。 演習を通じて追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。

このラボの推定所要時間: **60 分**。

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a>演習 1: 新しい ASP.NET MVC 4 プロジェクトテンプレート

この演習では、ASP.NET MVC 4 プロジェクトテンプレートの拡張機能について説明します。 MVC 3 に既に存在するインターネットアプリケーションテンプレートに加えて、このバージョンにはモバイルアプリケーション用の別のテンプレートが含まれるようになりました。 まず、各テンプレートの関連する機能をいくつか見ていきます。 次に、適切な方法を使用して、さまざまなプラットフォームでページを正しく表示します。

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a>タスク 1-インターネットアプリケーションテンプレートを探索する

1. **Visual Studio** を開きます。
2. ファイルを選択してください **|新規 |[プロジェクト**] メニューコマンド。 **新しいプロジェクト** ダイアログで、 **Visual C# | を選択します。** 左側のウィンドウツリーで web テンプレート を選択し、 **ASP.NET MVC 4 web アプリケーション** を選択します。 プロジェクトに**Photogallery**という名前を設定し、場所を選択して (または既定値のままにして)、[ **OK]** をクリックします。

    > [!NOTE]
    > 後で、作成中の PhotoGallery ASP.NET MVC 4 ソリューションをカスタマイズします。

    ![新しいプロジェクトの作成](whats-new-in-aspnet-mvc-4/_static/image1.png "新しいプロジェクトを作成します。")

    *新しいプロジェクトの作成*
3. **[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** プロジェクトテンプレートを選択し、 **[OK]** をクリックします。 ビューエンジンとして Razor が選択されていることを確認します。

    ![新しい ASP.NET MVC 4 インターネットアプリケーションを作成する](whats-new-in-aspnet-mvc-4/_static/image2.png "新しい ASP.NET MVC 4 インターネットアプリケーションを作成する")

    *新しい ASP.NET MVC 4 インターネットアプリケーションを作成する*

    > [!NOTE]
    > Razor 構文は、ASP.NET MVC 3 で導入されました。 その目的は、ファイルで必要とされる文字数とキーストローク数を最小限に抑えることです。これにより、高速で滑らかなコーディングワークフローが可能になります。 Razor は、 C#既存の/VB (またはその他の) 言語スキルを活用し、優れた HTML 構築ワークフローを可能にするテンプレートマークアップ構文を提供します。
4. **F5**キーを押してソリューションを実行し、更新されたテンプレートを確認します。 次の機能を確認できます。

    **モダンスタイルのテンプレート**

    テンプレートが更新され、最新のスタイルを提供しています。

    ![ASP.NET MVC 4 の再スタイル化テンプレート](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 の再スタイル化テンプレート")

    *ASP.NET MVC 4 の再スタイル化テンプレート*

    ![新しい連絡先ページ](whats-new-in-aspnet-mvc-4/_static/image4.png "新しい連絡先ページ")

    *新しい連絡先ページ*

    **アダプティブレンダリング**

    ブラウザーウィンドウのサイズを変更し、ページレイアウトが新しいウィンドウサイズに動的に適応することを確認します。 これらのテンプレートでは、アダプティブレンダリング技法を使用して、デスクトップとモバイルの両方のプラットフォームで適切にレンダリングできます。カスタマイズは必要ありません。

    ![さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート](whats-new-in-aspnet-mvc-4/_static/image5.png "さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート")

    *さまざまなブラウザーサイズでの ASP.NET MVC 4 プロジェクトテンプレート*

    **JavaScript を使用した豊富な UI**

    既定のプロジェクトテンプレートのもう1つの拡張機能は、JavaScript を使用してより対話的な JavaScript を提供することです。 テンプレートで使用されるログインリンクとレジスタリンクは、jQuery 検証を使用してクライアント側から入力フィールドを検証する方法を知性します。

    ![jQuery 検証](whats-new-in-aspnet-mvc-4/_static/image6.png)

    *jQuery 検証*

    > [!NOTE]
    > 2つのログセクションに注目してください。最初のセクションでは、サイトの登録済みアカウントを使用してログインできます。2番目のセクションでは、別の認証サービス (既定では無効) を使用してログインすることもできます。
5. ブラウザーを閉じて、デバッガーを停止し、Visual Studio に戻ります。
6. **アプリ\_** の [開始] フォルダーの下にあるファイル**AuthConfig.cs**を開きます。
7. 最後の行のコメントを削除して、Google client for *OAuth* authentication を登録します。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > Facebook、Twitter、Microsoft などの OpenID または OAuth サービスを使用して、認証を簡単に有効にすることができます。
8. **F5**キーを押してソリューションを実行し、ログインページに移動します。
9. [ **Google** service] を選択してログインします。

    ![ログインサービスの選択](whats-new-in-aspnet-mvc-4/_static/image7.png)

    *ログインサービスの選択*
10. Google アカウントを使用してログインします。
11. サイト (localhost) が Google アカウントから情報を取得できるようにします。
12. 最後に、Google アカウントを関連付けるために、サイトに登録する必要があります。

   ![Google アカウントを関連付ける](whats-new-in-aspnet-mvc-4/_static/image8.png)

   *Google アカウントの関連付け*
13. ブラウザーを閉じて、デバッガーを停止し、Visual Studio に戻ります。
14. 次に、ソリューションを調べて、プロジェクトテンプレートで ASP.NET MVC 4 によって導入された他の新機能を確認します。

   ![ASP.NET MVC 4 インターネットアプリケーションプロジェクトテンプレート](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 インターネットアプリケーションプロジェクトテンプレート")

   *ASP.NET MVC 4 インターネットアプリケーションプロジェクトテンプレート*

    - **HTML 5 マークアップ**

       テンプレートビューを参照して、新しいテーママークアップを確認します。

       ![新しいテンプレート (Razor と HTML5 のマークアップを使用した場合)。](whats-new-in-aspnet-mvc-4/_static/image10.png "新しいテンプレート (Razor と HTML5 のマークアップを使用した場合)。")

       *新しいテンプレート。 Razor および HTML5 マークアップを使用します (約 cshtml)。*
    - **更新された JavaScript ライブラリ**

       ASP.NET MVC 4 の既定のテンプレートには、javascript と HTML を使用して高度で応答性の高い web アプリケーションを作成するための JavaScript MVVM フレームワークである KnockoutJS が含まれるようになりました。 MVC3 の場合と同様に、jQuery および jQuery UI ライブラリも ASP.NET MVC 4 に含まれています。

     > [!NOTE]
     > KnockOutJS library の詳細については、「 [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/)」を参照してください。 また、 [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)の jQuery および jquery UI についても学習できます。

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a>タスク 2-モバイルアプリケーションテンプレートを探索する

ASP.NET MVC 4 は、モバイルおよびタブレットブラウザー用の web サイトの開発を容易にします。 このテンプレートには、インターネットアプリケーションテンプレートと同じアプリケーション構造があります (コントローラーコードは事実上同じであることに注意してください) が、タッチベースのモバイルデバイスで適切にレンダリングされるようにスタイルが変更されています。

1. ファイルを選択してください **|新規 |[プロジェクト**] メニューコマンド。 **[新しいプロジェクト]** ダイアログで、[ **Visual C# |] を選択します。** 左側のウィンドウツリーで [Web テンプレート] を選択し、 **ASP.NET MVC 4 web アプリケーション**を選択します。 プロジェクトに「 **Photogallery. Mobile**」という名前を設定し、場所を選択し (または既定値のまま)、[&quot;をソリューションに追加&quot;] を選択し、 **[OK]** をクリックします。
2. **[New ASP.NET MVC 4 プロジェクト]** ダイアログで、 **[モバイルアプリケーション]** プロジェクトテンプレートを選択し、 **[OK]** をクリックします。 ビューエンジンとして Razor が選択されていることを確認します。

    ![新しい ASP.NET MVC 4 モバイルアプリケーションの作成](whats-new-in-aspnet-mvc-4/_static/image11.png "新しい ASP.NET MVC 4 モバイルアプリケーションの作成")

    *新しい ASP.NET MVC 4 モバイルアプリケーションの作成*
3. これで、ソリューションを探索し、mobile 用の ASP.NET MVC 4 ソリューションテンプレートで導入された新機能の一部を確認できます。

    - **jQuery モバイルライブラリ**

        モバイルアプリケーションプロジェクトテンプレートには、モバイルブラウザー互換性のためのオープンソースライブラリである jQuery Mobile library が含まれています。 jQuery Mobile は、CSS と JavaScript をサポートするモバイルブラウザーにプログレッシブ拡張機能を適用します。 プログレッシブ拡張機能を使用すると、すべてのブラウザーで web ページの基本コンテンツを表示できるだけではありますが、リッチコンテンツを表示できるのは最も強力なブラウザーのみになります。 JQuery Mobile スタイルに含まれている JavaScript ファイルと CSS ファイルを使用すると、モバイルブラウザーでページマークアップを変更することなく、コンテンツを画面に収めることができます。

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        *テンプレートに含まれている jQuery mobile ライブラリ*
    - **HTML5 ベースのマークアップ**

        ![-HTML5-マークアップの使用](whats-new-in-aspnet-mvc-4/_static/image13.png)

        *HTML5 マークアップを使用したモバイルアプリケーションテンプレート (Login. cshtml および index. cshtml)*
4. F5 キーを押して、ソリューションを実行します。
5. **Windows Phone 7 エミュレーター**を開きます。
6. 電話のスタート画面で、Internet Explorer を開きます。 デスクトップアプリケーションが開始した URL を確認し、電話からその URL を参照します (例: `http://localhost:[PortNumber]/`)。
7. これで、ログインページを入力したり、[バージョン情報] ページを確認したりできるようになりました。 Web サイトのスタイルは、mobile 用の新しい Metro アプリに基づいていることに注意してください。 ASP.NET MVC 4 プロジェクトテンプレートがモバイルデバイスに正しく表示され、ページのすべての要素が表示され、有効になっていることを確認します。 ヘッダーのリンクは、クリックまたはタップするのに十分な大きさであることに注意してください。

    ![モバイルデバイスのプロジェクトテンプレートページ](whats-new-in-aspnet-mvc-4/_static/image14.png "モバイルデバイスのプロジェクトテンプレートページ")

    *モバイルデバイスのプロジェクトテンプレートページ*
8. 新しいテンプレートでは、**ビューポートメタタグ**も使用されます。 ほとんどのモバイルブラウザーでは、仮想ブラウザーウィンドウの幅が定義されているか、または &quot;ビューポートが&quot;。これは、モバイルデバイスの実際の幅を超えています。 これにより、モバイルブラウザーで web ページ全体を仮想ディスプレイ内に表示できるようになります。 Web 開発者は、**ビューポート meta タグ**を使用して、モバイルデバイスのブラウザー領域の幅、高さ、およびスケールを設定でき**ます。** モバイルアプリケーション用の ASP.NET MVC 4 テンプレートでは、レイアウトテンプレート (*Views\Shared\_layout*) で、ビューポートがデバイスの幅に設定され (&quot;width = デバイス幅&quot;)、すべてのページのビューポートがデバイスの画面幅に設定されるようにします。 ビューポートメタタグは、既定のブラウザービューを変更しないことに注意してください。
9. Views | にある **\_Layout を開きます。** **共有**フォルダーと、ビューポートメタタグをコメント化します。 まだ開いていない場合はアプリケーションを実行し、相違点を確認します。

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

![ビューポートメタタグをコメント化した後のサイト](whats-new-in-aspnet-mvc-4/_static/image15.png "ビューポートメタタグをコメント化した後のサイト")

*ビューポートメタタグをコメント化した後のサイト*
10. Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。
11. ビューポートのメタタグをコメント解除します。

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a>タスク 3-アダプティブレンダリングの使用

この実習では、カスタマイズを行わずに、モバイルデバイスと Web ブラウザーで Web ページを正しく表示する別の方法について学習します。 同じ目的でビューポートメタタグを既に使用しています。 次に、別の強力な方法である*アダプティブレンダリング*を使用します。

アダプティブレンダリングは、 **CSS3 メディアクエリ**を使用して、ページに適用されるスタイルをカスタマイズする手法です。 メディアクエリは、スタイルシート内で条件を定義し、特定の条件下で CSS スタイルをグループ化します。 条件が true の場合にのみ、宣言されたオブジェクトにスタイルが適用されます。

アダプティブレンダリング手法によって実現される柔軟性により、さまざまなデバイスでサイトを表示するためのカスタマイズが可能になります。 スタイルを選択するロジックコードを記述しなくても、1つのスタイルシートに対して必要な数だけスタイルを定義できます。 そのため、ページスタイルを適合させるための非常に便利な方法です。これにより、重複するコードの量と描画のためのロジックが減少します。 一方、CSS ファイルのサイズがわずかに増加する可能性があるため、帯域幅の消費が増加します。

アダプティブレンダリング技法を使用すると、ブラウザーに関係なく、サイトが**正しく表示されます。** ただし、帯域幅の追加負荷が問題になるかどうかを検討する必要があります。

> [!NOTE]
> メディアクエリの基本的な形式は次のとおりです。 @media \[Scope: all |ハンドヘルド |print |射影 |画面\] ([プロパティ: 値] と...[プロパティ: 値])

メディアクエリの例: &gt; **@media すべて (最大幅: 1000px) と (最小幅: 700px) {}:** 700px から1000px までのすべての解像度を示します。

> **@media 画面および (最小幅: 400px) と (最大幅: 700px) {...}:** 画面にのみ使用できます。 解像度は 400 ~ 700px の範囲で指定する必要があります。
> 
> **@media ハンドヘルドと (最小幅: 20em)、画面および (最小幅: 20em) {...}:** ハンドヘルド (モバイルおよびデバイス) と画面の場合。 最小幅は20em よりも大きくする必要があります。
> 
> 詳細については、 [W3C サイト](http://www.w3.org/TR/css3-mediaqueries/)を参照してください。

アダプティブレンダリングがどのように動作するかを調べ、ASP.NET MVC 4 の既定の web サイトテンプレートの読みやすさを向上させます。

1. タスク1で作成した**photogallery .sln**ソリューションを開き、 **photogallery**プロジェクトを選択します。 F5 キーを押して、ソリューションを実行します。
2. ブラウザーの幅を変更し、ウィンドウを半分または元のサイズの4分の1に設定します。 ヘッダーの項目がどのように処理されるかに注意してください。一部の要素は、ヘッダーの表示領域に表示されません。
3. **コンテンツ**プロジェクトフォルダーにある Visual Studio ソリューションエクスプローラーから、**サイトの .css**ファイルを開きます。 **CTRL + F**キーを押して Visual Studio 統合検索を開き、`@media` を記述して**CSS メディアクエリ**を見つけます。

    このテンプレートで定義されているメディアクエリ条件は、次のように動作します。ブラウザーのウィンドウサイズが**850 px**を下回る場合、適用される CSS ルールは、このメディアブロック内で定義されているものです。

    ![メディアクエリの検索](whats-new-in-aspnet-mvc-4/_static/image16.png "メディアクエリの検索")

    *メディアクエリの検索*
4. アダプティブレンダリングを無効にするために、850 px で設定された最大幅属性の値を**10px**に置き換え、 **ctrl + S**キーを押して変更を保存します。 ブラウザーに戻り、CTRL キーを押し**ながら F5**キーを押して、変更内容を反映したページを更新します。 ウィンドウの幅を調整するときに、両方のページの違いに注目してください。

    ![左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。](whats-new-in-aspnet-mvc-4/_static/image17.png "左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。")

    *左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。*

    では、モバイルデバイスの動作を確認してみましょう。

    ![左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。](whats-new-in-aspnet-mvc-4/_static/image18.png "左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。")

    *左側では、ページは @media スタイルを適用しています。右側では、スタイルは省略されています。*

    Web ブラウザーでページを表示したときの変更はあまり重要ではありませんが、モバイルデバイスを使用すると、違いがより明確になります。 画像の左側には、カスタムスタイルの読みやすさが向上していることがわかります。

    アダプティブレンダリングは、他の多くのシナリオで使用できます。これにより、Web サイトに条件付きスタイルを適用したり、一般的なスタイルの問題を適切な方法で解決したりすることが容易になります。

    ビューポートのメタタグと CSS メディアクエリは ASP.NET MVC 4 に固有のものではないため、これらの機能はどの web アプリケーションでも利用できます。
5. Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a>演習 2: フォトギャラリー Web アプリケーションの作成

この演習では、フォトギャラリーアプリケーションを使用して写真を表示します。 まず、ASP.NET MVC 4 プロジェクトテンプレートを使用します。次に、サービスから写真を取得してホームページに表示する機能を追加します。

次の演習では、モバイルデバイスでの表示方法を向上させるために、このソリューションを更新します。

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a>タスク 1-モック写真サービスの作成

このタスクでは、ギャラリーに表示されるコンテンツを取得するために、フォトサービスのモックを作成します。 これを行うには、各写真のデータと共に JSON ファイルを返すだけの新しいコントローラーを追加します。

1. まだ開いていない場合は、 **Visual Studio**を開きます。
2. ファイルを選択してください **|新規 |[プロジェクト**] メニューコマンド。 **新しいプロジェクト** ダイアログで、 **Visual C# | を選択します。** 左側のウィンドウツリーで web テンプレート を選択し、 **ASP.NET MVC 4 web アプリケーション** を選択します。 プロジェクトに**Photogallery**という名前を設定し、場所を選択して (または既定値のままにして)、[ **OK]** をクリックします。 または、**演習 1**の既存の ASP.NET MVC 4**インターネットアプリケーション**ソリューションから作業を続行し、次の手順をスキップすることもできます。
3. **[New ASP.NET MVC 4 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** プロジェクトテンプレートを選択し、 **[OK]** をクリックします。 ビューエンジンとして Razor が選択されていることを確認します。
4. **ソリューションエクスプローラー**で、プロジェクトの [ **App\_Data** ] フォルダーを右クリックし、[追加] を選択します。 **既存のアイテム**。 このラボの**Source\Assets\App\_Data**フォルダーに移動し、 **Photos**ファイルを追加します。
5. **Photocontroller**という名前の新しいコントローラーを作成します。 これを行うには、 **Controllers**フォルダーを右クリックし、**追加** にアクセスして、コントローラー を選択し**ます。** コントローラー名を入力し、**空の MVC コントローラー**テンプレートをそのまま使用して、 **[追加]** をクリックします。

    ![PhotoController の追加](whats-new-in-aspnet-mvc-4/_static/image19.png "PhotoController の追加")

    *PhotoController の追加*
6. **Index**メソッドを次の**ギャラリー**アクションに置き換え、最近プロジェクトに追加した JSON ファイルからコンテンツを返します。

    (コードスニペット- *ASP.NET MVC 4 Lab-Ex02 アクション*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. **F5**キーを押してソリューションを実行し、モック写真サービスをテストするために次の URL を参照します。 `http://localhost:[port]/photo/gallery` ([port] 値は、アプリケーションが起動された現在のポートによって異なります)。 この URL への要求では、 **Photos**ファイルのコンテンツを取得する必要があります。

    ![モック写真サービスのテスト](whats-new-in-aspnet-mvc-4/_static/image20.png "モック写真サービスのテスト")

    *モック写真サービスのテスト*

実際の実装では、 [ASP.NET Web API](../../../../web-api/index.md)を使用してフォトギャラリーサービスを実装できます。 ASP.NET Web API は、ブラウザーやモバイル デバイスなどを含む多様なクライアントに提供できる HTTP サービスの構築が容易になるフレームワークです。 ASP.NET Web API は、.NET Framework 上で RESTful アプリケーションを構築するためのプラットフォームとして理想的です。

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a>タスク 2-フォトギャラリーを表示する

このタスクでは、この演習の最初の作業で作成したモックサービスを使用して、ホームページを更新し、フォトギャラリーを表示します。 モデルファイルを追加し、ギャラリービューを更新します。

1. Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。
2. **[モデル]** フォルダーに**Photo**クラスを作成します。 これを行うには、 **[モデル]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[クラス]** をクリックします。 次に、名前を**Photo.cs**に設定し、 **[追加]** をクリックします。
3. 次のメンバーを**Photo**クラスに追加します。

    (コードスニペット- *ASP.NET MVC 4 Lab-Ex02-Photo モデル*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. **Controllers** フォルダーから **HomeController.cs** ファイルを開きます。
5. 次の using ステートメントを追加します。

    (コードスニペット- *ASP.NET MVC 4 Lab-Ex02-HomeController using*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. **Httpclient**を使用してギャラリーデータを取得するように**Index**アクションを更新し、 **JavaScriptSerializer**を使用してビューモデルに逆シリアル化します。

    (コードスニペット- *ASP.NET MVC 4 Lab-Ex02 アクション*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. **Views\Home**フォルダーの下にある**インデックスの cshtml**ファイルを開き、すべての内容を次のコードに置き換えます。

    このコードは、サービスから取得したすべての写真をループ処理し、順序なしの一覧に表示します。

    (コードスニペット- *ASP.NET MVC 4 Lab-Ex02-Photo List*)

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. **ソリューションエクスプローラー**で、プロジェクトの**コンテンツ**フォルダーを右クリックし、[追加] を選択します。 **既存のアイテム**。 このラボの**Source\Assets\Content**フォルダーを参照し、サイトの **.css**ファイルを追加します。 置換を確認する必要があります。 **サイトの .css**ファイルを開いている場合は、ファイルを再度読み込むことも確認する必要があります。
9. ファイルエクスプローラーを開き、このラボの **[Source\ Assets]** フォルダーの下にある **[Photos]** フォルダー全体を、ソリューションエクスプローラーのプロジェクトのルートフォルダーにコピーします。
10. アプリケーションを実行します。 これで、ギャラリーに写真を表示するホームページが表示されます。

    ![フォトギャラリー](whats-new-in-aspnet-mvc-4/_static/image21.png "フォト ギャラリー")

    *フォトギャラリー*
11. Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a>演習 3: モバイルデバイスのサポートを追加する

ASP.NET MVC 4 の主要な更新プログラムの1つに、モバイル開発のサポートがあります。 この演習では、前の演習で作成した PhotoGallery ソリューションを拡張することで、モバイルアプリケーションの ASP.NET MVC 4 の新機能について説明します。

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a>タスク 1-ASP.NET MVC 4 アプリケーションで jQuery Mobile をインストールする

1. **Source/Ex3-MobileSupport/begin/** folder にある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. [ > **ツール**] **[NuGet パッケージマネージャー]** [ > **パッケージマネージャーコンソール**] オプションの順にクリックして、**パッケージマネージャーコンソール**を開きます。

    ![NuGet パッケージマネージャーコンソールを開く](whats-new-in-aspnet-mvc-4/_static/image22.png "NuGet パッケージマネージャーコンソールを開く")

    *NuGet パッケージマネージャーコンソールを開く*
3. パッケージマネージャーコンソールで、次のコマンドを実行して、 **jQuery**パッケージをインストールします。

    jQuery Mobile は、タッチに最適化された web UI を構築するためのオープンソースライブラリです。 JQuery の NuGet パッケージには、ASP.NET MVC 4 アプリケーションで jQuery Mobile を使用するヘルパーが含まれています。

    > [!NOTE]
    > 次のコマンドを実行すると、Nuget から jQuery. Mobile. MVC ライブラリがダウンロードされます。

    PM

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    このコマンドにより、jQuery Mobile と、次のようなヘルパーファイルがインストールされます。

    - **Views/Shared/\_layout: mobile. cshtml**: 小さい画面用に最適化された jQuery モバイルベースのレイアウトです。 Web サイトがモバイルブラウザーから要求を受信すると、元のレイアウト (\_Layout) がこの web サイトに置き換えられます。
    - ビュースイッチャーコンポーネント: **Views/Shared/\_ViewSwitcher (cshtml** partial) ビューと**ViewSwitcherController.cs**コントローラーで構成されます。 このコンポーネントは、ユーザーがページのデスクトップバージョンに切り替えることができるように、モバイルブラウザーにリンクを表示します。  
        ![Mobile support を使用したフォトギャラリープロジェクト](whats-new-in-aspnet-mvc-4/_static/image23.png "Mobile support を使用したフォトギャラリープロジェクト")

        *Mobile support を使用したフォトギャラリープロジェクト*
4. モバイルバンドルを登録します。 これを行うには、 **Global.asax.cs**ファイルを開き、次の行を追加します。

    (コードスニペット- *ASP.NET MVC 4 Lab-Ex03-Mobile バンドルの登録*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. デスクトップ web ブラウザーを使用してアプリケーションを実行します。
6. [スタート] メニューにある [ **Windows Phone 7] エミュレーターを**開きます。 **すべてのプログラム |Windows Phone SDK 7.1 |Windows Phone エミュレーター。**
7. 電話のスタート画面で、Internet Explorer を開きます。 アプリケーションが開始された URL を確認し、電話ブラウザーでその URL を参照します (例: `http://localhost:[PortNumber]/`)。

    Windows Phone エミュレーターでは、アプリケーションの外観が異なることがわかります。これは、モバイルデバイス用に最適化されたビューを表示する新しいアセットがプロジェクトに作成されたためです。

    電話の上部に、デスクトップビューに切り替えるリンクが表示されていることを確認します。 また、インストールしたパッケージによって作成された **\_のレイアウト**は、アプリケーションに別のレイアウトが含まれています。

    > [!NOTE]
    > ここまでは、モバイルビューに戻るためのリンクはありません。 これは、それ以降のバージョンに含まれる予定です。

    ![フォトギャラリーホームページのモバイルビュー](whats-new-in-aspnet-mvc-4/_static/image24.png "フォトギャラリーホームページのモバイルビュー")

    *フォトギャラリーホームページのモバイルビュー*
8. Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a>タスク 2-モバイルビューの作成

このタスクでは、モバイルデバイスでの外観を改善するためにコンテンツを適合させた状態で、インデックスビューのモバイルバージョンを作成します。

1. **Views\Home\Index.cshtml**ビューをコピーして貼り付け、コピーを作成します。新しいファイルの名前を「 **Index. Mobile. cshtml**」に変更します。
2. 新しく作成した**Index. Mobile. cshtml**ビューを開き、既存の &lt;ul&gt; タグをこのコードで置き換えます。 これにより、jquery のモバイルテーマを使用するように、jQuery モバイルデータ注釈を使用して &lt;ul&gt; タグを更新することになります。

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > 次のことに注意してください。
    > 
    > - **Listview**に設定されている**データロール**属性は、listview スタイルを使用してリストを表示します。
    > 
    > - **データ埋め込み**属性が true に設定されている場合は、境界線と余白が丸められたリストが表示されます。
    > 
    > - **データフィルター**属性を**true**に設定すると、検索ボックスが生成されます。
    > 
    > JQuery Mobile の規則の詳細については、次のプロジェクトドキュメントを参照してください: [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)
3. **CTRL + S**キーを押して、変更を保存します。
4. **Windows Phone エミュレーター**に切り替えて、サイトを最新の状態に更新します。 ギャラリーの一覧の新しい外観と、上部にある新しい検索ボックスに注目してください。 次に、検索ボックスに単語 (例、 **Tulips**) を入力して、フォトギャラリーで検索を開始します。

    ![フィルターを使用して listview スタイルを使用するギャラリー](whats-new-in-aspnet-mvc-4/_static/image25.png "フィルターを使用して listview スタイルを使用するギャラリー")

    *フィルターを使用して listview スタイルを使用するギャラリー*

    まとめると、「Mobilizer 表示」レシピを使用して、&quot;mobile&quot; サフィックスを持つインデックスビューのコピーを作成しました。 このサフィックスは、モバイルデバイスから生成されたすべての要求がこのインデックスのコピーを使用することを ASP.NET MVC 4 に示します。 さらに、モバイルデバイスのサイトの外観を拡張するために jQuery Mobile を使用するように、インデックスビューのモバイルバージョンを更新しました。
5. Visual Studio に戻り、 **Content**フォルダーの下にある **[.css]** を開きます。
6. 画像の右側に表示されるように、写真のタイトルの位置を修正します。 これを行うには、次のコードを追加し**ます。**

    CSS

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. **CTRL + S**キーを押して、変更を保存します。
8. **Windows Phone エミュレーター**に戻り、サイトを最新の状態に更新します。 写真のタイトルが正しく配置されていることを確認します。

    ![イメージの右側に配置されたタイトル](whats-new-in-aspnet-mvc-4/_static/image26.png "イメージの右側に配置されたタイトル")

    *イメージの右側に配置されたタイトル*

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a>タスク 3-jQuery Mobile のテーマ

JQuery Mobile のすべてのレイアウトとウィジェットは、新しいオブジェクト指向の CSS フレームワークを中心に設計されています。これにより、完全な統合されたビジュアルデザインテーマをサイトとアプリケーションに適用できます。

jQuery Mobile の既定のテーマには、クイックリファレンス用に文字 (a、b、c、d、e) が指定された5つの見本が含まれています。

このタスクでは、既定とは異なるテーマを使用するようにモバイルレイアウトを更新します。

1. Visual Studio に戻ります。
2. **Views\Shared**にある **\_Layout**ファイルを開きます。
3. データロールが &quot;ページ&quot; に設定されている div 要素を見つけ、**データテーマ**を &quot;**e**&quot;に更新します。

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. **CTRL + S**キーを押して、変更を保存します。
5. **Windows Phone エミュレーター**でサイトを更新すると、新しい配色が表示されます。

    ![別の配色でのモバイルレイアウト](whats-new-in-aspnet-mvc-4/_static/image27.png "別の配色でのモバイルレイアウト")

    *別の配色でのモバイルレイアウト*

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a>タスク 4-ビュースイッチャーコンポーネントとブラウザーを使用して機能をオーバーライドする

モバイルで最適化された web ページの規則としては、ユーザーがデスクトップバージョンのページに切り替えることができるように、デスクトップビューや完全サイトモードなどのテキストを持つリンクを追加します。 JQuery パッケージには、この目的のためのサンプルの**ビュースイッチャー**コンポーネントが含まれています。これは **\_Layout**ビューで使用されます。

![デスクトップビューに切り替えるためのリンク](whats-new-in-aspnet-mvc-4/_static/image28.png "デスクトップビューに切り替えるためのリンク")

*デスクトップビューに切り替えるためのリンク*

ビュースイッチャーは、**ブラウザーのオーバーライド**と呼ばれる新しい機能を使用します。 この機能により、アプリケーションは、実際に使用されているものとは異なるブラウザー (ユーザーエージェント) からの要求を処理できます。

このタスクでは、ASP.NET によって追加されたビュースイッチャーの実装のサンプルと、新しいブラウザーで、MVC 4 の新機能をオーバーライドします。

1. Visual Studio に戻ります。
2. **Views\Shared**フォルダーの下にある **\_Layout**を開き、ビュースイッチャーコンポーネントが部分ビューとして参照されていることを確認します。

    ![ビュースイッチャーコンポーネントを使用したモバイルレイアウト](whats-new-in-aspnet-mvc-4/_static/image29.png "ビュースイッチャーコンポーネントを使用したモバイルレイアウト")

    *ビュースイッチャーコンポーネントを使用したモバイルレイアウト*
3. **\_ViewSwitcher**の部分ビューを開きます。

    部分ビューでは、新しいメソッド**GetOverriddenBrowser ()** を使用して、web 要求の送信元を特定し、対応するリンクを表示してデスクトップまたはモバイルビューに切り替えます。

    **GetOverriddenBrowser**メソッドは、要求に対して現在設定されているユーザーエージェント (実際またはオーバーライド) に対応する**HttpBrowserCapabilitiesBase**インスタンスを返します。 この値を使用して、 **IsMobileDevice**などのプロパティを取得できます。

    ![ViewSwitcher 部分ビュー](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 部分ビュー")

    *ViewSwitcher 部分ビュー*
4. **Controllers**フォルダーにある**ViewSwitcherController.cs**クラスを開きます。 この SwitchView アクションが ViewSwitcher コンポーネントのリンクによって呼び出され、新しい HttpContext メソッドがあることを確認します。

    - **ClearOverriddenBrowser ()** メソッドは、現在の要求に対してオーバーライドされたユーザーエージェントを削除します。
    - **SetOverriddenBrowser ()** メソッドは、指定されたユーザーエージェントを使用して、要求の実際のユーザーエージェント値をオーバーライドします。  
        ![ViewSwitcher コントローラー](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher コントローラー")  
*ViewSwitcher コントローラー*

        ブラウザーのオーバーライドは ASP.NET MVC 4 の中核機能であり、jQuery パッケージをインストールしない場合でも利用できます。 ただし、この機能は、ビュー、レイアウト、および部分ビューのみに影響し、要求の Browser オブジェクトに依存する機能には影響しません。

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a>タスク 5-デスクトップビューでのビュースイッチャーの追加

このタスクでは、ビュースイッチャーを含むようにデスクトップレイアウトを更新します。 これにより、モバイルユーザーは、デスクトップビューを参照するときにモバイルビューに戻ることができます。

1. **Windows Phone エミュレーター**でサイトを最新の状態に更新します。
2. ギャラリーの上部にある **[デスクトップビュー]** リンクをクリックします。 デスクトップビューには、モバイルビューに戻ることができるビュースイッチャーがないことに注意してください。
3. Visual Studio に戻り、 **\_Layout**ビューを開きます。
4. Login セクションを検索し、呼び出しを挿入して、 **\_LogOnPartial**部分ビューの下に **\_viewswitcher**部分ビューを表示します。 次に、 **CTRL + S**キーを押して、変更を保存します。

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. **CTRL + S**キーを押して、変更を保存します。
6. Windows Phone エミュレーターでページを更新し、画面をダブルクリックして拡大します。 ホームページの [モバイル**ビュー** ] リンクが表示され、モバイルからデスクトップへの表示に切り替わります。

    ![デスクトップビューで表示されたビュースイッチャー](whats-new-in-aspnet-mvc-4/_static/image32.png "デスクトップビューで表示されたビュースイッチャー")

    *デスクトップビューで表示されたビュースイッチャー*
7. もう一度モバイルビューに切り替えて、 **[バージョン情報]** ページ (http://localhost[ポート]/Home/About) に移動します。 About. Mobile. cshtml ビューを作成していない場合でも、モバイルレイアウト (\_Layout) を使用して [バージョン情報] ページが表示されることに注意してください。

    ![[バージョン情報] ページ](whats-new-in-aspnet-mvc-4/_static/image33.png "About ページ")

    *[バージョン情報] ページ*
8. 最後に、デスクトップ Web ブラウザーでサイトを開きます。 以前の更新プログラムがデスクトップビューに影響を与えていないことに注意してください。

    ![PhotoGallery デスクトップビュー](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery デスクトップビュー")

    *PhotoGallery デスクトップビュー*

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a>タスク 6-新しい表示モードを作成する

新しい表示モード機能を使用すると、アプリケーションは要求を生成しているブラウザーに応じてビューを選択できます。 たとえば、デスクトップブラウザーがホームページを要求した場合、アプリケーションは**Views\Home\Index.cshtml**テンプレートを返します。 その後、モバイルブラウザーがホームページを要求すると、アプリケーションは**Views\Home\Index.mobile.cshtml**テンプレートを返します。

このタスクでは、iPhone デバイス用にカスタマイズされたレイアウトを作成し、iPhone デバイスからの要求をシミュレートする必要があります。 これを行うには、iPhone エミュレーター/シミュレーター ([電気モバイルシミュレーター](http://www.electricplum.com/)など) を使用するか、ユーザーエージェントを変更するアドオンを含むブラウザーを使用します。 Safari ブラウザーでユーザーエージェント文字列を設定して iPhone をエミュレートする方法については、David Alison のブログで Safari を使用して[いることを safari に任せる方法](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html)に関する記事をご覧ください。

**このタスクは省略可能であることに注意してください。ラボを実行しなくても続行できます。**

1. Visual Studio で、 **SHIFT** + **F5**キーを押してアプリケーションのデバッグを停止します。
2. **Global.asax.cs**を開き、次の using ステートメントを追加します。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. 次の強調表示されたコードをアプリケーション\_の開始メソッドに追加します。

    (コードスニペット- *ASP.NET MVC 4 Lab-Ex03-IPhone DisplayMode*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

静的な**Displaymodeprovider. Instance. mode** **&quot;&quot;という名前の新しい defaultdisplaymode**を登録しました。これは、各受信要求に対して照合されます。 受信要求に iPhone&quot;の文字列 &quot;が含まれている場合、ASP.NET MVC では、名前に &quot;iPhone&quot; サフィックスが含まれるビューが検索されます。 0パラメーターは、どのように新しいモードを指定するかを示します。たとえば、このビューは、モバイルデバイスからの要求に一致する一般的な &quot;mobile&quot; ルールよりも具体的です。

このコードが実行されると、iPhone ブラウザーが要求を生成するときに、アプリケーションでは、次の手順で作成する**Views\Shared\\_Layout**を使用します。

> [!NOTE]
> IPhone の要求をテストするこの方法はデモを目的として簡略化されており、すべての iPhone ユーザーエージェント文字列で想定どおりに機能しない可能性があります (たとえば、テストでは大文字と小文字が区別されます)。

4. **Views\Shared**フォルダーに **\_Layout**ファイルのコピーを作成し、コピーの名前を &quot; **\_layout**&quot;に変更します。
5. 前の手順で作成した **\_のレイアウト**を開きます。
6. データロール属性が**ページ**に設定されている div 要素を見つけ、**データテーマ**属性**を&quot;&quot;に変更**します。

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

これで、ASP.NET MVC 4 アプリケーションに3つのレイアウトが作成されるようになりました。

1. **\_layout**: デスクトップブラウザーで使用される既定のレイアウトです。
2. **\_** は、モバイルデバイスで使用される既定のレイアウトです。
3. **\_** のレイアウトです。 iphone デバイスの特定のレイアウトでは、別の配色を使用して \_のレイアウトを区別します。
7. **F5**キーを押してアプリケーションを実行し、 **Windows Phone エミュレーター**でサイトを参照します。
8. **Iphone**シミュレーターを開き (iphone シミュレーターのインストールと構成の手順については、[付録 C](#AppendixC)を参照してください)、サイトを参照してください。 各電話で特定のテンプレートが使用されていることに注意してください。

    ![-デバイス2を使用して-異なるビューを使用する](whats-new-in-aspnet-mvc-4/_static/image35.png)

    *モバイルデバイスごとに異なるビューを使用する*

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a>演習 4: 非同期コントローラーの使用

Microsoft .NET Framework 4.5 でC#は、と Visual Basic の新しい言語機能が導入されており、.net プログラミングにおける非同期性の新しい基盤を提供しています。 この新しい基盤により、非同期プログラミングは、と同様に、同期型のプログラミングと同様に簡単に行うことができます。 **Asynccontroller**クラスを使用して、ASP.NET MVC 4 で非同期アクションメソッドを記述できるようになりました。 非同期アクション メソッドは、実行に時間のかかる CPU バインド以外の要求に使用できます。 これにより、要求の処理中に Web サーバーによる処理の実行が妨げられることがなくなります。 AsyncController クラスは、通常、実行時間の長い Web サービス呼び出しに使用されます。

この演習では、ASP.NET MVC 4 での非同期操作の基本について説明します。 詳細については、次の記事を確認してください: [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a>タスク 1-非同期コントローラーを実装する

1. **Source/Ex4/begin/** folder にある**begin**ソリューションを開きます。 それ以外の場合は、前の演習を完了することによって得られた**終了**ソリューションを引き続き使用することができます。

   1. 提供された**Begin**ソリューションを開いた場合は、続行する前に、不足している NuGet パッケージをダウンロードする必要があります。 これを行うには、 **[プロジェクト]** メニューをクリックし、 **[NuGet パッケージの管理]** を選択します。
   2. **[NuGet パッケージの管理]** ダイアログで、 **[復元]** をクリックして、不足しているパッケージをダウンロードします。
   3. 最後に、[**ビルド** | **ビルド**] をクリックしてソリューションをビルドします。

      > [!NOTE]
      > NuGet を使用する利点の1つは、プロジェクトのすべてのライブラリを配布する必要がなく、プロジェクトのサイズを小さくすることです。 NuGet パワーツールを使用すると、パッケージのバージョンを app.config ファイルで指定することで、プロジェクトを初めて実行するときに必要なすべてのライブラリをダウンロードできます。 このため、このラボから既存のソリューションを開いた後に、これらの手順を実行する必要があります。
2. **Controllers**フォルダーから**HomeController.cs**クラスを開きます。
3. 次の using ステートメントを追加します。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. **Asynccontroller**から継承するように**HomeController**クラスを更新します。 AsyncController から派生したコントローラーは、ASP.NET が非同期要求を処理できるようにします。また、同期アクションメソッドを処理することもできます。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. **Async**キーワードを**Index**メソッドに追加し、Type**タスク&lt;actionresult&gt;** を返します。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > **Async**キーワードは、.NET Framework 4.5 が提供する新しいキーワードの1つです。このメソッドは、このメソッドが非同期コードを含むことをコンパイラに伝えます。 **Task**オブジェクトは、将来のある時点で完了する可能性のある非同期操作を表します。
6. クライアントを置き換え**ます。GetAsync ()** は、次に示すように、await キーワードを使用する完全な非同期バージョンでを呼び出します。

    (コードスニペット- *ASP.NET MVC 4 Lab-Ex04-GetAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > 以前のバージョンでは、**タスク**オブジェクトから**result**プロパティを使用して、結果が返されるまでスレッドをブロックしていました (同期バージョン)。
    > 
    > **Await**キーワードを追加すると、メソッド呼び出しから返されたタスクを非同期に待機するようにコンパイラに指示します。 これは、待機中のメソッドが完了した後にのみ、コードの残りの部分がコールバックとして実行されることを意味します。 もう1つの注意点は、この作業を行うために try-catch ブロックを変更する必要がないことです。つまり、バックグラウンドまたはフォアグラウンドで発生する例外は、フレームワークによって提供されるハンドラーを使用して追加の作業を行わずにキャッチされます。
7. 次に示すように、行を新しいコードに置き換えて、非同期実装で続行するようにコードを変更します。

    (コードスニペット- *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. アプリケーションを実行します。 大きな変更はありませんが、スレッドプールからのスレッドをブロックすることはできません。これにより、サーバーリソースの使用率が向上し、パフォーマンスが向上します。

    > [!NOTE]
    > このラボの新しい非同期プログラミング機能の詳細については、Visual Studio トレーニングキットに含まれている **C#と Visual Basic&quot; の .net 4.5 での &quot;非同期プログラミング」** を参照してください。

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a>タスク 2-キャンセルトークンを使用したタイムアウト処理

タスクインスタンスを返す非同期アクションメソッドは、タイムアウトをサポートすることもできます。 このタスクでは、キャンセルトークンを使用してタイムアウトシナリオを処理するように、インデックスメソッドコードを更新します。

1. Visual Studio に戻り、SHIFT キーを押し**ながら F5**キーを押してデバッグを停止します。
2. 次の using ステートメントを**HomeController.cs**ファイルに追加します。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. **CancellationToken**引数を受け取るように Index アクションを更新します。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. **GetAsync**呼び出しを更新して、キャンセルトークンを渡します。

    (コードスニペット- *ASP.NET MVC 4 Lab-Ex04-SendAsync With CancellationToken*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. **Asynctimeout**属性を500ミリ秒に設定し、 **TimedOut**ビューにリダイレクトして**TaskCanceledException**を処理するように構成された**HandleError**属性を使用して、 *Index*メソッドを修飾します。

    (コードスニペット- *ASP.NET MVC 4 Ex04-Attributes*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. **Photocontroller**クラスを開き、実行時間の長いタスクをシミュレートするために、1000ミリ秒 (1 秒) の実行を遅延するように**ギャラリー**メソッドを更新します。

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. **Web.config ファイルを**開き、次の要素を追加してカスタムエラーを有効にします。

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. **TimedOut**という名前の新しいビューを**Views\Shared**に作成し、既定のレイアウトを使用します。 ソリューションエクスプローラーで、 **Views\Shared**フォルダーを右クリックし、[追加] を選択します。 **ビュー**。

    ![モバイルデバイスごとに異なるビューを使用する](whats-new-in-aspnet-mvc-4/_static/image36.png "モバイルデバイスごとに異なるビューを使用する")

    *モバイルデバイスごとに異なるビューを使用する*
9. 次に示すように、 **TimedOut** view コンテンツを更新します。

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. アプリケーションを実行し、ルート URL に移動します。 スレッドを追加したときに、1000ミリ秒の**スリープ状態**でタイムアウトエラーが発生し、 **asynctimeout**属性によって生成され、 **HandleError**属性でキャッチされます。

    ![タイムアウト例外の処理](whats-new-in-aspnet-mvc-4/_static/image37.png "タイムアウト例外の処理")

    *タイムアウト例外の処理*

> [!NOTE]
> また、このアプリケーションは、 [「付録 D: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行](#AppendixD)」に従って、Windows Azure の Web サイトにデプロイすることもできます。

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>まとめ

このハンズオンラボでは、ASP.NET MVC 4 に存在する新機能の一部を確認しました。 次の概念について説明しました。

- ASP.NET MVC プロジェクトテンプレートの機能強化を活用する (新しいモバイルアプリケーションプロジェクトテンプレートを含む)
- HTML5 ビューポート属性と CSS メディアクエリを使用してモバイルデバイスの表示を改善する
- JQuery Mobile を使用してプログレッシブ拡張を行い、タッチに最適化された web UI を作成する
- モバイル固有のビューを作成する
- アプリケーションのモバイルビューとデスクトップビューを切り替えるには、ビュースイッチャーコンポーネントを使用します。
- タスクサポートを使用して非同期コントローラーを作成する

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>付録 A: コードスニペットの使用

コードスニペットを使用すると、必要なすべてのコードをすぐに利用できます。 次の図に示すように、ラボドキュメントには、使用できるタイミングがわかります。

![Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する](whats-new-in-aspnet-mvc-4/_static/image38.png "Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する")

*Visual Studio のコードスニペットを使用してプロジェクトにコードを挿入する*

***キーボードを使用してコードスニペットを追加C#するには (のみ)***

1. コードを挿入する場所にカーソルを置きます。
2. (スペースまたはハイフンを含まない) スニペット名の入力を開始します。
3. IntelliSense によって、一致するスニペットの名前が表示されます。
4. 正しいスニペットを選択します (または、スニペットの名前全体が選択されるまで入力し続けます)。
5. Tab キーを2回押すと、スニペットがカーソル位置に挿入されます。

![スニペット名の入力を開始します](whats-new-in-aspnet-mvc-4/_static/image39.png "スニペット名の入力を開始します")

*スニペット名の入力を開始します*

![Tab キーを押して、強調表示されているスニペットを選択します](whats-new-in-aspnet-mvc-4/_static/image40.png "Tab キーを押して、強調表示されているスニペットを選択します")

*Tab キーを押して、強調表示されているスニペットを選択します*

![もう一度 Tab キーを押すと、スニペットが展開されます。](whats-new-in-aspnet-mvc-4/_static/image41.png "もう一度 Tab キーを押すと、スニペットが展開されます。")

*もう一度 Tab キーを押すと、スニペットが展開されます。*

***マウス (C#、VISUAL BASIC および XML) を使用してコードスニペットを追加するには***

1. コードスニペットを挿入する場所を右クリックします。
2. **[スニペットの挿入]** 、 **[マイコードスニペット**] の順に選択します。
3. 一覧から該当するスニペットをクリックして選択します。

![コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。](whats-new-in-aspnet-mvc-4/_static/image42.png "コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。")

*コードスニペットを挿入する場所を右クリックし、[スニペットの挿入] を選択します。*

![一覧から関連するスニペットをクリックして選択します。](whats-new-in-aspnet-mvc-4/_static/image43.png "一覧から関連するスニペットをクリックして選択します。")

*一覧から関連するスニペットをクリックして選択します。*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>付録 B: Visual Studio Express 2012 を Web 用にインストールする

**[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** を使用して、Web または別の &quot;Express&quot; バージョン**用に Microsoft Visual Studio Express 2012**をインストールできます。 次の手順では、 *Microsoft Web Platform Installer*を使用して*Visual studio Express 2012 for Web*をインストールするために必要な手順について説明します。

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)にアクセスします。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、製品 &quot;*Visual Studio Express 2012 For web With Windows AZURE SDK*&quot;を検索することもできます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![Visual Studio Express のインストール](whats-new-in-aspnet-mvc-4/_static/image44.png "Visual Studio Express のインストール")

    *Visual Studio Express のインストール*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](whats-new-in-aspnet-mvc-4/_static/image45.png)

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![Installation progress](whats-new-in-aspnet-mvc-4/_static/image46.png)

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](whats-new-in-aspnet-mvc-4/_static/image47.png)

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。
8. Web 用の Visual Studio Express を開くには、**スタート**画面にアクセスして &quot;**VS Express**&quot;の書き込みを開始し、 **[VS Express for Web]** タイルをクリックします。

    ![VS Express for Web タイル](whats-new-in-aspnet-mvc-4/_static/image48.png)

    *VS Express for Web タイル*

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a>付録 C: WebMatrix 2 と iPhone シミュレーターのインストール

シミュレートされた iPhone デバイスでサイトを実行するには、iPhone の拡張機能 &quot;iPhone の&quot;に使用できます。 また、Visual Studio 2012 からシミュレーターを実行するための同じ拡張機能を構成することもできます。

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a>タスク 1-WebMatrix 2 をインストールする

1. [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169)にアクセスします。 または、Web Platform Installer が既にインストールされている場合は、それを開いて、 *WebMatrix 2*&quot;の製品 &quot;検索することもできます。
2. **[今すぐインストール]** をクリックします。 **Web Platform Installer**がない場合は、最初にダウンロードしてインストールするようにリダイレクトされます。
3. **Web Platform Installer**が開いたら、 **[インストール]** をクリックしてセットアップを開始します。

    ![WebMatrix 2 をインストールする](whats-new-in-aspnet-mvc-4/_static/image49.png "WebMatrix 2 をインストールする")

    *WebMatrix 2 をインストールする*
4. すべての製品のライセンスと条項を読み、[**同意**する] をクリックして続行します。

    ![ライセンス条項に同意する](whats-new-in-aspnet-mvc-4/_static/image50.png "ライセンス条項に同意する")

    *ライセンス条項に同意する*
5. ダウンロードとインストールのプロセスが完了するまで待ちます。

    ![インストールの進行状況](whats-new-in-aspnet-mvc-4/_static/image51.png "Installation progress")

    *インストールの進行状況*
6. インストールが完了したら、 **[完了]** をクリックします。

    ![インストールの完了](whats-new-in-aspnet-mvc-4/_static/image52.png "インストールの完了")

    *インストールの完了*
7. **[終了]** をクリックして Web Platform Installer を閉じます。

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a>タスク 2-iPhone シミュレーター拡張機能のインストール

1. **WebMatrix**を実行し、既存の Web サイトを開くか、新しい Web サイトを作成します。
2. **[ホーム]** リボンの **[実行]** ボタンをクリックし、 **[新規追加]** を選択します。

    ![新しい WebMatrix 拡張機能を追加しています](whats-new-in-aspnet-mvc-4/_static/image53.png "新しい WebMatrix 拡張機能を追加しています")

    *新しい WebMatrix 拡張機能を追加しています*
3. **[IPhone シミュレーター]** を選択し、 **[インストール]** をクリックします。

    ![WebMatrix 拡張機能の参照](whats-new-in-aspnet-mvc-4/_static/image54.png "WebMatrix 拡張機能の参照")

    *WebMatrix 拡張機能の参照*
4. パッケージの詳細 で、**インストール** をクリックして拡張機能のインストールを続行します。

    ![iPhone シミュレーター拡張機能](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone シミュレーター拡張機能")

    *iPhone シミュレーター拡張機能*
5. 拡張機能の EULA を読んで同意します。

    ![WebMatrix 拡張機能の EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 拡張機能の EULA")

    *WebMatrix 拡張機能の EULA*
6. これで、iPhone シミュレーターオプションを使用して WebMatrix から Web サイトを実行できます。

    ![IPhone を使用して実行する](whats-new-in-aspnet-mvc-4/_static/image57.png "IPhone を使用して実行する")

    *IPhone を使用して実行する*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a>タスク 3-iPhone シミュレーターを実行するように Visual Studio 2012 を構成する

1. **Visual Studio 2012**を開き、任意の Web サイトを開くか、新しいプロジェクトを作成します。
2. 実行 ボタンの下矢印をクリックし、**参照** を選択します。

    ![参照](whats-new-in-aspnet-mvc-4/_static/image58.png "参照")

    *参照*
3. [&quot; の &quot;を参照] ダイアログボックスで、 **[追加]** をクリックします。
4. [&quot;プログラム&quot; の追加] ダイアログで、次の値を使用します。

   - **Program**: C:\Users\*{CurrentUser} * \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(それに応じてパスを更新します)*
   - **引数**: &quot;1&quot;
   - **フレンドリ名**: iPhone シミュレーター

     ![プログラムの追加](whats-new-in-aspnet-mvc-4/_static/image59.png "プログラムの追加")

     *参照するプログラムを追加する*
5. [ **OK]** をクリックして、ダイアログを閉じます。
6. これで、iPhone シミュレーターで Visual Studio 2012 から Web アプリケーションを実行できるようになりました。

    ![IPhone シミュレーターを使用して参照する](whats-new-in-aspnet-mvc-4/_static/image60.png "IPhone シミュレーターを使用して参照する")

    *IPhone シミュレーターを使用して参照する*

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>付録 D: Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

この付録では、windows azure 管理ポータルから新しい web サイトを作成し、Windows Azure によって提供される Web 配置公開機能を活用して、ラボに従って取得したアプリケーションを発行する方法について説明します。

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>タスク 1-Windows Azure ポータルから新しい Web サイトを作成する

1. [Windows Azure 管理ポータル](https://manage.windowsazure.com/)にアクセスし、サブスクリプションに関連付けられている Microsoft 資格情報を使用してサインインします。

    > [!NOTE]
    > Windows Azure では、10 ASP.NET の Web サイトを無料でホストし、トラフィックの増加に合わせて拡張できます。 [ここで](https://aka.ms/aspnet-hol-azure)サインアップできます。

    ![Windows Azure portal にログオンします。](whats-new-in-aspnet-mvc-4/_static/image61.png "Windows Azure portal にログオンします。")

    *Windows Azure 管理ポータルにログオンします。*
2. コマンドバーの **[新規]** をクリックします。

    ![新しい Web サイトの作成](whats-new-in-aspnet-mvc-4/_static/image62.png "新しい Web サイトの作成")

    *新しい Web サイトの作成*
3. [ **Compute** | **Web サイト**] をクリックします。 次に、 **[簡易作成]** オプションを選択します。 新しい web サイトの使用可能な URL を指定し、 **[Web サイトの作成]** をクリックします。

    > [!NOTE]
    > Windows Azure の Web サイトは、制御および管理が可能なクラウドで実行されている web アプリケーションのホストです。 [簡易作成] オプションを使用すると、完成した web アプリケーションをポータルの外部から Windows Azure の Web サイトにデプロイできます。 データベースを設定する手順は含まれていません。

    ![簡易作成を使用した新しい Web サイトの作成](whats-new-in-aspnet-mvc-4/_static/image63.png "簡易作成を使用した新しい Web サイトの作成")

    *簡易作成を使用した新しい Web サイトの作成*
4. 新しい**Web サイト**が作成されるまで待ちます。
5. Web サイトが作成されたら、 **[URL]** 列の下のリンクをクリックします。 新しい Web サイトが機能していることを確認します。

    ![新しい web サイトを参照しています](whats-new-in-aspnet-mvc-4/_static/image64.png "新しい web サイトを参照しています")

    *新しい web サイトを参照しています*

    ![実行中の Web サイト](whats-new-in-aspnet-mvc-4/_static/image65.png "実行中の Web サイト")

    *実行中の Web サイト*
6. ポータルに戻り、 **[名前]** 列の下にある web サイトの名前をクリックして、管理ページを表示します。

    ![Web サイトの管理ページを開く](whats-new-in-aspnet-mvc-4/_static/image66.png "Web サイトの管理ページを開く")

    *Web サイトの管理ページを開く*
7. **[ダッシュボード]** ページの **[概要] セクションで**、 **[発行プロファイルのダウンロード]** リンクをクリックします。

    > [!NOTE]
    > *発行プロファイル*には、有効になっている各発行方法について、Windows Azure web サイトに web アプリケーションを発行するために必要なすべての情報が含まれています。 発行プロファイルには、発行メソッドが有効化される各エンドポイントに接続して認証するために必要な URL、ユーザーの資格情報、およびデータベース文字列が含まれています。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**および**Microsoft Visual Studio 2012**では、発行プロファイルを読み取り、Web アプリケーションを Windows Azure websites に発行するためのこれらのプログラムの構成を自動化することがサポートされています。

    ![Web サイト発行プロファイルをダウンロードしています](whats-new-in-aspnet-mvc-4/_static/image67.png "Web サイト発行プロファイルをダウンロードしています")

    *Web サイト発行プロファイルをダウンロードしています*
8. 発行プロファイルファイルを既知の場所にダウンロードします。 この演習では、このファイルを使用して、Visual Studio から Windows Azure Web サイトに web アプリケーションを発行する方法について説明します。

    ![発行プロファイルファイルを保存しています](whats-new-in-aspnet-mvc-4/_static/image68.png "発行プロファイルを保存しています")

    *発行プロファイルファイルを保存しています*

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>タスク 2-データベースサーバーの構成

アプリケーションで SQL Server データベースを使用する場合は、SQL Database サーバーを作成する必要があります。 SQL Server を使用しない単純なアプリケーションを展開する場合は、このタスクを省略できます。

1. アプリケーションデータベースを格納するには、SQL Database サーバーが必要です。 サブスクリプションの**SQL Database サーバーは**、Windows Azure 管理ポータルの**SQL データベース** | サーバー | **サーバーのダッシュボード**で確認できます。 サーバーを作成していない場合は、コマンドバーの **[追加]** ボタンを使用して作成できます。 次のタスクで使用するので、**サーバー名と URL、管理者のログイン名、パスワード**をメモしておきます。 データベースは、後の段階で作成されるため、まだ作成しないでください。

    ![SQL Database サーバーダッシュボード](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database サーバーダッシュボード")

    *SQL Database サーバーダッシュボード*
2. 次のタスクでは、Visual Studio からデータベース接続をテストします。そのため、**使用可能な Ip アドレス**の一覧にローカル ip アドレスを含める必要があります。 これを行うには、 **[構成]** をクリックし、 **[現在のクライアント IP アドレス]** の ip アドレスを選択して、 **[開始 Ip アドレス]** と **[終了 ip アドレス]** のテキストボックスに貼り付け、[![の](whats-new-in-aspnet-mvc-4/_static/image70.png) 追加] をクリックします。

    ![クライアント IP アドレスを追加しています](whats-new-in-aspnet-mvc-4/_static/image71.png)

    *クライアント IP アドレスを追加しています*
3. [許可された IP アドレス] の一覧に**クライアントの Ip アドレス**が追加されたら、 **[保存]** をクリックして変更を確認します。

    ![変更の確認](whats-new-in-aspnet-mvc-4/_static/image72.png)

    *変更の確認*

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>タスク 3-Web 配置を使用した ASP.NET MVC 4 アプリケーションの発行

1. ASP.NET MVC 4 ソリューションに戻ります。 **ソリューションエクスプローラー**で、web サイトプロジェクトを右クリックし、 **[発行]** を選択します。

    ![アプリケーションの発行](whats-new-in-aspnet-mvc-4/_static/image73.png "アプリケーションの発行")

    *Web サイトの公開*
2. 最初のタスクで保存した発行プロファイルをインポートします。

    ![発行プロファイルをインポートしています](whats-new-in-aspnet-mvc-4/_static/image74.png "発行プロファイルをインポートしています")

    *発行プロファイルをインポートしています*
3. **[接続の検証]** をクリックします。 検証が完了したら、 **[次へ]** をクリックします。

    > [!NOTE]
    > 検証が完了すると、[接続の検証] ボタンの横に緑色のチェックマークが表示されます。

    ![接続の検証](whats-new-in-aspnet-mvc-4/_static/image75.png "接続の検証")

    *接続の検証*
4. **[設定]** ページの **[データベース]** セクションで、データベース接続のテキストボックスの横にあるボタン ( **defaultconnection**など) をクリックします。

    ![Web deploy の構成](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy の構成")

    *Web deploy の構成*
5. 次のようにデータベース接続を構成します。

   - **サーバー名**には、 *tcp:* プレフィックスを使用して SQL Database サーバーの URL を入力します。
   - **User name (ユーザー名**) に、サーバー管理者のログイン名を入力します。
   - **パスワード**で、サーバー管理者のログインパスワードを入力します。
   - 新しいデータベース名を入力します (例: *MVC4SampleDB*)。

     ![変換先の接続文字列を構成しています](whats-new-in-aspnet-mvc-4/_static/image77.png "変換先の接続文字列を構成しています")

     *変換先の接続文字列を構成しています*
6. 次に、 **[OK]** をクリックします データベースの作成を求めるメッセージが表示されたら、[**はい]** をクリックします。

    ![データベースの作成](whats-new-in-aspnet-mvc-4/_static/image78.png "データベース文字列の作成")

    *データベースの作成*
7. Windows Azure の SQL Database に接続するために使用する接続文字列は、[既定の接続] ボックスに表示されます。 続けて、 **[次へ]** をクリックします。

    ![SQL Database を指す接続文字列](whats-new-in-aspnet-mvc-4/_static/image79.png "SQL Database を指す接続文字列")

    *SQL Database を指す接続文字列*
8. **[プレビュー]** ページで、 **[発行]** をクリックします。

    ![Web アプリケーションの発行](whats-new-in-aspnet-mvc-4/_static/image80.png "Web アプリケーションの発行")

    *Web アプリケーションの発行*
9. 発行プロセスが完了すると、既定のブラウザーによって公開された web サイトが開きます。

    ![Windows Azure に発行されたアプリケーション](whats-new-in-aspnet-mvc-4/_static/image81.png "Windows Azure に発行されたアプリケーション")

    *Windows Azure に発行されたアプリケーション*

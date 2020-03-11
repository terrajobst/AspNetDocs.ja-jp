---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: モデル、ビュー、およびコントローラーについC#て () |Microsoft Docs
author: StephenWalther
description: モデル、ビュー、およびコントローラーについて混同されていない場合は、 このチュートリアルでは、Stephen Walther が ASP.NET MVC アプリケーションのさまざまな部分について説明します。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: 57dc82d02d38adc2514aa2c02c6f156ed0fb88a6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486088"
---
# <a name="understanding-models-views-and-controllers-c"></a>モデル、ビュー、コントローラーを理解する (C#)

[Stephen Walther](https://github.com/StephenWalther)

> モデル、ビュー、およびコントローラーについて混同されていない場合は、 このチュートリアルでは、Stephen Walther が ASP.NET MVC アプリケーションのさまざまな部分について説明します。

このチュートリアルでは、ASP.NET MVC モデル、ビュー、およびコントローラーの概要について説明します。 言い換えると、ASP.NET MVC では M '、V '、および C ' が説明されています。

このチュートリアルを読んだ後、ASP.NET MVC アプリケーションのさまざまな部分がどのように連携するかを理解する必要があります。 また、ASP.NET MVC アプリケーションのアーキテクチャが ASP.NET Web フォームアプリケーションまたは Active Server ページアプリケーションとどのように異なるかについても理解しておく必要があります。

## <a name="the-sample-aspnet-mvc-application"></a>サンプル ASP.NET MVC アプリケーション

ASP.NET MVC Web アプリケーションを作成するための既定の Visual Studio テンプレートには、ASP.NET MVC アプリケーションのさまざまな部分を理解するために使用できる、非常に単純なサンプルアプリケーションが含まれています。 このチュートリアルでは、このシンプルなアプリケーションを利用します。

MVC テンプレートを使用して新しい ASP.NET MVC アプリケーションを作成するには、Visual Studio 2008 を起動し、メニューオプションファイル [新しいプロジェクト] を選択します (図1を参照)。 新しいプロジェクト ダイアログボックスで、プロジェクトの種類 (Visual Basic またはC#) で任意のプログラミング言語を選択し、テンプレート で  **ASP.NET MVC Web アプリケーション** を選択します。 [OK] ボタンをクリックします。

[[新しいプロジェクトの ![] ダイアログ](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)

**図 01**: [新しいプロジェクト] ダイアログボックス ([クリックすると、フルサイズの画像が表示](understanding-models-views-and-controllers-cs/_static/image2.png)される)

新しい ASP.NET MVC アプリケーションを作成すると、 **[単体テストプロジェクトの作成]** ダイアログボックスが表示されます (図2を参照)。 このダイアログボックスでは、ASP.NET MVC アプリケーションをテストするためのソリューションに別のプロジェクトを作成できます。 **[いいえ、単体テストプロジェクトを作成しません]** オプションを選択し、 **[OK]** ボタンをクリックします。

[![単体テストの作成 ダイアログ](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)

**図 02**: 単体テストダイアログを作成[する (クリックすると、フルサイズの画像が表示](understanding-models-views-and-controllers-cs/_static/image4.png)される)

新しい ASP.NET MVC アプリケーションが作成された後。 [ソリューションエクスプローラー] ウィンドウに複数のフォルダーとファイルが表示されます。 特に、モデル、ビュー、およびコントローラーという名前の3つのフォルダーが表示されます。 フォルダー名から推測されるように、これらのフォルダーには、モデル、ビュー、およびコントローラーを実装するためのファイルが含まれています。

Controllers フォルダーを展開すると、AccountController.cs という名前のファイルと HomeController.cs という名前のファイルが表示されます。 Views フォルダーを展開すると、"Account"、"Home"、および "Shared" という名前の3つのサブフォルダーが表示されます。 [ホーム] フォルダーを展開すると、"About .aspx" と "Index .aspx" という名前の2つの追加ファイルが表示されます (図3を参照)。 これらのファイルは、既定の ASP.NET MVC テンプレートに含まれるサンプルアプリケーションを構成します。

[[ソリューションエクスプローラー] ウィンドウの ![](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)

**図 03**: ソリューションエクスプローラーウィンドウ ([クリックしてフルサイズの画像を表示する](understanding-models-views-and-controllers-cs/_static/image6.png))

このサンプルアプリケーションを実行するには、デバッグ メニューの **デバッグの開始** をクリックします。 または、F5 キーを押してもかまいません。

ASP.NET アプリケーションを初めて実行すると、図4のダイアログが表示され、デバッグモードを有効にすることをお勧めします。 [OK] ボタンをクリックすると、アプリケーションが実行されます。

[![デバッグが有効になっていません ダイアログ](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)

**図 04**: デバッグが有効になっていないダイアログボックス ([クリックすると、フルサイズの画像が表示](understanding-models-views-and-controllers-cs/_static/image8.png)されます)

ASP.NET MVC アプリケーションを実行すると、Visual Studio によって web ブラウザーでアプリケーションが起動されます。 サンプルアプリケーションは、インデックスページと [バージョン情報] ページの2つのページで構成されています。 アプリケーションを初めて起動すると、インデックスページが表示されます (図5を参照)。 [バージョン情報] ページに移動するには、アプリケーションの右上にあるメニューリンクをクリックします。

[インデックスページの ![](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)

**図 05**: インデックスページ ([クリックすると、フルサイズの画像が表示](understanding-models-views-and-controllers-cs/_static/image11.png)されます)

ブラウザーのアドレスバーに Url が表示されます。 たとえば、[バージョン情報] メニューリンクをクリックすると、ブラウザーのアドレスバーの URL が **/Home/About**に変わります。

ブラウザーウィンドウを閉じて Visual Studio に戻ると、[ホーム]、[バージョン情報] のパスのファイルを見つけることができなくなります。 ファイルが存在しません。 設定できないのでしょうか。

## <a name="a-url-does-not-equal-a-page"></a>URL がページと一致しません

従来の ASP.NET Web フォームアプリケーションまたは Active Server ページアプリケーションをビルドする場合、URL とページの間に1対1の対応があります。 サーバーから ".aspx" という名前のページを要求すると、ディスク上のページに ".aspx" という名前が付けられていることがわかります。 ページ .aspx ファイルが存在しない場合は、 **404-ページが見つかりませんでし**たというエラーが表示されます。

一方、ASP.NET MVC アプリケーションをビルドする場合は、ブラウザーのアドレスバーに入力した URL と、アプリケーションで検出されたファイルの間には対応していません。 ASP.NET MVC アプリケーションでは、URL はディスク上のページではなく、コントローラーアクションに対応します。

従来の ASP.NET または ASP アプリケーションでは、ブラウザーの要求はページにマップされます。 一方、ASP.NET MVC アプリケーションでは、ブラウザーの要求はコントローラーアクションにマップされます。 ASP.NET Web フォームアプリケーションは、コンテンツ中心です。 これに対して、ASP.NET MVC アプリケーションはアプリケーションロジック中心です。

## <a name="understanding-aspnet-routing"></a>ASP.NET ルーティングについて

Browser 要求は、 *ASP.NET Routing*と呼ばれる ASP.NET フレームワークの機能を介して、コントローラーアクションにマップされます。 ASP.NET Routing は、着信要求をコントローラーアクションに*ルーティング*するために ASP.NET MVC フレームワークによって使用されます。

ASP.NET ルーティングは、ルートテーブルを使用して受信要求を処理します。 このルートテーブルは、web アプリケーションの初回起動時に作成されます。 ルートテーブルは、global.asax ファイルに設定されます。 既定の MVC global.asax ファイルは、リスト1に含まれています。

**リスト 1-global.asax**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

ASP.NET アプリケーションを初めて起動すると、アプリケーション\_Start () メソッドが呼び出されます。 リスト1では、このメソッドは RegisterRoutes () メソッドを呼び出し、RegisterRoutes () メソッドは既定のルートテーブルを作成します。

既定のルートテーブルは、1つのルートで構成されます。 この既定のルートでは、すべての受信要求が3つのセグメントに分割されます (URL セグメントは、スラッシュの間の任意のものです)。 最初のセグメントはコントローラー名にマップされ、2番目のセグメントはアクション名にマップされ、最後のセグメントは、Id という名前のアクションに渡されるパラメーターにマップされます。

たとえば、次のような URL があるとします。

/Product/Details/3

この URL は、次のように3つのパラメーターに解析されます。

Controller = 製品

Action = 詳細

id = 3

Global.asax ファイルで定義されている既定のルートには、3つのパラメーターすべての既定値が含まれています。 既定のコントローラーは Home、既定のアクションは Index、既定の Id は空の文字列です。 これらの既定値を考慮して、次の URL がどのように解析されるかを検討します。

/Employee

この URL は、次のように3つのパラメーターに解析されます。

Controller = Employee

Action = インデックス

Id =

最後に、URL (`http://localhost`など) を指定せずに ASP.NET MVC アプリケーションを開くと、URL は次のように解析されます。

コントローラー = ホーム

Action = インデックス

Id =

要求は、HomeController クラスの Index () アクションにルーティングされます。

## <a name="understanding-controllers"></a>コントローラーについて

コントローラーは、ユーザーが MVC アプリケーションと対話する方法を制御する役割を担います。 コントローラーには、ASP.NET MVC アプリケーションのフロー制御ロジックが含まれています。 コントローラーは、ユーザーがブラウザー要求を行ったときにユーザーに返される応答を決定します。

コントローラーは、クラス (Visual Basic やC#クラスなど) にすぎません。 サンプル ASP.NET MVC アプリケーションには、Controllers フォルダーにある HomeController.cs という名前のコントローラーが含まれています。 HomeController.cs ファイルの内容は、リスト2で再現されます。

**リスト 2-HomeController.cs**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

HomeController には、Index () と About () という2つのメソッドがあることに注意してください。 これらの2つのメソッドは、コントローラーによって公開される2つのアクションに対応しています。 URL/Home/Index は HomeController () メソッドを呼び出し、URL/Home/About は HomeController () メソッドを呼び出します。

コントローラー内のパブリックメソッドは、コントローラーアクションとして公開されます。 このことに注意する必要があります。 つまり、コントローラーに含まれているすべてのパブリックメソッドは、ブラウザーに正しい URL を入力することによって、インターネットにアクセスできるすべてのユーザーが呼び出すことができます。

## <a name="understanding-views"></a>ビューについて

HomeController クラスによって公開されている2つのコントローラーアクション (Index () と About ()) は、どちらもビューを返します。 ビューには、ブラウザーに送信される HTML マークアップとコンテンツが含まれています。 ビューは、ASP.NET MVC アプリケーションを操作するときのページに相当します。

適切な場所にビューを作成する必要があります。 HomeController () アクションは、次のパスにあるビューを返します。

\Views\Home\Index.aspx

HomeController () アクションは、次のパスにあるビューを返します。

\Views\Home\About.aspx

一般に、コントローラーアクションのビューを返す場合は、コントローラーと同じ名前のサブフォルダーを Views フォルダーに作成する必要があります。 サブフォルダー内では、コントローラーアクションと同じ名前の .aspx ファイルを作成する必要があります。

リスト3のファイルには、About .aspx ビューが含まれています。

**リスト 3-About .aspx**

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

リスト3の最初の行を無視した場合、ビューの残りの部分のほとんどは標準の HTML で構成されます。 ここで必要な HTML を入力して、ビューの内容を変更できます。

ビューは Active Server ページまたは ASP.NET Web フォームのページによく似ています。 ビューには、HTML コンテンツとスクリプトを含めることができます。 任意の .NET プログラミング言語 (たとえば、 C#や Visual Basic .net) でスクリプトを記述できます。 スクリプトを使用して、データベースデータなどの動的なコンテンツを表示します。

## <a name="understanding-models"></a>モデルについて

コントローラーについて説明し、ビューについて説明しました。 最後に説明する必要のあるトピックは、モデルです。 MVC モデルとは

MVC モデルには、ビューまたはコントローラーに含まれていないアプリケーションロジックがすべて含まれています。 モデルには、アプリケーションのビジネスロジック、検証ロジック、およびデータベースアクセスロジックがすべて含まれている必要があります。 たとえば、データベースにアクセスするために Microsoft Entity Framework を使用している場合は、Entity Framework クラス (.edmx ファイル) を [モデル] フォルダーに作成します。

ビューには、ユーザーインターフェイスの生成に関連するロジックだけを含める必要があります。 コントローラーには、適切なビューを返す、またはユーザーを別のアクション (フロー制御) にリダイレクトするために必要な最小限のロジックのみが含まれている必要があります。 それ以外はすべてモデルに含まれている必要があります。

一般に、fat モデルと skinny コントローラーを使用することをお勧めします。 コントローラーメソッドには数行のコードのみを含める必要があります。 コントローラーアクションが大きすぎる場合は、[モデル] フォルダー内の新しいクラスにロジックを移動することを検討してください。

## <a name="summary"></a>まとめ

このチュートリアルでは、ASP.NET MVC web アプリケーションのさまざまな部分について概要を説明しました。 ASP.NET Routing が着信ブラウザーの要求を特定のコントローラーアクションにマップする方法について学習しました。 コントローラーで、ビューがブラウザーに返される方法を調整する方法について学習しました。 最後に、モデルにアプリケーションのビジネス、検証、およびデータベースアクセスのロジックが含まれていることを学習しました。

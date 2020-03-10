---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWIN Startup クラスの検出 |Microsoft Docs
author: Praburaj
description: このチュートリアルでは、読み込まれる OWIN startup クラスを構成する方法について説明します。 OWIN の詳細については、「Project Katana の概要」を参照してください。 このチュートリアルは...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500182"
---
# <a name="owin-startup-class-detection"></a>OWIN スタートアップ クラス検出

> このチュートリアルでは、読み込まれる OWIN startup クラスを構成する方法について説明します。 OWIN の詳細については、「 [Project Katana の概要](an-overview-of-project-katana.md)」を参照してください。 このチュートリアルは、Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )、Praburaj Thiagarajan、Howard Dierking ( [@howard\_Dierking](https://twitter.com/howard_dierking) ) によって作成されました。
>
> ## <a name="prerequisites"></a>前提条件
>
> [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a>OWIN スタートアップ クラス検出

 すべての OWIN アプリケーションには、アプリケーションパイプラインのコンポーネントを指定する startup クラスがあります。 スタートアップクラスは、選択したホスティングモデル (OwinHost、IIS、および IIS Express) に応じて、ランタイムに接続する方法が異なります。 このチュートリアルで示されている startup クラスは、すべてのホストアプリケーションで使用できます。 スタートアップクラスは、次のいずれかの方法を使用してホスティングランタイムに接続します。

1. **名前付け規則**: Katana は、アセンブリ名またはグローバル名前空間に一致する名前空間内の `Startup` という名前のクラスを検索します。
2. **Owinstartup 属性**: これは、ほとんどの開発者がスタートアップクラスを指定するために実行するアプローチです。 次の属性は、startup クラスを `StartupDemo` 名前空間の `TestStartup` クラスに設定します。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   `OwinStartup` 属性は、名前付け規則をオーバーライドします。 この属性を使用してフレンドリ名を指定することもできますが、フレンドリ名を使用するには、構成ファイルの `appSetting` 要素も使用する必要があります。
3. **構成ファイルの appSetting 要素**: `appSetting` 要素は、`OwinStartup` 属性と名前付け規則をオーバーライドします。 (それぞれ `OwinStartup` 属性を使用して) 複数のスタートアップクラスを設定し、次のようなマークアップを使用して構成ファイルに読み込むスタートアップクラスを構成することができます。

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   スタートアップクラスとアセンブリを明示的に指定する次のキーを使用することもできます。

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   構成ファイルの次の XML では、`ProductionConfiguration`のわかりやすいスタートアップクラス名を指定しています。

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   上のマークアップは、フレンドリ名を指定し、`ProductionStartup2` クラスを実行する次の `OwinStartup` 属性と共に使用する必要があります。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. OWIN スタートアップ検出を無効にするには、web.config ファイルで `"false"` の値を使用して `appSetting owin:AutomaticAppStartup` を追加します。

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a>OWIN Startup を使用して ASP.NET Web アプリを作成する

1. 空の Asp.Net web アプリケーションを作成し、 **Startupdemo**という名前を指定します。 -NuGet パッケージマネージャーを使用して `Microsoft.Owin.Host.SystemWeb` をインストールします。 **[ツール]** メニューの **[NuGet パッケージマネージャー]** をポイントし、 **[パッケージマネージャーコンソール]** をクリックします。 次のコマンドを入力します。

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. OWIN startup クラスを追加します。 Visual Studio 2017 でプロジェクトを右クリックし、 **[クラスの追加]** を選択します。 **[新しい項目の追加]** ダイアログボックスで、検索フィールドに「 *OWIN* 」と入力し、名前を「Startup.cs」に変更し、 **[追加]** を選択します。

     ![](owin-startup-class-detection/_static/image1.png)

   次に*Owin Startup クラス*を追加するときに、 **[追加]** メニューから使用できるようになります。

     ![](owin-startup-class-detection/_static/image2.png)

   または、プロジェクトを右クリックし、 **[追加]** 、 **[新しい項目]** の順に選択して、 **Owin Startup クラス**を選択します。

     ![](owin-startup-class-detection/_static/image3.png)

- *Startup.cs*ファイル内の生成されたコードを次のコードに置き換えます。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  `app.Use` のラムダ式は、指定されたミドルウェアコンポーネントを OWIN パイプラインに登録するために使用されます。 この例では、受信要求に応答する前に、受信要求のログ記録を設定しています。 `next` パラメーターは、パイプラインの次のコンポーネントに対するデリゲート ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt;[タスク](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx)&gt;) です。 `app.Run` のラムダ式は、パイプラインを受信要求にフックし、応答機構を提供します。
     > [!NOTE]
     > 上記のコードでは、`OwinStartup` 属性をコメントアウトし、`Startup` という名前のクラスを実行する規則に依存しています。- ***F5***キーを押してアプリケーションを実行します。 数回更新します。

    ![](owin-startup-class-detection/_static/image4.png) メモ: このチュートリアルの画像に示されている数字は、表示される数字と一致しません。 ミリ秒の文字列は、ページを更新したときに新しい応答を表示するために使用されます。
  **[出力]** ウィンドウにトレース情報が表示されます。

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a>スタートアップクラスをさらに追加する

このセクションでは、別のスタートアップクラスを追加します。 複数の OWIN startup クラスをアプリケーションに追加できます。 たとえば、開発、テスト、および運用のスタートアップクラスを作成することができます。

1. 新しい OWIN Startup クラスを作成し、`ProductionStartup`という名前を指定します。
2. 生成されたコードを次のコードに置き換えます。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. Ctrl F5 キーを押してアプリを実行します。 `OwinStartup` 属性は、実稼働スタートアップクラスを実行することを指定します。

    ![](owin-startup-class-detection/_static/image6.png)
4. 別の OWIN Startup クラスを作成し、`TestStartup`という名前を指定します。
5. 生成されたコードを次のコードに置き換えます。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   上の `OwinStartup` 属性オーバーロードは、スタートアップクラスの*フレンドリ*名として `TestingConfiguration` を指定します。
6. *Web.config ファイルを*開き、スタートアップクラスのフレンドリ名を指定する OWIN App スタートアップキーを追加します。

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. Ctrl F5 キーを押してアプリを実行します。 アプリ設定要素が優先され、テスト構成が実行されます。

    ![](owin-startup-class-detection/_static/image7.png)
8. `TestStartup` クラスの `OwinStartup` 属性から*表示名を削除します*。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. *Web.config ファイルの*OWIN App スタートアップキーを次のように置き換えます。

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. 各クラスの `OwinStartup` 属性を、Visual Studio によって生成される既定の属性コードに戻します。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    次に示す OWIN App スタートアップキーを使うと、実稼働クラスが実行されます。

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    最後のスタートアップキーは、スタートアップの構成方法を指定します。 次の OWIN App スタートアップキーを使用すると、構成クラスの名前を `MyConfiguration` に変更できます。

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a>Owinhost .exe の使用

1. Web.config ファイルを次のマークアップに置き換えます。

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   最後のキーが優先されるため、この場合は `TestStartup` が指定されます。
2. PMC から Owinhost をインストールします。

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. アプリケーションフォルダー ( *web.config ファイルが格納されて*いるフォルダー) に移動し、コマンドプロンプトで次のように入力します。

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   次のコマンドウィンドウが表示されます。

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. URL `http://localhost:5000/`でブラウザーを起動します。

    ![](owin-startup-class-detection/_static/image8.png)

   OwinHost は、上記のスタートアップ規約を受け入れています。
5. コマンドウィンドウで、Enter キーを押して OwinHost を終了します。
6. `ProductionStartup` クラスで、 *ProductionConfiguration*のフレンドリ名を指定する次の OwinStartup 属性を追加します。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. コマンドプロンプトで、次のように入力します。

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   Production startup クラスが読み込まれます。
    ![](owin-startup-class-detection/_static/image9.png)

   このアプリケーションには複数のスタートアップクラスがあります。この例では、ランタイムまで読み込まれるスタートアップクラスを遅延しています。
8. 次のランタイムスタートアップオプションをテストします。

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]

---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: OData v4 クライアント アプリ (c#) の作成 | Microsoft ドキュメント
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448120"
---
# <a name="create-an-odata-v4-client-app-c"></a>OData v4 クライアント アプリ (c#) の作成

[Mike Wasson](https://github.com/MikeWasson)

前のチュートリアルでは、CRUD 操作をサポートする基本的な OData サービスを作成しました。 次はサービスのクライアントを作成しましょう。

Visual Studio の新しいインスタンスを開始し、新しいコンソール アプリケーション プロジェクトを作成します。 **新しいプロジェクト** ダイアログで、 **インストールされている**&gt;**テンプレート** &gt; **Visual C#**  &gt; **Windows デスクトップ** を選択し、**コンソールアプリケーション** テンプレートを選択します。 プロジェクトに &quot;製品アプリ&quot;という名前を指定します。

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> OData サービスを含んでいる同じ Visual Studio ソリューションにコンソール アプリを追加することもできます。

## <a name="install-the-odata-client-code-generator"></a>OData Client Code Generator をインストールする

**[ツール]** メニューの **[拡張機能と更新プログラム]** を選択します。 [**オンライン**&gt; **Visual Studio ギャラリー**] を選択します。 検索ボックスで、&quot;OData クライアントコードジェネレーター&quot;を検索します。 **[ダウンロード]** をクリックして、VSIX をインストールします。 ここでは　Visual Studio の再起動を求められることがあります。

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a>OData サービスをローカルで実行する

Visual Studio から ProductService プロジェクトを実行します。 既定では、Visual Studio はアプリケーション ルートに対してブラウザーを起動します。 次の手順で必要になるので、ここでの URI を書き留めておいてください。 アプリケーションは実行されている状態のままにします。

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> 同じソリューションに両方のプロジェクトを配置する場合は ProductService プロジェクトがデバッグをせずに実行されていることを確認してください。 次の手順では、コンソール アプリケーション プロジェクトを変更している間、サービスが実行され続けている必要があります。

## <a name="generate-the-service-proxy"></a>サービス プロキシを生成する

サービスプロキシは、OData サービスにアクセスするためのメソッドを定義する .NET クラスです。 プロキシは、メソッドの呼び出しを HTTP 要求に変換します。 [T4 テンプレート](https://msdn.microsoft.com/library/bb126445.aspx)を実行して、プロキシクラスを作成します。

プロジェクトで右クリックします。 **[追加]** &gt; **[新しい項目]** の順に選択します。

![](create-an-odata-v4-client-app/_static/image5.png)

**新しい項目の追加** ダイアログで、**コード**&gt; **OData クライアント**&gt; コードを選択し**C#** ます。 テンプレートに ProductClient.tt&quot;&quot;名前を指定します。 **追加** をクリックし、セキュリティの警告 をクリックします。

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

この時点でエラーが表示されますが、無視してもよいものです。 Visual Studio は、自動的にテンプレートを実行させますが、このテンプレートは最初にいくつかの構成設定を必要とします。

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

ProductClient. odata. .config ファイルを開きます。`Parameter` 要素で、ProductService プロジェクトの URI (前の手順) を貼り付けます。 次に例を示します。

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

テンプレートをもう一度実行してください。 ソリューションエクスプローラーで、ProductClient.tt ファイルを右クリックし、 **[カスタムツールの実行]** を選択します。

テンプレートは、プロキシを定義する ProductClient.cs という名前のコード ファイルを作成します。 アプリを開発するときに、OData エンドポイントを変更した場合は、プロキシを更新するためにテンプレートを再実行してください。

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a>OData サービスの呼び出すためにサービス プロキシを使用する

Program.cs ファイルを開き、定型コードを次のコードに置き換えます。

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

*Serviceuri*の値を、前のサービス uri に置き換えます。

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

アプリを実行すると、次のような出力を得られるはずです。

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]

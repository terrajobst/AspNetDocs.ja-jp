---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: 単体テスト ASP.NET Web API 2 |Microsoft Docs
author: Rick-Anderson
description: このガイダンスとアプリケーションでは、Web API 2 アプリケーションの単純な単体テストを作成する方法を示します。 このチュートリアルでは、単体テストを含める方法について説明します...
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446986"
---
# <a name="unit-testing-aspnet-web-api-2"></a>単体テスト ASP.NET Web API 2

[Tom FitzMacken](https://github.com/tfitzmac)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> このガイダンスとアプリケーションでは、Web API 2 アプリケーションの単純な単体テストを作成する方法を示します。 このチュートリアルでは、ソリューションに単体テストプロジェクトを追加し、コントローラーメソッドから返された値を確認するテストメソッドを記述する方法について説明します。
>
> このチュートリアルでは、ASP.NET Web API の基本的な概念を理解していることを前提としています。 入門用のチュートリアルについては、「 [ASP.NET Web API 2 を使用したはじめに](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)」を参照してください。
>
> このトピックの単体テストは、単純なデータのシナリオに意図的に限定されています。 より高度なデータシナリオの単体テストについては、「[単体テスト ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)」の「モック Entity Framework」を参照してください。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2

## <a name="in-this-topic"></a>このトピックの内容

このトピックには、次のセクションが含まれます。

- [前提条件](#prereqs)
- [コードのダウンロード](#download)
- [単体テストプロジェクトを使用したアプリケーションの作成](#appwithunittest)
    - [アプリケーションの作成時に単体テストプロジェクトを追加する](#whencreate)
    - [既存のアプリケーションに単体テストプロジェクトを追加する](#addtoexisting)
- [Web API 2 アプリケーションをセットアップする](#setupproject)
- [テストプロジェクトに NuGet パッケージをインストールする](#testpackages)
- [テストの作成](#tests)
- [テストの実行](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a>前提条件

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)Community、Professional、または Enterprise edition

<a id="download"></a>
## <a name="download-code"></a>コードをダウンロードする

完成し[たプロジェクト](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)をダウンロードします。 ダウンロード可能なプロジェクトには、このトピックの単体テストコードと、[単体テスト ASP.NET Web API トピックのモック Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)が含まれています。

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>単体テストプロジェクトを使用したアプリケーションの作成

アプリケーションを作成するとき、または既存のアプリケーションに単体テストプロジェクトを追加するときに、単体テストプロジェクトを作成することができます。 このチュートリアルでは、単体テストプロジェクトを作成する2つの方法について説明します。 このチュートリアルを実行するには、どちらの方法でも使用できます。

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a>アプリケーションの作成時に単体テストプロジェクトを追加する

**Storeapp**という名前の新しい ASP.NET Web アプリケーションを作成します。

![プロジェクトの作成](unit-testing-with-aspnet-web-api/_static/image1.png)

New ASP.NET プロジェクトウィンドウで、**空**のテンプレートを選択し、Web API のフォルダーとコア参照を追加します。 **[単体テストの追加]** オプションを選択します。 単体テストプロジェクトには、 **Storeapp.** test という名前が自動的に付けられます。 この名前をそのまま使用できます。

![単体テストプロジェクトの作成](unit-testing-with-aspnet-web-api/_static/image2.png)

アプリケーションを作成すると、2つのプロジェクトが含まれていることがわかります。

![2つのプロジェクト](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a>既存のアプリケーションに単体テストプロジェクトを追加する

アプリケーションの作成時に単体テストプロジェクトを作成しなかった場合は、いつでも追加できます。 たとえば、StoreApp という名前のアプリケーションが既にあり、単体テストを追加するとします。 単体テストプロジェクトを追加するには、ソリューションを右クリックし、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

![ソリューションへの新しいプロジェクトの追加](unit-testing-with-aspnet-web-api/_static/image4.png)

左ペインで **[テスト]** を選択し、プロジェクトの種類として **[単体テストプロジェクト]** を選択します。 プロジェクトに Storeapp という名前を指定し**ます。**

![単体テストプロジェクトの追加](unit-testing-with-aspnet-web-api/_static/image5.png)

ソリューションに単体テストプロジェクトが表示されます。

単体テストプロジェクトで、元のプロジェクトへのプロジェクト参照を追加します。

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a>Web API 2 アプリケーションをセットアップする

StoreApp プロジェクトで、 **Product.cs**という名前の**モデル**フォルダーにクラスファイルを追加します。 このファイルの内容を次のコードに置き換えます。

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

ソリューションをビルドします。

Controllers フォルダーを右クリックし、 **[追加]** 、 **[新しいスキャフォールディング項目]** の順に選択します。 **[WEB API 2 コントローラー-空]** を選択します。

![新しいコントローラーの追加](unit-testing-with-aspnet-web-api/_static/image6.png)

コントローラー名を**Simpleproductcontroller**に設定し、 **[追加]** をクリックします。

![コントローラーの指定](unit-testing-with-aspnet-web-api/_static/image7.png)

既存のコードを次のコードに置き換えます。 この例を簡略化するために、データはデータベースではなく一覧に格納されます。 このクラスで定義されているリストは、実稼働データを表します。 コントローラーには、製品オブジェクトの一覧をパラメーターとして受け取るコンストラクターが含まれていることに注意してください。 このコンストラクターを使用すると、単体テスト時にテストデータを渡すことができます。 また、このコントローラーには、非同期メソッドの単体テストを示す2つの**非同期**メソッドも含まれています。 これらの非同期メソッドは、余分なコードを最小限に抑えるために、 **FromResult**を呼び出すことによって実装されましたが、通常、メソッドにはリソースを大量に消費する操作が含まれます。

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

GetProduct メソッドは、 **Ihttpactionresult**インターフェイスのインスタンスを返します。 IHttpActionResult は、Web API 2 の新機能の1つであり、単体テストの開発を簡略化します。 IHttpActionResult インターフェイスを実装するクラスは、System.web. [http.sys](https://msdn.microsoft.com/library/system.web.http.results.aspx)名前空間にあります。 これらのクラスは、アクション要求からの応答を表し、HTTP ステータスコードに対応します。

ソリューションをビルドします。

これで、テストプロジェクトを設定する準備ができました。

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>テストプロジェクトに NuGet パッケージをインストールする

空のテンプレートを使用してアプリケーションを作成する場合、単体テストプロジェクト (StoreApp. Tests) には、インストールされている NuGet パッケージは含まれません。 Web API テンプレートなどの他のテンプレートには、単体テストプロジェクトにいくつかの NuGet パッケージが含まれています。 このチュートリアルでは、テストプロジェクトに Microsoft ASP.NET Web API 2 コアパッケージを含める必要があります。

StoreApp. Tests プロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選択します。 パッケージをプロジェクトに追加するには、StoreApp. Tests プロジェクトを選択する必要があります。

![パッケージの管理](unit-testing-with-aspnet-web-api/_static/image8.png)

Microsoft ASP.NET Web API 2 コアパッケージを検索してインストールします。

![web api core パッケージのインストール](unit-testing-with-aspnet-web-api/_static/image9.png)

[NuGet パッケージの管理] ウィンドウを閉じます。

<a id="tests"></a>
## <a name="create-tests"></a>テストの作成

既定では、テストプロジェクトには、UnitTest1.cs という名前の空のテストファイルが含まれています。 このファイルには、テストメソッドの作成に使用する属性が表示されます。 単体テストでは、このファイルを使用するか、独自のファイルを作成することができます。

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

このチュートリアルでは、独自のテストクラスを作成します。 UnitTest1.cs ファイルを削除できます。 **TestSimpleProductController.cs**という名前のクラスを追加し、コードを次のコードに置き換えます。

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>テストの実行

これで、テストを実行する準備が整いました。 "完了 **" 属性で**マークされているすべてのメソッドがテストされます。 **[テスト]** メニュー項目から、テストを実行します。

![テストの実行](unit-testing-with-aspnet-web-api/_static/image11.png)

**[テストエクスプローラー]** ウィンドウを開き、テストの結果を確認します。

![テスト結果](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a>まとめ

これで、このチュートリアルが完了しました。 このチュートリアルのデータは、単体テストの条件に焦点を当てるために意図的に簡略化されています。 より高度なデータシナリオの単体テストについては、「[単体テスト ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)」の「モック Entity Framework」を参照してください。

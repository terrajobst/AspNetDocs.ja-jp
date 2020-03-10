---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: 単体テスト ASP.NET Web API 2 | のモック Entity FrameworkMicrosoft Docs
author: Rick-Anderson
description: このガイドとアプリケーションでは、Entity Framework を使用する Web API 2 アプリケーションの単体テストを作成する方法を示します。 変更する方法を示しています...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447088"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a>単体テスト時のモック Entity Framework ASP.NET Web API 2

[Tom FitzMacken](https://github.com/tfitzmac)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> このガイドとアプリケーションでは、Entity Framework を使用する Web API 2 アプリケーションの単体テストを作成する方法を示します。 スキャフォールディングコントローラーを変更して、テスト用のコンテキストオブジェクトを渡すことができるようにする方法と、Entity Framework で使用するテストオブジェクトを作成する方法を示します。
>
> ASP.NET Web API を使用した単体テストの概要については、「 [ASP.NET Web API 2 を使用した単体](unit-testing-with-aspnet-web-api.md)テスト」を参照してください。
>
> このチュートリアルでは、ASP.NET Web API の基本的な概念を理解していることを前提としています。 入門用のチュートリアルについては、「 [ASP.NET Web API 2 を使用したはじめに](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)」を参照してください。
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
- [モデルクラスを作成する](#modelclass)
- [コントローラーの追加](#controller)
- [依存関係の挿入の追加](#dependency)
- [テストプロジェクトに NuGet パッケージをインストールする](#testpackages)
- [テストコンテキストの作成](#testcontext)
- [テストの作成](#tests)
- [テストの実行](#runtests)

[ASP.NET Web API 2 での単体テスト](unit-testing-with-aspnet-web-api.md)の手順を既に完了している場合は、「[コントローラーを追加](#controller)する」のセクションに進んでください。

<a id="prereqs"></a>
## <a name="prerequisites"></a>前提条件

Visual Studio 2017 Community、Professional、または Enterprise edition

<a id="download"></a>
## <a name="download-code"></a>コードをダウンロードする

完成し[たプロジェクト](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)をダウンロードします。 ダウンロード可能なプロジェクトには、このトピックの単体テストコードと[単体テスト ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)のトピックが含まれています。

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>単体テストプロジェクトを使用したアプリケーションの作成

アプリケーションを作成するとき、または既存のアプリケーションに単体テストプロジェクトを追加するときに、単体テストプロジェクトを作成することができます。 このチュートリアルでは、アプリケーションの作成時に単体テストプロジェクトを作成する方法について説明します。

**Storeapp**という名前の新しい ASP.NET Web アプリケーションを作成します。

New ASP.NET プロジェクトウィンドウで、**空**のテンプレートを選択し、Web API のフォルダーとコア参照を追加します。 **[単体テストの追加]** オプションを選択します。 単体テストプロジェクトには、 **Storeapp.** test という名前が自動的に付けられます。 この名前をそのまま使用できます。

![単体テストプロジェクトの作成](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

アプリケーションを作成した後、2つのプロジェクトが含まれていることがわかります ( **storeapp**と**Storeapp. テスト**)。

<a id="modelclass"></a>
## <a name="create-the-model-class"></a>モデルクラスを作成する

StoreApp プロジェクトで、 **Product.cs**という名前の**モデル**フォルダーにクラスファイルを追加します。 このファイルの内容を次のコードに置き換えます。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

ソリューションをビルドします。

<a id="controller"></a>
## <a name="add-the-controller"></a>コントローラーの追加

Controllers フォルダーを右クリックし、 **[追加]** 、 **[新しいスキャフォールディング項目]** の順に選択します。 Entity Framework を使用して、アクションがある Web API 2 コントローラーを選択します。

![新しいコントローラーの追加](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

次の値を設定します。

- コントローラー名: **Productcontroller**
- モデルクラス: **Product**
- データコンテキストクラス: [**新しいデータコンテキスト**を選択] をクリックすると、以下の値が表示されます。

![コントローラーの指定](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

自動的に生成されたコードを使用してコントローラーを作成するには、 **[追加]** をクリックします。 このコードには、Product クラスのインスタンスを作成、取得、更新、および削除するメソッドが含まれています。 次のコードは、製品を追加する方法を示しています。 メソッドが**Ihttpactionresult**のインスタンスを返すことに注意してください。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

IHttpActionResult は、Web API 2 の新機能の1つであり、単体テストの開発を簡略化します。

次のセクションでは、生成されたコードをカスタマイズして、テストオブジェクトをコントローラーに渡すのを容易にします。

<a id="dependency"></a>
## <a name="add-dependency-injection"></a>依存関係の挿入の追加

現在、ProductController クラスは、StoreAppContext クラスのインスタンスを使用するようにハードコーディングされています。 依存関係の注入と呼ばれるパターンを使用して、アプリケーションを変更し、ハードコーディングされた依存関係を削除します。 この依存関係を分割することにより、テスト時にモックオブジェクトを渡すことができます。

**[モデル]** フォルダーを右クリックし、 **Istoreappcontext**という名前の新しいインターフェイスを追加します。

このコードを次のコードに置き換えます。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

StoreAppContext.cs ファイルを開き、次の強調表示された変更を行います。 注意すべき重要な変更点は次のとおりです。

- StoreAppContext クラスは IStoreAppContext インターフェイスを実装します
- MarkAsModified メソッドが実装されています

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

ProductController.cs ファイルを開きます。 強調表示されたコードに一致するように既存のコードを変更します。 これらの変更により、StoreAppContext の依存関係が解除され、他のクラスがコンテキストクラスの別のオブジェクトを渡すことができるようになります。 この変更により、単体テスト中にテストコンテキストを渡すことができます。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

ProductController でもう1つの変更を行う必要があります。 **Putproduct**メソッドで、エンティティの状態を設定する行を MarkAsModified メソッドの呼び出しに置き換えます。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

ソリューションをビルドします。

これで、テストプロジェクトを設定する準備ができました。

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>テストプロジェクトに NuGet パッケージをインストールする

空のテンプレートを使用してアプリケーションを作成する場合、単体テストプロジェクト (StoreApp. Tests) には、インストールされている NuGet パッケージは含まれません。 Web API テンプレートなどの他のテンプレートには、単体テストプロジェクトにいくつかの NuGet パッケージが含まれています。 このチュートリアルでは、Entity Framework パッケージと Microsoft ASP.NET Web API 2 コアパッケージをテストプロジェクトに含める必要があります。

StoreApp. Tests プロジェクトを右クリックし、 **[NuGet パッケージの管理]** を選択します。 パッケージをプロジェクトに追加するには、StoreApp. Tests プロジェクトを選択する必要があります。

![パッケージの管理](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

オンラインパッケージから EntityFramework パッケージ (バージョン6.0 以降) を検索してインストールします。 EntityFramework パッケージが既にインストールされている場合は、StoreApp. Tests プロジェクトではなく StoreApp プロジェクトを選択している可能性があります。

![Entity Framework の追加](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

Microsoft ASP.NET Web API 2 コアパッケージを検索してインストールします。

![web api core パッケージのインストール](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

[NuGet パッケージの管理] ウィンドウを閉じます。

<a id="testcontext"></a>
## <a name="create-test-context"></a>テストコンテキストの作成

**Testdbset**という名前のクラスをテストプロジェクトに追加します。 このクラスは、テストデータセットの基本クラスとして機能します。 このコードを次のコードに置き換えます。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

**Testproductdbset**という名前のクラスをテストプロジェクトに追加します。このクラスには、次のコードが含まれています。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

**Teststoreappcontext**という名前のクラスを追加し、既存のコードを次のコードに置き換えます。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a>テストの作成

既定では、テストプロジェクトには、 **UnitTest1.cs**という名前の空のテストファイルが含まれています。 このファイルには、テストメソッドの作成に使用する属性が表示されます。 このチュートリアルでは、新しいテストクラスを追加するため、このファイルを削除できます。

**Testproductcontroller**という名前のクラスをテストプロジェクトに追加します。 このコードを次のコードに置き換えます。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>テストの実行

これで、テストを実行する準備が整いました。 "完了 **" 属性で**マークされているすべてのメソッドがテストされます。 **[テスト]** メニュー項目から、テストを実行します。

![テストの実行](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

**[テストエクスプローラー]** ウィンドウを開き、テストの結果を確認します。

![テスト結果](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)

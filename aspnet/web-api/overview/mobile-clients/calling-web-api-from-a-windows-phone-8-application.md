---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: Windows Phone 8 アプリケーションから Web API を呼び出す (C#)-ASP.NET 4.x
author: rmcmurray
description: 'コードを使用したチュートリアル: Windows Phone 8 アプリケーションに書籍のカタログを提供する、ASP.NET 4.x の ASP.NET Web API アプリケーションを作成します。'
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498214"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a>Windows Phone 8 アプリケーションから Web API を呼び出す (C#)

[Robert McMurray](https://github.com/rmcmurray)

このチュートリアルでは、Windows Phone 8 アプリケーションに書籍のカタログを提供する ASP.NET Web API アプリケーションで構成される完全なエンドツーエンドのシナリオを作成する方法について説明します。

### <a name="overview"></a>概要

ASP.NET Web API のような RESTful サービスは、サーバー側とクライアント側のアプリケーションのアーキテクチャを抽象化することによって、開発者のための HTTP ベースのアプリケーションの作成を簡略化します。 Web API 開発者は、通信用に専用のソケットベースのプロトコルを作成するのではなく、必要な HTTP メソッド (GET、POST、PUT、DELETE など) をアプリケーションに対して発行するだけで済みます。また、クライアントアプリケーションの開発者は、アプリケーションに必要な HTTP メソッド。

このエンドツーエンドのチュートリアルでは、Web API を使用して次のプロジェクトを作成する方法について説明します。

- [このチュートリアルの最初の部分](#STEP1)では、すべての作成、読み取り、更新、および削除 (CRUD) 操作をサポートし、書籍カタログを管理する ASP.NET Web API アプリケーションを作成します。 このアプリケーションでは、MSDN の[サンプル Xml ファイル (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx)を使用します。
- [このチュートリアルの2番目のパート](#STEP2)では、Web API アプリケーションからデータを取得する対話型 Windows Phone 8 アプリケーションを作成します。

#### <a name="prerequisites"></a>前提条件

- Windows Phone 8 SDK がインストールされている Visual Studio 2013
- Windows 8 以降 (Hyper-v がインストールされている64ビットシステムの場合)
- その他の要件の一覧については、 [WINDOWS PHONE SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471)ダウンロードページの「*システム要件*」セクションを参照してください。

> [!NOTE]
> ローカルシステム上の Web API と Windows Phone 8 プロジェクト間の接続をテストする場合は、「 *[Windows Phone 8 エミュレーターをローカルコンピューターの WEB Api アプリケーションに接続](https://go.microsoft.com/fwlink/?LinkId=324014)* する」の手順に従って、テスト環境を設定する必要があります。

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a>手順 1: Web API 書店プロジェクトを作成する

このエンドツーエンドチュートリアルの最初の手順では、すべての CRUD 操作をサポートする Web API プロジェクトを作成します。このチュートリアルの[手順 2](#STEP2)では、このソリューションに Windows Phone アプリケーションプロジェクトを追加することに注意してください。

1. **Visual Studio 2013**を開きます。
2. **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。
3. **[新しいプロジェクト]** ダイアログボックスが表示されたら、 **[インストール済み]** 、 **[テンプレート]** 、 **[ C#ビジュアル]** 、 **[Web]** の順に展開します。

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                [イメージ] をクリックして展開します。                                                                |

4. **ASP.NET Web アプリケーション**を強調表示し、プロジェクト名として「**書店**」と入力して、[ **OK]** をクリックします。
5. **[新しい ASP.NET プロジェクト]** ダイアログボックスが表示されたら、 **Web API**テンプレートを選択し、 **[OK]** をクリックします。

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                [イメージ] をクリックして展開します。                                                                |

6. Web API プロジェクトが開いたら、プロジェクトからサンプルコントローラーを削除します。

    1. ソリューションエクスプローラーで**Controllers**フォルダーを展開します。
    2. **ValuesController.cs**ファイルを右クリックし、 **[削除]** をクリックします。
    3. 削除の確認を求めるメッセージが表示されたら、[ **OK]** をクリックします。
7. XML データファイルを Web API プロジェクトに追加します。このファイルには、書店カタログの内容が含まれています。

   1. ソリューションエクスプローラーで [ **App\_Data** ] フォルダーを右クリックし、 **[追加]** をクリックして、 **[新しい項目]** をクリックします。
   2. **[新しい項目の追加]** ダイアログボックスが表示されたら、 **XML ファイル**テンプレートを強調表示します。
   3. ファイルに「 **books.xml**」という名前を指定し、 **[追加]** をクリックします。
   4. **Books.xml**ファイルを開いたら、ファイル内のコードを、MSDN のサンプルの**BOOKS.XML**ファイルの xml に置き換えます。 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. XML ファイルを保存して閉じます。

8. Web API プロジェクトに書店モデルを追加します。このモデルには、書店アプリケーションの作成、読み取り、更新、および削除 (CRUD) のロジックが含まれています。

   1. ソリューションエクスプローラーで **[モデル]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[クラス]** をクリックします。
   2. **[新しい項目の追加]** ダイアログボックスが表示されたら、クラスファイルに**BookDetails.cs**という名前を指定し、 **[追加]** をクリックします。
   3. **BookDetails.cs**ファイルを開いたら、ファイル内のコードを次のコードに置き換えます。 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. **BookDetails.cs**ファイルを保存して閉じます。

9. Web API プロジェクトに書店コントローラーを追加します。

   1. ソリューションエクスプローラーで**Controllers**フォルダーを右クリックし、 **[追加]** をクリックして、 **[コントローラー]** をクリックします。
   2. **[スキャフォールディングの追加]** ダイアログボックスが表示されたら、 **[Web API 2 コントローラー-空]** を強調表示し、 **[追加]** をクリックします。
   3. **[コントローラーの追加]** ダイアログボックスが表示されたら、コントローラーに「 **bookscontroller**」という名前を指定し、 **[追加]** をクリックします。
   4. **BooksController.cs**ファイルを開いたら、ファイル内のコードを次のコードに置き換えます。 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. **BooksController.cs**ファイルを保存して閉じます。

10. Web API アプリケーションをビルドして、エラーがないかどうかを確認します。

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a>手順 2: Windows Phone 8 書店カタログプロジェクトの追加

このエンドツーエンドのシナリオの次の手順では、Windows Phone 8 のカタログアプリケーションを作成します。 このアプリケーションでは、既定のユーザーインターフェイスに*Windows Phone データバインドアプリ*テンプレートを使用します。このテンプレートは、このチュートリアルの[手順 1](#STEP1)で作成した Web API アプリケーションをデータソースとして使用します。

1. ソリューションエクスプローラーで、の**書店**ソリューションを右クリックし、 **[追加]** 、 **[新しいプロジェクト]** の順にクリックします。
2. **新しいプロジェクト** ダイアログボックスが表示されたら、**インストール済み**、 **C#ビジュアル** の順に展開し、 **Windows Phone** をクリックします。
3. **データバインドアプリ Windows Phone**強調表示し、名前として「 **bookcatalog** 」と入力して、 **OK**をクリックします。
4. Json.NET NuGet パッケージを**Bookcatalog**プロジェクトに追加します。

    1. ソリューションエクスプローラーで**Bookcatalog**プロジェクトの **[参照]** を右クリックし、 **[NuGet パッケージの管理]** をクリックします。
    2. **[NuGet パッケージの管理]** ダイアログボックスが表示されたら、 **[オンライン]** セクションを展開し、 **[nuget.org]** を強調表示します。
    3. 検索フィールドに「 **Json.NET** 」と入力し、[検索] アイコンをクリックします。
    4. 検索結果で**Json.NET**を強調表示し、 **[インストール]** をクリックします。
    5. インストールが完了したら、 **[閉じる]** をクリックします。
5. Bookdetails プロジェクトに**Bookdetails**モデルを追加します。これには、書店クラスの汎用モデルが含まれます。

   1. ソリューションエクスプローラーで**Bookcatalog**プロジェクトを右クリックし、 **[追加]** をクリックして、 **[新しいフォルダー]** をクリックします。
   2. 新しいフォルダーに**モデル**の名前を指定します。
   3. ソリューションエクスプローラーで **[モデル]** フォルダーを右クリックし、 **[追加]** をクリックして、 **[クラス]** をクリックします。
   4. **[新しい項目の追加]** ダイアログボックスが表示されたら、クラスファイルに**BookDetails.cs**という名前を指定し、 **[追加]** をクリックします。
   5. **BookDetails.cs**ファイルを開いたら、ファイル内のコードを次のコードに置き換えます。 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. **BookDetails.cs**ファイルを保存して閉じます。

6. **MainViewModel.cs**クラスを更新して、書店の Web API アプリケーションと通信する機能を含めます。

   1. ソリューションエクスプローラーで**viewmodel**フォルダーを展開し、 **MainViewModel.cs**ファイルをダブルクリックします。
   2. **MainViewModel.cs**ファイルを開いたら、ファイル内のコードを次のコードに置き換えます。`apiUrl` 定数の値は、実際の Web API の URL で更新する必要があることに注意してください。 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. **MainViewModel.cs**ファイルを保存して閉じます。

7. **Mainpage.xaml**ファイルを更新して、アプリケーション名をカスタマイズします。

   1. ソリューションエクスプローラーで**mainpage.xaml**ファイルをダブルクリックします。
   2. **Mainpage.xaml**ファイルを開いたら、次のコード行を見つけます。 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. これらの行を次のコードに置き換えます。 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. **Mainpage.xaml**ファイルを保存して閉じます。

8. **DetailsPage**ファイルを更新して、表示される項目をカスタマイズします。

   1. ソリューションエクスプローラーで**DetailsPage**ファイルをダブルクリックします。
   2. **DetailsPage**ファイルを開いたら、次のコード行を見つけます。 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. これらの行を次のコードに置き換えます。 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. **DetailsPage**ファイルを保存して閉じます。

9. Windows Phone アプリケーションをビルドして、エラーがないかどうかを確認します。

### <a name="step-3-testing-the-end-to-end-solution"></a>手順 3: エンドツーエンドのソリューションをテストする

このチュートリアルの*前提条件*のセクションで説明したように、ローカルシステム上の web api と Windows Phone 8 プロジェクト間の接続をテストするときは、「 *[Windows Phone 8 エミュレーターをローカルコンピューターの web Api アプリケーションに接続](https://go.microsoft.com/fwlink/?LinkId=324014)* する」の手順に従って、テスト環境を設定する必要があります。

テスト環境を構成したら、Windows Phone アプリケーションをスタートアッププロジェクトとして設定する必要があります。 これを行うには、ソリューションエクスプローラーで**Bookcatalog**アプリケーションを強調表示し、 **[スタートアッププロジェクトに設定]** をクリックします。

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| [イメージ] をクリックして展開します。 |

F5 キーを押すと、Visual Studio は Windows Phone エミュレーターの両方を起動します。これにより、Web API からアプリケーションデータが取得されている間、&quot; メッセージ &quot;を表示します。

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| [イメージ] をクリックして展開します。 |

すべての処理が成功すると、カタログが表示されます。

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| [イメージ] をクリックして展開します。 |

任意の書籍のタイトルをタップすると、アプリケーションにブックの説明が表示されます。

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| [イメージ] をクリックして展開します。 |

アプリケーションが Web API と通信できない場合は、次のエラーメッセージが表示されます。

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| [イメージ] をクリックして展開します。 |

エラーメッセージをタップすると、エラーに関する追加情報が表示されます。

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 [イメージ] をクリックして展開します。                                                                 |

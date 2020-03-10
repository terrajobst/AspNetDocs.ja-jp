---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: 'イテレーション #1 –アプリケーションを作成する (VB) |Microsoft Docs'
author: microsoft
description: 最初のイテレーションでは、最も簡単な方法で Contact Manager を作成します。 基本的なデータベース操作 (Create、Read、Update、および D...) のサポートを追加します。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: c6bf4712fb734cf14420fd62c9eaf190a2c28168
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487570"
---
# <a name="iteration-1--create-the-application-vb"></a>イテレーション #1 –アプリケーションを作成する (VB)

[Microsoft](https://github.com/microsoft)

[コードのダウンロード](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> 最初のイテレーションでは、最も簡単な方法で Contact Manager を作成します。 基本的なデータベース操作 (作成、読み取り、更新、削除) のサポートを追加します。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Contact Management ASP.NET MVC アプリケーションの構築 (VB)

この一連のチュートリアルでは、最初から最後まで、連絡先管理アプリケーション全体を作成します。 連絡先マネージャーアプリケーションを使用すると、連絡先情報 (名前、電話番号、電子メールアドレスなど) をユーザーの一覧に格納できます。

複数のイテレーションに対してアプリケーションをビルドします。 各イテレーションで、アプリケーションを段階的に改善します。 この複数のイテレーションアプローチの目的は、各変更の理由を理解できるようにすることです。

- イテレーション #1-アプリケーションを作成します。 最初のイテレーションでは、最も簡単な方法で Contact Manager を作成します。 基本的なデータベース操作 (作成、読み取り、更新、削除) のサポートを追加します。

- イテレーション #2-アプリケーションの外観を良くします。 このイテレーションでは、既定の ASP.NET MVC ビューマスターページとカスケードスタイルシートを変更することによって、アプリケーションの外観を改善します。

- イテレーション #3-フォーム検証を追加します。 3番目のイテレーションでは、基本的なフォーム検証を追加します。 必要なフォームフィールドを完了しないで、フォームを送信できないようにします。 また、電子メールアドレスと電話番号も検証します。

- イテレーション #4-アプリケーションの疎結合を実現します。 この4回目のイテレーションでは、複数のソフトウェア設計パターンを利用して、連絡先マネージャーアプリケーションを簡単に管理および変更できるようにします。 たとえば、リポジトリパターンと依存関係の注入パターンを使用するようにアプリケーションをリファクターします。

- イテレーション #5-単体テストを作成します。 5番目のイテレーションでは、単体テストを追加することによって、アプリケーションの保守と変更を容易にします。 データモデルクラスをモック化し、コントローラーと検証ロジックの単体テストをビルドします。

- イテレーション #6-テスト駆動型開発を使用します。 この6番目のイテレーションでは、最初に単体テストを記述し、単体テストに対してコードを記述することによって、アプリケーションに新しい機能を追加します。 このイテレーションでは、連絡先グループを追加します。

- イテレーション #7-Ajax 機能を追加します。 7番目のイテレーションでは、Ajax のサポートを追加することによって、アプリケーションの応答性とパフォーマンスを向上させます。

## <a name="this-iteration"></a>このイテレーション

この最初のイテレーションでは、基本的なアプリケーションをビルドします。 目標は、最も高速で最も簡単な方法で連絡先マネージャーを構築することです。 後のイテレーションでは、アプリケーションの設計が改善されます。

Contact Manager アプリケーションは、データベース主導型の基本的なアプリケーションです。 アプリケーションを使用して、新しい連絡先の作成、既存の連絡先の編集、および連絡先の削除を行うことができます。

このイテレーションでは、次の手順を実行します。

1. ASP.NET MVC アプリケーション
2. 連絡先を格納するデータベースを作成する
3. Microsoft Entity Framework を使用してデータベースのモデルクラスを生成する
4. コントローラーアクションとビューを作成して、データベース内のすべての連絡先を一覧表示できるようにします。
5. コントローラーアクションとビューを作成して、データベースに新しい連絡先を作成できるようにします。
6. コントローラーアクションとビューを作成して、データベース内の既存の連絡先を編集できるようにします。
7. コントローラーアクションとビューを作成して、データベース内の既存の連絡先を削除できるようにします。

## <a name="software-prerequisites"></a>ソフトウェアの必要なコンポーネント

ASP.NET MVC アプリケーションでは、Visual Studio 2008 または Visual Web Developer 2008 がコンピューターにインストールされている必要があります (visual Web Developer は visual studio の無料版で、visual Studio のすべての高度な機能が含まれているわけではありません)。 Visual Studio 2008 または Visual Web Developer の試用版は、次のアドレスからダウンロードできます。

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> Visual Web Developer で ASP.NET MVC アプリケーションを使用するには、Visual Web Developer Service Pack 1 がインストールされている必要があります。 Service Pack 1 を適用していない場合、Web アプリケーションプロジェクトを作成することはできません。

ASP.NET MVC フレームワーク。 ASP.NET MVC フレームワークは、次のアドレスからダウンロードできます。

[https://www.asp.net/mvc](../../../index.md)

このチュートリアルでは、Microsoft Entity Framework を使用してデータベースにアクセスします。 Entity Framework は .NET Framework 3.5 Service Pack 1 に含まれています。 この Service Pack は次の場所からダウンロードできます。

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;d isplaylang = en](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

これらの各ダウンロードを1つずつ実行する代わりに、Web Platform Installer (Web PI) を利用することもできます。 Web PI は、次のアドレスからダウンロードできます。

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC プロジェクト

ASP.NET MVC Web アプリケーションプロジェクト。 Visual Studio を起動し、メニューオプション**ファイル [新しいプロジェクト**] を選択します。 **[新しいプロジェクト]** ダイアログボックスが表示されます (図1を参照)。 **[Web]** プロジェクトの種類 と **[ASP.NET MVC web アプリケーション]** テンプレートを選択します。 新しいプロジェクトに「 *Contactmanager* 」という名前を指定し、[OK] ボタンをクリックします。

**[新しいプロジェクト]** ダイアログボックスの右上にあるドロップダウンリストから .NET Framework 3.5 が選択されていることを確認します。 それ以外の場合、ASP.NET MVC Web アプリケーションテンプレートは表示されません。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)

**図 01**: [新しいプロジェクト] ダイアログボックス ([クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image2.png)されます)

ASP.NET MVC アプリケーションでは、 **[単体テストプロジェクトの作成]** ダイアログボックスが表示されます。 このダイアログボックスを使用すると、ASP.NET MVC アプリケーションを作成するときに、単体テストプロジェクトを作成してソリューションに追加することを指定できます。 このイテレーションでは単体テストを作成しませんが、後のイテレーションで単体テストを追加する予定のため、 **[はい、単体テストプロジェクトを作成**する] オプションを選択する必要があります。 新しい ASP.NET MVC プロジェクトを初めて作成するときにテストプロジェクトを追加する方が、ASP.NET MVC プロジェクトの作成後にテストプロジェクトを追加するよりもはるかに簡単です。

> [!NOTE] 
> 
> Visual Web Developer はテストプロジェクトをサポートしていないため、Visual Web Developer を使用する場合、[単体テストプロジェクトの作成] ダイアログボックスは表示されません。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)

**図 02**: [単体テストプロジェクトの作成] ダイアログ ([クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image4.png)されます)

ASP.NET MVC アプリケーションが Visual Studio のソリューションエクスプローラーウィンドウに表示されます (図3を参照)。 [ソリューションエクスプローラー] ウィンドウが表示されない場合は、このウィンドウを開くには、メニューオプションの [**表示]、[ソリューションエクスプローラー**] の順に選択します。 ソリューションには、ASP.NET MVC プロジェクトとテストプロジェクトという2つのプロジェクトが含まれていることに注意してください。 ASP.NET MVC プロジェクトには ContactManager という名前が付けられ、テストプロジェクトの名前は ContactManager. テストになります。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)

**図 03**: ソリューションエクスプローラーウィンドウ ([クリックしてフルサイズの画像を表示する](iteration-1-create-the-application-vb/_static/image6.png))

## <a name="deleting-the-project-sample-files"></a>プロジェクトサンプルファイルを削除しています

ASP.NET MVC プロジェクトテンプレートには、コントローラーとビューのサンプルファイルが含まれています。 新しい ASP.NET MVC アプリケーションを作成する前に、これらのファイルを削除する必要があります。 ファイルまたはフォルダーを右クリックし、**削除** メニューオプションを選択すると、ソリューションエクスプローラー ウィンドウでファイルやフォルダーを削除できます。

ASP.NET MVC プロジェクトから次のファイルを削除する必要があります。

- \Controllers\HomeController.vb

- \Views\Home\About.aspx

- \Views\Home\Index.aspx

また、テストプロジェクトから次のファイルを削除する必要があります。

\Controllers\HomeControllerTest.vb

## <a name="creating-the-database"></a>データベースの作成

Contact Manager アプリケーションは、データベース主導の web アプリケーションです。 連絡先情報を格納するためにデータベースを使用します。

Microsoft SQL Server、Oracle、MySQL、および IBM DB2 データベースを含む最新のデータベースを備えた ASP.NET MVC フレームワーク。 このチュートリアルでは、Microsoft SQL Server データベースを使用します。 Visual Studio をインストールすると、無料版の Microsoft SQL Server データベースである Microsoft SQL Server Express をインストールするオプションが表示されます。

[ソリューションエクスプローラー] ウィンドウで [App\_Data] フォルダーを右クリックし、[**追加]、[新しい項目**] の順に選択して、新しいデータベースを作成します。 **[新しい項目の追加]** ダイアログで、 **[データ]** カテゴリと **[SQL Server データベース]** テンプレートを選択します (図4を参照)。 新しいデータベースに「ContactManagerDB .mdf」という名前を指定し、[OK] ボタンをクリックします。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)

**図 04**: 新しい Microsoft SQL Server Express データベースを作成する ([クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image8.png)される)

新しいデータベースを作成すると、[ソリューションエクスプローラー] ウィンドウの [アプリ\_データ] フォルダーにデータベースが表示されます。 ContactManager .mdf ファイルをダブルクリックして [サーバーエクスプローラー] ウィンドウを開き、データベースに接続します。

> [!NOTE] 
> 
> Microsoft Visual Web Developer の場合は、[サーバーエクスプローラー] ウィンドウを [データベースエクスプローラー] ウィンドウと呼びます。

[サーバーエクスプローラー] ウィンドウを使用すると、データベーステーブル、ビュー、トリガー、ストアドプロシージャなどの新しいデータベースオブジェクトを作成できます。 テーブル フォルダーを右クリックし、**新しいテーブルの追加** メニューオプションを選択します。 データベーステーブルデザイナーが表示されます (図5を参照)。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)

**図 05**: データベーステーブルデザイナー ([クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image10.png)されます)

次の列を含むテーブルを作成する必要があります。

<a id="0.2_table01"></a>

| **列名** | **[データ型]** | **[NULL を許容]** |
| --- | --- | --- |
| Id | INT | false |
| FirstName | nvarchar(50) | false |
| LastName | nvarchar(50) | false |
| Phone | nvarchar(50) | false |
| Email | nvarchar(255) | false |

最初の列である Id 列は特殊です。 Id 列を Id 列および主キー列としてマークする必要があります。 列が Id 列であることを示すには、列のプロパティを展開し (図6の下部を参照)、[Identity Specification] プロパティまでスクロールします。 **(Is id)** プロパティを **[はい]** に設定します。

列を選択し、キーのアイコンの付いたボタンをクリックすることで、列を主キー列としてマークします。 列を主キー列としてマークすると、その列の横にキーのアイコンが表示されます (図6を参照)。

テーブルの作成が完了したら、[保存] ボタン (フロッピーのアイコンが付いたボタン) をクリックして、新しいテーブルを保存します。 新しいテーブル*に名前を付けます*。

Contacts データベーステーブルの作成が完了したら、いくつかのレコードをテーブルに追加する必要があります。 サーバーエクスプローラーウィンドウで Contacts テーブルを右クリックし、 **[テーブルデータの表示]** メニューオプションを選択します。 表示されるグリッドに1つ以上の連絡先を入力します。

## <a name="creating-the-data-model"></a>データモデルの作成

ASP.NET MVC アプリケーションは、モデル、ビュー、およびコントローラーで構成されています。 最初に、前のセクションで作成した Contacts テーブルを表すモデルクラスを作成します。

このチュートリアルでは、Microsoft Entity Framework を使用して、データベースからモデルクラスを自動的に生成します。

> [!NOTE] 
> 
> ASP.NET MVC フレームワークは、どのような方法でも Microsoft Entity Framework に関連付けられていません。 ASP.NET MVC は、NHibernate、LINQ to SQL、ADO.NET などの別のデータベースアクセステクノロジと共に使用できます。

データモデルクラスを作成するには、次の手順に従います。

1. ソリューションエクスプローラーウィンドウで [モデル] フォルダーを右クリックし、[**追加]、[新しい項目**] の順に選択します。 **[新しい項目の追加]** ダイアログボックスが表示されます (図6を参照)。
2. **[データ]** カテゴリと **[ADO.NET Entity Data Model]** テンプレートを選択します。 データモデルに「 *Contactmanagermodel. .edmx* 」という名前を指定し、 **[追加]** ボタンをクリックします。 Entity Data Model ウィザードが表示されます (図7を参照)。
3. **[モデルの内容の選択]** ステップで、 **[データベースから生成]** を選択します (図7を参照)。
4. **[データ接続の選択]** ステップで、ContactManagerDB .mdf データベースを選択し、エンティティ接続設定の名前として*Contactmanagerdbentities*を入力します (図8を参照)。
5. **データベースオブジェクトの選択** ステップで、テーブル チェックボックスをオンにします (図9を参照)。 データモデルには、データベースに格納されているすべてのテーブルが含まれます (Contacts テーブルは1つだけです)。 名前空間*モデル*を入力します。 ウィザードを完了するには、[完了] をクリックします。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)

**図 06**: [新しい項目の追加] ダイアログ ([クリックしてフルサイズのイメージを表示](iteration-1-create-the-application-vb/_static/image12.png))

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)

**図 07**: モデルのコンテンツを選択[する (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image14.png)される)

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)

**図 08**: データ接続を選択[する (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image16.png)される)

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)

**図 09**: データベースオブジェクトを選択[する (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image18.png)される)

Entity Data Model ウィザードを完了すると、Entity Data Model デザイナーが表示されます。 デザイナーには、モデル化されている各テーブルに対応するクラスが表示されます。 Contact という名前のクラスが1つ表示できます。

Entity Data Model ウィザードでは、データベーステーブル名に基づいてクラス名が生成されます。 ほとんどの場合、ウィザードによって生成されるクラスの名前を変更する必要があります。 デザイナーで Contacts クラスを右クリックし、メニューオプション [名前の**変更**] を選択します。 クラスの名前を [Contacts (複数形)] から [Contact] (単数形) に変更します。 クラス名を変更すると、図10のようにクラスが表示されます。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)

**図 10**: Contact クラス ([クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image20.png)されます)

この時点で、データベースモデルが作成されました。 Contact クラスを使用して、データベース内の特定の連絡先レコードを表すことができます。

## <a name="creating-the-home-controller"></a>Home コントローラーの作成

次の手順では、Home コントローラーを作成します。 Home コントローラーは、ASP.NET MVC アプリケーションで呼び出される既定のコントローラーです。

Home コントローラークラスを作成するには、[ソリューションエクスプローラー] ウィンドウで Controllers フォルダーを右クリックし、[**追加]、[コントローラー** ] の順に選択します (図11を参照)。 **作成、更新、詳細の各シナリオの [アクションメソッドの追加] と**いうラベルのチェックボックスが表示されます。 **[追加]** ボタンをクリックする前に、このチェックボックスがオンになっていることを確認します。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)

**図 11**: ホームコントローラーを追加[する (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image22.png)されます)

Home コントローラーを作成すると、リスト1のクラスが表示されます。

**リスト 1-Controllers\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a>連絡先を一覧表示する

Contacts データベーステーブルのレコードを表示するには、Index () アクションとインデックスビューを作成する必要があります。

Home コントローラーには既に Index () アクションが含まれています。 リスト2のようにこのメソッドを変更する必要があります。

**リスト 2-Controllers\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

リスト2の Home controller クラスに \_エンティティという名前のプライベートフィールドが含まれていることに注意してください。 [\_エンティティ] フィールドは、データモデルのエンティティを表します。 データベースとの通信には、\_エンティティフィールドを使用します。

Index () メソッドは、Contacts データベーステーブルのすべての連絡先を表すビューを返します。 エンティティ \_式。ContactSet。 ToList () は、連絡先のリストをジェネリックリストとして返します。

インデックスコントローラーを作成したので、次にインデックスビューを作成する必要があります。 インデックスビューを作成する前に、ビルド メニューの **ソリューションのビルド** を選択して、アプリケーションをコンパイルします。 **[ビューの追加]** ダイアログでモデルクラスの一覧が表示されるようにするには、ビューを追加する前にプロジェクトをコンパイルする必要があります。

インデックスビューを作成するには、Index () メソッドを右クリックし、 **[ビューの追加]** メニューオプションを選択します (図12を参照)。 このメニューオプションを選択すると、 **[ビューの追加]** ダイアログボックスが開きます (図13を参照)。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)

**図 12**: インデックスビュー[を追加する (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image24.png)されます)

**[ビューの追加]** ダイアログボックスで、 **[厳密に型指定されたビューを作成する]** チェックボックスをオンにします。 ビューデータクラス ContactManager を選択します。連絡先とビューコンテンツの一覧を選択します。 これらのオプションを選択すると、連絡先レコードの一覧を表示するビューが生成されます。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)

**図 13**: [ビューの追加] ダイアログボックス ([クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image26.png)されます)

**[追加]** ボタンをクリックすると、リスト3のインデックスビューが生成されます。 ファイルの先頭に表示される &lt;% @ Page%&gt; ディレクティブに注意してください。 インデックスビューは、ViewPage&lt;IEnumerable&lt;ContactManager. モデル&gt;&gt; クラスから継承されます。 言い換えると、ビューのモデルクラスは、連絡先エンティティの一覧を表します。

インデックスビューの本文には、モデルクラスによって表される各連絡先を反復処理する foreach ループが含まれています。 Contact クラスの各プロパティの値は、HTML テーブル内に表示されます。

**リスト 3-Views\Home\Index.aspx (未変更)**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

インデックスビューに1つの変更を加える必要があります。 詳細ビューを作成していないので、[詳細] リンクを削除できます。 インデックスビューから次のコードを見つけて削除します。

{. id = item。Id})%&gt;

インデックスビューを変更した後、Contact Manager アプリケーションを実行できます。 メニューオプション [デバッグ]、[デバッグ開始] のいずれかを選択するか、F5 キーを押します。 アプリケーションを初めて実行するときに、図14のダイアログが表示されます。 **Web.config ファイルを変更してデバッグを有効にする** オプションを選択し、OK ボタンをクリックします。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)

**図 14**: デバッグを有効[にする (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image28.png)される)

既定では、インデックスビューが返されます。 このビューには、Contacts データベーステーブルのすべてのデータが一覧表示されます (図15を参照)。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)

**図 15**: インデックスビュー ([クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image30.png)されます)

ビューの下部に [新規作成] というラベルのリンクが表示されていることに注意してください。 次のセクションでは、新しい連絡先を作成する方法について説明します。

## <a name="creating-new-contacts"></a>新しい連絡先の作成

ユーザーが新しい連絡先を作成できるようにするには、Home コントローラーに2つの Create () アクションを追加する必要があります。 新しい連絡先を作成するための HTML フォームを返す Create () アクションを1つ作成する必要があります。 新しい連絡先の実際のデータベース挿入を実行する2つ目の Create () アクションを作成する必要があります。

Home コントローラーに追加する必要がある新しい Create () メソッドは、リスト4に含まれています。

**リスト 4-Controllers\HomeController.vb (Create メソッドを含む)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

最初の Create () メソッドは、http GET を使用して呼び出すことができますが、2番目の Create () メソッドは HTTP POST によってのみ呼び出すことができます。 つまり、2番目の Create () メソッドは、HTML フォームを投稿するときにのみ呼び出すことができます。 最初の Create () メソッドは、新しい連絡先を作成するための HTML フォームを含むビューを返します。 2番目の Create () メソッドは、データベースに新しい連絡先を追加することでさらに興味深いものです。

Contact クラスのインスタンスを受け入れるように、2番目の Create () メソッドが変更されていることに注意してください。 HTML フォームからポストされたフォーム値は、ASP.NET MVC フレームワークによって自動的にこの Contact クラスにバインドされます。 HTML 作成フォームの各フォームフィールドは、Contact パラメーターのプロパティに割り当てられます。

Contact パラメーターが [Bind] 属性で修飾されていることに注意してください。 [Bind] 属性は、"Contact Id" プロパティをバインドから除外するために使用されます。 Id プロパティは id プロパティを表すので、Id プロパティを設定する必要はありません。

Create () メソッドの本体では、データベースに新しい連絡先を挿入するために Entity Framework が使用されます。 新しい連絡先が既存の連絡先のセットに追加され、SaveChanges () メソッドが呼び出され、基になるデータベースにこれらの変更が反映されます。

新しい連絡先を作成するための HTML フォームを生成するには、2つの Create () メソッドのいずれかを右クリックし、 **[ビューの追加]** メニューオプションを選択します (図16を参照)。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)

**図 16**: 作成ビュー[を追加する (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image32.png)されます)

**[ビューの追加]** ダイアログで、 **contactmanager. contact**クラスと、ビューコンテンツの **[作成]** オプションを選択します (図17を参照)。 **[追加]** ボタンをクリックすると、作成ビューが自動的に生成されます。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)

**図 17**: ページの爆発を[確認する (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image34.png)される)

Create ビューには、Contact クラスの各プロパティのフォームフィールドが含まれています。 リスト5には、Create ビューのコードが含まれています。

**リスト 5-Views\Home\Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

Create () メソッドを変更し、Create ビューを追加した後、Contact manager アプリケーションを実行して新しい連絡先を作成できます。 インデックスビューに表示される **新規作成** リンクをクリックして、作成 ビューに移動します。 図18にビューが表示されます。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)

**図 18**: [作成] ビュー ([クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image36.png)されます)

## <a name="editing-contacts"></a>連絡先の編集

連絡先レコードを編集する機能を追加することは、新しい連絡先レコードを作成する機能を追加することとよく似ています。 まず、Home controller クラスに2つの新しい Edit メソッドを追加する必要があります。 これらの新しい Edit () メソッドは、リスト6に含まれています。

**リスト 6-Controllers\HomeController.vb (Edit メソッドを含む)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

最初の Edit () メソッドは、HTTP の GET 操作によって呼び出されます。 このメソッドには、編集する連絡先レコードの Id を表す Id パラメーターが渡されます。 Entity Framework は、Id と一致する連絡先を取得するために使用されます。レコードを編集するための HTML フォームを含むビューが返されます。

2番目の Edit () メソッドは、実際の更新をデータベースに対して実行します。 このメソッドは、Contact クラスのインスタンスをパラメーターとして受け取ります。 ASP.NET MVC フレームワークは、フォームフィールドを編集フォームからこのクラスに自動的にバインドします。 連絡先を編集するときは、[Bind] 属性を含めないことに注意してください (Id プロパティの値が必要です)。

Entity Framework は、変更された連絡先をデータベースに保存するために使用します。 最初に、元の連絡先をデータベースから取得する必要があります。 次に、Entity Framework ApplyPropertyChanges () メソッドを呼び出して、連絡先への変更を記録します。 最後に、Entity Framework SaveChanges () メソッドを呼び出して、基になるデータベースへの変更を保持します。

Edit () メソッドを右クリックして [ビューの追加] メニューオプションを選択すると、編集フォームを含むビューを生成できます。 [ビューの追加] ダイアログで、 **Contactmanager. モデルの連絡先**クラスと**編集**ビューのコンテンツを選択します (図19を参照)。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)

**図 19**: 編集ビュー[を追加する (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image38.png)されます)

[追加] ボタンをクリックすると、新しい編集ビューが自動的に生成されます。 生成される HTML フォームには、Contact クラスの各プロパティに対応するフィールドが含まれています (リスト7を参照)。

**リスト 7-Views\Home\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>連絡先の削除

連絡先を削除する場合は、Home コントローラークラスに2つの Delete () アクションを追加する必要があります。 最初の Delete () アクションでは、削除の確認フォームが表示されます。 2番目の Delete () アクションは、実際の削除を実行します。

> [!NOTE] 
> 
> その後、イテレーション #7 で Contact Manager を変更して、Ajax の1ステップの削除をサポートするようにします。

2つの新しい Delete () メソッドは、リスト8に含まれています。

**Controllers\HomeController.vb の一覧表示 (Delete メソッド)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

最初の Delete () メソッドでは、データベースから連絡先レコードを削除するための確認フォームが返されます (「Figure20」を参照してください)。 2番目の Delete () メソッドは、データベースに対して実際の削除操作を実行します。 データベースから元の連絡先を取得した後、Entity Framework の DeleteObject () メソッドと SaveChanges () メソッドを呼び出して、データベースの削除を実行します。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)

**図 20**: 削除の確認ビュー ([クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image40.png)されます)

連絡先レコードを削除するためのリンクが含まれるように、インデックスビューを変更する必要があります (図21を参照)。 編集リンクを含む同じテーブルセルに次のコードを追加する必要があります。

{. id = item。Id})%&gt;

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)

**図 21**: 編集リンクがあるインデックスビュー ([クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image42.png)される)

次に、削除の確認ビューを作成する必要があります。 Home コントローラークラスで Delete () メソッドを右クリックし、メニューオプション [ビューの追加] を選択します。 [ビューの追加] ダイアログボックスが表示されます (図22を参照)。

リスト、作成、および編集ビューの場合とは異なり、[ビューの追加] ダイアログには、削除ビューを作成するオプションがありません。 代わりに、 **Contactmanager. モデルの contact**データクラスと**空**のビューコンテンツを選択します。 空のビューコンテンツオプションを選択するには、自分でビューを作成する必要があります。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)

**図 22**: 削除確認ビュー[を追加する (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image44.png)されます)

削除ビューの内容は、リスト9に含まれています。 このビューには、特定の連絡先を削除する必要があるかどうかを確認するフォームが含まれています (図21を参照)。

**リスト 9-Views\Home\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>既定のコントローラーの名前を変更する

連絡先を操作するためのコントローラークラスの名前は、HomeController クラスという名前になることがあります。 コントローラーに ContactController という名前を付けないでください。

この問題は、簡単に修正できます。 まず、Home コントローラーの名前をリファクターする必要があります。 Visual Studio Code エディターで HomeController クラスを開き、クラスの名前を右クリックして、メニューオプション **[名前の変更]** を選択します。 このメニューオプションを選択すると、[名前の変更] ダイアログボックスが開きます。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)

**図 23**: コントローラー名をリファクタリング[する (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image46.png)される)

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)

**図 24**: [名前の変更] ダイアログを使用[する (クリックすると、フルサイズの画像が表示](iteration-1-create-the-application-vb/_static/image48.png)されます)

コントローラークラスの名前を変更すると、Visual Studio によって Views フォルダー内のフォルダーの名前も更新されます。 Visual Studio は、\Views\Home フォルダーの名前を \Views\Contact フォルダーに変更します。

この変更を行った後、アプリケーションにはホームコントローラーがなくなります。 アプリケーションを実行すると、図25のエラーページが表示されます。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)

**図 25**: 既定のコントローラーがない ([クリックしてフルサイズのイメージを表示する](iteration-1-create-the-application-vb/_static/image50.png))

Global.asax ファイルの既定のルートを更新して、Home コントローラーではなく Contact controller を使用する必要があります。 Global.asax ファイルを開き、既定のルートで使用される既定のコントローラーを変更します (一覧10を参照)。

**リスト 10-global.asax**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

これらの変更を行った後、連絡先マネージャーが正常に実行されます。 これで、Contact controller クラスが既定のコントローラーとして使用されます。

## <a name="summary"></a>まとめ

この最初のイテレーションでは、最も迅速な方法で基本的な Contact Manager アプリケーションを作成しました。 Visual Studio を利用して、コントローラーとビューの初期コードを自動的に生成しました。 また、Entity Framework を利用して、データベースモデルクラスを自動的に生成しました。

現在、連絡先マネージャーアプリケーションを使用して、連絡先レコードの一覧表示、作成、編集、および削除を行うことができます。 言い換えると、データベース駆動型 web アプリケーションで必要な基本的なデータベース操作をすべて実行できます。

残念ながら、アプリケーションにはいくつかの問題があります。 まず、連絡先マネージャーアプリケーションは最も魅力的なアプリケーションではありません。 いくつかのデザイン作業が必要です。 次のイテレーションでは、アプリケーションの外観を向上させるために、既定のビューマスターページとカスケードスタイルシートをどのように変更できるかを見ていきます。

2つ目は、フォーム検証を実装していないことです。 たとえば、フォームのフィールドに値を入力することなく、Create contact フォームを送信できないようにすることはできません。 また、無効な電話番号と電子メールアドレスを入力することもできます。 イテレーション #3 でのフォーム検証の問題に取り組むことを開始します。

最後に、最も重要なのは、Contact Manager アプリケーションの現在のイテレーションを簡単に変更または管理できないことです。 たとえば、データベースアクセスロジックはコントローラーアクションに組み込まれています。 つまり、コントローラーを変更することなくデータアクセスコードを変更することはできません。 後のイテレーションでは、連絡先マネージャーがより柔軟に変更できるように実装できるソフトウェア設計パターンについて説明します。

> [!div class="step-by-step"]
> [前へ](iteration-7-add-ajax-functionality-cs.md)
> [次へ](iteration-2-make-the-application-look-nice-vb.md)

---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
title: メンバーシップと管理 |Microsoft Docs
author: Erikre
description: このチュートリアルシリーズでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォームアプリケーションを構築するための基本について説明します。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 732a2316-e49f-4f72-becd-0cd72f14457e
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
msc.type: authoredcontent
ms.openlocfilehash: ab00bc90bfc767d06e747be6dfb973245b5aae88
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615470"
---
# <a name="membership-and-administration"></a>メンバーシップと管理

[Erik Reitan](https://github.com/Erikre)

[Wingtip Toys サンプルプロジェクト (C#) をダウンロード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)するか[、電子書籍 (PDF) をダウンロード](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)します。

> このチュートリアルシリーズでは、ASP.NET 4.5 を使用して ASP.NET Web フォームアプリケーションを構築するための基礎と、Web 用の Microsoft Visual Studio Express 2013 について説明します。 このチュートリアルシリーズ[でC#は、ソースコードが含ま](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)れる Visual Studio 2013 プロジェクトを利用できます。

このチュートリアルでは、Wingtip Toys サンプルアプリケーションを更新してカスタムロールを追加し、ASP.NET Identity を使用する方法について説明します。 また、カスタムロールを持つユーザーが web サイトから製品を追加および削除できる管理ページを実装する方法についても説明します。

[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)は、ASP.NET web アプリケーションのビルドに使用されるメンバーシップシステムであり、ASP.NET 4.5 で使用できます。 ASP.NET Identity は、Visual Studio 2013 Web フォームプロジェクトテンプレートと、 [ASP.NET MVC](../../../../mvc/index.md)、 [ASP.NET Web API](../../../../web-api/index.md)、および[ASP.NET のシングルページアプリケーション](../../../../single-page-application/index.md)のテンプレートで使用されます。 空の Web アプリケーションから開始する場合は、NuGet を使用して ASP.NET Identity システムを明示的にインストールすることもできます。 ただし、このチュートリアルシリーズでは、ASP.NET Identity システムを含む**Web フォーム**projecttemplate を使用します。 ASP.NET Identity を使用すると、ユーザー固有のプロファイルデータをアプリケーションデータに簡単に統合できます。 また、ASP.NET Identity を使用すると、アプリケーションのユーザープロファイルの永続性モデルを選択できます。 データは、SQL Server データベースまたは別のデータストア (Windows Azure Storage テーブルなどの*NoSQL*データストア) に格納できます。

このチュートリアルでは、Wingtip Toys チュートリアルシリーズで、前述の「PayPal を使用した精算と支払い」というタイトルのチュートリアルを基にしています。

## <a name="what-youll-learn"></a>学習内容:

- コードを使用して、カスタムロールとユーザーをアプリケーションに追加する方法。
- 管理フォルダーとページへのアクセスを制限する方法。
- カスタムロールに属しているユーザーのナビゲーションを提供する方法。
- モデルバインドを使用して、 [DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx)コントロールに製品カテゴリを設定する方法について説明します。
- [FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx)コントロールを使用して web アプリケーションにファイルをアップロードする方法。
- 検証コントロールを使用して入力検証を実装する方法。
- アプリケーションの製品を追加および削除する方法。

## <a name="these-features-are-included-in-the-tutorial"></a>このチュートリアルでは、次の機能について説明します。

- ASP.NET Identity
- 構成と承認
- モデル バインド
- 控えめに検証

ASP.NET Web フォームは、メンバーシップ機能を提供します。 既定のテンプレートを使用すると、アプリケーションの実行時にすぐに使用できる組み込みのメンバーシップ機能を使用できます。 このチュートリアルでは、ASP.NET Identity を使用してカスタムロールを追加し、そのロールにユーザーを割り当てる方法について説明します。 管理フォルダーへのアクセスを制限する方法についても説明します。 管理フォルダーにページを追加して、カスタムロールを持つユーザーが製品を追加および削除したり、追加後に製品をプレビューしたりできるようにします。

## <a name="adding-a-custom-role"></a>カスタムロールの追加

ASP.NET Identity を使用すると、カスタムロールを追加し、コードを使用してそのロールにユーザーを割り当てることができます。

1. **ソリューションエクスプローラー**で、 *Logic*フォルダーを右クリックし、新しいクラスを作成します。
2. 新しいクラスに*RoleActions.cs*という名前を指定します。
3. 次のようにコードを変更します。  

    [!code-csharp[Main](membership-and-administration/samples/sample1.cs?highlight=8)]
4. **ソリューションエクスプローラー**で、 *Global.asax.cs*ファイルを開きます。
5. 次のように、黄色で強調表示されているコードを追加して、 *Global.asax.cs*ファイルを変更します。  

    [!code-csharp[Main](membership-and-administration/samples/sample2.cs?highlight=11,26-28)]
6. `AddUserAndRole` が赤で下線が引かれていることに注意してください。 AddUserAndRole コードをダブルクリックします。  
   強調表示されたメソッドの先頭にある文字 "A" に下線が引かれます。
7. 文字 "A" をポイントし、`AddUserAndRole` メソッドのメソッドスタブを生成するための UI をクリックします。 

    ![メンバーシップと管理-メソッドスタブの生成](membership-and-administration/_static/image1.png)
8. 次のタイトルのオプションをクリックします。  
    `Generate method stub for "AddUserAndRole" in "WingtipToys.Logic.RoleActions"`
9. *Logic*フォルダーから*RoleActions.cs*ファイルを開きます。  
   `AddUserAndRole` メソッドがクラスファイルに追加されました。
10. `NotImplementedException` を削除し、次のように黄色で強調表示されているコードを追加して、 *RoleActions.cs*ファイルを変更します。  

    [!code-csharp[Main](membership-and-administration/samples/sample3.cs?highlight=5-7,15-51)]

上記のコードでは、最初にメンバーシップデータベースのデータベースコンテキストを確立します。 メンバーシップデータベースは、 *App\_Data*フォルダーに *.mdf*ファイルとしても格納されます。 最初のユーザーがこの web アプリケーションにサインインすると、このデータベースを表示できるようになります。 

> [!NOTE] 
> 
> メンバーシップデータと製品データを格納する場合は、上記のコードに製品データを格納するために使用したものと同じ**Dbcontext**を使用することを検討してください。

 *Internal*キーワードは、型 (クラスなど) および型のメンバー (メソッドやプロパティなど) のアクセス修飾子です。 内部の型またはメンバーは、同じアセンブリ *(.dll*ファイル) に含まれるファイル内でのみアクセスできます。 アプリケーションをビルドすると、アプリケーションの実行時に実行されるコードを含むアセンブリファイル *(.dll*) が作成されます。 

ロール管理を提供する `RoleStore` オブジェクトは、データベースコンテキストに基づいて作成されます。

> [!NOTE] 
> 
> `RoleStore` オブジェクトが作成されると、ジェネリック `IdentityRole` 型が使用されることに注意してください。 これは、`RoleStore` に `IdentityRole` オブジェクトのみを含めることができることを意味します。 また、ジェネリックを使用することにより、メモリ内のリソースの処理が向上します。

次に、`RoleManager` オブジェクトが、先ほど作成した `RoleStore` オブジェクトに基づいて作成されます。 `RoleManager` オブジェクトは、`RoleStore`への変更を自動的に保存するために使用できるロール関連の API を公開します。 このコードでは `<IdentityRole>` ジェネリック型が使用されているため、`RoleManager` には `IdentityRole` オブジェクトのみを含めることができます。

"CanEdit" ロールがメンバーシップデータベースに存在するかどうかを判断するには、`RoleExists` メソッドを呼び出します。 そうでない場合は、ロールを作成します。

`UserManager` オブジェクトの作成は、`RoleManager` コントロールよりも複雑に見えますが、ほぼ同じです。 このコードは、いくつかではなく1行に記述されているだけです。 ここでは、渡されるパラメーターは、かっこ内に含まれる新しいオブジェクトとしてインスタンス化されます。

次に、新しい `ApplicationUser` オブジェクトを作成して "canEditUser" ユーザーを作成します。 その後、ユーザーが正常に作成されたら、そのユーザーを新しいロールに追加します。

> [!NOTE] 
> 
> エラー処理は、このチュートリアルシリーズの後半の「ASP.NET Error 処理」チュートリアルで更新されます。

アプリケーションの次回の起動時に、"canEditUser" という名前のユーザーが、アプリケーションの "canEdit" という名前のロールとして追加されます。 このチュートリアルの後の方で、このチュートリアルで追加する機能を表示するには、"canEditUser" ユーザーとしてログインします。 ASP.NET Identity に関する API の詳細につい[ては、](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx)「」を参照してください。 ASP.NET Identity システムの初期化の詳細については、 [AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs)を参照してください。

### <a name="restricting-access-to-the-administration-page"></a>管理ページへのアクセスの制限

Wingtip Toys サンプルアプリケーションでは、匿名ユーザーとログインユーザーの両方が製品を表示および購入できます。 ただし、カスタムの "canEdit" ロールを持つログインユーザーは、製品を追加および削除するために制限されたページにアクセスできます。

#### <a name="add-an-administration-folder-and-page"></a>管理フォルダーとページの追加

次に、Wingtip Toys サンプルアプリケーションのカスタムロールに属している "canEditUser" ユーザーの " *Admin* " という名前のフォルダーを作成します。

1. **ソリューションエクスプローラー**でプロジェクト名 (**Wingtip Toys**) を右クリックし、[ -&gt;**新しいフォルダー**の**追加**] を選択します。
2. 新しいフォルダーに「 *Admin*」という名前を指定します。
3. [ *Admin* ] フォルダーを右クリックし、[ -の**追加**] &gt; **[新しい項目]** の順に選択します。   
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
4. 左側の<strong>[ C# Visual</strong>-&gt; <strong>Web</strong>テンプレート] グループを選択します。 中央の一覧で、[<strong>マスターページを含む Web フォーム</strong>] を選択し、「 <em>adminpage .aspx</em><strong>」</strong>という名前を付けて、[<strong>追加</strong>] を選択します。
5. マスターページとして [] を選択し、[ **OK]** を選択し*ます。*

#### <a name="add-a-webconfig-file"></a>Web.config ファイルを追加する

*管理*フォルダーに*web.config*ファイルを追加することで、フォルダーに含まれているページへのアクセスを制限できます。

1. [ *Admin* ] フォルダーを右クリックし、 **[追加]** [ -&gt;**新しい項目**] の順に選択します。  
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. C# Visual web テンプレートの一覧から、中央の一覧から [ <strong>web 構成ファイル</strong>] を選択し、web.config の既定の名前をそのまま<strong>使用し</strong><em>て、[</em><strong>追加</strong>] を選択します。
3. *Web.config ファイル内*の既存の XML コンテンツを次の内容に置き換えます。  

    [!code-xml[Main](membership-and-administration/samples/sample4.xml)]

*Web.config ファイルを*保存します。 Web.config*ファイルは*、アプリケーションの "canedit" ロールに属しているユーザーのみが、*管理*フォルダーに含まれるページにアクセスできることを指定します。

### <a name="including-custom-role-navigation"></a>カスタムロールナビゲーションを含む

カスタムの "canEdit" ロールのユーザーがアプリケーションの [管理] セクションに移動できるようにするには、サイトの [*マスター* ] ページへのリンクを追加する必要があります。 "CanEdit" ロールに属しているユーザーのみが、管理**者**リンクを表示し、[管理] セクションにアクセスできます。

1. ソリューションエクスプローラーで、[ *] ページを*見つけて開きます。
2. "CanEdit" ロールのユーザーのリンクを作成するには、次のようにリストが表示されるように、黄色で強調表示されているマークアップを次の順序付けされていないリスト `<ul>` 要素に追加します。  

    [!code-html[Main](membership-and-administration/samples/sample5.html?highlight=2-3)]
3. *Site.Master.cs*ファイルを開きます。 黄色で強調表示されているコードを `Page_Load` ハンドラーに追加することで、"canEditUser" ユーザーにのみ**Admin**リンクを表示します。 `Page_Load` ハンドラーは次のように表示されます。   

    [!code-csharp[Main](membership-and-administration/samples/sample6.cs?highlight=3-6)]

ページが読み込まれると、コードは、ログインしているユーザーのロールが "canEdit" であるかどうかを確認します。 ユーザーが "canEdit" ロールに属している場合、 *adminpage .aspx*ページへのリンクを含む span 要素 (およびスパン内のリンク) が表示されます。

### <a name="enabling-product-administration"></a>製品管理の有効化

ここまでで、"canEdit" ロールを作成し、"canEditUser" ユーザー、管理フォルダー、および管理ページを追加しました。 管理フォルダーとページのアクセス権を設定し、アプリケーションに "canEdit" ロールのユーザーのナビゲーションリンクを追加しました。 次に、 *adminpage .aspx*ページにマークアップを追加し、 *AdminPage.aspx.cs*分離コードファイルにコードを追加します。これにより、"canedit" ロールのユーザーが製品を追加したり削除したりできるようになります。

1. **ソリューションエクスプローラー**で、 *Admin*フォルダーから*adminpage*ファイルを開きます。
2. 既存のマークアップを次のように置き換えます。  

    [!code-aspx[Main](membership-and-administration/samples/sample7.aspx)]
3. 次に、 *adminpage*を右クリックして **[コードの表示]** をクリックし、 *AdminPage.aspx.cs*分離コードファイルを開きます。
4. *AdminPage.aspx.cs*分離コードファイルの既存のコードを次のコードに置き換えます。  

    [!code-csharp[Main](membership-and-administration/samples/sample8.cs)]

*AdminPage.aspx.cs*分離コードファイルに入力したコードでは、`AddProducts` というクラスを使用して、実際に製品をデータベースに追加する作業が行われます。 このクラスはまだ存在しないため、ここで作成します。

1. **ソリューションエクスプローラー**で、 *Logic*フォルダーを右クリックし、 **[追加]** [ -&gt;**新しい項目**] の順に選択します。   
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. 左側の **[ C# Visual** -&gt;**コード**テンプレート] グループを選択します。 次に、中央の一覧から **[クラス]** を選択し、「 *AddProducts.cs*」という名前を指定します。   
   新しいクラスファイルが表示されます。
3. 既存のコードを次のコードに置き換えます。  

    [!code-csharp[Main](membership-and-administration/samples/sample9.cs)]

*Adminpage .aspx*ページでは、"canedit" ロールに属しているユーザーが製品を追加および削除できます。 新しい製品が追加されると、製品の詳細が検証され、データベースに入力されます。 新しい製品は、web アプリケーションのすべてのユーザーがすぐに使用できるようになります。

#### <a name="unobtrusive-validation"></a>控えめに検証

ユーザーが*adminpage .aspx*ページで提供する製品の詳細は、検証コントロール (`RequiredFieldValidator` および `RegularExpressionValidator`) を使用して検証されます。 これらのコントロールは、控えめな検証を自動的に使用します。 控えめな検証では、検証コントロールがクライアント側の検証ロジックに JavaScript を使用できるようになります。これは、ページが検証のためにサーバーへのトリップを必要としないことを意味します。 既定では、次の構成設定に基づいて、控えめな検証が*web.config ファイルに*含まれています。

[!code-xml[Main](membership-and-administration/samples/sample10.xml)]

#### <a name="regular-expressions"></a>正規表現

*Adminpage .aspx*ページの製品価格は、 **RegularExpressionValidator**コントロールを使用して検証されます。 このコントロールは、関連付けられている入力コントロール ("AddProductPrice" テキストボックス) の値が正規表現で指定されたパターンと一致するかどうかを検証します。 正規表現は、パターンマッチングの表記で、特定の文字パターンをすばやく検索して一致させることができます。 **RegularExpressionValidator**コントロールには、次に示すように、価格入力の検証に使用される正規表現を含む `ValidationExpression` という名前のプロパティが含まれています。

[!code-aspx[Main](membership-and-administration/samples/sample11.aspx)]

#### <a name="fileupload-control"></a>FileUpload コントロール

入力コントロールと検証コントロールに加えて、 **FileUpload**コントロールを*adminpage .aspx*ページに追加しました。 このコントロールには、ファイルをアップロードする機能が用意されています。 この場合、イメージファイルのアップロードのみを許可します。 分離コードファイル (*AdminPage.aspx.cs*) で、`AddProductButton` をクリックすると、コードは**FileUpload**コントロールの `HasFile` プロパティをチェックします。 コントロールにファイルがあり、ファイルの種類 (ファイル拡張子に基づく) が許可されている場合、イメージは*images*フォルダーと、アプリケーションの*images/親指*フォルダーに保存されます。

#### <a name="model-binding"></a>モデル バインド

このチュートリアルシリーズの前半では、モデルバインドを使用して**ListView**コントロール、**フォームビュー**コントロール、 **GridView**コントロール、および**ビュー**コントロールを設定していました。 このチュートリアルでは、モデルバインドを使用して、 **DropDownList**コントロールに製品カテゴリの一覧を設定します。

*Adminpage*ファイルに追加したマークアップには、`DropDownAddCategory`という**DropDownList**コントロールが含まれています。

[!code-aspx[Main](membership-and-administration/samples/sample12.aspx)]

モデルバインドを使用して、`ItemType` 属性と `SelectMethod` 属性を設定して、この**DropDownList**を設定します。 `ItemType` 属性は、コントロールを設定するときに `WingtipToys.Models.Category` 型を使用することを指定します。 この型は、このチュートリアルシリーズの冒頭で、`Category` クラスを作成して定義しています (以下の図を参照)。 `Category` クラスは、 *Category.cs*ファイル内の [*モデル*] フォルダーにあります。

[!code-csharp[Main](membership-and-administration/samples/sample13.cs)]

**DropDownList**コントロールの `SelectMethod` 属性は、分離コードファイル (*AdminPage.aspx.cs*) に含まれる `GetCategories` メソッド (下記参照) を使用することを指定します。

[!code-csharp[Main](membership-and-administration/samples/sample14.cs)]

このメソッドは、`Category` 型に対してクエリを評価するために `IQueryable` インターフェイスを使用することを指定します。 返された値は、ページのマークアップ (*adminpage*) で**DropDownList**を設定するために使用されます。

リスト内の各項目に対して表示されるテキストは、`DataTextField` 属性を設定することによって指定されます。 `DataTextField` 属性は、上に示した `Category` クラスの `CategoryName` を使用して、 **DropDownList**コントロールに各カテゴリを表示します。 **DropDownList**コントロールで項目が選択されたときに渡される実際の値は、`DataValueField` 属性に基づきます。 `DataValueField` 属性は、上に示した `Category` クラスの定義に従って `CategoryID` に設定されます。

### <a name="how-the-application-will-work"></a>アプリケーションの動作

"CanEdit" ロールに属しているユーザーが最初にページに移動すると、前述のように `DropDownAddCategory`**DropDownList**コントロールが設定されます。 `DropDownRemoveProduct`**DropDownList**コントロールにも、同じ方法で製品が設定されます。 "CanEdit" ロールに属しているユーザーは、カテゴリの種類を選択し、製品の詳細 (**名前**、**説明**、**価格**、および**画像ファイル**) を追加します。 "CanEdit" ロールに属しているユーザーが **[製品の追加]** ボタンをクリックすると、`AddProductButton_Click` イベントハンドラーがトリガーされます。 分離コードファイル (*AdminPage.aspx.cs*) にある `AddProductButton_Click` イベントハンドラーは、イメージファイルが、許可されているファイルの種類 *(.gif*、 *.png*、 *.jpeg*、または *.jpg*) と一致しているかどうかを確認します。 次に、イメージファイルは Wingtip Toys サンプルアプリケーションのフォルダーに保存されます。 次に、新しい製品がデータベースに追加されます。 新しい製品の追加を完了するために、`AddProducts` クラスの新しいインスタンスが作成され、製品という名前が付けられます。 `AddProducts` クラスには `AddProduct`という名前のメソッドがあり、products オブジェクトはこのメソッドを呼び出して、製品をデータベースに追加します。

[!code-csharp[Main](membership-and-administration/samples/sample15.cs)]

コードによって新しい製品がデータベースに正常に追加されると、`ProductAction=add`クエリ文字列値を使用してページが再読み込みされます。

[!code-csharp[Main](membership-and-administration/samples/sample16.cs)]

ページが再読み込みされると、クエリ文字列が URL に含まれます。 ページを再読み込みすると、"canEdit" ロールに属しているユーザーは、 *adminpage .aspx*ページの**DropDownList**コントロールで更新をすぐに確認できます。 また、URL と共にクエリ文字列を含めることで、"canEdit" ロールに属しているユーザーに成功メッセージを表示できます。

*Adminpage .aspx*ページを再読み込みすると、`Page_Load` イベントが呼び出されます。

[!code-csharp[Main](membership-and-administration/samples/sample17.cs)]

`Page_Load` イベントハンドラーは、クエリ文字列の値を確認し、成功メッセージを表示するかどうかを決定します。

## <a name="running-the-application"></a>アプリケーションの実行

ここでアプリケーションを実行して、ショッピングカートのアイテムを追加、削除、および更新する方法を確認できます。 ショッピングカートの合計には、ショッピングカート内のすべての品目の合計コストが反映されます。

1. ソリューションエクスプローラーで、 **F5**キーを押して Wingtip Toys サンプルアプリケーションを実行します。  
   ブラウザーが開き、 *default.aspx*ページが表示されます。
2. ページの上部にある **[ログイン]** リンクをクリックします。 

    ![メンバーシップと管理-[ログイン] リンク](membership-and-administration/_static/image2.png)

   *Login.aspx*ページが表示されます。
3. 次のユーザー名とパスワードを使用します。  
   ユーザー名: canEditUser@wingtiptoys.com  
   パスワード: Pa $ $word 1 

    ![メンバーシップと管理-[ログイン] ページ](membership-and-administration/_static/image3.png)
4. ページの下部にある **[ログイン]** ボタンをクリックします。
5. 次のページの上部にある **[管理者]** リンクを選択して、 *adminpage .aspx*ページに移動します。 

    ![メンバーシップと管理-管理者リンク](membership-and-administration/_static/image4.png)
6. 入力の検証をテストするには、製品の詳細を追加せずに **[製品の追加]** ボタンをクリックします。 

    ![メンバーシップと管理-[管理者] ページ](membership-and-administration/_static/image5.png)

   必須フィールドメッセージが表示されていることに注意してください。
7. 新しい製品の詳細を追加し、 **[製品の追加]** ボタンをクリックします。 

    ![メンバーシップと管理-製品の追加](membership-and-administration/_static/image6.png)
8. 上部のナビゲーションメニューから **[製品]** を選択すると、追加した新しい製品が表示されます。 

    ![メンバーシップと管理-新しい製品の表示](membership-and-administration/_static/image7.png)
9. [管理**者**] リンクをクリックして、[管理] ページに戻ります。
10. ページの **[製品の削除]** セクションで、ドロップダウン**リスト**に追加した新しい製品を選択します。
11. **[製品の削除]** ボタンをクリックして、新しい製品をアプリケーションから削除します。 

    ![メンバーシップと管理-製品の削除](membership-and-administration/_static/image8.png)
12. 上部のナビゲーションメニューから **[製品]** を選択して、製品が削除されたことを確認します。
13. [ログオフ] を**クリックして**、存在する管理モードにします。   
    上部のナビゲーションウィンドウに **[管理]** メニュー項目が表示されなくなっていることに注意してください。

## <a name="summary"></a>要約

このチュートリアルでは、カスタムロールとカスタムロールに属しているユーザー、管理フォルダーとページへの制限付きアクセス、およびカスタムロールに属しているユーザーのナビゲーションを追加しました。 モデルバインドを使用して、 **DropDownList**コントロールにデータを設定しています。 **FileUpload**コントロールと検証コントロールを実装しています。 また、データベースの製品を追加および削除する方法についても説明しました。 次のチュートリアルでは、ASP.NET ルーティングを実装する方法について説明します。

## <a name="additional-resources"></a>その他の資料

[Web.config-authorization 要素](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)  
[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)  
[メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET Web フォームアプリを Azure の Web サイトにデプロイする](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure-無料試用版](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [前へ](checkout-and-payment-with-paypal.md)
> [次へ](url-routing.md)

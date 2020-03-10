---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Razor および控えめな JavaScript を使用した MVC 3 アプリケーションの作成 |Microsoft Docs
author: microsoft
description: ユーザー一覧のサンプル web アプリケーションでは、Razor ビューエンジンを使用して ASP.NET MVC 3 アプリケーションを簡単に作成する方法を示しています。 サンプルアプリケーション...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434998"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Razor および控えめな JavaScript を使用した MVC 3 アプリケーションの作成

[Microsoft](https://github.com/microsoft)

> ユーザー一覧のサンプル web アプリケーションでは、Razor ビューエンジンを使用して ASP.NET MVC 3 アプリケーションを簡単に作成する方法を示しています。 このサンプルアプリケーションでは、ASP.NET MVC version 3 と Visual Studio 2010 で新しい Razor ビューエンジンを使用して、ユーザーの作成、表示、編集、削除などの機能を含む架空のユーザーリスト web サイトを作成する方法を示します。
> 
> このチュートリアルでは、ユーザーリストのサンプル ASP.NET MVC 3 アプリケーションをビルドするために実行された手順について説明します。 このトピックでC#は、visual Studio プロジェクトと VB ソースコードを[ダウンロード](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)できます。 このチュートリアルについてご不明な点がある場合は、 [MVC フォーラム](https://forums.asp.net/1146.aspx)に投稿してください。

## <a name="overview"></a>概要

構築するアプリケーションは、単純なユーザーリストの web サイトです。 ユーザーは、ユーザー情報の入力、表示、および更新を行うことができます。

![サンプルサイト](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

[ここで](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)は、VB およびC#完成したプロジェクトをダウンロードできます。

## <a name="creating-the-web-application"></a>Web アプリケーションの作成

チュートリアルを開始するには、Visual Studio 2010 を開き、 *ASP.NET MVC 3 Web アプリケーション*テンプレートを使用して新しいプロジェクトを作成します。 アプリケーション &quot;Mvc3Razor&quot;という名前を指定します。

[新しい MVC 3 プロジェクトの ![](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

**[New ASP.NET MVC 3 プロジェクト]** ダイアログボックスで、 **[インターネットアプリケーション]** を選択し、Razor ビューエンジンを選択して、 **[OK]** をクリックします。

![新しい ASP.NET MVC 3 プロジェクトダイアログ](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

このチュートリアルでは、ASP.NET メンバーシッププロバイダーを使用しないので、ログオンとメンバーシップに関連付けられているすべてのファイルを削除できます。 **ソリューションエクスプローラー**で、次のファイルとディレクトリを削除します。

- *コントローラー \ アカウント*
- *Models\AccountModels*
- *Views\Shared\\_LogOnPartial*
- *Views\Account* (およびこのディレクトリ内のすべてのファイル)

![% N Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<em>\_Layout</em>ファイルを編集し、`logindisplay` という名前の `<div>` 要素内のマークアップを、ログインが無効になっている&quot;<em>&quot;</em>メッセージに置き換えます。 新しいマークアップの例を次に示します。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>モデルの追加

**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順にクリックします。

![新しいユーザー Mdl クラス](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

クラスに `UserModel` という名前を付けます。 *Usermodel*ファイルの内容を次のコードに置き換えます。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

`UserModel` クラスは、ユーザーを表します。 クラスの各メンバーには、 [Dataannotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間の[Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性で注釈が付けられます。 [Dataannotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間の属性は、web アプリケーションのクライアント側およびサーバー側の自動検証を提供します。

`HomeController` クラスを開き、`UserModel` および `Users` クラスにアクセスできるように、`using` ディレクティブを追加します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

`HomeController` 宣言の直後に、次のコメントと、`Users` クラスへの参照を追加します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

`Users` クラスは、このチュートリアルで使用する簡素化されたインメモリデータストアです。 実際のアプリケーションでは、データベースを使用してユーザー情報を格納します。 `HomeController` ファイルの最初の数行を次の例に示します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

アプリケーションをビルドして、次の手順でスキャフォールディングウィザードでユーザーモデルが使用できるようにします。

## <a name="creating-the-default-view"></a>既定のビューの作成

次の手順では、ユーザーを表示するためのアクションメソッドとビューを追加します。

既存の*Views\Home\Index*ファイルを削除します。 ユーザーを表示するには、新しい*インデックス*ファイルを作成します。

`HomeController` クラスで、`Index` メソッドの内容を次のコードに置き換えます。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

`Index` メソッド内を右クリックし、 **[ビューの追加]** をクリックします。

![ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

**[厳密に型指定されたビューを作成する]** オプションを選択します。 **[ビューデータクラス]** で、 **[Mvc3Razor]** を選択します。 ( **[データクラスの表示]** ボックスに**Mvc3Razor**が表示されない場合は、プロジェクトをビルドする必要があります)。ビューエンジンが**Razor**に設定されていることを確認します。 **[表示コンテンツ]** を **[一覧]** に設定 に設定し、 **[追加]** をクリックします。

![インデックスビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

新しいビューでは、`Index` ビューに渡されたユーザーデータが自動的にスキャフォールディングされます。 新しく生成された*Views\Home\Index*ファイルを確認します。 **[新規作成]** 、 **[編集]** 、 **[詳細]** 、および **[削除]** の各リンクは機能しませんが、ページの残りの部分は機能します。 ページを実行します。 ユーザーの一覧が表示できます。

![インデックスページ](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

次のコードを使用して、*インデックスの cshtml*ファイルを開き、 **Edit**、 **Details**、 **Delete**のマークアップ `ActionLink` を置き換えます。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

ユーザー名は、 **[編集]** 、 **[詳細]** 、および **[削除]** リンクで選択したレコードを検索するための ID として使用されます。

## <a name="creating-the-details-view"></a>詳細ビューの作成

次の手順では、ユーザーの詳細を表示するために `Details` アクションメソッドとビューを追加します。

![詳細](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

次の `Details` メソッドを home コントローラーに追加します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

`Details` メソッド内を右クリックし、[<strong>ビューの追加</strong>] を選択します。 [<strong>データクラスの表示</strong>] ボックスに<strong>Mvc3Razor</strong>が含まれていることを確認し<em>ます。</em> [<strong>表示コンテンツ</strong>] を [<strong>詳細</strong>] に設定し、[<strong>追加</strong>] をクリックします。

![詳細ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

アプリケーションを実行し、[詳細] リンクを選択します。 自動スキャフォールディングは、モデル内の各プロパティを表示します。

![詳細](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>編集ビューを作成する

次の `Edit` メソッドを home コントローラーに追加します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

前の手順と同様にビューを追加しますが、**ビューの内容**を**編集**するように設定します。

![編集ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

アプリケーションを実行し、1人のユーザーの姓と名を編集します。 `UserModel` クラスに適用されている `DataAnnotation` 制約に違反した場合は、フォームを送信すると、サーバーコードによって生成された検証エラーが表示されます。 たとえば、名 &quot;"彩&quot;" を&quot;&quot;に変更すると、フォームの送信時にフォームに次のエラーが表示されます。

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

このチュートリアルでは、ユーザー名を主キーとして扱います。 そのため、ユーザー名プロパティは変更できません。 `Html.BeginForm` ステートメントの直後にある*Edit. cshtml*ファイルで、ユーザー名を隠しフィールドに設定します。 これにより、プロパティがモデルで渡されます。 次のコードフラグメントは、`Hidden` ステートメントの配置を示しています。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

ユーザー名の `TextBoxFor` および `ValidationMessageFor` マークアップを `DisplayFor` 呼び出しに置き換えます。 `DisplayFor` メソッドは、プロパティを読み取り専用の要素として表示します。 完全なマークアップの例を次に示します。 元の `TextBoxFor` と `ValidationMessageFor` の呼び出しは、Razor の開始コメントと終了コメント文字 (`@* *@`) でコメントアウトされます。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>クライアント側の検証を有効にする

ASP.NET MVC 3 でクライアント側の検証を有効にするには、2つのフラグを設定し、3つの JavaScript ファイルを含める必要があります。

アプリケーションの*web.config*ファイルを開きます。 アプリケーション設定で `that ClientValidationEnabled` および `UnobtrusiveJavaScriptEnabled` が true に設定されていることを確認します。 ルートの web.config ファイルの次のフラグメントは、正しい設定を示して*い*ます。

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

`UnobtrusiveJavaScriptEnabled` を true に設定すると、控えめな Ajax と控えめなクライアント検証が有効になります。 控えめな検証を使用すると、検証規則が HTML5 属性に変換されます。 HTML5 属性名は、小文字、数字、およびダッシュのみで構成されています。

`ClientValidationEnabled` を true に設定すると、クライアント側の検証が有効になります。 アプリケーションの*web.config*ファイルでこれらのキーを設定すると、アプリケーション全体に対してクライアント検証と控えめな JavaScript が有効になります。 また、次のコードを使用して、個々のビューまたはコントローラーのメソッドでこれらの設定を有効または無効にすることもできます。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

また、レンダリングされたビューに複数の JavaScript ファイルを含める必要があります。 JavaScript をすべてのビューに含める簡単な方法として、 *Views\Shared\\_Layout*ファイルに追加することができます。 *\_Layout*ファイルの `<head>` 要素を次のコードに置き換えます。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

最初の2つの jQuery スクリプトは、Microsoft Ajax Content Delivery Network (CDN) によってホストされます。 Microsoft Ajax CDN を利用することにより、アプリケーションの最初のヒットパフォーマンスを大幅に向上させることができます。

アプリケーションを実行し、[編集] リンクをクリックします。 ブラウザーでページのソースを表示します。 ブラウザーソースには、(データ検証の) `data-val` フォームの多くの属性が表示されます。 クライアント検証と控えめな JavaScript が有効になっている場合、クライアント検証規則を持つ入力フィールドには、控えめなクライアント検証をトリガーするための `data-val="true"` 属性が含まれています。 たとえば、モデルの `City` フィールドが[Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性で修飾された場合、次の例に示すように HTML が生成されます。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

各クライアント検証規則に対して、`data-val-rulename="message"`という形式の属性が追加されます。 前に示した `City` フィールドの例を使用すると、必要なクライアント検証規則によって `data-val-required` 属性が生成され、City フィールド &quot;メッセージが&quot;必要になります。 アプリケーションを実行し、いずれかのユーザーを編集して、[`City`] フィールドをオフにします。 フィールドからタブを除外すると、クライアント側の検証エラーメッセージが表示されます。

![市区町村が必要です](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

同様に、クライアント検証規則の各パラメーターには、`data-val-rulename-paramname=paramvalue`という形式の属性が追加されます。 たとえば、`FirstName` プロパティは[Stringlength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性で注釈が付けられ、最小長は3、最大長は8です。 `length` という名前のデータ検証規則では、パラメーター名 `max` とパラメーター値8が指定されています。 次に、いずれかのユーザーを編集するときに `FirstName` フィールドに対して生成される HTML を示します。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

控えめなクライアント検証の詳細については、Brad Wilson のブログの「 [ASP.NET MVC 3 の控えめなクライアント検証](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)」を参照してください。

> [!NOTE]
> ASP.NET MVC 3 Beta では、クライアント側の検証を開始するためにフォームを送信することが必要になる場合があります。 これは、最終リリースで変更される可能性があります。

## <a name="creating-the-create-view"></a>作成ビューの作成

次の手順では、ユーザーが新しいユーザーを作成できるようにするために `Create` アクションメソッドとビューを追加します。 次の `Create` メソッドを home コントローラーに追加します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

前の手順と同様にビューを追加しますが、[**作成**する**ビューコンテンツ**] を設定します。

![CREATE VIEW](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

アプリケーションを実行し、 **[作成]** リンクを選択して、新しいユーザーを追加します。 `Create` メソッドでは、クライアント側とサーバー側の検証を自動的に利用します。 &quot;Ben X&quot;などの空白を含むユーザー名を入力してください。 [ユーザー名] フィールドから tab キーを使用すると、クライアント側の検証エラー (`White space is not allowed`) が表示されます。

## <a name="add-the-delete-method"></a>Delete メソッドを追加する

このチュートリアルを完了するには、次の `Delete` メソッドを home コントローラーに追加します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

前の手順のように `Delete` ビューを追加して、[**ビューコンテンツ**を**削除**する] に設定します。

![ビューの削除](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

これで、完全に機能する単純な ASP.NET MVC 3 アプリケーションが検証されました。

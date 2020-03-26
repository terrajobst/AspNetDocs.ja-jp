---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: JQuery UI Datepicker とモデルバインドおよび web フォームとの統合 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データの相互作用がより簡単になり-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521980"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a>JQuery UI Datepicker とモデルバインドおよび web フォームとの統合

によって[Tom FitzMacken](https://github.com/tfitzmac)

> このチュートリアルシリーズでは、ASP.NET Web フォームプロジェクトでモデルバインドを使用するための基本的な側面を示します。 モデルバインドを使用すると、データソースオブジェクト (ObjectDataSource や SqlDataSource など) を処理するよりも、データ操作がより簡単になります。 このシリーズでは、入門資料から開始し、以降のチュートリアルでより高度な概念に移ります。
> 
> このチュートリアルでは、JQuery UI [Datepicker ウィジェット](http://jqueryui.com/datepicker/)を Web フォームに追加し、モデルバインドを使用して、選択した値でデータベースを更新する方法について説明します。
> 
> このチュートリアルは、シリーズの[第 1](retrieving-data.md)部と[第 2](updating-deleting-and-creating-data.md)部で作成したプロジェクトに基づいています。
> 
> 完全なプロジェクトは、またはC# VB で[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=286116)できます。 ダウンロード可能なコードは、Visual Studio 2012 または Visual Studio 2013 で動作します。 このチュートリアルでは、Visual Studio 2012 テンプレートを使用します。これは、このチュートリアルで示した Visual Studio 2013 テンプレートとは少し異なります。

## <a name="what-youll-build"></a>ビルドする内容

このチュートリアルでは、次のことについて説明します。

1. 学生の登録日を記録するために、モデルにプロパティを追加します
2. JQuery UI Datepicker ウィジェットを使用して、ユーザーが登録日を選択できるようにします
3. 登録日に検証規則を適用する

JQuery UI Datepicker ウィジェットを使用すると、ユーザーがフィールドと対話したときに表示されるカレンダーから日付を簡単に選択できます。 このウィジェットを使用すると、ユーザーが手動で日付を入力するよりも便利です。 データ操作にモデルバインドを使用するページに Datepicker ウィジェットを統合するには、少量の追加作業のみが必要です。

## <a name="add-a-new-property-to-the-model"></a>新しいプロパティをモデルに追加します。

まず、スチューデントモデルに**Datetime**プロパティを追加し、その変更をデータベースに移行します。 **UniversityModels.cs**を開き、強調表示されているコードを Student モデルに追加します。

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

**Rangeattribute**は、プロパティの検証規則を適用するために含まれています。 このチュートリアルでは、Contoso 大学が2013年1月1日に設立されていることを前提としています。そのため、以前の登録日は無効です。

[Package Management] ウィンドウで、 **AddEnrollmentDate**コマンドを実行して移行を追加します。 移行コードによって、新しい Datetime 列が Student テーブルに追加されていることに注意してください。 RangeAttribute で指定した値と一致させるには、次の強調表示されているコードに示すように、新しい列の既定値を追加します。

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

移行ファイルに変更を保存します。

データを再度シードする必要はありません。 そのため、[移行] フォルダーで**Configuration.cs**を開き、 **Seed**メソッドのコードを削除またはコメントアウトします。 ファイルを保存して閉じます。

次に、コマンド**update-database**を実行します。 列がデータベースに存在し、既存のすべてのレコードの既定値が EnrollmentDate になっていることに注意してください。

## <a name="add-dynamic-controls-for-enrollment-date"></a>登録日の動的コントロールを追加する

ここで、登録日を表示および編集するためのコントロールを追加します。 この時点で、値はテキストボックスを使用して編集されます。 このチュートリアルの後半では、テキストボックスを JQuery Datepicker ウィジェットに変更します。

まず、 **Addstudent .aspx**ファイルを変更する必要がないことに注意してください。 DynamicEntity コントロールは、新しいプロパティを自動的に表示します。

**Student**を開き、次の強調表示されたコードを追加します。

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

アプリケーションを実行して、登録日の値を日付を入力して設定できることを確認します。 新しい学生を追加する場合:

![日付の設定](integrating-jquery-ui/_static/image1.png)

または、既存の値を編集します。

![日付の編集](integrating-jquery-ui/_static/image2.png)

日付を入力しても機能しますが、お客様が提供するユーザーエクスペリエンスとは限りません。 次のセクションでは、カレンダーを使用して日付を選択できるようにします。

## <a name="install-nuget-package-to-work-with-jquery-ui"></a>JQuery UI を使用するための NuGet パッケージのインストール

**ジュース ui** NuGet パッケージを使用すると、JQuery ui ウィジェットを web アプリケーションに簡単に統合できます。 このパッケージを使用するには、NuGet を使用してインストールします。

![ジュース UI の追加](integrating-jquery-ui/_static/image3.png)

インストールするジュース UI のバージョンが、アプリケーションの JQuery のバージョンと競合する可能性があります。 このチュートリアルを続行する前に、アプリケーションを実行してみてください。 JavaScript エラーが発生した場合は、JQuery バージョンを調整する必要があります。 必要なバージョンの JQuery を Scripts フォルダー (このチュートリアルの作成時にバージョン 1.8.2) に追加するか、または、サイトで JQuery ファイルへのパスを指定することができます。

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a>Datepicker ウィジェットを含めるように DateTime テンプレートをカスタマイズする

Datetime 値を編集するために、動的データテンプレートに Datepicker ウィジェットを追加します。 テンプレートにウィジェットを追加すると、新しい学生を追加するためのフォームと、学生を編集するためのグリッドビューの両方に自動的にレンダリングされます。 **DateTime\_Edit .ascx**を開き、次の強調表示されたコードを追加します。

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

分離コードファイルでは、DatePicker の日付の最小値と最大値を設定します。 これらの値を設定すると、ユーザーが無効な日付に移動するのを防ぐことができます。 DateTime プロパティの**Rangeattribute**から最小値と最大値を取得します (指定されている場合)。 **DateTime\_Edit.ascx.cs**を開き、次の強調表示されたコードをページ\_Load メソッドに追加します。

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

Web アプリケーションを実行し、AddStudent ページに移動します。 フィールドに値を指定すると、登録日のテキストボックスをクリックするとカレンダーが表示されることがわかります。

![日付の選択](integrating-jquery-ui/_static/image4.png)

日付を選択し、 **[挿入]** をクリックします。 RangeAttribute は、サーバーで検証を強制します。 Datepicker の minDate プロパティを設定することにより、クライアントに検証も適用します。 このカレンダーでは、ユーザーは minDate の値より前の日付に移動することはできません。

グリッドビューでレコードを編集すると、カレンダーも表示されます。

![GridView の Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a>まとめ

このチュートリアルでは、モデルバインドを使用する web フォームに JQuery ウィジェットを組み込む方法について学習しました。

次の[チュートリアル](using-query-string-values-to-retrieve-data.md)では、データを選択するときにクエリ文字列値を使用します。

> [!div class="step-by-step"]
> [前へ](sorting-paging-and-filtering-data.md)
> [次へ](using-query-string-values-to-retrieve-data.md)

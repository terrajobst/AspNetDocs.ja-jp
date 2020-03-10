---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: ASP.NET Web ページ (Razor) サイトでのユーザー入力の検証Microsoft Docs
author: Rick-Anderson
description: この記事では、ユーザーから取得した情報を検証する方法について説明します。これは、ユーザーがという形式で HTML フォームの有効な情報を入力することを確認するために &mdash; ます。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454300"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a>ASP.NET Web ページ (Razor) サイトでのユーザー入力の検証

[Tom FitzMacken](https://github.com/tfitzmac)

> この記事では、ユーザー &mdash; から取得した情報を検証する方法について説明します。つまり、ユーザーが ASP.NET Web ページ (Razor) サイトの HTML フォームに有効な情報を入力していることを確認します。
> 
> ここでは、次の内容について学習します。
> 
> - ユーザーの入力が定義した検証条件に一致するかどうかを確認する方法。
> - すべての検証テストが成功したかどうかを確認する方法。
> - 検証エラーを表示する方法 (および書式設定方法)。
> - ユーザーから直接取得されないデータを検証する方法。
> 
> この記事で紹介する ASP.NET プログラミングの概念は次のとおりです。
> 
> - `Validation` ヘルパー。
> - `Html.ValidationSummary` メソッドと `Html.ValidationMessage` メソッド。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 3
>   
> 
> このチュートリアルは ASP.NET Web ページ2でも動作します。

このトピックの内容は次のとおりです。

- [ユーザー入力の検証の概要](#Overview_of_User_Input_Validation)
- [ユーザー入力の検証](#Validating_User_Input)
- [クライアント側の検証の追加](#Adding_Client-Side_Validation)
- [検証エラーの書式設定](#Formatting_Validation_Errors)
- [ユーザーから直接取得されていないデータの検証](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a>ユーザー入力の検証の概要

たとえば、フォームに情報を入力するようユーザーに求める場合は、入力した値が有効であることを確認することが重要です。 たとえば、重要な情報が欠落しているフォームを処理する必要がないとします。

ユーザーが HTML フォームに値を入力すると、入力した値は文字列になります。 多くの場合、必要な値は、整数や日付などの他のデータ型です。 そのため、ユーザーが入力する値を適切なデータ型に正しく変換できることも確認する必要があります。

また、値に特定の制限がある場合もあります。 たとえば、ユーザーが適切に整数を入力したとしても、値が特定の範囲内に収まるようにする必要がある場合があります。

![CSS スタイルクラスを使用する検証エラー](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> **重要**ユーザー入力の検証は、セキュリティのためにも重要です。 ユーザーがフォームに入力できる値を制限すると、サイトのセキュリティを損なう可能性のある値をユーザーが入力できる可能性が低くなります。

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a>ユーザー入力の検証

ASP.NET Web ページ2では、`Validator` ヘルパーを使用してユーザー入力をテストできます。 基本的な方法は次のとおりです。

1. 検証する入力要素 (フィールド) を決定します。

    通常、フォーム内の `<input>` 要素の値を検証します。 ただし、`<select>` リストのような制約された要素からの入力も含め、すべての入力を検証することをお勧めします。 これにより、ユーザーがページ上のコントロールをバイパスしてフォームを送信しないようにすることができます。
2. ページコードで、`Validation` ヘルパーのメソッドを使用して、各入力要素に対して個別の検証チェックを追加します。

    必須フィールドを確認するには、`Validation.RequireField(field, [error message])` (個々のフィールド) または `Validation.RequireFields(field1, field2, ...))` (フィールドの一覧) を使用します。 その他の種類の検証については、`Validation.Add(field, ValidationType)`を使用します。 `ValidationType`には、次のオプションを使用できます。

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. ページが送信されたら、`Validation.IsValid`を確認して、検証が成功したかどうかを確認します。

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    検証エラーが発生した場合は、通常のページ処理をスキップします。 たとえば、ページの目的がデータベースを更新する必要がある場合、すべての検証エラーが修正されるまで、そのような処理は行われません。
4. 検証エラーが発生した場合は、`Html.ValidationSummary` または `Html.ValidationMessage`、またはその両方を使用して、ページのマークアップにエラーメッセージを表示します。

次の例は、これらの手順を示すページを示しています。

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

検証のしくみを確認するには、このページを実行し、意図的に間違いを犯してください。 たとえば、コース名を入力し忘れた場合に、「」と入力したときに、無効な日付を入力すると、次のようなページが表示されます。

![レンダリングされたページでの検証エラー](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a>クライアント側の検証の追加

既定では、ユーザーの入力は、ユーザーがページを送信した後に検証されます。つまり、検証はサーバーコードで実行されます。 この方法の欠点は、ユーザーがページを送信するまでエラーが発生したことをユーザーが認識していないことです。 フォームが長い場合や複雑な場合は、ページが送信された後にのみエラーを報告すると、ユーザーにとって不便な場合があります。

クライアントスクリプトで検証を実行するためのサポートを追加できます。 この場合、ユーザーがブラウザーで作業するときに検証が実行されます。 たとえば、値が整数であることを指定したとします。 ユーザーが整数以外の値を入力した場合、ユーザーが入力フィールドを離れるとすぐにエラーが報告されます。 ユーザーはすぐにフィードバックを受け取ります。これは便利です。 クライアントベースの検証では、複数のエラーを修正するために、ユーザーがフォームを送信する必要がある回数を減らすこともできます。

> [!NOTE]
> クライアント側の検証を使用する場合でも、検証はサーバーコードで常に実行されます。 サーバーコードでの検証の実行は、ユーザーがクライアントベースの検証を省略した場合のセキュリティ対策です。

1. ページに次の JavaScript ライブラリを登録します。  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   2つのライブラリは、コンテンツ配信ネットワーク (CDN) から読み込むことができるため、コンピューターまたはサーバーに必ずしも必要ではありません。 ただし、 *jquery*のローカルコピーを持っている必要があります。 ライブラリを含む WebMatrix テンプレート (**スターターサイト**など) をまだ使用していない場合は、 **starter サイト**に基づいた Web ページサイトを作成します。 次に、 *.js*ファイルを現在のサイトにコピーします。
2. マークアップで、検証する要素ごとに `Validation.For(field)`の呼び出しを追加します。 このメソッドは、クライアント側の検証で使用される属性を出力します。 (実際の JavaScript コードを出力するのではなく、メソッドは `data-val-...`のような属性を出力します。 これらの属性は、jQuery を使用して作業を行う控えめなクライアント検証をサポートしています)。

次のページは、前に示した例にクライアント検証機能を追加する方法を示しています。

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

すべての検証チェックがクライアントで実行されるわけではありません。 特に、データ型の検証 (整数、日付など) は、クライアントでは実行されません。 次のチェックは、クライアントとサーバーの両方で機能します。

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

この例では、有効な日付のテストがクライアントコードで機能しません。 ただし、テストはサーバーコードで実行されます。

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a>検証エラーの書式設定

次の予約名を持つ CSS クラスを定義することで、検証エラーを表示する方法を制御できます。

- [https://login.microsoftonline.com/consumers/](`field-validation-error`) エラーを表示しているときの `Html.ValidationMessage` メソッドの出力を定義します。
- [https://login.microsoftonline.com/consumers/](`field-validation-valid`) エラーがない場合に `Html.ValidationMessage` メソッドの出力を定義します。
- [https://login.microsoftonline.com/consumers/](`input-validation-error`) エラーが発生した場合に `<input>` 要素をどのようにレンダリングするかを定義します。 (たとえば、このクラスを使用すると、&lt;入力&gt; 要素の背景色を、値が無効である場合に別の色に設定できます)。この CSS クラスは、クライアント検証中にのみ使用されます (ASP.NET Web ページ 2)。
- [https://login.microsoftonline.com/consumers/](`input-validation-valid`) エラーがない場合の `<input>` 要素の外観を定義します。
- [https://login.microsoftonline.com/consumers/](`validation-summary-errors`) エラーの一覧を表示している `Html.ValidationSummary` メソッドの出力を定義します。
- [https://login.microsoftonline.com/consumers/](`validation-summary-valid`) エラーがない場合に `Html.ValidationSummary` メソッドの出力を定義します。

次の `<style>` ブロックは、エラー条件のルールを示しています。

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

前の記事の例のページにこのスタイルブロックを含めると、エラー表示は次の図のようになります。

![CSS スタイルクラスを使用する検証エラー](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> ASP.NET Web ページ2でクライアント検証を使用していない場合、`<input>` 要素 (`input-validation-error` および `input-validation-valid` の CSS クラスには何の効果もありません。

### <a name="static-and-dynamic-error-display"></a>静的および動的なエラー表示

CSS ルールは、`validation-summary-errors` や `validation-summary-valid`など、ペアで提供されます。 これらのペアを使用すると、エラー条件と "通常の" (非エラー) 条件の両方の条件に対してルールを定義できます。 エラーがない場合でも、エラー表示のマークアップは常に表示されることを理解しておくことが重要です。 たとえば、ページにマークアップに `Html.ValidationSummary` メソッドがある場合、ページが初めて要求されたときでも、ページソースには次のマークアップが含まれます。

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

つまり、`Html.ValidationSummary` メソッドは、エラー一覧が空の場合でも、常に `<div>` 要素とリストをレンダリングします。 同様に、`Html.ValidationMessage` メソッドは、エラーがない場合でも、個々のフィールドエラーのプレースホルダーとして `<span>` 要素を常にレンダリングします。

場合によっては、エラーメッセージを表示すると、ページの折り返しが発生し、ページ上の要素が移動する可能性があります。 `-valid` で終わる CSS 規則を使用すると、この問題を回避するためのレイアウトを定義できます。 たとえば、`field-validation-error` を定義し、`field-validation-valid` を同じ固定サイズにすることができます。 このようにして、フィールドの表示領域は静的であり、エラーメッセージが表示されている場合はページフローが変更されません。

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a>ユーザーから直接取得されていないデータの検証

場合によっては、HTML フォームから直接取得されない情報を検証する必要があります。 一般的な例としては、次の例のように、クエリ文字列に値が渡されるページがあります。

`http://server/myapp/EditClassInformation?classid=1022`

この場合、ページに渡された値 (`classid`の値の 1022) が有効であることを確認する必要があります。 この検証を実行するために `Validation` ヘルパーを直接使用することはできません。 ただし、検証エラーメッセージを表示する機能のように、検証システムの他の機能を使用することもできます。

> [!NOTE] 
> 
> **重要**フォームフィールドの値、クエリ文字列の値、cookie の値など、*任意*のソースから取得した値を常に検証します。 これらの値を簡単に変更できます (悪意のある目的の場合など)。 アプリケーションを保護するために、これらの値を確認する必要があります。

次の例は、クエリ文字列で渡される値を検証する方法を示しています。 このコードは、値が空ではなく、整数であることをテストします。

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

要求がフォーム送信 (`if(!IsPost)`) でない場合は、テストが実行されることに注意してください。 このテストは、ページが初めて要求されたときに合格しますが、要求がフォーム送信の場合は成功しません。

このエラーを表示するには、`Validation.AddFormError("message")`を呼び出して、エラーを検証エラーの一覧に追加します。 ページに `Html.ValidationSummary` メソッドの呼び出しが含まれている場合は、ユーザー入力の検証エラーと同様にエラーが表示されます。

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>その他のリソース

[ASP.NET Web ページサイトでの HTML フォームの操作](https://go.microsoft.com/fwlink/?LinkID=202892)

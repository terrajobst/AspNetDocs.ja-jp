---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET Web ページ (Razor) API クイックリファレンス |Microsoft Docs
author: Rick-Anderson
description: このページには、Razor 構文で ASP.NET Web ページをプログラミングするための最も一般的に使用されるオブジェクト、プロパティ、およびメソッドの簡単な例を含む一覧が含まれています。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463582"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="0812d-103">ASP.NET Web ページ (Razor) API クイックリファレンス</span><span class="sxs-lookup"><span data-stu-id="0812d-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>

<span data-ttu-id="0812d-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0812d-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0812d-105">このページには、Razor 構文で ASP.NET Web ページをプログラミングするための最も一般的に使用されるオブジェクト、プロパティ、およびメソッドの簡単な例を含む一覧が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0812d-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="0812d-106">"(V2)" でマークされた説明は ASP.NET Web ページバージョン2で導入されました。</span><span class="sxs-lookup"><span data-stu-id="0812d-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="0812d-107">API リファレンスドキュメントについては、MSDN の[ASP.NET Web ページリファレンスドキュメント](https://go.microsoft.com/fwlink/?LinkId=208659)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0812d-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="0812d-108">ソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="0812d-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="0812d-109">ASP.NET Web ページ (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="0812d-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="0812d-110">このチュートリアルでは、ASP.NET Web ページ2および ASP.NET Web ページ 1.0 (v2 とマークされている機能を除く) でも動作します。</span><span class="sxs-lookup"><span data-stu-id="0812d-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>

<span data-ttu-id="0812d-111">このページには、次の参照情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0812d-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="0812d-112">クラス</span><span class="sxs-lookup"><span data-stu-id="0812d-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="0812d-113">データ</span><span class="sxs-lookup"><span data-stu-id="0812d-113">Data</span></span>](#Data)
- [<span data-ttu-id="0812d-114">支援</span><span class="sxs-lookup"><span data-stu-id="0812d-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="0812d-115">検証</span><span class="sxs-lookup"><span data-stu-id="0812d-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="0812d-116">クラス</span><span class="sxs-lookup"><span data-stu-id="0812d-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="0812d-117">アプリケーション内の任意のページで共有できるデータを格納します。</span><span class="sxs-lookup"><span data-stu-id="0812d-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="0812d-118">次の例のように、動的 `App` プロパティを使用して、同じデータにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="0812d-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="0812d-119">文字列値をブール値 (true/false) に変換します。</span><span class="sxs-lookup"><span data-stu-id="0812d-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="0812d-120">False を返します。文字列が true または false を表さない場合は、指定された値を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="0812d-121">文字列値を日付/時刻に変換します。</span><span class="sxs-lookup"><span data-stu-id="0812d-121">Converts a string value to date/time.</span></span> <span data-ttu-id="0812d-122">文字列が日付/時刻を表していない場合は `DateTime.MinValue` または指定された値を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="0812d-123">文字列値を10進値に変換します。</span><span class="sxs-lookup"><span data-stu-id="0812d-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="0812d-124">文字列が10進数値を表していない場合は、0.0 または指定された値を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="0812d-125">文字列値を float に変換します。</span><span class="sxs-lookup"><span data-stu-id="0812d-125">Converts a string value to a float.</span></span> <span data-ttu-id="0812d-126">文字列が10進数値を表していない場合は、0.0 または指定された値を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="0812d-127">文字列値を整数に変換します。</span><span class="sxs-lookup"><span data-stu-id="0812d-127">Converts a string value to an integer.</span></span> <span data-ttu-id="0812d-128">文字列が整数を表さない場合は、0または指定された値を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="0812d-129">省略可能な追加のパス部分を使用して、ローカルファイルパスからブラウザーと互換性のある URL を作成します。</span><span class="sxs-lookup"><span data-stu-id="0812d-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="0812d-130">HTML エンコードされた出力として表示するのではなく、*値*を html マークアップとしてレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="0812d-131">値を文字列から指定した型に変換できる場合は true を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="0812d-132">オブジェクトまたは変数に値がない場合に true を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="0812d-133">要求が POST の場合は true を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="0812d-134">(最初の要求は通常 GET です)。</span><span class="sxs-lookup"><span data-stu-id="0812d-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="0812d-135">このページに適用するレイアウトページのパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="0812d-136">現在の要求のページ、レイアウトページ、および部分ページ間で共有されるデータを格納します。</span><span class="sxs-lookup"><span data-stu-id="0812d-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="0812d-137">次の例のように、動的 `Page` プロパティを使用して、同じデータにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="0812d-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="0812d-138">(レイアウトページ)名前付きセクションに含まれていないコンテンツページのコンテンツをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="0812d-139">指定されたパスと省略可能な追加データを使用してコンテンツページを表示します。</span><span class="sxs-lookup"><span data-stu-id="0812d-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="0812d-140">余分なパラメーターの値は、位置 (例 1) またはキー (例 2) で `PageData` から取得できます。</span><span class="sxs-lookup"><span data-stu-id="0812d-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="0812d-141">(レイアウトページ)名前を持つコンテンツセクションをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="0812d-142">省略可能なセクションを作成するには、 *required*を false に設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="0812d-143">HTTP クッキーの値を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="0812d-144">現在の要求でアップロードされたファイルを取得します。</span><span class="sxs-lookup"><span data-stu-id="0812d-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="0812d-145">(文字列として) フォームにポストされたデータを取得します。</span><span class="sxs-lookup"><span data-stu-id="0812d-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="0812d-146">`Request[key]` は、`Request.Form` コレクションと `Request.QueryString` コレクションの両方をチェックします。</span><span class="sxs-lookup"><span data-stu-id="0812d-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="0812d-147">URL クエリ文字列で指定されたデータを取得します。</span><span class="sxs-lookup"><span data-stu-id="0812d-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="0812d-148">`Request[key]` は、`Request.Form` コレクションと `Request.QueryString` コレクションの両方をチェックします。</span><span class="sxs-lookup"><span data-stu-id="0812d-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="0812d-149">フォーム要素、クエリ文字列値、cookie、またはヘッダー値の要求の検証を選択的に無効にします。</span><span class="sxs-lookup"><span data-stu-id="0812d-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="0812d-150">要求の検証は既定で有効になっており、ユーザーがマークアップや危険な可能性のあるその他のコンテンツを投稿できないようにします。</span><span class="sxs-lookup"><span data-stu-id="0812d-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="0812d-151">HTTP サーバーヘッダーを応答に追加します。</span><span class="sxs-lookup"><span data-stu-id="0812d-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="0812d-152">指定された時間のページ出力をキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="0812d-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="0812d-153">必要に応じて*スライディング*を設定して各ページのアクセスと*varyByParams*のタイムアウトをリセットし、ページ要求内の異なるクエリ文字列ごとに異なるバージョンのページをキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="0812d-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="0812d-154">ブラウザー要求を新しい場所にリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="0812d-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="0812d-155">ブラウザーに送信される HTTP ステータスコードを設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="0812d-156">オプションの MIME の種類を使用して、*データ*の内容を応答に書き込みます。</span><span class="sxs-lookup"><span data-stu-id="0812d-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="0812d-157">ファイルの内容を応答に書き込みます。</span><span class="sxs-lookup"><span data-stu-id="0812d-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="0812d-158">(レイアウトページ)名前を持つコンテンツセクションを定義します。</span><span class="sxs-lookup"><span data-stu-id="0812d-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="0812d-159">HTML エンコードされた文字列をデコードします。</span><span class="sxs-lookup"><span data-stu-id="0812d-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="0812d-160">HTML マークアップでの表示用に文字列をエンコードします。</span><span class="sxs-lookup"><span data-stu-id="0812d-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="0812d-161">指定された仮想パスのサーバー物理パスを返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="0812d-162">URL からテキストをデコードします。</span><span class="sxs-lookup"><span data-stu-id="0812d-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="0812d-163">URL に配置するためにテキストをエンコードします。</span><span class="sxs-lookup"><span data-stu-id="0812d-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="0812d-164">ユーザーがブラウザーを閉じるまで存在する値を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="0812d-165">オブジェクトの値の文字列形式を表示します。</span><span class="sxs-lookup"><span data-stu-id="0812d-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="0812d-166">URL から追加のデータを取得します (たとえば、 */MyPage/ExtraData*)。</span><span class="sxs-lookup"><span data-stu-id="0812d-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="0812d-167">指定したユーザーのパスワードを変更します。</span><span class="sxs-lookup"><span data-stu-id="0812d-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="0812d-168">アカウント確認トークンを使用してアカウントを確認します。</span><span class="sxs-lookup"><span data-stu-id="0812d-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="0812d-169">指定されたユーザー名とパスワードを使用して、新しいユーザーアカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="0812d-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="0812d-170">確認トークンを要求するには、RequireConfirmationToken に true を渡し*ます。*</span><span class="sxs-lookup"><span data-stu-id="0812d-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="0812d-171">現在ログインしているユーザーの整数識別子を取得します。</span><span class="sxs-lookup"><span data-stu-id="0812d-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="0812d-172">現在ログインしているユーザーの名前を取得します。</span><span class="sxs-lookup"><span data-stu-id="0812d-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="0812d-173">ユーザーがパスワードをリセットできるように、ユーザーに電子メールで送信できるパスワードリセットトークンを生成します。</span><span class="sxs-lookup"><span data-stu-id="0812d-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="0812d-174">ユーザー名からユーザー ID を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="0812d-175">現在のユーザーがログインしている場合は true を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="0812d-176">ユーザーが確認されている場合 (確認メールなど)、true を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="0812d-177">現在のユーザーの名前が指定されたユーザー名と一致する場合に true を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="0812d-178">Cookie の認証トークンを設定して、にユーザーを記録します。</span><span class="sxs-lookup"><span data-stu-id="0812d-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="0812d-179">認証トークン cookie を削除してユーザーをログアウトします。</span><span class="sxs-lookup"><span data-stu-id="0812d-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="0812d-180">ユーザーが認証されていない場合、HTTP ステータスを 401 (Unauthorized) に設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="0812d-181">現在のユーザーが指定されたいずれかのロールのメンバーでない場合は、HTTP ステータスを 401 (未承認) に設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="0812d-182">現在のユーザーがユーザー*名*で指定されたユーザーでない場合は、HTTP ステータスを 401 (未承認) に設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="0812d-183">パスワードリセットトークンが有効な場合、はユーザーのパスワードを新しいパスワードに変更します。</span><span class="sxs-lookup"><span data-stu-id="0812d-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="0812d-184">Data</span><span class="sxs-lookup"><span data-stu-id="0812d-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="0812d-185">INSERT、DELETE、UPDATE などの*SQLstatement* (省略可能なパラメーターを使用) を実行し、影響を受けたレコードの数を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="0812d-186">最近挿入された行から ID 列を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="0812d-187">指定されたデータベースファイルまたは web.config ファイルの名前付き接続文字列を使用して指定されたデータベースを*開きます。*</span><span class="sxs-lookup"><span data-stu-id="0812d-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="0812d-188">接続文字列を使用してデータベースを開きます。</span><span class="sxs-lookup"><span data-stu-id="0812d-188">Opens a database using the connection string.</span></span> <span data-ttu-id="0812d-189">(これは、接続文字列名を使用する `Database.Open`とは対照的です)。</span><span class="sxs-lookup"><span data-stu-id="0812d-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="0812d-190">*SQLstatement* (必要に応じてパラメーターを渡す) を使用してデータベースにクエリを実行し、結果をコレクションとして返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="0812d-191">(省略可能なパラメーターを使用して) *SQLstatement*を実行し、1つのレコードを返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="0812d-192">(省略可能なパラメーターを使用して) *SQLstatement*を実行し、単一の値を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="0812d-193">ヘルパー</span><span class="sxs-lookup"><span data-stu-id="0812d-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="0812d-194">指定された ID の Google Analytics JavaScript コードをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="0812d-195">指定されたプロジェクトの StatCounter Analytics JavaScript コードをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="0812d-196">指定されたアカウントの Yahoo Analytics JavaScript コードをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="0812d-197">Bing に検索を渡します。</span><span class="sxs-lookup"><span data-stu-id="0812d-197">Passes a search to Bing.</span></span> <span data-ttu-id="0812d-198">検索するサイトと検索ボックスのタイトルを指定するには、`Bing.SiteUrl` と `Bing.SiteTitle` のプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="0812d-199">通常は、これらのプロパティを [ *\_該当*] ページで設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="0812d-200">グラフを初期化します。</span><span class="sxs-lookup"><span data-stu-id="0812d-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="0812d-201">グラフに凡例を追加します。</span><span class="sxs-lookup"><span data-stu-id="0812d-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="0812d-202">グラフに一連の値を追加します。</span><span class="sxs-lookup"><span data-stu-id="0812d-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="0812d-203">指定されたデータのハッシュを返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="0812d-204">既定のアルゴリズムは `sha256`です。</span><span class="sxs-lookup"><span data-stu-id="0812d-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="0812d-205">Facebook ユーザーがページに接続できるようにします。</span><span class="sxs-lookup"><span data-stu-id="0812d-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="0812d-206">ファイルをアップロードするための UI をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="0812d-207">指定された Xbox ゲーマータグをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="0812d-208">指定された電子メールアドレスの Gravatar イメージをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="0812d-209">データオブジェクトを JavaScript Object Notation (JSON) 形式の文字列に変換します。</span><span class="sxs-lookup"><span data-stu-id="0812d-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="0812d-210">JSON でエンコードされた入力文字列を、反復処理またはデータベースへの挿入が可能なデータオブジェクトに変換します。</span><span class="sxs-lookup"><span data-stu-id="0812d-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="0812d-211">指定されたタイトルと省略可能な URL を使用してソーシャルネットワークリンクを表示します。</span><span class="sxs-lookup"><span data-stu-id="0812d-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="0812d-212">エラーメッセージをフォームフィールドに関連付けます。</span><span class="sxs-lookup"><span data-stu-id="0812d-212">Associates an error message with a form field.</span></span> <span data-ttu-id="0812d-213">このメンバーにアクセスするには、`ModelState` ヘルパーを使用します。</span><span class="sxs-lookup"><span data-stu-id="0812d-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="0812d-214">エラーメッセージをフォームに関連付けます。</span><span class="sxs-lookup"><span data-stu-id="0812d-214">Associates an error message with a form.</span></span> <span data-ttu-id="0812d-215">このメンバーにアクセスするには、`ModelState` ヘルパーを使用します。</span><span class="sxs-lookup"><span data-stu-id="0812d-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="0812d-216">検証エラーがない場合は true を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="0812d-217">このメンバーにアクセスするには、`ModelState` ヘルパーを使用します。</span><span class="sxs-lookup"><span data-stu-id="0812d-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="0812d-218">オブジェクトおよび子オブジェクトのプロパティと値を表示します。</span><span class="sxs-lookup"><span data-stu-id="0812d-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="0812d-219">ReCAPTCHA 検証テストをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="0812d-220">ReCAPTCHA サービスの公開キーと秘密キーを設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="0812d-221">通常は、これらのプロパティを [ *\_該当*] ページで設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="0812d-222">ReCAPTCHA テストの結果を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="0812d-223">ASP.NET Web ページに関するステータス情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="0812d-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="0812d-224">指定されたユーザーの Twitter ストリームをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="0812d-225">指定された検索テキストの Twitter ストリームをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="0812d-226">指定したファイルに対して、オプションの幅と高さを指定して Flash video player をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="0812d-227">指定したファイルの Windows Media player を、オプションの幅と高さを使用して表示します。</span><span class="sxs-lookup"><span data-stu-id="0812d-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="0812d-228">指定*した .xap*ファイルの、必要な幅と高さを持つ Silverlight プレーヤーをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="0812d-229">*キー*で指定されたオブジェクトを返します。オブジェクトが見つからない場合は null を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="0812d-230">*キー*で指定されたオブジェクトをキャッシュから削除します。</span><span class="sxs-lookup"><span data-stu-id="0812d-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="0812d-231">*キー*で指定された名前でキャッシュに*値*を格納します。</span><span class="sxs-lookup"><span data-stu-id="0812d-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="0812d-232">クエリのデータを使用して、新しい `WebGrid` オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="0812d-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="0812d-233">HTML テーブルにデータを表示するためのマークアップをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="0812d-234">`WebGrid` オブジェクトのポケットベルを表示します。</span><span class="sxs-lookup"><span data-stu-id="0812d-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="0812d-235">指定されたパスからイメージを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="0812d-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="0812d-236">指定されたイメージをウォーターマークとして追加します。</span><span class="sxs-lookup"><span data-stu-id="0812d-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="0812d-237">指定したテキストをイメージに追加します。</span><span class="sxs-lookup"><span data-stu-id="0812d-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="0812d-238">画像を水平方向または垂直方向に反転します。</span><span class="sxs-lookup"><span data-stu-id="0812d-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="0812d-239">ファイルのアップロード中にイメージがページにポストされたときにイメージを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="0812d-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="0812d-240">イメージのサイズを変更します。</span><span class="sxs-lookup"><span data-stu-id="0812d-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="0812d-241">イメージを左または右に回転します。</span><span class="sxs-lookup"><span data-stu-id="0812d-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="0812d-242">指定したパスにイメージを保存します。</span><span class="sxs-lookup"><span data-stu-id="0812d-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="0812d-243">SMTP サーバーのパスワードを設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="0812d-244">通常、このプロパティは [ *\_該当*] ページで設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="0812d-245">電子メール メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="0812d-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="0812d-246">SMTP サーバー名を設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-246">Sets the SMTP server name.</span></span> <span data-ttu-id="0812d-247">通常、このプロパティは [ *\_該当*] ページで設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-247">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="0812d-248">SMTP サーバーのユーザー名を設定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="0812d-249">通常は、[ *\_該当*] ページでこのプロパティを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0812d-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="0812d-250">検証</span><span class="sxs-lookup"><span data-stu-id="0812d-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="0812d-251">v2指定したフィールドの検証エラーメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="0812d-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="0812d-252">v2すべての検証エラーの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="0812d-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="0812d-253">v2指定された種類の検証にユーザー入力要素を登録します。</span><span class="sxs-lookup"><span data-stu-id="0812d-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="0812d-254">v2検証エラーメッセージを書式設定できるように、クライアント側検証の CSS クラス属性を動的にレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="0812d-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="0812d-255">(適切なクライアントスクリプトライブラリを参照し、CSS クラスを定義する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="0812d-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="0812d-256">v2ユーザー入力フィールドに対してクライアント側の検証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="0812d-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="0812d-257">(適切なクライアントスクリプトライブラリを参照する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="0812d-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="0812d-258">v2検証のために registred されているすべてのユーザー入力要素に有効な値が含まれている場合に true を返します。</span><span class="sxs-lookup"><span data-stu-id="0812d-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="0812d-259">v2ユーザーがユーザー入力要素の値を指定する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="0812d-260">v2ユーザーが各ユーザー入力要素の値を指定する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="0812d-261">このメソッドでは、カスタムエラーメッセージを指定することはできません。</span><span class="sxs-lookup"><span data-stu-id="0812d-261">This method does not let you specify a custom error message.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

<span data-ttu-id="0812d-262">v2`Validation.Add` メソッドを使用する場合の検証テストを指定します。</span><span class="sxs-lookup"><span data-stu-id="0812d-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]

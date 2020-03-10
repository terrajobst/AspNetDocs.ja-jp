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
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET Web ページ (Razor) API クイックリファレンス

[Tom FitzMacken](https://github.com/tfitzmac)

> このページには、Razor 構文で ASP.NET Web ページをプログラミングするための最も一般的に使用されるオブジェクト、プロパティ、およびメソッドの簡単な例を含む一覧が含まれています。
> 
> "(V2)" でマークされた説明は ASP.NET Web ページバージョン2で導入されました。
> 
> API リファレンスドキュメントについては、MSDN の[ASP.NET Web ページリファレンスドキュメント](https://go.microsoft.com/fwlink/?LinkId=208659)を参照してください。
> 
> ## <a name="software-versions"></a>ソフトウェアのバージョン
> 
> 
> - ASP.NET Web ページ (Razor) 3
>   
> 
> このチュートリアルでは、ASP.NET Web ページ2および ASP.NET Web ページ 1.0 (v2 とマークされている機能を除く) でも動作します。

このページには、次の参照情報が含まれています。

- [クラス](#Classes)
- [データ](#Data)
- [支援](#Helpers)
- [検証](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>クラス

### `AppState[key], AppState[index],App`

アプリケーション内の任意のページで共有できるデータを格納します。 次の例のように、動的 `App` プロパティを使用して、同じデータにアクセスできます。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

文字列値をブール値 (true/false) に変換します。 False を返します。文字列が true または false を表さない場合は、指定された値を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

文字列値を日付/時刻に変換します。 文字列が日付/時刻を表していない場合は `DateTime.MinValue` または指定された値を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

文字列値を10進値に変換します。 文字列が10進数値を表していない場合は、0.0 または指定された値を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

文字列値を float に変換します。 文字列が10進数値を表していない場合は、0.0 または指定された値を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

文字列値を整数に変換します。 文字列が整数を表さない場合は、0または指定された値を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

省略可能な追加のパス部分を使用して、ローカルファイルパスからブラウザーと互換性のある URL を作成します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

HTML エンコードされた出力として表示するのではなく、*値*を html マークアップとしてレンダリングします。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

値を文字列から指定した型に変換できる場合は true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

オブジェクトまたは変数に値がない場合に true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

要求が POST の場合は true を返します。 (最初の要求は通常 GET です)。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

このページに適用するレイアウトページのパスを指定します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

現在の要求のページ、レイアウトページ、および部分ページ間で共有されるデータを格納します。 次の例のように、動的 `Page` プロパティを使用して、同じデータにアクセスできます。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(レイアウトページ)名前付きセクションに含まれていないコンテンツページのコンテンツをレンダリングします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

指定されたパスと省略可能な追加データを使用してコンテンツページを表示します。 余分なパラメーターの値は、位置 (例 1) またはキー (例 2) で `PageData` から取得できます。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(レイアウトページ)名前を持つコンテンツセクションをレンダリングします。 省略可能なセクションを作成するには、 *required*を false に設定します。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

HTTP クッキーの値を取得または設定します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

現在の要求でアップロードされたファイルを取得します。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

(文字列として) フォームにポストされたデータを取得します。 `Request[key]` は、`Request.Form` コレクションと `Request.QueryString` コレクションの両方をチェックします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

URL クエリ文字列で指定されたデータを取得します。 `Request[key]` は、`Request.Form` コレクションと `Request.QueryString` コレクションの両方をチェックします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

フォーム要素、クエリ文字列値、cookie、またはヘッダー値の要求の検証を選択的に無効にします。 要求の検証は既定で有効になっており、ユーザーがマークアップや危険な可能性のあるその他のコンテンツを投稿できないようにします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

HTTP サーバーヘッダーを応答に追加します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

指定された時間のページ出力をキャッシュします。 必要に応じて*スライディング*を設定して各ページのアクセスと*varyByParams*のタイムアウトをリセットし、ページ要求内の異なるクエリ文字列ごとに異なるバージョンのページをキャッシュします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

ブラウザー要求を新しい場所にリダイレクトします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

ブラウザーに送信される HTTP ステータスコードを設定します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

オプションの MIME の種類を使用して、*データ*の内容を応答に書き込みます。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

ファイルの内容を応答に書き込みます。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(レイアウトページ)名前を持つコンテンツセクションを定義します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

HTML エンコードされた文字列をデコードします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

HTML マークアップでの表示用に文字列をエンコードします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

指定された仮想パスのサーバー物理パスを返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

URL からテキストをデコードします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

URL に配置するためにテキストをエンコードします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

ユーザーがブラウザーを閉じるまで存在する値を取得または設定します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

オブジェクトの値の文字列形式を表示します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

URL から追加のデータを取得します (たとえば、 */MyPage/ExtraData*)。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

指定したユーザーのパスワードを変更します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

アカウント確認トークンを使用してアカウントを確認します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

指定されたユーザー名とパスワードを使用して、新しいユーザーアカウントを作成します。 確認トークンを要求するには、RequireConfirmationToken に true を渡し*ます。*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

現在ログインしているユーザーの整数識別子を取得します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

現在ログインしているユーザーの名前を取得します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

ユーザーがパスワードをリセットできるように、ユーザーに電子メールで送信できるパスワードリセットトークンを生成します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

ユーザー名からユーザー ID を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

現在のユーザーがログインしている場合は true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

ユーザーが確認されている場合 (確認メールなど)、true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

現在のユーザーの名前が指定されたユーザー名と一致する場合に true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

Cookie の認証トークンを設定して、にユーザーを記録します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

認証トークン cookie を削除してユーザーをログアウトします。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

ユーザーが認証されていない場合、HTTP ステータスを 401 (Unauthorized) に設定します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

現在のユーザーが指定されたいずれかのロールのメンバーでない場合は、HTTP ステータスを 401 (未承認) に設定します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

現在のユーザーがユーザー*名*で指定されたユーザーでない場合は、HTTP ステータスを 401 (未承認) に設定します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

パスワードリセットトークンが有効な場合、はユーザーのパスワードを新しいパスワードに変更します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>Data

### `Database.Execute(SQLstatement [,parameters]`

INSERT、DELETE、UPDATE などの*SQLstatement* (省略可能なパラメーターを使用) を実行し、影響を受けたレコードの数を返します。

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

最近挿入された行から ID 列を返します。

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

指定されたデータベースファイルまたは web.config ファイルの名前付き接続文字列を使用して指定されたデータベースを*開きます。*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

接続文字列を使用してデータベースを開きます。 (これは、接続文字列名を使用する `Database.Open`とは対照的です)。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

*SQLstatement* (必要に応じてパラメーターを渡す) を使用してデータベースにクエリを実行し、結果をコレクションとして返します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

(省略可能なパラメーターを使用して) *SQLstatement*を実行し、1つのレコードを返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

(省略可能なパラメーターを使用して) *SQLstatement*を実行し、単一の値を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>ヘルパー

### `Analytics.GetGoogleHtml(webPropertyId)`

指定された ID の Google Analytics JavaScript コードをレンダリングします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

指定されたプロジェクトの StatCounter Analytics JavaScript コードをレンダリングします。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

指定されたアカウントの Yahoo Analytics JavaScript コードをレンダリングします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

Bing に検索を渡します。 検索するサイトと検索ボックスのタイトルを指定するには、`Bing.SiteUrl` と `Bing.SiteTitle` のプロパティを設定します。 通常は、これらのプロパティを [ *\_該当*] ページで設定します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

グラフを初期化します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

グラフに凡例を追加します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

グラフに一連の値を追加します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

指定されたデータのハッシュを返します。 既定のアルゴリズムは `sha256`です。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Facebook ユーザーがページに接続できるようにします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

ファイルをアップロードするための UI をレンダリングします。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

指定された Xbox ゲーマータグをレンダリングします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

指定された電子メールアドレスの Gravatar イメージをレンダリングします。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

データオブジェクトを JavaScript Object Notation (JSON) 形式の文字列に変換します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

JSON でエンコードされた入力文字列を、反復処理またはデータベースへの挿入が可能なデータオブジェクトに変換します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

指定されたタイトルと省略可能な URL を使用してソーシャルネットワークリンクを表示します。

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

エラーメッセージをフォームフィールドに関連付けます。 このメンバーにアクセスするには、`ModelState` ヘルパーを使用します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

エラーメッセージをフォームに関連付けます。 このメンバーにアクセスするには、`ModelState` ヘルパーを使用します。

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

検証エラーがない場合は true を返します。 このメンバーにアクセスするには、`ModelState` ヘルパーを使用します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

オブジェクトおよび子オブジェクトのプロパティと値を表示します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

ReCAPTCHA 検証テストをレンダリングします。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

ReCAPTCHA サービスの公開キーと秘密キーを設定します。 通常は、これらのプロパティを [ *\_該当*] ページで設定します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

ReCAPTCHA テストの結果を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

ASP.NET Web ページに関するステータス情報を表示します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

指定されたユーザーの Twitter ストリームをレンダリングします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

指定された検索テキストの Twitter ストリームをレンダリングします。

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

指定したファイルに対して、オプションの幅と高さを指定して Flash video player をレンダリングします。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

指定したファイルの Windows Media player を、オプションの幅と高さを使用して表示します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

指定*した .xap*ファイルの、必要な幅と高さを持つ Silverlight プレーヤーをレンダリングします。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

*キー*で指定されたオブジェクトを返します。オブジェクトが見つからない場合は null を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

*キー*で指定されたオブジェクトをキャッシュから削除します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

*キー*で指定された名前でキャッシュに*値*を格納します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

クエリのデータを使用して、新しい `WebGrid` オブジェクトを作成します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

HTML テーブルにデータを表示するためのマークアップをレンダリングします。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

`WebGrid` オブジェクトのポケットベルを表示します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

指定されたパスからイメージを読み込みます。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

指定されたイメージをウォーターマークとして追加します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

指定したテキストをイメージに追加します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

画像を水平方向または垂直方向に反転します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

ファイルのアップロード中にイメージがページにポストされたときにイメージを読み込みます。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

イメージのサイズを変更します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

イメージを左または右に回転します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

指定したパスにイメージを保存します。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

SMTP サーバーのパスワードを設定します。 通常、このプロパティは [ *\_該当*] ページで設定します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

電子メール メッセージを送信します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

SMTP サーバー名を設定します。 通常、このプロパティは [ *\_該当*] ページで設定します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

SMTP サーバーのユーザー名を設定します。 通常は、[ *\_該当*] ページでこのプロパティを設定する必要があります。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>検証

### `Html.ValidationMessage(field)`

v2指定したフィールドの検証エラーメッセージを表示します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

v2すべての検証エラーの一覧を表示します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

v2指定された種類の検証にユーザー入力要素を登録します。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

v2検証エラーメッセージを書式設定できるように、クライアント側検証の CSS クラス属性を動的にレンダリングします。 (適切なクライアントスクリプトライブラリを参照し、CSS クラスを定義する必要があります)。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

v2ユーザー入力フィールドに対してクライアント側の検証を有効にします。 (適切なクライアントスクリプトライブラリを参照する必要があります)。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

v2検証のために registred されているすべてのユーザー入力要素に有効な値が含まれている場合に true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

v2ユーザーがユーザー入力要素の値を指定する必要があることを指定します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

v2ユーザーが各ユーザー入力要素の値を指定する必要があることを指定します。 このメソッドでは、カスタムエラーメッセージを指定することはできません。

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

v2`Validation.Add` メソッドを使用する場合の検証テストを指定します。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]

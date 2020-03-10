---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: ASP.NET AJAX 認証とプロファイルアプリケーションサービスについて |Microsoft Docs
author: scottcate
description: 認証サービスを使用すると、ユーザーは認証 cookie を受信するための資格情報を入力できます。また、カスタムユーザーを許可するゲートウェイサービスです...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: cab9acb1ffd75cca87f6c575a6abdd000235828e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520312"
---
# <a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a>ASP.NET AJAX 認証とプロファイル アプリケーション サービスについて理解する

[Scott Cate](https://github.com/scottcate)

[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> 認証サービスを使用すると、ユーザーは認証 cookie を受信するために資格情報を提供できます。また、ASP.NET によって提供されるカスタムユーザープロファイルを許可するゲートウェイサービスです。 ASP.NET AJAX 認証サービスの使用は標準の ASP.NET フォーム認証と互換性があるため、現在フォーム認証を使用しているアプリケーション (ログインコントロールなど) は AJAX 認証サービスにアップグレードしても破損しません。

## <a name="introduction"></a>はじめに

.NET Framework 3.5 の一部として、Microsoft は、さまざまな環境のアップグレードを提供しています。新しい開発環境が利用可能になるだけでなく、新しい統合言語クエリ (LINQ) 機能やその他の言語の機能強化が予定されています。 さらに、他のツールセットのいくつかの使い慣れた機能 (特に ASP.NET AJAX 拡張機能) は、基本クラスライブラリ .NET Framework のファーストクラスメンバーとして含まれています。 これらの拡張機能により、ページの完全な更新を必要としないページの部分的なレンダリング、クライアントスクリプト (ASP.NET プロファイリング API を含む) を使用した Web サービスへのアクセス機能、広範なクライアント側 API など、多くの豊富なクライアント機能が有効になります。ASP.NET のサーバー側コントロールセットで見られる多くのコントロールスキームをミラー化するように設計されています。

このホワイトペーパーでは、ASP.NET プロファイリングとフォーム認証サービスの実装と使用方法について考察しています。これらは Microsoft ASP.NET AJAX ExtensionsThe よって公開されており、AJAX 拡張機能によってフォーム認証が非常に簡単にサポートされるようになります (また、プロファイルサービス) は、Web サービスプロキシスクリプトを通じて公開されます。 AJAX 拡張は、AuthenticationServiceManager クラスを使用したカスタム認証もサポートしています。

このホワイトペーパーは、Visual Studio 2008 のベータ2リリースと .NET Framework 3.5 に基づいています。 また、このホワイトペーパーでは、visual Web Developer Express ではなく Visual Studio 2008 Beta 2 を使用することを前提としています。また、Visual Studio のユーザーインターフェイスに従ってチュートリアルを提供します。 一部のコードサンプルでは、Visual Web Developer Express で使用できないプロジェクトテンプレートを使用する場合があります。

## <a name="profiles-and-authentication"></a>*プロファイルと認証*

Microsoft ASP.NET のプロファイルと認証サービスは ASP.NET Forms 認証システムによって提供され、ASP.NET の標準コンポーネントです。 ASP.NET AJAX 拡張機能は、クライアント AJAX ライブラリの Sys. Services 名前空間の下にある非常に単純なモデルを使用して、これらのサービスへのスクリプトアクセスをスクリプトプロキシを介して提供します。

認証サービスを使用すると、ユーザーは認証 cookie を受信するために資格情報を提供できます。また、ASP.NET によって提供されるカスタムユーザープロファイルを許可するゲートウェイサービスです。 ASP.NET AJAX 認証サービスの使用は標準の ASP.NET フォーム認証と互換性があるため、現在フォーム認証を使用しているアプリケーション (ログインコントロールなど) は AJAX 認証サービスにアップグレードしても破損しません。

プロファイルサービスを使用すると、認証サービスによって提供されるメンバーシップに基づいて、ユーザーデータを自動統合および格納できます。 格納されているデータは web.config ファイルによって指定され、さまざまなプロファイリングサービスプロバイダーがデータ管理を処理します。 認証サービスと同様に、AJAX プロファイルサービスは標準の ASP.NET profile service と互換性があるため、ASP.NET Profile service の機能が現在組み込まれているページは、AJAX サポートを含むことによって破損しないようにする必要があります。

ASP.NET 認証とプロファイルサービスをアプリケーションに組み込むことは、このホワイトペーパーの範囲外です。 トピックの詳細については、MSDN ライブラリリファレンス記事「 [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx)でメンバーシップを使用してユーザーを管理する」を参照してください。 また、ASP.NET には、ASP.NET メンバーシップの既定の認証サービスプロバイダーである SQL Server のメンバーシップを自動的に設定するユーティリティも含まれています。 詳細については、 [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)の「ASP.NET SQL Server Registration Tool (Aspnet\_regsql)」を参照してください。

## <a name="using-the-aspnet-ajax-authentication-service"></a>*ASP.NET AJAX 認証サービスの使用*

Web.config ファイルで ASP.NET AJAX Authentication service が有効になっている必要があります。

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

認証サービスでは、ASP.NET フォーム認証を有効にし、クライアントブラウザーでクッキーを有効にする必要があります (クッキーレスセッションでは URL パラメーターが必要であるため、スクリプトでクッキーレスセッションを有効にすることはできません)。

AJAX 認証サービスが有効化され、構成されると、クライアントスクリプトはすぐに AuthenticationService オブジェクトを利用できます。 主に、クライアントスクリプトは、`login` メソッドと `isLoggedIn` プロパティを利用します。 Login メソッドの既定値を提供するいくつかのプロパティが用意されています。これは、多数のパラメーターを受け取ることができます。

*AuthenticationService のメンバー*

*ログイン方法:*

Login () メソッドは、ユーザーの資格情報の認証要求を開始します。 このメソッドは非同期であり、実行をブロックしません。

*パラメーター:*

| **パラメーター名** | **意味** |
| --- | --- |
| userName | 必須。 認証するユーザー名。 |
| パスワード | 省略可能 (既定値は null)。 ユーザーのパスワード。 |
| isPersistent | 省略可能 (既定値は false)。 ユーザーの認証クッキーをセッション間で保持する必要があるかどうか。 False の場合、ブラウザーが終了したとき、またはセッションの有効期限が切れたときに、ユーザーがログアウトします。 |
| redirectUrl | 省略可能 (既定値は null)。認証が成功したときにブラウザーをリダイレクトする URL。 このパラメーターが null または空の文字列の場合、リダイレクトは実行されません。 |
| customInfo | 省略可能 (既定値は null)。 このパラメーターは現在使用されていないため、将来使用するために予約されています。 |
| loginCompletedCallback | 省略可能 (既定値は null)。ログインが正常に完了したときに呼び出す関数。 指定した場合、このパラメーターは defaultLoginCompleted プロパティよりも優先されます。 |
| failedCallback | 省略可能 (既定値は null)。ログインが失敗したときに呼び出す関数。 指定した場合、このパラメーターは Defaultの Callback プロパティよりも優先されます。 |
| userContext | 省略可能 (既定値は null)。 コールバック関数に渡される必要があるカスタムユーザーコンテキストデータ。 |

*戻り値:*

この関数には、戻り値は含まれません。 ただし、この関数の呼び出しの完了時には、いくつかの動作が含まれます。

- `redirectUrl` パラメーターが null でも空の文字列でもない場合、現在のページは更新されるか、または変更されます。
- ただし、パラメーターが null または空の文字列の場合は、`loginCompletedCallback` パラメーター、または `defaultLoginCompletedCallback` プロパティが呼び出されます。
- Web サービスへの呼び出しが失敗した場合、`defaultFailedCallback` プロパティの `failedCallback` パラメーターが呼び出されます。

*logout メソッド:*

Logout () メソッドは、資格情報の cookie を削除し、web アプリケーションから現在のユーザーをログアウトします。

*パラメーター:*

| **パラメーター名** | **意味** |
| --- | --- |
| redirectUrl | 省略可能 (既定値は null)。認証が成功したときにブラウザーをリダイレクトする URL。 このパラメーターが null または空の文字列の場合、リダイレクトは実行されません。 |
| logoutCompletedCallback | 省略可能 (既定値は null)。ログアウトが正常に完了したときに呼び出す関数。 指定した場合、このパラメーターは defaultLogoutCompleted プロパティよりも優先されます。 |
| failedCallback | 省略可能 (既定値は null)。ログインが失敗したときに呼び出す関数。 指定した場合、このパラメーターは Defaultの Callback プロパティよりも優先されます。 |
| userContext | 省略可能 (既定値は null)。 コールバック関数に渡される必要があるカスタムユーザーコンテキストデータ。 |

*戻り値:*

この関数には、戻り値は含まれません。 ただし、この関数の呼び出しの完了時には、いくつかの動作が含まれます。

- `redirectUrl` パラメーターが null でも空の文字列でもない場合、現在のページは更新されるか、または変更されます。
- ただし、パラメーターが null または空の文字列の場合は、`logoutCompletedCallback` パラメーター、または `defaultLogoutCompletedCallback` プロパティが呼び出されます。
- Web サービスへの呼び出しが失敗した場合、`defaultFailedCallback` プロパティの `failedCallback` パラメーターが呼び出されます。

*Default失敗コールバックプロパティ (get、set):*

このプロパティは、web サービスとの通信エラーが発生した場合に呼び出される必要がある関数を指定します。 デリゲート (または関数参照) を受け取る必要があります。

このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

*パラメーター:*

| **パラメーター名** | **意味** |
| --- | --- |
| error | エラー情報を指定します。 |
| userContext | Login または logout 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。 |
| methodName | 呼び出し元のメソッドの名前。 |

*defaultLoginCompletedCallback プロパティ (get、set):*

このプロパティは、ログイン web サービスの呼び出しが完了したときに呼び出される必要がある関数を指定します。 デリゲート (または関数参照) を受け取る必要があります。

このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

*パラメーター:*

| **パラメーター名** | **意味** |
| --- | --- |
| validCredentials | ユーザーが有効な資格情報を指定したかどうかを指定します。 ユーザーが正常にログインした場合は `true`。それ以外の場合は `false`。 |
| userContext | Login 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。 |
| methodName | 呼び出し元のメソッドの名前。 |

*defaultLogoutCompletedCallback プロパティ (get、set):*

このプロパティは、ログアウト web サービスの呼び出しが完了したときに呼び出される必要がある関数を指定します。 デリゲート (または関数参照) を受け取る必要があります。

このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

*パラメーター:*

| **パラメーター名** | **意味** |
| --- | --- |
| 結果 | このパラメーターは常に `null`になります。将来使用するために予約されています。 |
| userContext | Login 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。 |
| methodName | 呼び出し元のメソッドの名前。 |

*isLoggedIn プロパティ (get):*

このプロパティは、ユーザーの現在の認証状態を取得します。これは、ページ要求中に ScriptManager オブジェクトによって設定されます。

このプロパティは、ユーザーが現在ログインしている場合に `true` を返します。それ以外の場合は `false`を返します。

*path プロパティ (get、set):*

このプロパティは、認証 web サービスの場所をプログラムによって決定します。 既定の認証プロバイダー、および ScriptManager コントロールの AuthenticationService 子ノードの Path プロパティで宣言によって宣言された1つのセットをオーバーライドするために使用できます (詳細については、「カスタム認証サービスプロバイダーの使用」を参照してください)。次のトピックを参照してください。

既定の認証サービスの場所は変更されないことに注意してください。 ただし、ASP.NET AJAX では、ASP.NET AJAX authentication service プロキシと同じクラスインターフェイスを提供する web サービスの場所を指定できます。

また、このプロパティは、現在のサイトからスクリプト要求を送信する値に設定しないでください。 現在のアプリケーションは認証資格情報を受信しないため、役に立ちません。また、AJAX の基盤となるテクノロジは、クロスサイト要求を送信しないようにする必要があります。また、クライアントブラウザーでセキュリティ例外が発生する可能性があります。

このプロパティは、認証 web サービスへのパスを表す `String` オブジェクトです。

*timeout プロパティ (get、set):*

このプロパティは、ログイン要求が失敗したことを前提として、認証サービスを待機する時間の長さを決定します。 の呼び出しが完了するのを待機している間にタイムアウトが経過した場合、要求が失敗したコールバックが呼び出され、呼び出しは完了しません。

このプロパティは、認証サービスからの結果を待機するミリ秒数を表す `Number` オブジェクトです。

*コードサンプル: 認証サービスへのログイン*

次のマークアップは、AuthenticationService クラスの login メソッドと logout メソッドへの単純なスクリプト呼び出しを含む ASP.NET ページの例です。

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a>AJAX を使用した ASP.NET プロファイルデータへのアクセス

ASP.NET プロファイリングサービスも ASP.NET AJAX 拡張機能を介して公開されます。 ASP.NET プロファイルサービスは、ユーザーデータを格納および取得するための豊富で詳細な API を提供しているため、これは優れた生産性向上ツールになります。

Web.config でプロファイルサービスが有効になっている必要があります。既定ではありません。 これを行うには、`profileService` の子要素が web.config で指定されていることを確認し、次のように読み取りまたは書き込みが可能なプロパティを指定します。

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

プロファイルサービスも構成する必要があります。 プロファイルサービスの構成はこのホワイトペーパーの範囲外ですが、プロファイル構成設定で定義されているグループは、グループ名のサブプロパティとしてアクセスできることに注意してください。 たとえば、次のプロファイルセクションが指定されているとします。

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

クライアントスクリプトは、ProfileService クラスの properties フィールドのプロパティとして、Name、address... Line2、address. City、address. 市区町村、および BackgroundColor にアクセスできるようになります。

AJAX プロファイルサービスが構成されると、ページですぐに使用できるようになります。ただし、使用する前に1回読み込む必要があります。

*サービスのメンバー*

*プロパティフィールド:*

プロパティフィールドは、構成されているすべてのプロファイルデータを、ドット演算子名の規則で参照できる子プロパティとして公開します。 プロパティグループの子であるプロパティは、GroupName. PropertyName と呼ばれます。 上記のプロファイル構成の例では、ユーザーの状態を取得するために、次の識別子を使用できます。

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

*load メソッド:*

サーバーから選択された一覧またはすべてのプロパティを読み込みます。

*パラメーター:*

| **パラメーター名** | **意味** |
| --- | --- |
| propertyNames | 省略可能 (既定値は null)。 サーバーから読み込まれるプロパティ。 |
| loadCompletedCallback | 省略可能 (既定値は null)。 読み込みが完了したときに呼び出す関数。 |
| failedCallback | 省略可能 (既定値は null)。 エラーが発生した場合に呼び出される関数。 |
| userContext | 省略可能 (既定値は null)。 コールバック関数に渡されるコンテキスト情報。 |

Load 関数に戻り値がありません。 呼び出しが正常に完了した場合は、`loadCompletedCallback` パラメーターまたは `defaultLoadCompletedCallback` のいずれかのプロパティが呼び出されます。 呼び出しが失敗した場合、またはタイムアウトが経過した場合は、`failedCallback` パラメーターまたは `defaultFailedCallback` プロパティのいずれかが呼び出されます。

`propertyNames` パラメーターが指定されていない場合は、読み取りが構成されているすべてのプロパティがサーバーから取得されます。

*メソッドの保存:*

Save () メソッドは、指定されたプロパティリスト (またはすべてのプロパティ) をユーザーの ASP.NET プロファイルに保存します。

*パラメーター:*

| **パラメーター名** | **意味** |
| --- | --- |
| propertyNames | 省略可能 (既定値は null)。 サーバーに保存するプロパティです。 |
| saveCompletedCallback | 省略可能 (既定値は null)。 保存が完了したときに呼び出す関数。 |
| failedCallback | 省略可能 (既定値は null)。 エラーが発生した場合に呼び出される関数。 |
| userContext | 省略可能 (既定値は null)。 コールバック関数に渡されるコンテキスト情報。 |

Save 関数に戻り値がありません。 呼び出しが正常に完了した場合は、`saveCompletedCallback` パラメーターまたは `defaultSaveCompletedCallback` のいずれかのプロパティが呼び出されます。 呼び出しが失敗した場合、またはタイムアウトが経過した場合は、`failedCallback` または `defaultFailedCallback` のいずれかのプロパティが呼び出されます。

`propertyNames` パラメーターが null の場合は、すべてのプロファイルプロパティがサーバーに送信され、サーバーは保存できるプロパティと実行できないプロパティを決定します。

*Default失敗コールバックプロパティ (get、set):*

このプロパティは、web サービスとの通信エラーが発生した場合に呼び出される必要がある関数を指定します。 デリゲート (または関数参照) を受け取る必要があります。

このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

*パラメーター:*

| **パラメーター名** | **意味** |
| --- | --- |
| エラー | エラー情報を指定します。 |
| userContext | Load または save 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。 |
| methodName | 呼び出し元のメソッドの名前。 |

*defaultSaveCompleted プロパティ (get、set):*

このプロパティは、ユーザーのプロファイルデータの保存が完了したときに呼び出す必要がある関数を指定します。 デリゲート (または関数参照) を受け取る必要があります。

このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

*パラメーター:*

| **パラメーター名** | **意味** |
| --- | --- |
| numPropsSaved | 保存されたプロパティの数を指定します。 |
| userContext | Load または save 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。 |
| methodName | 呼び出し元のメソッドの名前。 |

*defaultLoadCompleted プロパティ (get、set):*

このプロパティは、ユーザーのプロファイルデータの読み込みが完了したときに呼び出す必要がある関数を指定します。 デリゲート (または関数参照) を受け取る必要があります。

このプロパティで指定される関数参照は、次のシグネチャを持つ必要があります。

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

*パラメーター:*

| **パラメーター名** | **意味** |
| --- | --- |
| numPropsLoaded | 読み込まれるプロパティの数を指定します。 |
| userContext | Load または save 関数が呼び出されたときに指定されたユーザーコンテキスト情報を指定します。 |
| methodName | 呼び出し元のメソッドの名前。 |

*path プロパティ (get、set):*

このプロパティは、プロファイル web サービスの場所をプログラムによって決定します。 これを使用すると、ScriptManager コントロールの ProfileService 子ノードの Path プロパティで宣言された1つの設定だけでなく、既定のプロファイルサービスプロバイダーをオーバーライドできます。

既定のプロファイルサービスの場所は変更されないことに注意してください。 ただし、ASP.NET AJAX では、ASP.NET AJAX authentication service プロキシと同じクラスインターフェイスを提供する web サービスの場所を指定できます。

また、このプロパティは、現在のサイトからスクリプト要求を送信する値に設定しないでください。 AJAX の基盤となるテクノロジは、クロスサイト要求を送信しないでください。クライアントブラウザーでセキュリティ例外が発生する可能性があります。

このプロパティは、プロファイル web サービスへのパスを表す `String` オブジェクトです。

*timeout プロパティ (get、set):*

このプロパティは、読み込み要求または保存要求が失敗したことを前提として、プロファイルサービスを待機する時間を指定します。 の呼び出しが完了するのを待機している間にタイムアウトが経過した場合、要求が失敗したコールバックが呼び出され、呼び出しは完了しません。

このプロパティは、プロファイルサービスからの結果を待機するミリ秒数を表す `Number` オブジェクトです。

*コードサンプル: ページ読み込み時のプロファイルデータの読み込み*

次のコードは、ユーザーが認証されているかどうかを確認し、存在する場合は、ユーザーの適切な背景色をページのとして読み込みます。

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a>*カスタム認証サービスプロバイダーの使用*

ASP.NET AJAX 拡張機能を使用すると、カスタム web サービスを使用して機能を公開することにより、カスタムスクリプト認証サービスプロバイダーを作成できます。 使用するには、web サービスが2つのメソッド、`Login` と `Logout`を公開する必要があります。これらのメソッドは、既定の ASP.NET AJAX 認証 web サービスと同じメソッドシグネチャを使用して指定する必要があります。

カスタム web サービスを作成したら、そのサービスへのパスを指定する必要があります。これは、ページで宣言されているか、コード内でプログラムによって実行されるか、クライアントスクリプトを使用して行います。

*パスを宣言によって設定するには*

パスを宣言によって設定するには、ScriptManager オブジェクトの AuthenticationService 子を ASP.NET ページに追加します。

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

*コードでパスを設定するには、次のようにします。*

プログラムによってパスを設定するには、スクリプトマネージャーのインスタンスを使用してパスを指定します。

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

*スクリプトでパスを設定するには、次のようにします。*

スクリプトでパスをプログラムで設定するには、AuthenticationService クラスの `path` プロパティを使用します。

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

*カスタム認証用のサンプル Web サービス*

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a>まとめ

ASP.NET services-特に、プロファイル、メンバーシップ、および認証サービスは、クライアントブラウザーで JavaScript に簡単に公開されます。 これにより、開発者はクライアント側のコードを認証メカニズムとシームレスに統合できます。これにより、UpdatePanels などのコントロールに依存せずに、大量の処理を行うことができます。 Web 構成設定を利用することで、プロファイルデータをクライアントからも保護できます。既定ではデータは使用できず、開発者はプロファイルプロパティをオプトインする必要があります。

さらに、同等のメソッドシグネチャを使用して簡略化された web サービス実装を作成することにより、開発者は、これらの組み込み ASP.NET サービス用のカスタムスクリプトプロバイダーを作成できます。 これらの手法をサポートすることで、豊富なクライアントアプリケーションの開発が簡素化され、開発者は特定のニーズに合わせて幅広い柔軟性を得ることができます。

## <a name="bio"></a>*略歴*

Scott Cate は1997以来 Microsoft の Web テクノロジを使用しています。また、myKB.com ([www.myKB.com](http://www.myKB.com)) の大統領で、サポート技術情報のソフトウェアソリューションに重点を置いた ASP.NET ベースのアプリケーションを作成することを専門としています。 Scott は、 [scott.cate@myKB.com](mailto:scott.cate@myKB.com)または彼のブログ ( [ScottCate.com](http://ScottCate.com) ) で、電子メールで連絡を受けることができます。

> [!div class="step-by-step"]
> [前へ](understanding-asp-net-ajax-updatepanel-triggers.md)
> [次へ](understanding-asp-net-ajax-localization.md)

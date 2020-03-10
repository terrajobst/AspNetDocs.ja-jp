---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 認証と承認を使用してアプリケーションをセキュリティで保護する |Microsoft Docs
author: microsoft
description: 手順 9. では、ユーザーが登録してサイトにログインして、作成する必要があるように、このアプリケーションをセキュリティで保護するための認証と承認を追加する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8d509c5f15bb4d5014e53b8dc2a736454238e72c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486424"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>認証と承認を利用した安全なアプリケーション

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法を説明する、無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順9です。
> 
> 手順 9. では、ユーザーが登録してサイトにログインして新しいディナーを作成する必要があり、ディナーをホストしているユーザーのみが後で編集できるようにするために、認証と承認を追加して、そのアプリケーションをセキュリティで保護する方法を示します。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-9-authentication-and-authorization"></a>ステップ 9: 認証と承認

現在、このアプリケーションでは、サイトにアクセスするすべてのユーザーに、ディナーの詳細を作成および編集する権限を付与しています。 これを変更して、新しいディナーを作成するためにユーザーがサイトに登録してログインする必要があるようにして、ディナーをホストしているユーザーのみが後で編集できるように制限を追加してみましょう。

これを有効にするには、アプリケーションをセキュリティで保護するために認証と承認を使用します。

### <a name="understanding-authentication-and-authorization"></a>認証と承認について

*認証*は、アプリケーションにアクセスするクライアントの id を識別および検証するプロセスです。 もっと簡単に説明すると、エンドユーザーが web サイトにアクセスしたときの "だれ" を特定することになります。 ASP.NET は、ブラウザーユーザーを認証するための複数の方法をサポートしています。 インターネット web アプリケーションの場合、使用される最も一般的な認証方法は "フォーム認証" と呼ばれます。 フォーム認証を使用すると、開発者はアプリケーション内に HTML ログインフォームを作成し、エンドユーザーがデータベースまたは他のパスワード資格情報ストアに対して送信したユーザー名とパスワードを検証できます。 ユーザー名とパスワードの組み合わせが正しい場合、開発者は、今後の要求でユーザーを識別するために、暗号化された HTTP クッキーを発行するように ASP.NET に要求できます。 フォーム認証を使用して、このアプリケーションを使用します。

*承認*とは、認証されたユーザーが特定の URL またはリソースにアクセスする権限を持っているか、何らかのアクションを実行する権限を持っているかどうかを判断するプロセスです。 たとえば、世界中のアプリケーションでは、ログインしているユーザーのみが */Dins/create* URL にアクセスでき、新しいディナーを作成できることを承認する必要があります。 また、ディナーをホストしているユーザーのみが編集できるように承認ロジックを追加し、他のすべてのユーザーへの編集アクセスを拒否します。

### <a name="forms-authentication-and-the-accountcontroller"></a>フォーム認証と AccountController

新しい ASP.NET MVC アプリケーションが作成されると、ASP.NET MVC の既定の Visual Studio プロジェクトテンプレートによってフォーム認証が自動的に有効になります。 また、事前に構築されたアカウントログインページの実装がプロジェクトに自動的に追加されるため、サイト内でのセキュリティの統合が非常に簡単になります。

既定のサイトのマスターページでは、アクセスしているユーザーが認証されていない場合に、サイトの右上に [ログオン] リンクが表示されます。

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

[ログオン] リンクをクリックすると、ユーザーは */アカウントのログオン*URL に移動します。

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

登録されていない訪問者は、"Register" リンクをクリックすることによってこれを行うことができます。これにより、/アカウント/*レジスタ*の URL に移動し、アカウントの詳細を入力できます。

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

[Register] \ (登録 \) ボタンをクリックすると、ASP.NET メンバーシップシステム内に新しいユーザーが作成され、フォーム認証を使用してユーザーがサイトで認証されます。

ユーザーがログインすると、ページの右上にある "Welcome [username]!" を出力するように変更されます。 メッセージを表示し、"ログオン" ではなく "ログオフ" リンクを表示します。 [ログオフ] リンクをクリックすると、ユーザーがログアウトします。

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

上記のログイン、ログアウト、および登録機能は、プロジェクトの作成時に Visual Studio によってプロジェクトに追加された AccountController クラス内に実装されます。 AccountController の UI は、\Views\Account ディレクトリ内のビューテンプレートを使用して実装されます。

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

AccountController クラスは、暗号化された認証 cookie を発行するために ASP.NET Forms 認証システムを使用し、ユーザー名/パスワードを格納して検証するために ASP.NET Membership API を使用します。 ASP.NET Membership API は拡張可能であり、任意のパスワード資格情報ストアを使用できます。 ASP.NET には、SQL データベース内、または Active Directory 内にユーザー名とパスワードを格納する、組み込みのメンバーシッププロバイダーの実装が付属しています。

ここでは、プロジェクトのルートにある "web.config" ファイルを開き、その中の &lt;メンバーシップ&gt; セクションを検索することで、このアプリケーションで使用する必要があるメンバーシッププロバイダーを構成できます。 プロジェクトの作成時に追加された既定の web.config は、SQL メンバーシッププロバイダーを登録し、データベースの場所を指定するために "ApplicationServices" という接続文字列を使用するように構成します。

Web.config ファイルの &lt;connectionStrings&gt; セクション内で指定されている既定の "ApplicationServices" 接続文字列は、SQL Express を使用するように構成されています。 "ASPNETDB.MDF" という名前の SQL Express データベースを指します。MDF "アプリケーションの" App\_Data "ディレクトリにあります。 アプリケーション内でメンバーシップ API を初めて使用するときに、このデータベースが存在しない場合、ASP.NET は自動的にデータベースを作成し、その中に適切なメンバーシップデータベーススキーマをプロビジョニングします。

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

SQL Express を使用する代わりに、完全な SQL Server インスタンス (またはリモートデータベースへの接続) を使用する場合は、web.config ファイル内の "ApplicationServices" 接続文字列を更新して、適切なメンバーシップスキーマを確認するだけで済みます。は、が指すデータベースに追加されています。 \Windows\Microsoft.NET\Framework\v2.0.50727\ ディレクトリ内で "aspnet\_regsql .exe" ユーティリティを実行すると、メンバーシップとその他の ASP.NET アプリケーションサービスに適したスキーマをデータベースに追加できます。

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>[承認] フィルターを使用して、/Dins/create URL を承認しています

セキュリティで保護された認証とアカウント管理の実装を、このアプリケーションに対して有効にするためのコードを作成する必要はありませんでした。 ユーザーは、アプリケーションに新しいアカウントを登録し、サイトのログイン/ログアウトを行うことができます。

これで、承認ロジックをアプリケーションに追加し、訪問者の認証状態とユーザー名を使用して、サイト内で実行できることとできないことを制御できます。 最初に、Dinのコントローラークラスの "作成" アクションメソッドに承認ロジックを追加します。 具体的には、 */dinurl*にアクセスするユーザーがログインしている必要があります。 ログインしていない場合は、ログインページにリダイレクトして、サインインできるようにします。

このロジックの実装は非常に簡単です。 必要なのは、次のように、Create アクションメソッドに [承認] フィルター属性を追加することだけです。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC では、アクションメソッドに宣言的に適用できる再利用可能なロジックを実装するために使用できる "アクションフィルター" を作成する機能がサポートされています。 [承認] フィルターは、ASP.NET MVC によって提供される組み込みアクションフィルターの1つであり、開発者は、アクションメソッドとコントローラークラスに承認規則を宣言によって適用できます。

パラメーターを指定せずに適用した場合 (上記のように)、[承認] フィルターによって、アクションメソッド要求を行うユーザーがログインする必要があることが強制されます。そうでない場合は、ブラウザーがログイン URL に自動的にリダイレクトされます。 このリダイレクトを実行すると、最初に要求された URL が querystring 引数として渡されます (例:/Account/LogOn)。ReturnUrl =% 2fDinners% 2fCreate)。 その後、ユーザーがログインすると、AccountController は最初に要求された URL にリダイレクトします。

[承認] フィルターでは、必要に応じて、ユーザーがログインしていること、許可されているユーザーの一覧、または許可されているセキュリティロールのメンバーであることを要求するために使用できる "ユーザー" プロパティまたは "ロール" プロパティを指定する機能がサポートされています。 たとえば、次のコードでは、"scottgu" と "billg" という2つの特定のユーザーのみが、/Dins/create URL にアクセスできます。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

コード内に特定のユーザー名を埋め込むことは、それによって保守が容易になる傾向があります。 より適切な方法は、コードがチェックする上位レベルの "ロール" を定義し、データベースまたは active directory システムを使用してユーザーをロールにマップすることです (実際のユーザーマッピングリストをコードから外部に格納できるようにします)。 ASP.NET には、組み込みのロール管理 API だけでなく、組み込みのロールプロバイダーのセット (SQL および Active Directory 用のロールプロバイダーを含む) が含まれており、このユーザー/ロールマッピングを実行するのに役立ちます。 次に、特定の "管理者" ロール内のユーザーのみが/Dins/create URL にアクセスできるようにコードを更新できます。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>ディナーを作成するときに User.Identity.Name プロパティを使用する

コントローラーの基本クラスで公開されている User.Identity.Name プロパティを使用して、要求の現在ログインしているユーザーのユーザー名を取得できます。

前に、Create () アクションメソッドの HTTP POST バージョンを実装したので、ディナーの "HostedBy" プロパティを静的文字列にハードコーディングしました。 次に、User.Identity.Name プロパティを使用するようにこのコードを更新できるようになりました。また、ディナーを作成したホストの RSVP を自動的に追加することもできます。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

Create () メソッドに [承認] 属性を追加したので、ASP.NET MVC では、ユーザーがサイトにログインしている場合にのみ、アクションメソッドが実行されるようにしています。 そのため、User.Identity.Name プロパティの値には、常に有効なユーザー名が含まれます。

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>ディナーを編集するときに User.Identity.Name プロパティを使用する

ここで、ユーザー自身がホストしているディナーのプロパティのみを編集できるように、ユーザーを制限する認証ロジックを追加してみましょう。

この問題を解決するには、まず、先ほど作成した Dinner.cs 部分クラス内で、ディナーオブジェクトに "IsHostedBy (username)" ヘルパーメソッドを追加します。 このヘルパーメソッドは、指定されたユーザー名がディナー HostedBy プロパティに一致するかどうかに応じて true または false を返し、大文字と小文字を区別しない文字列比較を実行するために必要なロジックをカプセル化します。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

次に、Dinの Scontroller クラス内の Edit () アクションメソッドに [承認] 属性を追加します。 これにより、ユーザーは、// *//[id]* の URL を要求するようにログインする必要があります。

次に、IsHostedBy (username) ヘルパーメソッドを使用して、ログインしているユーザーがディナーホストと一致することを確認するコードを Edit メソッドに追加できます。 ユーザーがホストでない場合は、"InvalidOwner" ビューを表示し、要求を終了します。 このコードは次のようになります。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

次に、\Views\Dinners ディレクトリを右クリックし、[&gt;ビューの追加] メニューコマンドを選択して、新しい "InvalidOwner" ビューを作成します。 これには、次のエラーメッセージが表示されます。

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

これで、ユーザーが所有していないディナーを編集しようとすると、次のエラーメッセージが表示されます。

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

コントローラー内の Delete () アクションメソッドに対しても同じ手順を繰り返して、ディナーを削除するためのアクセス許可をロックダウンし、ディナーのホストだけが削除できるようにします。

### <a name="showinghiding-edit-and-delete-links"></a>編集と削除のリンクの表示/非表示

この記事では、次のように、[詳細 URL] から Dinの Scontroller クラスの編集および削除アクションメソッドにリンクしています。

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

現時点では、詳細 URL の訪問者がディナーのホストであるかどうかに関係なく、[編集] および [削除] アクションリンクが表示されています。 これを変更して、訪問しているユーザーがディナーの所有者である場合にのみリンクが表示されるようにしましょう。

Dinでの Details () アクションメソッドは、ディナーオブジェクトを取得し、それをモデルオブジェクトとしてビューテンプレートに渡します。

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

次のような IsHostedBy () ヘルパーメソッドを使用して、ビューテンプレートを更新して、条件に応じて編集と削除のリンクを表示/非表示にすることができます。

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>次の手順

ここで、AJAX を使用して、認証されたユーザーをディナーの RSVP に対して有効にする方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](implement-efficient-data-paging.md)
> [次へ](use-ajax-to-deliver-dynamic-updates.md)

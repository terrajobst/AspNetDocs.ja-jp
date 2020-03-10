---
uid: single-page-application/overview/templates/backbonejs-template
title: バックボーンテンプレート |Microsoft Docs
author: madskristensen
description: バックボーンの js SPA テンプレート
ms.author: riande
ms.date: 04/04/2013
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 7297db7d5b35a53b40f9d9162960e529a167bd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449776"
---
# <a name="backbone-template"></a>Backbone テンプレート

[Mads Kristensen](https://github.com/madskristensen)

> バックボーン SPA テンプレートは Kazi Manzur Rashid によって書き込まれました
> 
> [バックボーンの node.js SPA テンプレートをダウンロードする](https://go.microsoft.com/fwlink/?LinkId=293631)

このような場合は[、バックボーンを使用し](http://backbonejs.org/)て、対話型のクライアント側 web アプリを簡単に構築できるように設計されています。

このテンプレートは、ASP.NET MVC でのバックボーンアプリケーション開発の初期スケルトンを提供します。 既定では、ユーザーのサインアップ、サインイン、パスワードのリセット、基本的な電子メールテンプレートを使用したユーザーの確認など、基本的なユーザーログイン機能が提供されています。

要件:

- [ASP.NET and Web Tools 2012.2 更新プログラム](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a>バックボーンテンプレートプロジェクトを作成する

上の [ダウンロード] ボタンをクリックして、テンプレートをダウンロードしてインストールします。 このテンプレートは、Visual Studio 拡張機能 (VSIX) ファイルとしてパッケージ化されています。 場合によっては、Visual Studio を再起動する必要があります。

**[テンプレート]** ペインで、 **[インストールされたテンプレート]** を選択し、  **C#ビジュアル**ノードを展開します。 **[ビジュアルC# ]** で **[Web]** を選択します。 プロジェクトテンプレートの一覧で、 **[ASP.NET MVC 4 Web アプリケーション]** を選択します。 プロジェクト名を指定して、 **[OK]** をクリックします。

![](backbonejs-template/_static/image1.png)

**新しいプロジェクト**ウィザードで、[バックボーン SPA プロジェクト] を選択します。

![](backbonejs-template/_static/image2.png)

Ctrl キーを押しながら F5 キーを押してアプリケーションをビルドし、デバッグせずに実行するか、F5 キーを押してデバッグを実行します。

![](backbonejs-template/_static/image3.png)

[アカウント] をクリックすると、ログインページが表示されます。

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a>チュートリアル: クライアントコード

では、クライアント側から始めましょう。 クライアントアプリケーションスクリプトは、~/Scripts/application フォルダーにあります。 アプリケーションは、JavaScript (.js ファイル) にコンパイルされる[TypeScript](http://www.typescriptlang.org/) (ts ファイル) で記述されます。

**Application**

`Application` は、application. ts に定義されています。 このオブジェクトは、アプリケーションを初期化し、ルート名前空間として機能します。 ユーザーがサインインしているかどうかなど、アプリケーション間で共有される構成および状態の情報を保持します。

`application.start` メソッドは、モーダルビューを作成し、ユーザーのサインインなどのアプリケーションレベルのイベントのイベントハンドラーをアタッチします。 次に、既定のルーターを作成し、クライアント側の URL が指定されているかどうかを確認します。 そうでない場合は、既定の url (#!/) にリダイレクトされます。

**イベント**

疎結合コンポーネントを開発する場合、イベントは常に重要です。 多くの場合、アプリケーションはユーザーの操作に応じて複数の操作を実行します。 バックボーンには、モデル、コレクション、ビューなどのコンポーネントを含む組み込みイベントが用意されています。 このテンプレートは、これらのコンポーネント間で依存関係を作成するのではなく、"pub/sub" モデルを使用します。 `events` オブジェクトは、アプリケーションイベントを発行およびサブスクライブするためのイベントハブとして機能します。 `events` オブジェクトはシングルトンです。 次のコードは、イベントをサブスクライブし、イベントをトリガーする方法を示しています。

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

**ルーター**

バックボーンでは、ルーターにクライアント側ページをルーティングし、それらをアクションやイベントに接続するためのメソッドが用意されています。 このテンプレートは、router で1つのルーターを定義します。 ルーターは、アクティブ化可能なビューを作成し、ビューを切り替えるときに状態を保持します。 アクティブ化可能なビューについては、次のセクションで説明します。初期状態では、プロジェクトには、[ホーム] と [バージョン情報] の2つのダミービューがあります。 また、NotFound ビューもあります。これは、ルートが不明の場合に表示されます。

**ビュー**

ビューは ~/スクリプト/アプリケーション/ビューで定義されています。 ビューには、activable ビューとモーダルダイアログビューの2種類があります。 アクティブ化可能なビューは、ルーターによって呼び出されます。 アクティブ化可能なビューが表示されると、他のすべてのアクティブ化可能なビューが非アクティブになります。 アクティブ化可能なビューを作成するには、`Activable` オブジェクトを使用してビューを拡張します。

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

`Activable` で拡張すると、ビュー、`activate`、および `deactivate`の2つの新しいメソッドが追加されます。 ルーターは、これらのメソッドを呼び出して、ビューをアクティブ化して残っ powerpivot します。

モーダルビューは、 [Twitter ブートストラップ](https://twitter.github.com/bootstrap/)モーダルダイアログとして実装されます。 `Membership` ビューと `Profile` ビューは、モーダルビューです。 モデルビューは、任意のアプリケーションイベントによって呼び出すことができます。 たとえば、`Navigation` ビューでは、[マイアカウント] リンクをクリックすると、ユーザーがログインしているかどうかに応じて、`Membership` ビューまたは `Profile` ビューが表示されます。 `Navigation` は、`data-command` 属性を持つすべての子要素に click イベントハンドラーをアタッチします。 HTML マークアップは次のとおりです。

[!code-html[Main](backbonejs-template/samples/sample3.html)]

次に示すのは、イベントをフックするための、ナビゲーションのコードです。

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

**モデル**

モデルは ~/Scripts/application/models. で定義されています。 すべてのモデルには、既定の属性、検証規則、およびサーバー側のエンドポイントという3つの基本的な特徴があります。 一般的な例を次に示します。

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

**プラグイン**

~/スクリプト/Application/lib フォルダーには、いくつかの便利な jQuery プラグインが含まれています。フォームの ts ファイルは、フォームデータを操作するためのプラグインを定義します。 多くの場合、フォームデータをシリアル化または逆シリアル化し、モデルの検証エラーを表示する必要があります。 フォームの ts プラグインには、`serializeFields`、`deserializeFields`、`showFieldErrors`などのメソッドがあります。 次の例では、フォームをモデルにシリアル化する方法を示します。

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

Flashbar プラグインは、さまざまな種類のフィードバックメッセージをユーザーに提供します。 メソッドは、`$.showSuccessbar`、`$.showErrorbar`、および `$.showInfobar`です。 バックグラウンドでは、Twitter のブートストラップアラートを使用して、適切にアニメーション化されたメッセージを表示します。

次のように、API は多少異なりますが、ブラウザーの [確認] ダイアログボックスは、ts プラグインによって置き換えられます。

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a>チュートリアル: サーバーコード

では、サーバー側を見てみましょう。

**コントローラー**

シングルページアプリケーションでは、サーバーはユーザーインターフェイスでごくわずかな役割を果たします。 通常、サーバーは最初のページを表示し、JSON データを送受信します。

テンプレートには、2つの MVC コントローラーがあります。 `HomeController` 最初のページを表示し、`SupportsController` を使用して新しいユーザーアカウントを確認し、パスワードをリセットします。 テンプレート内の他のすべてのコントローラーは ASP.NET Web API コントローラーで、JSON データを送受信します。 既定では、コントローラーは新しい `WebSecurity` クラスを使用して、ユーザー関連のタスクを実行します。 ただし、これらのタスクに対してデリゲートを渡すことができるオプションのコンストラクターも用意されています。 これにより、テストが容易になり、IoC コンテナーを使用して `WebSecurity` を別のものに置き換えることができます。 たとえば次のようになります。

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a>ビュー

ビューはモジュール化されるように設計されています。ページの各セクションには専用のビューがあります。 シングルページアプリケーションでは、対応するコントローラーを持たないビューが含まれるのが一般的です。 `@Html.Partial('myView')`を呼び出すことによってビューを含めることができますが、これは面倒です。 これを簡単にするために、テンプレートは、指定されたフォルダー内のすべてのビューを表示するヘルパーメソッド `IncludeClientViews`を定義します。

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

フォルダー名が指定されていない場合、既定のフォルダー名は "ClientViews" になります。 クライアントビューでも部分ビューが使用されている場合は、部分ビューにアンダースコア文字を付けます (たとえば、`_SignUp`)。 `IncludeClientViews` メソッドでは、アンダースコアで始まる名前を持つビューは除外されます。 部分ビューをクライアントビューに含めるには、`Html.Partial('_SignUp')`ではなく `Html.ClientView('SignUp')` を呼び出します。

**電子メールの送信**

電子メールを送信する場合、テンプレートは[郵便](http://aboutcode.net/postal)を使用します。 ただし、郵便は `IMailer` インターフェイスを使用してコードの残りの部分から抽象化されるため、別の実装に簡単に置き換えることができます。 電子メールテンプレートは、[Views/email] フォルダーにあります。 送信者の電子メールアドレスは、web.config ファイルの**appSettings**セクションの `sender.email` キーに指定されます。 また、web.config で `debug="true"` 場合、アプリケーションは開発を高速化するためにユーザーの電子メール確認を必要としません。

## <a name="github"></a>GitHub

また、 [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)では、バックボーンの node.js のテンプレートを見つけることもできます。

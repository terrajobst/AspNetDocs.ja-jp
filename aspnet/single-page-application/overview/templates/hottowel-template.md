---
uid: single-page-application/overview/templates/hottowel-template
title: ホットタオルテンプレート |Microsoft Docs
author: madskristensen
description: ホットタオルテンプレート
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075061"
---
# <a name="hot-towel-template"></a>Hot Towel テンプレート

[Mads Kristensen](https://github.com/madskristensen)

> ホットタオル MVC テンプレートは John Papa によって作成されます。
> 
> ダウンロードするバージョンの選択:
> 
> [Visual Studio 2012 用のホットペーパー MVC テンプレート](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [Visual Studio 2013 用のホットタオル MVC テンプレート](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> ホットタオル: SPA にアクセスしないようにする必要があります。

SPA を構築するが、どこから開始するかを決定できない場合は、 ホットタオルを使用して、数秒で SPA とすべてのツールを構築する必要があります。

ホットタオルでは、ASP.NET を使用してシングルページアプリケーション (SPA) を構築するための開始点として優れています。 すぐに使えるように、コードのモジュール形式の構造、ビューのナビゲーション、データバインディング、豊富なデータ管理、シンプルで洗練されたスタイル設定を提供しています。 ホットタオルは SPA を構築するために必要なすべての機能を備えているので、アプリに集中することができます。

> 詳細については[、John Papa のビデオ、チュートリアル、Pluralsight コース](http://johnpapa.net/spa?vsix)からの SPA の構築に関するページを参照してください。

## <a name="application-structure"></a>アプリケーション構造

ホットタオル SPA には、アプリケーションを定義する JavaScript および HTML ファイルを含むアプリフォルダーが用意されています。

アプリフォルダー内:

- durandal
- サービス
- viewmodel
- 表示

アプリフォルダーには、モジュールのコレクションが含まれています。 これらのモジュールは、機能をカプセル化し、他のモジュールとの依存関係を宣言します。 Views フォルダーには、アプリケーションの HTML が含まれています。また、viewmodel フォルダーには、ビューのプレゼンテーションロジック (共通 MVVM パターン) が含まれています。 Services フォルダーは、アプリケーションで必要になる可能性のある一般的なサービス (HTTP データの取得やローカルストレージの相互作用など) を格納するのに最適です。 複数の viewmodel では、サービスモジュールのコードを再利用するのが一般的です。

## <a name="aspnet-mvc-server-side-application-structure"></a>ASP.NET MVC サーバー側のアプリケーション構造

ホットタオルは、使い慣れた強力な ASP.NET MVC 構造を基盤としています。

- アプリ\_開始
- コンテンツ
- コントローラー
- モデル
- スクリプト
- ビュー

## <a name="featured-libraries"></a>おすすめのライブラリ

- ASP.NET MVC
- ASP.NET Web API
- ASP.NET Web Optimization-バンドルと縮小
- 簡単な[.js](http://Breezejs.com) -豊富なデータ管理
- [Durandal](http://Durandaljs.com) -ナビゲーションとビューのコンポジション
- [ノックアウト](http://Knockoutjs.com)-データバインディング
- [必要な .js](http://requirejs.org) -AMD および optimization によるモジュール性
- [Toastr](http://jpapa.me/c7toastr) -ポップアップメッセージ
- [Twitter のブートストラップ](https://twitter.github.com/bootstrap/)-堅牢な CSS スタイル

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a>Visual Studio 2012 ホットタオルの SPA テンプレートを使用したインストール

ホットタオルは、Visual Studio 2012 テンプレートとしてインストールできます。 `File` | `New Project` をクリックし、`ASP.NET MVC 4 Web Application` を選択します。 次に、"ホットタオルシングルページアプリケーション" テンプレートを選択し、を実行します。

## <a name="installing-via-the-nuget-package"></a>NuGet パッケージを使用したインストール

また、Hot タオルは、既存の空の ASP.NET MVC プロジェクトを補強する NuGet パッケージでもあります。 Nuget を使用してインストールするだけで、を実行します。

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a>ホットタオルでビルドするにはどうすればいいですか。

単にコードの追加を開始します。

1. 独自のサーバー側コードを追加します (できれば Entity Framework と WebAPI)。
2. `App/views` フォルダーへのビューの追加
3. `App/viewmodels` フォルダーに viewmodel を追加する
4. 新しいビューに HTML およびノックアウトデータバインドを追加する
5. `shell.js` のナビゲーションルートを更新する

## <a name="walkthrough-of-the-htmljavascript"></a>HTML/JavaScript のチュートリアル

### <a name="viewshottowelindexcshtml"></a>Views/HotTowel/index.cshtml

index. cshtml は、MVC アプリケーションの開始ルートおよびビューです。 これには、すべての標準的なメタタグ、css リンク、および必要とされる JavaScript の参照が含まれています。 本文には、要求されたときにすべてのコンテンツ (ビュー) が配置される1つの `<div>` が含まれています。 `@Scripts.Render` は、`main.js` ファイルに格納されているアプリケーションのコードの開始ポイントを実行するために、必要な .js を使用します。 スプラッシュスクリーンは、アプリの読み込み中にスプラッシュスクリーンを作成する方法を示すために用意されています。

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a>アプリ/メイン js

`main.js` ファイルには、アプリが読み込まれるとすぐに実行されるコードが含まれています。 ここでは、ナビゲーションルートを定義し、スタートアップビューを設定し、アプリケーションのデータの準備などの設定/ブートストラップを実行します。

`main.js` ファイルは、アプリケーションの起動を開始するために役立ついくつかの durandal のモジュールを定義します。 Define ステートメントを使用すると、モジュールの依存関係を解決して、関数で使用できるようになります。 まず、デバッグメッセージが有効になります。これにより、アプリケーションがコンソールウィンドウに対して実行しているイベントに関するメッセージが送信されます。 アプリの開始コードは、アプリケーションを起動するように durandal framework に指示します。 規則は、durandal がすべてのビューを認識し、viewmodel が同じ名前付きフォルダーにそれぞれ含まれるように設定されています。 最後に、定義済みの `entrance` アニメーションを使用して、`app.setRoot` によって `shell` が読み込まれます。

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a>ビュー

ビューは `App/views` フォルダーにあります。

### <a name="shellhtml"></a>shell.html

`shell.html` には、HTML のマスターレイアウトが含まれています。 他のすべてのビューは、`shell` ビューの側のどこかに構成されます。 ホットタオルは、ヘッダー、コンテンツ領域、およびフッターという3つの領域を持つ `shell` を提供します。 これらの各リージョンには、要求されたときに他のビューのコンテンツと共に読み込まれます。

ヘッダーとフッターの `compose` バインドは、`nav` ビューと `footer` ビューを指すように、ホットタオルでハードコーディングされます。 セクション `#content` の作成バインドは、`router` モジュールのアクティブな項目にバインドされます。 つまり、ナビゲーションリンクをクリックすると、対応するビューがこの領域に読み込まれます。

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a>nav.html

`nav.html` には、SPA のナビゲーションリンクが含まれています。 たとえば、メニュー構造を配置できます。 多くの場合、これは、`shell.js`で定義したナビゲーションを表示するために、`router` モジュールへの (ノックアウトを使用した) データバインドです。 ノックアウトは、データバインド属性を検索し、それらを `shell` ビューモデルにバインドして、ナビゲーションルートを表示したり、`router` モジュールがあるビューから別のビューに移動しているときに (Twitter ブートストラップを使用して) progressbar を表示したりします (`router.isNavigating`を参照)。

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a>home .html と details .html

これらのビューには、カスタムビューの HTML が含まれています。 `nav` ビューのメニューの [`home`] リンクをクリックすると、`home` ビューが `shell` ビューのコンテンツ領域に配置されます。 これらのビューは、独自のカスタムビューに拡張することも、置き換えることもできます。

### <a name="footerhtml"></a>footer.html

`footer.html` には、`shell` ビューの下部にあるフッターに表示される HTML が含まれています。

## <a name="viewmodels"></a>ViewModels

Viewmodel フォルダー `App/viewmodels` にあります。

### <a name="shelljs"></a>shell.js

`shell` ビューモデルには、`shell` ビューにバインドされているプロパティおよび関数が含まれています。 多くの場合、メニューナビゲーションバインドが見つかります (`router.mapNav` ロジックを参照)。

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a>home .js と details js

これらの viewmodel には、`home` ビューにバインドされているプロパティおよび関数が含まれています。 また、ビューのプレゼンテーションロジックも含まれており、データとビューの間の接着です。

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a>サービス

サービスは、App/services フォルダーにあります。 リモートデータの取得と送信を行う dataservice モジュールなどの今後のサービスを配置するのが理想的です。

### <a name="loggerjs"></a>logger.js

ホットタオルでは、services フォルダーに `logger` モジュールが提供されます。 `logger` モジュールは、コンソールにメッセージを記録する場合と、ユーザーにポップアップで表示する場合に最適です。

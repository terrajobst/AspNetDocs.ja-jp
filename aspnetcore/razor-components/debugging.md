---
title: Razor のコンポーネントをデバッグします。
author: guardrex
description: Blazor と剃刀コンポーネントのアプリをデバッグする方法について説明します。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/debug
ms.openlocfilehash: fb7ddcf3ae40ec28a372adf724a293b375be28a1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034119"
---
# <a name="debug-razor-components"></a>Razor のコンポーネントをデバッグします。

[Daniel Roth](https://github.com/danroth27)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

Razor のコンポーネントがいくつか*ごく初期*WebAssembly Chrome 内で実行されているクライアント側 Blazor アプリのデバッグをサポートします。 この初期のデバッグのサポートは、非常に限られ unpolished には、クラスタ リング、基本的なデバッグ インフラストラクチャを示します。

Chrome でクライアント側 Blazor アプリをデバッグします。

* Blazor アプリ構築`Debug`(非によって発行されたアプリの既定値) を構成します。
* Chrome (バージョン 70 またはそれ以降) で Blazor アプリを実行します。
* (おそらく混乱が少なく、デバッグ エクスペリエンスを閉じる必要があります開発ツール パネル) ではないアプリで、キーボード フォーカスを持つ Blazor 固有の次のキーボード ショートカットを選択します。
  * `Shift+Alt+D` Windows または Linux で
  * `Shift+Cmd+D` macOS で

リモート デバッグを Blazor アプリのデバッグを有効には、Chrome を実行します。 リモート デバッグが無効になっている場合、エラー ページは、Chrome によって生成されます。 エラー ページは、実行されている Chrome デバッグ ポートを開く Blazor デバッグ プロキシは、アプリに接続できるようにする方法について説明します。 *Chrome のすべてのインスタンスを閉じて*の指示に従って、Chrome を再起動します。

![Blazor デバッグ エラー ページ](https://user-images.githubusercontent.com/1874516/43123091-01ec0796-8ed8-11e8-844c-23b4e6e9d069.png)

リモート デバッグを有効に Chrome が実行されると、デバッグのキーボード ショートカットは、新しいデバッガー タブを開きます。しばらくすると、*ソース* タブには、アプリでの .NET アセンブリの一覧が表示されます。 各アセンブリを展開し、検索、 *.cs*/*.cshtml*ソース ファイルのデバッグに使用します。 ブレークポイントの設定、アプリのタブに戻ると、ブレークポイントがヒットします。 ブレークポイントがヒットすると、シングル ステップ (`F10`) または再開 (`F8`) 通常します。

![Blazor のデバッグ](https://user-images.githubusercontent.com/1874516/43123060-efb0b3b0-8ed7-11e8-9ea5-97aa34247a0b.png)

Blazor 提供デバッグ プロキシを実装する、 [Chrome DevTools Protocol](https://chromedevtools.github.io/devtools-protocol/)でプロトコルを拡張するとします。NET 固有の情報。 デバッグのキーボード ショートカットが押されたときに、Blazor はプロキシで Chrome DevTools を指します。 デバッグしようとしているブラウザー ウィンドウに、プロキシが接続する (したがってリモート デバッグを有効にする必要が)。

かもしれません。 なぜブラウザー ソース マップを使用しないだけです。 ソース マップは、コンパイル済みファイルを元のソース ファイルにマップするブラウザーを許可します。 ただし、Blazor がマップされないC#JS/WASM (少なくとも現時点) に直接します。 代わりに、ソース マップは関連性のないように、Blazor は、ブラウザー内での IL 変換を行います。

デバッガーの機能は**非常に限られた**します。 のみ現在実行できます。

* 設定し、ブレークポイントを削除します。
* コードまたは再開を 1 ステップずつ (`F8`)。
* *ローカル*型の任意のローカル変数の値を確認、表示`int`、`string`と`bool`します。
* 呼び出しチェーンには、.NET の JavaScript および .NET から javascript を含む、呼び出し履歴を参照してください。

*できません*:

* はない任意のローカル変数の値を確認、 `int`、 `string`、または`bool`します。
* クラスのプロパティまたはフィールドの値を確認します。
* 変数の値を表示するポインターを合わせる
* コンソール内の式を評価します。
* 非同期呼び出しの間のステップします。
* 他のほとんどの通常のデバッグ シナリオを実行します。

さらにデバッグ シナリオの開発では、エンジニア リング チームの継続的にフォーカスが。

## <a name="troubleshooting-tip"></a>トラブルシューティングのヒント

エラーを実行している場合は、次のヒントが役立つ場合があります。

**デバッガー**  タブで、お使いのブラウザーで開発者ツールを開きます。 コンソールで、次のように実行します。 `localStorage.clear()` 、ブレークポイントを削除します。

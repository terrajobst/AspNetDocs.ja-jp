---
ms.openlocfilehash: eb2f83504129ae2b19ff5d85a2bc7d90293b43d6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043399"
---
* Startup.cs:[スタートアップ クラス](xref:fundamentals/startup)-クラスは、アプリケーションに対して行われたすべての要求を処理する要求パイプラインを構成します。
* Program.cs:[クラスをプログラム](xref:fundamentals/index)アプリケーションのメイン エントリ ポイントを格納しています。
* firstapp.csproj :[プロジェクト ファイル](/dotnet/articles/core/preview3/tools/csproj)ASP.NET Core アプリケーション用の MSBuild プロジェクト ファイル形式。 プロジェクト間参照を含む NuGet 参照およびその他のプロジェクト関連の項目。
* appsettings.json/appsettings します。Development.json:環境ベースのアプリ設定の構成ファイルです。 [構成を参照してください。](xref:fundamentals/configuration/index)します。
* bower.json:Bower パッケージは、プロジェクトの依存関係。
* .bowerrc。Bower は、資産をダウンロードするときに、コンポーネントをインストールする場所を定義する bower 構成ファイルです。
* bundleconfig.json: バンドルと縮小のフロント エンド JavaScript と CSS の資産の構成ファイル。
* 表示モード：Razor ビューが含まれています。 ビューは、アプリのユーザー インターフェイス (UI) を表示するコンポーネントです。 一般に、この UI ではモデル データが表示されます。
* コント ローラー:最初に MVC コント ローラーを含む*HomeController.cs*します。 コント ローラーは、ブラウザーの要求を処理するクラスです。
* wwwroot:Web アプリケーションのルート フォルダー。

詳細については、次を参照してください。 [、MVC パターン](xref:mvc/overview)します。

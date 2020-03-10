---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: Visual Studio 2013 のスキャフォールディングを ASP.NET |Microsoft Docs
author: Rick-Anderson
description: ASP.NET スキャフォールディングは Visual Studio 2013 に含まれる新機能です。
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449566"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a>Visual Studio 2013 の ASP.NET スキャフォールディング

[Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET スキャフォールディングは Visual Studio 2013 に含まれる新機能です。

## <a name="overview"></a>概要

ASP.NET スキャフォールディングは、ASP.NET Web アプリケーションのコード生成フレームワークです。 Visual Studio 2013 には、MVC および Web API プロジェクト用のプレインストールされたコードジェネレーターが含まれています。 データモデルと対話するコードをすばやく追加する場合は、スキャフォールディングをプロジェクトに追加します。 スキャフォールディングを使用すると、プロジェクトで標準データ操作を開発するための時間を短縮できます。

既定では、Visual Studio 2013 は Web フォームプロジェクトのコードの生成をサポートしていませんが、MVC の依存関係をプロジェクトに追加するか、拡張機能をインストールすることにより、Web フォームでスキャフォールディングを使用できます。 両方の方法を次に示します。

Visual Studio 2013 Update 2 (現在 RC) では、シナリオの要件を満たすように ASP.NET スキャフォールディングを拡張することができます。 この機能を使用すると、カスタマイズされたスキャフォールディングテンプレートを作成し、[新しいスキャフォールディングの追加] ダイアログに追加できます。 カスタマイズしたテンプレート内で、スキャフォールディング項目を追加するときに生成されるコードを指定します。 詳細については、「 [Visual Studio のカスタム Scaffolder の作成](https://go.microsoft.com/fwlink/p/?LinkId=395029)」を参照してください。

## <a name="prerequisites"></a>前提条件

ASP.NET スキャフォールディングを使用するには、次のものが必要です。

- Microsoft Visual Studio 2013
- Web 開発者ツール (既定 Visual Studio 2013 インストールの一部)
- ASP.NET Web フレームワークとツール 2013 (既定の Visual Studio 2013 インストールの一部)

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a>MVC または Web API にスキャフォールディング項目を追加する

スキャフォールディングを追加するには、次の図に示すように、プロジェクトまたはプロジェクト内のフォルダーを右クリックし、[**追加**-**新規スキャフォールディング項目**] を選択します。

![スキャフォールディング項目の追加](aspnet-scaffolding-overview/_static/image1.png)

**[Add スキャフォールディング]** ウィンドウで、追加するスキャフォールディングの種類を選択します。

![スキャフォールディングの種類を選択します](aspnet-scaffolding-overview/_static/image2.png)

**[コントローラーの追加]** ウィンドウでは、Entity Framework 6 の新しい非同期機能を使用するかどうかなど、コントローラーを生成するためのオプションを選択できます。

![コントローラーの追加](aspnet-scaffolding-overview/_static/image3.png)

シナリオに応じて、関連するクラスとページが作成されます。 たとえば、次の図は、ムービーという名前のモデルクラスのスキャフォールディングによって作成された MVC コントローラーとビューを示しています。

![作成されたファイル](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a>スキャフォールディング項目を Web フォームに追加する

Web フォームコードを生成するスキャフォールディングを追加するには、Visual Studio に拡張機能をインストールするか、MVC 依存関係を追加する必要があります。 両方の方法を次に示しますが、これらの方法のいずれかを実行するだけでよいでしょう。

### <a name="web-forms-scaffolding-extension"></a>Web フォームのスキャフォールディング拡張機能

Web フォームプロジェクトでスキャフォールディングを使用できるようにする Visual Studio 拡張機能をインストールできます。 Visual Studio で、 **[ツール]** 、 **[拡張機能と更新プログラム]** の順に選択します。 このダイアログでは、Visual Studio ギャラリーで**Web フォームのスキャフォールディング**を検索します。

![web フォームのスキャフォールディングをインストールする](aspnet-scaffolding-overview/_static/image5.png)

詳細については、「 [Web フォームのスキャフォールディング](https://go.microsoft.com/fwlink/p/?LinkId=396478)」を参照してください。

### <a name="mvc-dependencies"></a>MVC の依存関係

MVC の依存関係を追加するには、[ **add** - **New スキャフォールディング Item**] を選択します。 次に示すように、スキャフォールディングの追加 ウィンドウで、 **MVC の依存関係** を選択します。

![MVC の依存関係の追加](aspnet-scaffolding-overview/_static/image6.png)

MVC のスキャフォールディングには、2つのオプションがあります。最小と完全。 [最小] を選択すると、ASP.NET MVC の NuGet パッケージと参照のみがプロジェクトに追加されます。 [完全] オプションを選択した場合は、最小の依存関係だけでなく、MVC プロジェクトに必要なコンテンツファイルが追加されます。 スキャフォールディングを簡単に使用するには、[完全な依存関係] を選択します。

![完全な依存関係の選択](aspnet-scaffolding-overview/_static/image7.png)

依存関係を追加すると、 **readme.txt**ファイルが表示されます。 このファイルの指示に従って、プロジェクトが正しく動作することを確認します。

Readme.txt ファイルの手順を完了したら、前の「MVC と Web API について」セクションで示したように、新しいスキャフォールディング項目を追加できます。 自動的に生成されたビューとコントローラーは、プロジェクト内で正しく機能します。

## <a name="tutorials"></a>チュートリアル

カスタマイズした scaffolder を作成するには、「 [Visual Studio のカスタム scaffolder の作成](https://go.microsoft.com/fwlink/p/?LinkId=395029)」を参照してください。

生成されたファイルをカスタマイズする方法については、「 [New スキャフォールディング Item」ダイアログで生成されたファイルをカスタマイズする方法](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx)に関する説明を参照してください。

**Database First 開発**でスキャフォールディングを使用する例については、「 [EF DATABASE FIRST with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md)」を参照してください。

**Mvc**プロジェクトでスキャフォールディングを使用する例については、「[はじめに with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)」を参照してください。

**WEB api**プロジェクトでスキャフォールディングを使用する例については、「 [web Api 2 で属性ルーティングを使用して REST API を作成する](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md)」を参照してください。

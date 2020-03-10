---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 | にアップグレードするMicrosoft Docs
author: rick-anderson
description: このドキュメントでは、手動でアップグレードする方法と、ウィザードを使用して ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードする方法について説明します。 このドキュメントは、d...
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517300"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a>ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードする

> このドキュメントでは、手動でアップグレードする方法と、ウィザードを使用して ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードする方法について説明します。 このドキュメントは、[ダウンロード](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)することもできます。

## <a name="introduction"></a>はじめに

ASP.NET MVC 2 は、同じサーバーに ASP.NET MVC 1.0 とサイドバイサイドでインストールできます。 これにより、アプリケーション開発者は、ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードするタイミングを柔軟に選択できます。

Visual Studio 2010 には、Visual Studio 2008 でビルドされた既存の ASP.NET MVC 1.0 プロジェクトを ASP.NET MVC 2 にアップグレードするウィザードが含まれています。 アップグレードウィザードを開始するには、Visual Studio 2010 で ASP.NET MVC 1.0 プロジェクトを開きます。

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a>Visual Studio 2008 SP1 での ASP.NET MVC 1.0 のアップグレードウィザード

Visual Studio 2008 SP1 で ASP.NET MVC 1.0 アプリケーションを ASP.NET MVC 2 にアップグレードするには、(サポートされていない) MvcAppConverter アプリケーションを使用します。 このアプリケーションは、次の URL からダウンロードできます。

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a>ASP.NET MVC 1.0 プロジェクトの手動アップグレード

既存の ASP.NET MVC 1.0 アプリケーションをバージョン2に手動でアップグレードするには、次の手順を実行します。

1. 既存のプロジェクトのバックアップを作成します。
2. テキストエディターで、プロジェクトファイル (.csproj または .vbproj ファイル拡張子の付いたファイル) を開き、ProjectTypeGuid 要素を検索します。 この要素の値として、GUID {603c0e0b-11db56の値を {F85E285D-A4E0-4152-9332-AB1D724D3325} に置き換えます。この値を変更します。 完了すると、その要素の値は次のようになります。 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. Web アプリケーションのルートフォルダーで、web.config ファイルを編集します。 System.web. Mvc, Version = 1.0.0.0 を検索し、すべてのインスタンスを System.web. Mvc, Version = 2.0.0.0 に置き換えます。
4. Views フォルダーにある web.config ファイルに対して、前の手順を繰り返します。
5. Visual Studio を使用してプロジェクトを開き、**ソリューションエクスプローラー**で **[参照]** ノードを展開します。 (バージョン1.0 アセンブリを指す) System.web. Mvc への参照を削除します。 System.web. Mvc (v 2.0.0.0) への参照を追加します。
6. 次の bindingRedirect 要素を、アプリケーションルートの構成セクションにある web.config ファイルに追加します。   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. 新しい空の ASP.NET MVC 2 アプリケーションを作成します。 新しいアプリケーションの Scripts フォルダーにあるファイルを、既存のアプリケーションの Scripts フォルダーにコピーします。
8. 既存の™アプリケーションの css ファイルを、サイトの .css ファイルの CSS スタイル定義で更新します。
9. アプリケーションをコンパイルして実行します。 エラーが発生した場合は、「 [ASP.NET MVC 2 の新機能](https://go.microsoft.com/fwlink/?LinkID=185038)」ページの「互換性に影響する変更点」セクションを参照してください。

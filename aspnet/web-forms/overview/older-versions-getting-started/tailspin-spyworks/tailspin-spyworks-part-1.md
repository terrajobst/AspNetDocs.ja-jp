---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: 'パート 1: ファイル > 新しいプロジェクト |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート1では、概要とファイル/新しいプロジェクトについて説明します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516538"
---
# <a name="part-1-file--new-project"></a>パート 1: ファイル > 新しいプロジェクト

[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。 ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。
> 
> このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート1では、概要とファイル/新しいプロジェクトについて説明します。

## <a id="_Toc260221666"></a>概要

このチュートリアルでは、ASP.NET WebForms の概要について説明します。 開始に時間がかかります。初心者レベルの web 開発エクスペリエンスは問題ありません。

構築するアプリケーションは、単純なオンラインストアです。

![](tailspin-spyworks-part-1/_static/image1.jpg)

訪問者はカテゴリで製品を参照できます。

![](tailspin-spyworks-part-1/_static/image2.jpg)

1つの製品を表示し、カートに追加することができます。

![](tailspin-spyworks-part-1/_static/image3.jpg)

カートをレビューして、不要になったアイテムを削除することができます。

![](tailspin-spyworks-part-1/_static/image4.jpg)

チェックアウトに進むと、

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

順序を付けると、簡単な確認画面が表示されます。

![](tailspin-spyworks-part-1/_static/image7.jpg)

まず、Visual Studio 2010 で新しい ASP.NET WebForms プロジェクトを作成します。次に、機能を段階的に追加して、完全に機能するアプリケーションを作成します。 その過程で、データベースアクセス、リストとグリッドビュー、データ更新ページ、データの検証、ページレイアウトの一貫性のためのマスターページの使用、AJAX、検証、ユーザーメンバーシップなどについて説明します。

ステップバイステップで進めることができます。または、完成したアプリケーションをからダウンロードすることもでき[http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)

[https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/)から visual Studio 2010 または無料の Visual Web Developer 2010 を使用できます。 アプリケーションをビルドするには、SQL Server または無料の SQL Server Express を使用してデータベースをホストできます。

## <a id="_Toc260221667"></a>ファイル/新しいプロジェクト

まず、Visual Studio の [ファイル] メニューから新しいプロジェクトを選択します。 [新しいプロジェクト] ダイアログが表示されます。

![](tailspin-spyworks-part-1/_static/image8.jpg)

左側の [ビジュアルC# /Web テンプレート] グループを選択し、中央の列で [ASP.NET Web Application] テンプレートを選択します。 プロジェクトに TailspinSpyworks という名前を指定し、[OK] をクリックします。

![](tailspin-spyworks-part-1/_static/image9.jpg)

これにより、プロジェクトが作成されます。 アプリケーションに含まれているフォルダーを右側のソリューションエクスプローラーに見てみましょう。

![](tailspin-spyworks-part-1/_static/image10.jpg)

空のソリューションは完全に空ではないため、基本的なフォルダー構造が追加されます。

![](tailspin-spyworks-part-1/_static/image1.png)

ASP.NET 4 の既定のプロジェクトテンプレートによって実装される規則に注意してください。

- "Account" フォルダーには、ASP 用の基本的なユーザーインターフェイスが実装されています。NET のメンバーシップサブシステム。
- "Scripts" フォルダーは、クライアント側の JavaScript ファイルのリポジトリとして機能し、主要な jQuery .js ファイルは既定で使用可能になります。
- "Styles" フォルダーは、web サイトのビジュアルを整理するために使用されます (CSS スタイルシート)

F5 キーを押してアプリケーションを実行し、default.aspx ページを表示すると、次のような画面が表示されます。

![](tailspin-spyworks-part-1/_static/image11.jpg)

最初のアプリケーション拡張機能では、既定の WebForms テンプレートの .css ファイルを、CSS クラスと、Tailspin Spyworks アプリケーションに必要な visual asthetics をレンダリングする関連イメージファイルに置き換えます。

その後、default.aspx ページは次のようにレンダリングします。

![](tailspin-spyworks-part-1/_static/image12.jpg)

ページの右上の画像リンクと、マスターページに追加されたメニュー項目に注目してください。 "サインイン" リンクと "アカウント" リンクのみが、(既定のテンプレートによって生成される) 存在するページと、アプリケーションをビルドするときに実装する残りのページをポイントします。

また、マスターページを Styles ディレクトリに再配置します。 これは単なる優先事項ですが、将来アプリケーションを "skinable" にする場合は、少し簡単にすることができます。

この操作を行った後、既定の ASP.NET WebForms ページによって生成されるすべての .aspx ファイルのマスターページ参照を変更する必要があります。

> [!div class="step-by-step"]
> [Next](tailspin-spyworks-part-2.md)

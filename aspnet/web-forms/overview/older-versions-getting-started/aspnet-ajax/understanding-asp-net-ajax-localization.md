---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: ASP.NET AJAX ローカリゼーションについてMicrosoft Docs
author: scottcate
description: ローカリゼーションは、特定の言語とカルチャのサポートを設計し、アプリケーションまたはアプリケーションコンポーネントに統合するプロセスです。 Mic...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 003e7939accd7a68dab97441b3d999bca835b85a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78456628"
---
# <a name="understanding-aspnet-ajax-localization"></a>ASP.NET AJAX ローカライズについて理解する

[Scott Cate](https://github.com/scottcate)

[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> ローカリゼーションは、特定の言語とカルチャのサポートを設計し、アプリケーションまたはアプリケーションコンポーネントに統合するプロセスです。 Microsoft ASP.NET プラットフォームでは、標準の .NET ローカライズモデルを統合することによって、標準の ASP.NET アプリケーションのローカライズを広範にサポートしています。Microsoft AJAX Framework は、統合モデルを使用して、ローカライズを実行できるさまざまなシナリオをサポートします。

## <a name="introduction"></a>はじめに

Microsoft の ASP.NET テクノロジは、オブジェクト指向プログラミングモデルとイベントドリブンプログラミングモデルを提供し、コンパイル済みコードの利点と結び付けます。 ただし、そのサーバー側の処理モデルには、テクノロジに固有のいくつかの欠点があります。その多くは、の Microsoft AJAX サービスをカプセル化する、system.servicemodel 名前空間に含まれる新機能によって対処できます .NET Framework3.5。 これらの拡張機能により、多くのリッチクライアント機能が有効になります。以前は ASP.NET 2.0 AJAX 拡張機能の一部として提供されていましたが、現在は Framework 基底クラスライブラリの一部として利用できます この名前空間のコントロールと機能には、ページの完全更新を必要としないページの部分的なレンダリング、クライアントスクリプト (ASP.NET プロファイリング API を含む) を使用した Web サービスへのアクセス機能、および多くのものをミラー化するように設計された広範なクライアント側 API が含まれます。ASP.NET サーバー側のコントロールセットに表示されるコントロールスキーム。

このホワイトペーパーでは、Microsoft AJAX Framework および Microsoft AJAX スクリプトライブラリに含まれるローカリゼーション機能について説明します。ローカライズのサポートと、web でのローカライズに対する既に統合されたサポートの確認に関するビジネスニーズに対応しています.NET Framework によって提供されるアプリケーション。 Microsoft AJAX スクリプトライブラリでは、.NET アプリケーションで既に使用されている .resx ファイル形式を利用します。これにより、IDE の統合サポートと共有可能なリソースの種類が提供されます。

このホワイトペーパーは、Microsoft Visual Studio 2008 のベータ2リリースに基づいています。 また、このホワイトペーパーでは、visual Web Developer Express ではなく Visual Studio 2008 を使用することを前提としています。また、Visual Studio のユーザーインターフェイスに従ってチュートリアルを提供します。 一部のコードサンプルでは、Visual Web Developer Express で使用できないプロジェクトテンプレートを利用しています。

## <a name="the-need-for-localization"></a>*ローカリゼーションの必要性*

特に、エンタープライズアプリケーション開発者およびコンポーネント開発者にとって、カルチャと言語の違いを認識できるツールを作成する機能はますます必要になってきました。 クライアントのロケールに適応する機能を持つコンポーネントを設計すると、開発者の生産性が向上し、コンポーネントをグローバルに機能させるために必要な作業量が削減されます。

ローカリゼーションは、特定の言語とカルチャのサポートを設計し、アプリケーションまたはアプリケーションコンポーネントに統合するプロセスです。 Microsoft ASP.NET プラットフォームでは、標準の .NET ローカライズモデルを統合することによって、標準の ASP.NET アプリケーションのローカライズを広範にサポートしています。Microsoft AJAX Framework は、統合モデルを使用して、ローカライズを実行できるさまざまなシナリオをサポートします。 Microsoft AJAX Framework では、スクリプトをサテライトアセンブリに配置するか、静的ファイルシステム構造を使用することによって、ローカライズできます。

## <a name="embedding-scripts-with-satellite-assemblies"></a>*サテライトアセンブリを使用したスクリプトの埋め込み*

標準の .NET Framework ローカリゼーション戦略との一貫性を保つために、サテライトアセンブリにリソースを含めることができます。 サテライトアセンブリには、バイナリに含まれる従来のリソースよりもいくつかの利点があります。特定のローカライズは、より大きなイメージを更新せずに更新できます。また、サテライトアセンブリをにインストールするだけで、追加のローカライズを展開できます。プロジェクトフォルダーおよびサテライトアセンブリは、メインプロジェクトアセンブリを再読み込みせずに配置できます。 特に ASP.NET プロジェクトでは、増分更新によって使用されるシステムリソースの量を大幅に削減し、運用 web サイトの使用量を最小限に抑えることができるため便利です。

スクリプトは、コンパイル時にアセンブリに含まれるマネージ .resx (またはコンパイル済み .resources) ファイルに含めることで、アセンブリに埋め込まれます。 これらのリソースは、アセンブリレベルの属性を使用して、AJAX ランタイムによって生成されたコードを介してスクリプトアプリケーションで使用できるようになります。

*埋め込みスクリプトファイルの名前付け規則*

Microsoft AJAX Framework スクリプト管理は、スクリプトの配置とテストに使用するさまざまなオプションをサポートしており、これらのオプションを容易にするためのガイドラインが用意されています。

*デバッグを容易にするには:*

リリース (実稼働) スクリプトには、ファイル名に `.debug` 修飾子を含めないでください。 デバッグ用に設計されたスクリプトには、ファイル名に `.debug` を含める必要があります。

*ローカライズを容易にするには:*

ニュートラルカルチャスクリプトでは、ファイルの名前にカルチャ識別子を含めることはできません。 ローカライズされたリソースを含むスクリプトの場合は、ファイル名に ISO 言語コードを指定する必要があります。 たとえば、`es-CO` はスペイン語 (コロンビア) を表します。

次の表は、ファイルの名前付け規則と例をまとめたものです。

| ファイル名 | 意味 |
| --- | --- |
| Script.js | リリースバージョンのカルチャに依存しないスクリプト。 |
| Script.debug.js | デバッグバージョンのカルチャに依存しないスクリプト。 |
| Script.en-US.js | リリースバージョン英語、米国スクリプト。 |
| Script.debug.es-CO.js | デバッグバージョンのスペイン語、コロンビア用スクリプト。 |

## <a name="walkthrough-create-an-localized-embedded-script"></a>チュートリアル: ローカライズされた埋め込みスクリプトの作成

*注意: このチュートリアルでは、visual Web Developer Express にクラスライブラリプロジェクトのプロジェクトテンプレートが含まれていないため、Visual Studio 2008 を使用する必要があります。*

1. ASP.NET AJAX Extensions が統合された新しい Web サイトプロジェクトを作成します。 別のプロジェクト (クラスライブラリプロジェクト) を、LocalizingResources というソリューション内に作成します。
2. VerifyDeletion という名前の Jscript ファイルを LocalizingResources プロジェクトに追加し、DeletionResources と DeletionResources という名前の .resx リソースファイルを追加します。 前者には、カルチャに依存しないリソースが含まれます。後者にはスペイン語のリソースが含まれます。
3. VerifyDeletion に次のコードを追加します。

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

JavaScript Regex 構文に慣れていない場合、1つのスラッシュ (前の例では/FILENAME/が例) では、RegExp オブジェクトを表します。 MSDN ライブラリには広範な JavaScript リファレンスが含まれており、JavaScript ネイティブオブジェクトのリソースはオンラインで参照できます。

1. DeletionResources に次のリソース文字列を追加します。 

    **Verifydelete**: ファイル名を削除しますか?

    **Deleted**: ファイル名が削除されました。

1. DeletionResources に次のリソース文字列を追加します。 

    **Verifydelete**: Est seguro クエリ desee quitar FILENAME?

    **Deleted**: ファイル名 se ha quitado。
2. AssemblyInfo ファイルに次のコード行を追加します。

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. LocalizingResources プロジェクトに System.web および System.web 拡張子への参照を追加します。
2. Web サイトプロジェクトから LocalizingResources プロジェクトへの参照を追加します。
3. Default.aspx の Web サイトプロジェクトで、次の追加のマークアップを使用して ScriptManager コントロールを更新します。

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. Default.aspx では、ページ上の任意の場所に、次のマークアップが含まれています。

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. F5 キーを押す。 メッセージが表示されたら、デバッグを有効にします。 ページが読み込まれたら、[削除] ボタンをクリックします。 確認のために、(コンピューターが既定でスペイン語の言語リソースを優先するように設定されている場合を除き) 英語でメッセージが表示されることに注意してください。
2. ブラウザーウィンドウを閉じ、default.aspx に戻ります。 @Page header ディレクティブで、auto for Culture と UICulture を es ES に置き換えます。 もう一度 F5 キーを押して、ブラウザーで web アプリケーションを再び起動します。 今回は、スペイン語でファイルを削除するように求められます。

[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-localization/_static/image3.png)される)

[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

([クリックすると、フルサイズの画像が表示](understanding-asp-net-ajax-localization/_static/image6.png)される)

このチュートリアルにはいくつかのバリエーションがあることに注意してください。 たとえば、スクリプトは、ページの読み込み中にプログラムによって ScriptManager コントロールに登録できます。

## <a name="including-a-static-script-file-structure"></a>*静的スクリプトファイル構造を含める*

配置に静的スクリプトファイルを使用すると、固有の .NET ローカライズ方式を使用する利点の一部が失われます。 主に表示されるのは、スクリプトリソースファイルを含めて生成される自動型が失われることです。上記のチュートリアルでは、たとえば、ScriptManager コントロールからのメッセージと呼ばれる自動的に生成された型によってリソースが公開されていました。

ただし、静的なスクリプトファイルの構造を使用することには、いくつかの利点があります。 更新は、サテライトアセンブリを再コンパイルおよび再配置することなく実行できます。また、コンポーネントに付属していない機能のマイナー部分を統合するために、埋め込みスクリプトをオーバーライドする静的ファイル構造の使用を行うこともできます。

プロジェクトのコンパイル中にスクリプトリソースを自動的に生成することで、バージョン管理の問題を回避することをお勧めします。 広範なスクリプトコードベースを維持すると、コードの変更がローカライズされた各スクリプトに反映されるように、ますます困難になる可能性があります。 別の方法として、1つのロジックスクリプトと複数のローカライズスクリプトを保守するだけで、プロジェクトのビルド中にファイルをマージすることもできます。

宣言に含まれるリソースがないため、静的なスクリプトファイルは、ScriptManager コントロールの `<Scripts>` タグの子として `<asp:ScriptElement>` 要素を追加するか、実行時にページの `ScriptManager` コントロールの `Scripts` プロパティに `ScriptReference` オブジェクトをプログラムで追加することによって参照する必要があります。

## <a name="the-scriptmanager-and-its-role-in-localization"></a>*ローカライズにおける ScriptManager とその役割*

ScriptManager コントロールによって、ローカライズされたアプリケーションのいくつかの自動動作が可能になります。

- 設定と名前付け規則に基づいてスクリプトファイルを自動的に検索します。たとえば、デバッグモードでデバッグが有効なスクリプトを読み込み、ブラウザーのユーザーインターフェイスの選択に基づいて、ローカライズされたスクリプトを読み込みます。
- これにより、カスタムカルチャを含むカルチャの定義が可能になります。
- これにより、HTTP 経由でスクリプトファイルを圧縮できるようになります。
- 多くの要求を効率的に管理するためにスクリプトをキャッシュします。
- 暗号化された URL を使用してパイプを使用して、スクリプトに間接レイヤーを追加します。

スクリプト参照を ScriptManager コントロールに追加するには、プログラムから、または宣言型のマークアップを使用します。 宣言型マークアップは、web サイトプロジェクト自体以外のアセンブリに埋め込まれたスクリプトを使用する場合に特に便利です。これは、スクリプトの名前が変更されても変更されない可能性があるためです。

## <a name="summary"></a>まとめ

Web アプリケーションの規模が拡大するにつれて、より多くのユーザーにリーチできるようにするためには、より広範なカルチャに至ることができ、コミュニティはビジネスモデルの中核になります。e コマース web アプリケーションは、国外の通貨を扱うことができる必要があります。コンテンツ管理システムでは、コンテンツだけでなく、ナビゲーションヒントやフォームフィールドを他の言語でも表示できる必要があります。また、会社のニーズが利用.

.NET Framework は、サテライトアセンブリおよび XML リソース (.resx) ファイルを利用して、リソース文字列とイメージを検索するための統一された方法を提供する、豊富なローカライズフレームワークを本質的にサポートしています。 Microsoft AJAX Framework および Microsoft AJAX スクリプトライブラリを含む ASP.NET AJAX 拡張機能は、クライアント側のコードにこのプログラミングモデルのサポートを提供し、簡単なリソース文字列の参照を可能にします。 サテライトアセンブリは、ファイル名が指定された名前付けスキームに従っている限り、スクリプトリソース (実際の .js ファイル) を ScriptResource を通じて自動的に含めることをサポートしています。 このサポートにより、ASP.NET AJAX Extensions により、スクリプトのローカライズとアプリケーションのグローバリゼーションが簡略化されます。

## <a name="bio"></a>*略歴*

Scott Cate は1997以来 Microsoft の Web テクノロジを使用しています。また、myKB.com ([www.myKB.com](http://www.myKB.com)) の大統領で、サポート技術情報のソフトウェアソリューションに重点を置いた ASP.NET ベースのアプリケーションを作成することを専門としています。 Scott は、 [scott.cate@myKB.com](mailto:scott.cate@myKB.com)または彼のブログ ( [ScottCate.com](http://ScottCate.com) ) で、電子メールで連絡を受けることができます。

> [!div class="step-by-step"]
> [前へ](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
> [次へ](understanding-asp-net-ajax-web-services.md)

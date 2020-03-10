---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
title: 開発と運用の間の一般的な構成の違い (VB) |Microsoft Docs
author: rick-anderson
description: 前のチュートリアルでは、開発環境から運用環境に関連するすべてのファイルをコピーして、web サイトをデプロイしました。 しかし、
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 548e75f6-4d6c-4cb4-8da8-417915eb8393
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
msc.type: authoredcontent
ms.openlocfilehash: cc65af6eb4fca8b3b805e11e26da468a958a4221
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513250"
---
# <a name="common-configuration-differences-between-development-and-production-vb"></a>開発と運用の間の一般的な構成の違い (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[[Download PDF]\(PDF をダウンロード\)](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial05_ConfigDifferences_vb.pdf)

> 前のチュートリアルでは、開発環境から運用環境に関連するすべてのファイルをコピーして、web サイトをデプロイしました。 ただし、環境によって構成に違いがあることは珍しくありません。そのため、各環境には一意の Web.config ファイルが必要です。 このチュートリアルでは、一般的な構成の違いについて説明し、個別の構成情報を保持するための戦略について説明します。

## <a name="introduction"></a>はじめに

最後の2つのチュートリアルでは、単純な web アプリケーションのデプロイについて紹介します。 [*Ftp クライアントを使用したサイトのデプロイ*](deploying-your-site-using-an-ftp-client-vb.md)に関するチュートリアルでは、スタンドアロン ftp クライアントを使用して、開発環境から運用環境に必要なファイルをコピーする方法について説明しました。 前のチュートリアル「 [*Visual Studio を使用したサイト*](deploying-your-site-using-visual-studio-vb.md)のデプロイ」では、visual studio の [Web サイトツールのコピー] と [発行] オプションを使用したデプロイについて説明しました。 どちらのチュートリアルでも、運用環境のすべてのファイルは、開発環境のファイルのコピーでした。 ただし、運用環境の構成ファイルは、開発環境とは異なる場合があります。 Web アプリケーションの構成は `Web.config` ファイルに格納され、通常、データベース、web、電子メールサーバーなどの外部リソースに関する情報が含まれます。 また、ハンドルされない例外が発生した場合に実行するアクションなど、特定の状況におけるアプリケーションの動作も明らかにします。

Web アプリケーションを展開するときは、正しい構成情報が運用環境で終了することが重要です。 ほとんどの場合、開発環境の `Web.config` ファイルを実稼働環境にそのままコピーすることはできません。 代わりに、カスタマイズされたバージョンの `Web.config` を運用環境にアップロードする必要があります。 このチュートリアルでは、いくつかの一般的な構成の違いについて簡単に説明します。また、環境間でさまざまな構成情報を維持するためのいくつかの手法についても説明します。

## <a name="typical-configuration-differences-between-the-development-and-production-environments"></a>開発環境と運用環境の一般的な構成の違い

`Web.config` ファイルには、ASP.NET アプリケーションの構成情報が含まれています。 この構成情報の一部は、環境に関係なく同じです。 たとえば、`Web.config` ファイルの `<authentication>` 要素と `<authorization>` 要素に記載されている認証設定と URL 承認規則は、通常、環境に関係なく同じです。 ただし、外部リソースに関する情報などの他の構成情報は、通常、環境によって異なります。

データベース接続文字列は、環境によって異なる構成情報の代表的な例です。 Web アプリケーションがデータベースサーバーと通信するときは、まず接続を確立する必要があり、[接続文字列](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)を使用して処理を行います。 データベース接続文字列は、web ページまたはデータベースに接続するコード内で直接ハードコーディングすることができますが、接続文字列情報が1つの一元化された場所にあるように、`Web.config`の[`<connectionStrings>` 要素](https://msdn.microsoft.com/library/bf7sd233.aspx)に配置することをお勧めします。 開発時には、運用環境で使用されるデータベースとは異なるデータベースが使用されることがよくあります。このため、接続文字列情報は環境ごとに一意である必要があります。

> [!NOTE]
> 今後のチュートリアルでは、データドリブンアプリケーションのデプロイについて説明します。この時点で、データベース接続文字列を構成ファイルに格納する方法の詳細について説明します。

開発環境と運用環境の動作はかなり異なります。 開発環境での web アプリケーションの作成、テスト、およびデバッグは、開発者の小さなグループによって行われます。 運用環境では、同じアプリケーションが多数の異なる同時ユーザーによってアクセスされています。 ASP.NET には、開発者がアプリケーションのテストとデバッグを支援する多くの機能が含まれていますが、運用環境でのパフォーマンスとセキュリティ上の理由から、これらの機能を無効にする必要があります。 そのような構成設定をいくつか見てみましょう。

### <a name="configuration-settings-that-impact-performance"></a>パフォーマンスに影響する構成設定

ASP.NET ページに初めてアクセスしたとき (または、初めて変更された後)、その宣言型マークアップをクラスに変換し、このクラスをコンパイルする必要があります。 Web アプリケーションが自動コンパイルを使用する場合は、ページの分離コードクラスもコンパイルする必要があります。 `Web.config` ファイルの[`<compilation>` 要素](https://msdn.microsoft.com/library/s10awwz0.aspx)を使用して、一連のコンパイルオプションを構成できます。

Debug 属性は、`<compilation>` 要素の中で最も重要な属性の1つです。 `debug` 属性が "true" に設定されている場合、コンパイルされたアセンブリには、Visual Studio でアプリケーションをデバッグするときに必要なデバッグシンボルが含まれます。 ただし、デバッグシンボルはアセンブリのサイズを増やし、コードの実行時に追加のメモリ要件を強制します。 さらに、`debug` 属性が "true" に設定されている場合、`WebResource.axd` によって返されるコンテンツはキャッシュされません。つまり、ユーザーがページにアクセスするたびに、`WebResource.axd`によって返された静的コンテンツを再ダウンロードする必要があります。

> [!NOTE]
> `WebResource.axd` は、ASP.NET 2.0 で導入された組み込みの HTTP ハンドラーであり、サーバーコントロールは、スクリプトファイル、画像、CSS ファイル、その他のコンテンツなどの埋め込みリソースを取得するために使用します。 `WebResource.axd` のしくみと、それを使用してカスタムサーバーコントロールから埋め込みリソースにアクセスする方法の詳細については、「 [`WebResource.axd`を使用した URL を使用した埋め込みリソース](http://aspnet.4guysfromrolla.com/articles/080906-1.aspx)へのアクセス」を参照してください。

`<compilation>` 要素の `debug` 属性は、通常、開発環境では "true" に設定されます。 実際、web アプリケーションをデバッグするには、この属性を "true" に設定する必要があります。Visual Studio から ASP.NET アプリケーションをデバッグしようとしたときに、`debug` 属性が "false" に設定されている場合、Visual Studio では、`debug` 属性が "true" に設定され、この変更を行うようになるまで、アプリケーションをデバッグできないことを示すメッセージが表示されます。

運用環境では、パフォーマンスに影響を与えるため、`debug` 属性を "true" に設定することはでき**ません**。 このトピックの詳細については、 [Scott Guthrie](https://weblogs.asp.net/scottgu/)のブログ記事「 [`debug="true"` が有効になっている運用環境の ASP.NET アプリケーションを実行しない](https://weblogs.asp.net/scottgu/442448)」を参照してください。

### <a name="custom-errors-and-tracing"></a>カスタムエラーとトレース

ASP.NET アプリケーションでハンドルされない例外が発生すると、次の3つのうちのいずれかが発生した時点で、ランタイムに対してバブルアップします。

- 汎用ランタイムエラーメッセージが表示されます。 このページでは、ランタイムエラーが発生したことがユーザーに通知されますが、エラーの詳細は提供されません。
- 例外の詳細メッセージが表示されます。これには、スローされた例外に関する情報が含まれます。
- カスタムエラーページが表示されます。これは、目的のメッセージを表示するために作成する ASP.NET ページです。

未処理の例外が発生した場合の処理は、`Web.config` ファイルの[`<customErrors>` セクション](https://msdn.microsoft.com/library/h0hfz6fc.aspx)によって異なります。

アプリケーションを開発およびテストする場合は、ブラウザーで例外の詳細を確認するのに役立ちます。 ただし、運用環境のアプリケーションで例外の詳細を表示すると、セキュリティ上のリスクが生じる可能性があります。 さらに、unflattering があり、web サイトが不自然見えるになります。 理想的には、ハンドルされない例外が発生した場合に、開発環境の web アプリケーションは例外の詳細を表示しますが、運用環境の同じアプリケーションではカスタムエラーページが表示されます。

> [!NOTE]
> 既定の `<customErrors>` セクションの設定では、ページが localhost を介してアクセスされている場合にのみ例外の詳細メッセージが表示され、それ以外の場合は汎用ランタイムエラーページが表示されます。 これは理想的ではありませんが、既定の動作によって、ローカル以外の訪問者に対する例外の詳細が明らかにならないことを理解しておく必要があります。 今後のチュートリアルでは、`<customErrors>` のセクションについて詳しく説明し、運用環境でエラーが発生したときにカスタムエラーページを表示する方法を示します。

開発時に役立つもう1つの ASP.NET 機能はトレースです。 トレースを有効にすると、受信した各要求に関する情報が記録され、最近の要求の詳細を表示するための特別な web ページ `Trace.axd`が提供されます。 トレースは、`Web.config`の[`<trace>` 要素](https://msdn.microsoft.com/library/6915t83k.aspx)を使用して有効にし、構成することができます。

トレースを有効にした場合は、運用環境で無効になっていることを確認してください。 トレース情報には cookie、セッションデータ、およびその他の機密情報が含まれているため、運用環境でトレースを無効にすることが重要です。 既定では、トレースは無効になっています。また、`Trace.axd` ファイルには localhost を通じてのみアクセスできます。 開発でこれらの既定の設定を変更した場合は、運用環境でそれらの設定がオフになっていることを確認してください。

## <a name="techniques-for-maintaining-separate-configuration-information"></a>個別の構成情報を保持するための手法

開発環境と運用環境の構成設定が異なると、デプロイプロセスが複雑になります。 前の2つのチュートリアルでは、デプロイプロセスによって、必要なすべてのファイルが開発環境から運用環境にコピーされましたが、その方法は、両方の環境で構成情報が同じ場合にのみ機能します。 さまざまな構成情報を使用してアプリケーションを展開するには、さまざまな方法があります。 ホストされている web アプリケーションに対して、これらのオプションの一部をカタログ化してみましょう。

### <a name="manually-deploying-the-production-environment-configuration-file"></a>運用環境の構成ファイルを手動で展開する

最も簡単な方法は、`Web.config` ファイルの2つのバージョンを保持することです。1つは開発環境用で、もう1つは運用環境用です。 サイトを運用環境に展開するには、`Web.config` ファイルを*除き*、開発環境で運用サーバーにすべてのファイルをコピーすることがあります。 代わりに、運用環境固有の `Web.config` ファイルが運用環境にコピーされます。

この方法は非常に洗練されていませんが、構成情報があまり頻繁に変更されないため、簡単に実装できます。 これは、1つの web サーバーでホストされ、構成情報が頻繁に変更されない小規模な開発チームのアプリケーションに最適です。 スタンドアロン FTP クライアントを使用してアプリケーションファイルを手動で展開する場合は、この方法が最も高くなります。 Visual Studio の [Web サイトのコピー] ツールまたは [発行] オプションを使用する場合は、展開する前に、配置固有の `Web.config` ファイルを実稼働固有のファイルにスワップアウトしてから、配置の完了後にスワップする必要があります。

### <a name="change-the-configuration-during-the-build-or-deployment-process"></a>ビルドまたは配置プロセス中に構成を変更する

これまでに説明したのは、アドホックビルドとデプロイプロセスを想定したものです。 多くの大規模なソフトウェアプロジェクトには、オープンソース、ホーム拡張、またはサードパーティ製のツールを利用する、より形式化されたプロセスがあります。 このようなプロジェクトでは、運用環境にプッシュする前に構成情報を適切に変更するように、ビルドまたは配置プロセスをカスタマイズできます。 [MSBuild](http://en.wikipedia.org/wiki/MSBuild)、 [NAnt](http://nant.sourceforge.net/)、またはその他のビルドツールを使用して web アプリケーションをビルドする場合、ビルドステップを追加して、`Web.config` ファイルを変更して、実稼働固有の設定を含めることができます。 または、展開ワークフローがプログラムを使用してソース管理サーバーに接続し、適切な `Web.config` ファイルを取得することもできます。

運用環境に適切な構成情報を取得する実際の方法は、ツールとワークフローによって大きく異なります。 そのため、このトピックについては詳しく説明しません。 MSBuild や NAnt などの一般的なビルドツールを使用している場合は、web 検索を使用して、これらのツールに固有のデプロイの記事とチュートリアルを見つけることができます。

### <a name="managing-configuration-differences-via-the-web-deployment-project-add-in"></a>Web 配置プロジェクトアドインを使用した構成の違いの管理

2006では、Microsoft は Visual Studio 2005 用の Web 開発プロジェクトアドインをリリースしました。 Visual Studio 2008 用のアドインが2008でリリースされました。 このアドインを使用すると、ASP.NET 開発者は web アプリケーションプロジェクトと共に個別の Web 配置プロジェクトを作成できます。このプロジェクトは、ビルドされると、web アプリケーションを明示的にコンパイルし、ローカル出力ディレクトリに配置するためにファイルをコピーします。 Web アプリケーションプロジェクトでは、バックグラウンドで MSBuild を使用します。

既定では、開発環境の `Web.config` ファイルは出力ディレクトリにコピーされますが、Web 配置プロジェクトを設定して、

このディレクトリにコピーされる構成情報は、次の方法で設定します。

- 置換するセクションと置換テキストを含む XML ファイルを指定する、`Web.config` file セクションの置換。
- 外部構成ソースファイルへのパスを指定する。 このオプションを選択すると、Web 配置プロジェクトは、(開発環境で使用される `Web.config` ファイルではなく) 特定の `Web.config` ファイルを出力ディレクトリにコピーします。
- Web 配置プロジェクトによって使用される MSBuild ファイルにカスタム規則を追加します。

Web アプリケーションを配置するには、Web 配置プロジェクトをビルドし、プロジェクトの出力フォルダーから運用環境にファイルをコピーします。

Web デプロイプロジェクトの使用方法の詳細については、 [MSDN マガジン](https://msdn.microsoft.com/magazine/default.aspx)の2007年4月の問題から[この web デプロイプロジェクト](https://msdn.microsoft.com/magazine/cc163448.aspx)に関する記事をご覧ください。または、このチュートリアルの最後にある「関連項目」のリンクを参照してください。

> [!NOTE]
> Web 配置プロジェクトは Visual Studio アドインとして実装されており、Visual Studio Express エディション (Visual Web Developer を含む) ではアドインがサポートされていないため、Visual Web Developer では Web 配置プロジェクトを使用できません。

## <a name="summary"></a>まとめ

開発における web アプリケーションの外部リソースと動作は、通常、同じアプリケーションが運用環境にある場合とは異なります。 たとえば、データベース接続文字列、コンパイルオプション、および処理されない例外が発生した場合の動作は、通常、環境によって異なります。 デプロイプロセスでは、これらの違いに対応する必要があります。 このチュートリアルで説明したように、最も簡単な方法は、代替構成ファイルを運用環境に手動でコピーすることです。 Web 配置プロジェクトアドインを使用する場合や、このようなカスタマイズに対応できる、より形式化されたビルドまたは展開プロセスを使用する場合は、より洗練されたソリューションが可能です。

プログラミングを楽しんでください。

### <a name="further-reading"></a>参考資料

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [接続文字列の説明](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)
- [データベース接続文字列 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [`debug="true"` が有効になっている運用環境の ASP.NET アプリケーションを実行しない](https://weblogs.asp.net/scottgu/Don_1920_t-run-production-ASP.NET-Applications-with-debug_3D001D20_true_1D20_-enabled)
- [未処理の例外への適切な応答-ユーザーフレンドリなエラーページの表示](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [操作方法: Visual Studio 2008 Web 配置プロジェクトを使用する](../../../videos/how-do-i/how-do-i-use-a-visual-studio-2008-web-deployment-project.md)
- [データベースを配置するときのキーの構成設定](http://aspnet.4guysfromrolla.com/articles/121008-1.aspx)
- Visual studio [2008 web 配置プロジェクトのダウンロード](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) | [Visual Studio 2005 web 配置プロジェクトのダウンロード](https://download.microsoft.com/download/9/4/9/9496adc4-574e-4043-bb70-bc841e27f13c/WebDeploymentSetup.msi)
- [Vs 2008 Web 配置](https://weblogs.asp.net/scottgu/archive/2005/11/06/429723.aspx)プロジェクト | [Vs 2008 web 配置プロジェクトのサポートがリリース](https://weblogs.asp.net/scottgu/archive/2008/01/28/vs-2008-web-deployment-project-support-released.aspx)されました
- [Web 配置プロジェクト](https://msdn.microsoft.com/magazine/cc163448.aspx)

> [!div class="step-by-step"]
> [前へ](deploying-your-site-using-visual-studio-vb.md)
> [次へ](core-differences-between-iis-and-the-asp-net-development-server-vb.md)

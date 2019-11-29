---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/more-patterns-and-guidance
title: その他のパターンとガイダンス (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7e97cfc3-d830-4002-8ff7-5790d1ff49e6
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/more-patterns-and-guidance
msc.type: authoredcontent
ms.openlocfilehash: afade34477d1136883e7543d09e73dfbe435690e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585362"
---
# <a name="more-patterns-and-guidance-building-real-world-cloud-apps-with-azure"></a>その他のパターンとガイダンス (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson]((https://twitter.com/RickAndMSFT))、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

ここでは、クラウドコンピューティングを成功させる方法についてのガイダンスを提供する13のパターンを見てきました。 これらは、クラウドアプリに適用されるパターンのほんの一部です。 ここでは、クラウドコンピューティングに関するいくつかのトピックと、それらに役立つリソースを紹介します。

- 既存のオンプレミスアプリケーションをクラウドに移行しています。 

    - [アプリケーションをクラウドに移行して](https://msdn.microsoft.com/library/ff728592.aspx)います。 Microsoft のパターンとプラクティスによる電子書籍。 [ハードコピーペーパーバック](https://www.amazon.com/dp/1621140202)としても使用できます。
    - [Microsoft の ASP.NET と IIS.NET を移行して](https://go.microsoft.com/fwlink/?LinkId=400656)います。 Robert McMurray によるケーススタディ。
    - [4 番目の &amp; Mayor を Azure websites に移行](http://www.jeff.wilcox.name/2013/04/4thandmayor-azure-websites/)しています。 Jeff Wilcox chronicling のブログ投稿では、Azure App Service で web アプリをアマゾンウェブサービスから Web Apps に移行しています。
    - [Azure へのアプリの移動: どのような変更がありますか?](https://azure.microsoft.com/documentation/videos/web-sites-internals-and-the-file-system/) Stefan の短いビデオ、Azure App Service の Web Apps でのファイルシステムアクセスについて説明します。
    - [Azure ハイブリッドクラウド](https://www.amazon.com/dp/B00EOP4UQW)。 Danny Garber、Jamal M氏 k、および Adam Fazio によるコピー物または電子書籍。
- クラウドアプリケーションに固有のセキュリティ、認証、および承認の問題

    - [Azure のセキュリティガイダンス](https://azure.microsoft.com/blog/2014/02/10/best-practices-windows-azure-websites-waws/)
    - [Microsoft のパターンとプラクティス-Azure のガイダンス](https://msdn.microsoft.com/library/dn568099.aspx)。 「ゲートキーパーパターン」、「フェデレーション Id パターン」を参照してください。
    - [Azure のネットワークセキュリティ](https://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx)。 内容 ashwin の Ashin よるホワイトペーパー。

「 [Microsoft のパターンとプラクティス-Azure のガイダンス](https://msdn.microsoft.com/library/dn568099.aspx)」で、追加のクラウドコンピューティングパターンとガイダンスも参照してください。

<a id="resources"></a>
## <a name="resources"></a>リソース

この電子ブックの各章には、その特定のトピックの詳細についてのリソースへのリンクが記載されています。 次の一覧は、Azure でのクラウド開発を成功させるためのベストプラクティスと推奨されるパターンの概要へのリンクを示しています。

Documentation

- [Azure Cloud Services で大規模なサービスを設計するためのベストプラクティス](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 マーク Simm と Michael Thomassy によるホワイトペーパー。
- [フェイルセーフ: 回復力のあるクラウドアーキテクチャに関するガイダンス](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 ホワイトペーパー (Marc Mercuri、Ulrich Homann、Andrew Townhill)。 フェールセーフビデオシリーズの Web ページバージョン。
- [Azure のガイダンス](https://azure.microsoft.com/develop/net/guidance/)Azure 用アプリケーションの開発に関連する公式ドキュメントのポータルページです。

Videos

- [Azure を使用した実際のクラウドアプリの構築-パート 1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)と[パート 2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325) この電子書籍の基になっている Scott Guthrie によるプレゼンテーションのビデオ。 2013年9月のオーストラリアに発表されています。 同じプレゼンテーションの以前のバージョンは、2013年6月: [NDC part 1](http://vimeo.com/68215538), [NDC part 2](http://vimeo.com/68215602)で、ノルウェーの開発者のカンファレンス (NDC) で提供されています。
- [フェイルセーフ: スケーラブルで回復力のある Cloud Services を構築](https://channel9.msdn.com/Series/FailSafe)します。 Ulrich Homann、Marc Mercuri、Mark Simm による9部構成のビデオシリーズ。 クラウドアプリを設計する方法の400レベルのビューについて説明します。 このシリーズでは、理論上、推奨されるパターンの背後にある理由を中心に説明します。詳細については、「Simm」を参照してください。
- [大規模なビルド: Azure のお客様から学んだ教訓-パート 1](https://channel9.msdn.com/Events/Build/2012/3-029)と[パート 2](https://channel9.msdn.com/Events/Build/2012/3-030)。 Simon Davies と Mark Simm による2部構成のビデオシリーズ。フェイルセーフシリーズに似ていますが、実際の実装についてはこちらを参照してください。

コード サンプル

- [この電子書籍に付随する修正プログラムを適用し](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4?cdn_id=2013-12-03-002)ます。
- [Visual Studio 2012 C#向けの Azure におけるクラウドサービスの基礎](https://aka.ms/csf)。 Microsoft Code Gallery サイトのダウンロード可能なプロジェクトには、Microsoft カスタマーアドバイザリチーム (CAT) によって開発されたコードとドキュメントの両方が含まれています。 フェイルセーフで擁護、ビッグビデオシリーズおよびフェイルセーフホワイトペーパーを構築するためのベストプラクティスの多くを紹介します。 コードギャラリーのページでは、プロジェクトの作成者による広範なドキュメントへのリンクもあります。特に、プロジェクトの説明の先頭付近にある青いボックスの「[クラウドサービスの基礎 wiki コレクション](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx)」リンクを参照してください。 このプロジェクトとドキュメントは積極的に開発中であり、類似しているが古いホワイトペーパーよりも多くのトピックに関する情報をお勧めします。

ハードコピーブック

- [クラウドコンピューティング Bible](https://www.amazon.com/dp/0470903562)。 Barrie Sosinsky。
- [リリース: 運用環境に対応したソフトウェアを設計して展開し](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)ます。 Nygard。
- [クラウドアーキテクチャパターン: Microsoft Azure の使用](http://shop.oreilly.com/product/0636920023777.do)。 請求書別。
- [Windows Azure プラットフォーム](https://www.amazon.com/dp/1430235632)。 Tejaswi よる Redkar。
- [スタートアップのための Windows Azure プログラミングパターン](https://www.amazon.com/dp/1849685606)。 Riccardo muti します。
- [Microsoft Windows Azure 開発クックブック](https://www.amazon.com/dp/1849682224)。 Neil Mackenzie。

最後に、実際のアプリの構築を開始して Azure で実行すると、おそらく専門家のサポートが必要になります。 [Azure フォーラムや StackOverflow](https://azure.microsoft.com/support/forums/)などのコミュニティサイトで質問することができます。また、azure サポートについては、Microsoft に直接問い合わせることもできます。 Microsoft では、いくつかのレベルのテクニカルサポートを提供しています。オプションの概要と比較については、「 [azure のサポート](https://azure.microsoft.com/support/plans/)」を参照してください。

<a id="acknowledgments"></a>
## <a name="acknowledgments"></a>謝辞

このコンテンツは、Tom Dykstra、Rick Anderson、Mike Wasson によって作成されました。 元のコンテンツの大部分は[Scott Guthrie](https://weblogs.asp.net/scottgu/)からのものであり、Mark Simm と Microsoft カスタマーアドバイザリチーム (CAT) から資料を描きました。

Microsoft の他の多くの同僚が、下書きやコードについて確認し、コメントをしています。

- Tim Ammann-automation の章を確認します。
- Christopher Bennage-修正プログラムのコードを確認し、テストします。
- ライアン Berry-CD/CI の章を確認します。
- Vittorio を参照してください。 SSO の章を確認します。
- Chris Clayton-PowerShell スクリプトの技術的な問題を解決するのに役立ちます。
- Conor Cunningham-データストレージオプションの章を確認します。
- Carlos Farre-セキュリティの問題の修正 It コードを確認し、テストします。
- Larry Franks-テレメトリと監視に関する章を確認します。
- Jonathan を参照してください。データストレージオプションの章の Hadoop と MapReduce のセクションを確認します。
- Sidney Higa-すべての章を確認します。
- Gordon Hogenson-ソース管理の章を確認します。
- Tamra は、データストレージのオプション、blob、およびキューに関する章を確認します。
- Pranav Rastogi-SSO の章を確認します。
- June Blender Rogers-PowerShell オートメーションスクリプトへのエラー処理とヘルプを追加しました。
- Mani Subramanian-すべての章を確認し、コードレビューとテストプロセスを実行して、It コードを修正しました。
- Shaun Tinline-Jones-データのパーティション分割の章を確認します。
- Selcin Tukarslan-SQL Database と SQL Server について説明している章をレビューします。
- SSO 章用の Edward Wu によって提供されるサンプルコードです。
- Guang Yang-PowerShell オートメーションスクリプトを記述しました。

[Microsoft Developer ガイダンスアドバイザリ・協議会](https://aka.ms/DGAC)(dgac) のメンバーも、次のように下書きをレビューし、コメントにしています。

- Jean-Luc Boucho
- Catalin Gheorghiu
- Wouter de Kort
- Carlos dos Santos
- Neil Mackenzie
- デ nis の息子 son
- Sunil Sabat
- [Aleksey Sinyagin](http://www.linkedin.com/in/sinyagin)
- 請求 Wagner
- Michael ウッド

DGAC の他のメンバーについては、事前の概要について確認し、コメントをします。

- Damir Arh
- Edward Bakker
- Srdjan Bozの会社
- マニュアルのチャン・チャンネル
- Gianni Rosa Gallina
- パウロ Morgado
- Jason Oliveira
- Alberto Poblacion
- ライアン Riley
- Perez Jones Tsisah
- Roger ホワイトヘッド
- Pawel Wilkosz

> [!div class="step-by-step"]
> [前へ](queue-centric-work-pattern.md)
> [次へ](the-fix-it-sample-application.md)

---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: ソース管理 (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/23/2015
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: 5a1e0d7cd3c396d4be79c8958422602055eb3db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500530"
---
# <a name="source-control-building-real-world-cloud-apps-with-azure"></a>ソース管理 (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

ソース管理は、チーム環境だけでなく、すべてのクラウド開発プロジェクトに不可欠です。 ソースコードを編集したり、元に戻す機能や自動バックアップを使用せずに Word 文書を編集したりすることはできません。また、ソース管理を使用すると、これらの機能をプロジェクトレベルで実行できるので、問題が発生した場合により多くの時間を節約できます。 クラウドソース管理サービスを使用すると、複雑なセットアップについて心配する必要がなくなります。また、最大5人のユーザーに対して Azure Repos ソース管理を無料でご利用いただけます。

この章の最初の部分では、次の3つの重要なベストプラクティスについて説明します。

- [オートメーションスクリプトをソースコードとして扱い](#scripts)、アプリケーションコードと共にバージョンを作成します。
- シークレット (資格情報などの機密データ) をソースコードリポジトリに[チェックインしないで](#secrets)ください。
- [ソースブランチを設定](#devops)して、DevOps ワークフローを有効にします。

この章の残りの部分では、Visual Studio、Azure、および Azure Repos でこれらのパターンを実装する例をいくつか示します。

- [Visual Studio でソース管理にスクリプトを追加する](#vsscripts)
- [Azure に機密データを格納する](#appsettings)
- [Visual Studio で Git を使用して Azure Repos](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a>オートメーションスクリプトをソースコードとして扱う

クラウドプロジェクトで作業している場合は、頻繁に変更を行い、顧客から報告された問題に迅速に対応できるようにしたいと考えています。 迅速に対応するには、「[すべてを自動化](automate-everything.md)する」の章で説明されているように、自動化スクリプトを使用します。 環境の作成、デプロイ、スケーリングなどに使用するすべてのスクリプトは、アプリケーションのソースコードと同期している必要があります。

スクリプトをコードと同期させておくには、ソース管理システムにスクリプトを保存します。 その後、変更をロールバックするか、開発コードとは異なる実稼働コードをすばやく修正する必要がある場合は、どの設定が変更されたか、またはどのチームメンバーが必要なバージョンのコピーを保持しているかを追跡する時間を無駄にする必要がありません。 必要なスクリプトは、必要なコードベースと同期され、すべてのチームメンバーが同じスクリプトを使用することが確実になります。 次に、運用環境または新機能の開発に対する修正プログラムのテストと展開を自動化する必要があるかどうかにかかわらず、更新する必要があるコードに適したスクリプトが用意されています。

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a>シークレットをチェックインしない

通常、ソースコードリポジトリは、パスワードなどの機密データを適切にセキュリティで保護された場所に配置するために、多くのユーザーにアクセスできます。 スクリプトがパスワードなどのシークレットに依存している場合は、これらの設定をパラメーター化してソースコードに保存しないようにし、他の場所にシークレットを格納します。

たとえば、Azure では、発行プロファイルの作成を自動化するために、発行設定を含むファイルをダウンロードできます。 これらのファイルには、Azure サービスの管理を許可されているユーザー名とパスワードが含まれます。 この方法を使用して発行プロファイルを作成した場合、これらのファイルをソース管理にチェックインすると、リポジトリへのアクセス権を持つユーザーは、それらのユーザー名とパスワードを参照できます。 パスワードは暗号化されていて、既定ではソース管理に含まれていない*pubxml ユーザー*ファイルに格納されているため、発行プロファイル自体に安全に保存できます。

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a>DevOps ワークフローを容易にする構造ソースブランチ

リポジトリにブランチを実装する方法によって、新しい機能を開発し、運用環境で問題を修正する機能が変わります。 中規模のチームが使用しているパターンを次に示します。

![ソースブランチ構造](source-control/_static/image1.png)

Master 分岐は、常に運用環境にあるコードと一致します。 マスターの下にある分岐は、開発ライフサイクルのさまざまな段階に対応します。 開発分岐では、新機能を実装します。 小規模なチームでは、マスターと開発のみが必要ですが、多くの場合、開発とマスターの間にステージングブランチを作成することをお勧めします。 更新を運用環境に移行する前に、ステージングを使用して最終的な統合テストを行うことができます。

大規模なチームでは、新しい機能ごとに個別の分岐が存在する可能性があります。小規模なチームの場合、開発ブランチにチェックインする人がいます。

各機能の分岐がある場合、機能 A の準備が整ったら、ソースコードの変更を開発ブランチにマージし、その他の機能分岐にマージします。 このソースコードのマージ処理には時間がかかることがあります。また、機能を個別に維持したまま作業を回避するために、一部のチームは機能の *[切り替え](http://en.wikipedia.org/wiki/Feature_toggle)* (*機能フラグ*とも呼ばれます) と呼ばれる代替手段を実装しています。 これは、すべての機能のすべてのコードが同じ分岐にあることを意味しますが、コードのスイッチを使用して各機能を有効または無効にします。 たとえば、機能 A が It アプリのタスクを修正するための新しいフィールドであるとします。機能 B はキャッシュ機能を追加します。 両方の機能のコードは development 分岐に配置できますが、アプリは変数が true に設定されている場合にのみ新しいフィールドを表示し、異なる変数が true に設定されている場合にのみキャッシュを使用します。 機能 A を昇格する準備ができていないにもかかわらず、機能 B の準備ができている場合は、スイッチをオフにして機能 B をオンにして、すべてのコードを運用環境に昇格させることができます。 これにより、機能 A を完了し、後でソースコードをマージせずに昇格させることができます。

機能の分岐または切り替えを使用するかどうかにかかわらず、このような分岐構造では、開発からコードをアジャイルで反復的な方法で運用環境にフローさせることができます。

この構造により、お客様のフィードバックに迅速に対応することもできます。 実稼働環境にすばやく修正を加える必要がある場合は、それをアジャイルな方法で効率的に実行することもできます。 マスターまたはステージングから分岐を作成できます。また、マスターと機能の分岐にマージする準備ができたら、ブランチを作成できます。

![修正プログラムブランチ](source-control/_static/image2.png)

このような分岐構造を使用して運用と開発の分岐が分離されていない場合、運用上の問題によって、新しい機能コードを運用環境の修正プログラムと共に昇格させる必要があります。 新しい機能コードは完全にテストされていない場合があり、運用環境での準備が整っていない可能性があり、準備ができていない変更をバックアップするために大量の作業が必要になる場合があります。 または、変更をテストしてデプロイの準備を整えるために、修正を遅らせることが必要になる場合があります。

次に、Visual Studio、Azure、および Azure Repos でこれら3つのパターンを実装する方法の例を紹介します。 これらの例は、詳細なステップバイステップの手順ではありません。必要なすべてのコンテキストを提供する詳細な手順については、章の最後にある「 [resources](#resources) 」セクションを参照してください。

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a>Visual Studio でソース管理にスクリプトを追加する

Visual studio でソース管理にスクリプトを追加するには、visual studio のソリューションフォルダーにスクリプトを追加します (プロジェクトがソース管理内にあることを前提としています)。 これを行う1つの方法を次に示します。

ソリューションフォルダー ( *.sln*ファイルと同じフォルダー) にスクリプト用のフォルダーを作成します。

![Automation フォルダー](source-control/_static/image3.png)

スクリプトファイルをフォルダーにコピーします。

![Automation フォルダーの内容](source-control/_static/image4.png)

Visual Studio で、ソリューションフォルダーをプロジェクトに追加します。

![新しいソリューションフォルダーメニューの選択](source-control/_static/image5.png)

スクリプトファイルをソリューションフォルダーに追加します。

![[既存項目の追加] メニューの選択](source-control/_static/image6.png)

![[既存項目の追加] ダイアログ ボックス](source-control/_static/image7.png)

これで、スクリプトファイルがプロジェクトに含まれるようになりました。ソース管理は、対応するソースコードの変更と共にバージョンの変更を追跡しています。

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a>Azure に機密データを格納する

Azure の Web サイトでアプリケーションを実行する場合、資格情報をソース管理に保存しないようにする方法の1つとして、資格情報を Azure に保存する方法があります。

たとえば、It アプリケーションの修正プログラムでは、運用環境のパスワードを持つ2つの接続文字列と、Azure ストレージアカウントへのアクセスを提供するキーが web.config ファイルに格納されます。

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

これらの設定の実際の実稼働値を web.config*ファイルに*配置する場合、または配置時に挿入するように*web.config の変換*を構成するために web.config ファイルに配置する場合は、ソースリポジトリに格納されます。 実稼働発行プロファイルにデータベース接続文字列を入力すると、そのパスワードが*pubxml*ファイルに挿入されます。 ( *Pubxml*ファイルをソース管理から除外することもできますが、その他のすべての展開設定を共有する利点は失われます)。

Azure に*は、web.config ファイル*の**appSettings**と接続文字列のセクションの代替手段が用意されています。 Azure 管理ポータルでの web サイトの **[構成]** タブの関連部分を次に示します。

![ポータルでの appSettings と connectionStrings](source-control/_static/image8.png)

この web サイトにプロジェクトを配置し、アプリケーションを実行すると、Azure に格納した値によって、web.config ファイル内の値が上書きされます。

これらの値は、管理ポータルまたはスクリプトを使用して Azure で設定できます。 「[すべて自動化](automate-everything.md)」の章で説明した環境作成の自動化スクリプトは、Azure SQL Database を作成し、ストレージと SQL Database 接続文字列を取得して、これらのシークレットを web サイトの設定に保存します。

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

実際の値がソースリポジトリに保存されないように、スクリプトがパラメーター化されていることに注意してください。

開発環境でローカルに実行すると、アプリはローカルの web.config ファイルを読み取り、接続文字列は、web プロジェクトの*app\_Data*フォルダー内の LocalDB SQL Server データベースを参照します。 アプリを Azure で実行し、アプリが web.config ファイルからこれらの値を読み取ろうとすると、実際には、web.config ファイルの内容ではなく、web サイトに格納されている値が返されます。

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-azure-devops"></a>Visual Studio と Azure DevOps で Git を使用する

任意のソース管理環境を使用して、前に示した DevOps 分岐構造体を実装できます。 分散型チームの場合、[分散型バージョン管理システム](http://en.wikipedia.org/wiki/Distributed_revision_control)(dvcs) が最適な場合があります。他のチームにとっては、一元化された[システム](http://en.wikipedia.org/wiki/Revision_control)の機能が向上する可能性があります。

[Git](http://git-scm.com/)は、広く普及している分散型バージョン管理システムです。 ソース管理に Git を使用すると、ローカルコンピューター上のすべての履歴と共にリポジトリの完全なコピーが作成されます。 ネットワークに接続していない場合でも作業を続行できるので、多くのユーザーは、引き続きコミットとロールバックを実行したり、分岐を作成して切り替えることができます。 ネットワークに接続している場合でも、ブランチを作成したり、すべてがローカルの場合に分岐を切り替えたりする方が簡単で高速です。 また、他の開発者に影響を与えることなく、ローカルのコミットとロールバックを行うこともできます。 また、コミットをバッチ処理してからサーバーに送信することもできます。

[Azure Repos](/azure/devops/repos/index?view=vsts)には、 [Git](/azure/devops/repos/git/?view=vsts)と[Team Foundation バージョン管理](/azure/devops/repos/tfvc/index?view=vsts)(TFVC、一元化されたソース管理) の両方が用意されています。 Azure DevOps の使用を開始する[」を参照](https://app.vsaex.visualstudio.com/signup)してください。

Visual Studio 2017 には、組み込みのファーストクラスの[Git サポート](https://msdn.microsoft.com/library/hh850437.aspx)が含まれています。 そのしくみを簡単に説明します。

Visual Studio でプロジェクトを開き、**ソリューションエクスプローラー**でソリューションを右クリックし、 **[ソリューションをソース管理に追加]** を選択します。

![ソース管理へのソリューションの追加](source-control/_static/image9.png)

Visual Studio は、TFVC (一元化されたバージョン管理) と Git のどちらを使用するかをたずねます。

![ソース管理の選択](source-control/_static/image10.png)

Git を選択し、 **OK** をクリックすると、Visual Studio によってソリューションフォルダーに新しいローカル Git リポジトリが作成されます。 新しいリポジトリにはまだファイルがありません。Git コミットを実行してリポジトリに追加する必要があります。 **ソリューションエクスプローラー**でソリューションを右クリックし、 **[コミット]** をクリックします。

![Commit](source-control/_static/image11.png)

Visual Studio では、コミットのすべてのプロジェクトファイルが自動的にステージングされ、 **[含まれる変更]** ウィンドウの**チームエクスプローラー**に一覧表示されます。 (コミットに追加したくないものがある場合は、それを選択して右クリックし、 **[除外]** をクリックします)。

![チーム エクスプローラー](source-control/_static/image12.png)

コミットコメントを入力し、 **[コミット]** をクリックすると、Visual Studio によってコミットが実行され、コミット ID が表示されます。

![チームエクスプローラーの変更](source-control/_static/image13.png)

ここで、リポジトリの内容とは異なるコードを変更すると、その違いを簡単に確認できます。 変更したファイルを右クリックし、 **[未変更の比較]** を選択すると、コミットされていない変更を示す比較表示が表示されます。

![未変更の状態で比較](source-control/_static/image14.png)

![変更を示す Diff](source-control/_static/image15.png)

どのような変更が加えられているかを簡単に確認できます。

たとえば、分岐を作成する必要があるとします。これは、Visual Studio でも行うことができます。 **チームエクスプローラー**で、 **[新しいブランチ]** をクリックします。

![新しいブランチのチームエクスプローラー](source-control/_static/image16.png)

分岐名を入力し、 **[分岐の作成]** をクリックすると、分岐を **[チェックアウト]** を選択した場合、新しい分岐が自動的にチェックアウトされます。

![新しいブランチのチームエクスプローラー](source-control/_static/image17.png)

これで、ファイルを変更して、このブランチにチェックインできるようになりました。 また、分岐を簡単に切り替えることができます。 Visual Studio は、チェックアウトした分岐にファイルを自動的に同期します。この例では、 *\_Layout*の web ページタイトルは、HotFix1 分岐の "ホットフィックス 1" に変更されています。

![Hotfix1 ブランチ](source-control/_static/image18.png)

Master ブランチに戻ると、 *\_Layout*ファイルの内容が、master ブランチ内の内容に自動的に戻ります。

![マスターブランチ](source-control/_static/image19.png)

この例では、分岐をすばやく作成し、分岐間を逆方向に反転する方法を簡単に説明します。 この機能により、[[すべて自動化](automate-everything.md)] の章に示されている分岐構造と自動化スクリプトを使用して、高度にアジャイルなワークフローを実現できます。 たとえば、Development 分岐で作業したり、master からホットフィックス分岐を作成したり、新しい分岐に切り替えたり、変更を加えてコミットしたりできます。その後、開発ブランチに戻り、実行した操作を続行します。

ここでは、Visual Studio でローカル Git リポジトリを使用する方法について説明しました。 チーム環境では、通常、変更を共通リポジトリにプッシュすることもできます。 また、Visual Studio tools を使用すると、リモート Git リポジトリをポイントすることもできます。 その目的に GitHub.com を使用することも、 [Git と Azure Repos](/azure/devops/repos/git/overview?view=vsts)作業項目やバグの追跡などの他のすべての Azure DevOps 機能と統合することもできます。

もちろん、これはアジャイル分岐戦略を実装する唯一の方法ではありません。 一元化されたソース管理リポジトリを使用して、同じアジャイルワークフローを有効にすることができます。

## <a name="summary"></a>まとめ

変更を加えて、安全で予測可能な方法で利用できるようになるまでの時間に基づいて、ソース管理システムの成功を測定します。 1日または2回の手動テストを行う必要があるために変更を行う必要がある場合は、その変更を分単位または最低でも1時間以内に行う必要があるかどうかを自分で確認してください。 そのための1つの方法は、継続的インテグレーションと継続的デリバリーを実装することです。これについては、[次の章](continuous-integration-and-continuous-delivery.md)で説明します。

<a id="resources"></a>
## <a name="resources"></a>リソース

分岐戦略の詳細については、次のリソースを参照してください。

- [Team Foundation Server 2012 でリリースパイプラインをビルド](https://msdn.microsoft.com/library/dn449957.aspx)します。 Microsoft のパターンとプラクティスに関するドキュメント。 分岐戦略の詳細については、第6章を参照してください。 機能を使用して機能分岐を切り替えます。機能の分岐が使用されている場合は、有効期間を短くします (時間または日単位)。
- [バージョン管理ガイド](https://aka.ms/vsarsolutions)。 ALM Rangers による分岐戦略のガイド。 [ダウンロード] タブの [分岐方法] を参照してください。
- [機能の切り替えによるソフトウェア開発](https://msdn.microsoft.com/magazine/dn683796.aspx)。 MSDN マガジンの記事です。
- [機能の切り替え](http://martinfowler.com/bliki/FeatureToggle.html)。 Martin Fowler のブログの機能の切り替え/機能フラグの概要を説明します。
- 機能によって[vs の機能分岐が切り替わり](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx)ます。 機能の切り替えに関するもう1つのブログ投稿 (Dylan Smith)

ソース管理リポジトリに保持しない機密情報を処理する方法の詳細については、次のリソースを参照してください。

- [ASP.NET と Azure App Service にパスワードやその他の機密データを展開するためのベストプラクティス](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
- [Azure websites: アプリケーション文字列と接続文字列の動作について説明](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)します。 *Web.config ファイルで*`appSettings` とデータの `connectionStrings` をオーバーライドする Azure 機能について説明します。
- [Azure websites のカスタム構成とアプリケーション設定-Stefan を使用する場合](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/)

ソース管理から機密情報を保持するその他の方法については、「 [ASP.NET MVC: ソース管理からプライベート設定を保持](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)する」を参照してください。

> [!div class="step-by-step"]
> [前へ](automate-everything.md)
> [次へ](continuous-integration-and-continuous-delivery.md)

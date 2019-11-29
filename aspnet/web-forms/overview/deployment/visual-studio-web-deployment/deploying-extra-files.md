---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 'Visual Studio を使用した ASP.NET Web 配置: 追加ファイルの配置 |Microsoft Docs'
author: tdykstra
description: このチュートリアルシリーズでは、ASP.NET web アプリケーションをデプロイ (発行) して、Web Apps またはサードパーティのホスティングプロバイダーに Azure App Service する方法について説明します。
ms.author: riande
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: eaa3141c22980f0c816e2f33b5597ac9fe69c23c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594907"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a>Visual Studio を使用した ASP.NET Web 配置: 追加ファイルの配置

[Tom Dykstra](https://github.com/tdykstra)

[スタートプロジェクトのダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> このチュートリアルシリーズでは、Visual Studio 2012 または Visual Studio 2010 を使用して、Azure App Service Web Apps またはサードパーティのホスティングプロバイダーにするために、ASP.NET web アプリケーションをデプロイ (発行) する方法について説明します。 シリーズの詳細については、[シリーズの最初のチュートリアル](introduction.md)を参照してください。

## <a name="overview"></a>の概要

このチュートリアルでは、Visual Studio web 発行パイプラインを拡張して、デプロイ中に追加のタスクを実行する方法について説明します。 このタスクでは、プロジェクトフォルダーに含まれていない余分なファイルをコピー先の web サイトにコピーします。

このチュートリアルでは、1つの追加ファイル ( *robots.txt*) をコピーします。 このファイルをステージングにデプロイしますが、運用環境には展開しません。 「[運用環境へのデプロイ](deploying-to-production.md)」チュートリアルでは、このファイルをプロジェクトに追加し、それを除外するように実稼働発行プロファイルを構成しました。 このチュートリアルでは、この状況に対処するための別の方法を紹介します。これは、配置するファイルには便利ですが、プロジェクトには含めないようにするためのものです。

## <a name="move-the-robotstxt-file"></a>Robots.txt ファイルを移動する

*Robots.txt*を処理する別の方法を準備するには、チュートリアルのこのセクションで、ファイルをプロジェクトに含まれていないフォルダーに移動し、そのステージング環境から*robots.txt*を削除します。 このファイルをステージングから削除する必要があります。これにより、その環境にファイルを展開する新しい方法が正常に機能していることを確認できます。

1. **ソリューションエクスプローラー**で、 *robots.txt*ファイルを右クリックし、 **[プロジェクトから除外]** をクリックします。
2. Windows エクスプローラーを使用して、ソリューションフォルダーに新しいフォルダーを作成し、 *ExtraFiles*という名前を指定します。
3. *ContosoUniversity*プロジェクトフォルダーから*ExtraFiles*フォルダーに*robots.txt*ファイルを移動します。

    ![ExtraFiles フォルダー](deploying-extra-files/_static/image1.png)
4. FTP ツールを使用して、[ステージング] web サイトから*robots.txt*ファイルを削除します。

    別の方法として、ステージング発行プロファイル の **設定** タブにある **ファイル発行オプション** の **宛先にある追加ファイルを削除**する を選択し、ステージングに再発行することもできます。

## <a name="update-the-publish-profile-file"></a>発行プロファイルファイルを更新する

ステージング環境には*robots.txt*のみが必要であるため、デプロイするために更新する必要がある発行プロファイルはステージングのみです。

1. Visual Studio で、[ファイル] [ *pubxml*] を開きます。
2. ファイルの末尾で、終了 `</Project>` タグの前に、次のマークアップを追加します。

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    このコードは、配置する追加ファイルを収集する新しい*ターゲット*を作成します。 ターゲットは、指定した条件に基づいて MSBuild が実行する1つ以上のタスクで構成されます。

    `Include` 属性は、ファイルを検索するフォルダーが*ExtraFiles*であり、プロジェクトフォルダーと同じレベルにあることを指定します。 MSBuild は、そのフォルダーからすべてのファイルを収集し、任意のサブフォルダーから再帰的にすべてのファイルを収集します (二重のアスタリスクは再帰サブフォルダーを指定します)。 このコードでは、複数のファイルとファイルを*ExtraFiles*フォルダー内のサブフォルダーに配置し、すべてを展開します。

    `DestinationRelativePath` 要素は、フォルダーとファイルを、 *ExtraFiles*フォルダーにあるのと同じファイルおよびフォルダー構造で、送信先 web サイトのルートフォルダーにコピーする必要があることを指定します。 *ExtraFiles*フォルダー自体をコピーする場合、`DestinationRelativePath` 値は*ExtraFiles\%(RecursiveDir)% (Filename)% (Extension)* になります。
3. ファイルの末尾で、終了 `</Project>` タグの前に、新しいターゲットをいつ実行するかを指定する次のマークアップを追加します。

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    このコードにより、コピー先のフォルダーにファイルをコピーするターゲットが実行されるたびに、新しい `CustomCollectFiles` ターゲットが実行されます。 発行と展開パッケージの作成には別のターゲットがあり、発行ではなく展開パッケージを使用して展開する場合に、両方のターゲットに新しいターゲットが挿入されます。

    *Pubxml*ファイルは、次の例のようになります。

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. *ステージングの pubxml*ファイルを保存して閉じます。

## <a name="publish-to-staging"></a>ステージングに発行する

ワンクリック発行またはコマンドラインを使用して、ステージングプロファイルを使用してアプリケーションを発行します。

ワンクリック発行を使用する場合は、 **[プレビュー]** ウィンドウで、 *robots.txt*がコピーされることを確認できます。 それ以外の場合は、FTP ツールを使用して、 *robots.txt*ファイルが配置後に web サイトのルートフォルダーにあることを確認します。

## <a name="summary"></a>要約

これで、ASP.NET web アプリケーションをサードパーティのホスティングプロバイダーにデプロイするための一連のチュートリアルが完了します。 これらのチュートリアルで説明されているトピックの詳細については、「 [ASP.NET Deployment Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282413)」を参照してください。

## <a name="more-information"></a>説明

MSBuild ファイルを操作する方法がわかっている場合は、(プロファイル固有のタスク用の) *pubxml*ファイルまたはプロジェクトの *.targets*ファイル (すべてのプロファイルに適用されるタスク用) にコードを記述することで、他の多くの配置タスクを自動化できます。 *Pubxml*および*wpp*ファイルの詳細については、「[方法: 発行プロファイル (Pubxml) ファイルの配置設定を編集する」および「Visual Studio Web プロジェクトの .targets ファイル](https://msdn.microsoft.com/library/ff398069)」を参照してください。 MSBuild コードの基本的な概要については、「エンタープライズ展開シリーズで**のプロジェクトファイルの構造** [: プロジェクトファイルについ](../web-deployment-in-the-enterprise/understanding-the-project-file.md)て」を参照してください。 MSBuild ファイルを操作して独自のシナリオでタスクを実行する方法については、「 [Microsoft Build Engine: msbuild と Team Foundation ビルド](http://msbuildbook.com)による作成者 Ibraham Hashimi とウィリアム Bartholow の使用」を参照してください。

## <a name="acknowledgements"></a>謝辞

このチュートリアルシリーズの内容に多大な貢献をした次の人々に感謝したいと思います。

- [Alberto Poblacion, MVP &amp; MCT, スペイン](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- Jarod Ferguson、Data Platform Development MVP、米国
- 過酷 Mittal、Microsoft
- [Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))
- [Kristina Olson、Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope、Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava、Microsoft
- [Raffaele Rialdi、イタリア](http://www.iamraf.net/)
- [Rick Anderson、Microsoft](https://blogs.msdn.com/b/rickandy/)
- [作成者 Hashimi、Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))
- [Scott マン Selman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))
- [Scott Hunter、Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))
- [Srđan Božović、セルビア](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi、Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))

> [!div class="step-by-step"]
> [前へ](command-line-deployment.md)
> [次へ](troubleshooting.md)

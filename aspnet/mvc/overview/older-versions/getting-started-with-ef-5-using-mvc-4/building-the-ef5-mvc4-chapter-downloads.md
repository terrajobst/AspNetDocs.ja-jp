---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: EF 5 MVC 4 チュートリアルのダウンロード章をビルドするMicrosoft Docs
author: Rick-Anderson
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 10237af40e3914b65e5181f17555697e86adea4b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457857"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a>EF 5 MVC 4 チュートリアルのダウンロード章をビルドする

[Rick Anderson](https://twitter.com/RickAndMSFT)

[完成したプロジェクトのダウンロード](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。 チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。

## <a name="building-the-chapter-downloads"></a>章ダウンロードの構築

1. プロジェクトサンプル zip ファイルをダウンロードして解凍します。 解凍されたダウンロードパッケージには、各章の完了のための追加の zip ファイルがあります。
2. 目的の zip ファイルを右クリックし、 **[プロパティ]** をクリックして、 **[ブロック解除]** ボタンをクリックします。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. ファイルを解凍します。
4. *Cux .sln*ファイルをダブルクリックして、Visual Studio を起動します。
5. **[ツール]** メニューの **[NuGet パッケージマネージャー]** 、 **[パッケージマネージャーコンソール]** の順にクリックします。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. パッケージマネージャーコンソール (PMC) で、 **[復元]** をクリックします。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. Visual Studio を終了します。
8. Visual Studio を再起動し、前の手順で閉じたソリューションファイルを開きます。
9. パッケージマネージャーコンソール (PMC) で、`Update-Database` コマンドを入力します。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > 次のエラーが発生する場合:  
    >   
    >  *"データベースの更新" という用語は、コマンドレット、関数、スクリプトファイル、または操作可能なプログラムの名前として認識されません。名前の綴りを確認するか、パスが含まれている場合は、パスが正しいことを確認してから、もう一度やり直してください。*  
    > Visual Studio を終了し、再起動します。

    各移行が実行された後、seed メソッドが実行されます。 これで、アプリを実行できるようになりました。

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [[戻る]](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)

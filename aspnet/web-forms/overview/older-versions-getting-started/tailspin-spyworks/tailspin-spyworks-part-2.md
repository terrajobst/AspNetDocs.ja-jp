---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: '第 2 部: データ アクセス レイヤー |Microsoft Docs'
author: JoeStagner
description: このチュートリアル シリーズでは、すべての Tailspin Spyworks サンプル アプリケーションをビルドする手順について説明します。 第 2 部では、データ アクセス層を追加することについて説明します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 3fbc6fe4d94534a038a81532b3cd8ca30ddf9b11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59378391"
---
# <a name="part-2-data-access-layer"></a>第 2 部: データ アクセス層

によって[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks では、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを作成するはどの非常に単純なを示します。 ASP.NET 4 の優れた新機能を使用して、ショッピング、チェック アウト、および管理を含む、オンライン ストアを構築する方法を示します。
> 
> このチュートリアル シリーズでは、すべての Tailspin Spyworks サンプル アプリケーションをビルドする手順について説明します。 第 2 部では、データ アクセス層を追加することについて説明します。


## <a id="_Toc260221668"></a>  データ アクセス層を追加します。

E コマース アプリケーションは、2 つのデータベースに左右されます。

顧客は、標準の ASP.NET メンバーシップ データベースを使用します。 ショッピング カート、製品カタログの SQL Express データベースを次のように実装します。

![](tailspin-spyworks-part-2/_static/image1.jpg)

アプリケーションのアプリ内でのデータベース (Commerce.mdf) を作成しなくて\_データ フォルダーが、.NET Entity Framework を使用して、データ アクセス層の作成に進むことができます。

という名前のフォルダーを作成します"データ\_アクセス"し、そのフォルダーを右クリックし、「新しい項目の追加」を選択します。

「インストールされたテンプレート」項目と選択し、"ADO.NET Entity Data Model"を入力 EDM\_Commerce.edmx 名前として、[追加] ボタンをクリックします。

![](tailspin-spyworks-part-2/_static/image2.jpg)

「データベースから生成」を選択します。

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

保存し、ビルドします。

これで、最初の機能 – 製品カテゴリ メニューに追加する準備が整いました。

> [!div class="step-by-step"]
> [前へ](tailspin-spyworks-part-1.md)
> [次へ](tailspin-spyworks-part-3.md)

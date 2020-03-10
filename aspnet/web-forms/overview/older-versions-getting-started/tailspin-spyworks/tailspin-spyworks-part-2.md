---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 'パート 2: データアクセス層 |Microsoft Docs'
author: JoeStagner
description: このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート2では、データアクセス層の追加について説明します。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462652"
---
# <a name="part-2-data-access-layer"></a>パート 2: データアクセス層

[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks は、.NET プラットフォーム用の強力でスケーラブルなアプリケーションを簡単に作成する方法を示しています。 ASP.NET 4 の優れた新機能を使用して、ショッピング、チェックアウト、管理などのオンラインストアを構築する方法を示しています。
> 
> このチュートリアルシリーズでは、Tailspin Spyworks サンプルアプリケーションを構築するために実行するすべての手順について詳しく説明します。 パート2では、データアクセス層の追加について説明します。

## <a id="_Toc260221668"></a>データアクセス層の追加

E コマースアプリケーションは、2つのデータベースに依存しています。

顧客情報については、標準の ASP.NET メンバーシップデータベースを使用します。 ショッピングカートと製品カタログについては、次のように SQL Express データベースを実装します。

![](tailspin-spyworks-part-2/_static/image1.jpg)

アプリケーションの App\_Data フォルダーにデータベース (コマース) を作成した後は、.NET Entity Framework を使用したデータアクセス層の作成に進むことができます。

"Data\_Access" という名前のフォルダーを作成し、そのフォルダーを右クリックして、[新しい項目の追加] を選択します。

[インストールされたテンプレート] 項目で、[ADO.NET Entity Data Model] を選択し、名前として「EDM\_」と入力して、[追加] ボタンをクリックします。

![](tailspin-spyworks-part-2/_static/image2.jpg)

[データベースから生成] を選択します。

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

保存してビルドします。

これで、最初の機能 (製品カテゴリメニュー) を追加する準備ができました。

> [!div class="step-by-step"]
> [前へ](tailspin-spyworks-part-1.md)
> [次へ](tailspin-spyworks-part-3.md)

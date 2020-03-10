---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 'パート 7: メンバーシップと承認 |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート7では、メンバーシップと承認について説明します。
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433468"
---
# <a name="part-7-membership-and-authorization"></a>パート 7: メンバーシップと承認

( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。  
>   
> MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。  
>   
> このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート7では、メンバーシップと承認について説明します。

現在、microsoft のストアマネージャーコントローラーは、サイトにアクセスするすべてのユーザーにアクセスできます。 これを変更して、サイト管理者にアクセス許可を制限してみましょう。

## <a name="adding-the-accountcontroller-and-views"></a>AccountController とビューの追加

Full ASP.NET MVC 3 Web アプリケーションテンプレートと ASP.NET MVC 3 空の Web アプリケーションテンプレートの違いの1つは、空のテンプレートにはアカウントコントローラーが含まれていないことです。 アカウントコントローラーを追加するには、full ASP.NET MVC 3 Web アプリケーションテンプレートから作成された新しい ASP.NET MVC アプリケーションからいくつかのファイルをコピーします。

Full ASP.NET MVC 3 Web アプリケーションテンプレートを使用して新しい ASP.NET MVC アプリケーションを作成し、次のファイルをプロジェクト内の同じディレクトリにコピーします。

1. Controllers ディレクトリで AccountController.cs をコピーする
2. モデルディレクトリに AccountModels をコピーする
3. Views ディレクトリ内にアカウントディレクトリを作成し、の4つのビューをすべてコピーします。

コントローラークラスとモデルクラスの名前空間を変更して、MvcMusicStore で始まるようにします。 AccountController クラスは MvcMusicStore 名前空間を使用する必要があり、Accountcontroller クラスは MvcMusicStore 名前空間を使用する必要があります。

*注: これらのファイルは、チュートリアルの最初にサイトデザインファイルをコピーした MvcMusicStore-Assets ダウンロードでも入手できます。メンバーシップファイルは、コードディレクトリにあります。*

更新されたソリューションは次のようになります。

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a>ASP.NET 構成サイトでの管理ユーザーの追加

Web サイトで承認が必要になる前に、アクセス権を持つユーザーを作成する必要があります。 ユーザーを作成する最も簡単な方法は、組み込みの ASP.NET 構成 web サイトを使用することです。

ソリューションエクスプローラーのアイコンをクリックして、ASP.NET 構成 web サイトを起動します。

![](mvc-music-store-part-7/_static/image2.png)

これにより、構成 web サイトが起動します。 ホーム画面の [セキュリティ] タブをクリックし、画面の中央にある [ロールの有効化] リンクをクリックします。

![](mvc-music-store-part-7/_static/image3.png)

[ロールの作成または管理] リンクをクリックします。

![](mvc-music-store-part-7/_static/image4.png)

ロール名として「Administrator」と入力し、[ロールの追加] ボタンをクリックします。

![](mvc-music-store-part-7/_static/image5.png)

[戻る] ボタンをクリックし、左側の [Create user] \ (ユーザーの作成 \) リンクをクリックします。

![](mvc-music-store-part-7/_static/image6.png)

次の情報を使用して、左側のユーザー情報フィールドに入力します。

| **フィールド** | **Value** |
| --- | --- |
| **ユーザー名** | 管理者 |
| **パスワード** | password123! |
| **[パスワードの確認入力]** | password123! |
| **電子メール** | (すべての電子メールアドレスが機能します) |
| **セキュリティの質問** | (任意のもの) |
| **セキュリティ返答** | (任意のもの) |

*注: もちろん、好きなパスワードを使用することもできます。既定のパスワードセキュリティ設定では、パスワードの長さが7文字で、英数字以外の文字が1つ含まれている必要があります。*

このユーザーの管理者ロールを選択し、[ユーザーの作成] ボタンをクリックします。

![](mvc-music-store-part-7/_static/image7.png)

この時点で、ユーザーが正常に作成されたことを示すメッセージが表示されます。

![](mvc-music-store-part-7/_static/image8.png)

ブラウザーウィンドウを閉じることができるようになりました。

## <a name="role-based-authorization"></a>ロールベースの承認

ここで、[承認] 属性を使用して StoreManagerController へのアクセスを制限できます。これにより、クラス内の任意のコントローラーアクションにアクセスするために、ユーザーが管理者ロールに存在する必要があることを指定します。

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

*注: [承認] 属性は、コントローラークラスレベルだけでなく、特定のアクションメソッドにも配置できます。*

これで、/storemanager を参照すると、[ログオン] ダイアログが表示されるようになります。

![](mvc-music-store-part-7/_static/image9.png)

新しい管理者アカウントでログオンすると、前と同じようにアルバムの編集画面にアクセスできるようになります。

> [!div class="step-by-step"]
> [前へ](mvc-music-store-part-6.md)
> [次へ](mvc-music-store-part-8.md)

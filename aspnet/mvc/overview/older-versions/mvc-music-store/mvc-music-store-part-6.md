---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: 'パート 6: モデルの検証にデータ注釈を使用する |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート6では、モデル V のデータ注釈の使用について説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: bc031dd5be61cc6707c522f85f6af77a420c8b31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433534"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a>パート 6: モデルの検証にデータ注釈を使用する

( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。  
>   
> MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。  
>   
> このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート6では、モデルの検証にデータ注釈を使用する方法について説明します。

作成フォームと編集フォームには重大な問題があります。検証は行われません。 必須フィールドを空白のままにする、または価格フィールドに文字を入力するなどの操作を実行できます。最初に表示されるエラーは、データベースからのものです。

モデルクラスにデータ注釈を追加することで、アプリケーションに検証を簡単に追加できます。 データ注釈を使用すると、モデルのプロパティに適用するルールを記述することができます。また、ASP.NET MVC では、ユーザーへの適切なメッセージの表示と表示が自動的に行われます。

## <a name="adding-validation-to-our-album-forms"></a>アルバムフォームへの検証の追加

次のデータ注釈属性を使用します。

- **必須**–プロパティが必須フィールドであることを示します。
- **DisplayName** –フォームフィールドおよび検証メッセージで使用するテキストを定義します。
- **Stringlength** –文字列フィールドの最大長を定義します。
- **Range** –数値フィールドの最大値と最小値を指定します。
- **Bind** –パラメーターまたはフォーム値をモデルプロパティにバインドするときに、除外または含めるフィールドを一覧表示します
- **ScaffoldColumn** –エディターフォームのフィールドを非表示にすることができます

*注: データ注釈属性を使用したモデル検証の詳細については、MSDN のドキュメントを参照してください*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)

アルバムクラスを開き、次の*using*ステートメントを先頭に追加します。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

次に、次に示すように、プロパティを更新して表示属性と検証属性を追加します。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

ここでは、ジャンルとアーティストも仮想プロパティに変更しました。 これにより、必要に応じて Entity Framework が遅延読み込みされます。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

これらの属性をアルバムモデルに追加した後、[作成] 画面と [編集] 画面では、すぐにフィールドの検証が開始され、選択した表示名 (AlbumArtUrl の代わりにアルバムアートの Url など) が使用されます。 アプリケーションを実行し、/StoreManager/Create. に移動します。

![](mvc-music-store-part-6/_static/image1.png)

次に、いくつかの検証規則を解除します。 価格に0を入力し、タイトルを空白のままにします。 [作成] ボタンをクリックすると、検証エラーメッセージが表示され、定義した検証ルールを満たしていないフィールドが表示されます。

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a>クライアント側の検証のテスト

サーバー側の検証は、ユーザーがクライアント側の検証を回避できるため、アプリケーションの観点から非常に重要です。 ただし、サーバー側の検証のみを実装する web ページフォームでは、3つの重要な問題が発生しています。

1. ユーザーは、フォームがポストされ、サーバーで検証され、応答がブラウザーに送信されるまで待機する必要があります。
2. ユーザーは、フィールドを修正するとすぐにフィードバックを得られず、検証ルールが渡されるようになります。
3. ユーザーのブラウザーを利用する代わりに、検証ロジックを実行するためにサーバーリソースを無駄にしています。

幸い、ASP.NET MVC 3 スキャフォールディングテンプレートでは、クライアント側の検証が組み込まれているので、追加の作業は必要ありません。

[タイトル] フィールドに1文字を入力すると検証要件が満たされるため、検証メッセージはすぐに削除されます。

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> [前へ](mvc-music-store-part-5.md)
> [次へ](mvc-music-store-part-7.md)

---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 'パート 5: フォームとテンプレートの編集 |Microsoft Docs'
author: jongalloway
description: このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート5では、フォームとテンプレートの編集について説明します。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450910"
---
# <a name="part-5-edit-forms-and-templating"></a>パート 5: フォームとテンプレートの編集

( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store は、ASP.NET MVC と Visual Studio を使用して web 開発を行う方法を紹介したチュートリアルアプリケーションです。  
>   
> MVC ミュージックストアは、音楽アルバムをオンラインで販売し、基本的なサイト管理、ユーザーサインイン、およびショッピングカート機能を実装する軽量のサンプルストア実装です。
> 
> このチュートリアルシリーズでは、ASP.NET MVC ミュージックストアサンプルアプリケーションをビルドするために実行するすべての手順について詳しく説明します。 パート5では、フォームとテンプレートの編集について説明します。

これまでの章では、データベースからデータを読み込んで表示していました。 この章では、データの編集も有効にします。

## <a name="creating-the-storemanagercontroller"></a>StoreManagerController の作成

まず、 **StoreManagerController**という名前の新しいコントローラーを作成します。 このコントローラーでは、ASP.NET MVC 3 Tools Update で提供されているスキャフォールディング機能を利用します。 次に示すように、[コントローラーの追加] ダイアログのオプションを設定します。

![](mvc-music-store-part-5/_static/image1.png)

[追加] ボタンをクリックすると、ASP.NET MVC 3 のスキャフォールディングメカニズムによって適切な作業が行われます。

- ローカル Entity Framework 変数を使用して新しい StoreManagerController を作成します。
- これにより、StoreManager フォルダーがプロジェクトの Views フォルダーに追加されます。
- これにより、作成した cshtml、Delete. cshtml、Details、Edit. cshtml、および Index. cshtml ビューが追加され、アルバムクラスに厳密に型指定されます。

![](mvc-music-store-part-5/_static/image2.png)

新しい StoreManager コントローラークラスには、CRUD (作成、読み取り、更新、削除) コントローラーアクションが含まれています。これは、アルバムモデルクラスを使用してデータベースアクセスに Entity Framework のコンテキストを使用する方法を知っています。

## <a name="modifying-a-scaffolded-view"></a>スキャフォールディングビューの変更

このコードが生成されましたが、このチュートリアル全体を通して記述したのと同じように、標準の ASP.NET MVC コードであることを覚えておくことが重要です。 これは、定型的なコントローラーコードを記述し、厳密に型指定されたビューを手動で作成するために費やされる時間を節約することを目的としていますが、これは、ディレクトリの警告で、コード. これはコードであり、変更することが期待されています。

では、StoreManager インデックスビューのクイック編集 (/Views/StoreManager/Index.cshtml) から始めましょう。 このビューには、[編集]、[詳細]、[削除] リンクを含むストア内のアルバムの一覧が表示され、アルバムのパブリックプロパティが含まれます。 この表示ではあまり役に立たないので、AlbumArtUrl フィールドを削除します。 下の強調表示されている行で示されているように、ビューコードの &lt;テーブル&gt; セクションで、次のように、AlbumArtUrl 参照を囲む &lt;th&gt; と &lt;td&gt; 要素を削除します。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

変更されたビューコードは次のようになります。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a>ストアマネージャーの最初の確認

ここで、アプリケーションを実行し、/StoreManager/. に移動します。 これにより、変更したばかりのストアマネージャーのインデックスが表示され、ストア内のアルバムの一覧と、編集、詳細、削除のリンクが表示されます。

![](mvc-music-store-part-5/_static/image3.png)

[編集] リンクをクリックすると、ジャンルとアーティストのドロップダウンを含む、アルバムのフィールドを含む編集フォームが表示されます。

![](mvc-music-store-part-5/_static/image4.png)

下部にある [一覧に戻る] リンクをクリックし、アルバムの [Details] リンクをクリックします。 これにより、個々のアルバムの詳細情報が表示されます。

![](mvc-music-store-part-5/_static/image5.png)

ここでも、[一覧に戻る] リンクをクリックし、[削除] リンクをクリックします。 これにより、アルバムの詳細が表示され、削除するかどうかを確認する確認ダイアログが表示されます。

![](mvc-music-store-part-5/_static/image6.png)

下部にある [削除] ボタンをクリックすると、アルバムが削除され、[インデックス] ページに戻ります。このページには、削除されたアルバムが表示されます。

ストアマネージャーでは実行されませんが、CRUD 操作を開始するためのコントローラーとビューコードが用意されています。

## <a name="looking-at-the-store-manager-controller-code"></a>ストアマネージャーコントローラーコードを見る

ストアマネージャーコントローラーには、十分な量のコードが含まれています。 これを上から下に見てみましょう。 コントローラーには、MVC コントローラーの標準名前空間と、モデルの名前空間への参照が含まれています。 コントローラーには、データアクセスの各コントローラーアクションによって使用される MusicStoreEntities のプライベートインスタンスがあります。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a>ストアマネージャーのインデックスと詳細アクション

インデックスビューでは、各アルバムの参照されているジャンルとアーティスト情報を含むアルバムの一覧が取得されます。これについては、ストアの参照方法に関する説明をご覧ください。 インデックスビューは、リンクオブジェクトへの参照に従っているので、各アルバムのジャンル名とアーティスト名を表示できるようにします。これにより、コントローラーは効率的になり、元の要求でこの情報を照会できます。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

StoreManager コントローラーの詳細コントローラーアクションは、先ほど作成したストアコントローラーの詳細アクションとまったく同じように動作します。これは、Find () メソッドを使用して ID でアルバムを照会し、それをビューに返します。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a>Create Action メソッド

作成アクションメソッドは、フォーム入力を処理するため、これまでに見たものとは少し異なります。 ユーザーが初めて/StoreManager/Create/にアクセスすると、空のフォームが表示されます。 この HTML ページには、&lt;フォーム&gt; 要素が含まれています。これには、ドロップダウンおよびテキストボックスの入力要素が含まれており、そこでアルバムの詳細を入力できます。

ユーザーがアルバムフォームの値を入力したら、[保存] ボタンをクリックして、これらの変更をアプリケーションに送信し、データベース内に保存することができます。 ユーザーが [save] \ (保存 \) ボタンを押すと、&lt;フォーム&gt; によって/StoreManager/Create/URL への HTTP ポストバックが実行され、HTTP POST の一部として &lt;フォーム&gt; 値が送信されます。

ASP.NET MVC を使用すると、これら2つの URL 呼び出しシナリオのロジックを簡単に分割できます。 StoreManagerController クラス内に2つの個別の "Create" アクションメソッドを実装し、1つは/StoreManager/Create/URL への最初の HTTP 取得を処理し、もう1つは、送信された変更の HTTP POST を処理します。

### <a name="passing-information-to-a-view-using-viewbag"></a>ViewBag を使用して情報をビューに渡す

このチュートリアルの前半で ViewBag を使用しましたが、これについてはあまり説明していません。 ViewBag を使用すると、厳密に型指定されたモデルオブジェクトを使用せずに、ビューに情報を渡すことができます。 この場合、[HTTP-GET controller の編集] アクションでは、ドロップダウンを設定するために、ジャンルとアーティストの一覧の両方をフォームに渡す必要があります。これを行う最も簡単な方法は、ViewBag 項目として返すことです。

ViewBag は動的なオブジェクトです。つまり、ViewBag または ViewBag と入力すると、これらのプロパティを定義するコードを記述しなくてもかまいません。 この場合、コントローラーコードは ViewBag と ViewBag を使用して、フォームと共に送信されるドロップダウンの値が GenreId および ArtistId になります。これは、設定されるアルバムプロパティです。

これらのドロップダウン値は、その目的のためだけに構築された SelectList オブジェクトを使用してフォームに返されます。 これは、次のようなコードを使用して行います。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

アクションメソッドコードからわかるように、このオブジェクトを作成するために3つのパラメーターが使用されています。

- ドロップダウンに表示される項目の一覧。 これは文字列ではないことに注意してください。ジャンルの一覧を渡しています。
- SelectList に渡される次のパラメーターは、選択された値です。 ここでは、リスト内の項目を事前に選択する方法について説明します。 これは、編集フォームを見たときに理解しやすくなります。
- 最後のパラメーターは、表示されるプロパティです。 この場合、Genre.Name プロパティがユーザーに表示されることを示しています。

この点を念頭に置いて、HTTP GET Create アクションは非常に単純であり、2つの SelectLists が ViewBag に追加され、モデルオブジェクトは (まだ作成されていないため) フォームに渡されません。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a>作成ビューでドロップダウンを表示する HTML ヘルパー

ここではドロップダウン値がビューにどのように渡されるかを説明したので、ビューを見て、それらの値がどのように表示されるかを見てみましょう。 [コードの表示] (/Views/StoreManager/Create.cshtml) では、ジャンルドロップダウンを表示するために次の呼び出しが行われていることがわかります。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

これを HTML ヘルパーと呼びます。これは、一般的なビュータスクを実行するユーティリティメソッドです。 HTML ヘルパーは、ビューコードを簡潔かつ読みやすくするために非常に役立ちます。 ASP.NET MVC は Html の DropDownList ヘルパーを提供しますが、後で説明するように、アプリケーションで再利用するコードを表示するための独自のヘルパーを作成することができます。

Html の DropDownList 呼び出しには、表示するリストを取得する場所と、事前に選択する必要がある値 (存在する場合) を2つ指定するだけで済みます。 最初のパラメーター GenreId は、モデルまたは ViewBag のいずれかで GenreId という値を検索するように DropDownList に指示します。 2番目のパラメーターは、ドロップダウンリストで最初に選択された値を示すために使用されます。 このフォームは作成フォームなので、事前に選択された値はありません。空の文字列が渡されます。

### <a name="handling-the-posted-form-values"></a>ポストされたフォーム値の処理

前に説明したように、各フォームには2つのアクションメソッドが関連付けられています。 最初のは、HTTP GET 要求を処理し、フォームを表示します。 2つ目は、送信されたフォーム値を含む HTTP POST 要求を処理します。 コントローラーアクションには [HttpPost] 属性があり、ASP.NET MVC は HTTP POST 要求にのみ応答する必要があることに注意してください。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

このアクションには、次の4つの役割があります。

- 1. フォームの値を読み取る
- 2. フォーム値が検証規則に合格するかどうかを確認します。
- 3. フォームの送信が有効な場合は、データを保存して更新された一覧を表示します。
- 4. フォームの送信が有効でない場合は、検証エラーが表示されたフォームを再表示します。

#### <a name="reading-form-values-with-model-binding"></a>モデルバインドを使用したフォーム値の読み取り

コントローラーアクションは、GenreId と ArtistId (ドロップダウンリスト) の値、および Title、Price、および AlbumArtUrl のテキストボックス値を含むフォーム送信を処理しています。 フォーム値に直接アクセスすることもできますが、ASP.NET MVC に組み込まれているモデルバインド機能を使用する方法が適しています。 コントローラーアクションがモデル型をパラメーターとして受け取ると、ASP.NET MVC は、フォーム入力 (および route および querystring 値) を使用して、その型のオブジェクトを設定しようとします。 これを行うには、モデルオブジェクトのプロパティと一致する名前を持つ値を探します。たとえば、新しいアルバムオブジェクトの GenreId 値を設定すると、GenreId という名前の入力が検索されます。 ASP.NET MVC の標準メソッドを使用してビューを作成する場合、フォームは常に入力フィールド名としてプロパティ名を使用して表示されるため、このフィールド名は一致するだけです。

#### <a name="validating-the-model"></a>モデルの検証

モデルは、ModelState. IsValid の単純な呼び出しで検証されます。 まだアルバムクラスに検証ルールを追加していません。これは少しの間、このチェックはあまり実行されません。 重要なのは、この ModelStat. IsValid check は、モデルに配置した検証規則に適合するため、今後、検証規則を変更しても、コントローラーのアクションコードを更新する必要はありません。

#### <a name="saving-the-submitted-values"></a>送信された値を保存しています

フォーム送信が検証に合格した場合は、その値をデータベースに保存します。 Entity Framework では、モデルをアルバムコレクションに追加し、SaveChanges を呼び出す必要があります。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

Entity Framework は、値を永続化するための適切な SQL コマンドを生成します。 データを保存すると、アルバムの一覧にリダイレクトされ、更新プログラムが表示されます。 これを行うには、表示するコントローラーアクションの名前を使用して RedirectToAction を返します。 この例では、これが Index メソッドです。

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a>検証エラーのある無効なフォーム送信の表示

無効なフォーム入力の場合は、ドロップダウンの値が (HTTP GET の場合と同様に) ViewBag に追加され、バインドされたモデル値がビューに戻されて表示されます。 検証エラーは、@Html.ValidationMessageFor HTML ヘルパーを使用して自動的に表示されます。

#### <a name="testing-the-create-form"></a>作成フォームのテスト

これをテストするには、アプリケーションを実行し、/StoreManager/Create/に移動します。これにより、StoreController Create HTTP-GET メソッドによって返された空白のフォームが表示されます。

いくつかの値を入力し、[作成] ボタンをクリックしてフォームを送信します。

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a>編集の処理

編集アクションのペア (HTTP-GET と HTTP POST) は、先ほど見た Create アクションメソッドによく似ています。 編集シナリオでは既存のアルバムを操作するため、Edit HTTP-GET メソッドは、ルートを介して渡される "id" パラメーターに基づいてアルバムを読み込みます。 AlbumId によってアルバムを取得するためのこのコードは、前に「コントローラーの詳細」アクションで確認したものと同じです。 Create/HTTP-GET メソッドと同様に、ドロップダウンの値は ViewBag を使用して返されます。 これにより、ViewBag を介して追加のデータ (ジャンルの一覧など) を渡すとともに、モデルオブジェクトとしてアルバムを (アルバムクラスに厳密に型指定された) ビューに返すことができます。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

Edit HTTP-POST アクションは、Create HTTP-POST アクションと非常によく似ています。 唯一の違いは、新しいアルバムを db に追加するのではなく、アルバムコレクション。 db を使用してアルバムの現在のインスタンスを検索しています。エントリ (アルバム) を入力し、その状態を "変更済み" に設定します。 これは、新しいアルバムを作成するのではなく、既存のアルバムを変更することを Entity Framework します。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

これをテストするには、アプリケーションを実行し、/Storemanger/に移動して、アルバムの [編集] リンクをクリックします。

![](mvc-music-store-part-5/_static/image9.png)

これにより、Edit HTTP-GET メソッドによって表示される編集フォームが表示されます。 いくつかの値を入力し、[保存] ボタンをクリックします。

![](mvc-music-store-part-5/_static/image10.png)

これにより、フォームが投稿され、値が保存されて、値が更新されたことを示すアルバムリストに戻ります。

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a>削除の処理

削除は、編集と作成と同じパターンに従い、1つのコントローラーアクションを使用して確認フォームを表示し、もう1つのコントローラーアクションを使用してフォームの送信を処理します。

HTTP-Delete controller アクションは、以前のストアマネージャー詳細コントローラーアクションとまったく同じです。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

[ビューコンテンツの削除] テンプレートを使用して、アルバムの種類に厳密に型指定されたフォームを表示します。

![](mvc-music-store-part-5/_static/image12.png)

[削除] テンプレートには、モデルのすべてのフィールドが表示されますが、簡単に簡略化できます。 /Views/StoreManager/Delete.cshtml のビューコードを次のように変更します。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

これにより、簡略化された削除の確認が表示されます。

![](mvc-music-store-part-5/_static/image13.png)

[削除] ボタンをクリックすると、フォームがサーバーにポストバックされます。これにより、DeleteConfirmed アクションが実行されます。

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

HTTP ポスト削除コントローラーアクションは、次の操作を実行します。

- 1. ID でアルバムを読み込みます
- 2. アルバムを削除し、変更を保存します
- 3. リストからアルバムが削除されたことを示すインデックスにリダイレクトします。

これをテストするには、アプリケーションを実行し、/StoreManager. に移動します。 一覧からアルバムを選択し、[削除] リンクをクリックします。

![](mvc-music-store-part-5/_static/image14.png)

削除の確認画面が表示されます。

![](mvc-music-store-part-5/_static/image15.png)

[削除] ボタンをクリックすると、アルバムが削除され、[ストアマネージャーインデックス] ページに戻ります。これは、アルバムが削除されたことを示しています。

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a>カスタム HTML ヘルパーを使用したテキストの切り捨て

ストアマネージャーのインデックスページでは、潜在的な問題が1つあります。 アルバムのタイトルとアーティスト名のプロパティは、どちらも、テーブルの書式設定を破棄するのに十分な長さにすることができます。 ここでは、これらのプロパティとその他のプロパティをビューで簡単に切り捨てることができるように、カスタム HTML ヘルパーを作成します。

![](mvc-music-store-part-5/_static/image17.png)

Razor の @helper 構文では、ビューで使用する独自のヘルパー関数を簡単に作成できました。 /Views/StoreManager/Index.cshtml ビューを開き、@model 行の直後に次のコードを追加します。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

このヘルパーメソッドは、文字列と最大長を使用して許可します。 指定したテキストが指定された長さより短い場合、ヘルパーはそれをそのように出力します。 長い場合は、テキストを切り捨て、"..." をレンダリングします。それ以外の場合はです。

ここで、Truncate helper を使用して、アルバムのタイトルとアーティスト名の両方のプロパティが25文字未満であることを確認できます。 新しい Truncate ヘルパーを使用する完全なビューコードは次のようになります。

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

ここで、/StoreManager/URL を参照したときに、アルバムとタイトルは最大長の下に保持されます。

![](mvc-music-store-part-5/_static/image18.png)

注: これは、ヘルパーを作成して1つのビューで使用する単純なケースを示しています。 サイト全体で使用できるヘルパーの作成の詳細については、ブログの投稿: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)を参照してください。

> [!div class="step-by-step"]
> [前へ](mvc-music-store-part-4.md)
> [次へ](mvc-music-store-part-6.md)

---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'ASP.NET Web API での HTML フォームデータの送信: ファイルのアップロードとマルチパート MIME-ASP.NET 4.x'
author: MikeWasson
description: このチュートリアルでは、web API にファイルをアップロードする方法について説明します。 また、マルチパート MIME データを処理する方法についても説明します。
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449212"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a>ASP.NET Web API での HTML フォームデータの送信: ファイルのアップロードとマルチパート MIME

[Mike Wasson](https://github.com/MikeWasson)

## <a name="part-2-file-upload-and-multipart-mime"></a>パート 2: ファイルのアップロードとマルチパート MIME

このチュートリアルでは、web API にファイルをアップロードする方法について説明します。 また、マルチパート MIME データを処理する方法についても説明します。

> [!NOTE]
> [完成したプロジェクトをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d)します。

ファイルをアップロードするための HTML フォームの例を次に示します。

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

このフォームには、テキスト入力コントロールとファイル入力コントロールが含まれています。 フォームにファイル入力コントロールが含まれている場合、 **enctype**属性は常にマルチパート/フォームデータ&quot;&quot;する必要があります。これにより、フォームがマルチパート MIME メッセージとして送信されることが指定されます。

マルチパート MIME メッセージの形式は、要求の例を見て理解するのが最も簡単です。

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

このメッセージは、フォームコントロールごとに1つずつ、2つの*部分*に分かれています。 部分境界は、ダッシュで始まる線によって示されます。

> [!NOTE]
> 部分境界には、境界文字列がメッセージ部分の内部に誤って表示されないようにするために、ランダムなコンポーネント (&quot;41184676334&quot;) が含まれています。

各メッセージ部分には、1つまたは複数のヘッダーが含まれ、その後にパーツコンテンツが含まれます。

- コンテンツディスポジションヘッダーには、コントロールの名前が含まれます。 ファイルの場合は、ファイル名も含まれます。
- Content-type ヘッダーは、パーツ内のデータを記述します。 このヘッダーを省略した場合、既定値は text/plain です。

前の例では、ユーザーが GrandCanyon という名前のファイルをアップロードしました。コンテンツの種類は image/jpeg です。テキスト入力の値は、夏休暇&quot;&quot;でした。

## <a name="file-upload"></a>ファイルのアップロード

次に、マルチパート MIME メッセージからファイルを読み取る Web API コントローラーを見てみましょう。 コントローラーはファイルを非同期的に読み取ります。 Web API は、[タスクベースのプログラミングモデル](https://msdn.microsoft.com/library/dd460693.aspx)を使用した非同期アクションをサポートしています。 まず、 **async**キーワードと**await**キーワードをサポートする .NET Framework 4.5 を対象とするコードを次に示します。

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

コントローラーアクションにはパラメーターがないことに注意してください。 これは、メディアの種類のフォーマッタを呼び出さずに、アクション内で要求本文を処理するためです。

**Ismultipartcontent**メソッドは、要求にマルチパート MIME メッセージが含まれているかどうかを確認します。 それ以外の場合、コントローラーは HTTP 状態コード 415 (サポートされていないメディアの種類) を返します。

**Multipartformdatastreamprovider**クラスは、アップロードされたファイルのファイルストリームを割り当てるヘルパーオブジェクトです。 マルチパート MIME メッセージを読み取るには、 **Readasmultipartasync**メソッドを呼び出します。 このメソッドは、すべてのメッセージ部分を抽出し、 **Multipartformdatastreamprovider**によって提供されるストリームに書き込みます。

メソッドが完了すると、 **FileData**プロパティからファイルに関する情報を取得できます。このプロパティは、 **MultipartFileData**オブジェクトのコレクションです。

- **MultipartFileData**は、ファイルが保存されたサーバー上のローカルファイル名です。
- **MultipartFileData**には、(要求ヘッダーでは*なく*) パーツヘッダーが含まれています。 これを使用して、コンテンツ\_の内容およびコンテンツタイプのヘッダーにアクセスできます。

名前が示すように、 **Readasmultipartasync**は非同期メソッドです。 メソッドの完了後に作業を実行するには、[継続タスク](https://msdn.microsoft.com/library/ee372288.aspx)(.net 4.0) または**await**キーワード (.net 4.5) を使用します。

前のコードの .NET Framework 4.0 バージョンを次に示します。

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a>フォームコントロールデータの読み取り

先ほど見た HTML フォームには、テキスト入力コントロールがありました。

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

このコントロールの値は、 **Multipartformdatastreamprovider**の**formdata**プロパティから取得できます。

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

**Formdata**は、フォームコントロールの名前と値のペアを含む**NameValueCollection**です。 コレクションには重複するキーを含めることができます。 次の形式を考えてみましょう。

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

要求本文は次のようになります。

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

その場合、 **Formdata**コレクションには次のキーと値のペアが含まれます。

- 旅行: ラウンドトリップ
- オプション: 無着陸
- オプション: 日付
- 座席: ウィンドウ

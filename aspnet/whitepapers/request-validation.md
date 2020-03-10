---
uid: whitepapers/request-validation
title: 要求の検証-スクリプト攻撃の防止 |Microsoft Docs
author: rick-anderson
description: このホワイトペーパーでは、ASP.NET の要求検証機能について説明します。既定では、アプリケーションはエンコードされていない HTML コンテンツを処理できません。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520582"
---
# <a name="request-validation---preventing-script-attacks"></a>要求検証 - スクリプト攻撃を防ぐ

> このホワイトペーパーでは、ASP.NET の要求検証機能について説明します。既定では、アプリケーションは、エンコードされていない HTML コンテンツをサーバーに送信できません。 この要求の検証機能は、アプリケーションが HTML データを安全に処理するように設計されている場合は無効にすることができます。
> 
> ASP.NET 1.1 と ASP.NET 2.0 に適用されます。

要求の検証は ASP.NET 1.1 以降の機能で、エンコードされていない HTML を含むコンテンツを、サーバーが受け入れられないようにします。 この機能は、スクリプト インジェクション攻撃、つまり、クライアント スクリプト コードや HTML が知らないうちにサーバーに送信され、格納された後、他のユーザーに提供されるのを防ぐことを目的としています。 ただし、すべての入力データを適宜検証し、HTML エンコードを行うことを強くお勧めします。

たとえば、ユーザーの電子メールアドレスを要求する Web ページを作成し、その電子メールアドレスをデータベースに保存します。 ユーザーが &lt;スクリプト&gt;の警告 ("hello from SCRIPT") を入力すると、有効な電子メールアドレスではなく、/SCRIPT&gt;&lt;ます。そのデータが表示されると、コンテンツが正しくエンコードされていない場合は、このスクリプトを実行できます。 ASP.NET の要求の検証機能によって、この問題が発生することはありません。

## <a name="why-this-feature-is-useful"></a>この機能が役に立つ理由

多くのサイトは、単純なスクリプトインジェクション攻撃に対して開かれていることを認識していません。 これらの攻撃の目的は、HTML を表示するか、クライアントスクリプトを実行してユーザーをハッカーのサイトにリダイレクトすることであるかどうかにかかわらず、スクリプトインジェクション攻撃は、Web 開発者が対処する必要がある問題です。

スクリプトインジェクション攻撃は、ASP.NET、ASP、またはその他の web 開発テクノロジを使用しているかどうかに関係なく、すべての web 開発者にとって重要です。

ASP.NET 要求の検証機能では、開発者がコンテンツを許可しない限り、エンコードされていない HTML コンテンツをサーバーで処理できないようにすることで、これらの攻撃を事前に防ぐことができます。

## <a name="what-to-expect-error-page"></a>期待される内容: エラーページ

次のスクリーンショットは、サンプルの ASP.NET コードを示しています。

![](request-validation/_static/image1.png)

このコードを実行すると、テキストボックスにテキストを入力し、ボタンをクリックして、ラベルコントロールにテキストを表示できる単純なページが生成されます。

![](request-validation/_static/image2.png)

ただし、`<script>alert("hello!")</script>` の入力や送信などの JavaScript は、次のような例外が発生します。

![](request-validation/_static/image3.png)

エラーメッセージは、"危険な要求が発生した可能性がある" という値が検出されたことを示し、何が発生したか、および動作を変更する方法を説明する詳細情報を提供します。 次に例を示します。

要求の検証で、危険な可能性のあるクライアント入力値が検出され、要求の処理が中止されました。 この値は、クロスサイトスクリプティング攻撃など、アプリケーションのセキュリティを侵害しようとしている可能性があります。 ページディレクティブまたは構成セクションで `validateRequest=false` を設定することによって、要求の検証を無効にすることができます。 ただし、この場合は、アプリケーションですべての入力を明示的に確認することを強くお勧めします。

## <a name="disabling-request-validation-on-a-page"></a>ページでの要求の検証を無効にする

ページでの要求の検証を無効にするには、Page ディレクティブの `validateRequest` 属性を `false`に設定する必要があります。

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> 要求の検証が無効になっている場合は、ページにコンテンツを送信できます。コンテンツが適切にエンコードまたは処理されていることを確認するのは、ページ開発者の責任です。

## <a name="disabling-request-validation-for-your-application"></a>アプリケーションの要求の検証を無効にしています

アプリケーションの要求の検証を無効にするには、アプリケーションの web.config ファイルを変更または作成し、`<pages />` セクションの validateRequest 属性を `false`に設定する必要があります。

[!code-xml[Main](request-validation/samples/sample2.xml)]

サーバー上のすべてのアプリケーションに対する要求の検証を無効にする場合は、machine.config ファイルに変更を加えることができます。

> [!CAUTION]
> 要求の検証が無効になっている場合、コンテンツをアプリケーションに送信できます。コンテンツが適切にエンコードまたは処理されていることを確認するのは、アプリケーション開発者の責任です。

次のコードは、要求の検証を無効にするように変更されています。

![](request-validation/_static/image4.png)

ここで、次の JavaScript がテキストボックスに入力された場合 `<script>alert("hello!")</script>` 結果は次のようになります。

![](request-validation/_static/image5.png)

これが行われないようにするには、要求の検証を無効にして、コンテンツを HTML エンコードする必要があります。

## <a name="how-to-html-encode-content"></a>方法: コンテンツを HTML エンコードする

要求の検証を無効にしている場合は、今後使用するために保存されるコンテンツを HTML エンコードすることをお勧めします。 HTML エンコードでは、任意の '&lt;' または '&gt;' が、他のいくつかのシンボルと共に、対応する HTML エンコードされた表現に自動的に置き換えられます。 たとえば、'&lt;' は '&amp;lt; ' に置き換えられ、'&gt;' は '&amp;gt; ' に置き換えられます。 ブラウザーでは、これらの特殊なコードを使用して '&lt;' または '&gt;' がブラウザーに表示されます。

コンテンツは、`Server.HtmlEncode(string)` API を使用して、サーバー上で簡単に HTML エンコードできます。 また、コンテンツは簡単に HTML デコードできます。つまり、`Server.HtmlDecode(string)` メソッドを使用して標準 HTML に戻されます。

![](request-validation/_static/image6.png)

結果は次のようになります。

![](request-validation/_static/image7.png)

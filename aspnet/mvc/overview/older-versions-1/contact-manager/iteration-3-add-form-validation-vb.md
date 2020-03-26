---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: 'イテレーション #3 –フォーム検証を追加する (VB) |Microsoft Docs'
author: microsoft
description: 3番目のイテレーションでは、基本的なフォーム検証を追加します。 必要なフォームフィールドを完了しないで、フォームを送信できないようにします。 また、emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 73b307f53875abe84b592c75b1ff614ffd9d8b82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437968"
---
# <a name="iteration-3--add-form-validation-vb"></a>イテレーション #3 –フォーム検証の追加 (VB)

[Microsoft](https://github.com/microsoft)

[コードのダウンロード](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> 3番目のイテレーションでは、基本的なフォーム検証を追加します。 必要なフォームフィールドを完了しないで、フォームを送信できないようにします。 また、電子メールアドレスと電話番号も検証します。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Contact Management ASP.NET MVC アプリケーションの構築 (VB)

この一連のチュートリアルでは、最初から最後まで、連絡先管理アプリケーション全体を作成します。 連絡先マネージャーアプリケーションを使用すると、連絡先情報 (名前、電話番号、電子メールアドレスなど) をユーザーの一覧に格納できます。

複数のイテレーションに対してアプリケーションをビルドします。 各イテレーションで、アプリケーションを段階的に改善します。 この複数のイテレーションアプローチの目的は、各変更の理由を理解できるようにすることです。

- イテレーション #1-アプリケーションを作成します。 最初のイテレーションでは、最も簡単な方法で Contact Manager を作成します。 基本的なデータベース操作のサポートを追加します。作成、読み取り、更新、および削除 (CRUD)。

- イテレーション #2-アプリケーションの外観を良くします。 このイテレーションでは、既定の ASP.NET MVC ビューマスターページとカスケードスタイルシートを変更することによって、アプリケーションの外観を改善します。

- イテレーション #3-フォーム検証を追加します。 3番目のイテレーションでは、基本的なフォーム検証を追加します。 必要なフォームフィールドを完了しないで、フォームを送信できないようにします。 また、電子メールアドレスと電話番号も検証します。

- イテレーション #4-アプリケーションの疎結合を実現します。 この4回目のイテレーションでは、複数のソフトウェア設計パターンを利用して、連絡先マネージャーアプリケーションを簡単に管理および変更できるようにします。 たとえば、リポジトリパターンと依存関係の注入パターンを使用するようにアプリケーションをリファクターします。

- イテレーション #5-単体テストを作成します。 5番目のイテレーションでは、単体テストを追加することによって、アプリケーションの保守と変更を容易にします。 データモデルクラスをモック化し、コントローラーと検証ロジックの単体テストをビルドします。

- イテレーション #6-テスト駆動型開発を使用します。 この6番目のイテレーションでは、最初に単体テストを記述し、単体テストに対してコードを記述することによって、アプリケーションに新しい機能を追加します。 このイテレーションでは、連絡先グループを追加します。

- イテレーション #7-Ajax 機能を追加します。 7番目のイテレーションでは、Ajax のサポートを追加することによって、アプリケーションの応答性とパフォーマンスを向上させます。

## <a name="this-iteration"></a>このイテレーション

Contact Manager アプリケーションのこの2回目のイテレーションでは、基本的なフォーム検証を追加します。 必須フォームフィールドの値を入力することなく、連絡先を送信できないようにします。 また、電話番号と電子メールアドレスも検証します (図1を参照)。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)

**図 01**:検証付きのフォーム ([クリックすると、フルサイズの画像が表示](iteration-3-add-form-validation-vb/_static/image2.png)される)

このイテレーションでは、コントローラーアクションに検証ロジックを直接追加します。 一般に、ASP.NET MVC アプリケーションに検証を追加する方法として推奨されていません。 より優れたアプローチは、アプリケーションの検証ロジックを別の[サービス層](http://martinfowler.com/eaaCatalog/serviceLayer.html)に配置することです。 次のイテレーションでは、アプリケーションの保守が容易になるように Contact Manager アプリケーションをリファクターします。

このイテレーションでは、簡単にするために、すべての検証コードを手動で記述します。 検証コードを自分で記述する代わりに、検証フレームワークを利用することもできます。 たとえば、Microsoft エンタープライズライブラリ検証アプリケーションブロック (VAB) を使用して、ASP.NET MVC アプリケーションの検証ロジックを実装できます。 検証アプリケーションブロックの詳細については、以下を参照してください。

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>Create ビューへの検証の追加

まず、検証ロジックを Create ビューに追加します。 幸い、Visual Studio で作成ビューを生成したため、検証メッセージを表示するために必要なすべてのユーザーインターフェイスロジックが既に作成ビューに含まれています。 [作成] ビューは、リスト1に含まれています。

**Listing 1 - \Views\Contact\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

フィールド検証-エラークラスは、Html. ValidationMessage () ヘルパーによって表示される出力のスタイルを適用するために使用されます。 入力検証-エラークラスは、Html の TextBox () ヘルパーによって表示されるテキストボックスのスタイルを適用するために使用されます。 "検証-概要-エラー" クラスは、Html. ValidationSummary () ヘルパーによって表示される順序付けられていないリストのスタイルを適用するために使用されます。

> [!NOTE] 
> 
> このセクションで説明するスタイルシートクラスを変更して、検証エラーメッセージの外観をカスタマイズできます。

## <a name="adding-validation-logic-to-the-create-action"></a>作成アクションへの検証ロジックの追加

現時点では、メッセージを生成するロジックが記述されていないため、Create view は検証エラーメッセージを表示しません。 検証エラーメッセージを表示するには、エラーメッセージを ModelState に追加する必要があります。

> [!NOTE] 
> 
> UpdateModel () メソッドは、フォームフィールドの値をプロパティに割り当てるときにエラーが発生した場合に、エラーメッセージを ModelState に自動的に追加します。 たとえば、文字列 "apple" を DateTime 値を受け取る "誕生日" プロパティに割り当てようとすると、UpdateModel () メソッドによって ModelState にエラーが追加されます。

リスト2の Create () メソッドを変更すると、新しい連絡先がデータベースに挿入される前に Contact クラスのプロパティを検証する新しいセクションが追加されます。

**リスト 2-コントローラーの一覧表示 (検証を使用した作成)**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

Validate セクションでは、4つの異なる検証規則が適用されます。

- FirstName プロパティの長さは0よりも大きくする必要があります (スペースだけで構成することはできません)
- LastName プロパティの長さは0よりも大きくする必要があります (スペースだけで構成することはできません)
- Phone プロパティの値が (長さが0より大きい) 場合、Phone プロパティは正規表現と一致する必要があります。
- Email プロパティの値が (長さが0より大きい) 場合、Email プロパティは正規表現と一致する必要があります。

検証規則違反が発生すると、AddModelError () メソッドを使用してエラーメッセージが ModelState に追加されます。 ModelState にメッセージを追加する場合は、プロパティの名前と検証エラーメッセージのテキストを指定します。 このエラーメッセージは、Html. ValidationSummary () および Html の Validationsummary () ヘルパーメソッドによってビューに表示されます。

検証規則が実行されると、ModelState の IsValid プロパティがチェックされます。 IsValid プロパティは、ModelState に検証エラーメッセージが追加されたときに false を返します。 検証が失敗すると、エラーメッセージと共に作成フォームが再生成されます。

> [!NOTE] 
> 
> の正規表現リポジトリから電話番号と電子メールアドレスを検証する正規表現があります。 [ *http://regexlib.com* ](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>編集アクションへの検証ロジックの追加

Edit () アクションを実行すると、連絡先が更新されます。 Edit () アクションでは、Create () アクションとまったく同じ検証を実行する必要があります。 同じ検証コードを複製するのではなく、Create () と Edit () の両方のアクションが同じ検証メソッドを呼び出すように Contact controller をリファクターする必要があります。

変更した Contact controller クラスは、リスト3に含まれています。 このクラスには、Create () アクションと Edit () アクションの両方で呼び出される新しい ValidateContact () メソッドがあります。

**Listing 3 - Controllers\ContactController.vb**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a>まとめ

このイテレーションでは、Contact Manager アプリケーションに基本的なフォーム検証を追加しました。 この検証ロジックにより、ユーザーは FirstName プロパティと LastName プロパティの値を指定せずに、新しい連絡先を送信したり、既存の連絡先を編集したりすることができなくなります。 さらに、ユーザーは有効な電話番号と電子メールアドレスを入力する必要があります。

このイテレーションでは、最も簡単な方法で Contact Manager アプリケーションに検証ロジックを追加しました。 ただし、検証ロジックをコントローラーロジックに混在させると、長期的に問題が発生します。 時間の経過と共に、アプリケーションの保守と変更が困難になります。

次のイテレーションでは、検証ロジックとデータベースアクセスロジックをコントローラーからリファクターします。 複数のソフトウェア設計原則を利用して、より疎結合で保守性の高いアプリケーションを作成できるようにします。

> [!div class="step-by-step"]
> [前へ](iteration-2-make-the-application-look-nice-vb.md)
> [次へ](iteration-4-make-the-application-loosely-coupled-vb.md)

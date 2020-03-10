---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
title: 'イテレーション #4 –アプリケーションを疎結合にする (VB) |Microsoft Docs'
author: microsoft
description: この4回目のイテレーションでは、複数のソフトウェア設計パターンを利用して、連絡先マネージャーアプリケーションを簡単に管理および変更できるようにします。 ...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 92c70297-4430-4e4e-919a-9c2333a8d09a
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
msc.type: authoredcontent
ms.openlocfilehash: 422c75406d9c08279d0c2224ee4b6db3a71eb1b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470224"
---
# <a name="iteration-4--make-the-application-loosely-coupled-vb"></a>イテレーション #4 –アプリケーションを疎結合にする (VB)

[Microsoft](https://github.com/microsoft)

[コードのダウンロード](iteration-4-make-the-application-loosely-coupled-vb/_static/contactmanager_4_vb1.zip)

> この4回目のイテレーションでは、複数のソフトウェア設計パターンを利用して、連絡先マネージャーアプリケーションを簡単に管理および変更できるようにします。 たとえば、リポジトリパターンと依存関係の注入パターンを使用するようにアプリケーションをリファクターします。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Contact Management ASP.NET MVC アプリケーションの構築 (VB)

この一連のチュートリアルでは、最初から最後まで、連絡先管理アプリケーション全体を作成します。 連絡先マネージャーアプリケーションを使用すると、連絡先情報 (名前、電話番号、電子メールアドレスなど) をユーザーの一覧に格納できます。

複数のイテレーションに対してアプリケーションをビルドします。 各イテレーションで、アプリケーションを段階的に改善します。 この複数のイテレーションアプローチの目的は、各変更の理由を理解できるようにすることです。

- イテレーション #1-アプリケーションを作成します。 最初のイテレーションでは、最も簡単な方法で Contact Manager を作成します。 基本的なデータベース操作 (作成、読み取り、更新、削除) のサポートを追加します。

- イテレーション #2-アプリケーションの外観を良くします。 このイテレーションでは、既定の ASP.NET MVC ビューマスターページとカスケードスタイルシートを変更することによって、アプリケーションの外観を改善します。

- イテレーション #3-フォーム検証を追加します。 3番目のイテレーションでは、基本的なフォーム検証を追加します。 必要なフォームフィールドを完了しないで、フォームを送信できないようにします。 また、電子メールアドレスと電話番号も検証します。

- イテレーション #4-アプリケーションの疎結合を実現します。 この4回目のイテレーションでは、複数のソフトウェア設計パターンを利用して、連絡先マネージャーアプリケーションを簡単に管理および変更できるようにします。 たとえば、リポジトリパターンと依存関係の注入パターンを使用するようにアプリケーションをリファクターします。

- イテレーション #5-単体テストを作成します。 5番目のイテレーションでは、単体テストを追加することによって、アプリケーションの保守と変更を容易にします。 データモデルクラスをモック化し、コントローラーと検証ロジックの単体テストをビルドします。

- イテレーション #6-テスト駆動型開発を使用します。 この6番目のイテレーションでは、最初に単体テストを記述し、単体テストに対してコードを記述することによって、アプリケーションに新しい機能を追加します。 このイテレーションでは、連絡先グループを追加します。

- イテレーション #7-Ajax 機能を追加します。 7番目のイテレーションでは、Ajax のサポートを追加することによって、アプリケーションの応答性とパフォーマンスを向上させます。

## <a name="this-iteration"></a>このイテレーション

Contact Manager アプリケーションのこの4番目のイテレーションでは、アプリケーションの疎結合を行うようにアプリケーションをリファクターします。 アプリケーションが疎結合されている場合は、アプリケーションの他の部分のコードを変更することなく、アプリケーションのある部分でコードを変更できます。 疎結合アプリケーションでは、変更の回復性が向上します。

現在、Contact Manager アプリケーションで使用されるすべてのデータアクセスおよび検証ロジックは、コントローラークラスに含まれています。 これは不適切な考え方です。 アプリケーションの一部を変更する必要がある場合は常に、アプリケーションの別の部分にバグを導入するリスクがあります。 たとえば、検証ロジックを変更すると、新しいバグがデータアクセスまたはコントローラーロジックに導入されるリスクがあります。

> [!NOTE] 
> 
> (SRP) クラスは、複数の理由で変更することはできません。 コントローラー、検証、データベースのロジックを組み合わせることは、単一責任の原則に大きな違反となります。

アプリケーションの変更が必要になる理由はいくつかあります。 アプリケーションに新しい機能を追加する必要がある場合や、アプリケーションのバグを修正する必要がある場合、またはアプリケーションの機能を実装する方法を変更する必要がある場合があります。 アプリケーションが静的であることはほとんどありません。 時間の経過と共に成長し、変化する傾向があります。

たとえば、データアクセス層の実装方法を変更する場合を考えてみましょう。 現在、Contact Manager アプリケーションは、Microsoft Entity Framework を使用してデータベースにアクセスします。 ただし、ADO.NET Data Services や NHibernate などの別のデータアクセステクノロジに移行することもできます。 ただし、データアクセスコードは検証とコントローラーのコードから分離されていないため、データアクセスに直接関連しない他のコードを変更することなく、アプリケーションのデータアクセスコードを変更することはできません。

一方、アプリケーションが疎結合されている場合は、アプリケーションの他の部分に触れることなく、アプリケーションのある部分に変更を加えることができます。 たとえば、検証やコントローラーロジックを変更することなく、データアクセステクノロジを切り替えることができます。

このイテレーションでは、連絡先マネージャーアプリケーションをより疎結合されたアプリケーションにリファクタリングできるようにする、いくつかのソフトウェア設計パターンを利用しています。 完了すると、連絡先マネージャーは、これまでに実行されなかったことをすべて実行します。 ただし、将来、アプリケーションをより簡単に変更できるようになります。

> [!NOTE] 
> 
> リファクタリングは、既存の機能が失われないようにアプリケーションを書き換えるプロセスです。

## <a name="using-the-repository-software-design-pattern"></a>リポジトリソフトウェア設計パターンの使用

最初の変更点は、リポジトリパターンと呼ばれるソフトウェア設計パターンを利用することです。 リポジトリパターンを使用して、データアクセスコードをアプリケーションの他の部分から分離します。

リポジトリパターンを実装するには、次の2つの手順を完了する必要があります。

1. インターフェイスを作成する
2. インターフェイスを実装する具象クラスを作成する

最初に、実行する必要があるすべてのデータアクセスメソッドを記述するインターフェイスを作成する必要があります。 IContactManagerRepository インターフェイスは、リスト1に含まれています。 このインターフェイスには、CreateContact ()、DeleteContact ()、EditContact ()、GetContact、ListContacts () の5つのメソッドが記述されています。

**リスト 1-Models\IContactManagerRepository.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample1.vb)]

次に、IContactManagerRepository インターフェイスを実装する具象クラスを作成する必要があります。 ここでは、データベースにアクセスするために Microsoft Entity Framework を使用しているため、EntityContactManagerRepository という名前の新しいクラスを作成します。 このクラスは、リスト2に含まれています。

**リスト 2-Models\EntityContactManagerRepository.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample2.vb)]

EntityContactManagerRepository クラスに IContactManagerRepository インターフェイスが実装されていることに注意してください。 クラスは、そのインターフェイスによって記述された5つのメソッドすべてを実装します。

インターフェイスを使用する必要があるのはなぜでしょうか。 インターフェイスとそれを実装するクラスの両方を作成する必要があるのはなぜですか。

1つの例外として、アプリケーションの残りの部分は、具象クラスではなく、インターフェイスと対話します。 EntityContactManagerRepository クラスによって公開されるメソッドを呼び出すのではなく、IContactManagerRepository インターフェイスによって公開されているメソッドを呼び出します。

このようにして、アプリケーションの残りの部分を変更することなく、新しいクラスを使用してインターフェイスを実装できます。 たとえば、将来の日付で、IContactManagerRepository インターフェイスを実装する DataServicesContactManagerRepository クラスを実装することが必要になる場合があります。 DataServicesContactManagerRepository クラスは、ADO.NET Data Services を使用して、Microsoft Entity Framework ではなくデータベースにアクセスする場合があります。

アプリケーションコードが具象 EntityContactManagerRepository クラスではなく IContactManagerRepository インターフェイスに対してプログラミングされている場合、コードの残りの部分を変更せずに具象クラスを切り替えることができます。 たとえば、データアクセスや検証ロジックを変更せずに、EntityContactManagerRepository クラスから DataServicesContactManagerRepository クラスに切り替えることができます。

具象クラスではなくインターフェイス (抽象化) に対してプログラミングを行うと、アプリケーションの変更に対する回復性が向上します。

> [!NOTE] 
> 
> メニューオプション [リファクター]、[インターフェイスの抽出] の順に選択すると、Visual Studio 内の具象クラスからインターフェイスをすばやく作成できます。 たとえば、まず EntityContactManagerRepository クラスを作成し、次に Extract インターフェイスを使用して IContactManagerRepository インターフェイスを自動的に生成できます。

## <a name="using-the-dependency-injection-software-design-pattern"></a>依存関係の注入ソフトウェア設計パターンの使用

データアクセスコードを別のリポジトリクラスに移行したので、このクラスを使用するように Contact controller を変更する必要があります。 Microsoft は、コントローラーでリポジトリクラスを使用するために、依存関係の注入と呼ばれるソフトウェア設計パターンを利用します。

変更した連絡先コントローラーは、リスト3に含まれています。

**リスト 3-コントローラーと vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample3.vb)]

リスト3の Contact controller に2つのコンストラクターがあることに注意してください。 1つ目のコンストラクターは、IContactManagerRepository インターフェイスの具象インスタンスを2番目のコンストラクターに渡します。 Contact controller クラスは、*コンストラクターの依存関係の挿入*を使用します。

最初のコンストラクターでは、EntityContactManagerRepository クラスが使用されるのは1つだけです。 クラスの残りの部分では、具象 EntityContactManagerRepository クラスではなく、IContactManagerRepository インターフェイスを使用します。

これにより、将来、IContactManagerRepository クラスの実装を簡単に切り替えることができます。 EntityContactManagerRepository クラスの代わりに DataServicesContactRepository クラスを使用する場合は、最初のコンストラクターを変更するだけです。

コンストラクターの依存関係の挿入によって、Contact controller クラスも非常にテスト可能になります。 単体テストでは、IContactManagerRepository クラスのモック実装を渡すことによって Contact コントローラーをインスタンス化できます。 依存関係の注入のこの機能は、Contact Manager アプリケーションの単体テストをビルドするときに、次のイテレーションで非常に重要になります。

> [!NOTE] 
> 
> IContactManagerRepository インターフェイスの特定の実装から Contact controller クラスを完全に分離する場合は、構造体 Map や Microsoft のような依存関係の注入をサポートするフレームワークを利用できます。Entity Framework (MEF)。 依存関係挿入フレームワークを利用することで、コード内の具象クラスを参照する必要がなくなります。

## <a name="creating-a-service-layer"></a>サービス層の作成

リスト3の変更されたコントローラークラスのコントローラーロジックと検証ロジックが混在していることがわかっているかもしれません。 データアクセスロジックを分離するという同じ理由から、検証ロジックを分離することをお勧めします。

この問題を解決するには、別の[サービスレイヤー](http://martinfowler.com/eaaCatalog/serviceLayer.html)を作成します。 サービスレイヤーは、コントローラーとリポジトリクラスの間に挿入できる個別のレイヤーです。 サービス層には、すべての検証ロジックを含むビジネスロジックが含まれています。

ContactManagerService は、リスト4に含まれています。 これには、Contact controller クラスの検証ロジックが含まれています。

**リスト 4-Model\ Contactmanagerservice. vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample4.vb)]

ContactManagerService のコンストラクターには、ValidationDictionary が必要であることに注意してください。 サービス層は、この ValidationDictionary を介してコントローラーレイヤーと通信します。 次のセクションでは、デコレータパターンについて説明するときに、ValidationDictionary について詳しく説明します。

さらに、ContactManagerService が IContactManagerService インターフェイスを実装していることに注目してください。 具象クラスではなく、常にインターフェイスに対してプログラミングすることをお勧めします。 Contact Manager アプリケーションの他のクラスは、ContactManagerService クラスと直接やり取りしません。 代わりに、1つの例外を除き、Contact Manager アプリケーションの残りの部分は IContactManagerService インターフェイスに対してプログラミングされます。

IContactManagerService インターフェイスは、リスト5に含まれています。

**リスト 5-Models\IContactManagerService.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample5.vb)]

変更した Contact controller クラスは、リスト6に含まれています。 Contact controller が ContactManager リポジトリとやり取りしなくなったことに注意してください。 代わりに、Contact controller は ContactManager サービスとやり取りします。 各レイヤーは、他のレイヤーから可能な限り分離されます。

**リスト 6-コントローラーの一覧表示、vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample6.vb)]

このアプリケーションでは、単一責任原則 (SRP) の afoul が実行されなくなりました。 リスト6の連絡先コントローラーは、アプリケーション実行のフローを制御する以外に、すべての責任から取り除かれています。 すべての検証ロジックが Contact コントローラーから削除され、サービス層にプッシュされました。 すべてのデータベースロジックがリポジトリレイヤーにプッシュされました。

## <a name="using-the-decorator-pattern"></a>デコレータパターンの使用

ここでは、サービスレイヤーをコントローラーレイヤーから完全に分離できるようにしたいと考えています。 原則として、MVC アプリケーションに参照を追加しなくても、サービスレイヤーをコントローラーレイヤーとは別のアセンブリでコンパイルできるようにする必要があります。

ただし、サービスレイヤーは検証エラーメッセージをコントローラーレイヤーに渡すことができる必要があります。 サービス層がコントローラーとサービス層を結合せずに検証エラーメッセージを伝達できるようにするにはどうすればよいですか。 [デコレータパターン](http://en.wikipedia.org/wiki/Decorator_pattern)というソフトウェア設計パターンを利用できます。

コントローラーは ModelState という名前の ModelStateDictionary を使用して、検証エラーを表します。 そのため、コントローラーレイヤーからサービスレイヤーに ModelState を渡すことが必要になる場合があります。 ただし、サービス層で ModelState を使用すると、サービス層は ASP.NET MVC フレームワークの機能に依存するようになります。 これは、いつか、ASP.NET MVC アプリケーションではなく、WPF アプリケーションでサービス層を使用することが必要になる場合があるため、問題になります。 この場合、ModelStateDictionary クラスを使用するために ASP.NET MVC フレームワークを参照する必要はありません。

デコレータパターンを使用すると、インターフェイスを実装するために、新しいクラスの既存のクラスをラップすることができます。 連絡先マネージャープロジェクトには、リスト7に含まれる ModelStateWrapper クラスが含まれています。 ModelStateWrapper クラスは、リスト8のインターフェイスを実装します。

**リスト 7-Models\Validation\ModelStateWrapper.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample7.vb)]

**リスト 8-モデル \ 検証 \ vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample8.vb)]

リスト5をよく見ると、ContactManager サービスレイヤーが IValidationDictionary インターフェイスのみを使用していることがわかります。 ContactManager サービスは ModelStateDictionary クラスに依存しません。 Contact controller が ContactManager サービスを作成すると、コントローラーは次のように ModelState をラップします。

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample9.vb)]

## <a name="summary"></a>まとめ

このイテレーションでは、Contact Manager アプリケーションに新しい機能を追加しませんでした。 このイテレーションの目的は、連絡先マネージャーアプリケーションをリファクタリングして、管理と変更が容易になるようにすることでした。

まず、リポジトリソフトウェア設計パターンを実装しています。 すべてのデータアクセスコードを別の ContactManager リポジトリクラスに移行しています。

また、この検証ロジックをコントローラーロジックから分離しています。 ここでは、すべての検証コードを含む別のサービスレイヤーを作成しました。 コントローラーレイヤーはサービス層と対話し、サービス層はリポジトリレイヤーと対話します。

サービスレイヤーを作成したときに、デコレータパターンを利用してサービスレイヤーから ModelState を分離しました。 サービス層では、ModelState ではなく IValidationDictionary インターフェイスに対してプログラミングされていました。

最後に、依存関係の挿入パターンというソフトウェア設計パターンを利用しました。 このパターンを使用すると、具象クラスではなくインターフェイス (抽象化) に対してプログラミングできます。 依存関係の注入デザインパターンを実装することで、コードのテストが容易になります。 次のイテレーションでは、プロジェクトに単体テストを追加します。

> [!div class="step-by-step"]
> [前へ](iteration-3-add-form-validation-vb.md)
> [次へ](iteration-5-create-unit-tests-vb.md)

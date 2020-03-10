---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: 'イテレーション #6 –テスト駆動型開発を使用C#する () |Microsoft Docs'
author: microsoft
description: この6番目のイテレーションでは、最初に単体テストを記述し、単体テストに対してコードを記述することによって、アプリケーションに新しい機能を追加します。 このイテレーションの,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: aee0ff9d8d7f17e8a00dab12467bd3a3457fbe18
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487126"
---
# <a name="iteration-6--use-test-driven-development-c"></a>イテレーション #6 –テスト駆動開発 (C#) を使用する

[Microsoft](https://github.com/microsoft)

[コードのダウンロード](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> この6番目のイテレーションでは、最初に単体テストを記述し、単体テストに対してコードを記述することによって、アプリケーションに新しい機能を追加します。 このイテレーションでは、連絡先グループを追加します。

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Contact Management ASP.NET MVC アプリケーションの構築 (C#)

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

Contact Manager アプリケーションの前のイテレーションでは、コードの安全性を確保するための単体テストを作成しました。 単体テストを作成するための動機は、コードを変更するための回復力を高めることでした。 単体テストを実施することで、コードを適切に変更し、既存の機能が損なわれていないかどうかをすぐに確認することができます。

このイテレーションでは、まったく異なる目的で単体テストを使用します。 このイテレーションでは、*テスト駆動型開発*と呼ばれるアプリケーション設計思想の一部として単体テストを使用します。 テスト駆動開発を行う場合は、まずテストを作成してから、テストに対してコードを記述します。

より正確には、テスト駆動開発を実践するときに、コードを作成するときに実行する手順が3つあります (赤、緑、リファクタリング)。

1. 失敗した単体テストを記述する (赤)
2. 単体テストに合格するコードを記述する (緑)
3. コードをリファクターする (リファクター)

まず、単体テストを記述します。 単体テストでは、コードがどのように動作するかを判断する必要があります。 最初に単体テストを作成すると、単体テストは失敗します。 テストに適合するアプリケーションコードがまだ作成されていないため、テストは失敗します。

次に、単体テストを成功させるために十分なコードを記述します。 目標は、laziest、sloppiest、および最速の方法でコードを記述することです。 アプリケーションのアーキテクチャについて検討する時間を無駄にすることは避けてください。 代わりに、単体テストで表現される目的を満たすために必要な最小限のコードを記述することに重点を置いてください。

最後に、十分なコードを記述したら、前に戻って、アプリケーションの全体的なアーキテクチャを検討できます。 この手順では、リポジトリパターンなどのソフトウェア設計パターンを利用して、コードを書き直し (リファクター) します。これにより、コードの保守が容易になります。 コードは単体テストでカバーされているため、この手順でコードを書き直して完備ことができます。

テスト駆動開発の実践によって得られる多くの利点があります。 まず、テスト駆動開発では、実際に記述する必要があるコードに集中する必要があります。 特定のテストを渡すために十分なコードを記述するだけではないため、雑草に公して、使用しない大量のコードを記述することはできません。

2つ目は、"テストの最初の" 設計手法で、コードの使用方法の観点からコードを記述することです。 つまり、テスト駆動開発を実践する場合、ユーザーの観点からテストを常に作成することになります。 そのため、テスト駆動開発では、より明確でわかりやすい Api が得られます。

最後に、テスト駆動型開発では、通常のアプリケーション書き込みプロセスの一環として単体テストを記述する必要があります。 プロジェクトの期限のアプローチとして、通常、テストはウィンドウの最初の段階です。 一方、テスト駆動型の開発を練習する場合、単体テストの記述は、アプリケーションを構築するプロセスの中心となる単体テストを行うため、好循環になる可能性が高くなります。

> [!NOTE] 
> 
> テスト駆動開発の詳細については、**従来のコードで効果的**に Michael Feathers book を使用することをお勧めします。

このイテレーションでは、Contact Manager アプリケーションに新しい機能を追加します。 連絡先グループのサポートを追加します。 連絡先グループを使用して、連絡先をビジネスグループやフレンドグループなどのカテゴリに分類することができます。

テスト駆動型開発のプロセスに従って、この新しい機能をアプリケーションに追加します。 まず単体テストを作成し、これらのテストに対してすべてのコードを記述します。

## <a name="what-gets-tested"></a>テスト対象

前のイテレーションで説明したように、通常は、データアクセスロジックまたはビューロジックの単体テストを作成しません。 データベースにアクセスする操作は比較的低速であるため、データアクセスロジックの単体テストを作成することはできません。 ビューにアクセスするには、ビューロジックの単体テストを記述しないでください。ビューにアクセスするには、比較的低速な操作である web サーバーをスピンアップする必要があります。 テストを何度も高速に実行できる場合を除き、単体テストを記述しないでください

テスト駆動開発は単体テストによって主導されるため、最初にコントローラーとビジネスロジックを記述することに重点を置いています。 データベースまたはビューに触れることは避けてください。 このチュートリアルの最後まで、データベースを変更したり、ビューを作成したりすることはありません。 まず、テスト可能なものから始めます。

## <a name="creating-user-stories"></a>ユーザーストーリーの作成

テスト駆動開発を練習する場合は、常にテストを記述することから始めます。 これにより、最初に、どのようなテストを作成するかを決めることができます。 この質問に答えるには、一連の[**ユーザーストーリー**](http://en.wikipedia.org/wiki/User_stories)を記述する必要があります。

ユーザーストーリーは、ソフトウェア要件の概要 (通常は1文) です。 これは、ユーザーの観点から書かれた要件の技術的ではない説明にする必要があります。

ここでは、新しい連絡先グループの機能に必要な機能について説明した一連のユーザーストーリーについて説明します。

1. ユーザーは、連絡先グループの一覧を表示できます。
2. ユーザーは新しい連絡先グループを作成できます。
3. ユーザーは、既存の連絡先グループを削除できます。
4. ユーザーは、新しい連絡先を作成するときに連絡先グループを選択できます。
5. ユーザーは、既存の連絡先を編集するときに連絡先グループを選択できます。
6. 連絡先グループの一覧がインデックスビューに表示されます。
7. ユーザーが連絡先グループをクリックすると、一致する連絡先の一覧が表示されます。

このユーザーストーリーの一覧は、顧客が完全に理解できることに注意してください。 技術的な実装の詳細については説明しません。

アプリケーションの構築プロセス中に、一連のユーザーストーリーがより洗練されます。 ユーザーストーリーを複数のストーリー (要件) に分割することもできます。 たとえば、新しい連絡先グループを作成する場合は、検証が必要になることがあります。 名前なしで連絡先グループを送信すると、検証エラーが返されます。

ユーザーストーリーのリストを作成したら、最初の単体テストを記述することができます。 まず、連絡先グループの一覧を表示するための単体テストを作成します。

## <a name="listing-contact-groups"></a>連絡先グループの一覧表示

最初のユーザーストーリーは、ユーザーが連絡先グループの一覧を表示できるようにすることです。 このストーリーをテストで表現する必要があります。

新しい単体テストを作成するには、ContactManager. Tests プロジェクトで Controllers フォルダーを右クリックし、[**追加]、[新しいテスト**] の順に選択して、**単体テスト**テンプレートを選択します (図1を参照)。 新しい単体テストに GroupControllerTest.cs という名前を指定し、 **[OK]** ボタンをクリックします。

[Groupコントローラーテスト単体テストの追加 ![](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)

**図 01**: groupコントローラーテスト単体テスト[を追加する (クリックすると、フルサイズのイメージが表示](iteration-6-use-test-driven-development-cs/_static/image2.png)されます)

最初の単体テストは、リスト1に含まれています。 このテストでは、グループコントローラーの Index () メソッドがグループのセットを返すことを確認します。 このテストでは、グループのコレクションがビューデータで返されることを確認します。

**リスト 1-コントローラーのグループ \ コントローラー**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

Visual Studio でリスト1のコードを最初に入力すると、赤の波線が多数表示されます。 GroupController クラスまたは Group クラスが作成されていません。

この時点では、最初の単体テストを実行できないように、アプリケーションを構築することもできます。 すばらしいですね。 失敗したテストとしてカウントされます。 このため、アプリケーションコードの記述を開始するアクセス許可が与えられました。 テストを実行するには、十分なコードを記述する必要があります。

リスト2のグループコントローラークラスには、単体テストに合格するために必要な最小限のコードが含まれています。 Index () アクションは、静的にコード化されたグループのリストを返します (Group クラスはリスト3で定義されています)。

**リスト 2-コントローラーのグループ**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

**リスト 3-modelgroup、cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

GroupController クラスと Group クラスをプロジェクトに追加した後、最初の単体テストは正常に完了します (図2を参照)。 テストに合格するために必要な最小限の作業が完了しました。 お誕生日です。

[![成功しました。](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)

**図 02**: 成功!([クリックすると、フルサイズの画像が表示](iteration-6-use-test-driven-development-cs/_static/image4.png)される)

## <a name="creating-contact-groups"></a>連絡先グループの作成

これで、2番目のユーザーストーリーに進むことができます。 新しい連絡先グループを作成できる必要があります。 この目的をテストで表現する必要があります。

リスト4のテストでは、新しいグループを使用して Create () メソッドを呼び出すと、Index () メソッドによって返されるグループのリストにグループが追加されることが確認されます。 つまり、新しいグループを作成すると、Index () メソッドによって返されたグループの一覧から新しいグループを取得できるようになります。

**リスト 4-コントローラーのグループを一覧表示する**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

リスト4のテストは、新しい連絡先グループを使用して Group controller Create () メソッドを呼び出します。 次に、Group controller Index () メソッドを呼び出すと、ビューデータに新しいグループが返されることがテストによって確認されます。

リスト5の変更されたグループコントローラーには、新しいテストに合格するために必要な最小限の変更が含まれています。

**リスト 5-コントローラーの一覧 (& c)**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>リスト5のグループコントローラーには、新しい Create () 操作があります。 この操作では、グループのコレクションにグループを追加します。 Index () アクションが変更され、グループのコレクションの内容が返されていることに注意してください。

ここでも、単体テストに合格するために必要な最小限の作業が実行されています。 これらの変更をグループコントローラーに加えた後、すべての単体テストが成功します。

## <a name="adding-validation"></a>検証の追加

この要件は、ユーザーストーリーで明示的に記述されていません。 ただし、グループには名前が必要です。 そうしないと、連絡先をグループに分類するのはあまり役に立ちません。

リスト6には、この目的を表す新しいテストが含まれています。 このテストでは、名前を指定せずにグループを作成しようとすると、モデル状態に検証エラーメッセージが表示されることを確認します。

**一覧 6-コントローラー \ コントローラー**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

このテストを満たすためには、Group クラスに Name プロパティを追加する必要があります (リスト7を参照)。 さらに、Group controller s Create () アクションには、少しの検証ロジックを追加する必要があります (リスト8を参照)。

**リスト 7-modelgroupgroup, cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

**8-コントローラーの一覧表示**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

Group controller Create () アクションに検証とデータベースの両方のロジックが含まれていることに注意してください。 現在、グループコントローラーによって使用されるデータベースは、メモリ内コレクションを超えるものではありません。

## <a name="time-to-refactor"></a>リファクタリングする時間

赤/緑/リファクターの3番目の手順はリファクター部分です。 この時点で、コードからステップバックし、アプリケーションの設計を改善するためにアプリケーションをリファクターする方法を検討する必要があります。 リファクターステージは、ソフトウェア設計の原則とパターンを実装するための最適な方法を検討する段階です。

コードの設計を改善するために、コードを自由に変更することができます。 既存の機能を壊すことを防ぐために、単体テストの安全性が確保されています。

現時点では、グループコントローラーは優れたソフトウェア設計の観点からは厄介です。 グループコントローラーには、伴っの検証とデータアクセスのコードが含まれています。 単一責任の原則に違反しないようにするには、これらの懸念事項を別々のクラスに分ける必要があります。

リファクタリングされた Group controller クラスは、リスト9に含まれています。 このコントローラーは、ContactManager サービスレイヤーを使用するように変更されています。 これは、Contact コントローラーで使用するのと同じサービス層です。

リスト10には、グループの検証、一覧表示、および作成をサポートするために、ContactManager サービスレイヤーに追加された新しいメソッドが含まれています。 IContactManagerService インターフェイスが更新され、新しいメソッドが追加されました。

リスト11には、IContactManagerRepository インターフェイスを実装する新しい FakeContactManagerRepository クラスが含まれています。 IContactManagerRepository インターフェイスも実装する EntityContactManagerRepository クラスとは異なり、新しい FakeContactManagerRepository クラスはデータベースとは通信しません。 FakeContactManagerRepository クラスは、メモリ内コレクションをデータベースのプロキシとして使用します。 このクラスは、フェイクリポジトリレイヤーとして、単体テストで使用します。

**リスト 9-コントローラーグループ**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

**10コントローラーの一覧を表示します。**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

**リスト 11-Controllers\FakeContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

IContactManagerRepository インターフェイスを変更するには、EntityContactManagerRepository クラスで CreateGroup () メソッドと ListGroups () メソッドを実装するためにを使用する必要があります。 これを行うための laziest と最速の方法は、次のようなスタブメソッドを追加することです。   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]

最後に、このようなアプリケーションの設計を変更するには、単体テストに変更を加える必要があります。 次に、単体テストを実行するときに FakeContactManagerRepository を使用する必要があります。 更新された Groupコントローラーテストクラスは、リスト12に含まれています。

**12コントローラーを一覧表示します。**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

これらの変更をすべて行った後、すべての単体テストに合格します。 赤/緑/リファクターのサイクル全体が完了しました。 最初の2つのユーザーストーリーを実装しました。 ユーザーストーリーに示されている要件の単体テストがサポートされるようになりました。 ユーザーストーリーの残りの部分を実装する場合は、赤/緑/リファクターと同じサイクルを繰り返す必要があります。

## <a name="modifying-our-database"></a>データベースの変更

残念ながら、単体テストで表現されるすべての要件を満たしていても、作業は行われません。 この場合も、データベースを変更する必要があります。

新しいグループデータベーステーブルを作成する必要があります。 次の手順に従います。

1. サーバーエクスプローラー ウィンドウで、テーブル フォルダーを右クリックし、**新しいテーブルの追加** メニューオプションを選択します。
2. 次に示す2つの列をテーブルデザイナーで入力します。
3. Id 列を主キーと Id 列としてマークします。
4. フロッピーのアイコンをクリックして、新しいテーブルを名前のグループと共に保存します。

<a id="0.11_table01"></a>

| **列名** | **[データ型]** | **[NULL を許容]** |
| --- | --- | --- |
| Id | INT | False |
| Name | nvarchar(50) | False |

次に、Contacts テーブルからすべてのデータを削除する必要があります (それ以外の場合、Contacts テーブルと Groups テーブルの間にリレーションシップを作成することはできません)。 次の手順に従います。

1. Contacts テーブルを右クリックし、 **[テーブルデータの表示]** メニューオプションを選択します。
2. すべての行を削除します。

次に、グループデータベーステーブルと既存の Contacts データベーステーブルの間のリレーションシップを定義する必要があります。 次の手順に従います。

1. サーバーエクスプローラーウィンドウで Contacts テーブルをダブルクリックして、テーブルデザイナーを開きます。
2. GroupId という名前の Contacts テーブルに新しい整数型の列を追加します。
3. [リレーションシップ] ボタンをクリックして、[外部キーのリレーションシップ] ダイアログを開きます (図3を参照)。
4. [追加] ボタンをクリックします。
5. [テーブルと列の指定] ボタンの横に表示される省略記号ボタンをクリックします。
6. [テーブルと列] ダイアログボックスで、主キーテーブルとして [グループ] を主キー列として選択します。 外部キーテーブルとして [連絡先] を、外部キー列として [GroupId] を選択します (図4を参照)。 [OK] ボタンをクリックします。
7. **[挿入および更新の指定]** で、 **[ルールの削除]** に値**Cascade**を選択します。
8. [閉じる] ボタンをクリックして、[外部キーのリレーションシップ] ダイアログを閉じます。
9. [保存] ボタンをクリックして、Contacts テーブルへの変更を保存します。

[データベーステーブルリレーションシップの作成 ![](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)

**図 03**: データベーステーブルのリレーションシップの作成 ([クリックすると、フルサイズの画像が表示](iteration-6-use-test-driven-development-cs/_static/image6.png)される)

[テーブルのリレーションシップを指定 ![](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)

**図 04**: テーブルリレーションシップの指定 ([クリックすると、フルサイズの画像が表示](iteration-6-use-test-driven-development-cs/_static/image8.png)される)

### <a name="updating-our-data-model"></a>データモデルを更新しています

次に、新しいデータベーステーブルを表すようにデータモデルを更新する必要があります。 次の手順に従います。

1. [モデル] フォルダー内の ContactManagerModel .edmx ファイルをダブルクリックして、Entity Designer を開きます。
2. デザイナー画面を右クリックし、 **[データベースからモデルを更新]** メニューオプションを選択します。
3. 更新ウィザードで、[グループ] テーブルを選択し、[完了] ボタンをクリックします (図5を参照)。
4. Groups エンティティを右クリックし、メニューオプション **[名前の変更]** を選択します。 *グループ*エンティティの名前を "*グループ*" (単数形) に変更します。
5. Contact エンティティの下部に表示される [グループ] ナビゲーションプロパティを右クリックします。 *Groups*ナビゲーションプロパティの名前を " *Group* (単数)" に変更します。

[データベースから Entity Framework モデルを更新 ![には](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)

**図 05**: データベースから Entity Framework モデルを更新する ([クリックすると、フルサイズの画像が表示](iteration-6-use-test-driven-development-cs/_static/image10.png)されます)

これらの手順を完了すると、データモデルが連絡先テーブルとグループテーブルの両方を表すようになります。 Entity Designer には両方のエンティティが表示されます (図6を参照)。

[グループと連絡先の表示 Entity Designer ![](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)

**図 06**: グループと連絡先を表示する Entity Designer ([クリックすると、フルサイズの画像が表示](iteration-6-use-test-driven-development-cs/_static/image12.png)されます)

### <a name="creating-our-repository-classes"></a>リポジトリクラスの作成

次に、リポジトリクラスを実装する必要があります。 このイテレーションの過程で、単体テストを満たすコードを記述しながら、IContactManagerRepository インターフェイスにいくつかの新しいメソッドを追加しました。 IContactManagerRepository インターフェイスの最終バージョンは、一覧14に含まれています。

**リスト 14-Models\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

連絡先グループの操作に関連するどの方法も実際には実装していません。 現在、EntityContactManagerRepository クラスには、IContactManagerRepository インターフェイスに示されている contact group メソッドごとにスタブメソッドがあります。 たとえば、ListGroups () メソッドは現在、次のようになります。

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

スタブメソッドは、アプリケーションをコンパイルし、単体テストに合格できるようにしました。 しかし、ここでは、これらのメソッドを実際に実装します。 EntityContactManagerRepository クラスの最終バージョンは、一覧13に含まれています。

**リスト 13-Models\EntityContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a>ビューの作成

既定の ASP.NET view engine を使用する場合の ASP.NET MVC アプリケーション。 そのため、特定の単体テストに応答してビューを作成することはできません。 ただし、アプリケーションはビューなしでは役に立たないため、Contact Manager アプリケーションに含まれるビューを作成したり変更したりしなくても、このイテレーションを完了できます。

連絡先グループを管理するには、次の新しいビューを作成する必要があります (図7を参照)。

- Views\Group\Index.aspx-連絡先グループの一覧を表示します。
- Views\Group\Delete.aspx-連絡先グループを削除するための確認フォームが表示されます。

[グループインデックスビューの ![](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)

**図 07**: グループのインデックスビュー ([クリックすると、フルサイズの画像が表示](iteration-6-use-test-driven-development-cs/_static/image14.png)されます)

連絡先グループを含むように、次の既存のビューを変更する必要があります。

- Views\Home\Create.aspx
- Views\Home\Edit.aspx
- Views\Home\Index.aspx

このチュートリアルに付属している Visual Studio アプリケーションを見ると、変更されたビューを確認できます。 たとえば、図8は、連絡先のインデックスビューを示しています。

[連絡先のインデックスビューを ![する](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)

**図 08**: 連絡先のインデックスビュー ([クリックすると、フルサイズの画像が表示](iteration-6-use-test-driven-development-cs/_static/image16.png)されます)

## <a name="summary"></a>まとめ

このイテレーションでは、テスト駆動型開発アプリケーションの設計方法に従って、Contact Manager アプリケーションに新しい機能を追加しました。 まず、一連のユーザーストーリーを作成しました。 ユーザーストーリーによって表される要件に対応する一連の単体テストを作成しました。 最後に、単体テストで表現される要件を満たすのに十分なコードを記述しました。

単体テストで表現された要件を満たすために十分なコードを記述したら、データベースとビューを更新しました。 データベースに新しい Groups テーブルを追加し、Entity Framework データモデルを更新しました。 また、一連のビューを作成して変更しました。

次のイテレーション (最後のイテレーション) では、Ajax を利用するようにアプリケーションを書き直します。 Ajax を利用することで、Contact Manager アプリケーションの応答性とパフォーマンスが向上します。

> [!div class="step-by-step"]
> [前へ](iteration-5-create-unit-tests-cs.md)
> [次へ](iteration-7-add-ajax-functionality-cs.md)

---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 自動単体テストを有効にする |Microsoft Docs
author: microsoft
description: 手順 12. では、一連の自動単体テストを開発し、その機能を確認して、変更を行うための信頼を付与する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 09a7aa186605a6cce48ee94028425ded957c00d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435592"
---
# <a name="enable-automated-unit-testing"></a>自動化された単体テストを有効にする

[Microsoft](https://github.com/microsoft)

[[Download PDF]\(PDF をダウンロード\)](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、ASP.NET MVC 1 を使用して小規模で完成した web アプリケーションを構築する方法を説明する、無料の["" アプリケーションのチュートリアル](introducing-the-nerddinner-tutorial.md)の手順12です。
> 
> 手順 12. では、自動単体テストのスイートを開発し、その機能を検証します。これにより、将来アプリケーションの変更や機能強化を行う自信が得られます。
> 
> ASP.NET MVC 3 を使用している場合は、MVC 3 または[Mvc ミュージックストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[のチュートリアルではじめに](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)に従うことをお勧めします。

## <a name="nerddinner-step-12-unit-testing"></a>ステップ 12: 単体テストを実行する

この一連の自動化された単体テストを開発して、その機能を確認します。これにより、将来、アプリケーションの変更や改善を行う自信が得られます。

### <a name="why-unit-test"></a>単体テストの理由

このドライブを使用すると、作業中のアプリケーションに関するインスピレーションの突然のフラッシュが発生します。 アプリケーションのパフォーマンスを大幅に向上させるために実装できる変更があることを認識しています。 コードをクリーンアップしたり、新しい機能を追加したり、バグを修正したりするリファクタリングが考えられます。

お客様のコンピューターに到着したときの問題は、「この改善にはどの程度の安全性がありますか」ということです。 変更を行うと副作用が発生したり、何かが壊れる場合はどうなるでしょうか。 変更は単純で、実装には数分かかりますが、すべてのアプリケーションシナリオを手動でテストするのに数時間かかる場合はどうでしょうか。 シナリオの内容を忘れた場合、アプリケーションの運用が中断された場合はどうなりますか。 この機能強化によってすべての作業に大きな価値を持たせるのでしょうか。

自動化された単体テストは、アプリケーションを継続的に強化し、作業しているコードを恐れることがないようにする安全なネットワークを提供できます。 機能を迅速に検証する自動テストを使用すると、自信を持ってコーディングすることができ、それ以外の方法では満足できないように改善することができます。 また、保守性が高く、有効期間が長いソリューションを作成するのにも役立ちます。これにより、投資収益率が大幅に向上します。

ASP.NET MVC フレームワークを使用すると、単体テストアプリケーションの機能が簡単かつ自然になります。 また、テスト駆動開発 (TDD) ワークフローを有効にして、テストファーストベースの開発を可能にします。

### <a name="nerddinnertests-project"></a>NerdDinner.Tests Project

このチュートリアルの最初に、このチュートリアルの最初に「このアプリケーションを作成したときに、アプリケーションプロジェクトと一緒に実行する単体テストプロジェクトを作成する必要があるかどうかを確認するダイアログが表示されました。

![](enable-automated-unit-testing/_static/image1.png)

[はい、単体テストプロジェクトを作成する] オプションボタンをオンにしました。これにより、ソリューションに追加される "実行中のテスト" プロジェクトになります。

![](enable-automated-unit-testing/_static/image2.png)

このプロジェクトでは、このプロジェクトアセンブリを参照して、アプリケーションの機能を確認する自動テストを簡単に追加できます。

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>ディナーモデルクラスの単体テストの作成

モデルレイヤーを構築したときに作成したディナークラスを検証するテストを、このプロジェクトに追加してみましょう。

まず、"モデル" という名前のテストプロジェクト内に新しいフォルダーを作成します。このフォルダーには、モデル関連のテストを配置します。 次に、フォルダーを右クリックし、[**新しいテストの&gt;追加**] メニューコマンドを選択します。 [新しいテストの追加] ダイアログが表示されます。

"単体テスト" を作成し、"DinnerTest.cs" という名前を指定します。

![](enable-automated-unit-testing/_static/image3.png)

[Ok] ボタンをクリックすると、Visual Studio によって DinnerTest.cs ファイルがプロジェクトに追加 (開き) されます。

![](enable-automated-unit-testing/_static/image4.png)

既定の Visual Studio 単体テストテンプレートには、少し乱雑なボイラーコードが含まれています。 次のコードを含むようにクリーンアップしてみましょう。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

上記の Dinのテストクラスの [TestClass] 属性は、テストを含むクラスとして、およびオプションのテストの初期化および破棄コードを指定します。 この中に、[設定可能] 属性を持つパブリックメソッドを追加することによって、テストを定義できます。

次に、ディナークラスを実行する2つのテストの最初の例を示します。 最初のテストでは、すべてのプロパティが正しく設定されていない状態で新しいディナーが作成された場合に、ディナーが無効であることを確認します。 2番目のテストでは、ディナーがすべてのプロパティに有効な値を設定しているときに、ディナーが有効であることを確認します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

上記のテスト名は、非常に明確なものです (多少詳細)。 これは、数百または数千の小さなテストが作成される可能性があり、それぞれの意図と動作を簡単に判断できるようにするためです (特に、テストランナーでのエラーの一覧を参照している場合)。 テスト名は、テスト対象の機能の後に名前を付ける必要があります。 上の例では、"名詞\_\_動詞" という名前付けパターンを使用しています。

"AAA" テストパターンを使用してテストを構成しています。これは "Arrange, Act, Assert" を意味します。

- 配置: テスト対象の単位を設定します。
- Act: テストとキャプチャの結果で単位を練習する
- Assert: 動作を確認します。

テストを作成するときは、個々のテストがあまり多くなることを避ける必要があります。 代わりに、各テストで1つの概念のみを検証する必要があります (これにより、障害の原因を特定しやすくなります)。 テストごとに1つの assert ステートメントのみを使用することをお勧めします。 テストメソッドに複数の assert ステートメントがある場合は、それらがすべて同じ概念のテストに使用されていることを確認してください。 不明な場合は、別のテストを行います。

### <a name="running-tests"></a>テストの実行

Visual Studio 2008 Professional (およびそれ以降のエディション) には、IDE 内で Visual Studio 単体テストプロジェクトを実行するために使用できる組み込みのテストランナーが含まれています。 [ソリューション] メニューコマンド (または、Ctrl + A) を押してすべての単体テストを実行するには、**テスト&gt;実行&gt;すべてのテスト**を選択できます。 または、特定のテストクラスまたはテストメソッド内にカーソルを配置し、[現在のコンテキストメニューコマンド**でテスト&gt;実行&gt;テスト**を使用する] (または、Ctrl + t キーを押して) 単体テストのサブセットを実行することもできます。

Dinのテストクラス内にカーソルを置き、「Ctrl R, T」と入力して、先ほど定義した2つのテストを実行します。 これを行うと、Visual Studio 内に "テスト結果" ウィンドウが表示され、テストの実行結果がその中に表示されます。

![](enable-automated-unit-testing/_static/image5.png)

*注: [VS テストの結果] ウィンドウには、既定では [クラス名] 列が表示されません。これを追加するには、[テスト結果] ウィンドウ内で右クリックし、[列の追加と削除] メニューコマンドを使用します。*

2つのテストが実行されるのは1秒未満で、両方が成功したことがわかります。 ここでは、特定の規則の検証を確認する追加のテストを作成してそれを拡張し、ディナークラスに追加した2つのヘルパーメソッドである IsUserHost () と Isuserhost () について説明します。 これらのすべてのテストをディナークラスに対して実施することで、将来的に新しいビジネスルールと検証を追加することがより簡単かつ安全になります。 新しいルールロジックをディナーに追加し、数秒以内に以前のロジック機能が壊れていないことを確認できます。

説明的なテスト名を使用することにより、各テストがどのように検証されているかを簡単に把握できることに注意してください。 [**ツール]-&gt;[オプション**] メニューコマンドを使用して、[テストツール-&gt;テスト実行構成] 画面を開き、[失敗または結果不確定の単体テストの結果をダブルクリックするとテストの失敗ポイントを表示する] チェックボックスをオンにすることをお勧めします。 これにより、[テスト結果] ウィンドウでエラーをダブルクリックして、すぐにアサートエラーに戻ることができます。

### <a name="creating-dinnerscontroller-unit-tests"></a>Dincontroller の単体テストの作成

次に、Dincontroller 機能を検証する単体テストを作成しましょう。 まず、テストプロジェクト内の "Controllers" フォルダーを右クリックし、[**新しいテストの&gt;追加**] メニューコマンドを選択します。 "単体テスト" を作成し、"DinnersControllerTest.cs" という名前を指定します。

Dinで Details () アクションメソッドを確認する2つのテストメソッドを作成します。 最初のは、既存のディナーが要求されたときにビューが返されることを確認します。 2番目の方法では、存在しないディナーが要求されたときに "NotFound" ビューが返されることを確認します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

上記のコードはクリーンをコンパイルします。 ただし、テストを実行すると、どちらも失敗します。

![](enable-automated-unit-testing/_static/image6.png)

エラーメッセージが表示された場合、テストが失敗した理由は、Dinは Srepository クラスがデータベースに接続できなかったためです。 Linux アプリケーションでは、ローカル SQL Server Express ファイルへの接続文字列を使用しています。このファイルは、linux アプリケーションプロジェクトの \ App\_Data ディレクトリに存在します。 このテストプロジェクトは別のディレクトリでコンパイルおよび実行されるため、アプリケーションプロジェクトでは、接続文字列の相対パスの場所は正しくありません。

この問題*を解決する*には、SQL Express データベースファイルをテストプロジェクトにコピーし、テストプロジェクトの app.config に適切なテスト接続文字列を追加します。 これにより、上記のテストがブロック解除され、実行されます。

ただし、実際のデータベースを使用した単体テストのコードには、多くの課題があります。 具体的な内容は次のとおりです。

- 単体テストの実行時間が大幅に低下します。 テストの実行にかかる時間が長くなるほど、頻繁に実行される可能性が低くなります。 単体テストを数秒で実行できるようにすることをお勧めします。これは、プロジェクトをコンパイルするのと同じように行うことができます。
- これにより、テスト内のセットアップロジックとクリーンアップロジックが複雑になります。 各単体テストが分離され、他の単体テストに依存しないようにする必要があります (副作用も依存関係もありません)。 実際のデータベースに対して作業する場合は、状態を考慮して、テスト間でリセットする必要があります。

これらの問題を回避し、実際のデータベースをテストで使用する必要がないようにするための "依存関係の注入" という設計パターンを見てみましょう。

### <a name="dependency-injection"></a>依存関係の挿入

現在では、コントローラーは dinのリポジトリクラスに密に "結合" されています。 "結合" とは、クラスが動作するために別のクラスに明示的に依存している状況を指します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

Dinのリポジトリクラスはデータベースへのアクセスを必要とするため、dinを使用したのと同じように結合された依存関係は、dinのコントローラーのアクションメソッドをテストするためにデータベースを用意する必要があります。

この問題を回避するには、"依存関係の挿入" というデザインパターンを使用します。これは、依存関係 (データアクセスを提供するリポジトリクラスなど) が、それらを使用するクラス内で暗黙的に作成されなくなる方法です。 代わりに、コンストラクター引数を使用して、依存関係を使用するクラスに明示的に渡すことができます。 依存関係がインターフェイスを使用して定義されている場合、単体テストシナリオの "偽の" 依存関係の実装を柔軟に渡すことができます。 これにより、実際にはデータベースへのアクセスを必要としない、テスト固有の依存関係の実装を作成できます。

この動作を確認するために、Dinのコントローラーとの依存関係の挿入を実装してみましょう。

#### <a name="extracting-an-idinnerrepository-interface"></a>IDinnerRepository インターフェイスを抽出しています

最初の手順として、コントローラーがディナーを取得して更新するために必要なリポジトリコントラクトをカプセル化する新しい IDinnerRepository インターフェイスを作成します。

このインターフェイスコントラクトを手動で定義するには、[モデル] フォルダーを右クリックし、[**新しい項目の&gt;追加**] メニューコマンドを選択して、IDinnerRepository.cs という名前の新しいインターフェイスを作成します。

または、リファクタリングツールを組み込み Visual Studio Professional (およびそれ以降のエディション) を使用して、既存の Dinのリポジトリクラスから自動的にインターフェイスを抽出して作成することもできます。 VS を使用してこのインターフェイスを抽出するには、Dinレポジトリクラスのテキストエディターにカーソルを置き、右クリックして [**リファクター-&gt;Extract インターフェイス**] メニューコマンドを選択します。

![](enable-automated-unit-testing/_static/image7.png)

[インターフェイスの抽出] ダイアログボックスが開き、作成するインターフェイスの名前を入力するように求められます。 既定では IDinnerRepository に設定され、既存の Dinのリポジトリクラスのすべてのパブリックメソッドを自動的に選択して、インターフェイスに追加します。

![](enable-automated-unit-testing/_static/image8.png)

[Ok] ボタンをクリックすると、Visual Studio によって、新しい IDinnerRepository インターフェイスがアプリケーションに追加されます。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

また、既存の Dinのリポジトリクラスは、インターフェイスを実装するように更新されます。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>コンストラクターの挿入をサポートするように Dinを更新しています

次に、新しいインターフェイスを使用するように Dinのコントローラークラスを更新します。

現在は、"Dinのリポジトリ" フィールドが常に Dinのリポジトリクラスであるように、次のようにハードコーディングされています。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

これを変更して、"Dinレポジトリ" フィールドの種類が、Dinではなく IDinnerRepository になるようにします。 次に、2つのパブリック Dinscontroller コンストラクターを追加します。 コンストラクターの1つで、IDinnerRepository を引数として渡すことができます。 もう1つは、既存の Dinのリポジトリ実装を使用する既定のコンストラクターです。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

既定の ASP.NET MVC では既定のコンストラクターを使用してコントローラークラスが作成されるため、実行時の dinは、データアクセスを実行するために dinのリポジトリクラスを引き続き使用します。

ここでは、単体テストを更新して、パラメーターコンストラクターを使用して "偽の" ディナーリポジトリの実装を渡すことができるようになりました。 この "偽の" ディナーリポジトリは実際のデータベースへのアクセスを必要とせず、代わりにメモリ内のサンプルデータを使用します。

#### <a name="creating-the-fakedinnerrepository-class"></a>FakeDinnerRepository クラスの作成

FakeDinnerRepository クラスを作成してみましょう。

まず、このプロジェクト内に "フェイク" ディレクトリを作成してから、新しい FakeDinnerRepository クラスを追加します (フォルダーを右クリックし、[&gt;追加]、 **[新しいクラス]** の順に選択します)。

![](enable-automated-unit-testing/_static/image9.png)

ここでは、FakeDinnerRepository クラスが IDinnerRepository インターフェイスを実装するようにコードを更新します。 次に、それを右クリックし、[interface IDinnerRepository を実装する] コンテキストメニューコマンドを選択します。

![](enable-automated-unit-testing/_static/image10.png)

これにより、Visual Studio は、既定の "スタブアウト" の実装を使用して、すべての IDinnerRepository インターフェイスメンバーを FakeDinnerRepository クラスに自動的に追加します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

次に、Fakedinを更新して、メモリ内のリスト&lt;ディナー&gt; コレクションをコンストラクター引数として渡すことができます。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

これで、データベースを必要としないフェイクの IDinnerRepository 実装が作成されました。代わりに、ディナーオブジェクトのメモリ内リストを使用できなくなります。

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>単体テストでの Fakedinを使用したリポジトリの使用

データベースが使用できなかったために、前に失敗した Dincontroller の単体テストに戻りましょう。 テストメソッドを更新して、次のコードを使用して、メモリ内のディナーデータをサンプルに設定した Fakedinのリポジトリを使用するように更新できます。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

これらのテストを実行すると、両方とも次のようになります。

![](enable-automated-unit-testing/_static/image11.png)

何よりも、実行にはほんの数分しかかかりません。複雑なセットアップ/クリーンアップロジックは必要ありません。 これで、実際のデータベースに接続しなくても、すべての Dinのコントローラーのアクションメソッドコード (リスティング、ページング、詳細、作成、更新、削除など) を単体テストできるようになりました。

| **サイドトピック: 依存関係挿入フレームワーク** |
| --- |
| (上記のように) 手動による依存関係の挿入の実行は正常に機能しますが、アプリケーション内の依存関係とコンポーネントの数が増えるにつれて、保守が困難になります。 .NET には、依存関係の管理の柔軟性をさらに高めるのに役立つ、いくつかの依存関係挿入フレームワークが用意されています。 これらのフレームワークは、"コントロールの反転" (IoC) コンテナーとも呼ばれ、実行時に依存関係を指定してオブジェクトに渡すための構成サポートのレベルを追加できるようにするメカニズムを提供します (ほとんどの場合、コンストラクターの挿入を使用します)。). .NET での OSS 依存関係の注入/IOC フレームワークの中には、AutoFac、Ninject、Spring.NET、構造マップ、Windsor といった一般的なものがあります。 ASP.NET MVC は、開発者がコントローラーの解決とインスタンス化に参加できるようにする機能拡張 Api を公開します。これにより、このプロセス内で依存関係の挿入/IoC フレームワークを完全に統合できます。 DI/IOC フレームワークを使用すると、Dinのコントローラーから既定のコンストラクターを削除することもできます。これにより、このコンストラクターと Dinのリポジトリ間の結合が完全に削除されます。 私たちは、このアプリケーションでは、依存関係の注入/IOC フレームワークを使用しません。 しかし、これは将来のコードベースと機能が拡張された場合に考えられるものです。 |

### <a name="creating-edit-action-unit-tests"></a>編集アクションの単体テストを作成する

次に、Dinのコントローラーの編集機能を検証する単体テストを作成してみましょう。 まず、編集操作の HTTP-GET バージョンをテストします。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

次に、有効なディナーが要求されたときに Dinによってサポートされるビューが返されることを確認するテストを作成します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

ただし、テストを実行すると失敗することがわかります。これは、Edit メソッドが User.Identity.Name プロパティにアクセスして IsHostedBy () チェックを実行すると null 参照例外がスローされるためです。

コントローラーの基本クラスの User オブジェクトは、ログインしているユーザーに関する詳細をカプセル化し、実行時にコントローラーを作成するときに ASP.NET MVC によって設定されます。 Web サーバー環境の外部で Dinをテストしているため、ユーザーオブジェクトが設定されていません (したがって、null 参照の例外が発生します)。

### <a name="mocking-the-useridentityname-property"></a>User.Identity.Name プロパティのモック

モックフレームワークを使用すると、テストをサポートする依存オブジェクトのフェイクバージョンを動的に作成できるようになるため、テストが容易になります。 たとえば、編集アクションテストでモックフレームワークを使用して、ユーザーオブジェクトを動的に作成することができます。このオブジェクトは、ユーザーオブジェクトを使用して、シミュレートされたユーザー名を検索するために使用できます。 これにより、テストの実行時に null 参照がスローされるのを防ぐことができます。

ASP.NET MVC では、多くの .NET モックフレームワークを使用できます (ここでは、 [http://www.mockframeworks.com/](http://www.mockframeworks.com/))。 このアプリケーションをテストするために、"Moq" と呼ばれるオープンソースのモックフレームワークを使用します。これは、 [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)から無料でダウンロードできます。

ダウンロードが完了したら、次のように Moq .dll アセンブリに参照を追加します。

![](enable-automated-unit-testing/_static/image12.png)

次に、"CreateDinnersControllerAs (username)" というヘルパーメソッドをテストクラスに追加します。このメソッドは、パラメーターとしてユーザー名を受け取り、次に "モック" を使用します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

上の例では、Moq を使用して、コントローラーのコンテキストオブジェクトをフェイクするモックオブジェクトを作成します (ASP.NET MVC は、ユーザー、要求、応答、セッションなどのランタイムオブジェクトを公開するためにコントローラークラスに渡されます)。 モックで "SetupGet" メソッドを呼び出して、コントローラーの HttpContext.User.Identity.Name プロパティがヘルパーメソッドに渡されたユーザー名文字列を返す必要があることを示しています。

任意の数のコントローラーのコンテキストプロパティとメソッドをモックできます。 このことを示すために、要求の IsAuthenticated プロパティのための SetupGet () 呼び出しも追加しました (以下のテストでは実際には必要ありませんが、要求プロパティをモックする方法を説明しています)。 この作業が完了したら、ヘルパーメソッドが返す、コントローラーに対して、コントローラーに対して、コントローラーのインスタンスを割り当てます。

このヘルパーメソッドを使用して、さまざまなユーザーに関係する編集シナリオをテストする単体テストを作成できるようになりました。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

テストを実行すると、次のようになります。

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>UpdateModel () シナリオのテスト

編集アクションの HTTP GET バージョンをカバーするテストを作成しました。 次に、編集アクションの HTTP ポストバージョンを検証するテストを作成しましょう。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

このアクションメソッドをサポートするための興味深い新しいテストシナリオは、コントローラーの基本クラスで UpdateModel () ヘルパーメソッドを使用することです。 このヘルパーメソッドを使用して、フォームポストの値をディナーオブジェクトインスタンスにバインドしています。

次の2つのテストは、使用する UpdateModel () ヘルパーメソッドのフォームポスト値を指定する方法を示しています。 これを行うには、FormCollection オブジェクトを作成および設定してから、コントローラーの "ValueProvider" プロパティに割り当てます。

最初のテストでは、保存が成功したときに、ブラウザーが詳細アクションにリダイレクトされることを確認します。 2番目のテストでは、無効な入力が投稿されたときに、操作によって編集ビューが再度表示され、エラーメッセージが表示されることを確認します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>テストのラップアップ

ここでは、単体テストコントローラークラスに関連する主要な概念について説明しました。 これらの手法を使用すると、アプリケーションの動作を検証する数百の単純なテストを簡単に作成できます。

コントローラーとモデルのテストは実際のデータベースを必要としないため、非常に高速で簡単に実行できます。 数百の自動テストを数秒で実行できるようになり、加えた変更によって何かが破損していないかどうかについてすぐにフィードバックを受け取ることができます。 これにより、アプリケーションを継続的に改善、リファクタリング、および改良することができます。

この章の最後のトピックとして、テストについて説明しました。テストは開発プロセスの最後に行う必要があります。 逆に、開発プロセスでできるだけ早く自動テストを記述する必要があります。 これにより、開発時にすぐにフィードバックを取得できるようになり、アプリケーションのユースケースシナリオについて熟考と考えることができます。また、クリーンなレイヤーと結合を念頭に置いてアプリケーションを設計するためのガイドもあります。

この書籍の後半の章では、テスト駆動開発 (TDD) について説明し、ASP.NET MVC での使用方法について説明します。 TDD は反復的なコーディング手法であり、結果のコードが満たすテストを最初に記述します。 TDD では、実装する機能を検証するテストを作成して、各機能を開始します。 最初に単体テストを記述することで、機能を明確に理解し、それがどのように動作するかを明確に把握できます。 テストが作成された後にのみ (エラーが発生したことを確認した後)、テストによって検証される実際の機能を実装します。 機能がどのように動作するかについての考慮事項を既に費やしているので、要件とその実装に最適な方法を理解する必要があります。 実装が完了したら、テストを再実行して、機能が正しく動作するかどうかについてすぐにフィードバックを受け取ることができます。 TDD の詳細については、10章を参照してください。

### <a name="next-step"></a>次の手順

最後にコメントをラップします。

> [!div class="step-by-step"]
> [前へ](use-ajax-to-implement-mapping-scenarios.md)
> [次へ](nerddinner-wrap-up.md)

---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
title: 'イテレーション #2 –アプリケーションの外観を良くする (VB) |Microsoft Docs'
author: microsoft
description: このイテレーションでは、既定の ASP.NET MVC ビューマスターページとカスケードスタイルシートを変更することによって、アプリケーションの外観を改善します。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f65cb436-e493-46fd-9608-384b27385aa1
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
msc.type: authoredcontent
ms.openlocfilehash: cd392baaefcfc9eef3551bc534e0b912ccd349cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487282"
---
# <a name="iteration-2--make-the-application-look-nice-vb"></a>イテレーション #2 –アプリケーションの外観を良くする (VB)

[Microsoft](https://github.com/microsoft)

[コードのダウンロード](iteration-2-make-the-application-look-nice-vb/_static/contactmanager_2_vb1.zip)

> このイテレーションでは、既定の ASP.NET MVC ビューマスターページとカスケードスタイルシートを変更することによって、アプリケーションの外観を改善します。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Contact Management ASP.NET MVC アプリケーションの構築 (VB)

この一連のチュートリアルでは、最初から最後まで、連絡先管理アプリケーション全体を作成します。 連絡先マネージャーアプリケーションを使用すると、連絡先情報 (名前、電話番号、電子メールアドレス) をユーザーの一覧に格納することができます。

複数のイテレーションに対してアプリケーションをビルドします。 各イテレーションで、アプリケーションを段階的に改善します。 この複数のイテレーションアプローチの目的は、各変更の理由を理解できるようにすることです。

- イテレーション #1 –アプリケーションを作成します。 最初のイテレーションでは、最も簡単な方法で Contact Manager を作成します。 基本的なデータベース操作 (作成、読み取り、更新、削除) のサポートを追加します。

- イテレーション #2 –アプリケーションの外観を良くします。 このイテレーションでは、既定の ASP.NET MVC ビューマスターページとカスケードスタイルシートを変更することによって、アプリケーションの外観を改善します。

- イテレーション #3 –フォーム検証を追加します。 3番目のイテレーションでは、基本的なフォーム検証を追加します。 必要なフォームフィールドを完了しないで、フォームを送信できないようにします。 また、電子メールアドレスと電話番号も検証します。

- イテレーション #4 –アプリケーションを疎結合にします。 この4回目のイテレーションでは、複数のソフトウェア設計パターンを利用して、連絡先マネージャーアプリケーションを簡単に管理および変更できるようにします。 たとえば、リポジトリパターンと依存関係の注入パターンを使用するようにアプリケーションをリファクターします。

- イテレーション #5 –単体テストを作成します。 5番目のイテレーションでは、単体テストを追加することによって、アプリケーションの保守と変更を容易にします。 データモデルクラスをモック化し、コントローラーと検証ロジックの単体テストをビルドします。

- イテレーション #6 –テスト駆動型開発を使用します。 この6番目のイテレーションでは、最初に単体テストを記述し、単体テストに対してコードを記述することによって、アプリケーションに新しい機能を追加します。 このイテレーションでは、連絡先グループを追加します。

- イテレーション #7 – Ajax 機能を追加します。 7番目のイテレーションでは、Ajax のサポートを追加することによって、アプリケーションの応答性とパフォーマンスを向上させます。

## <a name="this-iteration"></a>このイテレーション

このイテレーションの目的は、Contact Manager アプリケーションの外観を向上させることです。 現在、連絡先マネージャーは、既定の ASP.NET MVC ビューマスターページとカスケードスタイルシートを使用します (図1を参照)。 これらの don は悪いのではありませんが、他のすべての ASP.NET MVC web サイトと同様に、連絡先マネージャーを見たくないと思います。 これらのファイルをカスタムファイルに置き換えます。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-2-make-the-application-look-nice-vb/_static/image1.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image1.png)

**図 01**: ASP.NET MVC アプリケーションの既定の外観 ([クリックすると、フルサイズの画像が表示](iteration-2-make-the-application-look-nice-vb/_static/image2.png)されます)

このイテレーションでは、アプリケーションのビジュアルデザインを向上させるための2つのアプローチについて説明します。 まず、ASP.NET MVC デザインギャラリーを利用して、無料の ASP.NET MVC デザインテンプレートをダウンロードする方法を説明します。 ASP.NET MVC デザインギャラリーを使用すると、作業を行わずに、プロフェッショナルな web アプリケーションを作成できます。

Contact Manager アプリケーションの ASP.NET MVC デザインギャラリーのテンプレートを使用しないことにしました。 私は、専門設計企業によって作成されたカスタム設計を持っていました。 このチュートリアルの2番目のパートでは、プロフェッショナル設計企業との連携によって最終的な ASP.NET MVC 設計を作成する方法について説明します。

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC デザインギャラリー

ASP.NET MVC デザインギャラリーは、Microsoft によって提供される無料のリソースです。 ASP.NET MVC ギャラリーは、次のアドレスにあります。

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC デザインギャラリーは、ASP.NET MVC プロジェクトでを使用するために特別に作成された、無料の web サイトデザインのコレクションをホストします。 設計は、コミュニティのメンバーによってアップロードされます。 ギャラリーへの訪問者は、お気に入りのデザインに投票できます (図2を参照)。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-2-make-the-application-look-nice-vb/_static/image2.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image3.png)

**図 02**: ASP.NET MVC デザインギャラリー ([クリックすると、フルサイズの画像が表示](iteration-2-make-the-application-look-nice-vb/_static/image4.png)されます)

このチュートリアルでは、ギャラリーで最も人気のある設計は、David Hauser によって10月という名前の設計になっています。 この設計は、次の手順を完了することで、ASP.NET MVC プロジェクトに使用できます。

1. **[ダウンロード]** ボタンをクリックして、10月の .zip ファイルをコンピューターにダウンロードします。
2. ダウンロードした10月の .zip ファイルを右クリックし、 **[ブロック解除]** ボタンをクリックします (図3を参照)。
3. 10月という名前のフォルダーにファイルを解凍します。
4. 10月のフォルダーに格納されている DesignTemplate フォルダーからすべてのファイルを選択し、ファイルを右クリックして、メニューオプション **[コピー]** を選択します。
5. Visual Studio のソリューションエクスプローラーウィンドウで ContactManager プロジェクトノードを右クリックし、メニューオプション **[貼り付け]** を選択します (図4を参照)。
6. Visual Studio のメニューオプション [編集]、[**検索と置換]、[クイック置換** *]、[Myprojectname]* を*Contactmanager*に置き換えます (図5を参照)。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-2-make-the-application-look-nice-vb/_static/image3.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image5.png)

**図 03**: web からダウンロードしたファイルのブロックを解除[する (クリックすると、フルサイズの画像が表示](iteration-2-make-the-application-look-nice-vb/_static/image6.png)されます)

[[新しいプロジェクト] ダイアログボックスの ![](iteration-2-make-the-application-look-nice-vb/_static/image4.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image7.png)

**図 04**: ソリューションエクスプローラー内のファイルを上書き[する (クリックすると、フルサイズの画像が表示](iteration-2-make-the-application-look-nice-vb/_static/image8.png)されます)

[[新しいプロジェクト] ダイアログボックスの ![](iteration-2-make-the-application-look-nice-vb/_static/image5.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image9.png)

**図 05**: [ProjectName] を contactmanager に置き換える ([クリックすると、フルサイズの画像が表示](iteration-2-make-the-application-look-nice-vb/_static/image10.png)される)

これらの手順を完了すると、web アプリケーションで新しいデザインが使用されます。 図6のページは、10月の設計で Contact Manager アプリケーションの外観を示しています。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-2-make-the-application-look-nice-vb/_static/image6.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image11.png)

**図 06**:10 月のテンプレートを使用した contactmanager ([クリックすると、フルサイズの画像が表示](iteration-2-make-the-application-look-nice-vb/_static/image12.png)されます)

## <a name="creating-a-custom-aspnet-mvc-design"></a>カスタム ASP.NET MVC デザインの作成

ASP.NET MVC デザインギャラリーでは、さまざまなデザインスタイルを選択できます。 ギャラリーでは、ASP.NET MVC アプリケーションの外観を簡単にカスタマイズすることができます。 もちろん、ギャラリーには完全に無料であるという大きな利点があります。

ただし、web サイトに完全に固有の設計を作成することが必要になる場合があります。 そのような場合は、web サイトデザイン会社で作業するのが理にかなっています。 Contact Manager アプリケーションの設計には、この方法を採用することにしました。

イテレーション #1 から連絡先マネージャーを圧縮し、そのプロジェクトをデザイン会社に送信しました。 これらのユーザーは Visual Studio を所有していませんでした (もったいないこと)。しかし、それには問題がありませんでした。 Microsoft Visual Web Developer を[https://www.asp.net](https://www.asp.net) web サイトから無料でダウンロードし、Visual web Developer で Contact Manager アプリケーションを開くことができました。 いくつかの日に、図7の設計が作成されています。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-2-make-the-application-look-nice-vb/_static/image7.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image13.png)

**図 07**: ASP.NET MVC Contact Manager の設計 ([クリックしてフルサイズの画像を表示する](iteration-2-make-the-application-look-nice-vb/_static/image14.png))

新しいデザインでは、新しいカスケードスタイルシートファイルと新しいビューマスターページファイルの2つのメインファイルが作成されています。 ビューマスターページには、ASP.NET MVC アプリケーションのビューのレイアウトと共有コンテンツが含まれています。 たとえば、ビューマスターページには、図7に示されているヘッダー、ナビゲーションタブ、およびフッターが含まれています。 既存のサイトを上書きしました。 Views\Shared フォルダーのマスタービューマスターページは、デザイン会社の新しいサイトのマスターファイルと共に、

設計会社は、新しいカスケードスタイルシートと一連のイメージも作成しました。 これらの新しいファイルをコンテンツフォルダーに配置し、既存のサイト .css ファイルを上書きしました。 コンテンツフォルダーには、すべての静的コンテンツを配置する必要があります。

連絡先マネージャーの新しいデザインに、連絡先の編集と削除を行うための画像が含まれていることに注意してください。 連絡先の HTML テーブル内の各連絡先の横に、編集および削除のイメージが表示されます。

もともと、これらのリンクは HTML でレンダリングされていました。Html.actionlink () ヘルパーは次のようになります。

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample1.aspx)]

Html.actionlink () メソッドは、イメージをサポートしていません (セキュリティ上の理由により、HTML はリンクテキストを HTML エンコードするメソッドです)。 したがって、Html.actionlink () への呼び出しを、次のように Url の呼び出しに置き換えます。

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample2.aspx)]

Html.actionlink () メソッドは、HTML ハイパーリンク全体を表示します。 一方、Url. Action () メソッドは、&lt;&gt; タグを含まない URL だけをレンダリングします。

さらに、新しいデザインには、選択したタブと選択されていないタブの両方が含まれることに注意してください。 たとえば、図8では、 **[新しい連絡先の作成]** タブが選択されており、 **[連絡先**] タブが選択されていません。

[[新しいプロジェクト] ダイアログボックスの ![](iteration-2-make-the-application-look-nice-vb/_static/image8.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image15.png)

**図 08**: 選択したタブと選択されていないタブ ([クリックしてフルサイズの画像を表示する](iteration-2-make-the-application-look-nice-vb/_static/image16.png))

選択したタブと選択されていないタブの両方の表示をサポートするために、MenuItemHelper という名前のカスタム HTML ヘルパーを作成しました。 このヘルパーメソッドは、現在のコントローラーとアクションが、ヘルパーに渡されたコントローラーとアクション名に対応しているかどうかに応じて、&lt;li&gt; タグ、または &lt;li class = "selected"&gt; タグのいずれかをレンダリングします。 MenuItemHelper のコードは、リスト1に含まれています。

**リスト1–公開しているサブメニュー**

[!code-vb[Main](iteration-2-make-the-application-look-nice-vb/samples/sample3.vb)]

MenuItemHelper は TagBuilder クラスを内部的に使用して、&lt;li&gt; HTML タグを構築します。 TagBuilder クラスは、新しい HTML タグを作成する必要がある場合に使用できる非常に便利なユーティリティクラスです。 これには、属性の追加、CSS クラスの追加、Id の生成、タグ s の内部 HTML の変更を行うためのメソッドが含まれています。

## <a name="summary"></a>まとめ

このイテレーションでは、ASP.NET MVC アプリケーションのビジュアルデザインを改良しました。 まず、ASP.NET MVC デザインギャラリーについて紹介しました。 ASP.NET MVC デザインギャラリーから、ASP.NET MVC アプリケーションで使用できる無料のデザインテンプレートをダウンロードする方法を学習しました。

次に、既定のカスケードスタイルシートファイルとマスタービューページファイルを変更して、カスタムデザインを作成する方法について説明しました。 新しい設計をサポートするために、Contact Manager アプリケーションに軽微な変更を加える必要がありました。 たとえば、選択したタブと選択されていないタブを表示する MenuItemHelper という名前の新しい HTML ヘルパーを追加しました。

次のイテレーションでは、検証の重要なサブジェクトに取り組みます。 アプリケーションに検証コードを追加して、ユーザーが新しい連絡先を作成できないようにします。これにより、ユーザーは、ユーザー名、姓などの必須の値を指定する必要がなくなります。

> [!div class="step-by-step"]
> [前へ](iteration-1-create-the-application-vb.md)
> [次へ](iteration-3-add-form-validation-vb.md)

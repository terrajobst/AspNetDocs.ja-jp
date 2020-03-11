---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: カスタム AJAX Control Toolkit コントロールエクステンダーを作成する (VB) |Microsoft Docs
author: microsoft
description: カスタムエクステンダーを使用すると、新しいクラスを作成しなくても、ASP.NET コントロールの機能をカスタマイズおよび拡張できます。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 0849fa6c13679e0cd01bb20a4067a097acbce298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78466864"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a>カスタム AJAX Control Toolkit コントロール エクステンダーを作成する (VB)

[Microsoft](https://github.com/microsoft)

> カスタムエクステンダーを使用すると、新しいクラスを作成しなくても、ASP.NET コントロールの機能をカスタマイズおよび拡張できます。

このチュートリアルでは、カスタム AJAX Control Toolkit コントロールエクステンダーを作成する方法について説明します。 テキストをテキストボックスに入力するときに、ボタンの状態を無効から有効に変更する、シンプルで便利な新しいエクステンダーを作成します。 このチュートリアルを読み終えると、独自の制御エクステンダーを使用して ASP.NET AJAX Toolkit を拡張できるようになります。

Visual Studio または Visual Web Developer を使用して、カスタムコントロールエクステンダーを作成できます (最新バージョンの Visual Web Developer があることを確認してください)。

## <a name="overview-of-the-disabledbutton-extender"></a>DisabledButton Extender の概要

新しいコントロールエクステンダーには、DisabledButton extender という名前が付けられています。 このエクステンダーには、次の3つのプロパティがあります。

- TargetControlID-コントロールが拡張するテキストボックス。
- TargetButtonIID-無効または有効になっているボタン。
- DisabledText-ボタンに最初に表示されるテキスト。 入力を開始すると、ボタンの [テキスト] プロパティの値が表示されます。

DisabledButton extender を TextBox コントロールと Button コントロールにフックします。 テキストを入力する前に、ボタンは無効になり、テキストボックスとボタンは次のようになります。

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png)される)

テキストの入力を開始すると、ボタンが有効になり、テキストボックスとボタンは次のようになります。

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png)される)

コントロールエクステンダーを作成するには、次の3つのファイルを作成する必要があります。

- DisabledButtonExtender-このファイルは、エクステンダーの作成を管理し、デザイン時にプロパティを設定できるサーバー側のコントロールクラスです。 また、extender で設定できるプロパティも定義されています。 これらのプロパティは、コードからアクセスでき、デザイン時に、DisableButtonBehavior .js ファイルで定義されているプロパティと一致します。
- DisabledButtonBehavior--このファイルは、すべてのクライアントスクリプトロジックを追加する場所です。
- DisabledButtonDesigner-このクラスを使用すると、デザイン時の機能が有効になります。 このクラスは、コントロールエクステンダーが Visual Studio/Visual Web Developer Designer で正しく動作するようにする場合に必要です。

したがって、制御エクステンダーは、サーバー側のコントロール、クライアント側の動作、およびサーバー側のデザイナークラスで構成されます。 これら3つのファイルをすべて作成する方法については、次のセクションで説明します。

## <a name="creating-the-custom-extender-website-and-project"></a>カスタム Extender Web サイトおよびプロジェクトの作成

最初の手順は、Visual Studio/Visual Web Developer でクラスライブラリプロジェクトと web サイトを作成することです。 クラスライブラリプロジェクトにカスタムエクステンダーを作成し、web サイトでカスタムエクステンダーをテストします。

Web サイトから始めましょう。 Web サイトを作成するには、次の手順を実行します。

1. メニューオプションファイル **[新しい Web サイト]** を選択します。
2. **ASP.NET Web サイト**テンプレートを選択します。
3. 新しい web サイトに*Website1*という名前を指定します。
4. **[OK]** をクリックします。

次に、コントロールエクステンダーのコードを含むクラスライブラリプロジェクトを作成する必要があります。

1. メニューオプション**ファイル、[追加]、[新しいプロジェクト**] を選択します。
2. **[クラスライブラリ]** テンプレートを選択します。
3. 新しいクラスライブラリに「 **Customextenders**」という名前を付けます。
4. **[OK]** をクリックします。

これらの手順を完了すると、ソリューションエクスプローラーウィンドウは図1のようになります。

[web サイトおよびクラスライブラリプロジェクトを使用したソリューションの ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)

**図 01**: web サイトおよびクラスライブラリプロジェクトを使用したソリューション ([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png)されます)

次に、必要なすべてのアセンブリ参照をクラスライブラリプロジェクトに追加する必要があります。

1. CustomExtenders プロジェクトを右クリックし、 **[参照の追加]** メニューオプションを選択します。
2. [.NET] タブを選択します。
3. 次のアセンブリへの参照を追加します。

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. System.Web.Extensions.Design.dll
4. [参照] タブを選択します。
5. AjaxControlToolkit アセンブリへの参照を追加します。 このアセンブリは、AJAX Control Toolkit をダウンロードしたフォルダーにあります。

プロジェクトを右クリックし、[プロパティ] をクリックして、[参照] タブをクリックすると、右の参照がすべて追加されていることを確認できます (図2を参照)。

[必要な参照を含む ![参照フォルダー](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)

**図 02**: 必要な参照を含むフォルダー[を参照する (クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png)される)

## <a name="creating-the-custom-control-extender"></a>カスタムコントロールエクステンダーの作成

これでクラスライブラリが用意されたので、extender コントロールの構築を開始できます。 では、カスタムエクステンダーコントロールクラスのベアボーンから始めましょう (リスト1を参照)。

**リスト 1-MyCustomExtender .vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

リスト1のコントロールエクステンダークラスに関しては、いくつかの点に注意してください。 まず、クラスが base ExtenderControlBase クラスから継承されていることに注意してください。 すべての AJAX コントロールツールキットエクステンダーコントロールは、この基本クラスから派生します。 たとえば、基本クラスには、すべてのコントロールエクステンダーの必須プロパティである TargetID プロパティが含まれています。

次に、クラスには、クライアントスクリプトに関連する次の2つの属性が含まれていることに注意してください。

- Webresource.axd-アセンブリに埋め込みリソースとしてファイルを含めます。
- ClientScriptResource-アセンブリからスクリプトリソースを取得します。

Webresource.axd 属性は、カスタムエクステンダーをコンパイルするときに、MyControlBehavior の JavaScript ファイルをアセンブリに埋め込むために使用されます。 ClientScriptResource 属性は、カスタム extender が web ページで使用されている場合に、アセンブリから MyControlBehavior .js スクリプトを取得するために使用されます。

Webresource.axd および ClientScriptResource 属性を機能させるには、JavaScript ファイルを埋め込みリソースとしてコンパイルする必要があります。 ソリューションエクスプローラーウィンドウでファイルを選択し、プロパティシートを開いて、"*埋め込みリソース*" という値を **[ビルドアクション]** プロパティに割り当てます。

コントロールエクステンダーにも TargetControlType 属性が含まれていることに注意してください。 この属性は、コントロールエクステンダーによって拡張されるコントロールの種類を指定するために使用されます。 リスト1の場合は、コントロールエクステンダーを使用してテキストボックスを拡張します。

最後に、カスタムエクステンダーに T.myproperty という名前のプロパティが含まれていることに注意してください。 プロパティは、ExtenderControlProperty 属性でマークされています。 GetPropertyValue () メソッドと SetPropertyValue () メソッドは、プロパティ値をサーバー側のコントロールエクステンダーからクライアント側の動作に渡すために使用されます。

では、DisabledButton extender のコードを実装してみましょう。 このエクステンダーのコードは、リスト2にあります。

**リスティング 2-DisabledButtonExtender**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

リスト2の DisabledButton extender には、TargetButtonID と DisabledText という2つのプロパティがあります。 TargetButtonID プロパティに適用された IDReferenceProperty では、ボタンコントロールの ID 以外のものをこのプロパティに割り当てることはできません。

Webresource.axd および ClientScriptResource 属性は、DisabledButtonBehavior という名前のファイルにあるクライアント側の動作をこのエクステンダーに関連付けます。 この JavaScript ファイルについては、次のセクションで説明します。

## <a name="creating-the-custom-extender-behavior"></a>カスタム Extender 動作の作成

コントロールエクステンダーのクライアント側コンポーネントは、動作と呼ばれます。 ボタンを無効および有効にするための実際のロジックは、DisabledButton の動作に含まれています。 この動作の JavaScript コードは、リスト3に含まれています。

**リスト 3-DisabledButton**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

リスト3の JavaScript ファイルには、DisabledButtonBehavior という名前のクライアント側クラスが含まれています。 このクラスには、サーバー側ツインと同様に、TargetButtonID と DisabledText という名前の2つのプロパティが含まれています。これは get\_TargetButtonID/set\_TargetButtonID を使用してアクセスでき、DisabledText/set\_DisabledText を取得\_ます。

Initialize () メソッドは、keyup イベントハンドラーを動作の target 要素に関連付けます。 この動作に関連付けられているテキストボックスに文字を入力するたびに、keyup ハンドラーが実行されます。 Keyup ハンドラーは、ビヘイビアーに関連付けられたテキストボックスにテキストが含まれているかどうかに応じて、ボタンを有効または無効にします。

リスト3の JavaScript ファイルを埋め込みリソースとしてコンパイルする必要があることに注意してください。 ソリューションエクスプローラーウィンドウでファイルを選択し、プロパティシートを開き、[値]*埋め込みリソース*を **[ビルドアクション]** プロパティに割り当てます (図3を参照)。 このオプションは、Visual Studio と Visual Web Developer の両方で使用できます。

[埋め込みリソースとして JavaScript ファイルを追加 ![には](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)

**図 03**: JavaScript ファイルを埋め込みリソースとして追加する ([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png)されます)

## <a name="creating-the-custom-extender-designer"></a>カスタムエクステンダーデザイナーの作成

Extender を完成させるために作成する必要がある最後のクラスが1つあります。 リスト4でデザイナークラスを作成する必要があります。 このクラスは、extender が Visual Studio/Visual Web Developer デザイナーで正しく動作するようにするために必要です。

**リスト 4-DisabledButtonDesigner**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

デザイナー属性を使用して、リスト4のデザイナーと DisabledButton extender を関連付けます。次のように、デザイナー属性を DisabledButtonExtender クラスに適用する必要があります。

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a>カスタム Extender の使用

DisabledButton control extender の作成が終了したので、ASP.NET の web サイトで使用します。 まず、カスタムエクステンダーをツールボックスに追加する必要があります。 次の手順に従います。

1. [ソリューションエクスプローラー] ウィンドウでページをダブルクリックして、ASP.NET ページを開きます。
2. ツールボックスを右クリックし、[項目の**選択**] メニューオプションを選択します。
3. [ツールボックスアイテムの選択] ダイアログで、CustomExtenders .dll アセンブリを参照します。
4. **[OK]** ボタンをクリックして、ダイアログを閉じます。

これらの手順を完了すると、DisabledButton コントロールエクステンダーがツールボックスに表示されます (図4を参照)。

[ツールボックスの ![DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)

**図 04**: ツールボックスの DisabledButton ([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png)されます)

次に、新しい ASP.NET ページを作成する必要があります。 次の手順に従います。

1. ShowDisabledButton という名前の新しい ASP.NET ページを作成します。
2. ScriptManager をページにドラッグします。
3. TextBox コントロールをページにドラッグします。
4. ボタンコントロールをページにドラッグします。
5. プロパティウィンドウで、[ボタン ID] プロパティを「 <em>Btnsave</em> 」の値に、Text プロパティを「 *save\** 」の値に変更します。

標準の ASP.NET TextBox と Button コントロールを使用してページを作成しました。

次に、DisabledButton extender を使用して TextBox コントロールを拡張する必要があります。

1. [拡張タスクの**追加**] オプションを選択して、extender ウィザードダイアログを開きます (図5を参照)。 このダイアログにはカスタム DisabledButton extender が含まれていることに注意してください。
2. DisabledButton extender を選択し、 **[OK]** をクリックします。

[Extender ウィザードダイアログ ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)

**図 05**: エクステンダーウィザードダイアログ ([クリックしてフルサイズのイメージを表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))

最後に、DisabledButton extender のプロパティを設定できます。 TextBox コントロールのプロパティを変更することで、DisabledButton extender のプロパティを変更できます。

1. デザイナーでテキストボックスを選択します。
2. プロパティウィンドウで、[Extender] ノードを展開します (図6を参照)。
3. 値*save*を DisabledText プロパティに割り当て、値*Btnsave*を TargetButtonID プロパティに割り当てます。

[extender プロパティの設定 ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)

**図 06**: extender のプロパティの設定 ([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png)される)

F5 キーを押してページを実行すると、ボタンコントロールは最初は無効になります。 テキストボックスへの入力を開始するとすぐに、ボタンコントロールが有効になります (図7を参照)。

[DisabledButton extender の動作の ![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)

**図 07**: DisabledButton extender の動作 ([クリックすると、フルサイズの画像が表示](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png)されます)

## <a name="summary"></a>まとめ

このチュートリアルの目的は、カスタム extender コントロールを使用して AJAX Control Toolkit を拡張する方法を説明することでした。 このチュートリアルでは、単純な DisabledButton 制御エクステンダーを作成しました。 このエクステンダーは、DisabledButtonExtender クラス、DisabledButtonBehavior JavaScript の動作、および DisabledButtonDesigner クラスを作成することによって実装されています。 カスタムコントロールエクステンダーを作成するたびに、同様の一連の手順に従います。

> [!div class="step-by-step"]
> [[戻る]](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)

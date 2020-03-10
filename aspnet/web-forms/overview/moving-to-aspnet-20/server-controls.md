---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: サーバーコントロール |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 では、さまざまな方法でサーバーコントロールを拡張します。 このモジュールでは、ASP.NET 2.0 と Visual Studio 200 のようなアーキテクチャの変更について説明します。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: c02a633013f061c09141d4f98871848c011a799e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521092"
---
# <a name="server-controls"></a>サーバー コントロール

[Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 では、さまざまな方法でサーバーコントロールを拡張します。 このモジュールでは、ASP.NET 2.0 と Visual Studio 2005 がサーバーコントロールを扱う方法に対するアーキテクチャの変更について説明します。

ASP.NET 2.0 では、さまざまな方法でサーバーコントロールを拡張します。 このモジュールでは、ASP.NET 2.0 と Visual Studio 2005 がサーバーコントロールを扱う方法に対するアーキテクチャの変更について説明します。

## <a name="view-state"></a>状態の表示

ASP.NET 2.0 でのビューステートの主な変更は、サイズの大幅な削減です。 カレンダーコントロールのみを含むページについて考えてみましょう。 ASP.NET 1.1 のビューステートを次に示します。

[!code-css[Main](server-controls/samples/sample1.css)]

ここで、ASP.NET 2.0 の同一ページのビューステートを示します。

[!code-css[Main](server-controls/samples/sample2.css)]

これは非常に重要な変更であり、ビューステートがネットワーク経由でやり取りされることを考慮して、この変更により、開発者はパフォーマンスを大幅に向上させることができます。 ビューステートのサイズを小さくすることは、主にそれを内部で処理する方法によるものです。 ビューステートは Base64 でエンコードされた文字列であることに注意してください。 ASP.NET 2.0 でのビューステートの変更について理解を深めるために、上記の例のデコードされた値を確認してみましょう。

デコードされた1.1 ビューステートは次のとおりです。

[!code-css[Main](server-controls/samples/sample3.css)]

これは、不自然なように見えますが、ここにはパターンがあります。 ASP.NET 1.x では、1つの文字を使用して、&lt;&gt; 文字を使用してデータ型と区切り値を識別しました。 上のビューステートサンプルの "t" は、3つの型を表します。 3つの組には ArrayLists のペアが含まれています ("l" は ArrayList を表します)。これらの ArrayLists の1つには、値1を持つ Int32 ("i") が含まれ、もう一方には別の3つの値が含まれています。 2つの組には、ArrayLists などのペアが含まれています。覚えておくべき重要な点は、ペアを含む Triplets を使用し、データ型を文字で識別し、&lt; と &gt; 文字を区切り記号として使用することです。

ASP.NET 2.0 では、デコードされたビューステートは少し異なります。

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

デコードされたビューステートの外観に大きな変化があることに注意してください。 この変更には、いくつかのアーキテクチャ基盤があります。 ASP.NET 1.x のビューステートでは、LosFormatter を使用してデータをシリアル化していました。 2\.0 では、新しい ObjectStateFormatter クラスを使用します。 このクラスは、ビューステートとコントロール状態のシリアル化と逆シリアル化を支援するように特別に設計されています。 (コントロールの状態については、次のセクションで説明します)。シリアル化と逆シリアル化を行う方法を変更すると、多くの利点が得られます。 最も大きな効果の1つは、TextWriter を使用する LosFormatter とは異なり、ObjectStateFormatter は BinaryWriter を使用するという事実です。 これにより、ASP.NET 2.0 では、ビューステートを文字列ではなく一連のバイトに格納できます。 たとえば、整数を取得します。 ASP.NET 1.1 では、整数のビューステートの4バイトが必要でした。 ASP.NET 2.0 では、その同じ整数に必要なのは1バイトだけです。 格納されるビューステートの量を減らすために、その他の機能強化が行われました。 たとえば、DateTime 値は、文字列ではなく TickCount を使用して格納されるようになりました。

すべてが十分ではなかったとしても、1. x のビューステートの最大のコンシューマーの1つが DataGrid および同様のコントロールであるという事実に注目しました。 ビューステートが考慮される DataGrid などのコントロールの大きな欠点は、多くの場合、大量の繰り返し情報が含まれていることです。 ASP.NET 1.x では、繰り返された情報が繰り返し格納されるだけで、ビューステートが肥大化します。 ASP.NET 2.0 では、新しい IndexedString クラスを使用して、そのようなデータを格納します。 文字列が繰り返される場合は、IndexedString のトークンと、IndexedString オブジェクトの実行中のテーブル内のインデックスを格納するだけです。

## <a name="control-state"></a>コントロールの状態

ビューステートを使用した開発者の主な gripes の1つは、HTTP ペイロードに追加したサイズでした。 既に説明したように、ビューステートの最大のコンシューマーの1つは、DataGrid コントロールです。 DataGrid によって生成される大量のビューステートを回避するには、多くの開発者がそのコントロールのビューステートを無効にするだけです。 残念ながら、そのソリューションは常に適切なソリューションではありませんでした。 ASP.NET 1.x のビューステートには、コントロールの正しい機能に必要なデータのみが含まれています。 また、コントロールの UI の状態に関する情報も含まれます。 これは、DataGrid での改ページ位置の自動修正を許可する場合、ビューステートに含まれるすべての UI 情報が不要な場合でも、ビューステートを有効にする必要があることを意味します。 これは、まったくまたはまったくないシナリオです。

ASP.NET 2.0 では、コントロールの状態によって、コントロールの状態の導入によって問題が適切に解決されます。 コントロールの状態には、コントロールの適切な機能に必要なデータが含まれています。 ビューステートとは異なり、コントロールの状態を無効にすることはできません。 したがって、コントロールの状態で格納されるデータは慎重に制御することが重要です。

> [!NOTE]
> コントロールの状態は、ビューステートと共に \_\_VIEWSTATE 隠しフォームフィールドに表示されます。

このビデオは、ビューステートとコントロールの状態のチュートリアルです。

![](server-controls/_static/image1.png)

[全画面表示のビデオを開く](server-controls/_static/state1.wmv)

サーバーコントロールがコントロールの状態を読み取り、書き込みを行うには、3つの手順を実行する必要があります。

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>手順 1: RegisterRequiresControlState メソッドを呼び出す

RegisterRequiresControlState メソッドは、コントロールがコントロールの状態を保持する必要があることを ASP.NET に通知します。 これは、登録されるコントロールである型コントロールの1つの引数を受け取ります。

登録は要求に対して保持されないことに注意してください。 したがって、コントロールの状態を保持する必要がある場合は、すべての要求に対してこのメソッドを呼び出す必要があります。 メソッドを OnInit で呼び出すことをお勧めします。

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>手順 2: SaveControlState をオーバーライドする

SaveControlState メソッドは、最後のポストバック以降にコントロールのコントロールの状態の変更を保存します。 このメソッドは、コントロールの状態を表すオブジェクトを返します。

## <a name="step-3-override-loadcontrolstate"></a>手順 3: LoadControlState をオーバーライドする

LoadControlState メソッドは、保存された状態をコントロールに読み込みます。 メソッドは、コントロールの保存された状態を保持する Object 型の引数を1つ受け取ります。

## <a name="full-xhtml-compliance"></a>完全な XHTML 準拠

Web 開発者は、Web アプリケーションの標準の重要性を把握しています。 標準ベースの開発環境を維持するために、ASP.NET 2.0 は完全に XHTML に準拠しています。 そのため、HTML 4.0 以上をサポートするブラウザーでは、すべてのタグが XHTML 標準に従ってレンダリングされます。

ASP.NET 1.1 の DOCTYPE 定義は次のようになりました。

[!code-html[Main](server-controls/samples/sample6.html)]

ASP.NET 2.0 では、既定の DOCTYPE 定義は次のようになります。

[!code-html[Main](server-controls/samples/sample7.html)]

このオプションを選択した場合は、構成ファイルの xhtmlConformance ノードを使用して、既定の XHTML 準拠を変更できます。 たとえば、web.config ファイルの次のノードは、XHTML 準拠を XHTML 1.0 Strict に変更します。

[!code-xml[Main](server-controls/samples/sample8.xml)]

を選択した場合は、次のように ASP.NET 1.x で使用される従来の構成を使用するように ASP.NET を構成することもできます。

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>アダプターを使用したアダプティブレンダリング

ASP.NET 1.x では、構成ファイルに、HttpBrowserCapabilities オブジェクトを設定する &lt;browserCaps&gt; セクションが含まれていました。 このオブジェクトを使用すると、開発者は特定の要求を行っているデバイスを特定し、適切にコードを表示できます。 ASP.NET 2.0 では、モデルが改善され、新しい ControlAdapter クラスが使用されるようになりました。 ControlAdapter クラスは、コントロールのライフサイクル内のイベントをオーバーライドし、ユーザーエージェントの機能に基づいてコントロールのレンダリングを制御します。 特定のユーザーエージェントの機能は、ブラウザー定義ファイル (拡張子が c:\windows\microsoft.net\framework\v2.0. のファイル) によって定義されます。\*\*\*\* フォルダーにあります。

> [!NOTE]
> ControlAdapter クラスは抽象クラスです。

1\. x の &lt;browserCaps&gt; セクションと同様に、ブラウザー定義ファイルでは、要求元のブラウザーを識別するために、正規表現を使用してユーザーエージェント文字列を解析します。 これにより、そのユーザーエージェントの特定の機能が定義されます。 ControlAdapter は、Render メソッドを使用してコントロールをレンダリングします。 したがって、Render メソッドをオーバーライドする場合は、基本クラスで Render を呼び出さないでください。 このようにすると、レンダリングが2回発生する可能性があります。1回はアダプターで、もう1つはコントロール自体に1回です。

## <a name="developing-a-custom-adapter"></a>カスタムアダプターの開発

ControlAdapter から継承することで、独自のカスタムアダプターを開発できます。 また、ページにアダプターが必要な場合は、抽象クラス PageAdapter を継承することもできます。 カスタムアダプターへのコントロールのマッピングは、ブラウザー定義ファイルの &lt;controlAdapters&gt; 要素を介して行われます。 たとえば、ブラウザー定義ファイルの次の XML は、メニューコントロールを MenuAdapter クラスにマップします。

[!code-html[Main](server-controls/samples/sample10.html)]

このモデルを使用すると、コントロール開発者は特定のデバイスやブラウザーを対象にすることが非常に簡単になります。 また、開発者は、すべてのデバイスでのページの表示方法を完全に制御できます。

## <a name="per-device-rendering"></a>デバイスごとのレンダリング

ASP.NET 2.0 のサーバーコントロールのプロパティは、ブラウザー固有のプレフィックスを使用して、デバイスごとに指定できます。 たとえば、次のコードでは、ページを参照するために使用されているデバイスに応じてラベルのテキストが変更されます。

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

このラベルを含むページが Internet Explorer から参照されている場合、ラベルには "Internet Explorer から参照しています" というテキストが表示されます。 ページが Firefox から参照されると、ラベルに "Firefox から参照しています" というテキストが表示されます。 他のデバイスからページが参照されると、"不明なデバイスから参照しています。" と表示されます。 任意のプロパティは、この特殊な構文を使用して指定できます。

## <a name="setting-focus"></a>設定 (フォーカスを)

ASP.NET 1.x の開発者は、特定のコントロールに最初のフォーカスを設定する方法についてよく寄せられるようになりました。 たとえば、ログインページでは、ページが最初に読み込まれるときに [ユーザー ID] ボックスにフォーカスを設定すると便利です。 ASP.NET 1.x で、これを行うには、いくつかのクライアント側スクリプトを記述する必要がありました。 このようなスクリプトは単純なタスクでも、SetFocus メソッドに感謝する ASP.NET 2.0 では不要になりました。 SetFocus メソッドは、フォーカスを受け取る必要があるコントロールを示す1つの引数を受け取ります。 この引数には、コントロールのクライアント ID を文字列として指定するか、コントロールオブジェクトとしてサーバーコントロールの名前を使用できます。 たとえば、最初のフォーカスを、ページが最初に読み込まれるときに txtUserID という名前のテキストボックスコントロールに設定するには、ページ\_の読み込みに次のコードを追加します。

[!code-csharp[Main](server-controls/samples/sample12.cs)]

--または

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0 では、Webresource.axd ハンドラー (前に説明しました) を使用して、フォーカスを設定するクライアント側の関数をレンダリングします。 クライアント側関数の名前は、次に示すように、Web フォーム\_自動フォーカスされます。

[!code-html[Main](server-controls/samples/sample14.html)]

また、コントロールにフォーカスメソッドを使用して、そのコントロールに最初のフォーカスを設定することもできます。 フォーカスメソッドは、コントロールクラスから派生し、すべての ASP.NET 2.0 コントロールで使用できます。 検証エラーが発生したときに、特定のコントロールにフォーカスを設定することもできます。 これについては、後のモジュールで説明します。

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2.0 の新しいサーバーコントロール

ASP.NET 2.0 の新しいサーバーコントロールを次に示します。 これらのいくつかについては、後のモジュールで詳しく説明します。

## <a name="imagemap-control"></a>ImageMap コントロール

ImageMap コントロールを使用すると、ポストバックを開始したり、URL に移動したりできるように、イメージにホットスポットを追加できます。 3種類のホットスポットを利用できます。CircleHotSpot、RectangleHotSpot、および PolygonHotSpot。 ホットスポットは、Visual Studio のコレクションエディター、またはコードでプログラムによって追加されます。 イメージ上にホットスポットを描画するために使用できるユーザーインターフェイスはありません。 ホットスポットの座標とサイズまたは半径は、宣言によって指定する必要があります。 デザイナーには、ホットスポットの視覚的な表現もありません。 ホットスポットが URL に移動するように構成されている場合は、ホットスポットの NavigateUrl プロパティを使用して URL が指定されます。 ポストバックホットスポットの場合、PostBackValue プロパティを使用すると、サーバー側のコードで取得できる文字列をポストバックに渡すことができます。

![Visual Studio での HotSpot コレクションエディター](server-controls/_static/image1.jpg)

**図 1**: Visual Studio での HotSpot コレクションエディター

## <a name="bulletedlist-control"></a>BulletedList コントロール

BulletedList コントロールは、データを簡単にバインドできる箇条書きリストです。 リストは、BulletStyle プロパティを使用して順序付け (番号付き) することも、順序を指定しないこともできます。 リスト内の各項目は、ListItem オブジェクトによって表されます。

![Visual Studio での BulletedList コントロール](server-controls/_static/image1.gif)

**図 2**: Visual Studio での BulletedList コントロール

## <a name="hiddenfield-control"></a>HiddenField コントロール

HiddenField コントロールは、非表示のフォームフィールドをページに追加します。このフィールドの値は、サーバー側のコードで使用できます。 通常、非表示のフォームフィールドの値は、ポストバック間で変更されないようにする必要があります。 ただし、悪意のあるユーザーがポストバック前に値を変更する可能性があります。 これが発生した場合、HiddenField コントロールは ValueChanged イベントを発生させます。 HiddenField コントロールに機密情報があり、変更されていないことを確認する必要がある場合は、コード内で ValueChanged イベントを処理する必要があります。

## <a name="fileupload-control"></a>FileUpload コントロール

ASP.NET 2.0 の FileUpload コントロールを使用すると、ASP.NET ページを介して Web サーバーにファイルをアップロードできます。 このコントロールは、いくつかの例外を除き、ASP.NET 1.x HtmlInputFile クラスによく似ています。 ASP.NET 1.x では、適切なファイルがあるかどうかを判断するために、PostedFile プロパティが null かどうかをチェックすることをお勧めしました。 ASP.NET 2.0 の FileUpload コントロールには、同じ目的で使用できる新しい HasFile プロパティが追加されています。これはもう少し効率的です。

PostedFile プロパティは、HttpPostedFile オブジェクトへのアクセスに使用できますが、HttpPostedFile の一部の機能は、本質的に FileUpload コントロールで使用できるようになりました。 たとえば、アップロードされたファイルを ASP.NET 1.x に保存するには、HttpPostedFile オブジェクトで SaveAs メソッドを呼び出します。 ASP.NET 2.0 の FileUpload コントロールを使用して、FileUpload コントロール自体で SaveAs メソッドを呼び出します。

2\.0 の動作におけるもう1つの重要な変更 (おそらく、最も重要な変更) は、アップロードされたファイル全体をメモリに読み込みてから保存する必要がなくなったことです。 1\.x では、アップロードされたすべてのファイルがディスクに書き込まれる前にすべてのメモリに保存されます。 このアーキテクチャでは、大きなファイルをアップロードできません。

ASP.NET 2.0 では、httpRuntime 要素の Requestlength Diskthreshold 属性を使用して、ディスクに書き込まれる前にメモリ内のバッファーに保持するキロバイト数を構成できます。

**重要**: MSDN ドキュメント (および他のドキュメント) では、この値が (kb ではなく) バイトで、既定値が256であることを指定しています。 値は実際にはキロバイト単位で指定され、既定値は80です。 既定値の80K を指定することで、バッファーが大きなオブジェクトヒープで終了しないようにします。

## <a name="wizard-control"></a>ウィザードコントロール

パネルを使用して一連の "ページ" で情報を収集したり、ページからページに移動したりすることに苦労している ASP.NET 開発者には、非常に一般的です。 多くの場合、この作業は面倒な作業であり、時間がかかります。 新しいウィザードコントロールは、ユーザーが使い慣れたウィザードインターフェイスで線形および非線形のステップを許可することで、問題を解決します。 ウィザードコントロールは、一連の手順で入力フォームを表示します。 各ステップは、コントロールの StepType プロパティによって指定された特定の種類です。 使用可能な手順の種類は次のとおりです。

| **ステップの種類** | **説明** |
| --- | --- |
| Auto | ステップ階層内の位置に基づいて、ステップの種類が自動的に決定されます。 |
| [開始] | 最初のステップ。多くの場合、導入ステートメントを提示するために使用されます。 |
| 手順 | 通常の手順です。 |
| [完了] | 最後の手順。通常は、ウィザードを終了するボタンを表示するために使用されます。 |
| 完了 | 成功したか失敗したかを伝えるメッセージを表示します。 |

> [!NOTE]
> ウィザードコントロールは、ASP.NET コントロールの状態を使用して状態を追跡します。 したがって、EnableViewState プロパティは、も不利を指定せずに false に設定できます。

このビデオは、ウィザードコントロールのチュートリアルです。

![](server-controls/_static/image2.png)

[全画面表示のビデオを開く](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>ローカライズコントロール

ローカライズコントロールは、リテラルコントロールに似ています。 ただし、Localize コントロールには、追加されたマークアップの表示方法を制御する**Mode**プロパティがあります。 Mode プロパティは、次の値をサポートします。

| **モード** | **説明** |
| --- | --- |
| 変換 | マークアップは、要求を行っているブラウザーのプロトコルに従って変換されます。 |
| PassThrough | マークアップはそのようにレンダリングされます。 |
| エンコード | コントロールに追加されたマークアップは、HtmlEncode を使用してエンコードされます。 |

## <a name="multiview-and-view-controls"></a>MultiView およびビューコントロール

MultiView コントロールは、ビューコントロールのコンテナーとして機能し、ビューコントロールは他のコントロールのコンテナーとして機能します (パネルコントロールに似ています)。 MultiView コントロールの各ビューは、単一のビューコントロールによって表されます。 MultiView の最初のビューコントロールはビュー0、2番目はビュー1などです。MultiView コントロールの ActiveViewIndex を指定することで、ビューを切り替えることができます。

## <a name="substitution-control"></a>Substitution コントロール

Substitution コントロールは、ASP.NET キャッシュと組み合わせて使用されます。 キャッシュを利用する場合に、各要求で更新する必要があるページの部分がある場合 (つまり、キャッシュから除外されているページの一部)、代替コンポーネントは優れたソリューションを提供します。 コントロールは実際に出力をレンダリングしません。 代わりに、サーバー側コードのメソッドにバインドされます。 ページが要求されると、メソッドが呼び出され、返されたマークアップが代替コントロールの代わりに表示されます。

Substitution コントロールがバインドされているメソッドは、 **MethodName**プロパティを使用して指定されます。 このメソッドは、次の条件を満たしている必要があります。

- Static (VB では shared) メソッドである必要があります。
- このメソッドは、HttpContext 型の1つのパラメーターを受け入れます。
- このメソッドは、ページ上のコントロールを置き換える必要があるマークアップを表す文字列を返します。

Substitution コントロールには、ページ上の他のコントロールを変更する機能はありませんが、パラメーターを使用して現在の HttpContext にアクセスできます。

## <a name="gridview-control"></a>GridView コントロール

GridView コントロールは、DataGrid コントロールの代わりになります。 このコントロールについては、後のモジュールで詳しく説明します。

## <a name="detailsview-control"></a>DetailsView コントロール

DetailsView コントロールを使用すると、データソースから1つのレコードを表示し、それを編集または削除できます。 詳細については、後のモジュールで詳しく説明します。

## <a name="formview-control"></a>FormView コントロール

FormView コントロールは、構成可能なインターフェイス内のデータソースから1つのレコードを表示するために使用されます。 詳細については、後のモジュールで詳しく説明します。

## <a name="accessdatasource-control"></a>AccessDataSource コントロール

AccessDataSource コントロールは、Access データベースのデータバインドに使用されます。 詳細については、後のモジュールで詳しく説明します。

## <a name="objectdatasource-control"></a>ObjectDataSource コントロール

ObjectDataSource コントロールは、3層アーキテクチャをサポートするために使用されます。これにより、コントロールがデータソースに直接バインドされている2層モデルではなく、中間層ビジネスオブジェクトにコントロールをデータバインドできます。 詳細については、後のモジュールで説明します。

## <a name="xmldatasource-control"></a>XmlDataSource コントロール

XmlDataSource コントロールは、XML データソースにデータをバインドするために使用されます。 詳細については、後のモジュールで詳しく説明します。

## <a name="sitemapdatasource-control"></a>SiteMapDataSource コントロール

SiteMapDataSource コントロールは、サイトマップに基づいてサイトナビゲーションコントロールのデータバインディングを提供します。 詳細については、後のモジュールで説明します。

## <a name="sitemappath-control"></a>SiteMapPath コントロール

SiteMapPath コントロールは、一般的に階層リンクと呼ばれる一連のナビゲーションリンクを表示します。 詳細については、後のモジュールで詳しく説明します。

## <a name="menu-control"></a>メニュー コントロール

メニューコントロールには、DHTML を使用した動的メニューが表示されます。 詳細については、後のモジュールで詳しく説明します。

## <a name="treeview-control"></a>TreeView コントロール

TreeView コントロールは、データの階層ツリービューを表示するために使用されます。 詳細については、後のモジュールで詳しく説明します。

## <a name="login-control"></a>ログイン制御

ログインコントロールは、Web サイトにログインするためのメカニズムを提供します。 詳細については、後のモジュールで詳しく説明します。

## <a name="loginview-control"></a>LoginView コントロール

LoginView コントロールを使用すると、ユーザーのログインの状態に基づいてさまざまなテンプレートを表示できます。 詳細については、後のモジュールで詳しく説明します。

## <a name="passwordrecovery-control"></a>PasswordRecovery コントロール

PasswordRecovery コントロールは、ASP.NET アプリケーションのユーザーが忘れたパスワードを取得するために使用されます。 詳細については、後のモジュールで詳しく説明します。

## <a name="loginstatus"></a>LoginStatus

LoginStatus コントロールには、ユーザーのログイン状態が表示されます。 詳細については、後のモジュールで詳しく説明します。

## <a name="loginname"></a>LoginName

ASP.NET アプリケーションにログインした後、[ログイン] コントロールにユーザーのユーザー名が表示されます。 詳細については、後のモジュールで詳しく説明します。

## <a name="createuserwizard"></a>CreateUserWizard

CreateUserWizard は構成可能なウィザードであり、ASP.NET アプリケーションで使用する ASP.NET メンバーシップアカウントをユーザーが作成することができます。 詳細については、後のモジュールで詳しく説明します。

## <a name="changepassword"></a>ChangePassword

ChangePassword コントロールを使用すると、ユーザーは ASP.NET アプリケーションのパスワードを変更できます。 詳細については、後のモジュールで詳しく説明します。

## <a name="various-webparts"></a>さまざまな Web パーツ

ASP.NET 2.0 には、さまざまな Web パーツが付属しています。 これらの詳細については、後のモジュールで詳しく説明します。

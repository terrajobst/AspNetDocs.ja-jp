---
uid: mvc/overview/advanced/custom-mvc-templates
title: カスタム MVC テンプレート |Microsoft Docs
author: joeloff
description: VSIX 拡張機能としてテンプレートを作成します。
ms.author: riande
ms.date: 12/10/2012
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 0603bc24e070e223551813f66a75889a2e46fd35
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499600"
---
# <a name="custom-mvc-template"></a>カスタム MVC テンプレート

[jacques victor 氏](https://github.com/joeloff)

MVC 3 Tools Update for Visual Studio 2010 のリリースでは、MVC プロジェクト用に個別のプロジェクトウィザードが導入されました。 この変更は、2つの要素によって行われました。 まず、MVC 3 の新しいテンプレートの導入と、Visual Studio の [新しいプロジェクト] ダイアログボックスの overcrowding のための Razor リーダーなどの追加のビューエンジンのサポートを紹介します。 2つ目は、顧客が拡張ポイントを要求していて、MVC プロジェクトの新規作成ウィザードでこれらの要求に応答する機会があることです。

カスタムテンプレートの追加は、困難なプロセスで、レジストリを使用して MVC プロジェクトウィザードで新しいテンプレートを表示することに依存していました。 新しいテンプレートの作成者は、インストール時に必要なレジストリエントリが確実に作成されるように、MSI 内にラップする必要がありました。 別の方法としては、テンプレートを含む ZIP ファイルを使用可能にし、エンドユーザーが必要なレジストリエントリを手動で作成するようにします。

前述のいずれの方法も理想的ではないため、Visual Studio 2012 の MVC 4 以降でカスタム MVC テンプレートを簡単に作成、配布、およびインストールできるように、 [VSIX](https://msdn.microsoft.com/library/ff363239.aspx)拡張機能に用意されている既存のインフラストラクチャの一部を利用することにしました。 この方法で提供される利点の一部を次に示します。

- VSIX 拡張機能には、さまざまな言語 (C#および Visual Basic) と複数のビューエンジン (ASPX および Razor) をサポートする複数のテンプレートを含めることができます。
- VSIX 拡張機能は、Express Sku を含む Visual Studio の複数の Sku をターゲットにすることができます。
- [Visual Studio ギャラリー](https://visualstudiogallery.msdn.microsoft.com/)では、拡張機能を広範囲の対象ユーザーに配布することができます。
- VSIX 拡張機能をアップグレードすると、カスタムテンプレートの修正や更新を簡単に作成できるようになります。

## <a name="prerequisites"></a>前提条件

- ユーザーは、.vstemplate ファイルに必要なマークアップなどのプロジェクトテンプレートの作成について理解している必要があります。
- ユーザーは、Visual Studio Professional 以降がインストールされている必要があります。 Express Sku では、VSIX プロジェクトの作成はサポートされていません。
- [Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668)がインストールされました。

## <a name="example"></a>例

最初の手順では、 C#または Visual Basic を使用して、新しい VSIX プロジェクトを作成します。 **[ファイル > 新しいプロジェクト]** を選択し、左側のウィンドウで **[拡張機能]** をクリックして、 **VSIX プロジェクト**を選択します。

![[新しいプロジェクト]](custom-mvc-templates/_static/image1.jpg)

プロジェクトが作成されると、VSIX デザイナーが開きます。

![プロジェクトデザイナーのメタデータ](custom-mvc-templates/_static/image2.jpg)

デザイナーを使用すると、拡張機能をインストールするときにユーザーに表示される拡張機能の全般的なプロパティを編集したり、Visual Studio でインストールされている拡張機能を参照したりすることができます (**ツール > の拡張機能と更新プログラム**)。 一般情報を完了したら、[インストールの**対象] タブ**をクリックします。

![プロジェクトデザイナーのインストールターゲット](custom-mvc-templates/_static/image3.jpg)

このタブは、拡張機能でサポートされている Visual Studio の Sku とバージョンを指定するために使用されます。 **すべてのユーザーが**vsix のコンピューター単位のインストールを有効にするには、[この vsix をインストールする] チェックボックスをオンにします。 右側にある **[新規]** ボタンをクリックして、Web Developer Express (vwd) などのその他の sku を追加します。

![新しいインストール先の追加](custom-mvc-templates/_static/image4.jpg)

すべての Professional およびそれ以降の Sku (Professional、Premium、および Ultimate) をサポートする場合は、ファミリ**Microsoft.VisualStudio.Pro**の最小 sku のみを選択する必要があります。 インストールターゲットを完了したら、すべての変更を保存してください。

![プロジェクトデザイナーのインストールターゲット](custom-mvc-templates/_static/image5.jpg)

**[アセット]** タブは、すべてのコンテンツファイルを VSIX に追加するために使用されます。 MVC にはカスタムメタデータが必要であるため、 **[アセット]** タブを使用してコンテンツを追加するのではなく、VSIX マニフェストファイルの未加工の XML を編集します。 まず、VSIX プロジェクトにテンプレートの内容を追加します。 フォルダーの構造とコンテンツは、プロジェクトのレイアウトをミラー化することが重要です。 次の例には、Basic MVC プロジェクトテンプレートから派生した4つのプロジェクトテンプレートが含まれています。 プロジェクトテンプレートを構成するすべてのファイル (ProjectTemplates フォルダーの下にあるすべてのファイル) が VSIX プロジェクトファイルの**コンテンツ**itemgroup に追加されていること、および次の例に示すように、各項目に**Copytooutputdirectory**と**IncludeInVsix**メタデータセットが含まれていることを確認します。

&lt;コンテンツインクルード =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;

&lt;CopyToOutputDirectory&gt;常に&lt;/CopyToOutputDirectory&gt;

&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;

&lt;/コンテンツ&gt;

そうでない場合は、VSIX のビルド時に IDE によってテンプレートの内容がコンパイルされ、エラーが発生する可能性があります。 多くの場合、テンプレート内のコードファイルには、プロジェクトテンプレートがインスタンス化されるときに Visual Studio によって使用される特殊な[テンプレートパラメーター](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx)が含まれているため、IDE でコンパイルすることはできません。

![ソリューション エクスプローラー](custom-mvc-templates/_static/image6.jpg)

VSIX デザイナーを閉じ、**ソリューションエクスプローラー**で**ソースの拡張子のマニフェスト**ファイルを右クリックし、 **[ファイルを開くアプリケーション]** の選択 をクリックして **[XML (テキスト) エディター]** オプションを選択します。

![ダイアログで開く](custom-mvc-templates/_static/image7.jpg)

**&lt;Assets&gt;** 要素を作成し、VSIX に含める必要がある各ファイルに **&lt;Asset&gt;** 要素を追加します。 各 **&lt;Asset&gt;** 要素の**Type**属性は、 **VisualStudio**に設定する必要があります。 これは、MVC プロジェクトウィザードのみで認識されるカスタムの名前空間です。 マニフェストファイルの構造とレイアウトの詳細については、VSIX 2.0 スキーマのドキュメントを参照してください。

VSIX にファイルを追加するだけでは、テンプレートを MVC ウィザードに登録するのに十分ではありません。 MVC ウィザードでは、テンプレート名、説明、サポートされているビューエンジン、プログラミング言語などの情報を提供する必要があります。 この情報は、各 **.vstemplate**ファイルの **&lt;Asset&gt;** 要素に関連付けられているカスタム属性に格納されます。

&lt;Asset d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;

「=&quot;VisualStudio&quot;」と入力します。

&quot;ファイル&quot;

Path =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;

ProjectType =&quot;MVC&quot;

言語 =&quot;C#&quot;

ViewEngine =&quot;Aspx&quot;

TemplateId =&quot;MyMvcApplication&quot;

Title = カスタム基本的な Web アプリケーション&quot; の&quot;

Description = 基本的な MVC web アプリケーション (Razor) から派生したカスタムテンプレートを&quot;&quot;

バージョン =&quot;4.0&quot;/&gt;

次に示すのは、存在する必要があるカスタム属性の説明です。

- **ProjectType**は MVC に設定する必要があります。
- **Language**は、テンプレートでサポートされている開発言語を指定します。 有効な値はC# 、または VB です。
- **Viewengine**は、テンプレートでサポートされているビューエンジン (Aspx、Razor など) を指定します。 このフィールドには、カスタム値を指定できます。
- **TemplateId**は、テンプレートをグループ化するために使用されます。 値が既存のテンプレート ID と一致する場合は、MVC ウィザードで以前に登録されたテンプレートより優先されます。
- **[タイトル]** は、各プロジェクトテンプレートの下にある MVC ウィザードに表示される短い説明を指定します。
- **説明**テンプレートの詳細な説明を指定します。

すべてのファイルをマニフェストに追加して保存すると、デザイナーの **[アセット]** タブにはすべてのファイルが表示されますが、 **.vstemplate**ファイルの **&lt;Asset&gt;** 要素に追加したカスタム属性は表示されません。

![プロジェクトデザイナーのアセット](custom-mvc-templates/_static/image8.jpg)

これで、VSIX プロジェクトをコンパイルしてインストールすることができます。

VSIX 拡張機能をテストするコンピューターで Visual Studio のすべてのインスタンスが閉じられていることを確認します。 Visual Studio は起動時に新しい拡張機能をスキャンします。そのため、VSIX のインストール中に IDE が開いている場合は、Visual Studio を再起動する必要があります。 [エクスプローラー] で、VSIX ファイルをダブルクリックして、 **Vsix インストーラー**を起動します。次に、 **[インストール]** をクリックし、Visual Studio を起動します。

![VSIX インストーラー](custom-mvc-templates/_static/image9.jpg)

メニューから [ **> ツール] [拡張機能と更新プログラム**] を選択して、拡張機能がインストールされたことを確認します。 拡張機能のインストール中に VSIX インストーラーによってエラーが報告された場合は、VSIX インストーラーログで詳細を確認できます。 通常、ログは、拡張機能をインストールしたユーザーの **% temp%** フォルダー (たとえば、 **C:\Users\Bob\AppData\Local\Temp**) に作成されます。

![拡張機能と更新プログラム](custom-mvc-templates/_static/image10.jpg)

ウィンドウを閉じた後、MVC 4 プロジェクトを作成して、新しいテンプレートが MVC ウィザードに表示されているかどうかを確認できます。

![新しい ASP.NET MVC 4 プロジェクト](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a>制限事項

1. MVC ウィザードでは、ローカライズされたカスタムテンプレートはサポートされていません。
2. カスタムテンプレートの特定に失敗した場合、ウィザードはエラーを報告しません。 必要なカスタム属性のいずれかが存在しない場合、テンプレートは単純にウィザードから除外されます。

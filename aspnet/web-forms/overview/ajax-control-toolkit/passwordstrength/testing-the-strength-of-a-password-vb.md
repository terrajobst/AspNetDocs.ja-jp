---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: パスワードの強度をテストする (VB) |Microsoft Docs
author: wenz
description: パスワードはほとんどすべての場所で必要になるため、レイジーユーザーは簡単に解読できる単純なパスワードを選択する傾向があります。 ASP の PasswordStrength 制御。N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: b614e1788eeafc175dd792ec6d3e4619f9ea2b7a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508972"
---
# <a name="testing-the-strength-of-a-password-vb"></a>パスワードの強度をテストする (VB)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)

> パスワードはほとんどすべての場所で必要になるため、レイジーユーザーは簡単に解読できる単純なパスワードを選択する傾向があります。 ASP.NET AJAX Control Toolkit の PasswordStrength 制御では、パスワードがどれだけ良好かを確認できます。

## <a name="overview"></a>概要

パスワードはほとんどすべての場所で必要になるため、レイジーユーザーは簡単に解読できる単純なパスワードを選択する傾向があります。 ASP.NET AJAX Control Toolkit の `PasswordStrength` コントロールは、パスワードがどれだけ良好かを確認できます。

## <a name="steps"></a>手順

`PasswordStrength` コントロールによってテキストボックスが拡張され、パスワードが十分であるかどうかがチェックされます。 属性を使用した豊富なオプションが用意されています。その一部を次に示します。

- パスワードに必要な数字の最小文字数を `MinimumNumericCharacters` します。
- パスワードに必要な記号 (文字と数字以外) の最小数を `MinimumSymbolCharacters` します。
- パスワードの最小 `PreferredPasswordLength` 長さ
- パスワードが大文字と小文字の両方を使用する必要があるかどうかを `RequiresUpperAndLowerCaseCharacters` する

`StrengthIndicatorType` には、パスワードの強度をテキスト (値 `"Text"`)、または進行状況バーの種類 (値 `"BarIndicator"`) として表示する方法が記載されています。 `DisplayPosition` 属性では、情報が表示される場所を構成します。 ここでは、ASP.NET AJAX `ScriptManager` コントロール、`PasswordStrength` 制御、ユーザーがパスワードを入力するテキストボックスなど、完全な例を示します。 このデモでは、後者のフォームフィールドは通常のテキストフィールドであり、パスワードフィールドではなく、開発中に入力した内容を確認できるようにするためのものです。

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

ページを実行して入力し直します: 小文字、大文字、数字、および記号を入力した後にのみ、パスワードは分割されていないと見なされます。

[現在、パスワードは (非常に) 良い ![](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)

これで、パスワードが (かなり) 良好になりました ([クリックすると、フルサイズの画像が表示](testing-the-strength-of-a-password-vb/_static/image3.png)されます)

> [!div class="step-by-step"]
> [[戻る]](testing-the-strength-of-a-password-cs.md)

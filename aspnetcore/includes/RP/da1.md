---
ms.openlocfilehash: e5565381f44480e2531925717ee7815da92d1ff5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030039"
---
# <a name="update-the-generated-pages"></a>生成されたページの更新

作成者: [Rick Anderson](https://twitter.com/RickAndMSFT)

ムービー アプリは上々の滑り出しでしたが、表示が理想的ではありません。 時刻の表示が好ましくなく (下の画像の 12:00:00 AM)、**ReleaseDate** は **Release Date** (2 つの単語) にするべきです。

![ムービー データが表示された、Chrome で開かれているムービー アプリケーション](../../tutorials/razor-pages/sql/_static/m55.png)

## <a name="update-the-generated-code"></a>生成されたコードの更新

*Models/Movie.cs* ファイルを開き、下のコードで強調表示されている行を追加します。

[!code-csharp[](code/Models/Movie.cs?highlight=2,11-12)]

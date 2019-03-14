---
ms.openlocfilehash: 2cd201e16cd491d0f468e8ef141b522f1694a257
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57165867"
---
**警告**:次のコードでは`GetTempFileName`、どのがスローされます、 `IOException` 65535 を超えるファイルが以前の一時ファイルを削除せずに作成された場合。 実際のアプリで一時ファイルが削除されるか、`GetTempPath` と `GetRandomFileName` を使用して一時ファイル名が作成されるはずです。 65535 のファイル制限はサーバーごとであるため、サーバー上の別のアプリが 65535 のすべてのファイルを使用することができます。 

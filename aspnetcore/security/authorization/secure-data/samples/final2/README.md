---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049109"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a>セキュリティで保護されたユーザー データのサンプルをビルド/実行する方法

* Secret Manager ツールを使用したパスワードを設定します。

  `dotnet user-secrets set SeedUserPW <pw>`

* データベースを更新します。

    `dotnet ef database update`

* プロジェクトで HTTPS を有効にします。

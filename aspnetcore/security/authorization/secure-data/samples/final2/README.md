---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049109"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a><span data-ttu-id="4c497-101">セキュリティで保護されたユーザー データのサンプルをビルド/実行する方法</span><span class="sxs-lookup"><span data-stu-id="4c497-101">How to build/run Secure user data sample</span></span>

* <span data-ttu-id="4c497-102">Secret Manager ツールを使用したパスワードを設定します。</span><span class="sxs-lookup"><span data-stu-id="4c497-102">Set password with the Secret Manager tool:</span></span>

  `dotnet user-secrets set SeedUserPW <pw>`

* <span data-ttu-id="4c497-103">データベースを更新します。</span><span class="sxs-lookup"><span data-stu-id="4c497-103">Update the database:</span></span>

    `dotnet ef database update`

* <span data-ttu-id="4c497-104">プロジェクトで HTTPS を有効にします。</span><span class="sxs-lookup"><span data-stu-id="4c497-104">Enable HTTPS in the project</span></span>

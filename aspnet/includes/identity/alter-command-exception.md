---
ms.openlocfilehash: b90e7963c5d9e5ef09fb519b72672c63bdffabee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57188719"
---
> <span data-ttu-id="d4ccd-101">いくつかのコマンドは、アプリは、その Id のデータ ストアとして SQLite を使用する場合にサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d4ccd-101">Some commands aren't supported if the app uses SQLite as its Identity data store.</span></span> <span data-ttu-id="d4ccd-102">データベース エンジンの制限により`Alter`コマンドは、次の例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="d4ccd-102">Due to limitations in the database engine, `Alter` commands throw the following exception:</span></span>
>
> <span data-ttu-id="d4ccd-103">"System.NotSupportedException:SQLite 操作をサポートしませんこの移行します。"</span><span class="sxs-lookup"><span data-stu-id="d4ccd-103">"System.NotSupportedException: SQLite does not support this migration operation."</span></span> 
>
> <span data-ttu-id="d4ccd-104">回避策としては、テーブルを変更するには、データベース、Code First migrations を実行します。</span><span class="sxs-lookup"><span data-stu-id="d4ccd-104">As a work around, run Code First migrations on the database to change the tables.</span></span>

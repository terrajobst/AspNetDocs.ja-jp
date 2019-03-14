---
ms.openlocfilehash: b90e7963c5d9e5ef09fb519b72672c63bdffabee
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57188719"
---
> いくつかのコマンドは、アプリは、その Id のデータ ストアとして SQLite を使用する場合にサポートされていません。 データベース エンジンの制限により`Alter`コマンドは、次の例外をスローします。
>
> "System.NotSupportedException:SQLite 操作をサポートしませんこの移行します。" 
>
> 回避策としては、テーブルを変更するには、データベース、Code First migrations を実行します。

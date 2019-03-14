---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048219"
---

> [!NOTE]
> スキーマ変更操作の多くは、EF Core の SQLite プロバイダーによってサポートされていません。 たとえば、列の追加はサポートされていますが、列の削除はサポートされていません。 移行を作成して、列を削除する場合、`ef migrations add`コマンドが成功したが、`ef database update`コマンドは失敗します。 これらの制限の一部は、手動でテーブルの再構築を実行する移行コードを記述することで解決できます。 テーブルの再構築が含まれます。

>* 既存のテーブルの名前を変更します。
>* 新しいテーブルを作成します。
>* 新しいテーブルには、古いテーブルからデータをコピーします。
>* 古いテーブルを削除しています。

詳細については、次のリソースを参照してください。
> * [SQLite EF Core データベース プロバイダーの制限事項](/ef/core/providers/sqlite/limitations)
> * [移行コードをカスタマイズする](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [データのシード処理](/ef/core/modeling/data-seeding)
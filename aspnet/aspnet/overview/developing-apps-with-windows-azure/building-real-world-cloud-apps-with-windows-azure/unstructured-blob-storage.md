---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
title: 非構造化 Blob Storage (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 03/30/2015
ms.assetid: 9f05ccb1-2004-4661-ad8b-c370e6c09c8e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
msc.type: authoredcontent
ms.openlocfilehash: f48b2be755b84dff9b2672bd348c73107602c6dd
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456792"
---
# <a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a>非構造化 Blob Storage (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

前の章では、パーティション構成について説明し、It アプリの修正によって Azure Storage Blob サービスに画像が格納される方法、および Azure SQL Database のその他のタスクデータについて説明しました。 この章では、Blob service について詳しく説明し、修正した It プロジェクトコードでの実装方法を示します。

## <a name="what-is-blob-storage"></a>BLOB ストレージとは

Azure Storage Blob サービスは、クラウドにファイルを格納する方法を提供します。 Blob service には、ローカルネットワークファイルシステムにファイルを保存するよりも多くの利点があります。

- 拡張性に優れています。 1つのストレージアカウントは、[数百テラバイトの](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx)データを格納でき、複数のストレージアカウントを持つことができます。 最大の Azure のお客様は、数百のペタバイトを格納しています。 Microsoft SkyDrive は、blob ストレージを使用します。
- 持続性があります。 Blob service に格納するすべてのファイルが自動的にバックアップされます。
- 高可用性が提供されます。 [ストレージの SLA](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409)は、選択した geo 冗長オプションに応じて、99.9% または99.99% の稼働時間を保証します。
- Azure のサービスとしてのプラットフォーム (PaaS) 機能です。これにより、ファイルを格納して取得するだけで、実際に使用したストレージの量に対してのみ料金が発生します。また、Azure では、処理.
- Blob service には、REST API を使用するか、プログラミング言語 API を使用してアクセスできます。 Sdk は、.NET、Java、Ruby などで使用できます。
- Blob service にファイルを保存すると、インターネット経由で簡単に公開できるようになります。
- Blob service のファイルは、承認されたユーザーのみがアクセスできるようにセキュリティで保護することができます。また、限られた期間だけユーザーが使用できるようにする一時的なアクセストークンを提供することもできます。

Azure 向けアプリを構築しているときに、オンプレミスの環境にある大量のデータを保存する場合は、画像、ビデオ、Pdf、スプレッドシートなどのファイルを使用することをお勧めします。 Blob service を検討してください。

## <a name="creating-a-storage-account"></a>ストレージアカウントの作成

Blob service の使用を開始するには、Azure でストレージアカウントを作成します。 ポータルで、[**新規** -- ] をクリックして、[**ストレージ** -- **簡易作成**] -- **Data Services** 、URL とデータセンターの場所を入力します。 データセンターの場所は、web アプリと同じである必要があります。

![ストレージアカウントの作成](unstructured-blob-storage/_static/image1.png)

コンテンツを格納するプライマリリージョンを選択します。 [geo レプリケーション](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage)オプションを選択した場合、Azure は、国の別のリージョンの別のデータセンターにすべてのデータのレプリカを作成します。 たとえば、米国西部のデータセンターを選択した場合、ファイルを保存すると、米国西部のデータセンターに移動しますが、バックグラウンドでは、他の米国のデータセンターのいずれかにもコピーされます。 ある国の1つのリージョンで障害が発生した場合でも、データは安全です。

Azure は地理的な境界を越えてデータをレプリケートしません。プライマリロケーションが米国内にある場合、ファイルは米国内の別のリージョンにのみレプリケートされます。プライマリの場所がオーストラリアの場合、ファイルはオーストラリアの別のデータセンターにのみレプリケートされます。

もちろん、先ほど見たように、スクリプトからコマンドを実行してストレージアカウントを作成することもできます。 ストレージアカウントを作成するための Windows PowerShell コマンドを次に示します。

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

ストレージアカウントを作成したら、すぐに Blob service にファイルの格納を開始できます。

## <a name="using-blob-storage-in-the-fix-it-app"></a>It アプリを修正するための Blob storage の使用

Fix It アプリでは、写真をアップロードできます。

![修正するタスクを作成する](unstructured-blob-storage/_static/image2.png)

**[FixIt の作成]** をクリックすると、アプリケーションは指定されたイメージファイルをアップロードし、Blob service に保存します。

### <a name="set-up-the-blob-container"></a>Blob コンテナーを設定する

Blob service にファイルを格納するには、そのファイルを格納する*コンテナー*が必要です。 Blob service コンテナーは、ファイルシステムフォルダーに対応します。 「[すべて自動化](automate-everything.md)」の章で確認した環境作成スクリプトでは、ストレージアカウントが作成されますが、コンテナーは作成されません。 したがって、`PhotoService` クラスの `CreateAndConfigure` メソッドの目的は、コンテナーがまだ存在しない場合に作成することです。 このメソッドは、 *global.asax*の `Application_Start` メソッドから呼び出されます。

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

ストレージアカウント名とアクセスキー*は、web.config ファイルの*`appSettings` コレクションに格納され、`StorageUtils.StorageAccount` メソッド内のコードはこれらの値を使用して接続文字列を作成し、接続を確立します。

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

次に、`CreateAndConfigureAsync` メソッドは、Blob service を表すオブジェクトと、Blob service 内の "images" という名前のコンテナー (フォルダー) を表すオブジェクトを作成します。

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

"Images" という名前のコンテナーがまだ存在しない場合は、新しいストレージアカウントに対して初めてアプリを実行したときに true になります。このコードでは、コンテナーを作成し、アクセス許可を設定してパブリックにすることができます。 (既定では、新しい blob コンテナーはプライベートであり、ストレージアカウントへのアクセス許可を持つユーザーのみがアクセスできます)。

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a>アップロードした写真を Blob storage に保存する

イメージファイルをアップロードして保存するために、アプリは、`IPhotoService` インターフェイスと、`PhotoService` クラスのインターフェイスの実装を使用します。 *PhotoService.cs*ファイルには、Blob service と通信する Fix It アプリのすべてのコードが含まれています。

次の MVC コントローラーメソッドは、ユーザーが  **FixIt の作成**をクリックしたときに呼び出されます。 このコードでは、`photoService` は `PhotoService` クラスのインスタンスを参照し、`fixittask` は新しいタスクのデータを格納する `FixItTask` エンティティクラスのインスタンスを参照します。

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

`PhotoService` クラスの `UploadPhotoAsync` メソッドは、アップロードされたファイルを Blob service に格納し、新しい Blob を指す URL を返します。

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

`CreateAndConfigure` メソッドと同様に、コードはストレージアカウントに接続し、"images" blob コンテナーを表すオブジェクトを作成します。ただし、コンテナーが既に存在していることを前提としています。

次に、新しい GUID 値をファイル拡張子と連結して、アップロードするイメージの一意の識別子を作成します。

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

次に、blob コンテナーオブジェクトと新しい一意識別子を使用して blob オブジェクトを作成し、ファイルの種類を示す属性をそのオブジェクトに設定して、blob オブジェクトを使用して blob ストレージにファイルを格納します。

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

最後に、blob を参照する URL を取得します。 この URL はデータベースに格納され、アップロードされたイメージを表示するために、It web ページの修正に使用できます。

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

この URL は、FixItTask テーブルの列の1つとしてデータベースに格納されます。

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

データベース内の URL と Blob storage のイメージのみを使用すると、It アプリケーションの修正によってデータベースのサイズが小さくなり、スケーラブルで、低コストになります。一方、ストレージは安価で、テラバイトまたはペタバイト単位で処理することができます。 1つのストレージアカウントは、数百テラバイトの写真を修正でき、使用した分だけ支払います。 最初のギガバイトに対しては9セントの低料金で開始でき、さらにギガバイトごとに少額のイメージを追加することもできます。

### <a name="display-the-uploaded-file"></a>アップロードされたファイルを表示する

It アプリケーションを修正すると、タスクの詳細が表示されるときに、アップロードされたイメージファイルが表示されます。

![写真を使用して It タスクの詳細を修正する](unstructured-blob-storage/_static/image3.png)

画像を表示するには、すべての MVC ビューで、ブラウザーに送信される HTML に `PhotoUrl` 値が含まれている必要があります。 Web サーバーとデータベースでは、イメージを表示するためにサイクルが使用されていません。イメージの URL に対して数バイトしか処理されません。 次の Razor コードでは、`Model` は `FixItTask` エンティティクラスのインスタンスを参照します。

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

表示されるページの HTML を見ると、次のような blob ストレージ内のイメージを直接指す URL が表示されます。

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a>要約

修正プログラムによる It アプリの Blob service でのイメージの保存方法と、SQL データベースのイメージ Url の使用方法について説明しました。 Blob service を使用すると、SQL データベースは、それ以外の場合と比べて大幅に小さくなります。これにより、ほぼ無制限の数のタスクをスケールアップすることができ、多くのコードを記述することなく実行できます。

ストレージアカウントには数百テラバイトを含めることができますが、ストレージコストは SQL Database ストレージよりもはるかにコストがかかります。これは、1 gb あたり約3セントで、トランザクション料金は小さいものです。 また、最大容量に対しては料金がかかりませんが、実際に格納されている量に対してのみ料金がかかります。そのため、アプリは拡張することができますが、その他の容量については一切料金がかかりません。

次の[章](design-to-survive-failures.md)では、クラウドアプリがエラーを適切に処理できるようにすることの重要性について説明します。

## <a name="resources"></a>リソース

詳細については、次のリソースを参照してください。

- [AZURE BLOB Storage の概要](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/)。 ブログ (Mike 木材)
- [.Net で Azure Blob Storage サービスを使用する方法](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。 MicrosoftAzure.com サイトの公式ドキュメント。 Blob storage の概要と、blob storage への接続、コンテナーの作成、blob のアップロードとダウンロードなどを示すコード例を紹介します。
- [フェイルセーフ: スケーラブルで回復力のある Cloud Services を構築](https://channel9.msdn.com/Series/FailSafe)します。 Ulrich Homann、Marc Mercuri、Mark Simm による9部構成のビデオシリーズ。 高度な概念とアーキテクチャの原則を、非常にアクセスしやすく興味深い方法で紹介します。実際の顧客との Microsoft カスタマーアドバイザリチーム (CAT) エクスペリエンスによってストーリーが描画されます。 Azure Storage サービスと blob の詳細については、35:13 以降のエピソード5を参照してください。
- [Microsoft のパターンとプラクティス-Azure のガイダンス](https://msdn.microsoft.com/library/dn568099.aspx)。 「Valet キーパターン」を参照してください。

> [!div class="step-by-step"]
> [前へ](data-partitioning-strategies.md)
> [次へ](design-to-survive-failures.md)

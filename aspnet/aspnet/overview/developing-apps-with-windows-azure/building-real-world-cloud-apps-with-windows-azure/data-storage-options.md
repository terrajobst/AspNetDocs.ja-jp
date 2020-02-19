---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
title: データストレージのオプション (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: e51fcecb-cb33-4f9e-8428-6d2b3d0fe1bf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
msc.type: authoredcontent
ms.openlocfilehash: 9357ed5aef39bed501cdac9ac26d46c884d4fae0
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457181"
---
# <a name="data-storage-options-building-real-world-cloud-apps-with-azure"></a>データストレージのオプション (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章](introduction.md)を参照してください。

ほとんどのユーザーはリレーショナルデータベースに使用され、クラウドアプリの設計時に他のデータストレージオプションが見落とされる傾向があります。 [NoSQL](http://en.wikipedia.org/wiki/NoSQL) (非リレーショナル) データベースはリレーショナルデータベースよりも効率的にタスクを処理できるので、結果は最適なパフォーマンス、高コスト、またはさらに悪化する可能性があります。 重要なデータストレージの問題の解決に役立つ情報をお客様からお寄せいただいた場合、多くの場合、NoSQL オプションのいずれかが適切に機能したリレーショナルデータベースがあることが原因です。 このような状況では、運用環境にアプリを展開する前に NoSQL ソリューションを実装している場合、顧客はより適切になります。

一方、NoSQL データベースでは、すべての問題を十分に処理できるということも間違いではありません。 すべてのデータストレージタスクに最適な1つのデータ管理を選択することはできません。さまざまなデータ管理ソリューションは、さまざまなタスクに合わせて最適化されています。 ほとんどの実際のクラウドアプリにはさまざまなデータストレージ要件があり、多くの場合、複数のデータストレージソリューションの組み合わせによって最適に提供されます。

この章の目的は、クラウドアプリで使用できるデータストレージオプションについて詳しく説明することと、シナリオに適したオプションを選択する方法についての基本的なガイダンスを提供することです。 アプリケーションを開発する前に、使用可能なオプションを認識し、長所と短所について検討することをお勧めします。 運用アプリでデータストレージオプションを変更することは非常に困難な場合があります。たとえば、プレーンフライト中に jet エンジンを変更する必要があります。

## <a name="data-storage-options-on-azure"></a>Azure のデータストレージオプション

クラウドによって、さまざまなリレーショナルデータストアや NoSQL データストアを比較的簡単に使用できます。 ここでは、Azure で使用できるデータストレージプラットフォームをいくつか紹介します。

![](data-storage-options/_static/image1.png)

次の表は、4種類の NoSQL データベースを示しています。

- [キー/値データベース](https://msdn.microsoft.com/library/dn313285.aspx#sec7)は、キー値ごとに1つのシリアル化されたオブジェクトを格納します。 指定されたキー値に対して 1 つの項目を取得し、項目の他のプロパティに基づいてクエリを実行する必要がない、大量のデータを格納する場合に適しています。

    [Azure Blob storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/)は、クラウド内のファイルストレージのように機能するキー/値データベースであり、フォルダー名とファイル名に対応するキー値を持ちます。 ファイルは、ファイルの内容の値を検索するのではなく、フォルダーとファイル名で取得します。

    [Azure Table storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)は、キー/値データベースでもあります。 各値は、(パーティションキーと行キーによって識別される)*エンティティ*と呼ばれ、複数の*プロパティ*を含みます (列に似ていますが、テーブル内のすべてのエンティティが同じ列を共有する必要はありません)。 キー以外の列に対するクエリは非常に非効率的であり、回避する必要があります。 たとえば、1つのユーザーに関する情報を格納する1つのパーティションを使用して、ユーザープロファイルデータを格納することができます。 ユーザー名、パスワードハッシュ、生年月日などのデータを、1つのエンティティの個別のプロパティ、または同じパーティション内の別のエンティティに格納することができます。 ただし、特定の期間の生年月日を持つすべてのユーザーを照会することはできません。また、プロファイルテーブルと別のテーブルとの間で結合クエリを実行することもできません。 テーブルストレージは、リレーショナルデータベースよりもスケーラビリティが高く、コストが低くなりますが、複雑なクエリや結合は使用できません。
- [Documentdatabases](https://msdn.microsoft.com/library/dn313285.aspx#sec8)は、値が*ドキュメント*であるキー/値データベースです。 ここでの "Document" は、Word または Excel のドキュメントの意味では使用されませんが、名前付きフィールドと値のコレクションを意味します。これらはいずれも子ドキュメントである可能性があります。 たとえば、注文履歴テーブルでは、注文書ドキュメントに order number、order date、および customer の各フィールドが含まれている可能性があります。また、customer フィールドには、[名前] フィールドと [住所] フィールドがあります。 データベースは、XML、YAML、JSON、BSON などの形式でフィールドデータをエンコードします。または、プレーンテキストを使用することもできます。 ドキュメントデータベースをキー/値データベースとは別に設定する機能の1つとして、非キーフィールドに対してクエリを実行し、セカンダリインデックスを定義してクエリの効率を高めることができます。 この機能により、ドキュメントデータベースは、ドキュメントキーの値よりも複雑な条件に基づいてデータを取得する必要があるアプリケーションに適しています。 たとえば、販売注文履歴ドキュメントデータベースでは、製品 ID、顧客 ID、顧客名などのさまざまなフィールドに対してクエリを実行できます。 [MongoDB](http://www.mongodb.org/)は、一般的なドキュメントデータベースです。
- [列ファミリデータベース](https://msdn.microsoft.com/library/dn313285.aspx#sec9)は、列ファミリと呼ばれる関連列のコレクションにデータストレージを構造化するためのキー/値データストアです。 たとえば、国勢調査データベースには、個人の名前 (最初、中央、最後)、個人の住所のグループ、および個人のプロファイル情報 (DOB、性別など) の1つのグループが含まれているとします。 その後、データベースは各列ファミリを個別のパーティションに格納し、同じキーに関連付けられている1人のデータをすべて保持できます。 その後、すべてのプロファイル情報を読み取ることができます。すべての名前とアドレス情報を読み取る必要はありません。 [Cassandra](http://cassandra.apache.org/)は広く普及している列ファミリデータベースです。
- [グラフデータベース](https://msdn.microsoft.com/library/dn313285.aspx#sec10)は、情報をオブジェクトとリレーションシップのコレクションとして格納します。 グラフデータベースの目的は、アプリケーションがオブジェクトのネットワークを通過するクエリと、オブジェクト間のリレーションシップを効率的に実行できるようにすることです。 たとえば、人事データベースではオブジェクトは従業員の可能性があります。また、"佐藤さんのために直接的または間接的に働いているすべての従業員を検索する" などのクエリを簡単にすることもできます。 [Neo4j](http://www.neo4j.org/)は一般的なグラフデータベースです。

リレーショナルデータベースと比較すると、NoSQL オプションを使用すると、構造化されていないデータのストレージと分析について、はるかに高いスケーラビリティとコスト効果が得ます。 トレードオフとは、リレーショナルデータベースの豊富な queryability と堅牢なデータ整合性機能を提供しないことです。 NoSQL は、クエリの結合を必要としない大量のボリュームを含む IIS ログデータに対して適切に機能します。 NoSQL は、データの絶対整合性を必要とし、他のアカウント関連データとの多くの関係を伴う銀行取引には適していません。

また、NoSQL データベースのスケーラビリティとリレーショナルデータベースの queryability およびトランザクション整合性を組み合わせる[Newsql](http://en.wikipedia.org/wiki/NewSQL)という名前の新しいカテゴリもあります。 NewSQL データベースは、分散ストレージおよびクエリ処理向けに設計されており、多くの場合、"OldSQL" データベースに実装するのは困難です。 [NuoDB](http://www.nuodb.com/)は、Azure で使用できる newsql データベースの例です。

<a id="hadoop"></a>
## <a name="hadoop-and-mapreduce"></a>Hadoop と MapReduce

NoSQL データベースに格納できる大量のデータは、適切なタイミングで効率的に分析するのが困難な場合があります。 これを行うには、 [MapReduce](http://en.wikipedia.org/wiki/MapReduce)機能を実装する[Hadoop](http://hadoop.apache.org/)などのフレームワークを使用します。 MapReduce プロセスは、基本的に次のような処理を行います。

- データストアから選択することで、処理する必要があるデータのサイズを制限します。実際に分析する必要があるデータのみを選択します。 たとえば、ユーザープロファイルデータストアの誕生日だけを選択する場合は、ユーザーの基本を誕生年別に把握しておく必要があります。
- データを部分的に分割し、処理のために別のコンピューターに送信します。 コンピューター A は、1950-1959 日、コンピューター B が1960-1969 を使用している人数を計算します。このグループのコンピューターは、 *Hadoop クラスター*と呼ばれます。
- パーツの処理が完了した後、各パーツの結果をまとめて配置します。 これで、各誕生年のユーザー数と、このリスト全体のパーセンテージを計算するタスクが比較的短いリストになりました。

Azure では、Hadoop の機能を使用してビッグデータを処理、分析し、新しい洞察を[得ることが](https://azure.microsoft.com/services/hdinsight/)できます。 たとえば、web サーバーのログを分析するために使用できます。

- ストレージアカウントへの web サーバーのログ記録を有効にします。 これにより、アプリケーションへのすべての HTTP 要求に対して Blob サービスにログを書き込むように Azure が設定されます。 Blob サービスは基本的にクラウドファイルストレージであり、HDInsight との統合に適しています。

    ![Blob Storage するログ](data-storage-options/_static/image2.png)
- アプリがトラフィックを取得すると、web サーバーの IIS ログが Blob ストレージに書き込まれます。

    ![Web サーバー ログ](data-storage-options/_static/image3.png)
- ポータルで、**新規** -  をクリックして**Data Services** - **hdinsight** - **簡易作成** をクリックし、HDInsight クラスター名、クラスターのサイズ (hdinsight クラスターのデータノードの数)、hdinsight クラスターのユーザー名とパスワードを指定します。

    ![HDInsight](data-storage-options/_static/image4.png)

これで、MapReduce ジョブを設定してログを分析し、次のような疑問に対する答えを得ることができます。

- アプリが最大または最小のトラフィックを取得するのはどのような時間ですか。
- トラフィックの発信元の国
- トラフィックの発信元となる領域の平均的な周辺収入は何ですか。 (IP アドレスによって地域の収入を提供するパブリックデータセットがあります。これは、web サーバーログの IP アドレスと一致させることができます)。
- 近所の収入は、サイト内の特定のページまたは製品とどのように関連付けられていますか。

次に、このような質問に対する回答を利用して、顧客が関心を持つ可能性や、特定の製品を購入する可能性に基づいて広告を対象にすることができます。

「[すべて自動化](automate-everything.md)」の章で説明したように、ポータルで実行できるほとんどの関数は自動化でき、HDInsight 分析ジョブの設定と実行も含まれます。 一般的な HDInsight スクリプトには、次の手順が含まれる場合があります。

- HDInsight クラスターをプロビジョニングし、Blob storage の入力用にストレージアカウントにリンクします。
- MapReduce ジョブの実行可能ファイル (.jar または .exe ファイル) を HDInsight クラスターにアップロードします。
- 出力データを Blob storage に格納する MapReduce を送信します。
- ジョブが完了するまで待ちます。
- HDInsight クラスターを削除する。
- Blob storage からの出力にアクセスします。

すべてを実行するスクリプトを実行することで、HDInsight クラスターがプロビジョニングされる時間を最小限に抑えることができます。これにより、コストを最小限に抑えることができます。

<a id="paasiaas"></a>
## <a name="platform-as-a-service-paas-versus-infrastructure-as-a-service-iaas"></a>サービスとしてのプラットフォーム (PaaS) とサービスとしてのインフラストラクチャ (IaaS)

前述のデータストレージオプションには、サービスとしてのプラットフォーム (PaaS) とサービスとしてのインフラストラクチャ (IaaS) ソリューションの両方が含まれています。 PaaS は、ハードウェアとソフトウェアのインフラストラクチャを管理し、サービスを使用することを意味します。 SQL Database は、Azure の PaaS 機能です。 データベースを要求すると、その後、Azure によって Vm がセットアップおよび構成され、データベースが設定されます。 Vm に直接アクセスすることはできません。 Vm を管理する必要はありません。IaaS は、データセンターインフラストラクチャで実行される Vm を設定、構成、および管理し、必要なものを任意に配置することを意味します。 一般的な VM 構成用に事前に構成された VM イメージのギャラリーが用意されています。 たとえば、Windows Server 2008、Windows Server 2012、BizTalk Server、Oracle WebLogic Server、Oracle Database などの事前構成済みの VM イメージをインストールできます。

Azure が提供する PaaS データソリューションには、次のものがあります。

- Azure SQL Database (旧称 SQL Azure)。 SQL Server に基づくクラウドリレーショナルデータベース。
- Azure Table Storage。 キー/値 NoSQL データベース。
- Azure Blob Storage。 クラウド内のファイルストレージ。

IaaS の場合は、VM に読み込むことのできるすべてのものを実行できます。次に例を示します。

- リレーショナルデータベース (SQL Server、Oracle、MySQL、SQL Compact、SQLite、Postgres など)。
- Memcached、Redis、Cassandra、Riak などのキー/値データストア。
- HBase などの列データストア。
- MongoDB、RavenDB、CouchDB などのドキュメントデータベース。
- Neo4j などのグラフデータベース。

![Azure のデータストレージオプション](data-storage-options/_static/image5.png)

IaaS オプションを使用すると、ほとんど無制限のデータストレージオプションが得られます。構成済みのイメージを使用して Vm を作成できるため、これらの多くは特に簡単に使用できます。 たとえば、管理ポータルで**Virtual Machines**に移動し、 **[イメージ]** タブをクリックして、VM の使用方法の **[参照]** をクリックします。

![VM の引き取りを参照](data-storage-options/_static/image6.png)

数[百の事前構成済みの vm イメージ](http://www.hanselman.com/blog/Over400VirtualMachineImagesOfOpenSourceSoftwareStacksInTheVMDepotAzureGallery.aspx)の一覧が表示され、MongoDB、Neo4J、Redis、Cassandra、CouchDB などのデータベース管理システムがプレインストールされたイメージから vm を作成できます。

![VM の引き取りでの MongoDB](data-storage-options/_static/image7.png)

Azure では、IaaS データストレージオプションを可能な限り簡単に使用できますが、PaaS オファリングには、多くのシナリオにおいてコスト効率が高く、実用的であるという多くの利点があります。

- Vm を作成する必要はありませんが、ポータルまたはスクリプトを使用してデータストアを設定するだけです。 200テラバイトのデータストアが必要な場合は、ボタンをクリックするかコマンドを実行するだけで、数秒で使用できるようになります。
- サービスによって使用される Vm を管理または修正する必要はありません。Microsoft は自動的にこれを行います。-スケーリングや高可用性のためのインフラストラクチャのセットアップについて心配する必要はありません。Microsoft はすべてのことを処理します。
- ライセンスを購入する必要はありません。ライセンス料金は、サービス料金に含まれています。
- 料金は使用した分だけになります。

Azure の PaaS データストレージオプションには、サードパーティプロバイダーによって提供されるサービスが含まれています。 たとえば、Azure ストアから[MongoLab アドオン](https://azure.microsoft.com/documentation/articles/store-mongolab-web-sites-dotnet-store-data-mongodb/)を選択して、MongoDB データベースをサービスとしてプロビジョニングすることができます。

## <a name="choosing-a-data-storage-option"></a>データストレージオプションの選択

すべてのシナリオに適した方法はありません。 このテクノロジが答えであることがわかっている場合、最初に質問するのは、さまざまなソリューションがさまざまな用途に合わせて最適化されているためです。 リレーショナルモデルには明確な利点があります。そのため、これはそれほど長くありません。 ただし、NoSQL ソリューションを使用して対処できる、SQL のダウンサイドもあります。

多くの場合、1つのソリューションで SQL と NoSQL を使用する複合的なアプローチが最適です。 ユーザーが NoSQL を採用している場合でも、何をしているかを掘り下げていくと、さまざまな NoSQL フレームワークを使用していることがよくわかります。これらのフレームワークでは、 [CouchDB](http://wiki.apache.org/couchdb/Introduction)、 [Redis](http://redis.io/)、および[riak](http://basho.com/riak/)がさまざまな目的で使用されています。 NoSQL を幅広く使用する Facebook でも、サービスのさまざまな部分に異なる NoSQL フレームワークを使用します。 データストレージのアプローチを柔軟に組み合わせることは、複数のデータソリューションを使用して1つのアプリに統合するのが簡単であるため、クラウドにとって優れている点の1つです。

アプローチを選択する場合は、次の点を考慮する必要があります。

| データセマンティック | -コアデータストレージとデータアクセスのセマンティックとは何ですか (リレーショナルデータまたは非構造化データを格納していますか)。 メディアファイルなどの非構造化データは、blob ストレージに最適です。製品、在庫、仕入先、顧客注文などの関連データのコレクションは、リレーショナルデータベースに最適です。 |
| --- | --- |
| クエリのサポート | -データに対してクエリを実行するのは簡単ですか。 -どのような種類の質問を効率的に要求できますか。 キー値を指定して1つの行を取得するには、キー/値データストアが非常に優れていますが、複雑なクエリには適していません。 常に1つの特定のユーザーのデータを取得しているユーザープロファイルデータストアの場合、キー/値データストアが正常に機能する可能性があります。製品カタログでは、さまざまな製品属性に基づいて異なるグループを取得する必要がある場合は、リレーショナルデータベースの方が適している可能性があります。 NoSQL データベースは大量のデータを効率的に格納できますが、アプリがデータを照会する方法を中心にデータベースを構成する必要があります。これにより、アドホッククエリの実行が困難になります。 リレーショナルデータベースを使用すると、ほぼすべての種類のクエリを作成できます。 |
| 機能プロジェクション | -サーバー側で実行できる質問や集計などがありますか。 SQL のテーブルから SELECT COUNT (\*) を実行すると、サーバー上のすべての作業が非常に効率的に実行され、探している数値が返されます。 集計をサポートしていない NoSQL データストアから同じ計算を行う場合、これは非効率的な "無制限クエリ" であり、タイムアウトする可能性があります。クエリが成功した場合でも、サーバーからクライアントにすべてのデータを取得し、クライアントの行をカウントする必要があります。 -使用できる式の言語または種類を教えてください。 リレーショナルデータベースでは、SQL を使用できます。 Azure Table storage などの一部の NoSQL データベースでは、 [OData](http://www.odata.org/)を使用します。これは、主キーに対してフィルター処理を行い、プロジェクションを取得する (使用可能なフィールドのサブセットを選択する) だけです。 |
| 拡張性の向上 | -どのくらいの頻度でデータをスケールする必要がありますか。 -プラットフォームはネイティブにスケールアウトを実装していますか。 -容量 (サイズとスループット) を追加または削除するのは簡単ですか? リレーショナルデータベースとテーブルは、拡張性を確保するために自動的にパーティション分割されないため、特定の制限を超えて拡張することは困難です。 Azure Table storage のような NoSQL データストアは、本質的にすべてをパーティション分割します。パーティションの追加にはほとんど制限がありません。 最大200テラバイトの Table Storage を簡単にスケーリングできますが、Azure SQL Database のデータベースの最大サイズは 500 gb です。 リレーショナルデータは、複数のデータベースにパーティション分割することによって拡張できますが、そのモデルをサポートするようにアプリケーションを設定するには、多数のプログラミング作業が必要になります。 |
| インストルメンテーションと管理性 | -プラットフォームがどの程度簡単にインストルメント化、監視、および管理できるか。 データストアの正常性とパフォーマンスに関する情報を常に把握しておく必要があります。そのため、プラットフォームが無償で提供するメトリックと、自分で開発する必要があるものを事前に把握しておく必要があります。 |
| 運用 | -Azure でデプロイおよび実行するプラットフォームはどれほど簡単ですか? PaaS? IaaS? マシン? Table Storage と SQL Database は、Azure で簡単にセットアップできます。 Azure PaaS ソリューションが組み込まれていないプラットフォームでは、より多くの労力が必要になります。 |
| API のサポート | -プラットフォームを簡単に操作できる API が用意されていますか。 Azure Table Service の SDK には、.net 4.5 の非同期プログラミングモデルをサポートする .NET API が含まれています。 .NET アプリを作成している場合は、Azure Table Service のコードを記述してテストする方がはるかに簡単です。 API がない別のキー/値列のデータストアプラットフォームや、あまり包括的ではないものがあります。 |
| トランザクションの整合性とデータの一貫性 | -プラットフォームがデータの一貫性を保証するためにトランザクションをサポートしていることは重要ですか。 送信された一括メールを追跡するには、データプラットフォームでのトランザクションまたは参照整合性の自動サポートよりもパフォーマンスと低データストレージコストが重要になることがあります。そのため、Azure Table Service を使用することをお勧めします。 銀行口座の残高や注文書を追跡する場合は、強力なトランザクション保証を提供するリレーショナルデータベースプラットフォームの方が適しています。 |
| ビジネス継続性 | -バックアップ、復元、ディザスターリカバリーの容易さ 前または後の実稼働データが破損しているため、元に戻す機能が必要です。 多くの場合、リレーショナルデータベースには、特定の時点に復元する機能など、よりきめ細かな復元機能があります。 検討している各プラットフォームで使用できる復元機能を理解することは、考慮すべき重要な要素です。 |
| Cost | -複数のプラットフォームがデータワークロードをサポートできる場合、コストを比較するにはどうすればよいでしょうか。 たとえば、ASP.NET Identity を使用する場合、ユーザープロファイルデータを Azure Table Service または Azure SQL Database に格納できます。 SQL Database の豊富なクエリ機能が不要な場合は、Azure テーブルを選択することもできます。これは、特定の量のストレージに対してコストが大幅に削減されるためです。 |

データストレージソリューションを選択する前に、これらの各カテゴリの質問に対する回答を確認することをお勧めします。

また、ワークロードには、プラットフォームによってはサポートされる可能性のある特定の要件がある場合があります。 例 :

- アプリケーションには監査機能が必要ですか。
- データの保存期間の要件はどのようなものですか?-自動アーカイブまたは削除の機能が必要ですか?
- 特別なセキュリティニーズはありますか。 たとえば、データには PII (個人を特定できる情報) が含まれますが、クエリ結果から PII が除外されるようにする必要があります。
- 規制や技術的な理由でクラウドに保存できないデータがある場合は、オンプレミスストレージとの統合を容易にするクラウドデータストレージプラットフォームが必要になることがあります。

## <a name="demo--using-sql-database-in-azure"></a>デモ– Azure での SQL Database の使用

Fix It アプリは、リレーショナルデータベースを使用してタスクを格納します。 「[すべて自動化](automate-everything.md)」の章に示されている環境作成の Windows PowerShell スクリプトは、2つの SQL Database インスタンスを作成します。 ポータルで **[SQL データベース]** タブをクリックすると、これらを確認できます。

![ポータルの SQL データベース](data-storage-options/_static/image8.png)

ポータルを使用してデータベースを簡単に作成することもできます。

**新規--Data Services** -- **SQL Database** -- **簡易作成** をクリックし、データベース名を入力します。アカウントに既にあるサーバーを選択するか、新しいサーバーを作成して、**SQL Database の作成** をクリックします。

![新しい SQL データベース](data-storage-options/_static/image9.png)

数秒待ってから、Azure のデータベースを使用する準備ができていることを確認してください。

![新しい SQL Database 作成済み](data-storage-options/_static/image10.png)

Azure では、オンプレミス環境での実行に1日または1週間以上かかることがあります。 また、スクリプト内や管理 API を使用してデータベースを自動的に作成するのと同じように、アプリケーションがプログラミングされている限り、データを複数のデータベースに分散させることで、動的にスケールアウトすることができます。

これは、サービスとしてのプラットフォームモデルの例です。 サーバーを管理する必要はありません。 バックアップについて心配する必要はありません。 高可用性で実行されています。データベース内のデータは、3つのサーバー間で自動的にレプリケートされます。 コンピューターで障害が発生した場合、自動的にフェールオーバーされ、データは失われます。 サーバーには定期的にパッチが適用されますが、それについて心配する必要はありません。

ボタンをクリックすると、必要な正確な接続文字列が表示され、新しいデータベースの使用をすぐに開始できます。

![Connection strings](data-storage-options/_static/image11.png)

ダッシュボードには、接続の履歴と使用されているストレージの量が表示されます。

![SQL Database ダッシュボード](data-storage-options/_static/image12.png)

データベースを管理するには、ポータルで、または既に使い慣れている SQL Server ツールを使用します。たとえば、SQL Server Management Studio (SSMS)、Visual Studio tools SQL Server オブジェクトエクスプローラー (SSOX)、サーバーエクスプローラーなどです。

![SSOX](data-storage-options/_static/image13.png)

もう1つの優れた点は、価格モデルです。 20 MB の無料データベースを使用して開発を開始することができ、運用データベースは1か月あたり約 $5 から開始できます。 実際には、データベースに格納されているデータの量に対してのみ課金され、最大容量は支払いません。 ライセンスを購入する必要はありません。

SQL Database は簡単に拡張できます。 It アプリを修正するために、自動化スクリプトで作成するデータベースは 1 gb に制限されています。 最大 150 gb まで拡張するには、ポータルに移動し、その設定を変更するか REST API コマンドを実行します。また、データを配置できる 150 gb のデータベースがあることを秒単位で確認できます。

![SQL Database のエディションとサイズ](data-storage-options/_static/image14.png)

これは、インフラストラクチャを迅速かつ簡単に立ち上げ、すぐに使用を開始するクラウドの能力です。

この修正プログラムでは、メンバーシップ (認証と承認) 用とデータ用の2つの SQL データベースが使用されています。これにより、プロビジョニングとスケーリングを行う必要があります。 Windows PowerShell スクリプトを使用してデータベースをプロビジョニングする方法について説明しましたが、ポータルで簡単に実行できることがわかりました。

## <a name="entity-framework-versus-direct-database-access-using-adonet"></a>ADO.NET を使用した Entity Framework とデータベースへの直接アクセス

この修正プログラムでは、.NET アプリケーション用の Microsoft の推奨される ORM (オブジェクトリレーショナルマッパー) Entity Framework を使用して、このようなデータベースにアクセスします。 ORM は、開発者の生産性を向上させる優れたツールですが、一部のシナリオではパフォーマンスが低下します。 実際のクラウドアプリでは、EF を使用するか、直接 ADO.NET を使用するかを選択することはできません。両方を使用します。 データベースで動作するコードを記述するほとんどの場合、パフォーマンスを最大にすることは重要ではなく、Entity Framework によって得られる単純化されたコーディングとテストを活用できます。 EF のオーバーヘッドによって許容できないパフォーマンスが発生する場合は、ストアドプロシージャを呼び出すことで、ADO.NET を使用して独自のクエリを記述して実行できます。

データベースへのアクセスに使用する方法にかかわらず、できるだけ "頻繁な通信" を最小化することをお勧めします。 つまり、必要なすべてのデータを、数十または数百の小さなクエリ結果セットではなく、1つの大きなクエリ結果セットとして取得できる場合は、通常はそれが適しています。 たとえば、学生とそれらが登録されているコースを一覧表示する必要がある場合は、通常、1つのクエリで学生を取得し、各学生のコースに対して個別のクエリを実行するのではなく、1つの結合クエリですべてのデータを取得することをお勧めします。

## <a name="sql-databases-and-the-entity-framework-in-the-fix-it-app"></a>SQL データベースと修正プログラムの It アプリの Entity Framework

Fix It app では、Entity Framework `DbContext` クラスから派生した `FixItContext` クラスによってデータベースが識別され、データベース内のテーブルが指定されます。 コンテキストでは、タスクのエンティティセット (テーブル) を指定し、コードが接続文字列名をコンテキストに渡します。 この名前は、web.config ファイルで定義されている接続文字列を表します。

[!code-csharp[Main](data-storage-options/samples/sample1.cs?highlight=4,8)]

*Web.config ファイル内*の接続文字列は、appdb という名前になります (ここでは、ローカル開発データベースを指しています)。

[!code-xml[Main](data-storage-options/samples/sample2.xml?highlight=3)]

Entity Framework は、`FixItTask` エンティティクラスに含まれるプロパティに基づいて、 *Fixittasks*テーブルを作成します。 これは単純な POCO (Plain Old CLR Object) クラスです。つまり、これは、から継承されたり、Entity Framework に依存したりしないことを意味します。 ただし Entity Framework は、それに基づいてテーブルを作成し、CRUD (作成、読み取り、更新、削除) 操作を実行する方法を知っています。

[!code-csharp[Main](data-storage-options/samples/sample3.cs)]

![FixItTasks テーブル](data-storage-options/_static/image15.png)

Fix It アプリには、データストアを操作する CRUD 操作に使用するリポジトリインターフェイスが含まれています。

[!code-csharp[Main](data-storage-options/samples/sample4.cs)]

リポジトリのメソッドがすべて非同期であるため、すべてのデータアクセスを完全に非同期に実行できます。

リポジトリの実装は、LINQ クエリだけでなく、挿入、更新、および削除の各操作についても、データを操作するために Entity Framework 非同期メソッドを呼び出します。 Fix It タスクを検索するコードの例を次に示します。

[!code-csharp[Main](data-storage-options/samples/sample5.cs)]

ここでは、タイミングとエラーのログ記録のコードもあります。この点については、後で[監視とテレメトリ](monitoring-and-telemetry.md)に関する章をご覧ください。

<a id="sqliaas"></a>
## <a name="choosing-sql-database-paas-versus-sql-server-in-a-vm-iaas-in-azure"></a>Azure での VM (IaaS) での SQL Database (PaaS) と SQL Server の選択

SQL Server と Azure SQL Database についての優れた点は、両方のコアプログラミングモデルが同じであることです。 同じスキルのほとんどを両方の環境で使用できます。 開発中の SQL Server データベースとクラウドの SQL Database インスタンスを使用することもできます。これは、It アプリの修正プログラムのセットアップ方法です。

別の方法として、IaaS Vm にインストールして、オンプレミスで実行するのと同じ SQL Server をクラウドで実行することもできます。 一部のレガシアプリケーションでは、VM で SQL Server を実行する方が適している場合があります。 SQL Server データベースは専用 VM 上で実行されるため、共有サーバーで実行されている SQL Database データベースよりも多くのリソースを使用できます。 つまり、SQL Server データベースは大きくなる可能性があり、それでも正常に動作します。 一般に、データベースのサイズとテーブルのサイズが小さいほど、SQL Database (PaaS) でのユースケースの方が適しています。

2つのモデルを選択する方法に関するガイドラインを次に示します。

| Azure SQL Database (PaaS) | 仮想マシン (IaaS) での SQL Server |
| --- | --- |
| **長所**-vm の作成や管理、OS や SQL の更新、パッチの適用は不要です。Azure では、このことを行います。 -データベースレベルの SLA を備えた組み込みの高可用性。 -総保有コスト (TCO) は、使用した分だけ支払います (ライセンスは必要ありません)。 -小さいデータベースを大量に処理する場合に適しています (&lt;はそれぞれ 500 GB です)。 -新しいデータベースを動的に作成して、スケールアウトを有効にすることができます。 | ***プロフェッショナル***-機能とオンプレミスの SQL Server との互換性。 -VM レベルの SLA を使用して、2つ以上の Vm で AlwaysOn を使用して SQL Server[高可用性](https://www.microsoft.com/sqlserver/solutions-technologies/mission-critical-operations/high-availability.aspx)を実装できます。 -SQL の管理方法を完全に制御できます。 -既に所有している SQL ライセンスを再利用することも、1時間ごとに支払いを行うこともできます。 -より小さい (1 TB 以上) データベースを処理する場合に適しています。 |
| **短所**-オンプレミスの SQL Server ( [CLR 統合](https://technet.microsoft.com/library/ms131102.aspx)の欠如、 [tde](https://technet.microsoft.com/library/bb934049.aspx)、[圧縮サポート](https://technet.microsoft.com/library/cc280449.aspx)、 [SQL Server Reporting Services](https://technet.microsoft.com/library/ms159106.aspx)など) と比較した一部の機能のギャップ (データベースサイズの上限は 500 gb)。 | ***短所***-更新プログラム/パッチ (OS と SQL) は、ユーザーの責任として、db の責任 (1 秒あたりの入力/出力操作) は約 8000 (16 データドライブを使用) に制限されます。 |

VM で SQL Server を使用する場合は、独自の SQL Server ライセンスを使用することも、1時間分の料金を支払うこともできます。 たとえば、ポータルまたは REST API 経由で、SQL Server イメージを使用して新しい VM を作成できます。

![SQL Server を使用した VM の作成](data-storage-options/_static/image16.png)

![SQL Server VM イメージの一覧](data-storage-options/_static/image17.png)

SQL Server イメージを使用して VM を作成すると、VM の使用量に基づいて、SQL Server ライセンスコストが1時間ごとに評価されます。 2か月に1回だけ実行するプロジェクトがある場合は、1時間分の料金がかかります。 プロジェクトが長年にわたって最後になると思われる場合は、通常どおりにライセンスを購入する方が安価です。

## <a name="summary"></a>要約

クラウドコンピューティングを使用すると、アプリケーションのニーズに合わせてデータストレージアプローチを最大限に活用し、対応することができます。 新しいアプリケーションを構築している場合は、ここに記載されている質問について慎重に検討して、アプリケーションの規模が拡大しても引き続き適切に機能する方法を選択してください。 [次の章](data-partitioning-strategies.md)では、複数のデータストレージアプローチを組み合わせるために使用できるパーティション分割方法について説明します。

## <a name="resources"></a>リソース

詳細については、次のリソースを参照してください。

データベースプラットフォームの選択:

- [拡張性の高いソリューションのためのデータアクセス: SQL、NoSQL、および多言語の永続性を使用](https://aka.ms/dag-doc)します。 Microsoft のパターンとプラクティスによって、クラウドアプリケーションで使用できるさまざまな種類のデータストアについて詳しく解説しています。
- [Microsoft のパターンとプラクティス-Azure のガイダンス](https://msdn.microsoft.com/library/ff898430.aspx)。 「データの一貫性の概要」、「データのレプリケーションと同期のガイダンス」、「インデックステーブルパターン」、「具体化されたビューパターン」を参照してください。
- [BASE: Acid の代替手段](http://queue.acm.org/detail.cfm?id=1394128)です。 データの一貫性とスケーラビリティのトレードオフについての記事です。
- 7[週間の7つのデータベース: 最新のデータベースと NoSQL 移動のガイドです](https://www.amazon.com/Seven-Databases-Weeks-Modern-Movement/dp/1934356921)。 Eric Redmond と Jim r. Wilson の書籍です。 現在利用可能なデータストレージプラットフォームの範囲についてご紹介します。

SQL Server と SQL Database の選択:

- [SQL Database ガイダンスの Premium プレビュー](https://msdn.microsoft.com/library/windowsazure/dn369873.aspx)。 SQL Database Premium の概要と、SQL Database Web edition および Business edition から選択する場合のガイダンスについて説明します。
- [ガイドラインと制限事項 (Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)。 SQL Database の制限事項に関するドキュメントにリンクされたポータルページ。 SQL Database がサポートしていない SQL Server の機能に重点を置いています。
- [Azure Virtual Machines で SQL Server](https://msdn.microsoft.com/library/windowsazure/jj823132.aspx)ます。 Azure での SQL Server の実行に関するドキュメントへのリンクが掲載されているポータルページ。
- [Scott Guthrie は、Azure の SQL データベースについて説明して](https://azure.microsoft.com/documentation/videos/sql-in-azure-scottgu/)います。 6分間のビデオでは、Scott Guthrie による SQL Database の概要について説明します。
- [Azure Virtual Machines で SQL Server するためのアプリケーションパターンと開発戦略](https://msdn.microsoft.com/library/windowsazure/dn574746.aspx)。

ASP.NET Web アプリでの Entity Framework と SQL Database の使用

- [MVC 5 を使用した EF 6 でのはじめに](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 「9パートチュートリアルシリーズ」では、EF を使用してデータベースを Azure にデプロイし、SQL Database する MVC アプリを構築する手順について説明します。
- [Visual Studio を使用した ASP.NET Web デプロイ](../../../../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 「12パートチュートリアルシリーズ」では、EF Code First を使用してデータベースを配置する方法についてさらに詳しく説明します。
- [メンバーシップ、OAuth、SQL Database を持つ Secure ASP.NET MVC 5 アプリを Azure の Web サイトにデプロイ](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)します。 認証を使用する web アプリを作成する手順を説明したチュートリアルです。メンバーシップデータベースにアプリケーションテーブルを格納し、データベーススキーマを変更して、Azure にアプリをデプロイします。
- [ASP.NET Data Access コンテンツマップ](https://go.microsoft.com/fwlink/p/?LinkId=282414)。 EF と SQL Database を操作するためのリソースへのリンク。

Azure での MongoDB の使用:

- [MongoLab-Azure での MongoDB](http://msopentech.com/opentech-projects/mongolab-mongodb-on-windows-azure/)。 Azure での MongoDB の実行に関するドキュメントのポータルページです。
- [Azure の仮想マシンで実行されている MongoDB に接続する azure の web サイトを作成](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-store-data-mongodb-vm/)します。 ASP.NET web アプリケーションで MongoDB データベースを使用する方法を示すステップバイステップのチュートリアルです。

HDInsight (Azure 上の Hadoop):

- [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)。 [Azure](https://azure.microsoft.com/) web サイトの HDInsight のドキュメントを参照してください。
- [Hadoop と HDInsight: Azure のビッグデータ](https://msdn.microsoft.com/magazine/dn385705.aspx)。 Bruno Terkaly と高橋さん Villalobos による MSDN マガジン記事。 Azure での Hadoop の導入。
- [Microsoft のパターンとプラクティス-Azure のガイダンス](https://msdn.microsoft.com/library/dn568099.aspx)。 MapReduce パターンを参照してください。

> [!div class="step-by-step"]
> [前へ](single-sign-on.md)
> [次へ](data-partitioning-strategies.md)

---
uid: web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
title: 追加のユーザー情報をC#格納する () |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、非常に基本的なゲストブックアプリケーションを構築することで、この質問に答えます。 ここでは、modeli のさまざまなオプションについて説明します。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 1642132a-1ca5-4872-983f-ab59fc8865d3
msc.legacyurl: /web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
msc.type: authoredcontent
ms.openlocfilehash: 24b96e86bc93e03d2639b73e35ed1fd1271bac5a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74641452"
---
# <a name="storing-additional-user-information-c"></a>追加のユーザー情報を格納する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_08_CS.zip)または[PDF のダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial08_ExtraUserInfo_cs.pdf)

> このチュートリアルでは、非常に基本的なゲストブックアプリケーションを構築することで、この質問に答えます。 ここでは、データベースでユーザー情報をモデル化するためのさまざまなオプションについて説明し、メンバーシップフレームワークによって作成されたユーザーアカウントにこのデータを関連付ける方法について説明します。

## <a name="introduction"></a>はじめに

ASP.NET のメンバーシップフレームワークは、ユーザーを管理するための柔軟なインターフェイスを提供します。 メンバーシップ API には、資格情報の検証、現在ログオンしているユーザーに関する情報の取得、新しいユーザーアカウントの作成、および他のユーザーアカウントの削除を行うためのメソッドが含まれています。 メンバーシップフレームワークの各ユーザーアカウントには、資格情報を検証し、ユーザーアカウント関連の重要なタスクを実行するために必要なプロパティのみが含まれています。 これは、メンバーシップフレームワークでユーザーアカウントをモデル化する[`MembershipUser` クラス](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)のメソッドとプロパティによって、このことが判明します。 このクラスには、 [`UserName`](https://msdn.microsoft.com/library/system.web.security.membershipuser.username.aspx)、 [`Email`](https://msdn.microsoft.com/library/system.web.security.membershipuser.email.aspx)、 [`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx)などのプロパティと、 [`GetPassword`](https://msdn.microsoft.com/library/system.web.security.membershipuser.getpassword.aspx)や[`UnlockUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)などのメソッドがあります。

多くの場合、アプリケーションでは、メンバーシップフレームワークに含まれていない追加のユーザー情報を格納する必要があります。 たとえば、オンライン小売業者は、各ユーザーに配送先住所と請求先住所、支払い情報、配信設定、連絡先の電話番号を保存することが必要になる場合があります。 さらに、システム内の各注文は、特定のユーザーアカウントに関連付けられています。

`MembershipUser` クラスには、`PhoneNumber`、`DeliveryPreferences`、`PastOrders`などのプロパティは含まれません。 では、アプリケーションが必要とするユーザー情報を追跡し、それをメンバーシップフレームワークと統合するにはどうすればよいでしょうか。 このチュートリアルでは、非常に基本的なゲストブックアプリケーションを構築することで、この質問に答えます。 ここでは、データベースでユーザー情報をモデル化するためのさまざまなオプションについて説明し、メンバーシップフレームワークによって作成されたユーザーアカウントにこのデータを関連付ける方法について説明します。 では、始めましょう。

## <a name="step-1-creating-the-guestbook-applications-data-model"></a>手順 1: ゲストブックアプリケーションのデータモデルを作成する

データベース内のユーザー情報をキャプチャし、メンバーシップフレームワークによって作成されたユーザーアカウントに関連付けることができるさまざまな手法があります。 これらの手法を説明するために、ユーザーに関連する何らかのデータをキャプチャするように、チュートリアル web アプリケーションを拡張する必要があります。 (現時点では、アプリケーションのデータモデルには、`SqlMembershipProvider`に必要なアプリケーションサービステーブルだけが含まれています)。

認証されたユーザーがコメントを残すことができる、非常に単純なゲストブックアプリケーションを作成しましょう。 ゲストブックのコメントを保存するだけでなく、各ユーザーに自宅の町、ホームページ、署名を保存することができます。 指定した場合、ユーザーのホーム、ホームページ、署名は、ゲストブックに残されている各メッセージに表示されます。

### <a name="adding-theguestbookcommentstable"></a>`GuestbookComments`テーブルの追加

ゲストブックのコメントを取得するには、`CommentId`、`Subject`、`Body`、`CommentDate`などの列を含む `GuestbookComments` という名前のデータベーステーブルを作成する必要があります。 また、`GuestbookComments` テーブル内の各レコードが、コメントを残したユーザーを参照している必要もあります。

このテーブルをデータベースに追加するには、Visual Studio のデータベースエクスプローラーに移動し、`SecurityTutorials` データベースにドリルダウンします。 [テーブル] フォルダーを右クリックし、[新しいテーブルの追加] をクリックします。 これにより、新しいテーブルの列を定義できるインターフェイスが表示されます。

[SecurityTutorials データベースに新しいテーブルを追加 ![には](storing-additional-user-information-cs/_static/image2.png)](storing-additional-user-information-cs/_static/image1.png)

**図 1**: `SecurityTutorials` データベースに新しいテーブルを追加する ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image3.png)されます)

次に、`GuestbookComments`の列を定義します。 まず、`uniqueidentifier`型の `CommentId` という名前の列を追加します。 この列は、ゲストブック内の各コメントを一意に識別するため、`NULL` を禁止し、テーブルの主キーとしてマークします。 各 `INSERT`の [`CommentId`] フィールドに値を指定するのではなく、列の既定値を `NEWID()`に設定することによって、`INSERT` 上のこのフィールドに対して新しい `uniqueidentifier` 値を自動的に生成するように指定できます。 この最初のフィールドを追加して主キーとしてマークし、既定値を設定すると、画面は図2に示すスクリーンショットのようになります。

[CommentId という名前のプライマリ列を追加 ![には](storing-additional-user-information-cs/_static/image5.png)](storing-additional-user-information-cs/_static/image4.png)

**図 2**: `CommentId` という名前のプライマリ列を追加[する (クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image6.png)される)

次に、`nvarchar(50)` 型の `Subject` という名前の列と `nvarchar(MAX)`型の `Body` という名前の列を追加し、両方の列で `NULL` s を禁止します。 その後、`datetime`型の `CommentDate` という名前の列を追加します。 `NULL` s を禁止し、`CommentDate` 列の既定値を `getdate()`に設定します。

残っているのは、各ゲストブックコメントにユーザーアカウントを関連付ける列を追加することだけです。 1つの方法として、`nvarchar(256)`型の `UserName` という名前の列を追加する方法があります。 このオプションは、`SqlMembershipProvider`以外のメンバーシッププロバイダーを使用する場合に適しています。 ただし、このチュートリアルシリーズで説明しているように、`SqlMembershipProvider`を使用する場合、`aspnet_Users` テーブルの `UserName` 列は一意であるとは限りません。 `aspnet_Users` テーブルの主キーが `UserId` であり、`uniqueidentifier`型です。 したがって、`GuestbookComments` テーブルには `uniqueidentifier` 型の `UserId` という名前の列が必要です (`NULL` 値は禁止されています)。 この列を追加します。

> [!NOTE]
> SQL Server チュートリアルの[*メンバーシップスキーマの作成*](creating-the-membership-schema-in-sql-server-cs.md)に関するチュートリアルで説明したように、メンバーシップフレームワークは、異なるユーザーアカウントを持つ複数の web アプリケーションで同じユーザーストアを共有できるように設計されています。 これは、ユーザーアカウントを別のアプリケーションに分割することによって行われます。 また、各ユーザー名はアプリケーション内で一意であることが保証されていますが、同じユーザーストアを使用する異なるアプリケーションで同じユーザー名を使用することもできます。 `UserName` フィールドと `ApplicationId` フィールドの `aspnet_Users` テーブルには複合 `UNIQUE` 制約がありますが、`UserName` フィールドだけではありません。 このため、aspnet\_Users テーブルには、同じ `UserName` 値を持つ2つ (以上) のレコードを含めることができます。 ただし、`aspnet_Users` テーブルの `UserId` フィールドには `UNIQUE` 制約があります (これは主キーであるため)。 `UNIQUE` 制約は、`GuestbookComments` テーブルと `aspnet_Users` テーブルの間に外部キー制約を設定できないため、重要です。

`UserId` 列を追加したら、ツールバーの [保存] アイコンをクリックしてテーブルを保存します。 新しいテーブルに `GuestbookComments`という名前を指定します。

`GuestbookComments` テーブルを使用して1つの最後の問題が発生しました。 `GuestbookComments.UserId` 列と `aspnet_Users.UserId` 列の間に[外部キー制約](https://msdn.microsoft.com/library/ms175464.aspx)を作成する必要があります。 これを実現するには、ツールバーの [リレーションシップ] アイコンをクリックして、[外部キーのリレーションシップ] ダイアログボックスを開きます。 (または、[テーブルデザイナー] メニューの [リレーションシップ] をクリックして、このダイアログボックスを起動することもできます)。

[外部キーのリレーションシップ] ダイアログボックスの左下隅にある [追加] ボタンをクリックします。 これにより、新しい外部キー制約が追加されます。ただし、リレーションシップに参加するテーブルを定義する必要があります。

[[外部キーのリレーションシップ] ダイアログボックスを使用してテーブルの Foreign Key 制約を管理 ![には](storing-additional-user-information-cs/_static/image8.png)](storing-additional-user-information-cs/_static/image7.png)

**図 3**: [外部キーのリレーションシップ] ダイアログボックスを使用してテーブルの外部キー制約を管理する ([クリックしてフルサイズの画像を表示する](storing-additional-user-information-cs/_static/image9.png))

次に、右側の [テーブルと列の指定] 行にある省略記号アイコンをクリックします。 [テーブルと列] ダイアログボックスが表示されます。ここでは、主キーテーブルと列、および `GuestbookComments` テーブルの外部キー列を指定できます。 特に、[`aspnet_Users`] を選択し、主キーのテーブルと列として `UserId` を選択し、`GuestbookComments` テーブルから外部キー列として `UserId` します (図4を参照)。 主キーと外部キーのテーブルおよび列を定義したら、[OK] をクリックして [外部キーのリレーションシップ] ダイアログボックスに戻ります。

[aspnet_Users テーブルと GuesbookComments テーブルの間に外部キー制約を確立 ![には](storing-additional-user-information-cs/_static/image11.png)](storing-additional-user-information-cs/_static/image10.png)

**図 4**: `aspnet_Users` テーブルと `GuesbookComments` テーブルの間に外部キー制約を設定[する (クリックしてフルサイズの画像を表示する](storing-additional-user-information-cs/_static/image12.png))

この時点で、外部キー制約が確立されています。 この制約が存在することで、存在しないユーザーアカウントを参照するゲストブックエントリがないことを保証することで、2つのテーブル間の[リレーショナル整合性](http://en.wikipedia.org/wiki/Referential_integrity)が保証されます。 既定では、対応する子レコードがある場合、外部キー制約によって親レコードが削除されることは許可されません。 つまり、ユーザーが1つ以上のゲストブックコメントを作成した後、そのユーザーアカウントを削除しようとすると、そのユーザーのゲストブックコメントが最初に削除されない限り、削除は失敗します。

親レコードが削除されたときに、関連付けられている子レコードを自動的に削除するように、Foreign key 制約を構成できます。 言い換えると、この外部キー制約を設定して、ユーザーのユーザーアカウントが削除されたときにユーザーのゲストブックエントリが自動的に削除されるようにすることができます。 これを行うには、[挿入と更新の指定] セクションを展開し、[ルールの削除] プロパティを Cascade に設定します。

[外部キー制約を連鎖削除に構成 ![には](storing-additional-user-information-cs/_static/image14.png)](storing-additional-user-information-cs/_static/image13.png)

**図 5**: 外部キー制約を構成して削除を連鎖させる ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image15.png)されます)

外部キーの制約を保存するには、[閉じる] ボタンをクリックして外部キーのリレーションシップを終了します。 次に、ツールバーの [保存] アイコンをクリックして、テーブルとこのリレーションシップを保存します。

### <a name="storing-the-users-home-town-homepage-and-signature"></a>ユーザーの自宅、ホームページ、署名を保存する

`GuestbookComments` の表は、ユーザーアカウントと一対多のリレーションシップを共有する情報を格納する方法を示しています。 各ユーザーアカウントには任意の数のコメントが関連付けられている可能性があるため、このリレーションシップは、各コメントを特定のユーザーにリンクする列を含む一連のコメントを保持するテーブルを作成することによってモデル化されます。 `SqlMembershipProvider`を使用する場合は、`uniqueidentifier` 型の `UserId` という名前の列と、この列と `aspnet_Users.UserId`の間の foreign key 制約を作成することによって、このリンクを作成することをお勧めします。

ここで、3つの列を各ユーザーアカウントに関連付けて、ユーザーのホーム、ホームページ、署名を保存する必要があります。これは、ゲストブックのコメントに表示されます。 これを実現するには、さまざまな方法があります。

- <strong>`aspnet_Users`テーブル</strong><strong>または</strong><strong>`aspnet_Membership`</strong>テーブル<strong>に新しい列を追加</strong>し<strong>ます。</strong> `SqlMembershipProvider`によって使用されるスキーマを変更するため、この方法はお勧めしません。 この決定は、ましょうに戻ってくる可能性があります。 たとえば、ASP.NET の将来のバージョンで別の `SqlMembershipProvider` スキーマを使用している場合はどうなるでしょうか。 Microsoft には、ASP.NET 2.0 `SqlMembershipProvider` データを新しいスキーマに移行するためのツールが含まれている場合がありますが、ASP.NET 2.0 `SqlMembershipProvider` スキーマを変更した場合は、変換できないことがあります。

- **ASP を使用します。ホーム、ホームページ、署名のプロファイルプロパティを定義する NET の Profile framework。** ASP.NET には、追加のユーザー固有データを格納するように設計されたプロファイルフレームワークが含まれています。 メンバーシップフレームワークと同様に、プロファイルフレームワークはプロバイダーモデルの上に構築されます。 .NET Framework には、SQL Server データベースにプロファイルデータを格納する `SqlProfileProvider` が付属しています。 実際、データベースには、`SqlProfileProvider` (`aspnet_Profile`) によって使用されているテーブルが既に存在しています。これは<a id="_msoanchor_2"> </a>、 [*SQL Server チュートリアルでメンバーシップスキーマを作成*](creating-the-membership-schema-in-sql-server-cs.md)するときにアプリケーションサービスを追加したときに追加されたためです。   
  プロファイルフレームワークの主な利点は、開発者が `Web.config` のプロファイルプロパティを定義できることです。これにより、基になるデータストアとの間でプロファイルデータをシリアル化するためにコードを記述する必要がなくなります。 簡単に言えば、一連のプロファイルプロパティを定義し、コードで使用することは非常に簡単です。 ただし、バージョン管理に関しては、プロファイルシステムが必要になることはほとんどありません。そのため、新しいユーザー固有のプロパティを後で追加したり、既存のプロパティを削除または変更したりする必要があるアプリケーションがある場合、プロファイルフレームワークは次のようにならない可能性があります。 最適なオプション。 さらに、`SqlProfileProvider` は、プロファイルのプロパティを非常に非正規化された形式で保存し、プロファイルデータに対して直接クエリを実行することができないようにします (たとえば、ニューヨークの自宅の町を持つユーザーの数)。   
  プロファイルフレームワークの詳細については、このチュートリアルの最後にある「参考資料」セクションを参照してください。

- <strong>この3つの列をデータベースの新しいテーブルに追加し、このテーブルと`aspnet_Users`の間に一対一のリレーションシップを確立し</strong><strong>ます。</strong> この方法では、プロファイルフレームワークよりも少し作業が必要になりますが、データベース内で追加のユーザープロパティがどのようにモデル化されるかについて、最大限の柔軟性が提供されます。 これは、このチュートリアルで使用するオプションです。

ここでは、`UserProfiles` という名前の新しいテーブルを作成し、各ユーザーのホームの町、ホームページ、および署名を保存します。 データベースエクスプローラーウィンドウで [テーブル] フォルダーを右クリックし、[新しいテーブルの作成] を選択します。 最初の列に `UserId` 名前を指定し、その型を `uniqueidentifier`に設定します。 `NULL` 値を許可せずに、列を主キーとしてマークします。 次に、`nvarchar(50)`型の `HomeTown` という名前の列を追加します。`nvarchar(100)`型の `HomepageUrl``nvarchar(500)`型のシグネチャ。 これら3つの列はそれぞれ `NULL` 値を受け取ることができます。

[UserProfiles テーブルを作成 ![には](storing-additional-user-information-cs/_static/image17.png)](storing-additional-user-information-cs/_static/image16.png)

**図 6**: `UserProfiles` テーブルを作成[する (クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image18.png)されます)

テーブルを保存し、`UserProfiles`という名前を付けます。 最後に、`UserProfiles` テーブルの `UserId` フィールドと `aspnet_Users.UserId` フィールドの間に外部キー制約を設定します。 `GuestbookComments` テーブルと `aspnet_Users` テーブルの間の foreign key 制約を使用したのと同様に、この制約を連鎖削除する必要があります。 `UserProfiles` の `UserId` フィールドは主キーであるため、ユーザーアカウントごとに `UserProfiles` テーブルにレコードが1つだけ存在することになります。 この種類のリレーションシップは、一対一と呼ばれます。

データモデルを作成したので、これを使用する準備ができました。 手順2と3では、現在ログオンしているユーザーが自宅の町、ホームページ、および署名情報を表示および編集する方法を確認します。 手順 4. では、認証されたユーザーが新しいコメントをゲストブックに送信し、既存のものを表示するためのインターフェイスを作成します。

## <a name="step-2-displaying-the-users-home-town-homepage-and-signature"></a>手順 2: ユーザーの自宅、ホームページ、および署名を表示する

現在ログオンしているユーザーが自宅の町、ホームページ、および署名情報を表示および編集できるようにするには、さまざまな方法があります。 TextBox コントロールや Label コントロールを使用してユーザーインターフェイスを手動で作成することも、DetailsView コントロールなどのデータ Web コントロールのいずれかを使用することもできます。 データベース `SELECT` と `UPDATE` ステートメントを実行するには、ページの分離コードクラスに ADO.NET コードを記述するか、または SqlDataSource で宣言型のアプローチを使用します。 アプリケーションでは、階層型アーキテクチャを使用するのが理想的です。これは、ページの分離コードクラスからプログラムで呼び出すことも、ObjectDataSource コントロールを使用して宣言することもできます。

このチュートリアルシリーズではフォーム認証、承認、ユーザーアカウント、およびロールに焦点を当てているため、これらのさまざまなデータアクセスオプションの詳細については説明しません。また、SQL ステートメントを直接実行するよりも、階層型アーキテクチャが推奨される理由については説明しません。[ASP.NET] ページから開始します。 ここでは、DetailsView と SqlDataSource の使用方法を順を追って説明します。最も迅速で簡単なオプションですが、ここで説明する概念は、他の Web コントロールやデータアクセスロジックにも確実に適用できます。 ASP.NET でのデータの操作の詳細については、 *[ASP.NET 2.0 チュートリアルシリーズのデータの操作](../../data-access/index.md)* に関する記事を参照してください。

`Membership` フォルダーの [`AdditionalUserInfo.aspx`] ページを開き、[DetailsView] コントロールをページに追加します。その `ID` プロパティを `UserProfile` に設定し、その `Width` と `Height` のプロパティをオフにします。 DetailsView のスマートタグを展開し、新しいデータソースコントロールにバインドすることを選択します。 これにより、データソース構成ウィザードが起動します (図7を参照)。 最初の手順では、データソースの種類を指定するように求められます。 `SecurityTutorials` データベースに直接接続するため、[データベース] アイコンを選択し、`ID` を `UserProfileDataSource`として指定します。

[UserProfileDataSource という名前の新しい SqlDataSource コントロールを追加 ![には](storing-additional-user-information-cs/_static/image20.png)](storing-additional-user-information-cs/_static/image19.png)

**図 7**: `UserProfileDataSource` という名前の新しい SqlDataSource コントロールを追加[する (クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image21.png)される)

次の画面では、使用するデータベースを入力するように求められます。 `SecurityTutorials` データベースの `Web.config` には、既に接続文字列が定義されています。 この接続文字列名 (`SecurityTutorialsConnectionString`) は、ドロップダウンリストに表示されます。 このオプションを選択し、[次へ] をクリックします。

[![ドロップダウンリストから [SecurityTutorialsConnectionString] を選択します。](storing-additional-user-information-cs/_static/image23.png)](storing-additional-user-information-cs/_static/image22.png)

**図 8**: ドロップダウンリストから `SecurityTutorialsConnectionString` を選択する ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image24.png)されます)

次の画面では、クエリを実行するテーブルと列を指定するように求められます。 ドロップダウンリストから `UserProfiles` テーブルを選択し、すべての列を確認します。

[UserProfiles テーブルからすべての列を戻す ![には](storing-additional-user-information-cs/_static/image26.png)](storing-additional-user-information-cs/_static/image25.png)

**図 9**: `UserProfiles` テーブルのすべての列を元に戻す ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image27.png)されます)

図9の現在のクエリでは `UserProfiles`の*すべて*のレコードが返されますが、現在ログオンしているユーザーのレコードのみが対象となります。 `WHERE` 句を追加するには、[`WHERE`] ボタンをクリックして [`WHERE` 句の追加] ダイアログボックスを表示します (図10を参照)。 ここでは、フィルターを適用する列、演算子、およびフィルターパラメーターのソースを選択できます。 列として [`UserId`] を選択し、演算子として "=" を選択します。

残念ながら、現在ログオンしているユーザーの `UserId` 値を返す組み込みパラメーターソースはありません。 この値はプログラムによって取得する必要があります。 そのため、[ソース] ドロップダウンリストを "なし" に設定し、[追加] ボタンをクリックしてパラメーターを追加し、[OK] をクリックします。

[UserId 列にフィルターパラメーターを追加 ![には](storing-additional-user-information-cs/_static/image29.png)](storing-additional-user-information-cs/_static/image28.png)

**図 10**: `UserId` 列にフィルターパラメーターを追加する ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image30.png)されます)

[OK] をクリックすると、図9に示す画面に戻ります。 ただし、この時点では、画面の下部にある SQL クエリには `WHERE` 句が含まれている必要があります。 [次へ] をクリックして、[クエリのテスト] 画面に移動します。 ここでクエリを実行し、結果を確認できます。 [完了] をクリックしてウィザードを終了します。

データソース構成ウィザードを完了すると、ウィザードで指定した設定に基づいて SqlDataSource コントロールが作成されます。 さらに、SqlDataSource の `SelectCommand`によって返される各列の DetailsView には、手動で BoundFields を追加します。 ユーザーがこの値を知る必要がないため、DetailsView に `UserId` フィールドを表示する必要はありません。 このフィールドを DetailsView コントロールの宣言型マークアップから直接削除することも、スマートタグから [フィールドの編集] リンクをクリックして削除することもできます。

この時点で、ページの宣言型マークアップは次のようになります。

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample1.aspx)]

データを選択する前に、SqlDataSource コントロールの `UserId` パラメーターを、現在ログインしているユーザーの `UserId` にプログラムで設定する必要があります。 これは、SqlDataSource の `Selecting` イベントのイベントハンドラーを作成し、そこに次のコードを追加することで実現できます。

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample2.cs)]

上記のコードは、`Membership` クラスの `GetUser` メソッドを呼び出すことによって、現在ログオンしているユーザーへの参照を取得することから始まります。 これにより、`ProviderUserKey` プロパティに `UserId`が含まれている `MembershipUser` オブジェクトが返されます。 `UserId` 値が SqlDataSource の `@UserId` パラメーターに割り当てられます。

> [!NOTE]
> `Membership.GetUser()` メソッドは、現在ログオンしているユーザーに関する情報を返します。 匿名ユーザーがページにアクセスしている場合は、`null`の値が返されます。 このような場合、`ProviderUserKey` プロパティを読み取ろうとすると、次のコード行の `NullReferenceException` になります。 もちろん、`AdditionalUserInfo.aspx` ページで `null` 値を返す `Membership.GetUser()` について心配する必要はありません。これは、認証されたユーザーのみがこのフォルダー内の ASP.NET リソースにアクセスできるように、前のチュートリアルで URL 承認を構成したためです。 匿名アクセスが許可されているページで現在ログオンしているユーザーに関する情報にアクセスする必要がある場合は、プロパティを参照する前に、`GetUser()` メソッドから非`null MembershipUser` オブジェクトが返されることを必ず確認してください。

ブラウザーで [`AdditionalUserInfo.aspx`] ページにアクセスすると、`UserProfiles` テーブルに行を追加していないため、空白のページが表示されます。 手順 6. では、CreateUserWizard コントロールをカスタマイズして、新しいユーザーアカウントが作成されたときに新しい行が `UserProfiles` テーブルに自動的に追加されるようにする方法について説明します。 ただし、現時点では、テーブルにレコードを手動で作成する必要があります。

Visual Studio で データベースエクスプローラーに移動し、テーブル フォルダーを展開します。 `aspnet_Users` テーブルを右クリックし、[テーブルデータの表示] を選択して、テーブル内のレコードを表示します。`UserProfiles` テーブルに対しても同じ処理を行います。 図11は、上下に並べて表示される場合の結果を示しています。 私のデータベースでは、現在は `aspnet_Users` のレコードがありますが、`UserProfiles` テーブルにはレコードがありません。

[aspnet_Users および UserProfiles テーブルの内容が表示され ![](storing-additional-user-information-cs/_static/image32.png)](storing-additional-user-information-cs/_static/image31.png)

**図 11**: `aspnet_Users` テーブルと `UserProfiles` テーブルの内容が表示される ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image33.png)されます)

`HomeTown`、`HomepageUrl`、および `Signature` の各フィールドの値を手動で入力して、`UserProfiles` テーブルに新しいレコードを追加します。 新しい `UserProfiles` レコードで有効な `UserId` 値を取得する最も簡単な方法は、`aspnet_Users` テーブルの特定のユーザーアカウントから `UserId` フィールドを選択し、`UserId` の `UserProfiles`フィールドにコピーして貼り付けることです。 図12は、新しいレコードが追加された後の `UserProfiles` テーブルを示しています。

[ユーザープロファイルにレコードが追加された ![](storing-additional-user-information-cs/_static/image35.png)](storing-additional-user-information-cs/_static/image34.png)

**図 12**: `UserProfiles` にレコードが追加されました ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image36.png)されます)

[`AdditionalUserInfo.aspx`] ページに戻ります。 図13に示すように、この設定が表示されます。

[現在アクセスしているユーザーの設定が表示され ![](storing-additional-user-information-cs/_static/image38.png)](storing-additional-user-information-cs/_static/image37.png)

**図 13**: 現在アクセスしているユーザーに設定が表示される ([クリックしてフルサイズの画像を表示する](storing-additional-user-information-cs/_static/image39.png))

> [!NOTE]
> ここで、メンバーシップユーザーごとに `UserProfiles` テーブルにレコードを手動で追加します。 手順 6. では、CreateUserWizard コントロールをカスタマイズして、新しいユーザーアカウントが作成されたときに新しい行が `UserProfiles` テーブルに自動的に追加されるようにする方法について説明します。

## <a name="step-3-allowing-the-user-to-edit-his-home-town-homepage-and-signature"></a>手順 3: ユーザーが自分の自宅、ホームページ、および署名を編集できるようにする

この時点で、現在ログインしているユーザーはホームの町、ホームページ、および署名の設定を表示できますが、まだ変更することはできません。 データを編集できるように DetailsView コントロールを更新してみましょう。

最初に行う必要があるのは、実行する `UPDATE` ステートメントとそれに対応するパラメーターを指定して、SqlDataSource の `UpdateCommand` を追加することです。 SqlDataSource を選択し、プロパティウィンドウの [UpdateQuery] プロパティの横にある省略記号をクリックして、[コマンドおよびパラメーターエディター] ダイアログボックスを表示します。 次の `UPDATE` ステートメントをテキストボックスに入力します。

[!code-sql[Main](storing-additional-user-information-cs/samples/sample3.sql)]

次に、[パラメーターの更新] ボタンをクリックします。これにより、`UPDATE` ステートメントの各パラメーターについて、SqlDataSource コントロールの `UpdateParameters` コレクションにパラメーターが作成されます。 すべてのパラメーターのソースを None に設定し、[OK] ボタンをクリックしてダイアログボックスを完成させます。

[SqlDataSource の UpdateCommand と UpdateParameters を指定 ![には](storing-additional-user-information-cs/_static/image41.png)](storing-additional-user-information-cs/_static/image40.png)

**図 14**: SqlDataSource の `UpdateCommand` と `UpdateParameters` を指定[する (クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image42.png)されます)

SqlDataSource コントロールに加えられた追加により、DetailsView コントロールで編集がサポートされるようになりました。 DetailsView のスマートタグから、[編集を有効にする] チェックボックスをオンにします。 これにより、`ShowEditButton` プロパティが True に設定されたコントロールの `Fields` コレクションに CommandField が追加されます。 これにより、編集モードで DetailsView が読み取り専用モードで表示されている場合は [編集] ボタンが表示され、[更新] ボタンと [キャンセル] ボタンが表示されます。 ただし、ユーザーが [編集] をクリックする必要はありませんが、DetailsView コントロールの[`DefaultMode` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode.aspx)を `Edit`に設定することにより、detailsview を "常に編集可能" 状態にすることができます。

これらの変更により、DetailsView コントロールの宣言型マークアップは次のようになります。

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample4.aspx)]

CommandField と `DefaultMode` プロパティが追加されていることに注意してください。

ブラウザーでこのページをテストしてみましょう。 `UserProfiles`に対応するレコードを持つユーザーと一緒にアクセスすると、ユーザーの設定が編集可能なインターフェイスに表示されます。

[DetailsView が編集可能なインターフェイスをレンダリング ![](storing-additional-user-information-cs/_static/image44.png)](storing-additional-user-information-cs/_static/image43.png)

**図 15**: DetailsView によって編集可能なインターフェイスがレンダリングされる ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image45.png)されます)

値を変更し、[更新] ボタンをクリックします。 何も起こらないかのように見えます。 ポストバックがあり、値はデータベースに保存されますが、保存が発生したことを視覚的に示すフィードバックはありません。

これを解決するには、Visual Studio に戻り、DetailsView の上に Label コントロールを追加します。 `ID` を `SettingsUpdatedMessage`に設定し、その `Text` プロパティを「設定が更新されました」に設定し、`Visible` プロパティと `EnableViewState` プロパティを `false`に設定します。

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample5.aspx)]

DetailsView が更新されるたびに `SettingsUpdatedMessage` ラベルを表示する必要があります。 これを実現するには、DetailsView の `ItemUpdated` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample6.cs)]

ブラウザーを使用して `AdditionalUserInfo.aspx` ページに戻り、データを更新します。 今回は、役に立つステータスメッセージが表示されます。

[設定が更新されると、短いメッセージ ![表示されます。](storing-additional-user-information-cs/_static/image47.png)](storing-additional-user-information-cs/_static/image46.png)

**図 16**: 設定が更新されたときに短いメッセージが表示される ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image48.png)されます)

> [!NOTE]
> DetailsView コントロールの編集インターフェイスは、必要に応じて大きくなります。 標準サイズのテキストボックスを使用しますが、署名フィールドは複数行のテキストボックスにする必要があります。 RegularExpressionValidator を使用して、ホームページの URL が "http://" または "https://" で始まることを確認する必要があります。 さらに、DetailsView コントロールの `DefaultMode` プロパティは `Edit`に設定されているため、[キャンセル] ボタンでは何も実行されません。 削除するか、クリックしてユーザーを他のページ (`~/Default.aspx`など) にリダイレクトする必要があります。 これらの機能強化は、読者のための演習として残しておきます。

### <a name="adding-a-link-to-theadditionaluserinfoaspxpage-in-the-master-page"></a>マスターページの`AdditionalUserInfo.aspx`ページへのリンクの追加

現在、web サイトには `AdditionalUserInfo.aspx` ページへのリンクはありません。 このページに移動する唯一の方法は、ブラウザーのアドレスバーにページの URL を直接入力することです。 `Site.master` マスターページで、このページへのリンクを追加してみましょう。

マスターページには、認証された訪問者と匿名の訪問者の異なるマークアップを表示する、`LoginContent` ContentPlaceHolder の LoginView Web コントロールが含まれていることを思い出してください。 LoginView コントロールの `LoggedInTemplate` を更新して、`AdditionalUserInfo.aspx` ページへのリンクを含めます。 これらの変更を行った後、LoginView コントロールの宣言型マークアップは次のようになります。

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample7.aspx)]

`LoggedInTemplate`に `lnkUpdateSettings` ハイパーリンクコントロールが追加されていることに注意してください。 このリンクを使用すると、認証されたユーザーはページにすばやく移動して、自宅、ホームページ、および署名の設定を表示および変更できます。

## <a name="step-4-adding-new-guestbook-comments"></a>手順 4: 新しいゲストブックコメントを追加する

[`Guestbook.aspx`] ページでは、認証されたユーザーがゲストブックを表示し、コメントを残すことができます。 まず、新しいゲストブックコメントを追加するためのインターフェイスの作成について説明します。

Visual Studio の [`Guestbook.aspx`] ページを開き、2つのテキストボックスコントロールで構成されるユーザーインターフェイスを作成します。1つは新しいコメントの件名用、もう1つは本文用です。 最初のテキストボックスコントロールの `ID` プロパティを `Subject` に設定し、その `Columns` プロパティを40に設定します。2番目の `ID` を `Body`に、その `TextMode` を `MultiLine`に、`Width` プロパティと `Rows` プロパティをそれぞれ "95%" と8に設定します。 ユーザーインターフェイスを完成させるには、`PostCommentButton` という名前のボタン Web コントロールを追加し、その `Text` プロパティを「コメントの投稿」に設定します。

各ゲストブックのコメントには件名と本文が必要であるため、各テキストボックスに RequiredFieldValidator を追加します。 これらのコントロールの `ValidationGroup` プロパティを "EnterComment" に設定します。同様に、`PostCommentButton` コントロールの `ValidationGroup` プロパティを "EnterComment" に設定します。 ASP の詳細については、「」を参照してください。NET の検証コントロール、 [ASP.NET でのフォーム検証](http://www.4guysfromrolla.com/webtech/090200-1.shtml)の確認、 [ASP.NET 2.0 の検証コントロールの解説](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)、 [W3Schools](http://www.w3schools.com/)の[検証サーバーコントロールのチュートリアル](http://www.w3schools.com/aspnet/aspnet_refvalidationcontrols.asp)。

ユーザーインターフェイスを作成した後、ページの宣言型マークアップは次のようになります。

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample8.aspx)]

ユーザーインターフェイスが完成したら、次に、`PostCommentButton` をクリックしたときに `GuestbookComments` テーブルに新しいレコードを挿入します。 これはさまざまな方法で実現できます。ボタンの `Click` イベントハンドラーに ADO.NET コードを記述できます。SqlDataSource コントロールをページに追加し、その `InsertCommand`を構成した後、`Click` イベントハンドラーからその `Insert` メソッドを呼び出すことができます。または、新しいゲストブックコメントの挿入を担当する中間層を構築し、この機能を `Click` イベントハンドラーから呼び出すこともできます。 手順 3. で SqlDataSource を使用することを確認したので、ここでは ADO.NET コードを使用してみましょう。

> [!NOTE]
> Microsoft SQL Server データベースのデータにプログラムでアクセスするために使用される ADO.NET クラスは、`System.Data.SqlClient` 名前空間にあります。 この名前空間をページの分離コードクラス (`using System.Data.SqlClient;`) にインポートすることが必要になる場合があります。

`PostCommentButton`の `Click` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample9.cs)]

`Click` イベントハンドラーは、ユーザーが指定したデータが有効であることを確認することによって開始されます。 そうでない場合は、レコードを挿入する前にイベントハンドラーが終了します。 指定されたデータが有効であると仮定すると、現在ログオンしているユーザーの `UserId` 値が取得され、`currentUserId` ローカル変数に格納されます。 `GuestbookComments`にレコードを挿入するときに `UserId` 値を指定する必要があるため、この値が必要になります。

その後、`SecurityTutorials` データベースの接続文字列が `Web.config` から取得され、`INSERT` SQL ステートメントが指定されます。 次に、`SqlConnection` オブジェクトを作成して開きます。 次に、`SqlCommand` オブジェクトが構築され、`INSERT` クエリで使用されるパラメーターの値が割り当てられます。 次に、`INSERT` ステートメントが実行され、接続が閉じられます。 イベントハンドラーの最後に、ユーザーの値がポストバック全体で保持されないように、`Subject` と `Body` のテキストボックスの `Text` プロパティがクリアされます。

ブラウザーでこのページをテストしてみましょう。 このページは `Membership` フォルダーにあるため、匿名訪問者はアクセスできません。 そのため、最初にログオンする必要があります (まだインストールしていない場合)。 `Subject` と `Body` のテキストボックスに値を入力し、[`PostCommentButton`] ボタンをクリックします。 これにより、新しいレコードが `GuestbookComments`に追加されます。 ポストバック時に、指定した件名と本文がテキストボックスからワイプされます。

[`PostCommentButton`] ボタンをクリックした後、コメントがゲストブックに追加されたことを示す視覚的なフィードバックはありません。 このページを更新して、既存のゲストブックのコメントを表示する必要もあります。これは、手順 5. で行います。 これを完了すると、コメントの一覧に追加されたコメントが表示され、適切な視覚的なフィードバックが得られます。 ここでは、`GuestbookComments` テーブルの内容を調べて、ゲストブックコメントが保存されていることを確認します。

図17は、2つのコメントが残された後の `GuestbookComments` テーブルの内容を示しています。

[ゲストブックのコメントを GuestbookComments テーブルに表示する ![](storing-additional-user-information-cs/_static/image50.png)](storing-additional-user-information-cs/_static/image49.png)

**図 17**: `GuestbookComments` テーブルにゲストブックのコメントを表示する ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image51.png)されます)

> [!NOTE]
> 危険性のあるマークアップ (HTML – ASP.NET など) を含むゲストブックコメントをユーザーが挿入しようとすると、`HttpRequestValidationException`がスローされます。 この例外の詳細、スローされる理由、ユーザーが危険な可能性のある値を送信することを許可する方法については、「要求の検証に関する[ホワイトペーパー](../../../../whitepapers/request-validation.md)」を参照してください。

## <a name="step-5-listing-the-existing-guestbook-comments"></a>手順 5: 既存のゲストブックコメントを一覧表示する

コメントを残すだけでなく、`Guestbook.aspx` ページにアクセスするユーザーも、ゲストブックの既存のコメントを表示することができます。 これを実現するには、`CommentList` という名前の ListView コントロールをページの下部に追加します。

> [!NOTE]
> ListView コントロールは、ASP.NET バージョン3.5 の新しいバージョンです。 カスタマイズ可能で柔軟性の高いレイアウトで項目の一覧を表示するように設計されていますが、GridView などの組み込みの編集、挿入、削除、ページング、および並べ替えの機能も提供しています。 ASP.NET 2.0 を使用している場合は、代わりに DataList または Repeater コントロールを使用する必要があります。 ListView の使用方法の詳細については、 [Scott Guthrie](https://weblogs.asp.net/scottgu/)のブログエントリ、 [Asp: listview コントロール](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)、および記事「 [Listview コントロールでデータを表示](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)する」を参照してください。

ListView のスマートタグを開き、[データソースの選択] ドロップダウンリストから新しいデータソースにコントロールをバインドします。 手順 2. で見たように、これによりデータソース構成ウィザードが起動します。 データベースアイコンを選択し、結果の SqlDataSource `CommentsDataSource`という名前を指定して、[OK] をクリックします。 次に、ドロップダウンリストから `SecurityTutorialsConnectionString` 接続文字列を選択し、[次へ] をクリックします。

手順2のこの時点で、ドロップダウンリストから `UserProfiles` テーブルを選択し、返す列を選択することによって、クエリするデータを指定しました (図9を参照)。 ここでは、`GuestbookComments`からレコードだけでなく、コメンターのホーム、ホームページ、署名、およびユーザー名も返す SQL ステートメントを記述する必要があります。 そのため、[カスタム SQL ステートメントまたはストアドプロシージャを指定してください] オプションを選択し、[次へ] をクリックします。

これにより、"カスタムステートメントまたはストアドプロシージャの定義" 画面が表示されます。 [クエリビルダー] ボタンをクリックして、クエリをグラフィカルに作成します。 クエリビルダーは、まずクエリを実行するテーブルを指定するように求めるメッセージが表示されます。 `GuestbookComments`、`UserProfiles`、および `aspnet_Users` テーブルを選択し、[OK] をクリックします。 これにより、3つすべてのテーブルがデザイン画面に追加されます。 `GuestbookComments`、`UserProfiles`、および `aspnet_Users` テーブルの間には foreign key 制約があるため、これらのテーブルはクエリビルダーによって自動的に `JOIN` されます。

残っているのは、返される列を指定することだけです。 `GuestbookComments` テーブルから、`Subject`、`Body`、および `CommentDate` 列を選択します。`UserProfiles` テーブルから `HomeTown`、`HomepageUrl`、および `Signature` の各列を返します。`aspnet_Users`から `UserName` を返します。 また、`SELECT` クエリの末尾に "`ORDER BY CommentDate DESC`" を追加して、最新の投稿が最初に返されるようにします。 これらの選択を行った後、クエリビルダーインターフェイスは、図18のスクリーンショットのようになります。

[構築されたクエリが GuestbookComments、UserProfiles、aspnet_Users テーブルを結合 ![](storing-additional-user-information-cs/_static/image53.png)](storing-additional-user-information-cs/_static/image52.png)

**図 18**: 構築されたクエリは、`GuestbookComments`、`UserProfiles`、および `aspnet_Users` テーブルを `JOIN` します ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image54.png)されます)。

[OK] をクリックしてクエリビルダーウィンドウを閉じ、[カスタムステートメントまたはストアドプロシージャの定義] 画面に戻ります。 [次へ] をクリックして [クエリのテスト] 画面に進みます。この画面では、[クエリのテスト] ボタンをクリックしてクエリの結果を表示できます。 準備ができたら、[完了] をクリックして、データソースの構成ウィザードを完了します。

手順2でデータソースの構成ウィザードを完了すると、関連する DetailsView コントロールの `Fields` コレクションが更新され、`SelectCommand`によって返される各列の BoundField が含まれるようになりました。 ただし、ListView は変更されません。そのレイアウトを定義する必要もあります。 ListView のレイアウトは、宣言型マークアップまたはスマートタグの [ListView の構成] オプションを使用して手動で構築できます。 通常はマークアップを手動で定義することをお勧めしますが、最も自然な方法を使用します。

ここでは、ListView コントロールに対して、次の `LayoutTemplate`、`ItemTemplate`、および `ItemSeparatorTemplate` を使用しました。

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample10.aspx)]

`LayoutTemplate` は、コントロールによって出力されるマークアップを定義し、`ItemTemplate` は SqlDataSource によって返される各項目をレンダリングします。 `ItemTemplate`の結果のマークアップは、`LayoutTemplate`の `itemPlaceholder` コントロールに配置されます。 `itemPlaceholder`に加えて、`LayoutTemplate` には DataPager コントロールが含まれています。このコントロールでは、ListView が1ページあたり10個のゲストブックコメントのみを表示するように制限されており、ページングインターフェイスがレンダリングされます。

マイ `ItemTemplate` には、各ゲストブックコメントの件名が件名の下にある `<h4>` 要素に表示されます。 本文の表示に使用される構文は、`Eval("Body")` databinding ステートメントによって返されるデータを取得し、それを文字列に変換し、改行を `<br />` 要素に置き換えることに注意してください。 この変換は、HTML では空白が無視されるため、コメントの送信時に入力した改行を表示するために必要です。 ユーザーの署名は、本文の下に斜体で表示され、その後にユーザーの自宅の町、ホームページへのリンク、コメントが作成された日付と時刻、コメントを残した人物のユーザー名が表示されます。

ブラウザーでページを表示してみましょう。 ここに表示されている手順5のゲストブックに追加したコメントが表示されます。

[![のゲストブックのコメントが表示されるようになりました](storing-additional-user-information-cs/_static/image56.png)](storing-additional-user-information-cs/_static/image55.png)

**図 19**: `Guestbook.aspx` がゲストブックのコメントを表示[する (クリックしてフルサイズの画像を表示する](storing-additional-user-information-cs/_static/image57.png))

ゲストブックに新しいコメントを追加してみてください。 `PostCommentButton` ボタンをクリックすると、ページがポストバックされ、コメントがデータベースに追加されますが、ListView コントロールは新しいコメントを表示するように更新されません。 これは、次のいずれかの方法で修正できます。

- `PostCommentButton` ボタンの `Click` イベントハンドラーを更新して、データベースに新しいコメントを挿入した後に ListView コントロールの `DataBind()` メソッドを呼び出すようにします。
- ListView コントロールの `EnableViewState` プロパティを `false`に設定します。 この方法は、コントロールのビューステートを無効にすることで、すべてのポストバックで基になるデータに再バインドする必要があるため、機能します。

このチュートリアルでダウンロードできるチュートリアル web サイトには、両方の方法が示されています。 `false` する ListView コントロールの `EnableViewState` プロパティ、およびプログラムによって ListView にデータを再バインドするために必要なコードは `Click` イベントハンドラーに存在しますが、コメントアウトされています。

> [!NOTE]
> 現在、[`AdditionalUserInfo.aspx`] ページでは、ユーザーは自分の自宅、ホームページ、および署名の設定を表示および編集できます。 `AdditionalUserInfo.aspx` を更新して、ログインしているユーザーのゲストブックコメントを表示すると便利な場合があります。 つまり、ユーザーは自分の情報を確認して変更するだけでなく、[`AdditionalUserInfo.aspx`] ページにアクセスして、過去に行われたゲストブックのコメントを確認することもできます。 これは関心のある読者のための演習として残されています。

## <a name="step-6-customizing-the-createuserwizard-control-to-include-an-interface-for-the-home-town-homepage-and-signature"></a>手順 6: CreateUserWizard コントロールをカスタマイズして、自宅、ホームページ、および署名のインターフェイスを含める

`Guestbook.aspx` ページで使用される `SELECT` クエリでは、`INNER JOIN` を使用して、`GuestbookComments`、`UserProfiles`、および `aspnet_Users` テーブル間で関連レコードを結合します。 `UserProfiles` にレコードを持たないユーザーがゲストブックコメントを作成した場合、`INNER JOIN` は `UserProfiles` および `aspnet_Users`に一致するレコードがある場合にのみ `GuestbookComments` レコードを返すため、ListView にコメントは表示されません。 手順 3. で見たように、ユーザーがレコードを持っていない場合 `UserProfiles` `AdditionalUserInfo.aspx` ページで自分の設定を表示または編集することはできません。

言うまでもありませんが、設計上の決定により、メンバーシップシステムのすべてのユーザーアカウントには、`UserProfiles` テーブルに一致するレコードがあることが重要です。 CreateUserWizard を使用して新しいメンバーシップユーザーアカウントが作成されるたびに、対応するレコードが `UserProfiles` に追加されます。

「[*ユーザーアカウントの作成*](creating-user-accounts-cs.md)」チュートリアルで説明したように、新しいメンバーシップユーザーアカウントが作成されると、CreateUserWizard コントロールによって[`CreatedUser` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)が発生します。 このイベントのイベントハンドラーを作成し、作成したユーザーの UserId を取得して、`HomeTown`、`HomepageUrl`、および `Signature` 列の既定値を使用して `UserProfiles` テーブルにレコードを挿入できます。 さらに、追加のテキストボックスを含めるように CreateUserWizard コントロールのインターフェイスをカスタマイズすることで、ユーザーにこれらの値の入力を求めることができます。

まず、既定値を使用して、`CreatedUser` イベントハンドラーの `UserProfiles` テーブルに新しい行を追加する方法を見てみましょう。 その後、CreateUserWizard コントロールのユーザーインターフェイスをカスタマイズして、新しいユーザーのホームの町、ホームページ、および署名を収集するための追加のフォームフィールドを含める方法を説明します。

### <a name="adding-a-default-row-touserprofiles"></a>`UserProfiles` に既定の行を追加する

「[*ユーザーアカウントの作成*](creating-user-accounts-cs.md)」チュートリアルでは、`Membership` フォルダーの `CreatingUserAccounts.aspx` ページに CreateUserWizard コントロールを追加しました。 ユーザーアカウントの作成時に CreateUserWizard コントロールが `UserProfiles` テーブルにレコードを追加するには、CreateUserWizard コントロールの機能を更新する必要があります。 `CreatingUserAccounts.aspx` のページにこれらの変更を加えるのではなく、`EnhancedCreateUserWizard.aspx` のページに新しい CreateUserWizard コントロールを追加して、このチュートリアルの変更を加えてみましょう。

Visual Studio の [`EnhancedCreateUserWizard.aspx`] ページを開き、[ツールボックス] から CreateUserWizard コントロールをページにドラッグします。 CreateUserWizard コントロールの `ID` プロパティを `NewUserWizard`に設定します。 「 <a id="_msoanchor_5"> </a>[*ユーザーアカウントの作成*](creating-user-accounts-cs.md)」チュートリアルで説明したように、CreateUserWizard の既定のユーザーインターフェイスによって、ビジターに必要な情報が表示されます。 この情報が提供されると、コントロールは内部的にメンバーシップフレームワークに新しいユーザーアカウントを作成します。1行のコードを記述する必要はありません。

CreateUserWizard コントロールは、ワークフローの実行中に多数のイベントを発生させます。 ビジターが要求情報を提供してフォームを送信すると、CreateUserWizard コントロールは最初にその[`CreatingUser` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)を発生させます。 作成プロセス中に問題が発生した場合は、 [`CreateUserError` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx)が発生します。ただし、ユーザーが正常に作成された場合は、 [`CreatedUser` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)が発生します。 <a id="_msoanchor_6"> </a>「[*ユーザーアカウントの作成*](creating-user-accounts-cs.md)」チュートリアルでは、指定されたユーザー名に先頭または末尾のスペースが含まれておらず、ユーザー名がパスワードのどこにも表示されていないことを確認するために、`CreatingUser` イベントのイベントハンドラーを作成しました。

作成したばかりのユーザーの `UserProfiles` テーブルに行を追加するには、`CreatedUser` イベントのイベントハンドラーを作成する必要があります。 `CreatedUser` イベントが発生した時点までに、メンバーシップフレームワークでユーザーアカウントが既に作成されているため、アカウントの UserId 値を取得できます。

`NewUserWizard`の `CreatedUser` イベントのイベントハンドラーを作成し、次のコードを追加します。

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample11.cs)]

上記のコードでは、追加されたユーザーアカウントの UserId を取得します。 これを行うには、`Membership.GetUser(username)` メソッドを使用して特定のユーザーに関する情報を返し、次に `ProviderUserKey` プロパティを使用してユーザー Id を取得します。 CreateUserWizard コントロールにユーザーが入力したユーザー名は、 [`UserName` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)を介して使用できます。

次に、接続文字列が `Web.config` から取得され、`INSERT` ステートメントが指定されます。 必要な ADO.NET オブジェクトがインスタンス化され、コマンドが実行されます。 このコードは、`@HomeTown`、`@HomepageUrl`、および `@Signature` の各パラメーターに[`DBNull`](https://msdn.microsoft.com/library/system.dbnull.aspx)インスタンスを割り当てます。これらのパラメーターには、`NULL`、`HomeTown`、および `HomepageUrl`の各フィールドのデータベース `Signature` 値が挿入された場合の効果があります。

ブラウザーを使用して `EnhancedCreateUserWizard.aspx` のページにアクセスし、新しいユーザーアカウントを作成します。 その後、Visual Studio に戻り、`aspnet_Users` テーブルと `UserProfiles` テーブルの内容を確認します (図12に戻っています)。 `aspnet_Users` に新しいユーザーアカウントが表示され、対応する `UserProfiles` 行 (`HomeTown`、`HomepageUrl`、`Signature`の `NULL` 値) が表示されます。

[新しいユーザーアカウントと UserProfiles レコードが追加された ![](storing-additional-user-information-cs/_static/image59.png)](storing-additional-user-information-cs/_static/image58.png)

**図 20**: 新しいユーザーアカウントと `UserProfiles` レコードが追加されました ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image60.png)されます)

訪問者が新しいアカウント情報を入力し、[Create User] \ (ユーザーの作成 \) ボタンをクリックすると、ユーザーアカウントが作成され、`UserProfiles` テーブルに行が追加されます。 その後、CreateUserWizard に `CompleteWizardStep`が表示され、成功メッセージと [続行] ボタンが表示されます。 [続行] ボタンをクリックするとポストバックが発生しますが、操作は行われず、ユーザーは `EnhancedCreateUserWizard.aspx` ページにスタックしたままになります。

CreateUserWizard コントロールの[`ContinueDestinationPageUrl` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)を使用して [続行] ボタンをクリックしたときに、ユーザーを送信する URL を指定できます。 [`ContinueDestinationPageUrl`] プロパティを "~/メンバーシップ/Additionaluserinfo.aspx" に設定します。 これにより、新しいユーザーが `AdditionalUserInfo.aspx`し、設定を表示および更新できるようになります。

### <a name="customizing-the-createuserwizards-interface-to-prompt-for-the-new-users-home-town-homepage-and-signature"></a>CreateUserWizard のインターフェイスをカスタマイズして、新しいユーザーのホーム、ホームページ、署名を要求する

CreateUserWizard コントロールの既定のインターフェイスでは、ユーザー名、パスワード、電子メールなどのコアユーザーアカウント情報だけを収集する必要がある単純なアカウント作成シナリオに十分です。 では、アカウントの作成中に自宅の町、ホームページ、署名を入力するように求めるメッセージが表示されます。 CreateUserWizard コントロールのインターフェイスをカスタマイズしてサインアップ時に追加情報を収集することができます。この情報は、基になるデータベースに追加のレコードを挿入するために `CreatedUser` イベントハンドラーで使用される場合があります。

CreateUserWizard コントロールは、ページ開発者が一連の順序付けられた `WizardSteps`を定義できるコントロールである、ASP.NET Wizard コントロールを拡張します。 ウィザードコントロールは、アクティブなステップをレンダリングし、ビジターがこれらの手順を移動できるようにするナビゲーションインターフェイスを提供します。 ウィザードコントロールは、長いタスクをいくつかの簡単な手順に分割するのに最適です。 ウィザードコントロールの詳細については、「 [ASP.NET 2.0 ウィザードコントロールを使用したステップバイステップのユーザーインターフェイスの作成](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)」を参照してください。

CreateUserWizard コントロールの既定のマークアップは、`CreateUserWizardStep` と `CompleteWizardStep`の2つの `WizardSteps`を定義します。

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample12.aspx)]

最初の `WizardStep`、`CreateUserWizardStep`では、ユーザー名、パスワード、電子メールなどを要求するインターフェイスがレンダリングされます。 訪問者がこの情報を提供し、[Create User (ユーザーの作成)] をクリックすると、`CompleteWizardStep`が表示され、成功メッセージと [続行] ボタンが表示されます。

追加のフォームフィールドを含めるように CreateUserWizard コントロールのインターフェイスをカスタマイズするには、次の操作を行います。

- <strong>追加のユーザーインターフェイス要素が含まれるように、</strong> <strong>1 つまたは複数の新しい</strong><strong>`WizardStep`</strong>s を作成します。 新しい `WizardStep` を CreateUserWizard に追加するには、そのスマートタグから [`WizardSteps`の追加/削除] リンクをクリックして `WizardStep` コレクションエディターを起動します。 そこから、ウィザードの手順を追加、削除、または順序変更することができます。 このチュートリアルで使用する方法を次に示します。

- <strong>`CreateUserWizardStep`</strong>を<strong>編集可能な</strong><strong>`WizardStep`</strong>に変換<strong>します。</strong> これにより、`CreateUserWizardStep` が、`CreateUserWizardStep`のと一致するユーザーインターフェイスを定義するマークアップを持つ同等の `WizardStep` に置き換えられます。 `CreateUserWizardStep` を `WizardStep` に変換することによって、コントロールの位置を変更したり、このステップにユーザーインターフェイス要素を追加したりできます。 `CreateUserWizardStep` または `CompleteWizardStep` を編集可能な `WizardStep`に変換するには、コントロールのスマートタグから [ユーザーの作成手順をカスタマイズする] または [完了手順のカスタマイズ] リンクをクリックします。

- **上記の2つのオプションの組み合わせを使用します。**

注意すべき重要な点の1つは、CreateUserWizard コントロールが、`CreateUserWizardStep`内から [Create User] \ (ユーザーの作成 \) ボタンをクリックしたときに、ユーザーアカウントの作成プロセスを実行することです。 `CreateUserWizardStep` の後に `WizardStep` が追加されているかどうかは関係ありません。

追加のユーザー入力を収集するためにカスタム `WizardStep` を CreateUserWizard コントロールに追加する場合、カスタム `WizardStep` は `CreateUserWizardStep`の前または後に配置できます。 `CreateUserWizardStep` の前にある場合は、カスタム `WizardStep` から収集された追加のユーザー入力を `CreatedUser` イベントハンドラーで使用できます。 ただし、カスタム `WizardStep` が `CreateUserWizardStep` 後、カスタム `WizardStep` が表示されたときに、新しいユーザーアカウントが既に作成されており、`CreatedUser` イベントが既に発生しています。

図21は、追加された `WizardStep` が `CreateUserWizardStep`の前にある場合のワークフローを示しています。 追加のユーザー情報は `CreatedUser` イベントが発生した時点までに収集されているため、`CreatedUser` イベントハンドラーを更新してこれらの入力を取得し、`DBNull.Value`ではなく `INSERT` ステートメントのパラメーター値に使用するだけです。

[追加の WizardStep が Createuserwizardstep.contenttemplate はの前にある場合は、CreateUserWizard ワークフローを ![します。](storing-additional-user-information-cs/_static/image62.png)](storing-additional-user-information-cs/_static/image61.png)

**図 21**: `WizardStep` が `CreateUserWizardStep` の前にある場合 ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image63.png)されます)

ただし、`CreateUserWizardStep`の*後*にカスタム `WizardStep` が配置されている場合は、ユーザーが自宅の町、ホームページ、または署名を入力する前に、ユーザーアカウントの作成プロセスが実行されます。 このような場合、図22に示すように、ユーザーアカウントが作成された後に、この追加情報をデータベースに挿入する必要があります。

[Createuserwizardstep.contenttemplate はの後に追加の WizardStep があるときに CreateUserWizard ワークフローを ![します。](storing-additional-user-information-cs/_static/image65.png)](storing-additional-user-information-cs/_static/image64.png)

**図 22**: `CreateUserWizardStep` の後に追加の `WizardStep` が発生した場合の CreateUserWizard のワークフロー ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image66.png)されます)

図22に示すワークフローは、手順 2. が完了するまで、`UserProfiles` テーブルにレコードを挿入するのを待機します。 ただし、手順1の後にビジターがブラウザーを閉じると、ユーザーアカウントが作成されたが、`UserProfiles`にレコードが追加されなかったという状態になります。 回避策の1つとして、`NULL` または既定値を持つレコードを `CreatedUser` イベントハンドラー (手順1の後に発生する) の `UserProfiles` に挿入して、手順 2. の完了後にこのレコードを更新します。 これにより、ユーザーが途中で登録プロセスを終了した場合でも、ユーザーアカウントの `UserProfiles` レコードが確実に追加されます。

このチュートリアルでは、`CreateUserWizardStep` の後、`CompleteWizardStep`の前に発生する新しい `WizardStep` を作成します。 まず、WizardStep を設定して構成してから、コードを見てみましょう。

CreateUserWizard コントロールのスマートタグから、[`WizardStep` の追加と削除] を選択すると、[`WizardStep` コレクションエディター] ダイアログが表示されます。 新しい `WizardStep`を追加し、その `ID` を `UserSettings`に設定します。その `Title` を "your Settings" に設定し、`StepType` を `Step`に設定します。 次に、図23に示すように、`CreateUserWizardStep` ("新しいアカウントにサインアップする") の後、`CompleteWizardStep` ("Complete") の前に来るように配置します。

[新しい WizardStep を CreateUserWizard コントロールに追加 ![には](storing-additional-user-information-cs/_static/image68.png)](storing-additional-user-information-cs/_static/image67.png)

**図 23**: CreateUserWizard コントロールに新しい `WizardStep` を追加する ([クリックすると、フルサイズの画像が表示](storing-additional-user-information-cs/_static/image69.png)されます)

[OK] をクリックして [`WizardStep` コレクションエディター] ダイアログボックスを閉じます。 新しい `WizardStep` は、CreateUserWizard コントロールによって更新された宣言型マークアップによって、次のようになります。

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample13.aspx)]

新しい `<asp:WizardStep>` 要素に注意してください。 ここでは、新しいユーザーのホームホーム、ホームページ、および署名を収集するために、ユーザーインターフェイスを追加する必要があります。 このコンテンツは、宣言構文またはデザイナーを使用して入力できます。 デザイナーを使用するには、スマートタグのドロップダウンリストから [自分の設定] ステップを選択して、デザイナーの手順を確認します。

> [!NOTE]
> スマートタグのドロップダウンリストからステップを選択すると、CreateUserWizard コントロールの[`ActiveStepIndex` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.activestepindex.aspx)が更新されます。このプロパティは、開始ステップのインデックスを指定します。 このため、このドロップダウンリストを使用してデザイナーの "自分の設定" 手順を編集する場合は、ユーザーが最初に `EnhancedCreateUserWizard.aspx` ページにアクセスしたときにこの手順が表示されるように、必ず [新しいアカウントにサインアップする] に設定してください。

`HomeTown`、`HomepageUrl`、`Signature`という3つのテキストボックスコントロールが含まれている [設定] ステップ内にユーザーインターフェイスを作成します。 このインターフェイスを構築した後、CreateUserWizard の宣言型マークアップは次のようになります。

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample14.aspx)]

ブラウザーを使用してこのページにアクセスし、新しいユーザーアカウントを作成して、ホーム、ホームページ、署名の値を指定します。 `CreateUserWizardStep` 完了すると、メンバーシップフレームワークにユーザーアカウントが作成され、`CreatedUser` イベントハンドラーが実行されます。これにより `UserProfiles`に新しい行が追加されますが、`HomeTown`、`HomepageUrl`、`Signature`のデータベース `NULL` 値が使用されます。 ホームの町、ホームページ、および署名に入力した値は使用されません。 この結果、`HomeTown`、`HomepageUrl`、および `Signature` のフィールドが指定されていない `UserProfiles` レコードを持つ新しいユーザーアカウントが作成されます。

ユーザーによって入力されたホームの町、honepage、および署名の値を取得する "your Settings" 手順の後にコードを実行し、適切な `UserProfiles` レコードを更新する必要があります。 ユーザーがウィザードコントロールのステップの間を移動するたびに、ウィザードの[`ActiveStepChanged` イベント](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.activestepchanged.aspx)が発生します。 このイベントのイベントハンドラーを作成し、"設定" 手順が完了したら、`UserProfiles` テーブルを更新できます。

CreateUserWizard の `ActiveStepChanged` イベントのイベントハンドラーを追加し、次のコードを追加します。

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample15.cs)]

上記のコードは、"Complete" 手順に到達したかどうかを判断することから始まります。 "完了" の手順は、"設定" の手順の直後に実行されるので、訪問者が "完了" の手順に達したときに、彼女が "自分の設定" 手順を完了したことを意味します。

このような場合は、`UserSettings WizardStep`内のテキストボックスコントロールをプログラムで参照する必要があります。 これを行うには、まず `FindControl` メソッドを使用してプログラムで `UserSettings WizardStep`を参照し、次に `WizardStep`内からテキストボックスを参照します。 テキストボックスが参照されたら、`UPDATE` ステートメントを実行する準備ができました。 `UPDATE` ステートメントには、`CreatedUser` イベントハンドラーの `INSERT` ステートメントと同じ数のパラメーターがありますが、ここでは、ユーザーによって指定されたホームの町、ホームページ、および署名の値を使用します。

このイベントハンドラーを配置したら、ブラウザーを使用して `EnhancedCreateUserWizard.aspx` のページにアクセスし、ホーム、ホームページ、および署名の値を指定する新しいユーザーアカウントを作成します。 新しいアカウントを作成した後、[`AdditionalUserInfo.aspx`] ページにリダイレクトされます。ここには、入力した自宅の町、ホームページ、および署名情報が表示されます。

> [!NOTE]
> Web サイトには、現在、訪問者が新しいアカウントを作成するための2つのページ (`CreatingUserAccounts.aspx` と `EnhancedCreateUserWizard.aspx`) があります。 Web サイトのサイトマップとログインページは `CreatingUserAccounts.aspx` ページを指していますが、[`CreatingUserAccounts.aspx`] ページでは、ユーザーに自宅の住所、ホームページ、および署名情報の入力を求めるメッセージは表示されず、対応する行は `UserProfiles`に追加されません。 したがって、この機能を提供するように `CreatingUserAccounts.aspx` ページを更新するか、`CreatingUserAccounts.aspx`ではなく `EnhancedCreateUserWizard.aspx` を参照するように sitemap と login ページを更新してください。 後者のオプションを選択した場合は、匿名ユーザーが `EnhancedCreateUserWizard.aspx` ページにアクセスできるように、`Membership` フォルダーの `Web.config` ファイルを必ず更新してください。

## <a name="summary"></a>要約

このチュートリアルでは、メンバーシップフレームワーク内のユーザーアカウントに関連するデータをモデル化するための手法について説明しました。 特に、一対多のリレーションシップをユーザーアカウントと共有するエンティティと、一対一のリレーションシップを共有するデータをモデル化することを検討しました。 さらに、この関連情報を表示、挿入、更新する方法についても説明しました。ここでは、SqlDataSource コントロールを使用した例と ADO.NET コードを使用したその他の例を紹介します。

このチュートリアルでは、ユーザーアカウントの概要について説明します。 次のチュートリアルでは、ロールに注目します。 次のいくつかのチュートリアルでは、ロールフレームワークについて説明します。新しいロールを作成する方法、ユーザーにロールを割り当てる方法、ユーザーが属するロールを確認する方法、およびロールベースの承認を適用する方法について説明します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>関連項目

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ASP.NET 2.0 でのデータへのアクセスと更新](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 2.0 ウィザードコントロール](https://weblogs.asp.net/scottgu/archive/2006/02/21/438732.aspx)
- [ASP.NET 2.0 Wizard コントロールを使用したステップバイステップのユーザーインターフェイスの作成](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [カスタム DataSource コントロールパラメーターの作成](http://aspnet.4guysfromrolla.com/articles/110106-1.aspx)
- [CreateUserWizard コントロールのカスタマイズ](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)
- [DetailsView コントロールのクイックスタート](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/detailsview.aspx)
- [ListView コントロールを使用したデータの表示](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [ASP.NET 2.0 の検証コントロールの解説](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)
- [データの挿入と削除の編集](../../data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)
- [ASP.NET でのフォームの検証](http://www.4guysfromrolla.com/webtech/090200-1.shtml)
- [カスタムユーザー登録情報を収集しています](https://weblogs.asp.net/scottgu/archive/2006/07/05/Tip_2F00_Trick_3A00_-Gathering-Custom-User-Registration-Information.aspx)
- [ASP.NET 2.0 のプロファイル](http://www.odetocode.com/Articles/440.aspx)
- [Asp: ListView コントロール](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)
- [ユーザープロファイルのクイックスタート](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/profile/default.aspx)

### <a name="about-the-author"></a>作成者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は、 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com)またはブログで[http://ScottOnWriting.NET](http://scottonwriting.net/)にアクセスできます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 今後の MSDN 記事を確認することに興味がありますか? その場合は、 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)の行を削除します。

> [!div class="step-by-step"]
> [前へ](user-based-authorization-cs.md)
> [次へ](creating-the-membership-schema-in-sql-server-vb.md)

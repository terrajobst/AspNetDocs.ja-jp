---
uid: identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
title: メンバーシップとユーザープロファイルのユニバーサルプロバイダーデータを ASP.NET Identity (C#)-ASP.NET 4.x に移行する
author: rustd
description: このチュートリアルでは、既存のアプリのユニバーサルプロバイダーを使用して作成されたユーザーとロールのデータとユーザープロファイルデータを移行するために必要な手順について説明します...
ms.author: riande
ms.date: 12/13/2013
ms.custom: seoapril2019
ms.assetid: 2e260430-d13c-4658-bd05-e256fc0d63b8
msc.legacyurl: /identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 31f02a0cec3c531c45c37b7aad8456e01e80b5ea
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499774"
---
# <a name="migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity-c"></a>メンバーシップとユーザー プロファイルのユニバーサル プロバイダー データを ASP.NET Identity に移行する (C#)

[Pranav Rastogi](https://github.com/rustd)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Robert mcmurray](https://github.com/rmcmurray)、 [suhas Joshi](https://github.com/suhasj)

> このチュートリアルでは、既存のアプリケーションのユニバーサルプロバイダーを使用して作成されたユーザーとロールのデータおよびユーザープロファイルデータを ASP.NET Identity モデルに移行するために必要な手順について説明します。 ここで説明する方法を使用して、ユーザープロファイルデータを移行することもできます。

Visual Studio 2013 のリリースでは、ASP.NET チームによって新しい ASP.NET Identity システムが導入されました。このリリースの詳細については、[こちら](../../index.md)を参照してください。 この記事では、 [SQL メンバーシップから新しい id システムに](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)web アプリケーションを移行する方法について説明します。この記事では、ユーザーとロールの管理のためにプロバイダーモデルに従っている既存のアプリケーションを新しい id モデルに移行する手順について説明します。 このチュートリアルでは、主にユーザープロファイルデータを移行して、新しいシステムにシームレスにフックする方法について説明します。 ユーザーとロールの情報の移行は、SQL メンバーシップに似ています。 プロファイルデータを移行するためのアプローチは、SQL メンバーシップを持つアプリケーションでも使用できます。

例として、プロバイダーモデルを使用する Visual Studio 2012 を使用して作成された web アプリから始めます。 次に、プロファイル管理用のコードを追加し、ユーザーを登録して、ユーザーのプロファイルデータを追加し、データベーススキーマを移行します。次に、ユーザーとロールの管理に Id システムを使用するようにアプリケーションを変更します。 移行のテストとして、ユニバーサルプロバイダーを使用して作成されたユーザーはログインして、新しいユーザーが登録できるようにする必要があります。

> [!NOTE]
> 完全なサンプルについては、 [https://github.com/suhasj/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations)を参照してください。

## <a name="profile-data-migration-summary"></a>プロファイルデータ移行の概要

移行を開始する前に、プロファイルデータをプロバイダーモデルに格納する操作を見てみましょう。 アプリケーションユーザーのプロファイルデータは、複数の方法で格納できます。多くの場合、ユニバーサルプロバイダーと共に出荷された組み込みのプロファイルプロバイダーを使用します。 手順は次のとおりです。

1. プロファイルデータを格納するために使用されるプロパティを持つクラスを追加します。
2. ' ProfileBase ' を拡張し、メソッドを実装してユーザーの上記のプロファイルデータを取得するクラスを追加します。
3. *Web.config ファイルで*既定のプロファイルプロバイダーを使用できるようにし、プロファイル情報へのアクセスに使用される手順 #2 で宣言されたクラスを定義します。

プロファイル情報は、シリアル化された xml およびバイナリデータとしてデータベースの "Profiles" テーブルに格納されます。

新しい ASP.NET Identity システムを使用するようにアプリケーションを移行すると、プロファイル情報が逆シリアル化され、ユーザークラスのプロパティとして格納されます。 各プロパティは、ユーザーテーブルの列にマップできます。 ここでの利点は、アクセスするたびにデータ情報をシリアル化または逆シリアル化する必要がないだけでなく、ユーザークラスを使用して直接プロパティを操作できることです。

## <a name="getting-started"></a>作業の開始

1. Visual Studio 2012 で新しい ASP.NET 4.5 Web フォームアプリケーションを作成します。 現在のサンプルでは、Web フォームテンプレートを使用しますが、MVC アプリケーションを使用することもできます。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.jpg)
2. プロファイル情報を格納するための新しいフォルダー ' モデル ' を作成します  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.png)
3. 例として、ユーザーの生年月日、市区町村、高さ、および重量をプロファイルに格納します。 高さと重みは、"ユーザーの統計情報" と呼ばれるカスタムクラスとして格納されます。 プロファイルを格納および取得するには、"ProfileBase" を拡張するクラスが必要です。 プロファイル情報を取得して格納するための新しいクラス ' AppProfile ' を作成してみましょう。

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample1.cs)]
4. *Web.config ファイルで*プロファイルを有効にします。 手順 #3 で作成したユーザー情報を格納または取得するために使用するクラス名を入力します。

    [!code-xml[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample2.xml)]
5. [アカウント] フォルダーに web フォームページを追加して、ユーザーからプロファイルデータを取得して保存します。 プロジェクトを右クリックし、[新しい項目の追加] を選択します。 マスターページ ' AddProfileData .aspx ' を含む新しい webforms ページを追加します。 ' MainContent ' セクションに次の内容をコピーします。

    [!code-html[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample3.html)]

   分離コードに次のコードを追加します。

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample4.cs)]

   AppProfile クラスが定義されている名前空間を追加して、コンパイルエラーを削除します。
6. アプリを実行し、ユーザー名が "**olduser"** の新しいユーザーを作成します。 [AddProfileData] ページに移動し、ユーザーのプロファイル情報を追加します。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.png)

[サーバーエクスプローラー] ウィンドウを使用して、データがシリアル化された xml として [プロファイル] テーブルに格納されていることを確認できます。 Visual Studio の [表示] メニューで、[サーバーエクスプローラー] を選択します。 *Web.config ファイルで*定義されているデータベースのデータ接続が存在する必要があります。 データ接続をクリックすると、異なるサブカテゴリが表示されます。 [テーブル] を展開してデータベース内のさまざまなテーブルを表示し、[プロファイル] を右クリックして、[テーブルデータの表示] を選択し、プロファイルテーブルに格納されているプロファイルデータを表示します。

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.png)

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image4.png)

## <a name="migrating-database-schema"></a>データベーススキーマの移行

既存のデータベースが Id システムで動作するようにするには、元のデータベースに追加したフィールドをサポートするように、Id データベースのスキーマを更新する必要があります。 これを行うには、SQL スクリプトを使用して新しいテーブルを作成し、既存の情報をコピーします。 [サーバーエクスプローラー] ウィンドウで、[DefaultConnection] を展開してテーブルを表示します。 [テーブル] を右クリックし、[新しいクエリ] を選択します。

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image5.png)

SQL スクリプトを[https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt)から貼り付けて実行します。 ' DefaultConnection ' が更新された場合は、新しいテーブルが追加されていることがわかります。 テーブル内のデータをチェックして、情報が移行されたことを確認できます。

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image6.png)

## <a name="migrating-the-application-to-use-aspnet-identity"></a>ASP.NET Identity を使用するためのアプリケーションの移行

1. ASP.NET Identity に必要な Nuget パッケージをインストールします。

    - Microsoft.AspNet.Identity.EntityFramework
    - Microsoft.AspNet.Identity.Owin
    - Microsoft.Owin.Host.SystemWeb
    - Owin (Microsoft. Security)
    - Microsoft.Owin.Security.Google
    - Microsoft.Owin.Security.MicrosoftAccount
    - Microsoft.Owin.Security.Twitter

   Nuget パッケージの管理の詳細については、こちらを参照して[ください](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)。
2. テーブル内の既存のデータを操作するには、テーブルにマップし直して Id システムにフックするモデルクラスを作成する必要があります。 Id コントラクトの一部として、モデルクラスは、Identity. Core dll で定義されているインターフェイスを実装するか、またはこれらのインターフェイスの既存の実装を拡張して使用できます。 ロール、ユーザーログイン、およびユーザー要求には、既存のクラスを使用します。 このサンプルでは、カスタムユーザーを使用する必要があります。 プロジェクトを右クリックして、新しいフォルダー ' ' の作成 ' を作成します。 次に示すように、新しい ' User ' クラスを追加します。

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample5.cs)]

   ' ProfileInfo ' が user クラスのプロパティになっていることに注意してください。 そのため、ユーザークラスを使用してプロファイルデータを直接操作できます。

**Id およびアカウント**フォルダー内**のファイル**をダウンロードソース ( [https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) ) からコピーします。 これらには、残りのモデルクラスと、ASP.NET Identity Api を使用したユーザーとロールの管理に必要な新しいページがあります。 使用される方法は SQL のメンバーシップに似ており、詳細な説明については[こちら](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)を参照してください。

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

## <a name="copying-profile-data-to-the-new-tables"></a>プロファイルデータを新しいテーブルにコピーする

前述のように、プロファイルテーブルの xml データを逆シリアル化し、AspNetUsers テーブルの列に格納する必要があります。 前の手順でユーザーテーブルに新しい列が作成されているので、これらの列に必要なデータを設定します。 これを行うには、コンソールアプリケーションを使用します。このアプリケーションは、ユーザーテーブルに新しく作成された列を設定するために1回実行されます。

1. 既存のソリューションに新しいコンソールアプリケーションを作成します。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.jpg)
2. Entity Framework パッケージの最新バージョンをインストールします。
3. 上で作成した web アプリケーションをコンソールアプリケーションへの参照として追加します。 これを行うには、[プロジェクト]、[参照の追加]、[ソリューション] の順にクリックし、プロジェクトをクリックして、[OK] をクリックします。
4. 次のコードを Program.cs クラスにコピーします。 このロジックは、各ユーザーのプロファイルデータを読み取り、それを ' ProfileInfo ' オブジェクトとしてシリアル化して、データベースに保存します。

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample6.cs)]

   使用されるモデルの一部は、web アプリケーションプロジェクトの ' ユーザーモデル ' フォルダーで定義されているため、対応する名前空間を含める必要があります。
5. 上記のコードは、前の手順で作成した web アプリケーションプロジェクトの App\_Data フォルダー内のデータベースファイルで動作します。 これを参照するには、コンソールアプリケーションの app.config ファイル内の接続文字列を、web アプリケーションの web.config の接続文字列で更新します。 また、' AttachDbFilename ' プロパティに完全な物理パスを指定します。
6. コマンドプロンプトを開き、上のコンソールアプリケーションの bin フォルダーに移動します。 次の図に示すように、実行可能ファイルを実行し、ログ出力を確認します。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.jpg)
7. サーバーエクスプローラーの ' AspNetUsers ' テーブルを開き、プロパティが格納されている新しい列のデータを確認します。 これらは、対応するプロパティ値で更新する必要があります。

## <a name="verify-functionality"></a>機能の確認

ASP.NET Identity を使用して実装された新しく追加されたメンバーシップページを使用して、古いデータベースからユーザーをログインします。 ユーザーは、同じ資格情報を使用してログインできる必要があります。 OAuth の追加、新しいユーザーの作成、パスワードの変更、ロールの追加、ロールへのユーザーの追加など、他の機能を試してみてください。

古いユーザーと新しいユーザーのプロファイルデータを取得して、users テーブルに保存する必要があります。 古いテーブルは参照できなくなります。

## <a name="conclusion"></a>まとめ

この記事では、ASP.NET Identity のメンバーシップのためにプロバイダーモデルを使用した web アプリケーションの移行プロセスについて説明しています。 この記事では、ユーザーが Id システムにフックするためのプロファイルデータの移行についても説明しています。 アプリを移行するときに発生する質問や問題については、以下のコメントを残してください。

*記事を確認するための Rick Anderson と Robert McMurray に感謝します。*

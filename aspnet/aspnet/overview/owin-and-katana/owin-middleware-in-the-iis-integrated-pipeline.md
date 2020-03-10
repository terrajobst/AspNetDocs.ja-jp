---
uid: aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
title: IIS 統合パイプラインの OWIN ミドルウェア |Microsoft Docs
author: Praburaj
description: この記事では、IIS 統合パイプラインで OWIN ミドルウェアコンポーネント (OMCs) を実行する方法と、OMCS を実行するパイプラインイベントを設定する方法について説明します。 ...
ms.author: riande
ms.date: 11/07/2013
ms.assetid: d031c021-33c2-45a5-bf9f-98f8fa78c2ab
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
msc.type: authoredcontent
ms.openlocfilehash: 7d157fb6bd9e2ae9b55af41ef06c1eb5e6310ce1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500260"
---
# <a name="owin-middleware-in-the-iis-integrated-pipeline"></a>IIS 統合パイプラインの OWIN ミドルウェア

[Praburaj Thiagarajan](https://github.com/Praburaj)、 [Rick Anderson](https://twitter.com/RickAndMSFT)

> この記事では、IIS 統合パイプラインで OWIN ミドルウェアコンポーネント (OMCs) を実行する方法と、OMCS を実行するパイプラインイベントを設定する方法について説明します。 このチュートリアルを読む前に、Project Katana と[OWIN Startup クラスの検出](owin-startup-class-detection.md)[の概要](an-overview-of-project-katana.md)を確認する必要があります。 このチュートリアルは、Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )、Chris Ross、Praburaj Thiagarajan、Howard Dierking ( [@howard\_Dierking](https://twitter.com/howard_dierking) ) によって作成されました。

[OWIN](an-overview-of-project-katana.md)ミドルウェアコンポーネント (omcs) は、主にサーバーに依存しないパイプラインで実行されるように設計されていますが、IIS 統合パイプラインで omcs を実行することもできます (**クラシックモードはサポートされて*いません*** )。 パッケージマネージャーコンソール (PMC) から次のパッケージをインストールすることによって、IIS 統合パイプラインで OMC を機能させることができます。

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample1.cmd)]

つまり、IIS と System.web の外部で実行できないアプリケーションフレームワークも含めて、既存の OWIN ミドルウェアコンポーネントの恩恵を受けることができます。 

> [!NOTE]
> Visual Studio 2013 の新しい Id システムに付属するすべての `Microsoft.Owin.Security.*` パッケージ (たとえば、Cookie、Microsoft アカウント、Google、Facebook、Twitter、[ベアラートークン](http://self-issued.info/docs/draft-ietf-oauth-v2-bearer.html)、OAuth、Authorization SERVER、JWT、Azure Active Directory、active directory フェデレーションサービスなど) は omcs として作成され、自己ホスト型および IIS ホスト型の両方のシナリオで使用できます。

## <a name="how-owin-middleware-executes-in-the-iis-integrated-pipeline"></a>IIS 統合パイプラインで OWIN ミドルウェアを実行する方法

OWIN コンソールアプリケーションでは、[スタートアップ構成](owin-startup-class-detection.md)を使用して構築されたアプリケーションパイプラインは、`IAppBuilder.Use` メソッドを使用して、コンポーネントが追加される順序によって設定されます。 つまり、 [Katana](an-overview-of-project-katana.md)ランタイムの OWIN パイプラインは、`IAppBuilder.Use`を使用して登録された順序で omcs を処理します。 IIS 統合パイプラインでは、要求パイプラインは、 [BeginRequest](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx)、 [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)、 [AuthorizeRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)などのパイプラインイベントの定義済みセットをサブスクライブしている[HttpModules](https://msdn.microsoft.com/library/ms178468(v=vs.85).aspx)で構成されます。

OMC を ASP.NET 世界の[HttpModule](https://msdn.microsoft.com/library/zec9k340(v=vs.85).aspx)のものと比較する場合は、omc を適切な定義済みのパイプラインイベントに登録する必要があります。 たとえば、パイプラインの[AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)ステージに要求が送られたときに、HttpModule `MyModule` が呼び出されます。

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample2.cs?highlight=10)]

OMC を同じイベントベースの実行順序に参加させるために、 [Katana](an-overview-of-project-katana.md)ランタイムコードは[スタートアップ構成](owin-startup-class-detection.md)をスキャンし、各ミドルウェアコンポーネントを統合パイプラインイベントにサブスクライブします。 たとえば、次の OMC と登録コードを使用すると、ミドルウェアコンポーネントの既定のイベント登録を確認できます。 (OWIN startup クラスを作成する方法の詳細については、「 [OWIN Startup クラスの検出](owin-startup-class-detection.md)」を参照してください)。

1. 空の web アプリケーションプロジェクトを作成し、 **owin2**という名前を指定します。
2. パッケージマネージャーコンソール (PMC) から、次のコマンドを実行します。 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample3.cmd)]
3. `OWIN Startup Class` を追加し、`Startup`という名前を指定します。 生成されたコードを次のコードに置き換えます (変更は強調表示されています)。  

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample4.cs?highlight=5-7,15-36)]
4. F5 キーを押してアプリを実行します。

スタートアップ構成では、3つのミドルウェアコンポーネント (最初の2つは診断情報を表示し、最後の2つは診断情報を表示します) を含むパイプラインを設定します。 `PrintCurrentIntegratedPipelineStage` メソッドは、このミドルウェアが呼び出された統合パイプラインイベントとメッセージを表示します。 出力ウィンドウには次の内容が表示されます。

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample5.cmd)]

Katana ランタイムは、OWIN ミドルウェアの各コンポーネントを既定で[Preexecuter](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)にマップします。これは、IIS パイプラインイベント[PreRequestHandlerExecute](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)に対応します。

## <a name="stage-markers"></a>ステージマーカー

`IAppBuilder UseStageMarker()` 拡張メソッドを使用して、OMCs をパイプラインの特定の段階で実行するようにマークすることができます。 特定のステージ中に一連のミドルウェアコンポーネントを実行するには、登録時に最後のコンポーネントが設定された直後にステージマーカーを挿入します。 ミドルウェアを実行できるパイプラインのステージと、命令コンポーネントを実行する必要があるパイプラインのルールがあります (ルールについては、このチュートリアルの後半で説明します)。 次に示すように、`UseStageMarker` メソッドを `Configuration` コードに追加します。

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample6.cs?highlight=13,19)]

`app.UseStageMarker(PipelineStage.Authenticate)` の呼び出しによって、以前に登録されたすべてのミドルウェアコンポーネント (この場合は、2つの診断コンポーネント) がパイプラインの認証ステージで実行されるように構成されます。 最後のミドルウェアコンポーネント (診断を表示して要求に応答) は、`ResolveCache` 段階 ( [ResolveRequestCache](https://msdn.microsoft.com/library/system.web.httpapplication.resolverequestcache.aspx)イベント) で実行されます。

F5 キーを押してアプリを実行します。出力ウィンドウには次のように表示されます。

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample7.cmd)]

## <a name="stage-marker-rules"></a>ステージマーカーのルール

Owin ミドルウェアコンポーネント (OMC) は、次の OWIN パイプラインステージイベントで実行するように構成できます。

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample8.cs)]

1. 既定では、OMCs は最後のイベント (`PreHandlerExecute`) で実行されます。 このため、最初の例のコードは "PreExecuteRequestHandler" と表示されています。
2. `PipelineStage` 列挙型に示されている OWIN パイプラインの任意のステージで、`app.UseStageMarker` メソッドを使用して OMC を登録し、前に実行することができます。
3. OWIN パイプラインと IIS パイプラインが順序付けられているため、`app.UseStageMarker` への呼び出しは順番に行う必要があります。 に登録されている最後のイベントの前にあるイベントにイベントハンドラーを設定することはできません `app.UseStageMarker`します。 たとえば、を呼び出し*た後*、次のようになります。

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample9.cmd)]

   `Authenticate` または `PostAuthenticate` を渡す `app.UseStageMarker` の呼び出しは受け入れられず、例外はスローされません。 OMCs は、既定では `PreHandlerExecute`である、最新のステージで実行されます。 ステージマーカーは、前の手順で実行するために使用されます。 ステージマーカーを順序どおりに指定しなかった場合は、前のマーカーに丸められます。 つまり、ステージマーカーを追加すると、"stage X より後に実行する" と表示されます。 OMC は、OWIN パイプラインで追加された最初のステージマーカーの後に実行されます。
4. `app.UseStageMarker` を呼び出すための最も早い段階では、が優先されます。 たとえば、前の例の `app.UseStageMarker` 呼び出しの順序を切り替える場合は次のようになります。

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample10.cs?highlight=13,19)]

   出力ウィンドウに次の内容が表示されます。 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample11.cmd)]

   OMCs はすべて `AuthenticateRequest` ステージで実行されます。これは、`Authenticate` イベントに登録された最後の OMCS で、`Authenticate` イベントが他のすべてのイベントの前になるためです。

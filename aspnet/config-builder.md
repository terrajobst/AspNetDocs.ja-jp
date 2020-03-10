---
uid: config-builder
title: ASP.NET の構成ビルダー
author: rick-anderson
description: 外部ソースからの web.config 値以外のソースから構成データを取得する方法について説明します。
ms.author: riande
ms.date: 10/29/2018
msc.type: content
ms.openlocfilehash: 5299d9ab057c3096773955a7461e77a80673ebfe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472306"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="97d10-103">ASP.NET の構成ビルダー</span><span class="sxs-lookup"><span data-stu-id="97d10-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="97d10-104">[Stephen Molloy](https://github.com/StephenMolloy)と[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="97d10-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="97d10-105">構成ビルダーは、ASP.NET アプリが外部ソースから構成値を取得するための最新のアジャイルメカニズムを備えています。</span><span class="sxs-lookup"><span data-stu-id="97d10-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="97d10-106">構成ビルダー:</span><span class="sxs-lookup"><span data-stu-id="97d10-106">Configuration builders:</span></span>

* <span data-ttu-id="97d10-107">は .NET Framework 4.7.1 以降で使用できます。</span><span class="sxs-lookup"><span data-stu-id="97d10-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="97d10-108">構成値を読み取るための柔軟なメカニズムを提供します。</span><span class="sxs-lookup"><span data-stu-id="97d10-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="97d10-109">アプリがコンテナーおよびクラウドに重点を置いた環境に移行する際の基本的なニーズに対処します。</span><span class="sxs-lookup"><span data-stu-id="97d10-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="97d10-110">を使用すると、.NET 構成システムで以前に使用できないソース (Azure Key Vault や環境変数など) から描画することによって、構成データの保護を向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="97d10-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="97d10-111">キー/値構成ビルダー</span><span class="sxs-lookup"><span data-stu-id="97d10-111">Key/value configuration builders</span></span>

<span data-ttu-id="97d10-112">構成ビルダーで処理できる一般的なシナリオは、キー/値パターンに従う構成セクションの基本的なキー/値置換機構を提供することです。</span><span class="sxs-lookup"><span data-stu-id="97d10-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="97d10-113">ConfigurationBuilders の .NET Framework 概念は、特定の構成セクションまたはパターンに限定されません。</span><span class="sxs-lookup"><span data-stu-id="97d10-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="97d10-114">ただし、`Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders)、 [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) の構成ビルダーの多くは、キー/値パターン内で動作します。</span><span class="sxs-lookup"><span data-stu-id="97d10-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="97d10-115">キー/値構成ビルダーの設定</span><span class="sxs-lookup"><span data-stu-id="97d10-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="97d10-116">次の設定は、`Microsoft.Configuration.ConfigurationBuilders`のすべてのキー/値構成ビルダーに適用されます。</span><span class="sxs-lookup"><span data-stu-id="97d10-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="97d10-117">モード</span><span class="sxs-lookup"><span data-stu-id="97d10-117">Mode</span></span>

<span data-ttu-id="97d10-118">構成ビルダーは、キー/値情報の外部ソースを使用して、構成システムの選択したキー/値要素を設定します。</span><span class="sxs-lookup"><span data-stu-id="97d10-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="97d10-119">具体的には、`<appSettings/>` セクションと `<connectionStrings/>` セクションは、構成ビルダーから特別な処理を受けます。</span><span class="sxs-lookup"><span data-stu-id="97d10-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="97d10-120">ビルダーは、次の3つのモードで動作します。</span><span class="sxs-lookup"><span data-stu-id="97d10-120">The builders work in three modes:</span></span>

* <span data-ttu-id="97d10-121">`Strict`-既定のモード。</span><span class="sxs-lookup"><span data-stu-id="97d10-121">`Strict` - The default mode.</span></span> <span data-ttu-id="97d10-122">このモードでは、構成ビルダーは既知のキー/値中心の構成セクションでのみ動作します。</span><span class="sxs-lookup"><span data-stu-id="97d10-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> <span data-ttu-id="97d10-123">`Strict` モードでは、セクション内の各キーが列挙されます。</span><span class="sxs-lookup"><span data-stu-id="97d10-123">`Strict` mode enumerates each key in the section.</span></span> <span data-ttu-id="97d10-124">一致するキーが外部ソースで見つかった場合は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="97d10-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="97d10-125">構成ビルダーは、結果として得られる構成セクションの値を外部ソースの値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="97d10-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* <span data-ttu-id="97d10-126">`Greedy`-このモードは `Strict` モードと密接に関係しています。</span><span class="sxs-lookup"><span data-stu-id="97d10-126">`Greedy` - This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="97d10-127">元の構成に既に存在するキーに限定されるわけではありません。</span><span class="sxs-lookup"><span data-stu-id="97d10-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="97d10-128">構成ビルダーは、外部ソースからのすべてのキーと値のペアを、結果の構成セクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="97d10-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* <span data-ttu-id="97d10-129">`Expand`-構成セクションオブジェクトに解析される前に、未加工の XML に対して動作します。</span><span class="sxs-lookup"><span data-stu-id="97d10-129">`Expand` - Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="97d10-130">文字列内のトークンの拡張と考えることができます。</span><span class="sxs-lookup"><span data-stu-id="97d10-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="97d10-131">`${token}` パターンに一致する未加工の XML 文字列の一部は、トークンの展開の候補です。</span><span class="sxs-lookup"><span data-stu-id="97d10-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="97d10-132">対応する値が外部ソースに見つからない場合、トークンは変更されません。</span><span class="sxs-lookup"><span data-stu-id="97d10-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="97d10-133">このモードのビルダーは、`<appSettings/>` および `<connectionStrings/>` のセクションに限定されていません。</span><span class="sxs-lookup"><span data-stu-id="97d10-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="97d10-134">Web.config の次のマークアップ*により、* `Strict` モードでの環境[configbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/)が有効になります。</span><span class="sxs-lookup"><span data-stu-id="97d10-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="97d10-135">次のコードは、前の*web.config*ファイルに示されている `<appSettings/>` と `<connectionStrings/>` を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="97d10-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="97d10-136">上記のコードでは、プロパティ値を次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="97d10-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="97d10-137">キーが環境変数に設定されていない場合*は、web.config ファイル内*の値。</span><span class="sxs-lookup"><span data-stu-id="97d10-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="97d10-138">環境変数の値 (設定されている場合)。</span><span class="sxs-lookup"><span data-stu-id="97d10-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="97d10-139">たとえば、`ServiceID` には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="97d10-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="97d10-140">環境変数 `ServiceID` が設定されていない場合は、"ServiceID の値を web.config" で指定します。</span><span class="sxs-lookup"><span data-stu-id="97d10-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="97d10-141">`ServiceID` 環境変数の値 (設定されている場合)。</span><span class="sxs-lookup"><span data-stu-id="97d10-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="97d10-142">次の図は、環境エディターで設定された上記の web.config ファイルの `<appSettings/>` キー/値を示して*い*ます。</span><span class="sxs-lookup"><span data-stu-id="97d10-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![環境エディター](config-builder/static/env.png)

<span data-ttu-id="97d10-144">メモ: 環境変数の変更を確認するには、Visual Studio を終了して再起動することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="97d10-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="97d10-145">プレフィックスの処理</span><span class="sxs-lookup"><span data-stu-id="97d10-145">Prefix handling</span></span>

<span data-ttu-id="97d10-146">キープレフィックスを使用すると、次の理由でキーの設定を簡略化できます。</span><span class="sxs-lookup"><span data-stu-id="97d10-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="97d10-147">.NET Framework 構成は複雑で、入れ子になっています。</span><span class="sxs-lookup"><span data-stu-id="97d10-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="97d10-148">外部キー/値ソースは、一般に基本的なものであり、本質的にフラットです。</span><span class="sxs-lookup"><span data-stu-id="97d10-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="97d10-149">たとえば、環境変数は入れ子になっていません。</span><span class="sxs-lookup"><span data-stu-id="97d10-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="97d10-150">次のいずれかの方法を使用して、`<appSettings/>` と `<connectionStrings/>` を環境変数を介して構成に挿入します。</span><span class="sxs-lookup"><span data-stu-id="97d10-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="97d10-151">既定の `Strict` モードの `EnvironmentConfigBuilder`、および構成ファイル内の適切なキー名。</span><span class="sxs-lookup"><span data-stu-id="97d10-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="97d10-152">上記のコードとマークアップは、この方法を採用しています。</span><span class="sxs-lookup"><span data-stu-id="97d10-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="97d10-153">この方法を使用すると、`<appSettings/>` と `<connectionStrings/>`の両方で同じ名前のキーを持つことはでき**ません**。</span><span class="sxs-lookup"><span data-stu-id="97d10-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="97d10-154">異なるプレフィックスと `stripPrefix`を使用して、`Greedy` モードで2つの `EnvironmentConfigBuilder`s を使用します。</span><span class="sxs-lookup"><span data-stu-id="97d10-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="97d10-155">この方法では、構成ファイルを更新しなくても、アプリは `<appSettings/>` と `<connectionStrings/>` を読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="97d10-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="97d10-156">次の[セクションでは、この](#stripprefix)方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="97d10-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="97d10-157">異なるプレフィックスを使用して、`Greedy` モードで2つの `EnvironmentConfigBuilder`s を使用します。</span><span class="sxs-lookup"><span data-stu-id="97d10-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="97d10-158">この方法では、キー名がプレフィックスによって異なる必要があるため、キー名を重複させることはできません。</span><span class="sxs-lookup"><span data-stu-id="97d10-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="97d10-159">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="97d10-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="97d10-160">上記のマークアップでは、同じフラットキー/値ソースを使用して、2つの異なるセクションの構成を設定できます。</span><span class="sxs-lookup"><span data-stu-id="97d10-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="97d10-161">次の図は、環境エディターで設定された上記の web.config ファイルの `<appSettings/>` と `<connectionStrings/>` のキーと値を示して*い*ます。</span><span class="sxs-lookup"><span data-stu-id="97d10-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![環境エディター](config-builder/static/prefix.png)

<span data-ttu-id="97d10-163">次のコードは、前の*web.config*ファイルに格納されている `<appSettings/>` と `<connectionStrings/>` のキーと値を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="97d10-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="97d10-164">上記のコードでは、プロパティ値を次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="97d10-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="97d10-165">キーが環境変数に設定されていない場合*は、web.config ファイル内*の値。</span><span class="sxs-lookup"><span data-stu-id="97d10-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="97d10-166">環境変数の値 (設定されている場合)。</span><span class="sxs-lookup"><span data-stu-id="97d10-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="97d10-167">たとえば、前の*web.config*ファイル、前の環境エディターイメージのキー/値、前のコードを使用すると、次の値が設定されます。</span><span class="sxs-lookup"><span data-stu-id="97d10-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="97d10-168">Key</span><span class="sxs-lookup"><span data-stu-id="97d10-168">Key</span></span>              | <span data-ttu-id="97d10-169">値</span><span class="sxs-lookup"><span data-stu-id="97d10-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="97d10-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="97d10-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="97d10-171">Env 変数からの AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="97d10-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="97d10-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="97d10-172">AppSetting_default</span></span>            | <span data-ttu-id="97d10-173">Env からの値の AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="97d10-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="97d10-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="97d10-174">ConnStr_default</span></span>         | <span data-ttu-id="97d10-175">Env からの ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="97d10-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="97d10-176">ストライプの Pprefix</span><span class="sxs-lookup"><span data-stu-id="97d10-176">stripPrefix</span></span>

<span data-ttu-id="97d10-177">`stripPrefix`: boolean、既定値は `false`です。</span><span class="sxs-lookup"><span data-stu-id="97d10-177">`stripPrefix`: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="97d10-178">上記の XML マークアップは、アプリケーション設定を接続文字列から分離しますが、指定されたプレフィックスを使用する*には、web.config ファイル内*のすべてのキーが必要です。</span><span class="sxs-lookup"><span data-stu-id="97d10-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="97d10-179">たとえば、プレフィックス `AppSetting` を `ServiceID` キー ("AppSetting_ServiceID") に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="97d10-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="97d10-180">`stripPrefix`では、プレフィックスは*web.config ファイルで*は使用されません。</span><span class="sxs-lookup"><span data-stu-id="97d10-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="97d10-181">プレフィックスは、構成ビルダーのソース (環境など) で必要です。ほとんどの開発者は `stripPrefix`を使用することを想定しています。</span><span class="sxs-lookup"><span data-stu-id="97d10-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="97d10-182">アプリケーションは通常、プレフィックスを削除します。</span><span class="sxs-lookup"><span data-stu-id="97d10-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="97d10-183">*次の web.config は*プレフィックスを取り除きます。</span><span class="sxs-lookup"><span data-stu-id="97d10-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="97d10-184">上記の*web.config*ファイルでは、`default` キーは `<appSettings/>` と `<connectionStrings/>`の両方にあります。</span><span class="sxs-lookup"><span data-stu-id="97d10-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="97d10-185">次の図は、環境エディターで設定された上記の web.config ファイルの `<appSettings/>` と `<connectionStrings/>` のキーと値を示して*い*ます。</span><span class="sxs-lookup"><span data-stu-id="97d10-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![環境エディター](config-builder/static/prefix.png)

<span data-ttu-id="97d10-187">次のコードは、前の*web.config*ファイルに格納されている `<appSettings/>` と `<connectionStrings/>` のキーと値を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="97d10-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="97d10-188">上記のコードでは、プロパティ値を次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="97d10-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="97d10-189">キーが環境変数に設定されていない場合*は、web.config ファイル内*の値。</span><span class="sxs-lookup"><span data-stu-id="97d10-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="97d10-190">環境変数の値 (設定されている場合)。</span><span class="sxs-lookup"><span data-stu-id="97d10-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="97d10-191">たとえば、前の*web.config*ファイル、前の環境エディターイメージのキー/値、前のコードを使用すると、次の値が設定されます。</span><span class="sxs-lookup"><span data-stu-id="97d10-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="97d10-192">Key</span><span class="sxs-lookup"><span data-stu-id="97d10-192">Key</span></span>              | <span data-ttu-id="97d10-193">値</span><span class="sxs-lookup"><span data-stu-id="97d10-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="97d10-194">ServiceID</span><span class="sxs-lookup"><span data-stu-id="97d10-194">ServiceID</span></span>           | <span data-ttu-id="97d10-195">Env 変数からの AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="97d10-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="97d10-196">既定値 (default)</span><span class="sxs-lookup"><span data-stu-id="97d10-196">default</span></span>            | <span data-ttu-id="97d10-197">Env からの値の AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="97d10-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="97d10-198">既定値 (default)</span><span class="sxs-lookup"><span data-stu-id="97d10-198">default</span></span>         | <span data-ttu-id="97d10-199">Env からの ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="97d10-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="97d10-200">tokenPattern</span><span class="sxs-lookup"><span data-stu-id="97d10-200">tokenPattern</span></span>

<span data-ttu-id="97d10-201">`tokenPattern`: String、既定値は `@"\$\{(\w+)\}"`</span><span class="sxs-lookup"><span data-stu-id="97d10-201">`tokenPattern`: String, defaults to `@"\$\{(\w+)\}"`</span></span>

<span data-ttu-id="97d10-202">ビルダーの `Expand` 動作は、未加工の XML で `${token}`のようなトークンを検索します。</span><span class="sxs-lookup"><span data-stu-id="97d10-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="97d10-203">検索は、既定の正規表現 `@"\$\{(\w+)\}"`を使用して行われます。</span><span class="sxs-lookup"><span data-stu-id="97d10-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="97d10-204">`\w` に一致する文字のセットは、XML よりも厳密であり、多くの構成ソースで許可されます。</span><span class="sxs-lookup"><span data-stu-id="97d10-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="97d10-205">トークン名に `@"\$\{(\w+)\}"` よりも多くの文字が必要な場合は、`tokenPattern` を使用します。</span><span class="sxs-lookup"><span data-stu-id="97d10-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

<span data-ttu-id="97d10-206">`tokenPattern`: 文字列:</span><span class="sxs-lookup"><span data-stu-id="97d10-206">`tokenPattern`: String:</span></span>

* <span data-ttu-id="97d10-207">開発者がトークン照合に使用される regex を変更できるようにします。</span><span class="sxs-lookup"><span data-stu-id="97d10-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="97d10-208">適切な形式の非危険な regex であることを確認するための検証は行われません。</span><span class="sxs-lookup"><span data-stu-id="97d10-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="97d10-209">キャプチャグループが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="97d10-209">It must contain a capture group.</span></span> <span data-ttu-id="97d10-210">Regex 全体がトークン全体と一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="97d10-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="97d10-211">最初のキャプチャは、構成ソース内で検索するトークン名にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="97d10-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="97d10-212">Microsoft. Configuration. ConfigurationBuilders の構成ビルダー</span><span class="sxs-lookup"><span data-stu-id="97d10-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="97d10-213">環境 Configbuilder</span><span class="sxs-lookup"><span data-stu-id="97d10-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="97d10-214">環境[Configbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span><span class="sxs-lookup"><span data-stu-id="97d10-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="97d10-215">は、最も単純な構成ビルダーです。</span><span class="sxs-lookup"><span data-stu-id="97d10-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="97d10-216">環境から値を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="97d10-216">Reads values from the environment.</span></span>
* <span data-ttu-id="97d10-217">には、追加の構成オプションはありません。</span><span class="sxs-lookup"><span data-stu-id="97d10-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="97d10-218">`name` 属性値は任意です。</span><span class="sxs-lookup"><span data-stu-id="97d10-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="97d10-219">**注:** Windows コンテナー環境では、実行時に設定される変数は EntryPoint プロセス環境にのみ挿入されます。</span><span class="sxs-lookup"><span data-stu-id="97d10-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="97d10-220">サービスとして実行されるアプリまたはエントリポイント以外のプロセスは、コンテナー内のメカニズムによって挿入されない限り、これらの変数を取得しません。</span><span class="sxs-lookup"><span data-stu-id="97d10-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="97d10-221">[IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)ベースのコンテナーの場合、 [ServiceMonitor](https://github.com/Microsoft/iis-docker/pull/41)の現在のバージョンは、この処理を*DefaultAppPool*でのみ処理します。</span><span class="sxs-lookup"><span data-stu-id="97d10-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="97d10-222">その他の Windows ベースのコンテナーバリアントでは、エントリポイント以外のプロセス用に独自の挿入機構を開発することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="97d10-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="97d10-223">UserSecretsConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="97d10-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="97d10-224">パスワード、機密性の高い接続文字列、またはその他の機密データをソースコードに格納しないでください。</span><span class="sxs-lookup"><span data-stu-id="97d10-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="97d10-225">運用シークレットは、開発またはテストには使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="97d10-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="97d10-226">この構成ビルダーには、 [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets)と同様の機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="97d10-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="97d10-227">[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/)は .NET Framework プロジェクトで使用できますが、シークレットファイルを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="97d10-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="97d10-228">または、プロジェクトファイルの `UserSecretsId` プロパティを定義し、読み取り用の正しい場所に生のシークレットファイルを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="97d10-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="97d10-229">外部の依存関係をプロジェクトから除外するために、シークレットファイルは XML 形式になっています。</span><span class="sxs-lookup"><span data-stu-id="97d10-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="97d10-230">XML の書式設定は実装の詳細であり、形式に依存することはできません。</span><span class="sxs-lookup"><span data-stu-id="97d10-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="97d10-231">.NET Core プロジェクトでシークレットの*json*ファイルを共有する必要がある場合は、 [Simplejsonconfigbuilder](#simplejsonconfigbuilder)の使用を検討してください。</span><span class="sxs-lookup"><span data-stu-id="97d10-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span></span> <span data-ttu-id="97d10-232">.NET Core の `SimpleJsonConfigBuilder` 形式は、変更される可能性のある実装の詳細についても考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="97d10-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="97d10-233">`UserSecretsConfigBuilder`の構成属性:</span><span class="sxs-lookup"><span data-stu-id="97d10-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* <span data-ttu-id="97d10-234">`userSecretsId`-これは、XML シークレットファイルを識別するために推奨される方法です。</span><span class="sxs-lookup"><span data-stu-id="97d10-234">`userSecretsId` - This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="97d10-235">これは、`UserSecretsId` プロジェクトプロパティを使用してこの識別子を格納する .NET Core に似ています。</span><span class="sxs-lookup"><span data-stu-id="97d10-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="97d10-236">文字列は一意である必要があります。 GUID である必要はありません。</span><span class="sxs-lookup"><span data-stu-id="97d10-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="97d10-237">この属性を使用すると、`UserSecretsConfigBuilder` は、この識別子に属するシークレットファイルの既知のローカルの場所 (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) を検索します。</span><span class="sxs-lookup"><span data-stu-id="97d10-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* <span data-ttu-id="97d10-238">`userSecretsFile`-シークレットを含むファイルを指定する省略可能な属性です。</span><span class="sxs-lookup"><span data-stu-id="97d10-238">`userSecretsFile` - An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="97d10-239">`~` 文字は、アプリケーションルートを参照するために開始時に使用できます。</span><span class="sxs-lookup"><span data-stu-id="97d10-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="97d10-240">この属性または `userSecretsId` 属性のいずれかが必要です。</span><span class="sxs-lookup"><span data-stu-id="97d10-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="97d10-241">両方を指定した場合、`userSecretsFile` が優先されます。</span><span class="sxs-lookup"><span data-stu-id="97d10-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* <span data-ttu-id="97d10-242">`optional`: ブール値、既定値 `true`-シークレットファイルが見つからない場合、例外が発生しないようにします。</span><span class="sxs-lookup"><span data-stu-id="97d10-242">`optional`: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="97d10-243">`name` 属性値は任意です。</span><span class="sxs-lookup"><span data-stu-id="97d10-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="97d10-244">シークレットファイルの形式は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="97d10-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="97d10-245">AzureKeyVaultConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="97d10-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="97d10-246">[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/)は、 [Azure Key Vault](/azure/key-vault/key-vault-whatis)に格納されている値を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="97d10-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

<span data-ttu-id="97d10-247">`vaultName` が必要です (資格情報コンテナーの名前または資格情報コンテナーへの URI)。</span><span class="sxs-lookup"><span data-stu-id="97d10-247">`vaultName` is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="97d10-248">他の属性では、接続先のコンテナーを制御できますが、`Microsoft.Azure.Services.AppAuthentication`で動作する環境でアプリケーションが実行されていない場合にのみ必要です。</span><span class="sxs-lookup"><span data-stu-id="97d10-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="97d10-249">Azure サービス認証ライブラリは、可能であれば、実行環境から接続情報を自動的に取得するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="97d10-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="97d10-250">接続文字列を指定することで、接続情報を自動的に取得することができます。</span><span class="sxs-lookup"><span data-stu-id="97d10-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* <span data-ttu-id="97d10-251">`vaultName`-`uri` が指定されていない場合に必要です。</span><span class="sxs-lookup"><span data-stu-id="97d10-251">`vaultName` - Required if `uri` in not provided.</span></span> <span data-ttu-id="97d10-252">キーと値のペアの読み取りに使用する Azure サブスクリプション内のコンテナーの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="97d10-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* <span data-ttu-id="97d10-253">`connectionString`- [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)によって使用可能な接続文字列</span><span class="sxs-lookup"><span data-stu-id="97d10-253">`connectionString` - A connection string usable by [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)</span></span>
* <span data-ttu-id="97d10-254">`uri`-指定した `uri` 値を使用して他の Key Vault プロバイダーに接続します。</span><span class="sxs-lookup"><span data-stu-id="97d10-254">`uri` - Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="97d10-255">指定しない場合、Azure (`vaultName`) はコンテナープロバイダーになります。</span><span class="sxs-lookup"><span data-stu-id="97d10-255">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* <span data-ttu-id="97d10-256">`version` Azure Key Vault には、シークレットのバージョン管理機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="97d10-256">`version` - Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="97d10-257">`version` が指定されている場合、ビルダーはこのバージョンと一致するシークレットのみを取得します。</span><span class="sxs-lookup"><span data-stu-id="97d10-257">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* <span data-ttu-id="97d10-258">`preloadSecretNames`-既定では、このビルダーは初期化時に key vault 内の**すべて**のキー名を querys ます。</span><span class="sxs-lookup"><span data-stu-id="97d10-258">`preloadSecretNames` - By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="97d10-259">すべてのキー値が読み取られないようにするには、この属性を `false`に設定します。</span><span class="sxs-lookup"><span data-stu-id="97d10-259">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="97d10-260">これを `false` に設定すると、一度に1つのシークレットが読み取られます。</span><span class="sxs-lookup"><span data-stu-id="97d10-260">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="97d10-261">資格情報コンテナーが "Get" アクセスを許可し、"リスト" アクセスを許可しない場合は、一度に1つのシークレットを読み取ると便利です。</span><span class="sxs-lookup"><span data-stu-id="97d10-261">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="97d10-262">**注:** `Greedy` モードを使用する場合は、`preloadSecretNames` を `true` (既定値) にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="97d10-262">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="97d10-263">KeyPerFileConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="97d10-263">KeyPerFileConfigBuilder</span></span>

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

<span data-ttu-id="97d10-264">[Keyperfileconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/)は、ディレクトリのファイルを値のソースとして使用する基本的な構成ビルダーです。</span><span class="sxs-lookup"><span data-stu-id="97d10-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="97d10-265">ファイル名はキーで、内容はの値です。</span><span class="sxs-lookup"><span data-stu-id="97d10-265">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="97d10-266">この構成ビルダーは、調整されたコンテナー環境で実行する場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="97d10-266">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="97d10-267">Docker の群れや Kubernetes などのシステムでは、ファイルごとにこのキーを使用して、調整された windows コンテナーに `secrets` を提供します。</span><span class="sxs-lookup"><span data-stu-id="97d10-267">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="97d10-268">属性の詳細:</span><span class="sxs-lookup"><span data-stu-id="97d10-268">Attribute details:</span></span>

* <span data-ttu-id="97d10-269">`directoryPath` - 必須。</span><span class="sxs-lookup"><span data-stu-id="97d10-269">`directoryPath` - Required.</span></span> <span data-ttu-id="97d10-270">値を検索するパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="97d10-270">Specifies a path to look in for values.</span></span> <span data-ttu-id="97d10-271">Docker for Windows シークレットは、既定では*C:\ProgramData\Docker\secrets*ディレクトリに格納されます。</span><span class="sxs-lookup"><span data-stu-id="97d10-271">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* <span data-ttu-id="97d10-272">`ignorePrefix`-このプレフィックスで始まるファイルは除外されます。</span><span class="sxs-lookup"><span data-stu-id="97d10-272">`ignorePrefix` - Files that start with this prefix are excluded.</span></span> <span data-ttu-id="97d10-273">既定値は "ignore" です。</span><span class="sxs-lookup"><span data-stu-id="97d10-273">Defaults to "ignore.".</span></span>
* <span data-ttu-id="97d10-274">`keyDelimiter`-既定値は `null`です。</span><span class="sxs-lookup"><span data-stu-id="97d10-274">`keyDelimiter` - Default value is `null`.</span></span> <span data-ttu-id="97d10-275">指定した場合、構成ビルダーはディレクトリの複数のレベルを走査し、この区切り記号を使用してキー名を構築します。</span><span class="sxs-lookup"><span data-stu-id="97d10-275">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="97d10-276">この値が `null`場合、構成ビルダーはディレクトリの最上位レベルのみを参照します。</span><span class="sxs-lookup"><span data-stu-id="97d10-276">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* <span data-ttu-id="97d10-277">`optional`-既定値は `false`です。</span><span class="sxs-lookup"><span data-stu-id="97d10-277">`optional` -  Default value is `false`.</span></span> <span data-ttu-id="97d10-278">ソースディレクトリが存在しない場合に、構成ビルダーでエラーを発生させるかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="97d10-278">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="97d10-279">SimpleJsonConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="97d10-279">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="97d10-280">パスワード、機密性の高い接続文字列、またはその他の機密データをソースコードに格納しないでください。</span><span class="sxs-lookup"><span data-stu-id="97d10-280">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="97d10-281">運用シークレットは、開発またはテストには使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="97d10-281">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="97d10-282">.NET Core プロジェクトでは、構成に JSON ファイルを頻繁に使用します。</span><span class="sxs-lookup"><span data-stu-id="97d10-282">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="97d10-283">[Simplejsonconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/)ビルダーでは、.NET Core JSON ファイルを .NET Framework で使用できます。</span><span class="sxs-lookup"><span data-stu-id="97d10-283">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="97d10-284">この構成ビルダーは、フラットキー/値ソースから .NET Framework 構成の特定のキー/値領域への基本的なマッピングを提供します。</span><span class="sxs-lookup"><span data-stu-id="97d10-284">This configuration builder is provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="97d10-285">この構成ビルダーでは、階層構造の構成は提供**されません**。</span><span class="sxs-lookup"><span data-stu-id="97d10-285">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="97d10-286">JSON バッキングファイルは、複雑な階層オブジェクトではなく、辞書に似ています。</span><span class="sxs-lookup"><span data-stu-id="97d10-286">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="97d10-287">複数レベルの階層ファイルを使用できます。</span><span class="sxs-lookup"><span data-stu-id="97d10-287">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="97d10-288">このプロバイダーは、`:` を区切り記号として使用して、各レベルにプロパティ名を追加することで、深さを `flatten`します。</span><span class="sxs-lookup"><span data-stu-id="97d10-288">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="97d10-289">属性の詳細:</span><span class="sxs-lookup"><span data-stu-id="97d10-289">Attribute details:</span></span>

* <span data-ttu-id="97d10-290">`jsonFile` - 必須。</span><span class="sxs-lookup"><span data-stu-id="97d10-290">`jsonFile` - Required.</span></span> <span data-ttu-id="97d10-291">読み取る JSON ファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="97d10-291">Specifies the JSON file to read from.</span></span> <span data-ttu-id="97d10-292">`~` 文字は、アプリのルートを参照するために開始時に使用できます。</span><span class="sxs-lookup"><span data-stu-id="97d10-292">The `~` character can be used at the start to reference the app root.</span></span>
* <span data-ttu-id="97d10-293">`optional`-ブール値。既定値は `true`です。</span><span class="sxs-lookup"><span data-stu-id="97d10-293">`optional` - Boolean,  default value is `true`.</span></span> <span data-ttu-id="97d10-294">JSON ファイルが見つからない場合に例外をスローしないようにします。</span><span class="sxs-lookup"><span data-stu-id="97d10-294">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* <span data-ttu-id="97d10-295">`jsonMode` - `[Flat|Sectional]`」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="97d10-295">`jsonMode` - `[Flat|Sectional]`.</span></span> <span data-ttu-id="97d10-296">`Flat` は既定値です。</span><span class="sxs-lookup"><span data-stu-id="97d10-296">`Flat` is the default.</span></span> <span data-ttu-id="97d10-297">`jsonMode` が `Flat`場合、JSON ファイルは1つのフラットキー/値ソースです。</span><span class="sxs-lookup"><span data-stu-id="97d10-297">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="97d10-298">`EnvironmentConfigBuilder` と `AzureKeyVaultConfigBuilder` は、単一のフラットキー/値ソースでもあります。</span><span class="sxs-lookup"><span data-stu-id="97d10-298">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="97d10-299">`SimpleJsonConfigBuilder` が `Sectional` モードで構成されている場合:</span><span class="sxs-lookup"><span data-stu-id="97d10-299">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="97d10-300">JSON ファイルは、概念的に最上位から複数の辞書に分割されています。</span><span class="sxs-lookup"><span data-stu-id="97d10-300">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="97d10-301">各ディクショナリは、接続されている最上位レベルのプロパティ名と一致する構成セクションにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="97d10-301">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="97d10-302">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="97d10-302">For example:</span></span>

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="97d10-303">カスタムキー/値構成ビルダーの実装</span><span class="sxs-lookup"><span data-stu-id="97d10-303">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="97d10-304">構成ビルダーがニーズを満たしていない場合は、カスタムのものを作成できます。</span><span class="sxs-lookup"><span data-stu-id="97d10-304">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="97d10-305">`KeyValueConfigBuilder` 基底クラスは、置換モードとほとんどのプレフィックスの問題を処理します。</span><span class="sxs-lookup"><span data-stu-id="97d10-305">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="97d10-306">実装するプロジェクトに必要なものは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="97d10-306">An implementing project need only:</span></span>

* <span data-ttu-id="97d10-307">基本クラスから継承し、`GetValue` と `GetAllValues`を使用してキーと値のペアの基本的なソースを実装します。</span><span class="sxs-lookup"><span data-stu-id="97d10-307">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="97d10-308">プロジェクトに、 [Microsoft. Configuration. configurationbuilders](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/)追加します。</span><span class="sxs-lookup"><span data-stu-id="97d10-308">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="97d10-309">`KeyValueConfigBuilder` の基本クラスを使用すると、キー/値構成ビルダー間での作業と一貫性のある動作が多くなります。</span><span class="sxs-lookup"><span data-stu-id="97d10-309">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="97d10-310">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="97d10-310">Additional resources</span></span>

* [<span data-ttu-id="97d10-311">構成ビルダー GitHub リポジトリ</span><span class="sxs-lookup"><span data-stu-id="97d10-311">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="97d10-312">.NET を使用して Azure Key Vault するためのサービス間認証</span><span class="sxs-lookup"><span data-stu-id="97d10-312">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)

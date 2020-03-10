---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API での JSON および XML シリアル化-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x の ASP.NET Web API の JSON および XML フォーマッタについて説明します。
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: 00fa07f00eabf7e6c883c5e9ceaf9a38a8f49605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449128"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>ASP.NET Web API での JSON および XML シリアル化

[Mike Wasson](https://github.com/MikeWasson)

この記事では、ASP.NET Web API の JSON フォーマッタと XML フォーマッタについて説明します。

ASP.NET Web API の*メディアタイプフォーマッタ*は、次のことが可能なオブジェクトです。

- HTTP メッセージ本文から CLR オブジェクトを読み取る
- CLR オブジェクトを HTTP メッセージ本文に書き込む

Web API は、JSON と XML の両方のメディアタイプフォーマッタを提供します。 フレームワークは、これらのフォーマッタを既定でパイプラインに挿入します。 クライアントは、HTTP 要求の Accept ヘッダーに JSON または XML のいずれかを要求できます。

## <a name="contents"></a>内容

- [JSON メディアタイプフォーマッタ](#json_media_type_formatter)

    - [読み取り専用プロパティ](#json_readonly)
    - [制約](#json_dates)
    - [インデント](#json_indenting)
    - [Camel 形式の文字種](#json_camelcasing)
    - [厳密に型指定されていない匿名のオブジェクト](#json_anon)
- [XML メディア型フォーマッタ](#xml_media_type_formatter)

    - [読み取り専用プロパティ](#xml_readonly)
    - [制約](#xml_dates)
    - [インデント](#xml_indenting)
    - [型ごとの XML シリアライザーの設定](#xml_pertype)
- [JSON または XML フォーマッタの削除](#removing_the_json_or_xml_formatter)
- [循環オブジェクト参照の処理](#handling_circular_object_references)
- [オブジェクトのシリアル化のテスト](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON メディアタイプフォーマッタ

JSON 形式は、 **JsonMediaTypeFormatter**クラスによって提供されます。 既定では、 **JsonMediaTypeFormatter**は[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)ライブラリを使用してシリアル化を実行します。 Json.NET は、サードパーティのオープンソースプロジェクトです。

必要に応じて、Json.NET ではなく**DataContractJsonSerializer**を使用するように**JsonMediaTypeFormatter**クラスを構成することもできます。 これを行うには、 **UseDataContractJsonSerializer**プロパティを**true**に設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON シリアル化

このセクションでは、既定の[Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer を使用して、JSON フォーマッタの特定の動作について説明します。 これは、Json.NET ライブラリの包括的なドキュメントではありません。詳細については、 [Json.NET のドキュメント](http://james.newtonking.com/projects/json/help/)を参照してください。

#### <a name="what-gets-serialized"></a>シリアル化の対象

既定では、すべてのパブリックプロパティとパブリックフィールドが、シリアル化された JSON に含まれます。 プロパティまたはフィールドを省略するには、 **Jsonignore**属性で装飾します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

&quot;オプトイン&quot; 方法を使用する場合は、 **DataContract**属性でクラスを装飾します。 この属性が存在する場合、メンバーは、 **DataMember**を持っている場合を除き、無視されます。 また、 **DataMember**を使用してプライベートメンバーをシリアル化することもできます。

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>読み取り専用プロパティ

読み取り専用プロパティは、既定でシリアル化されます。

<a id="json_dates"></a>
### <a name="dates"></a>日付

既定では、Json.NET は[ISO 8601](http://www.w3.org/TR/NOTE-datetime)形式で日付を書き込みます。 UTC (協定世界時) の日付は、サフィックス "Z" を使用して書き込まれます。 現地時刻の日付には、タイムゾーンオフセットが含まれます。 次に例を示します。

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

既定では、Json.NET はタイムゾーンを保持します。 これをオーバーライドするには、DateTimeZoneHandling プロパティを設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

ISO 8601 ではなく[MICROSOFT JSON 日付形式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)(`"\/Date(ticks)\/"`) を使用する場合は、シリアライザー設定の**DateFormatHandling**プロパティを設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>インデント

インデントされた JSON を書き込むには、**書式**設定を書式設定に設定**します。インデント**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>Camel 形式の文字種

データモデルを変更せずに camel 形式の JSON プロパティ名を書き込むには、シリアライザーで**CamelCasePropertyNamesContractResolver**を設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>厳密に型指定されていない匿名のオブジェクト

アクションメソッドは、匿名オブジェクトを返し、それを JSON にシリアル化できます。 次に例を示します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

応答メッセージの本文には、次の JSON が含まれます。

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

Web API がクライアントから緩やかに構造化された JSON オブジェクトを受信する場合は、要求本文を**Newtonsoft. Linq オブジェクト**型に逆シリアル化できます。

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

ただし、通常は、厳密に型指定されたデータオブジェクトを使用することをお勧めします。 その後、データを自分で解析する必要がなく、モデルの検証の利点が得られます。

XML シリアライザーは、匿名型または**Jobject**インスタンスをサポートしていません。 これらの機能を JSON データに使用する場合は、この記事の後半で説明するように、パイプラインから XML フォーマッタを削除する必要があります。

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML メディア型フォーマッタ

XML の書式設定は、 **XmlMediaTypeFormatter**クラスによって提供されます。 既定では、 **XmlMediaTypeFormatter**は**DataContractSerializer**クラスを使用してシリアル化を実行します。

必要に応じて、 **DataContractSerializer**ではなく**XmlSerializer**を使用するように**XmlMediaTypeFormatter**を構成できます。 これを行うには、 **UseXmlSerializer**プロパティを**true**に設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

**XmlSerializer**クラスでは、 **DataContractSerializer**よりも狭い種類の型がサポートされていますが、結果の XML はより詳細に制御できます。 既存の XML スキーマに一致する必要がある場合は、 **XmlSerializer**の使用を検討してください。

### <a name="xml-serialization"></a>XML シリアル化

このセクションでは、既定の**DataContractSerializer**を使用して、XML フォーマッタの特定の動作について説明します。

既定では、DataContractSerializer は次のように動作します。

- パブリックの読み取り/書き込みプロパティとフィールドはすべてシリアル化されます。 プロパティまたはフィールドを省略するには、 **Ignoredatamember**属性で装飾します。
- プライベートメンバーとプロテクトメンバーはシリアル化されません。
- 読み取り専用プロパティはシリアル化されません。 (ただし、読み取り専用コレクションプロパティの内容はシリアル化されます)。
- クラス名とメンバー名は、クラス宣言に出現するとおりに XML で記述されます。
- 既定の XML 名前空間が使用されます。

シリアル化をさらに制御する必要がある場合は、 **DataContract**属性を使用してクラスを装飾できます。 この属性が存在する場合、クラスは次のようにシリアル化されます。

- &quot;オプトイン&quot; 方法: 既定では、プロパティとフィールドはシリアル化されません。 プロパティまたはフィールドをシリアル化するには、 **DataMember**属性で装飾します。
- プライベートメンバーまたはプロテクトメンバーをシリアル化するには、 **DataMember**属性で装飾します。
- 読み取り専用プロパティはシリアル化されません。
- XML でのクラス名の表示方法を変更するには、 **DataContract**属性の*name*パラメーターを設定します。
- XML でのメンバー名の表示方法を変更するには、 **DataMember**属性に*name*パラメーターを設定します。
- XML 名前空間を変更するには、 **DataContract**クラスの*namespace*パラメーターを設定します。

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>読み取り専用プロパティ

読み取り専用プロパティはシリアル化されません。 読み取り専用プロパティにバッキングプライベートフィールドがある場合は、 **DataMember**属性を使用してプライベートフィールドをマークできます。 この方法では、クラスの**DataContract**属性が必要です。

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>日付

日付は ISO 8601 形式で記述されます。 たとえば、&quot;2012-05-23T20:21: 37.9116538 Z&quot;のようになります。

<a id="xml_indenting"></a>
### <a name="indenting"></a>インデント

インデントされた XML を書き込むには、 **[インデント]** プロパティを**true**に設定します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>型ごとの XML シリアライザーの設定

異なる CLR 型に対して異なる XML シリアライザーを設定できます。 たとえば、旧バージョンとの互換性のために**XmlSerializer**を必要とする特定のデータオブジェクトがある場合があります。 このオブジェクトに**XmlSerializer**を使用して、他の型に対して**DataContractSerializer**を引き続き使用することができます。

特定の型の XML シリアライザーを設定するには、 **Setserializer**を呼び出します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

**XmlSerializer**または**XmlObjectSerializer**から派生した任意のオブジェクトを指定できます。

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>JSON または XML フォーマッタの削除

フォーマッタを使用しない場合は、フォーマッタの一覧から JSON フォーマッタまたは XML フォーマッタを削除できます。 これを行う主な理由は次のとおりです。

- Web API の応答を特定のメディアの種類に制限する。 たとえば、JSON 応答のみをサポートし、XML フォーマッタを削除することができます。
- 既定のフォーマッタをカスタムフォーマッタに置き換える場合は。 たとえば、json フォーマッタを JSON フォーマッタの独自のカスタム実装に置き換えることができます。

次のコードは、既定のフォーマッタを削除する方法を示しています。 このメソッドは、global.asax で定義された**開始メソッド\_アプリケーション**から呼び出します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>循環オブジェクト参照の処理

既定では、JSON および XML フォーマッタはすべてのオブジェクトを値として書き込みます。 2つのプロパティが同じオブジェクトを参照している場合、またはコレクション内で同じオブジェクトが2回出現する場合、フォーマッタはオブジェクトを2回シリアル化します。 これは、オブジェクトグラフに循環が含まれている場合の問題です。これは、シリアライザーがグラフ内でループを検出したときに例外をスローするためです。

次のオブジェクトモデルとコントローラーを考えてみます。

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

このアクションを呼び出すと、フォーマッタによって例外がスローされ、クライアントへのステータスコード 500 (内部サーバーエラー) 応答に変換されます。

JSON でオブジェクト参照を保持するには、次のコードを、global.asax ファイルの**Application\_Start**メソッドに追加します。

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

これで、コントローラーアクションは次のような JSON を返します。

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

シリアライザーによって &quot;$id&quot; プロパティが両方のオブジェクトに追加されることに注意してください。 また、Employee. Department プロパティによってループが作成されていることが検出されるため、値は {&quot;$ref&quot;:&quot;1&quot;} というオブジェクト参照に置き換えられます。

> [!NOTE]
> オブジェクト参照は JSON では標準ではありません。 この機能を使用する前に、クライアントが結果を解析できるかどうかを検討してください。 グラフからサイクルを削除するだけでよい場合もあります。 たとえば、この例では、従業員から部署へのリンクは実際には必要ありません。

XML でオブジェクト参照を保持するには、2つのオプションがあります。 より簡単な方法は、モデルクラスに `[DataContract(IsReference=true)]` を追加することです。 *IsReference*パラメーターを使用すると、オブジェクト参照が有効になります。 **DataContract**ではシリアル化がオプトインされているため、プロパティに**DataMember**属性を追加する必要もあります。

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

これで、フォーマッタは次のような XML を生成します。

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

モデルクラスで属性を使用しない場合は、別のオプションがあります。新しい型固有の**DataContractSerializer**インスタンスを作成し、コンストラクターで*preserveObjectReferences*を**true**に設定します。 次に、このインスタンスを XML メディア型フォーマッタの型ごとのシリアライザーとして設定します。 次のコードは、これを行う方法を示しています。

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>オブジェクトのシリアル化のテスト

Web API を設計する際には、データオブジェクトがどのようにシリアル化されるかをテストすると便利です。 これは、コントローラーを作成したり、コントローラーアクションを呼び出したりせずに行うことができます。

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]

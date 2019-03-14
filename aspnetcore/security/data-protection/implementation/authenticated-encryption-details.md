---
title: ASP.NET Core での認証された暗号化の詳細
author: rick-anderson
description: ASP.NET Core データ保護が認証された暗号化の実装の詳細について説明します。
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/authenticated-encryption-details
ms.openlocfilehash: ac650e5c32e7eacc4088225e63f56340f95e1913
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047719"
---
# <a name="authenticated-encryption-details-in-aspnet-core"></a><span data-ttu-id="8703f-103">ASP.NET Core での認証された暗号化の詳細</span><span class="sxs-lookup"><span data-stu-id="8703f-103">Authenticated encryption details in ASP.NET Core</span></span>

<a name="data-protection-implementation-authenticated-encryption-details"></a>

<span data-ttu-id="8703f-104">IDataProtector.Protect への呼び出しは、認証された暗号化操作です。</span><span class="sxs-lookup"><span data-stu-id="8703f-104">Calls to IDataProtector.Protect are authenticated encryption operations.</span></span> <span data-ttu-id="8703f-105">機密性と完全性、保護メソッドが提供および IDataProtectionProvider ルートからのこの特定の IDataProtector インスタンスの派生に使用された目的のチェーンに関連付けられていること。</span><span class="sxs-lookup"><span data-stu-id="8703f-105">The Protect method offers both confidentiality and authenticity, and it's tied to the purpose chain that was used to derive this particular IDataProtector instance from its root IDataProtectionProvider.</span></span>

<span data-ttu-id="8703f-106">IDataProtector.Protect は、byte[] プレーン テキスト パラメーターを受け取り、その形式は以下の説明をバイト ・ [保護されたペイロードを生成します。</span><span class="sxs-lookup"><span data-stu-id="8703f-106">IDataProtector.Protect takes a byte[] plaintext parameter and produces a byte[] protected payload, whose format is described below.</span></span> <span data-ttu-id="8703f-107">(も、拡張機能メソッド オーバー ロードがプレーン テキストの文字列パラメーターを取得し、文字列の保護されたペイロードを返します。</span><span class="sxs-lookup"><span data-stu-id="8703f-107">(There's also an extension method overload which takes a string plaintext parameter and returns a string protected payload.</span></span> <span data-ttu-id="8703f-108">この API を使用する場合、保護されたペイロード形式が残っている、構造体には、以下がそのは[base64url でエンコードされた](https://tools.ietf.org/html/rfc4648#section-5))。</span><span class="sxs-lookup"><span data-stu-id="8703f-108">If this API is used the protected payload format will still have the below structure, but it will be [base64url-encoded](https://tools.ietf.org/html/rfc4648#section-5).)</span></span>

## <a name="protected-payload-format"></a><span data-ttu-id="8703f-109">保護されたペイロードの形式</span><span class="sxs-lookup"><span data-stu-id="8703f-109">Protected payload format</span></span>

<span data-ttu-id="8703f-110">保護されたペイロードの形式は、次の 3 つの主要なコンポーネントで構成されます。</span><span class="sxs-lookup"><span data-stu-id="8703f-110">The protected payload format consists of three primary components:</span></span>

* <span data-ttu-id="8703f-111">データ保護システムのバージョンを識別する 32 ビット マジック ヘッダー。</span><span class="sxs-lookup"><span data-stu-id="8703f-111">A 32-bit magic header that identifies the version of the data protection system.</span></span>

* <span data-ttu-id="8703f-112">この特定のペイロードを保護するために使用するキーを識別する 128 ビット キー id。</span><span class="sxs-lookup"><span data-stu-id="8703f-112">A 128-bit key id that identifies the key used to protect this particular payload.</span></span>

* <span data-ttu-id="8703f-113">保護されたペイロードの残りの部分は[このキーによってカプセル化された暗号化機能に固有](xref:security/data-protection/implementation/subkeyderivation#data-protection-implementation-subkey-derivation)します。</span><span class="sxs-lookup"><span data-stu-id="8703f-113">The remainder of the protected payload is [specific to the encryptor encapsulated by this key](xref:security/data-protection/implementation/subkeyderivation#data-protection-implementation-subkey-derivation).</span></span> <span data-ttu-id="8703f-114">次の例で、キーを表す、AES-CBC 256 + HMACSHA256 暗号化機能と、ペイロードは次のようにさらに分割します。 \* 128 ビット キー修飾子。</span><span class="sxs-lookup"><span data-stu-id="8703f-114">In the example below the key represents an AES-256-CBC + HMACSHA256 encryptor, and the payload is further subdivided as follows: \* A 128-bit key modifier.</span></span> <span data-ttu-id="8703f-115">\* は、128 ビットの初期化ベクトルです。</span><span class="sxs-lookup"><span data-stu-id="8703f-115">\* A 128-bit initialization vector.</span></span> <span data-ttu-id="8703f-116">\* AES-CBC 256 出力の 48 バイト数。</span><span class="sxs-lookup"><span data-stu-id="8703f-116">\* 48 bytes of AES-256-CBC output.</span></span> <span data-ttu-id="8703f-117">\*、HMACSHA256 認証タグ。</span><span class="sxs-lookup"><span data-stu-id="8703f-117">\* An HMACSHA256 authentication tag.</span></span>

<span data-ttu-id="8703f-118">保護されたペイロードのサンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="8703f-118">A sample protected payload is illustrated below.</span></span>

```
09 F0 C9 F0 80 9C 81 0C 19 66 19 40 95 36 53 F8
AA FF EE 57 57 2F 40 4C 3F 7F CC 9D CC D9 32 3E
84 17 99 16 EC BA 1F 4A A1 18 45 1F 2D 13 7A 28
79 6B 86 9C F8 B7 84 F9 26 31 FC B1 86 0A F1 56
61 CF 14 58 D3 51 6F CF 36 50 85 82 08 2D 3F 73
5F B0 AD 9E 1A B2 AE 13 57 90 C8 F5 7C 95 4E 6A
8A AA 06 EF 43 CA 19 62 84 7C 11 B2 C8 71 9D AA
52 19 2E 5B 4C 1E 54 F0 55 BE 88 92 12 C1 4B 5E
52 C9 74 A0
```

<span data-ttu-id="8703f-119">最初の 32 ビット、または 4 バイトのペイロード形式からは、マジックのヘッダー バージョン (09 F0 C9 F0) を識別します。</span><span class="sxs-lookup"><span data-stu-id="8703f-119">From the payload format above the first 32 bits, or 4 bytes are the magic header identifying the version (09 F0 C9 F0)</span></span>

<span data-ttu-id="8703f-120">次の 128 ビットまたは 16 バイトは、キー識別子 (80 9 の C 81 0 C 19 66 19 40 95 36 53 F8 AA FF EE 57)</span><span class="sxs-lookup"><span data-stu-id="8703f-120">The next 128 bits, or 16 bytes is the key identifier (80 9C 81 0C 19 66 19 40 95 36 53 F8 AA FF EE 57)</span></span>

<span data-ttu-id="8703f-121">残りの部分では、ペイロードを含むあり、使用する形式に固有です。</span><span class="sxs-lookup"><span data-stu-id="8703f-121">The remainder contains the payload and is specific to the format used.</span></span>

>[!WARNING]
> <span data-ttu-id="8703f-122">指定されたキーに対して保護されているすべてのペイロードは、同じ 20 バイト (魔法の値、キー id) ヘッダーで開始されます。</span><span class="sxs-lookup"><span data-stu-id="8703f-122">All payloads protected to a given key will begin with the same 20-byte (magic value, key id) header.</span></span> <span data-ttu-id="8703f-123">管理者は、およそのペイロードが生成されたときに、診断のために、このファクトを使用できます。</span><span class="sxs-lookup"><span data-stu-id="8703f-123">Administrators can use this fact for diagnostic purposes to approximate when a payload was generated.</span></span> <span data-ttu-id="8703f-124">たとえば、上記のペイロードは、{0c819c80-6619-4019-9536-53f8aaffee57} をキーに対応します。</span><span class="sxs-lookup"><span data-stu-id="8703f-124">For example, the payload above corresponds to key {0c819c80-6619-4019-9536-53f8aaffee57}.</span></span> <span data-ttu-id="8703f-125">キーのリポジトリを確認した後は、この特定のキーのアクティブ化日付が 2015-01-01 をし、その有効期限の日付が 2015-03-01、あると想定するが妥当を見つけられない場合、ペイロード (で改ざんされていない) 場合により、そのウィンドウ内で生成されたまたは小さないずれかの側の一種です。</span><span class="sxs-lookup"><span data-stu-id="8703f-125">If after checking the key repository you find that this specific key's activation date was 2015-01-01 and its expiration date was 2015-03-01, then it's reasonable to assume that the payload (if not tampered with) was generated within that window, give or take a small fudge factor on either side.</span></span>

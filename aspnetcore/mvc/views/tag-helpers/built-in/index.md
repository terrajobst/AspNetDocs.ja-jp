---
title: ASP.NET Core の組み込みタグ ヘルパー
author: pkellner
description: タグ ヘルパーに組み込まれた ASP.NET Core によって生産性がどのように向上するかをご確認ください。
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/Index
---

# <a name="aspnet-core-built-in-tag-helpers"></a><span data-ttu-id="ca77f-103">ASP.NET Core の組み込みタグ ヘルパー</span><span class="sxs-lookup"><span data-stu-id="ca77f-103">ASP.NET Core built-in Tag Helpers</span></span>

<span data-ttu-id="ca77f-104">著者: [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="ca77f-104">By [Peter Kellner](http://peterkellner.net)</span></span>

<span data-ttu-id="ca77f-105">タグ ヘルパーの概要については、「<xref:mvc/views/tag-helpers/intro>」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="ca77f-105">For an overview of Tag Helpers, see <xref:mvc/views/tag-helpers/intro>.</span></span>

> [!NOTE]
> <span data-ttu-id="ca77f-106">組み込みタグ ヘルパーがありますが、ドキュメントには記述されていません。</span><span class="sxs-lookup"><span data-stu-id="ca77f-106">There are built-in Tag Helpers which aren't described in the documentation.</span></span> <span data-ttu-id="ca77f-107">これらのタグ ヘルパーは、[Razor](xref:mvc/views/razor) ビュー エンジンによって内部で使用されます。</span><span class="sxs-lookup"><span data-stu-id="ca77f-107">These Tag Helpers are used internally by the [Razor](xref:mvc/views/razor) view engine.</span></span> <span data-ttu-id="ca77f-108">これには、Web サイトのルート パスに展開される `~` (チルダ) 文字のタグ ヘルパーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="ca77f-108">This includes a Tag Helper for the `~` (tilde) character, which expands to the root path of the website.</span></span>

## <a name="built-in-aspnet-core-tag-helpers"></a><span data-ttu-id="ca77f-109">組み込み ASP.NET Core タグ ヘルパー</span><span class="sxs-lookup"><span data-stu-id="ca77f-109">Built-in ASP.NET Core Tag Helpers</span></span>

<span data-ttu-id="ca77f-110">**[アンカー タグ ヘルパー](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-110">**[Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span></span>

<span data-ttu-id="ca77f-111">**[キャッシュ タグ ヘルパー](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-111">**[Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span></span>

<span data-ttu-id="ca77f-112">**[分散キャッシュ タグ ヘルパー](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-112">**[Distributed Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span></span>

<span data-ttu-id="ca77f-113">**[環境タグ ヘルパー](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-113">**[Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span></span>

[comment]: **[FormActionTagHelper](xref:mvc/views/tag-helpers/builtin-th/form-action-tag-helper)**

<span data-ttu-id="ca77f-114">**[フォーム タグ ヘルパー](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-114">**[Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span></span>

<span data-ttu-id="ca77f-115">**[イメージ タグ ヘルパー](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-115">**[Image Tag Helper](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span></span>

<span data-ttu-id="ca77f-116">**[入力タグ ヘルパー](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-116">**[Input Tag Helper](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span></span>

<span data-ttu-id="ca77f-117">**[ラベル タグ ヘルパー](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-117">**[Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span></span>

[comment]: **[LinkTagHelper](xref:mvc/views/tag-helpers/builtin-th/link-tag-helper)**

[comment]: **[OptionTagHelper](xref:mvc/views/tag-helpers/builtin-th/option-tag-helper)**

[comment]: **[ScriptTagHelper](xref:mvc/views/tag-helpers/builtin-th/script-tag-helper)**

<span data-ttu-id="ca77f-118">**[部分タグ ヘルパー](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-118">**[Partial Tag Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span></span>

<span data-ttu-id="ca77f-119">**[選択タグ ヘルパー](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-119">**[Select Tag Helper](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span></span>

<span data-ttu-id="ca77f-120">**[Textarea タグ ヘルパー](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-120">**[Textarea Tag Helper](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span></span>

<span data-ttu-id="ca77f-121">**[検証メッセージ タグ ヘルパー](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-121">**[Validation Message Tag Helper](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span></span>

<span data-ttu-id="ca77f-122">**[検証概要タグ ヘルパー](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ca77f-122">**[Validation Summary Tag Helper](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca77f-123">その他の技術情報</span><span class="sxs-lookup"><span data-stu-id="ca77f-123">Additional resources</span></span>

* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/th-components>

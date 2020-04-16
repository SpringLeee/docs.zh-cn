---
title: x:FieldModifier 指令
ms.date: 03/30/2017
helpviewer_keywords:
- FieldModifier attribute in XAML [XAML Services]
- x:FieldModifier attribute [XAML Services]
- XAML [XAML Services], x:FieldModifier attribute
ms.assetid: ed427cd4-2f35-4d24-bd2f-0fa7b71ec248
ms.openlocfilehash: 3e104b4c464d545e048f29901701c1c3dbb68229
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432778"
---
# <a name="xfieldmodifier-directive"></a><span data-ttu-id="a020b-102">x:FieldModifier 指令</span><span class="sxs-lookup"><span data-stu-id="a020b-102">x:FieldModifier Directive</span></span>
<span data-ttu-id="a020b-103">修改 XAML 编译行为，以便使用<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>访问而不是默认行为定义命名对象引用的<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>字段。</span><span class="sxs-lookup"><span data-stu-id="a020b-103">Modifies XAML compilation behavior so that fields for named object references are defined with <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> access instead of the <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> default behavior.</span></span>

## <a name="xaml-attribute-usage"></a><span data-ttu-id="a020b-104">XAML 属性用法</span><span class="sxs-lookup"><span data-stu-id="a020b-104">XAML Attribute Usage</span></span>

```xaml
<object x:FieldModifier="Public".../>
```

## <a name="xaml-values"></a><span data-ttu-id="a020b-105">XAML 值</span><span class="sxs-lookup"><span data-stu-id="a020b-105">XAML Values</span></span>

|||
|-|-|
|<span data-ttu-id="a020b-106">*公共*</span><span class="sxs-lookup"><span data-stu-id="a020b-106">*Public*</span></span>|<span data-ttu-id="a020b-107">传递给指定的<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>确切字符串因<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>所使用的代码后面编程语言而异。</span><span class="sxs-lookup"><span data-stu-id="a020b-107">The exact string you pass to specify <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> versus <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> varies, depending on the code-behind programming language that is used.</span></span> <span data-ttu-id="a020b-108">请参阅“备注”。</span><span class="sxs-lookup"><span data-stu-id="a020b-108">See Remarks.</span></span>|

## <a name="dependencies"></a><span data-ttu-id="a020b-109">依赖项</span><span class="sxs-lookup"><span data-stu-id="a020b-109">Dependencies</span></span>

 <span data-ttu-id="a020b-110">如果 XAML 生产`x:FieldModifier`在任何地方使用，则 XAML 生产的根元素必须声明[x：类指令](xclass-directive.md)。</span><span class="sxs-lookup"><span data-stu-id="a020b-110">If a XAML production uses `x:FieldModifier` anywhere, the root element of that XAML production must declare an [x:Class Directive](xclass-directive.md).</span></span>

## <a name="remarks"></a><span data-ttu-id="a020b-111">备注</span><span class="sxs-lookup"><span data-stu-id="a020b-111">Remarks</span></span>

<span data-ttu-id="a020b-112">`x:FieldModifier`与声明类或其成员的一般访问级别无关。</span><span class="sxs-lookup"><span data-stu-id="a020b-112">`x:FieldModifier` is not relevant for declaring the general access level of a class or its members.</span></span> <span data-ttu-id="a020b-113">它仅与 XAML 处理行为相关，因为处理属于 XAML 生产一部分的特定 XAML 对象，并成为在应用程序的对象图中可能可访问的对象。</span><span class="sxs-lookup"><span data-stu-id="a020b-113">It is relevant only for XAML-processing behavior when a particular XAML object that is part of a XAML production is processed, and becomes an object that is potentially accessible in the object graph of an application.</span></span> <span data-ttu-id="a020b-114">默认情况下，此类对象的字段引用保持私有，这可以防止控件使用者直接修改对象图。</span><span class="sxs-lookup"><span data-stu-id="a020b-114">By default, the field reference for such an object is kept private, which prevents control consumers from modifying the object graph directly.</span></span> <span data-ttu-id="a020b-115">相反，控件使用者应该使用编程模型启用的标准模式来修改对象图，例如通过获取布局根、子元素集合、专用公共属性等。</span><span class="sxs-lookup"><span data-stu-id="a020b-115">Instead, control consumers are expected to modify the object graph by using standard patterns that are enabled by programming models, such as by obtaining the layout root, the child element collections, the dedicated public properties, and so on.</span></span>

<span data-ttu-id="a020b-116">`x:FieldModifier`属性的值因编程语言而异，并且其用途可能因特定框架而异。</span><span class="sxs-lookup"><span data-stu-id="a020b-116">The value for the `x:FieldModifier` attribute varies by programming language, and its purpose can vary in specific frameworks.</span></span> <span data-ttu-id="a020b-117">要使用的字符串取决于每种语言如何实现其<xref:System.CodeDom.Compiler.CodeDomProvider>和返回的类型转换器来定义<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>和<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>的含义，以及该语言是否区分大小写。</span><span class="sxs-lookup"><span data-stu-id="a020b-117">The string to use depends on how each language implements its <xref:System.CodeDom.Compiler.CodeDomProvider> and the type converters it returns to define the meanings for <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> and <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>, and whether that language is case sensitive.</span></span>

- <span data-ttu-id="a020b-118">对于 C#，要传递到指定的<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>字符串为`public`。</span><span class="sxs-lookup"><span data-stu-id="a020b-118">For C#, the string to pass to designate <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> is `public`.</span></span>

- <span data-ttu-id="a020b-119">对于 Microsoft Visual Basic .NET，要传递<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>要`Public`指定的字符串为 。</span><span class="sxs-lookup"><span data-stu-id="a020b-119">For Microsoft Visual Basic .NET, the string to pass to designate <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> is `Public`.</span></span>

- <span data-ttu-id="a020b-120">对于C++/CLI，目前不存在 XAML 的目标;因此，要传递的字符串未定义。</span><span class="sxs-lookup"><span data-stu-id="a020b-120">For C++/CLI, no targets for XAML currently exist; therefore, the string to pass is undefined.</span></span>

<span data-ttu-id="a020b-121"><xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>您还可以指定（`internal`在 C# 中`Friend`，在 Visual Basic<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>中），`NotPublic`但指定是不寻常的，因为行为已经是默认值。</span><span class="sxs-lookup"><span data-stu-id="a020b-121">You can also specify <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> (`internal` in C#, `Friend` in Visual Basic) but specifying <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> is unusual because `NotPublic` as the behavior is already the default.</span></span>

<span data-ttu-id="a020b-122"><xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>是默认行为，因为编译 XAML 的程序集外部的代码很少需要访问 XAML 创建的元素。</span><span class="sxs-lookup"><span data-stu-id="a020b-122"><xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> is the default behavior because it is infrequent that code outside the assembly that compiled the XAML needs access to a XAML-created element.</span></span> <span data-ttu-id="a020b-123">WPF 安全体系结构以及 XAML 编译行为不会声明存储元素实例的字段为公共，除非您专门设置`x:FieldModifier`允许公共访问。</span><span class="sxs-lookup"><span data-stu-id="a020b-123">WPF security architecture together with XAML compilation behavior will not declare fields that store element instances as public, unless you specifically set the `x:FieldModifier` to allow public access.</span></span>

<span data-ttu-id="a020b-124">`x:FieldModifier`仅与[具有 x：name 指令](xname-directive.md)的元素相关，因为该名称用于在字段公开后引用该字段。</span><span class="sxs-lookup"><span data-stu-id="a020b-124">`x:FieldModifier` is only relevant for elements with an [x:Name Directive](xname-directive.md) because that name is used to reference the field after it is public.</span></span>

<span data-ttu-id="a020b-125">默认情况下，根元素的部分类是公共的;因此，根元素的部分类为公共类。但是，您可以使用[x：Class 修改器指令](xclassmodifier-directive.md)将其非公开。</span><span class="sxs-lookup"><span data-stu-id="a020b-125">By default, the partial class for the root element is public; however, you can make it nonpublic by using the [x:ClassModifier Directive](xclassmodifier-directive.md).</span></span> <span data-ttu-id="a020b-126">[x：Class 修改器指令](xclassmodifier-directive.md)还影响根元素类实例的访问级别。</span><span class="sxs-lookup"><span data-stu-id="a020b-126">The [x:ClassModifier Directive](xclassmodifier-directive.md) also affects the access level of the instance of the root element class.</span></span> <span data-ttu-id="a020b-127">您可以将 和`x:FieldModifier``x:Name`放在根元素上，但这仅使根元素的公共字段副本，真正的根元素类访问级别仍由[x：Class修改器指令](xclassmodifier-directive.md)控制。</span><span class="sxs-lookup"><span data-stu-id="a020b-127">You can put both `x:Name` and `x:FieldModifier` on the root element, but this only makes a public field copy of the root element, with the true root element class access level still controlled by [x:ClassModifier Directive](xclassmodifier-directive.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a020b-128">请参阅</span><span class="sxs-lookup"><span data-stu-id="a020b-128">See also</span></span>

- [<span data-ttu-id="a020b-129">XAML 及 WPF 的自定义类</span><span class="sxs-lookup"><span data-stu-id="a020b-129">XAML and Custom Classes for WPF</span></span>](../../framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)
- [<span data-ttu-id="a020b-130">WPF 中的代码隐藏和 XAML</span><span class="sxs-lookup"><span data-stu-id="a020b-130">Code-Behind and XAML in WPF</span></span>](../../framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [<span data-ttu-id="a020b-131">x:Name 指令</span><span class="sxs-lookup"><span data-stu-id="a020b-131">x:Name Directive</span></span>](xname-directive.md)
- <span data-ttu-id="a020b-132">[Building a WPF Application (WPF)](../../framework/wpf/app-development/building-a-wpf-application-wpf.md)（生成 WPF 应用程序 (WPF)）</span><span class="sxs-lookup"><span data-stu-id="a020b-132">[Building a WPF Application (WPF)](../../framework/wpf/app-development/building-a-wpf-application-wpf.md)</span></span>
- [<span data-ttu-id="a020b-133">x:ClassModifier 指令</span><span class="sxs-lookup"><span data-stu-id="a020b-133">x:ClassModifier Directive</span></span>](xclassmodifier-directive.md)
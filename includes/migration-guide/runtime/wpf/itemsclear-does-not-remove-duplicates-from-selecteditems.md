---
ms.openlocfilehash: 75f176133697056bab9349ba1d18d7a0e1aa7da2
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619815"
---
### <a name="itemsclear-does-not-remove-duplicates-from-selecteditems"></a>Items.Clear 不会从 SelectedItems 删除重复项

#### <a name="details"></a>详细信息

假设选择器（已启用多个选择）在其 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> 集合中有多个重复项（出现不止一次的相同项）。  从数据源删除这些项（例如通过调用 Items.Clear）不会从 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> 删除它们；仅删除第一个实例。 此外，随后使用 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName>（例如 SelectedItems.Clear()）可能会遇到 <xref:System.ArgumentException?displayProperty=fullName> 等问题，这是因为 <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> 包含不再出现在数据源中的项。

#### <a name="suggestion"></a>建议

如果可能请升级到 .NET Framework 4.6.2。

| “属性”    | “值”       |
|:--------|:------------|
| 范围   |次要|
|Version|4.5|
|类型|运行时

#### <a name="affected-apis"></a>受影响的 API

-<xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=nameWithType></li></ul>|

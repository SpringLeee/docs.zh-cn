---
ms.openlocfilehash: 770e303ab261b97efb49a3e0865a015d8de33247
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67802680"
---
### <a name="improvements-to-grid-star-rows-space-allocating-algorithm"></a><span data-ttu-id="8bd9d-101">网格星型行空格分配算法的改进</span><span class="sxs-lookup"><span data-stu-id="8bd9d-101">Improvements to Grid star-rows space allocating algorithm</span></span>

|   |   |
|---|---|
|<span data-ttu-id="8bd9d-102">详细信息</span><span class="sxs-lookup"><span data-stu-id="8bd9d-102">Details</span></span>|<span data-ttu-id="8bd9d-103">修复了在 .NET Framework 4.7 中引入的 <xref:System.Windows.Controls.Grid> 中[用于分配大小的算法](https://github.com/Microsoft/dotnet/blob/master/Documentation/compatibility/wpf-grid-allocation-of-space-to-star-columns.md)的问题。</span><span class="sxs-lookup"><span data-stu-id="8bd9d-103">Fixed a bug in the [algorithm for allocating sizes to ](https://github.com/Microsoft/dotnet/blob/master/Documentation/compatibility/wpf-grid-allocation-of-space-to-star-columns.md)) in a <xref:System.Windows.Controls.Grid> introduced in .NET Framework 4.7.</span></span>  <span data-ttu-id="8bd9d-104">在某些情况下，例如，<code>Height=&quot;Auto&quot;</code> 包含空行的网格，行排列在错误的位置，可能完全在网格之外。</span><span class="sxs-lookup"><span data-stu-id="8bd9d-104">In some cases, such as a Grid with <code>Height=&quot;Auto&quot;</code> containing empty rows, rows were arranged at the wrong position, possibly outside the Grid altogether.</span></span>|
|<span data-ttu-id="8bd9d-105">建议</span><span class="sxs-lookup"><span data-stu-id="8bd9d-105">Suggestion</span></span>|<span data-ttu-id="8bd9d-106">为使应用程序从这些更改中获益，它必须在 .NET Framework 4.8 或更高版本上运行。</span><span class="sxs-lookup"><span data-stu-id="8bd9d-106">In order for the application to benefit from these changes, it must run on the .NET Framework 4.8 or later.</span></span>|
|<span data-ttu-id="8bd9d-107">范围</span><span class="sxs-lookup"><span data-stu-id="8bd9d-107">Scope</span></span>|<span data-ttu-id="8bd9d-108">主要</span><span class="sxs-lookup"><span data-stu-id="8bd9d-108">Major</span></span>|
|<span data-ttu-id="8bd9d-109">Version</span><span class="sxs-lookup"><span data-stu-id="8bd9d-109">Version</span></span>|<span data-ttu-id="8bd9d-110">4.8</span><span class="sxs-lookup"><span data-stu-id="8bd9d-110">4.8</span></span>|
|<span data-ttu-id="8bd9d-111">类型</span><span class="sxs-lookup"><span data-stu-id="8bd9d-111">Type</span></span>|<span data-ttu-id="8bd9d-112">运行时</span><span class="sxs-lookup"><span data-stu-id="8bd9d-112">Runtime</span></span>|

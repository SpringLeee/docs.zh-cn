---
title: GetHashFromAssemblyFileW 函数
ms.date: 03/30/2017
api_name:
- GetHashFromAssemblyFileW
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetHashFromAssemblyFileW
helpviewer_keywords:
- GetHashFromAssemblyFileW function [.NET Framework strong naming]
ms.assetid: d1b2b172-5353-42af-a877-cf653c68ece0
topic_type:
- apiref
ms.openlocfilehash: cf7667f0f2a0f77cd793e00a5de8b030b0c53ec8
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73140697"
---
# <a name="gethashfromassemblyfilew-function"></a>GetHashFromAssemblyFileW 函数
使用指定的哈希算法获取指定程序集文件的哈希。 必须将程序集文件的路径指定为 Unicode 字符串。  
  
 此函数已弃用。 改为使用[ICLRStrongName：： GetHashFromAssemblyFileW](../hosting/iclrstrongname-gethashfromassemblyfilew-method.md)方法。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetHashFromAssemblyFileW (  
    [in]  LPCWSTR   wszFilePath,  
    [in, out] unsigned int   *piHashAlg,  
    [out] BYTE      *pbHash,  
    [in]  DWORD     cchHash,  
    [out] DWORD     *pchHash  
);  
```  
  
## <a name="parameters"></a>参数  
 `wszFilePath`  
 中要进行哈希处理的文件的路径。 此参数必须是 Unicode 字符串。  
  
 `piHashAlg`  
 [in，out]指定哈希算法的常量。 使用零作为默认哈希算法。  
  
 `pbHash`  
 弄返回的哈希缓冲区。  
  
 `cchHash`  
 中请求的最大 `pbHash`大小。  
  
 `pchHash`  
 弄返回 `pbHash`的大小（以字节为单位）。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../get-started/system-requirements.md)。  
  
 **标头：** Stackexchange.redis.strongname  
  
 **库：** 作为资源包括在 Mscoree.dll 中  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [GetHashFromAssemblyFileW 方法](../hosting/iclrstrongname-gethashfromassemblyfilew-method.md)
- [GetHashFromAssemblyFile 方法](../hosting/iclrstrongname-gethashfromassemblyfile-method.md)
- [ICLRStrongName 接口](../hosting/iclrstrongname-interface.md)

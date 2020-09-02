---
title: BP_LOCATION | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION
helpviewer_keywords:
- BP_LOCATION union
ms.assetid: ed1e874c-f289-4c31-8b6c-04dde03ad0f5
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2a3e5f690a679118c7bb02c110d6e5d066a2bd0d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153391"
---
# <a name="bp_location"></a>BP_LOCATION
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Especifica o tipo de estrutura usada para descrever o local do ponto de interrupção.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
typedef struct _BP_LOCATION {  
   BP_LOCATION_TYPE bpLocationType;  
   union {  
      BP_LOCATION_CODE_FILE_LINE   bplocCodeFileLine;  
      BP_LOCATION_CODE_FUNC_OFFSET bplocCodeFuncOffset;  
      BP_LOCATION_CODE_CONTEXT     bplocCodeContext;  
      BP_LOCATION_CODE_STRING      bplocCodeString;  
      BP_LOCATION_CODE_ADDRESS     bplocCodeAddress;  
      BP_LOCATION_DATA_STRING      bplocDataString;  
      BP_LOCATION_RESOLUTION       bplocResolution;  
      DWORD                        unused;  
   } bpLocation;  
} BP_LOCATION;  
```  
  
```csharp  
public struct BP_LOCATION {  
   public uint   bpLocationType;  
   public IntPtr unionmember1;  
   public IntPtr unionmember2;  
   public IntPtr unionmember3;  
   public IntPtr unionmember4;  
};  
```  
  
## <a name="members"></a>Membros  
 `bpLocationType`  
 Um valor da enumeração [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md) usada para interpretar a `bpLocation` União ou os `unionmemberX` Membros.  
  
 `bpLocation`.`bplocCodeFileLine`  
 [Somente C++] Contém a estrutura de [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md) se `bpLocationType`  =  `BPLT_CODE_FILE_LINE` .  
  
 `bpLocation.bplocCodeFuncOffset`  
 [Somente C++] Contém a estrutura de [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md) se `bpLocationType`  =  `BPLT_CODE_FUNC_OFFSET` .  
  
 `bpLocation.bplocCodeContext`  
 [Somente C++] Contém a estrutura de [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md) se `bpLocationType`  =  `BPLT_CODE_CONTEXT` .  
  
 `bpLocation.bplocCodeString`  
 [Somente C++] Contém a estrutura de [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md) se `bpLocationType`  =  `BPLT_CODE_STRING` .  
  
 `bpLocation.bplocCodeAddress`  
 [Somente C++] Contém a estrutura de [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md) se `bpLocationType`  =  `BPLT_CODE_ADDRESS` .  
  
 `bpLocation.bplocDataString`  
 [Somente C++] Contém a estrutura de [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md) se `bpLocationType`  =  `BPLT_DATA_STRING` .  
  
 `bpLocation.bplocResolution`  
 [Somente C++] Contém a estrutura de [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md) se `bpLocationType`  =  `BPLT_RESOLUTION` .  
  
 `unionmember1`  
 [Somente C#] Consulte comentários sobre como interpretar.  
  
 `unionmember2`  
 [Somente C#] Consulte comentários sobre como interpretar.  
  
 `unionmember3`  
 [Somente C#] Consulte comentários sobre como interpretar.  
  
 `unionmember4`  
 [Somente C#] Consulte comentários sobre como interpretar.  
  
## <a name="remarks"></a>Comentários  
 Essa estrutura é um membro das estruturas [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) e [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) .  
  
 [Somente C#] Os `unionmemberX` Membros são interpretados de acordo com a tabela a seguir. Procure a coluna à esquerda do `bpLocationType` valor e, em seguida, examine as outras colunas para determinar o que cada `unionmemberX` membro representa e Marshale de `unionmemberX` acordo. Consulte o exemplo de uma maneira de interpretar uma parte dessa estrutura em C#.  
  
|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|  
|----------------------|--------------------|--------------------|--------------------|--------------------|  
|`BPLT_CODE_FILE_LINE`|`string` (um contexto)|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|-|-|  
|`BPLT_CODE_FUNC_OFFSET`|`string` (um contexto)|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|-|-|  
|`BPLT_CODE_CONTEXT`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|  
|`BPLT_CODE_STRING`|`string` (um contexto)|`string` (expressão condicional)|-|-|  
|`BPLT_CODE_ADDRESS`|`string` (um contexto)|`string` (URL do módulo)|`string` (nome da função)|`string` corrigir|  
|`BPLT_DATA_STRING`|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|`string` (um contexto)|`string` (expressão de dados)|`uint` (número de elementos)|  
|`BPLT_RESOLUTION`|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|-|-|-|  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra como interpretar a `BP_LOCATION` estrutura em C# para o `BPLT_DATA_STRING` tipo. Esse tipo específico mostra como interpretar todos os quatro `unionmemberX` Membros em todos os formatos possíveis (objeto, Cadeia de caracteres e número).  
  
```csharp  
using System;  
using System.Runtime.Interop.Services;  
using Microsoft.VisualStudio.Debugger.Interop;  
  
namespace MyPackage  
{  
    public class MyClass  
    {  
        public void Interpret(BP_LOCATION bp)  
        {  
            if (bp.bpLocationType == (uint)enum_BP_LOCATION_TYPE.BPLT_DATA_STRING)  
            {  
                 IDebugThread2 pThread = (IDebugThread2)Marshal.GetObjectForIUnknown(bp.unionmember1);  
                 string context = Marshal.PtrToStringBSTR(bp.unionmember2);  
                 string dataExpression = Marshal.PtrToStringBSTR(bp.unionmember3);  
                 uint numElements = (uint)Marshal.ReadInt32(bp.unionmember4);  
            }  
        }  
    }  
}  
```  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg. h  
  
 Namespace: Microsoft. VisualStudio. Debugger. Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte Também  
 [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)   
 [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)   
 [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)   
 [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)   
 [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)   
 [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)   
 [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)   
 [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)

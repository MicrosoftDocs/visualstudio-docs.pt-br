---
title: DisplayKind | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- DisplayKind enumeration
ms.assetid: 940968c5-6065-4bda-8ee6-c31597db4d71
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 10bed6b3398b93b0776876491d812ec36c9e9e04
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198814"
---
# <a name="displaykind"></a>DisplayKind
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Enumera os valores válidos que representam os tipos de informações para levar de uma [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) de objeto e exibir para o usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
enum enum_DisplayKind  
{  
   DisplayKind_Value = 0x1,  
   DisplayKind_Name = 0x2,  
   DisplayKind_Type = 0x3,  
};  
typedef DWORD DisplayKind;  
```  
  
```csharp  
public enum enum_DisplayKind  
{  
   DisplayKind_Value = 0x1,  
   DisplayKind_Name = 0x2,  
   DisplayKind_Type = 0x3,  
};  
```  
  
#### <a name="parameters"></a>Parâmetros  
 DisplayKind_Value  
 Valor do campo.  
  
 DisplayKind_Name  
 Nome do campo.  
  
 DisplayKind_Type  
 Tipo de campo.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: EE.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetValueDisplayStringCount](../../../extensibility/debugger/reference/ieevisualizerservice-getvaluedisplaystringcount.md)

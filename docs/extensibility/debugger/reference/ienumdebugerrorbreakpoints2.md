---
title: IEnumDebugErrorBreakpoints2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IEnumDebugErrorBreakpoints2
helpviewer_keywords:
- IEnumDebugErrorBreakpoints2
ms.assetid: ffdad73d-969a-45ef-9ad1-7f5d3b814018
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1860b1baf5f5c42b5cf27d4521b29230d447ceae
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31125041"
---
# <a name="ienumdebugerrorbreakpoints2"></a>IEnumDebugErrorBreakpoints2
Essa interface enumera os pontos de interrupção de erro associados a um ponto de interrupção pendente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IEnumDebugErrorBreakpoints2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O mecanismo de depuração (DE) implementa essa interface como parte de seu suporte para pontos de interrupção.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Chamadas do Visual Studio [CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md) para obter essa interface que representa uma lista de pontos de interrupção não pode ser vinculado, ou [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md) para obter essa interface que representa uma lista de pontos de interrupção que não foram vinculados.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IEnumDebugErrorBreakpoints2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[Avançar](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-next.md)|Recupera um número especificado de pontos de interrupção de erro em uma sequência de enumeração.|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-skip.md)|Ignora um número especificado de pontos de interrupção de erro em uma sequência de enumeração.|  
|[Redefinir](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-reset.md)|Redefine uma sequência de enumeração para o início.|  
|[Clone](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração do enumerador atual.|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-getcount.md)|Obtém o número de pontos de interrupção de erro em um enumerador.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface contém uma lista de [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) interfaces, cada um deles descreve um ponto de interrupção que não pôde ser associado e por que ele não pôde ser associado. O Visual Studio usa o `IEnumDebugErrorBreakpoint2` interface para atualizar os pontos de interrupção mostrados no IDE.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de núcleo](../../../extensibility/debugger/reference/core-interfaces.md)   
 [CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)   
 [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)   
 [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
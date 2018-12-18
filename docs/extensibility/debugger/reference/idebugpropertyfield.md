---
title: IDebugPropertyField | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugPropertyField
helpviewer_keywords:
- IDebugPropertyField interface
ms.assetid: b50edb2c-fb8d-4def-993d-17d23d2027c1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 26b876b19d5242bb90a3d13f255f9245fe14f93a
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31119978"
---
# <a name="idebugpropertyfield"></a>IDebugPropertyField
Essa interface fornece as funções que permitem obter e definir uma propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugPropertyField : IDebugContainerField  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Um provedor de símbolo implementa essa interface no mesmo objeto que implementa o [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md). Esta interface é uma especialização que oferece suporte ao conceito de propriedades em uma classe.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Use [QueryInterface](/cpp/atl/queryinterface) para obter essa interface do [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) interface se o [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) método retornará `FIELD_KIND_PROP`.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 Além dos métodos de [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) e [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) interfaces, essa interface implementa os métodos a seguir:  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)|Obtém o método que obtém a propriedade.|  
|[GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)|Obtém o método que define a propriedade.|  
  
## <a name="remarks"></a>Comentários  
 Uma propriedade é um conceito de código gerenciado e representa um método que é tratado como uma variável. Propriedades não existem em C++ não gerenciado.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: sh.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de provedor de símbolo](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
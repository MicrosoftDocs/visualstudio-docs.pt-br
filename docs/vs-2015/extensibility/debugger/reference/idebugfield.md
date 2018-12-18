---
title: IDebugField | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugField
helpviewer_keywords:
- IDebugField interface
ms.assetid: adecdd1c-b1b9-4027-92da-74cbe910636f
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 4feaec188bcfcfbca9f6484e162f1c3e6ad22d67
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764985"
---
# <a name="idebugfield"></a>IDebugField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa interface representa um campo, ou seja, uma descrição de um tipo ou um símbolo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugField : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Um provedor de símbolo implementa essa interface como a classe base para todos os campos.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Essa interface é a classe base para todos os campos. Com base no valor de retorno [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md), essa interface pode retornar mais especializadas interfaces usando [QueryInterface](http://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3). Além disso, várias interfaces de retorno `IDebugField` objetos de vários métodos.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugField`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)|Obtém as informações que pode ser exibidas sobre o símbolo ou um tipo.|  
|[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)|Obtém o tipo de campo.|  
|[GetType](../../../extensibility/debugger/reference/idebugfield-gettype.md)|Obtém o tipo de campo.|  
|[GetContainer](../../../extensibility/debugger/reference/idebugfield-getcontainer.md)|Obtém o contêiner do campo.|  
|[GetAddress](../../../extensibility/debugger/reference/idebugfield-getaddress.md)|Obtém o endereço do campo.|  
|[GetSize](../../../extensibility/debugger/reference/idebugfield-getsize.md)|Obtém o tamanho de um campo, em bytes.|  
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugfield-getextendedinfo.md)|Obtém informações estendidas sobre um campo.|  
|[Igual](../../../extensibility/debugger/reference/idebugfield-equal.md)|Compara dois campos.|  
|[GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)|Obtém informações de tipo independente sobre o símbolo ou um tipo.|  
  
## <a name="remarks"></a>Comentários  
 Um tipo é equivalente a uma linguagem C `typedef`.  
  
 No exemplo a seguir language de C++, `weather` é um tipo de classe, e `sunny` e `stormy` são símbolos:  
  
```cpp#  
class weather;  
weather sunny;  
weather stormy;  
```  
  
 Se um campo representa um símbolo ou tipo pode ser determinado chamando [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) e examinando a [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) resultado. Se o `FIELD_KIND_TYPE` bit estiver definido, o campo é um tipo e se o `FIELD_KIND_SYMBOL` bit estiver definido, ele é um símbolo.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: sh.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de Provedor de Símbolos](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)


---
description: Essa interface representa uma classe como um tipo.
title: IDebugClassField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField
helpviewer_keywords:
- IDebugClassField interface
ms.assetid: 49358cbc-8973-4862-9dcc-79b1248e6712
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1c8f566d7decc344dda17700da6712ff78120a1c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102164169"
---
# <a name="idebugclassfield"></a>IDebugClassField
Essa interface representa uma classe como um tipo.

## <a name="syntax"></a>Sintaxe

```
IDebugClassField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um provedor de símbolo implementa essa interface no mesmo objeto que implementa a interface [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) . Essa interface é uma especialização que representa um tipo de classe.

## <a name="notes-for-callers"></a>Observações para chamadores
 Várias interfaces têm métodos que podem retornar essa interface, incluindo [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md), [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)e [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md). Além disso, você pode usar [QueryInterface](/cpp/atl/queryinterface) para obter essa interface da interface [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) se o método [getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md) retornar o sinalizador `FIELD_TYPE_CLASS` .

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos nas interfaces [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) e [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) , essa interface implementa o seguinte:

|Método|Descrição|
|------------|-----------------|
|[EnumBaseClasses](../../../extensibility/debugger/reference/idebugclassfield-enumbaseclasses.md)|Cria um enumerador para as classes base dessa classe.|
|[DoesInterfaceExist](../../../extensibility/debugger/reference/idebugclassfield-doesinterfaceexist.md)|Determina se uma interface específica está definida na classe.|
|[EnumNestedClasses](../../../extensibility/debugger/reference/idebugclassfield-enumnestedclasses.md)|Cria um enumerador para as classes aninhadas dessa classe.|
|[GetEnclosingClass](../../../extensibility/debugger/reference/idebugclassfield-getenclosingclass.md)|Obtém a classe que inclui essa classe.|
|[EnumInterfacesImplemented](../../../extensibility/debugger/reference/idebugclassfield-enuminterfacesimplemented.md)|Cria um enumerador para as interfaces implementadas por essa classe.|
|[EnumConstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)|Cria um enumerador para os construtores dessa classe.|
|[GetDefaultIndexer](../../../extensibility/debugger/reference/idebugclassfield-getdefaultindexer.md)|Obtém o nome do indexador padrão.|
|[EnumNestedEnums](../../../extensibility/debugger/reference/idebugclassfield-enumnestedenums.md)|Cria um enumerador para os enumeradores aninhados dessa classe.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de provedor de símbolos](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)

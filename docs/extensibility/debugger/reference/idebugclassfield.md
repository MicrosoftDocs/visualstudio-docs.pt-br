---
title: IDebugClassField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField
helpviewer_keywords:
- IDebugClassField interface
ms.assetid: 49358cbc-8973-4862-9dcc-79b1248e6712
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 681a426cc95ead710fbb8dab151bb5a23b6f1206
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62922590"
---
# <a name="idebugclassfield"></a>IDebugClassField
Essa interface representa uma classe como um tipo.

## <a name="syntax"></a>Sintaxe

```
IDebugClassField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>Observações para implementadores
 Um provedor de símbolo implementa essa interface no mesmo objeto que implementa o [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) interface. Essa interface é uma especialização que representa um tipo de classe.

## <a name="notes-for-callers"></a>Observações para chamadores
 Um número de interfaces têm métodos que podem retornar a essa interface, incluindo [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md), [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md), e [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md). Além disso, você pode usar [QueryInterface](/cpp/atl/queryinterface) para obter essa interface da [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) interface se o [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) método retorna o sinalizador `FIELD_TYPE_CLASS`.

## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable
 Além dos métodos na [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) e [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) interfaces, essa interface implementa o seguinte:

|Método|Descrição|
|------------|-----------------|
|[EnumBaseClasses](../../../extensibility/debugger/reference/idebugclassfield-enumbaseclasses.md)|Cria um enumerador para as classes base dessa classe.|
|[DoesInterfaceExist](../../../extensibility/debugger/reference/idebugclassfield-doesinterfaceexist.md)|Determina se uma interface específica é definida na classe.|
|[EnumNestedClasses](../../../extensibility/debugger/reference/idebugclassfield-enumnestedclasses.md)|Cria um enumerador para as classes aninhadas dessa classe.|
|[GetEnclosingClass](../../../extensibility/debugger/reference/idebugclassfield-getenclosingclass.md)|Obtém a classe que engloba essa classe.|
|[EnumInterfacesImplemented](../../../extensibility/debugger/reference/idebugclassfield-enuminterfacesimplemented.md)|Cria um enumerador para as interfaces implementadas por esta classe.|
|[EnumConstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)|Cria um enumerador para os construtores dessa classe.|
|[GetDefaultIndexer](../../../extensibility/debugger/reference/idebugclassfield-getdefaultindexer.md)|Obtém o nome do indexador padrão.|
|[EnumNestedEnums](../../../extensibility/debugger/reference/idebugclassfield-enumnestedenums.md)|Cria um enumerador para os enumeradores aninhados dessa classe.|

## <a name="requirements"></a>Requisitos
 Header: sh.h

 Namespace: Microsoft.VisualStudio.Debugger.Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
- [Interfaces de Provedor de Símbolos](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
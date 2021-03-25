---
title: IDebugProperty3 | Microsoft Docs
description: Essa interface fornece suporte para recuperar uma cadeia de caracteres longa e arbitrariamente associada à propriedade, associando uma ID exclusiva à propriedade, recuperando uma lista de visualizadores personalizados para a propriedade, definindo o valor de uma propriedade com a capacidade de relatar quaisquer erros resultantes.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3
helpviewer_keywords:
- IDebugProperty3 interface
ms.assetid: 8f9be68d-4490-4eca-8f6b-8a10ed77e226
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 933810ac5b1e0ba34edf7cfe8d4303180c862fe2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083902"
---
# <a name="idebugproperty3"></a>IDebugProperty3
Esta interface fornece suporte para:

- Recuperando uma cadeia de caracteres extensa arbitrariamente associada à propriedade.

- Associando uma ID exclusiva à propriedade.

- Recuperando uma lista de visualizadores personalizados para a propriedade.

- Definindo o valor de uma propriedade com a capacidade de relatar quaisquer erros resultantes

## <a name="syntax"></a>Sintaxe

```
IDebugProperty3 : IDebugProperty2
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface no mesmo objeto que implementa o [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) para fornecer suporte para cadeias de caracteres longas, IDs de propriedade e visualizadores personalizados.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [QueryInterface](/cpp/atl/queryinterface) em uma `IDebugProperty2` interface para obter essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos herdados do `IDebugProperty2` , a `IDebugProperty3` interface expõe os métodos a seguir.

|Método|Descrição|
|------------|-----------------|
|[GetStringCharLength](../../../extensibility/debugger/reference/idebugproperty3-getstringcharlength.md)|Retorna o comprimento da cadeia de caracteres associada à propriedade.|
|[GetStringChars](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md)|Retorna a cadeia de caracteres em um buffer fornecido pelo usuário.|
|[CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)|Cria uma ID exclusiva para essa propriedade.|
|[DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)|Destrói a ID exclusiva dessa propriedade.|
|[GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)|Retorna o número de visualizadores personalizados com os quais essa propriedade pode ser exibida.|
|[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)|Retorna a lista de visualizadores personalizados com os quais essa propriedade pode ser exibida.|
|[SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)|Define o valor dessa propriedade, retornando uma mensagem de erro se algo deu errado.|

## <a name="remarks"></a>Comentários
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md) é a maneira preferida para o SDM (Gerenciador de depuração de sessão) definir o valor de uma propriedade.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)

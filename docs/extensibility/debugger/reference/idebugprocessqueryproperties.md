---
description: Essa interface é uma interface de extensão implementada por implementadores de IDebugProcess2.
title: IDebugProcessQueryProperties | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties
ms.assetid: ce29a248-81a0-42c0-99a7-1606e8c548ec
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8205b96723a1b48da46e6e19162c50139c9fe71d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166210"
---
# <a name="idebugprocessqueryproperties"></a>IDebugProcessQueryProperties
Essa interface é uma interface de extensão implementada por implementadores de [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) . Ele permite que o implementador Obtenha informações sobre o ambiente de processo de depuração.

## <a name="syntax"></a>Sintaxe

```
IDebugProcessQueryProperties: IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Implemente essa interface para obter informações sobre o ambiente de execução de um processo de depuração.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugProcessQueryProperties` .

|Método|Descrição|
|------------|-----------------|
|[QueryProperty](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperty.md)|Consulta um valor de propriedade.|
|[QueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperties.md)|Consultas de valores de propriedade.|

## <a name="remarks"></a>Comentários
 Essa interface raramente é implementada.

## <a name="requirements"></a>Requisitos
 Cabeçalho: Portpriv. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)

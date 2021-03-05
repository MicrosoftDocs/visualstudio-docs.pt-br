---
description: Essa interface é usada para representar e obter informações de um servidor em um computador na rede.
title: IDebugCoreServer2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2
helpviewer_keywords:
- IDebugCoreServer2 interface
ms.assetid: 9c47d0a6-9eb1-464e-bd44-fa2b552d4d36
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 871f7ea5671fa4f3c615d84e0591bd331f945ccc
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102163129"
---
# <a name="idebugcoreserver2"></a>IDebugCoreServer2
Essa interface é usada para representar e obter informações de um servidor em um computador na rede.

## <a name="syntax"></a>Sintaxe

```
IDebugCoreServer2 : IUknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O Visual Studio implementa essa interface para representar um servidor. Cada instância do Visual Studio cria uma instância dessa interface.

## <a name="notes-for-callers"></a>Observações para chamadores
 Um fornecedor de porta personalizado recebe essa interface em uma chamada para [evento](../../../extensibility/debugger/reference/idebugportevents2-event.md).

 Um mecanismo de depuração pode obter essa interface indiretamente por meio de uma chamada para [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md) (que retorna [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md), uma interface derivada de `IDebugCoreServer2` ).

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugCoreServer2` .

|Método|Descrição|
|------------|-----------------|
|[GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)|Obtém o nome e os atributos de um computador.|
|[GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)|Obtém o nome de um computador.|
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)|Obtém um fornecedor de porta que existe em um computador.|
|[GetPort](../../../extensibility/debugger/reference/idebugcoreserver2-getport.md)|Obtém uma porta que já existe em um computador.|
|[EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)|Cria um enumerador para todas as portas em um computador.|
|[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)|Cria um enumerador para todos os fornecedores de porta em um computador.|
|[GetMachineUtilities_V7](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineutilities-v7.md)|Obtém os utilitários de máquina para um computador.|

## <a name="remarks"></a>Comentários
 Essa interface também é usada pelo Visual Studio para procurar processos em execução em computadores na rede.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [Evento](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)

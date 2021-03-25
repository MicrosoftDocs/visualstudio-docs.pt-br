---
description: Essa interface representa uma porta de depuração em um computador.
title: IDebugPort2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2
helpviewer_keywords:
- IDebugPort2 interface
ms.assetid: 8fd87f05-a950-4d14-b925-98be29d4facc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4d0b173f362418171def93ee92e3883b2910ad18
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087334"
---
# <a name="idebugport2"></a>IDebugPort2
Essa interface representa uma porta de depuração em um computador.

## <a name="syntax"></a>Sintaxe

```
IDebugPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um fornecedor de porta personalizado implementa essa interface para representar uma porta de depuração em um computador.

 Se a porta der suporte ao envio de eventos de porta, ela também deverá implementar a <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> interface para dar suporte a uma <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> interface que, por sua vez, fornece a interface [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) .

## <a name="notes-for-callers"></a>Observações para chamadores
 As chamadas para [GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md) ou [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) retornam essa interface, representando a porta solicitada.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugPort2` .

|Método|Descrição|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugport2-getportname.md)|Retorna o nome da porta.|
|[GetPortId](../../../extensibility/debugger/reference/idebugport2-getportid.md)|Retorna o identificador de porta.|
|[GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)|Retorna a solicitação usada para criar uma porta (se disponível).|
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)|Retorna o fornecedor da porta para esta porta.|
|[GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)|Retorna uma interface para o processo de acordo com o identificador do processo.|
|[EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)|Enumera todos os processos em execução em uma porta.|

## <a name="remarks"></a>Comentários
 A porta local fornece acesso a todos os processos e programas em execução no computador local. Outras portas podem representar uma conexão de cabo serial com um dispositivo baseado em Windows CE ou uma conexão de rede com um computador não DCOM. A `IDebugPort2` interface é usada para localizar o nome e o identificador de uma porta e enumerar todos os processos em execução na porta. Recursos para inicialização e encerramento de processos na porta são implementados na `IDebugPortEx2` interface.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)

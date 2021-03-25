---
description: Representa uma soma de verificação de documento para uma solicitação de ponto de interrupção.
title: IDebugBreakpointChecksumRequest2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBreakpointChecksumRequest2 interface
ms.assetid: 9cfdbca5-052c-48e9-8411-e2e9e4065d00
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 78361429e371bf19ee1fea27c090af80c2b79b73
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078078"
---
# <a name="idebugbreakpointchecksumrequest2"></a>IDebugBreakpointChecksumRequest2
Representa uma soma de verificação de documento para uma solicitação de ponto de interrupção.

## <a name="syntax"></a>Sintaxe

```
IDebugBreakpointChecksumRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Implementado pelo [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] pacote de depuração e consumido pelos mecanismos de depuração.

## <a name="methods"></a>Métodos
 A tabela a seguir mostra os métodos de `IDebugBreakpointChecksumRequest2` .

|Método|Descrição|
|------------|-----------------|
|[GetChecksum](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2-getchecksum.md)|Recupera a soma de verificação do documento para uma solicitação de ponto de interrupção, dado o identificador exclusivo do algoritmo de soma de verificação a ser usado.|
|[IsChecksumEnabled](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2-ischecksumenabled.md)|Determina se a soma de verificação está habilitada para este documento.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

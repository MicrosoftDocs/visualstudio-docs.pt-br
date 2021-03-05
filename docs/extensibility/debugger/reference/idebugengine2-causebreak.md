---
description: Solicita que todos os programas que estão sendo depurados por esse mecanismo de depuração (DE) interrompam a execução na próxima vez que um de seus threads tentarem ser executados.
title: 'IDebugEngine2:: CauseBreak | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::CauseBreak
helpviewer_keywords:
- IDebugEngine2::CauseBreak
ms.assetid: 17fe4698-b04e-4798-8412-80e0da60c387
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 344ca2e9e9758aaca5a2c1e6784a36467abde73c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162700"
---
# <a name="idebugengine2causebreak"></a>IDebugEngine2::CauseBreak
Solicita que todos os programas que estão sendo depurados por esse mecanismo de depuração (DE) interrompam a execução na próxima vez que um de seus threads tentarem ser executados.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CauseBreak( 
   void 
);
```

```csharp
int CauseBreak();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Este método é assíncrono: um evento [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) é enviado quando o programa tenta executar novamente depois que esse método é chamado.

## <a name="see-also"></a>Confira também
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)

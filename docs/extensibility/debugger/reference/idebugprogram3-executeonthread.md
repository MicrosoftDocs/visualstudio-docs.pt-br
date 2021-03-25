---
description: Executa o programa depurador.
title: 'IDebugProgram3:: ExecuteOnThread | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3::ExecuteOnThread
ms.assetid: 2f5211e3-7a3f-47bf-9595-dfc8b4895d0d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a86bca6aa26a6bb364e9d704e79f57cef8f55395
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084383"
---
# <a name="idebugprogram3executeonthread"></a>IDebugProgram3::ExecuteOnThread
Executa o programa depurador. O thread é retornado para fornecer as informações do depurador sobre qual thread o usuário está visualizando ao executar o programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT ExecuteOnThread(
   [in] IDebugThread2* pThread)
```

```csharp
int ExecuteOnThread(
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>Parâmetros
`pThread`\
no Um objeto [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Há três maneiras diferentes pelas quais um depurador pode retomar a execução após a interrupção:

- Execute: cancele qualquer etapa anterior e execute até o próximo ponto de interrupção e assim por diante.

- Etapa: cancele qualquer etapa antiga e execute até que a nova etapa seja concluída.

- Continuar: executar novamente e deixar qualquer etapa antiga ativa.

  O thread passado para `ExecuteOnThread` é útil ao decidir qual etapa cancelar. Se você não souber o thread, a execução de execute cancela todas as etapas. Com o conhecimento do thread, você só precisa cancelar a etapa no thread ativo.

## <a name="see-also"></a>Confira também
- [Executar](../../../extensibility/debugger/reference/idebugprogram2-execute.md)
- [IDebugProgram3](../../../extensibility/debugger/reference/idebugprogram3.md)

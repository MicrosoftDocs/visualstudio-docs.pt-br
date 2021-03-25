---
description: 'IDebugProgram2:: execute continua executando este programa a partir de um estado parado. Qualquer estado de execução anterior (como uma etapa) é limpo e o programa começa a ser executado novamente.'
title: 'IDebugProgram2:: execute | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Execute
helpviewer_keywords:
- IDebugProgram2::Execute
ms.assetid: f7205ce8-0ac6-4fcd-b6ec-b720b4fcaccf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6112dbf51664458bc2d592951dcc842d1352020b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075985"
---
# <a name="idebugprogram2execute"></a>IDebugProgram2::Execute
Continua executando este programa a partir de um estado parado. Qualquer estado de execução anterior (como uma etapa) é limpo e o programa começa a ser executado novamente.

> [!NOTE]
> Esse método é preterido. Em vez disso, use o método [Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md) .

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Execute(
   void
);
```

```csharp
int Execute();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Quando o usuário inicia a execução de um estado parado em algum outro thread do programa, esse método é chamado neste programa. Esse método também é chamado quando o usuário seleciona o comando **Iniciar** no menu **depurar** no IDE. A implementação desse método pode ser tão simples quanto chamar o método [resume](../../../extensibility/debugger/reference/idebugthread2-resume.md) no thread atual do programa.

> [!WARNING]
> Não enviar um evento de interrupção ou um evento imediato (síncrono) para [evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) ao lidar com essa chamada; caso contrário, o depurador pode parar de responder.

## <a name="see-also"></a>Confira também
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [Evento](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Retomar](../../../extensibility/debugger/reference/idebugthread2-resume.md)

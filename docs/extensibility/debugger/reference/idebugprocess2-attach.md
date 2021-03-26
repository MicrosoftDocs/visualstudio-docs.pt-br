---
description: Anexa o SDM (Gerenciador de depuração de sessão) ao processo.
title: 'IDebugProcess2:: Attach | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Attach
helpviewer_keywords:
- IDebugProcess2::Attach
ms.assetid: 40d78417-fde2-45c3-96c9-16e06bd9008d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c518a91ae6b6de32926f922d55943d7d950b4013
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071695"
---
# <a name="idebugprocess2attach"></a>IDebugProcess2::Attach
Anexa o SDM (Gerenciador de depuração de sessão) ao processo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   GUID*                 rgguidSpecificEngines,
   DWORD                 celtSpecificEngines,
   HRESULT*              rghrEngineAttach
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   Guid[]               rgguidSpecificEngines,
   uint                 celtSpecificEngines,
   int[]                rghrEngineAttach
);
```

## <a name="parameters"></a>Parâmetros
`pCallback`\
no Um objeto [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) que é usado para a notificação de evento de depuração.

`rgguidSpecificEngines`\
no Uma matriz de GUIDs de mecanismos de depuração a ser usada para depurar programas em execução no processo. Esse parâmetro pode ser um valor nulo. Consulte Comentários para obter detalhes.

`celtSpecificEngines`\
no O número de mecanismos de depuração na `rgguidSpecificEngines` matriz e o tamanho da `rghrEngineAttach` matriz.

`rghrEngineAttach`\
[entrada, saída] Uma matriz de códigos HRESULT retornados pelos mecanismos de depuração. O tamanho dessa matriz é especificado no `celtSpecificEngines` parâmetro. Cada código costuma ser `S_OK` ou `S_ATTACH_DEFERRED` . O segundo indica que o DE está conectado no momento a nenhum programa.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. A tabela a seguir mostra outros valores possíveis.

|Valor|Descrição|
|-----------|-----------------|
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|O processo especificado já está anexado ao depurador.|
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|Ocorreu uma violação de segurança durante o procedimento de anexação.|
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|Um processo de área de trabalho não pode ser anexado ao depurador.|

## <a name="remarks"></a>Comentários
 Anexar a um processo anexa o SDM a todos os programas em execução nesse processo que podem ser depurados pelos mecanismos de depuração especificados na `rgguidSpecificEngines` matriz. Defina o `rgguidSpecificEngines` parâmetro como um valor nulo ou inclua `GUID_NULL` na matriz para anexar a todos os programas no processo.

 Todos os eventos de depuração que ocorrem no processo são enviados para o objeto [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) fornecido. Esse `IDebugEventCallback2` objeto é fornecido quando o SDM chama esse método.

## <a name="see-also"></a>Confira também
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

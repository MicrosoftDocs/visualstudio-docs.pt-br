---
description: Anexa um mecanismo DE depuração (DE) a um programa ou programas.
title: 'IDebugEngine2:: Attach | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::Attach
helpviewer_keywords:
- IDebugEngine2::Attach
ms.assetid: 173dcbda-5019-4c5e-bca9-a071838b5739
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a780ab04e693fd2868579efbf015aef25e0cca32
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160142"
---
# <a name="idebugengine2attach"></a>IDebugEngine2::Attach
Anexa um mecanismo DE depuração (DE) a um programa ou programas. Chamado pelo SDM (Gerenciador de depuração de sessão) quando o DE está em execução em processo para o SDM.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Attach( 
   IDebugProgram2**      pProgram,
   IDebugProgramNode2**  rgpProgramNodes,
   DWORD                 celtPrograms,
   IDebugEventCallback2* pCallback,
   ATTACH_REASON         dwReason
);
```

```csharp
int Attach( 
   IDebugProgram2[]     pProgram,
   IDebugProgramNode2[] rgpProgramNodes,
   uint                 celtPrograms,
   IDebugEventCallback2 pCallback,
   Enum_ATTACH_REASON   dwReason
);
```

## <a name="parameters"></a>Parâmetros
`pProgram`\
no Uma matriz de objetos [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que representam os programas a serem anexados. Esses são os programas de porta.

`rgpProgramNodes`\
no Uma matriz de objetos [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) que representam nós de programa, um para cada programa. Os nós de programa nessa matriz representam os mesmos programas que no `pProgram` . Os nós de programa são fornecidos para que o DE possa identificar os programas aos quais anexar.

`celtPrograms`\
no Número de programas e/ou nós de programa nas `pProgram` `rgpProgramNodes` matrizes e.

`pCallback`\
no O objeto [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) a ser usado para enviar eventos de depuração para o SDM.

`dwReason`\
no Um valor da enumeração [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) que especifica o motivo para anexar esses programas. Para obter mais informações, consulte a seção Comentários.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Há três motivos para anexar a um programa, da seguinte maneira:

- `ATTACH_REASON_LAUNCH` indica que o DE está anexando ao programa porque o usuário iniciou o processo que o contém.

- `ATTACH_REASON_USER` indica que o usuário solicitou explicitamente o DE para anexar a um programa (ou o processo que contém um programa).

- `ATTACH_REASON_AUTO` indica que DE está anexando a um programa específico porque ele já está depurando outros programas em um processo específico. Isso também é chamado de anexação automática.

  Quando esse método é chamado, o DE precisa enviar esses eventos em sequência:

1. [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) (se ainda não tiver sido enviado para uma determinada instância do mecanismo de depuração)

2. [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

3. [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)

   Além disso, se o motivo da anexação for `ATTACH_REASON_LAUNCH` , o de precisa enviar o evento [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) .

   Depois de obter o objeto [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) correspondente ao programa que está sendo depurado, ele pode ser consultado para qualquer interface privada.

   Antes de chamar os métodos de um nó de programa na matriz fornecida por `pProgram` ou `rgpProgramNodes` , a representação, se necessário, deve ser habilitada na `IDebugProgram2` interface que representa o nó do programa. Normalmente, no entanto, essa etapa não é necessária. Para obter mais informações, consulte [problemas de segurança](../../../extensibility/debugger/security-issues.md).

## <a name="see-also"></a>Confira também
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)

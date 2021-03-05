---
description: Recupera uma lista de programas em execução a partir de um processo especificado.
title: 'IDebugProgramProvider2:: GetProviderProcessData | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProcessData
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProcessData
ms.assetid: 90cf7b7f-53d2-487e-b793-94501a6e24dd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b878a6731a9a7f2bf58bf55530d0b5f83cc978de
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102151552"
---
# <a name="idebugprogramprovider2getproviderprocessdata"></a>IDebugProgramProvider2::GetProviderProcessData
Recupera uma lista de programas em execução a partir de um processo especificado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetProviderProcessData(
   PROVIDER_FLAGS         Flags,
   IDebugDefaultPort2*    pPort,
   AD_PROCESS_ID          processId,
   CONST_GUID_ARRAY       EngineFilter,
   PROVIDER_PROCESS_DATA* pProcess
);
```

```csharp
int GetProviderProcessData(
   enum_PROVIDER_FLAGS     Flags,
   IDebugDefaultPort2      pPort,
   AD_PROCESS_ID           ProcessId,
   CONST_GUID_ARRAY        EngineFilter,
   PROVIDER_PROCESS_DATA[] pProcess
);
```

## <a name="parameters"></a>Parâmetros
`Flags`\
no Uma combinação de sinalizadores da enumeração de [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md) . Os seguintes sinalizadores são típicos para esta chamada:

|Sinalizador|Descrição|
|----------|-----------------|
|`PFLAG_REMOTE_PORT`|O chamador está sendo executado no computador remoto.|
|`PFLAG_DEBUGGEE`|O chamador está sendo depurado no momento (informações adicionais sobre marshaling serão retornadas para cada nó).|
|`PFLAG_ATTACHED_TO_DEBUGGEE`|O chamador foi anexado a, mas não foi iniciado pelo depurador.|
|`PFLAG_GET_PROGRAM_NODES`|O chamador está solicitando uma lista de nós de programa a serem retornados.|

`pPort`\
no A porta em que o processo de chamada está sendo executado.

`processId`\
no Uma estrutura de [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) que mantém a ID do processo que contém o programa em questão.

`EngineFilter`\
no Uma matriz de GUIDs para mecanismos de depuração atribuídos para depurar esse processo (eles serão usados para filtrar os programas que são realmente retornados com base em quais mecanismos fornecidos oferecem suporte; se nenhum mecanismo for especificado, todos os programas serão retornados).

`pProcess`\
fora Uma estrutura de [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md) que é preenchida com as informações solicitadas.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é normalmente chamado por um processo para obter uma lista de programas em execução nesse processo. As informações retornadas são uma lista de objetos [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) .

## <a name="see-also"></a>Confira também
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)

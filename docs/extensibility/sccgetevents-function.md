---
description: Essa função recupera um evento de status enfileirado.
title: Função SccGetEvents | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetEvents
helpviewer_keywords:
- SccGetEvents function
ms.assetid: 32f8147d-6dcc-465e-b07b-42da5824f9b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e7611a3f71b5fa6205708aca6b957f3921a71517
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072982"
---
# <a name="sccgetevents-function"></a>Função SccGetEvents
Essa função recupera um evento de status enfileirado.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccGetEvents (
   LPVOID pvContext,
   LPSTR  lpFileName,
   LPLONG lpStatus,
   LPLONG pnEventsRemaining
);
```

### <a name="parameters"></a>Parâmetros
 pvContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 lpFileName

[entrada, saída] Buffer em que o plug-in de controle do código-fonte coloca o nome do arquivo retornado (até _MAX_PATH caracteres).

 lpStatus

[entrada, saída] Retorna o código de status (consulte o [código de status do arquivo](../extensibility/file-status-code-enumerator.md) para obter os valores possíveis).

 pnEventsRemaining

[entrada, saída] Retorna o número de entradas deixadas na fila após essa chamada. Se esse número for grande, o chamador poderá decidir chamar o [SccQueryInfo](../extensibility/sccqueryinfo-function.md) para obter todas as informações ao mesmo tempo.

## <a name="return-value"></a>Retornar valor
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Êxito ao obter eventos.|
|SCC_E_OPNOTSUPPORTED|Não há suporte para essa função.|
|SCC_E_NONSPECIFICERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Essa função é chamada durante o processamento de ociosidade para ver se houve alguma atualização de status para arquivos sob controle do código-fonte. O plug-in de controle do código-fonte mantém o status de todos os arquivos que ele conhece e sempre que uma alteração de status é observada pelo plug-in, o status e o arquivo associado são armazenados em uma fila. Quando `SccGetEvents` é chamado, o elemento superior da fila é recuperado e retornado. Essa função é restrita para retornar somente informações armazenadas anteriormente em cache e deve ter um retorno muito rápido (ou seja, nenhuma leitura do disco ou pedir o status do sistema de controle do código-fonte); caso contrário, o desempenho do IDE pode começar a degradar.

 Se não houver nenhuma atualização de status para relatar, o plug-in de controle do código-fonte armazenará uma cadeia de caracteres vazia no buffer apontado por `lpFileName` . Caso contrário, o plug-in armazena o nome do caminho completo do arquivo para o qual as informações de status foram alteradas e retorna o código de status apropriado (um dos valores detalhados no [código de status do arquivo](../extensibility/file-status-code-enumerator.md)).

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Código de status do arquivo](../extensibility/file-status-code-enumerator.md)

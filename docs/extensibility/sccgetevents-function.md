---
description: Essa função recupera um evento de status na fila.
title: Função SccGetEvents | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: 9438ac10301e2da43b26a88575e44a8ad2c0bf82
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901052"
---
# <a name="sccgetevents-function"></a>Função SccGetEvents
Essa função recupera um evento de status na fila.

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

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 Lpfilename

[in, out] Buffer em que o plug-in de controle do código-fonte coloca o nome de arquivo retornado (até _MAX_PATH caracteres).

 lpStatus

[in, out] Retorna o código de status (consulte [Código de status do arquivo](../extensibility/file-status-code-enumerator.md) para ver os valores possíveis).

 pnEventsRemaining

[in, out] Retorna o número de entradas deixadas na fila após essa chamada. Se esse número for grande, o chamador poderá decidir chamar [o SccQueryInfo](../extensibility/sccqueryinfo-function.md) para obter todas as informações de uma só vez.

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Obter eventos bem-sucedidos.|
|SCC_E_OPNOTSUPPORTED|Não há suporte para essa função.|
|SCC_E_NONSPECIFICERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Essa função é chamada durante o processamento ocioso para ver se houve atualizações de status para arquivos sob controle do código-fonte. O plug-in de controle do código-fonte mantém o status de todos os arquivos que ele conhece e sempre que uma alteração de status é notada pelo plug-in, o status e o arquivo associado são armazenados em uma fila. Quando `SccGetEvents` é chamado, o elemento superior da fila é recuperado e retornado. Essa função é restrita para retornar apenas informações armazenadas em cache anteriormente e deve ter uma solução alternativa muito rápida (ou seja, nenhuma leitura do disco ou solicitando status ao sistema de controle do código-fonte); caso contrário, o desempenho do IDE pode começar a degradar.

 Se não houver nenhuma atualização de status para relatar, o plug-in de controle do código-fonte armazenará uma cadeia de caracteres vazia no buffer apontado por `lpFileName` . Caso contrário, o plug-in armazenará o nome completo do caminho do arquivo para o qual as informações de status foram alteradas e retornará o código de status apropriado (um dos valores detalhados em Código de [status do arquivo](../extensibility/file-status-code-enumerator.md)).

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Código de status do arquivo](../extensibility/file-status-code-enumerator.md)

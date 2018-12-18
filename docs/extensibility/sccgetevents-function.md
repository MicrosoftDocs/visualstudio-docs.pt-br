---
title: Função SccGetEvents | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccGetEvents
helpviewer_keywords:
- SccGetEvents function
ms.assetid: 32f8147d-6dcc-465e-b07b-42da5824f9b0
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 981b3c9b0a03abfa13fedc7c62e77f02a425b248
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49896985"
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
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 lpFileName  
 [no, out] Buffer em que o plug-in de controle do código-fonte coloca o nome de arquivo retornado (até caracteres MAX_PATH).  
  
 lpStatus  
 [no, out] Retorna o código de status (consulte [arquivo de código de status](../extensibility/file-status-code-enumerator.md) para possíveis valores).  
  
 pnEventsRemaining  
 [no, out] Retorna o número de entradas deixada na fila após esta chamada. Se esse número for grande, o chamador poderá optar por chamar o [SccQueryInfo](../extensibility/sccqueryinfo-function.md) para obter as informações ao mesmo tempo.  
  
## <a name="return-value"></a>Valor retornado  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Obter eventos com êxito.|  
|SCC_E_OPNOTSUPPORTED|Não há suporte para essa função.|  
|SCC_E_NONSPECIFICERROR|Falha não específica.|  
  
## <a name="remarks"></a>Comentários  
 Essa função é chamada durante o processamento ocioso para ver se houve quaisquer atualizações de status para arquivos sob controle do código-fonte. O plug-in de controle do código-fonte mantém o status de todos os arquivos que ele conhece e sempre que uma alteração de status é observada pelo plug-in, o status e o arquivo associado são armazenados em uma fila. Quando `SccGetEvents` é chamado, a parte superior elemento da fila é recuperado e retornado. Essa função é restrito para retornar somente informações armazenadas em cache anteriormente e deve ter um retorno muito rápido (ou seja, nenhuma leitura do disco ou solicitando que o sistema de controle do código-fonte para o status); Caso contrário, o desempenho do IDE pode começar a ser degradada.  
  
 Se não houver nenhuma atualização de status do relatório, o plug-in de controle do código-fonte armazena uma cadeia de caracteres no buffer apontado por `lpFileName`. Caso contrário, o plug-in armazena o nome de caminho completo do arquivo para o qual as informações de status foi alterado e retorna o código de status apropriado (um dos valores detalhados em [arquivo de código de status](../extensibility/file-status-code-enumerator.md)).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in da controle de origem](../extensibility/source-control-plug-in-api-functions.md)   
 [Código de status do arquivo](../extensibility/file-status-code-enumerator.md)
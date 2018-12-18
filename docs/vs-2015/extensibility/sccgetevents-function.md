---
title: Função SccGetEvents | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SccGetEvents
helpviewer_keywords:
- SccGetEvents function
ms.assetid: 32f8147d-6dcc-465e-b07b-42da5824f9b0
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 821d8f565c4f8ebb926459da9031a055c6c7992f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51807056"
---
# <a name="sccgetevents-function"></a>Função SccGetEvents
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa função recupera um evento de status na fila.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
SCCRTN SccGetEvents (  
   LPVOID pvContext,  
   LPSTR  lpFileName,  
   LPLONG lpStatus,  
   LPLONG pnEventsRemaining  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 lpFileName  
 [no, out] Buffer em que o plug-in de controle do código-fonte coloca o nome de arquivo retornado (até caracteres MAX_PATH).  
  
 lpStatus  
 [no, out] Retorna o código de status (consulte [código de Status do arquivo](../extensibility/file-status-code-enumerator.md) para possíveis valores).  
  
 pnEventsRemaining  
 [no, out] Retorna o número de entradas deixada na fila após esta chamada. Se esse número for grande, o chamador poderá optar por chamar o [SccQueryInfo](../extensibility/sccqueryinfo-function.md) para obter as informações ao mesmo tempo.  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Obter eventos com êxito.|  
|SCC_E_OPNOTSUPPORTED|Não há suporte para essa função.|  
|SCC_E_NONSPECIFICERROR|Falha não específica.|  
  
## <a name="remarks"></a>Comentários  
 Essa função é chamada durante o processamento ocioso para ver se houve quaisquer atualizações de status para arquivos sob controle do código-fonte. O plug-in de controle do código-fonte mantém o status de todos os arquivos que ele conhece e sempre que uma alteração de status é observada pelo plug-in, o status e o arquivo associado são armazenados em uma fila. Quando `SccGetEvents` é chamado, a parte superior elemento da fila é recuperado e retornado. Essa função é restrito para retornar somente informações armazenadas em cache anteriormente e deve ter um retorno muito rápido (ou seja, nenhuma leitura do disco ou solicitando que o sistema de controle do código-fonte para o status); Caso contrário, o desempenho do IDE pode começar a ser degradada.  
  
 Se não houver nenhuma atualização de status do relatório, o plug-in de controle do código-fonte armazena uma cadeia de caracteres no buffer apontado por `lpFileName`. Caso contrário, o plug-in armazena o nome de caminho completo do arquivo para o qual as informações de status foi alterado e retorna o código de status apropriado (um dos valores detalhados em [código de Status do arquivo](../extensibility/file-status-code-enumerator.md)).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [Código de status do arquivo](../extensibility/file-status-code-enumerator.md)


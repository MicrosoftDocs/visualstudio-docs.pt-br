---
description: Essa função enumera uma determinada lista de arquivos, fornecendo informações sobre alterações de nome para cada arquivo por meio de uma função de retorno de chamada.
title: Função SccQueryChanges | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccQueryChanges
helpviewer_keywords:
- SccQueryChanges function
ms.assetid: 4cd58eb3-6952-49b1-9620-8682e3eaa604
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f93ed14671995502356ae4a19664b14bbd32ce7b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900467"
---
# <a name="sccquerychanges-function"></a>Função SccQueryChanges
Essa função enumera uma determinada lista de arquivos, fornecendo informações sobre alterações de nome para cada arquivo por meio de uma função de retorno de chamada.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccQueryChanges(
   LPVOID           pContext,
   LONG             nFiles,
   LPCSTR*          lpFileNames,
   QUERYCHANGESFUNC pfnCallback,
   LPVOID           pvCallerData
);
```

#### <a name="parameters"></a>Parâmetros
 pContext

[in] O ponteiro de contexto do plug-in do controle do código-fonte.

 nFiles

[in] Número de arquivos na `lpFileNames` matriz.

 lpFileNames

[in] Matriz de nomes de arquivo para obter informações.

 Pfncallback

[in] Função de retorno de chamada a ser chamada para cada nome de arquivo na lista (consulte [QUERYCHANGESFUNC para](../extensibility/querychangesfunc.md) obter detalhes).

 pvCallerData

[in] Valor que será passado inalterado para a função de retorno de chamada.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O processo de consulta foi concluído com êxito.|
|SCC_E_PROJNOTOPEN|O projeto não foi aberto no controle do código-fonte.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção.|
|SCC_E_NONSPECIFICERROR|Ocorreu um erro não especificado ou geral.|

## <a name="remarks"></a>Comentários
 As alterações que estão sendo consultadas são para o namespace: especificamente, renomeando, adicionando e removendo um arquivo.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)
- [Códigos de Erro](../extensibility/error-codes.md)

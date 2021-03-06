---
description: Essa função enumera uma determinada lista de arquivos, fornecendo informações sobre alterações de nome para cada arquivo por meio de uma função de retorno de chamada.
title: Função SccQueryChanges | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryChanges
helpviewer_keywords:
- SccQueryChanges function
ms.assetid: 4cd58eb3-6952-49b1-9620-8682e3eaa604
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e34c37ca999b05e7148d910032fe90c33470ce50
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102220515"
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

no O ponteiro de contexto do plug-in de controle do código-fonte.

 nFiles

no Número de arquivos na `lpFileNames` matriz.

 lpFileNames

no Matriz de nomes de arquivo para obter informações.

 pfnCallback

no Função de retorno de chamada para chamar cada nome de arquivo na lista (consulte [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md) para obter detalhes).

 pvCallerData

no Valor que será passado inalterado para a função de retorno de chamada.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O processo de consulta foi concluído com êxito.|
|SCC_E_PROJNOTOPEN|O projeto não foi aberto no controle do código-fonte.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção.|
|SCC_E_NONSPECIFICERROR|Ocorreu um erro não especificado ou geral.|

## <a name="remarks"></a>Comentários
 As alterações que estão sendo consultadas são para o namespace: especificamente, renomear, adicionar e remover um arquivo.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)
- [Códigos de Erro](../extensibility/error-codes.md)

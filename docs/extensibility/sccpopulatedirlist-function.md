---
description: Essa função determina quais diretórios e (opcionalmente) arquivos são armazenados no controle do código-fonte, considerando uma lista de diretórios a examinar.
title: Função SccPopulateDirList | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccPopulateDirList
helpviewer_keywords:
- SccPopulateDirList function
ms.assetid: dfff634b-b155-498b-a356-6eb252ac4fad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bf2620ff42106be7c858c5104dbf9cb2521252ab
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902352"
---
# <a name="sccpopulatedirlist-function"></a>Função SccPopulateDirList
Essa função determina quais diretórios e (opcionalmente) arquivos são armazenados no controle do código-fonte, considerando uma lista de diretórios a examinar.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccPopulateDirList(
   LPVOID        pContext,
   LONG          nDirs,
   LPCSTR*       lpDirPaths,
   POPDIRLISTFUNCpfnPopulate,
   LPVOID        pvCallerData,
   LONG          fOptions
);
```

#### <a name="parameters"></a>Parâmetros
 pContext

[in] O ponteiro de contexto do plug-in do controle do código-fonte.

 nDirs

[in] Número de caminhos de diretório na `lpDirPaths` matriz.

 lpDirPaths

[in] Matriz de caminhos de diretório a examinar.

 pfnPopulate

[in] Função de retorno de chamada para chamar para cada caminho de diretório e (opcionalmente) nome de arquivo em `lpDirPaths` (consulte [POPDIRLISTFUNC para](../extensibility/popdirlistfunc.md) obter detalhes).

 pvCallerData

[in] Valor que deve ser passado inalterado para a função de retorno de chamada.

 fOptions

[in] Uma combinação de valores que controlam como os diretórios são processados (consulte a seção "PopulateDirList flags" de [Bitflags Used by Specific Commands](../extensibility/bitflags-used-by-specific-commands.md) para ver os valores possíveis).

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Operação concluída com sucesso.|
|SCC_E_UNKNOWNERROR|Ocorreu um erro.|

## <a name="remarks"></a>Comentários
 Somente os diretórios e (opcionalmente) nomes de arquivo que estão realmente no repositório de controle do código-fonte são passados para a função de retorno de chamada.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Sinalizadores de bit usados por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md)
- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)
- [Códigos de Erro](../extensibility/error-codes.md)

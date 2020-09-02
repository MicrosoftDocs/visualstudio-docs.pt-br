---
title: Função SccPopulateDirList | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccPopulateDirList
helpviewer_keywords:
- SccPopulateDirList function
ms.assetid: dfff634b-b155-498b-a356-6eb252ac4fad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4ac1c51ac694acadd2efb0cd7d1c5a3f1d66ebc1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700563"
---
# <a name="sccpopulatedirlist-function"></a>Função SccPopulateDirList
Essa função determina quais diretórios e (opcionalmente) os arquivos são armazenados no controle do código-fonte, dadas uma lista de diretórios a serem examinados.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccPopulateDirList(
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

no O ponteiro de contexto do plug-in de controle do código-fonte.

 nDirs

no Número de caminhos de diretório na `lpDirPaths` matriz.

 lpDirPaths

no Matriz de caminhos de diretório a serem examinados.

 pfnPopulate

no Função de retorno de chamada para chamar cada caminho de diretório e (opcionalmente) nome de arquivo em `lpDirPaths` (consulte [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md) para obter detalhes).

 pvCallerData

no Valor que deve ser passado inalterado para a função de retorno de chamada.

 fOptions

no Uma combinação de valores que controlam como os diretórios são processados (consulte a seção "sinalizadores de PopulateDirList" do [Bitflags usado por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md) para os valores possíveis).

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Operação concluída com êxito.|
|SCC_E_UNKNOWNERROR|Ocorreu um erro.|

## <a name="remarks"></a>Comentários
 Somente os diretórios e (opcionalmente) os nomes de arquivo que estão na verdade no repositório do controle do código-fonte são passados para a função de retorno de chamada.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Sinalizadores de bit usados por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md)
- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)
- [Códigos de Erro](../extensibility/error-codes.md)

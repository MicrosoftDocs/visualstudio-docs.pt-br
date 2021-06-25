---
description: Essa função atualiza uma lista de arquivos para um comando de controle do código-fonte específico e fornece o status do controle do código-fonte em todos os arquivos determinados.
title: Função SccPopulateList | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccPopulateList
helpviewer_keywords:
- SccPopulateList function
ms.assetid: 7416e781-c571-4a7f-8af3-a089ce8be662
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b386c576b48e14b6118f62d451c42ac20f048b45
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902339"
---
# <a name="sccpopulatelist-function"></a>Função SccPopulateList
Essa função atualiza uma lista de arquivos para um comando de controle do código-fonte específico e fornece o status do controle do código-fonte em todos os arquivos determinados.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccPopulateList (
   LPVOID          pvContext,
   enum SCCCOMMAND nCommand,
   LONG            nFiles,
   LPCSTR*         lpFileNames,
   POPLISTFUNC     pfnPopulate,
   LPVOID          pvCallerData,
   LPLONG          lpStatus,
   LONG            fOptions
);
```

#### <a name="parameters"></a>Parâmetros
 pvContext

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 nCommand

[in] O comando de controle do código-fonte que será aplicado a todos os arquivos na matriz `lpFileNames` (consulte [Código de comando](../extensibility/command-code-enumerator.md) para ver uma lista de comandos possíveis).

 nFiles

[in] Número de arquivos na `lpFileNames` matriz.

 lpFileNames

[in] Uma matriz de nomes de arquivo conhecidos pelo IDE.

 pfnPopulate

[in] A função de retorno de chamada do IDE a ser chamada para adicionar e remover arquivos (consulte [POPLISTFUNC para](../extensibility/poplistfunc.md) obter detalhes).

 pvCallerData

[in] Valor que deve ser passado inalterado para a função de retorno de chamada.

 lpStatus

[in, out] Uma matriz para o plug-in de controle do código-fonte retornar os sinalizadores de status para cada arquivo.

 fOptions

[in] Sinalizadores de comando (consulte a seção "PopulateList flag" de [Bitflags Used by Specific Commands para](../extensibility/bitflags-used-by-specific-commands.md) obter detalhes).

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Sucesso.|
|SCC_E_NONSPECIFICERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Essa função examina a lista de arquivos para seu status atual. Ele usa a função de retorno de chamada para notificar o chamador quando `pfnPopulate` um arquivo não corresponder aos critérios do `nCommand` . Por exemplo, se o comando for e um arquivo na lista não for verificado, o retorno de chamada será usado `SCC_COMMAND_CHECKIN` para informar o chamador. Ocasionalmente, o plug-in de controle do código-fonte pode encontrar outros arquivos que podem fazer parte do comando e adicioná-los. Isso permite, por exemplo, que um usuário Visual Basic faça check-out de um arquivo .bmp que é usado por seu projeto, mas não aparece no arquivo Visual Basic projeto. Um usuário escolhe o **comando Get** no IDE. O IDE exibirá uma lista de todos os arquivos que ele acha que o usuário pode obter, mas antes que a lista seja mostrada, a função é chamada para garantir que a lista a ser exibida está `SccPopulateList` atualizada.

## <a name="example"></a>Exemplo
 O IDE cria uma lista de arquivos que ele acha que o usuário pode obter. Antes de exibir essa lista, ela chama a função , dando ao plug-in de controle do código-fonte a oportunidade de adicionar `SccPopulateList` e excluir arquivos da lista. O plug-in modifica a lista chamando a função de retorno de chamada determinada (consulte [POPLISTFUNC](../extensibility/poplistfunc.md) para obter mais detalhes).

 O plug-in continua a chamar a função , que adiciona e exclui arquivos, até que ele seja concluído e, em `pfnPopulate` seguida, retorne da `SccPopulateList` função. O IDE pode exibir sua lista. A `lpStatus` matriz representa todos os arquivos na lista original passados pelo IDE. O plug-in preenche o status de todos esses arquivos, além de fazer uso da função de retorno de chamada.

> [!NOTE]
> Um plug-in de controle do código-fonte sempre tem a opção de simplesmente retornar imediatamente dessa função, deixando a lista como está. Se um plug-in implementar essa função, ele poderá indicar isso definindo o bitflag de funcionalidade na primeira chamada `SCC_CAP_POPULATELIST` para [sccInitialize.](../extensibility/sccinitialize-function.md) Por padrão, o plug-in sempre deve assumir que todos os itens que estão sendo passados são arquivos. No entanto, se o IDE define o sinalizador no parâmetro , todos os itens que estão sendo passados `SCC_PL_DIR` `fOptions` devem ser considerados diretórios. O plug-in deve adicionar todos os arquivos que pertencem aos diretórios. O IDE nunca passará uma mistura de arquivos e diretórios.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
- [Sinalizadores de bit usados por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md)
- [Código de comando](../extensibility/command-code-enumerator.md)

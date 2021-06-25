---
description: Essa função recupera uma cópia de um ou mais arquivos para exibição e compilação, mas não para edição.
title: Função SccGet | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGet
helpviewer_keywords:
- SccGet function
ms.assetid: 09a18bd2-b788-411a-9da6-067d806e46f6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 805c19b0c326e8389b4e1905edf370ad042aac92
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904546"
---
# <a name="sccget-function"></a>Função SccGet
Essa função recupera uma cópia de um ou mais arquivos para exibição e compilação, mas não para edição. Na maioria dos sistemas, os arquivos são marcados como somente leitura.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccGet(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>Parâmetros
 pvContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 nFiles

no Número de arquivos especificados na `lpFileNames` matriz.

 lpFileNames

no Matriz de nomes totalmente qualificados de arquivos a serem recuperados.

 fOptions

no Sinalizadores de comando ( `SCC_GET_ALL` , `SCC_GET_RECURSIVE` ).

 pvOptions

no Opções específicas de plug-ins de controle do código-fonte.

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Êxito na operação get.|
|SCC_E_FILENOTCONTROLLED|O arquivo não está no controle do código-fonte.|
|SCC_E_OPNOTSUPPORTED|O sistema de controle do código-fonte não oferece suporte a essa operação.|
|SCC_E_FILEISCHECKEDOUT|Não é possível obter o arquivo que o usuário fez check-out no momento.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. Uma nova tentativa é recomendada.|
|SCC_E_NOSPECIFIEDVERSION|Especificou uma versão ou data/hora inválida.|
|SCC_E_NONSPECIFICERROR|Falha não específica; o arquivo não foi sincronizado.|
|SCC_I_OPERATIONCANCELED|Operação cancelada antes da conclusão.|
|SCC_E_NOTAUTHORIZED|O usuário não está autorizado a executar essa operação.|

## <a name="remarks"></a>Comentários
 Essa função é chamada com uma contagem e uma matriz de nomes dos arquivos a serem recuperados. Se o IDE passar o sinalizador `SCC_GET_ALL` , isso significa que os itens em `lpFileNames` não são arquivos, mas diretórios, e que todos os arquivos sob controle do código-fonte nos diretórios determinados devem ser recuperados.

 O `SCC_GET_ALL` sinalizador pode ser combinado com o `SCC_GET_RECURSIVE` sinalizador para recuperar todos os arquivos nos diretórios especificados e todos os subdiretórios também.

> [!NOTE]
> `SCC_GET_RECURSIVE` Nunca deve ser passado sem `SCC_GET_ALL` . Além disso, observe que, se os diretórios *C:\A* e *C:\A\B* forem passados em uma obtenção recursiva, *C:\A\B* e todos os seus subdiretórios serão realmente recuperados duas vezes. É responsabilidade do IDE, e não o plug-in de controle do código-fonte, para garantir que duplicatas como essa sejam mantidas fora da matriz.

 Por fim, mesmo que um plug-in de controle do código-fonte tenha especificado o `SCC_CAP_GET_NOUI` sinalizador na inicialização, indicando que ele não tem uma interface do usuário para um comando Get, essa função ainda pode ser chamada pelo IDE para recuperar arquivos. O sinalizador simplesmente significa que o IDE não exibe um item de menu Get e que o plug-in não deve fornecer nenhuma interface do usuário.

## <a name="rename-files-and-sccget"></a>Renomear arquivos e SccGet
 Situação: um usuário faz o check-out de um arquivo, por exemplo, *a.txt* e o modifica. Antes que *a.txt* possa ser feito o check-in, um segundo usuário renomeia *a.txt* para *b.txt* no banco de dados de controle do código-fonte, verifica *b.txt*, faz algumas modificações no arquivo e verifica o arquivo em. O primeiro usuário quer as alterações feitas pelo segundo usuário para que o primeiro usuário renomeie sua versão local do *a.txt* arquivo como *b.txt* e faça um get no arquivo. No entanto, o cache local que controla os números de versão ainda pensa que a primeira versão do *a.txt* é armazenada localmente e, portanto, o controle do código-fonte não pode resolver as diferenças.

 Há duas maneiras de resolver essa situação em que o cache local das versões de controle do código-fonte fica fora de sincronia com o banco de dados de controle do código-fonte:

1. Não permitir a renomeação de um arquivo no banco de dados de controle do código-fonte que está com check-out no momento.

2. Faça o equivalente de "excluir antigo" seguido por "Adicionar novo". O algoritmo a seguir é uma maneira de fazer isso.

    1. Chame a função [SccQueryChanges](../extensibility/sccquerychanges-function.md) para saber mais sobre a renomeação de *a.txt* para *b.txt* no banco de dados de controle do código-fonte.

    2. Renomeie o *a.txt* local para *b.txt*.

    3. Chame a `SccGet` função para *a.txt* e *b.txt*.

    4. Como *a.txt* não existe no banco de dados de controle do código-fonte, o cache da versão local é limpo das informações de versão *a.txt* ausente.

    5. O arquivo de *b.txt* cujo check-out está sendo feito é mesclado com o conteúdo do arquivo de *b.txt* local.

    6. O arquivo atualizado *b.txt* agora pode ser verificado.

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Bitflags usado por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md)

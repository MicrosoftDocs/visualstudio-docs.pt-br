---
description: Essa função abre um projeto de controle do código-fonte existente ou cria um novo.
title: Função SccOpenProject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccOpenProject
helpviewer_keywords:
- SccOpenProject function
ms.assetid: d609510b-660a-46d7-b93d-2406df20434d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: baada63e84e95fd466e0e5640c592dfe303d8e1a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063754"
---
# <a name="sccopenproject-function"></a>Função SccOpenProject
Essa função abre um projeto de controle do código-fonte existente ou cria um novo.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccOpenProject (
   LPVOID        pvContext,
   HWND          hWnd,
   LPSTR         lpUser,
   LPCSTR        lpProjName,
   LPCSTR        lpLocalProjPath,
   LPSTR         lpAuxProjPath,
   LPCSTR        lpComment,
   LPTEXTOUTPROC lpTextOutProc,
   LONG          dwFlags
);
```

#### <a name="parameters"></a>Parâmetros
 pvContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 lpUser

[entrada, saída] O nome do usuário (sem exceder SCC_USER_SIZE, incluindo o terminador nulo).

 lpProjName

no A cadeia de caracteres que identifica o nome do projeto.

 lpLocalProjPath

no O caminho para a pasta de trabalho do projeto.

 lpAuxProjPath

[entrada, saída] Uma cadeia de caracteres auxiliar opcional que identifica o projeto (sem exceder SCC_AUXPATH_SIZE, incluindo o terminador nulo).

 lpComment

no Comente para um novo projeto que está sendo criado.

 lpTextOutProc

no Uma função de retorno de chamada opcional para exibir a saída de texto do plug-in de controle do código-fonte.

 dwFlags

no Sinaliza se um novo projeto precisa ser criado se o projeto for desconhecido para o plug-in de controle do código-fonte. O valor pode ser uma combinação de `SCC_OP_CREATEIFNEW` e `SCC_OP_SILENTOPEN.`

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Êxito ao abrir o projeto.|
|SCC_E_INITIALIZEFAILED|Não foi possível inicializar o projeto.|
|SCC_E_INVALIDUSER|O usuário não pôde fazer logon no sistema de controle do código-fonte.|
|SCC_E_COULDNOTCREATEPROJECT|O projeto não existia antes da chamada;  o `SCC_OPT_CREATEIFNEW` sinalizador foi definido, mas não foi possível criar o projeto.|
|SCC_E_PROJSYNTAXERR|Sintaxe de projeto inválida.|
|SCC_E_UNKNOWNPROJECT|O projeto é desconhecido para o plug-in de controle do código-fonte e o `SCC_OPT_CREATEIFNEW` sinalizador não foi definido.|
|SCC_E_INVALIDFILEPATH|Caminho de arquivo inválido ou inutilizável.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. Uma nova tentativa é recomendada.|
|SCC_E_NONSPECFICERROR|Uma falha não específica; o sistema de controle do código-fonte não foi inicializado.|

## <a name="remarks"></a>Comentários
 O IDE pode passar um nome de usuário ( `lpUser` ) ou pode simplesmente passar um ponteiro para uma cadeia de caracteres vazia. Se houver um nome de usuário, o plug-in de controle do código-fonte deverá usá-lo como padrão. No entanto, se nenhum nome foi passado ou se o logon falhou com o nome fornecido, o plug-in deverá solicitar que o usuário faça logon e retornará o nome válido `lpUser` quando receber um logon válido `.` porque o plug-in pode alterar a cadeia de caracteres de nome de usuário, o IDE sempre alocará um buffer de tamanho ( `SCC_USER_LEN` + 1 ou SCC_USER_SIZE, que inclui espaço para o terminador nulo

> [!NOTE]
> A primeira ação que o IDE pode precisar executar pode ser uma chamada para a `SccOpenProject` função ou [SccGetProjPath](../extensibility/sccgetprojpath-function.md). Por esse motivo, ambos têm um `lpUser` parâmetro idêntico.

 `lpAuxProjPath` e `lpProjName` são lidos do arquivo de solução, ou são retornados de uma chamada para a `SccGetProjPath` função. Esses parâmetros contêm as cadeias de caracteres que o plug-in de controle do código-fonte associa ao projeto e são significativos apenas para o plug-in. Se nenhuma cadeia de caracteres estiver no arquivo de solução e o usuário não tiver sido solicitado a procurar (que retornaria uma cadeia de caracteres por meio da `SccGetProjPath` função), o IDE passa cadeias de caracteres vazias para `lpAuxProjPath` e e `lpProjName` espera que esses valores sejam atualizados pelo plug-in quando essa função retorna.

 `lpTextOutProc` é um ponteiro para uma função de retorno de chamada fornecida pelo IDE para o plug-in de controle do código-fonte com a finalidade de exibir a saída do resultado do comando. Essa função de retorno de chamada é descrita em detalhes em [LPTEXTOUTPROC](../extensibility/lptextoutproc.md).

> [!NOTE]
> Se o plug-in de controle do código-fonte pretende tirar proveito disso, ele deve ter definido o `SCC_CAP_TEXTOUT` sinalizador no [SccInitialize](../extensibility/sccinitialize-function.md). Se esse sinalizador não tiver sido definido, ou se o IDE não oferecer suporte a esse recurso, `lpTextOutProc` será `NULL` .

 O `dwFlags` parâmetro controla o resultado no caso em que o projeto que está sendo aberto não exista atualmente. Ele consiste em dois bitflags, `SCC_OP_CREATEIFNEW` e `SCC_OP_SILENTOPEN` . Se o projeto que está sendo aberto já existir, a função simplesmente abrirá o projeto e retornará `SCC_OK` . Se o projeto não existir e se o `SCC_OP_CREATEIFNEW` sinalizador estiver ativado, o plug-in de controle do código-fonte poderá criar o projeto no sistema de controle do código-fonte, abri-lo e retornar `SCC_OK` . Se o projeto não existir e se o `SCC_OP_CREATEIFNEW` sinalizador for desativado, o plug-in deverá verificar o `SCC_OP_SILENTOPEN` sinalizador. Se esse sinalizador não estiver ativado, o plug-in poderá solicitar ao usuário um nome de projeto. Se esse sinalizador estiver ativado, o plug-in deverá simplesmente retornar `SCC_E_UNKNOWNPROJECT` .

## <a name="calling-order"></a>Ordem de chamada
 No curso normal de eventos, o [SccInitialize](../extensibility/sccinitialize-function.md) seria chamado primeiro para abrir uma sessão de controle do código-fonte. Uma sessão pode consistir em uma chamada para `SccOpenProject` , seguida por outras chamadas de função da API de plug-in de controle do código-fonte e será encerrada com uma chamada para o [SccCloseProject](../extensibility/scccloseproject-function.md). Essas sessões podem ser repetidas várias vezes antes de o [SccUninitialize](../extensibility/sccuninitialize-function.md) ser chamado.

 Se o plug-in de controle do código-fonte definir o `SCC_CAP_REENTRANT` bit em `SccInitialize` , a sequência de sessão acima poderá ser repetida muitas vezes em paralelo. `pvContext`Estruturas diferentes controlam as diferentes sessões, nas quais cada `pvContext` uma está associada a um projeto aberto por vez. Com base no `pvContext` parâmetro, o plug-in pode determinar qual projeto é referenciado em qualquer chamada específica. Se o bit de funcionalidade `SCC_CAP_REENTRANT` não estiver definido, os plug-ins de controle do código-fonte do nonreentrant serão limitados em sua capacidade de trabalhar com vários projetos.

> [!NOTE]
> O `SCC_CAP_REENTRANT` bit foi introduzido na versão 1,1 da API de plug-in de controle do código-fonte. Ele não está definido ou é ignorado na versão 1,0 e todos os plug-ins de controle do código-fonte da versão 1,0 são considerados nonreentrant.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccCloseProject](../extensibility/scccloseproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [Restrições de comprimentos de cadeia de caracteres](../extensibility/restrictions-on-string-lengths.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)

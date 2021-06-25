---
description: Essa função abre um projeto de controle do código-fonte existente ou cria um novo.
title: Função SccOpenProject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: 1326319b483aa707b77e0d7142d816b01fc7d3b1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902391"
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

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 lpUser

[in, out] O nome do usuário (não deve exceder SCC_USER_SIZE, incluindo o terminador NULL).

 lpProjName

[in] A cadeia de caracteres que identifica o nome do projeto.

 lpLocalProjPath

[in] O caminho para a pasta de trabalho do projeto.

 lp LpProjPath

[in, out] Uma cadeia de caracteres auxiliar opcional que identifica o projeto (não deve exceder SCC_AUXPATH_SIZE, incluindo o terminador NULL).

 lpComment

[in] Comente com um novo projeto que está sendo criado.

 lpTextOutProc

[in] Uma função de retorno de chamada opcional para exibir a saída de texto do plug-in de controle do código-fonte.

 dwFlags

[in] Sinaliza se um novo projeto precisa ser criado se o projeto for desconhecido para o plug-in de controle do código-fonte. O valor pode ser uma combinação de `SCC_OP_CREATEIFNEW` e `SCC_OP_SILENTOPEN.`

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Êxito ao abrir o projeto.|
|SCC_E_INITIALIZEFAILED|Não foi possível inicializar o projeto.|
|SCC_E_INVALIDUSER|O usuário não pôde fazer logoff no sistema de controle do código-fonte.|
|SCC_E_COULDNOTCREATEPROJECT|O projeto não existia antes da chamada;  o `SCC_OPT_CREATEIFNEW` sinalizador foi definido, mas o projeto não pôde ser criado.|
|SCC_E_PROJSYNTAXERR|Sintaxe de projeto inválida.|
|SCC_E_UNKNOWNPROJECT|O projeto é desconhecido para o plug-in de controle do código-fonte e o `SCC_OPT_CREATEIFNEW` sinalizador não foi definido.|
|SCC_E_INVALIDFILEPATH|Caminho de arquivo inválido ou inutilizável.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar essa operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção. Uma nova tentativa é recomendada.|
|SCC_E_NONSPECFICERROR|Uma falha não específica; O sistema de controle do código-fonte não foi inicializado.|

## <a name="remarks"></a>Comentários
 O IDE pode passar um nome de usuário ( ) ou pode simplesmente passar um ponteiro para uma cadeia `lpUser` de caracteres vazia. Se houver um nome de usuário, o plug-in de controle do código-fonte deverá usá-lo como padrão. No entanto, se nenhum nome tiver sido passado ou se o logon falhar com o nome fornecido, o plug-in deverá solicitar que o usuário faça logon e retornará o nome válido quando receber um logon válido Porque o plug-in pode alterar a cadeia de caracteres de nome de usuário, o IDE sempre alocará um buffer de tamanho `lpUser` `.` ( +1 ou SCC_USER_SIZE, que inclui espaço para o terminador `SCC_USER_LEN` nulo).

> [!NOTE]
> A primeira ação que o IDE pode precisar executar pode ser uma chamada para a função ou `SccOpenProject` [O SccGetProjPath.](../extensibility/sccgetprojpath-function.md) Por esse motivo, ambos têm um parâmetro `lpUser` idêntico.

 `lpAuxProjPath` e `lpProjName` são lidos do arquivo de solução ou são retornados de uma chamada para a `SccGetProjPath` função. Esses parâmetros contêm as cadeias de caracteres que o plug-in de controle do código-fonte associa ao projeto e são significativos apenas para o plug-in. Se nenhuma dessas cadeias de caracteres estiver no arquivo de solução e o usuário não tiver sido solicitado a procurar (o que retornaria uma cadeia de caracteres por meio da função ), o IDE passará cadeias de caracteres vazias para e e espera que esses valores sejam atualizados pelo `SccGetProjPath` plug-in quando essa função `lpAuxProjPath` `lpProjName` retornar.

 `lpTextOutProc` é um ponteiro para uma função de retorno de chamada fornecida pelo IDE para o plug-in de controle do código-fonte com a finalidade de exibir a saída do resultado do comando. Essa função de retorno de chamada é descrita em detalhes [em LPTEXTOUTPROC.](../extensibility/lptextoutproc.md)

> [!NOTE]
> Se o plug-in de controle do código-fonte pretende tirar proveito disso, ele deve ter definido o `SCC_CAP_TEXTOUT` sinalizador [no SccInitialize.](../extensibility/sccinitialize-function.md) Se esse sinalizador não foi definido ou se o IDE não dá suporte a esse recurso, `lpTextOutProc` será `NULL` .

 O parâmetro controla o resultado caso o projeto que está sendo `dwFlags` aberto não exista no momento. Ele consiste em dois bitflags, `SCC_OP_CREATEIFNEW` e `SCC_OP_SILENTOPEN` . Se o projeto que está sendo aberto já existir, a função simplesmente abrirá o projeto e retornará `SCC_OK` . Se o projeto não existir e se o sinalizador estiver, o plug-in de controle do código-fonte poderá criar o projeto no sistema de controle do `SCC_OP_CREATEIFNEW` código-fonte, abri-lo e retornar `SCC_OK` . Se o projeto não existir e se o sinalizador estiver desligado, o `SCC_OP_CREATEIFNEW` plug-in deverá verificar o `SCC_OP_SILENTOPEN` sinalizador. Se esse sinalizador não estiver conectado, o plug-in poderá solicitar um nome de projeto ao usuário. Se esse sinalizador estiver conectado, o plug-in deverá simplesmente retornar `SCC_E_UNKNOWNPROJECT` .

## <a name="calling-order"></a>Ordem de chamada
 No curso normal dos eventos, [o SccInitialize](../extensibility/sccinitialize-function.md) seria chamado primeiro para abrir uma sessão de controle do código-fonte. Uma sessão pode consistir em uma chamada para , seguida por outras chamadas de função de API de plug-in de controle do código-fonte e será encerrada com uma chamada para `SccOpenProject` [o SccCloseProject](../extensibility/scccloseproject-function.md). Essas sessões podem ser repetidas várias vezes antes [que sccUninitialize](../extensibility/sccuninitialize-function.md) seja chamado.

 Se o plug-in de controle do código-fonte define o bit em , a sequência de sessão `SCC_CAP_REENTRANT` acima pode ser repetida muitas vezes em `SccInitialize` paralelo. Estruturas diferentes acompanham as sessões diferentes, nas quais cada uma é `pvContext` associada a um projeto aberto por `pvContext` vez. Com base no `pvContext` parâmetro , o plug-in pode determinar qual projeto é referenciado em qualquer chamada específica. Se o bit de funcionalidade `SCC_CAP_REENTRANT` não estiver definido, os plug-ins de controle do código-fonte não reentrantes serão limitados em sua capacidade de trabalhar com vários projetos.

> [!NOTE]
> O `SCC_CAP_REENTRANT` bit foi introduzido na versão 1.1 da API de Plug-in de Controle do Código-Fonte. Ele não está definido ou é ignorado na versão 1.0 e todos os plug-ins de controle do código-fonte da versão 1.0 são presumidos como não reentrantes.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccCloseProject](../extensibility/scccloseproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [Restrições de comprimentos de cadeia de caracteres](../extensibility/restrictions-on-string-lengths.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)

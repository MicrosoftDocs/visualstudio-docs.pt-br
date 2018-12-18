---
title: Função SccOpenProject | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccOpenProject
helpviewer_keywords:
- SccOpenProject function
ms.assetid: d609510b-660a-46d7-b93d-2406df20434d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 928c1d63451dc49fabf01503e8cb7f6789b98998
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49837003"
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
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 lpUser  
 [no, out] O nome do usuário (não deve exceder SCC_USER_SIZE, incluindo o terminador NULL).  
  
 lpProjName  
 [in] A cadeia de caracteres que identifica o nome do projeto.  
  
 lpLocalProjPath  
 [in] O caminho para a pasta de trabalho para o projeto.  
  
 lpAuxProjPath  
 [no, out] Uma cadeia de auxiliar opcional identificando o projeto (não deve exceder SCC_AUXPATH_SIZE, incluindo o terminador NULL).  
  
 lpComment  
 [in] Comentário para um novo projeto que está sendo criado.  
  
 lpTextOutProc  
 [in] Uma função de retorno de chamada opcional para exibir o texto de saída do plug-in de controle do código-fonte.  
  
 dwFlags  
 [in] Se um novo projeto precisa ser criado se o projeto for desconhecido para a fonte de sinais de controlam plug-in. Valor pode ser uma combinação de `SCC_OP_CREATEIFNEW` e `SCC_OP_SILENTOPEN.`  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Êxito na abertura do projeto.|  
|SCC_E_INITIALIZEFAILED|Não foi possível inicializar o projeto.|  
|SCC_E_INVALIDUSER|O usuário não pôde fazer logon sistema de controle de origem.|  
|SCC_E_COULDNOTCREATEPROJECT|O projeto não existia antes da chamada;  o `SCC_OPT_CREATEIFNEW` sinalizador foi definido, mas não foi possível criar o projeto.|  
|SCC_E_PROJSYNTAXERR|Sintaxe de projeto inválido.|  
|SCC_E_UNKNOWNPROJECT|O projeto é desconhecido para o plug-in de controle de origem e o `SCC_OPT_CREATEIFNEW` sinalizador não foi configurado.|  
|SCC_E_INVALIDFILEPATH|Caminho de arquivo inválido ou inutilizável.|  
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. É recomendável uma nova tentativa.|  
|SCC_E_NONSPECFICERROR|Uma falha não específica; o sistema de controle do código-fonte não foi inicializado.|  
  
## <a name="remarks"></a>Comentários  
 O IDE pode passar um nome de usuário (`lpUser`), ou pode simplesmente passar um ponteiro para uma cadeia de caracteres vazia. Se houver um nome de usuário, o plug-in de controle do código-fonte deve usá-lo como padrão. No entanto, se nenhum nome foi passado ou se o logon falhou com o nome fornecido, o plug-in deve solicitar ao usuário para fazer logon e retornará o nome válido no `lpUser` quando ele recebe um logon válido`.` porque o plug-in pode mudar a cadeia de caracteres de nome de usuário , o IDE sempre alocará um buffer de tamanho (`SCC_USER_LEN`+ 1 ou SCC_USER_SIZE, que inclui espaço para o terminador nulo).  
  
> [!NOTE]
>  A primeira ação que o IDE pode ser necessário para executar pode ser uma chamada para o `SccOpenProject` função ou o [SccGetProjPath](../extensibility/sccgetprojpath-function.md). Por esse motivo, ambos têm um idênticos `lpUser` parâmetro.  
  
 `lpAuxProjPath` e`lpProjName` são lidas do arquivo de solução, ou eles são retornados de uma chamada para o `SccGetProjPath` função. Esses parâmetros contêm cadeias de caracteres que o plug-in de controle do código-fonte se associa ao projeto e são significativos para o plug-in. Se tais cadeias de caracteres não estão no arquivo de solução e o usuário não tiver sido solicitado para procurar (que retornaria uma cadeia de caracteres por meio de `SccGetProjPath` função), IDE passa cadeias de caracteres vazias para ambos `lpAuxProjPath` e `lpProjName`e espera que esses valores a serem atualizados pelo plug-in quando essa função retorna.  
  
 `lpTextOutProc` é um ponteiro para uma função de retorno de chamada fornecida pelo IDE para o plug-in para fins de exibição de saída de resultado do comando de controle de origem. Essa função de retorno de chamada é descrita detalhadamente no [LPTEXTOUTPROC](../extensibility/lptextoutproc.md).  
  
> [!NOTE]
>  Se o plug-in de controle do código-fonte pretende aproveitar isso, ele deve ter definido as `SCC_CAP_TEXTOUT` sinalizador na [SccInitialize](../extensibility/sccinitialize-function.md). Se esse sinalizador não for definido, ou se o IDE não dá suporte a esse recurso `lpTextOutProc` será `NULL`.  
  
 O `dwFlags` parâmetro controla o resultado que o projeto que está sendo aberto não existe. Ele consiste em dois sinalizadores de bit, `SCC_OP_CREATEIFNEW` e `SCC_OP_SILENTOPEN`. Se o projeto que está sendo aberto já existir, a função simplesmente abre o projeto e retorna `SCC_OK`. Se o projeto não existe e se o `SCC_OP_CREATEIFNEW` sinalizador é no, o plug-in de controle do código-fonte pode criar o projeto no sistema de controle de origem, abri-lo e retornar `SCC_OK`. Se o projeto não existe e se o `SCC_OP_CREATEIFNEW` sinalizador estiver desativado, o plug-in deve, em seguida, verificar se há o `SCC_OP_SILENTOPEN` sinalizador. Se esse sinalizador é desabilitado, o plug-in pode solicitar ao usuário um nome de projeto. Se esse sinalizador for na, o plug-in deve retornar apenas `SCC_E_UNKNOWNPROJECT`.  
  
## <a name="calling-order"></a>Ordem de chamada  
 No curso normal de eventos, o [SccInitialize](../extensibility/sccinitialize-function.md) seria chamado primeiro para abrir uma sessão de controle do código-fonte. Uma sessão pode consistir em uma chamada para `SccOpenProject`, seguido por outras chamadas de função de API de plug-in de controle do código-fonte e terminará com uma chamada para o [SccCloseProject](../extensibility/scccloseproject-function.md). Essas sessões poderão ser repetidas várias vezes antes do [SccUninitialize](../extensibility/sccuninitialize-function.md) é chamado.  
  
 Se o controle de fonte conjuntos de plug-in a `SCC_CAP_REENTRANT` bit no `SccInitialize`, em seguida, a sequência de sessão acima pode ser repetida várias vezes em paralelo. Diferentes `pvContext` estruturas de acompanhar as diferentes sessões em que cada `pvContext` está associado um projeto aberto por vez. Com base no`pvContext` parâmetro, o plug-in pode determinar qual projeto é referenciado em qualquer chamada específica. Se o recurso de bits `SCC_CAP_REENTRANT` não for definido, nonreentrant plug-ins de controle de origem são limitados em sua capacidade de trabalhar com vários projetos.  
  
> [!NOTE]
>  O `SCC_CAP_REENTRANT` bit foi introduzido na versão 1.1 do que a API de plug-in de controle do código-fonte. Ele não está definido ou é ignorado na versão 1.0, e todos os versão 1.0 fonte plug-ins de controle são considerados nonreentrant.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [SccCloseProject](../extensibility/scccloseproject-function.md)   
 [SccGetProjPath](../extensibility/sccgetprojpath-function.md)   
 [SccInitialize](../extensibility/sccinitialize-function.md)   
 [SccUninitialize](../extensibility/sccuninitialize-function.md)   
 [Restrições em comprimentos de cadeia de caracteres](../extensibility/restrictions-on-string-lengths.md)   
 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
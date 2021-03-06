---
description: Essa função cria um subprojeto com o nome fornecido em um projeto pai existente especificado pelo argumento lpParentProjPath.
title: Função SccCreateSubProject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCreateSubProject
helpviewer_keywords:
- SccCreateSubProject function
ms.assetid: 08154aed-ae5c-463c-8694-745d0e332965
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 38fb6a18954b0a2f976fad4b24819a08ed868ab6
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221607"
---
# <a name="scccreatesubproject-function"></a>Função SccCreateSubProject
Essa função cria um subprojeto com o nome fornecido em um projeto pai existente especificado pelo `lpParentProjPath` argumento.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccCreateSubProject(
   LPVOID pContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPCSTR lpParentProjPath,
   LPCSTR lpSubProjName,
   LPSTR  lpAuxProjPath,
   LPSTR  lpSubProjPath
);
```

### <a name="parameters"></a>Parâmetros
 pContext

no O ponteiro de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 lpUser

[entrada, saída] O nome de usuário (até SCC_USER_SIZE, incluindo o terminador nulo).

 lpParentProjPath

no Uma cadeia de caracteres que identifica o caminho do projeto pai (até SCC_PRJPATH_SIZE, incluindo o terminador nulo).

 lpSubProjName

no O nome sugerido do subprojeto (até SCC_PRJPATH_SIZE, incluindo o terminador nulo).

 lpAuxProjPath

[entrada, saída] Cadeia de caracteres auxiliar que identifica o projeto (até SCC_PRJPATH_SIZE, incluindo o terminador nulo).

 lpSubProjPath

[entrada, saída] Cadeia de caracteres de saída que identifica o caminho para o subprojeto (até SCC_PRJPATH_SIZE, incluindo o terminador nulo).

## <a name="return-value"></a>Retornar valor
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O subprojeto foi criado com êxito.|
|SCC_E_INITIALIZEFAILED|Não foi possível inicializar o projeto pai.|
|SCC_E_INVALIDUSER|O usuário não pôde fazer logon no sistema de controle do código-fonte.|
|SCC_E_COULDNOTCREATEPROJECT|O subprojeto não pode ser criado.|
|SCC_E_PROJSYNTAXERR|Sintaxe de projeto inválida.|
|SCC_E_UNKNOWNPROJECT|O projeto pai é desconhecido para o plug-in de controle do código-fonte.|
|SCC_E_INVALIDFILEPATH|Caminho de arquivo inválido ou inutilizável.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. Uma nova tentativa é recomendada.|
|SCC_E_CONNECTIONFAILURE|Houve um problema de conexão de plug-in de controle do código-fonte.|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Se já existir um subprojeto com o nome, a função poderá alterar o nome padrão para criar um exclusivo, por exemplo, adicionando "_ \<number> " a ele. O chamador deve estar preparado para aceitar alterações em `lpUser` , `lpSubProjPath` e `lpAuxProjPath` . Os `lpSubProjPath` `lpAuxProjPath` argumentos e são usados em uma chamada para o [SccOpenProject](../extensibility/sccopenproject-function.md). Eles não devem ser modificados pelo chamador no retorno. Essas cadeias de caracteres fornecem uma maneira para o plug-in de controle do código-fonte controlar informações que precisam ser associadas a um projeto. O IDE do chamador não exibirá esses dois parâmetros no retorno, porque o plug-in pode usar uma cadeia de caracteres formatada que pode não ser adequada para exibição. A função retorna um código de êxito ou de falha e, se for bem-sucedida, preenche a variável `lpSubProjPath` com o caminho completo do projeto para o novo projeto.

 Essa função é semelhante ao [SccGetProjPath](../extensibility/sccgetprojpath-function.md), exceto que ele cria silenciosamente um projeto em vez de solicitar que o usuário selecione um. Quando a `SccCreateSubProject` função é chamada `lpParentProjName` e `lpAuxProjPath` não estará vazia e corresponderá a um projeto válido. Essas cadeias de caracteres geralmente são recebidas pelo IDE de uma chamada anterior à `SccGetProjPath` função ou ao [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md).

 O `lpUser` argumento é o nome de usuário. O IDE passará o mesmo nome de usuário que tinha recebido anteriormente `SccGetProjPath` e o plug-in de controle do código-fonte deverá usar o nome como padrão. Se o usuário já tiver uma conexão aberta com o plug-in, o plug-in deverá tentar eliminar todos os prompts para garantir que a função funcione silenciosamente. No entanto, se o logon falhar, o plug-in deverá solicitar ao usuário um logon e, quando receber um logon válido, passar o nome de volta `lpUser` . Como o plug-in pode alterar essa cadeia de caracteres, o IDE sempre alocará um buffer de tamanho (SCC_USER_LEN + 1 ou SCC_USER_SIZE, que inclui o espaço para o terminador nulo). Se a cadeia de caracteres for alterada, a nova cadeia de caracteres deverá ser um nome de logon válido (pelo menos tão válido quanto a cadeia de caracteres antiga).

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>Notas técnicas para SccCreateSubProject e SccGetParentProjectPath
 A adição de soluções e projetos ao controle do código-fonte foi simplificada no Visual Studio para minimizar o número de vezes que um usuário é solicitado a selecionar locais no sistema de controle do código-fonte. Essas alterações são ativadas pelo Visual Studio se um plug-in de controle do código-fonte der suporte a ambas as novas funções `SccCreateSubProject` e `SccGetParentProjectPath` . No entanto, a seguinte entrada de registro pode ser usada para desabilitar essas alterações e reverter para o comportamento anterior do Visual Studio (API de plug-in de controle de origem versão 1,1):

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] "DoNotCreateSolutionRootFolderInSourceControl" = DWORD: 00000001**

 Se essa entrada de registro não existir ou for definida como DWORD: 00000000, o Visual Studio tentará usar as novas funções `SccCreateSubProject` e `SccGetParentProjectPath` .

 Se a entrada do registro for definida como DWORD: 00000001, o Visual Studio não tentará usar essas novas funções e as operações de adição ao controle do código-fonte funcionarão como faziam em versões anteriores do Visual Studio.

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)

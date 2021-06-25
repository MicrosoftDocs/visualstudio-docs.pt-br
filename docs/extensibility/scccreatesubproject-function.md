---
description: Essa função cria um subprojeto com o nome especificado em um projeto pai existente especificado pelo argumento lpParentProjPath.
title: Função SccCreateSubProject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccCreateSubProject
helpviewer_keywords:
- SccCreateSubProject function
ms.assetid: 08154aed-ae5c-463c-8694-745d0e332965
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a6df7a801d282113b530f24472419a9735256702
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904676"
---
# <a name="scccreatesubproject-function"></a>Função SccCreateSubProject
Essa função cria um subprojeto com o nome especificado em um projeto pai existente especificado pelo `lpParentProjPath` argumento .

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

[in] O ponteiro de contexto do plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 lpUser

[in, out] O nome de usuário (até SCC_USER_SIZE, incluindo o terminador NULL).

 lpParentProjPath

[in] Uma cadeia de caracteres que identifica o caminho do projeto pai (até SCC_PRJPATH_SIZE, incluindo o terminador NULL).

 lpSubProjName

[in] O nome do subprojeto sugerido (até SCC_PRJPATH_SIZE, incluindo o terminador NULL).

 lp LpProjPath

[in, out] Cadeia de caracteres auxiliar que identifica o projeto (até SCC_PRJPATH_SIZE, incluindo o terminador NULL).

 lpSubProjPath

[in, out] Cadeia de caracteres de saída que identifica o caminho para o subprojeto (até SCC_PRJPATH_SIZE, incluindo o terminador NULL).

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O subprojeto foi criado com êxito.|
|SCC_E_INITIALIZEFAILED|Não foi possível inicializar o projeto pai.|
|SCC_E_INVALIDUSER|O usuário não pôde fazer logoff no sistema de controle do código-fonte.|
|SCC_E_COULDNOTCREATEPROJECT|O subprojeto não pode ser criado.|
|SCC_E_PROJSYNTAXERR|Sintaxe de projeto inválida.|
|SCC_E_UNKNOWNPROJECT|O projeto pai é desconhecido para o plug-in de controle do código-fonte.|
|SCC_E_INVALIDFILEPATH|Caminho de arquivo inválido ou inutilizável.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar essa operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção. Uma nova tentativa é recomendada.|
|SCC_E_CONNECTIONFAILURE|Houve um problema de conexão de plug-in de controle do código-fonte.|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Se um subprojeto com o nome já existir, a função poderá alterar o nome padrão para criar um exclusivo, por exemplo, adicionando "_ \<number> " a ela. O chamador deve estar preparado para aceitar alterações `lpUser` em `lpSubProjPath` , e `lpAuxProjPath` . Os `lpSubProjPath` `lpAuxProjPath` argumentos e são usados em uma chamada para [o SccOpenProject](../extensibility/sccopenproject-function.md). Eles não devem ser modificados pelo chamador no retorno. Essas cadeias de caracteres fornecem uma maneira para o plug-in de controle do código-fonte rastrear informações que ele precisa associar a um projeto. O IDE do chamador não exibirá esses dois parâmetros no retorno, porque o plug-in pode usar uma cadeia de caracteres formatada que pode não ser adequada para exibição. A função retorna um código de êxito ou falha e, se bem-sucedido, preenche a variável com o caminho completo do projeto `lpSubProjPath` para o novo projeto.

 Essa função é semelhante ao [SccGetProjPath](../extensibility/sccgetprojpath-function.md), exceto pelo fato de que ela cria silenciosamente um projeto em vez de solicitar que o usuário selecione um. Quando a `SccCreateSubProject` função é chamada e não estará vazia e `lpParentProjName` `lpAuxProjPath` corresponderá a um projeto válido. Essas cadeias de caracteres geralmente são recebidas pelo IDE de uma chamada anterior para a função ou `SccGetProjPath` [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md).

 O `lpUser` argumento é o nome de usuário. O IDE passará o mesmo nome de usuário que recebeu anteriormente de e o plug-in de controle do `SccGetProjPath` código-fonte deve usar o nome como padrão. Se o usuário já tiver uma conexão aberta com o plug-in, o plug-in deverá tentar eliminar os prompts para garantir que a função funcione silenciosamente. No entanto, se o logon falhar, o plug-in deverá solicitar ao usuário um logon e, quando receber um logon válido, passe o nome de volta em `lpUser` . Como o plug-in pode alterar essa cadeia de caracteres, o IDE sempre alocará um buffer de tamanho (SCC_USER_LEN+1 ou SCC_USER_SIZE, que inclui espaço para o terminador nulo). Se a cadeia de caracteres for alterada, a nova cadeia de caracteres deverá ser um nome de logon válido (pelo menos tão válido quanto a cadeia de caracteres antiga).

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>Notas técnicas para SccCreateSubProject e SccGetParentProjectPath
 A adição de soluções e projetos ao controle do código-fonte foi simplificada Visual Studio minimizar o número de vezes que um usuário é solicitado a selecionar locais no sistema de controle do código-fonte. Essas alterações serão ativadas por Visual Studio se um plug-in de controle do código-fonte for compatível com ambas as novas funções, `SccCreateSubProject` e `SccGetParentProjectPath` . No entanto, a seguinte entrada do Registro pode ser usada para desabilitar essas alterações e reverter para o comportamento anterior Visual Studio (API de Plug-in de Controle do Código-fonte versão 1.1) :

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] "DoNotCreateSolutionRootFolderInSourceControl"=dword:00000001**

 Se essa entrada do Registro não existir ou estiver definida como dword:00000000, o Visual Studio tentará usar as novas funções `SccCreateSubProject` e `SccGetParentProjectPath` .

 Se a entrada do Registro estiver definida como dword:00000001, o Visual Studio não tentará usar essas novas funções e as operações de adição ao controle do código-fonte funcionarão como em versões anteriores do Visual Studio.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)

---
description: Essa função determina o caminho do projeto pai de um projeto especificado.
title: Função SccGetParentProjectPath | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetParentProjectPath
helpviewer_keywords:
- SccGetParentProjectPath function
ms.assetid: 62a71579-36b3-48b9-a1c8-04ab100efa08
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 305f226117bbb9cf906231a0b9bbaa24c1d87a8e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063975"
---
# <a name="sccgetparentprojectpath-function"></a>Função SccGetParentProjectPath
Essa função determina o caminho do projeto pai de um projeto especificado. Essa função é chamada quando o usuário está adicionando um projeto do Visual Studio ao controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccGetParentProjectPath(
   LPVOID pContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPCSTR lpProjPath,
   LPSTR  lpAuxProjPath,
   LPSTR  lpParentProjPath
);
```

### <a name="parameters"></a>Parâmetros
 pContext

no O ponteiro de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 lpUser

[entrada, saída] O nome de usuário (até SCC_USER_SIZE, incluindo o terminador nulo).

 lpProjPath

no Cadeia de caracteres que identifica o caminho do projeto (até SCC_PRJPATH_SIZE, incluindo o terminador nulo).

 lpAuxProjPath

[entrada, saída] Cadeia de caracteres auxiliar que identifica o projeto (até SCC_PRJPATH_SIZE, incluindo o terminador nulo).

 lpParentProjPath

[entrada, saída] Cadeia de caracteres de saída que identifica o caminho do projeto pai (até SCC_PRJPATH_SIZE, incluindo o terminador nulo).

## <a name="return-value"></a>Retornar valor
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O caminho do projeto pai foi obtido com êxito.|
|SCC_E_INITIALIZEFAILED|Não foi possível inicializar o projeto.|
|SCC_E_INVALIDUSER|O usuário não pôde fazer logon no plug-in de controle do código-fonte.|
|SCC_E_UNKNOWNPROJECT|O projeto é desconhecido para o plug-in de controle do código-fonte.|
|SCC_E_INVALIDFILEPATH|Caminho de arquivo inválido ou inutilizável.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. Uma nova tentativa é recomendada.|
|SCC_E_PROJSYNTAXERR|Sintaxe de projeto inválida.|
|SCC_E_CONNECTIONFAILURE|Problema de conexão de armazenamento.|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Essa função retorna um código de êxito ou de falha e, se for bem-sucedida, preenche a variável `lpParentProjPath` com o caminho completo do projeto para o projeto especificado.

 Essa função retorna o caminho do projeto pai de um projeto existente. Para o projeto raiz, a função retorna o caminho do projeto que foi passado (ou seja, o mesmo caminho do projeto raiz). Observe que um caminho de projeto é uma cadeia de caracteres que é significativa apenas para o plug-in de controle do código-fonte.

 O IDE também está preparado para aceitar alterações nos `lpUser` `lpAuxProjPath` parâmetros e. O IDE irá persistir essas cadeias de caracteres e passá-las para o [SccOpenProject](../extensibility/sccopenproject-function.md) quando o usuário abrir esse projeto no futuro. Portanto, essas cadeias de caracteres fornecem uma maneira para o plug-in de controle do código-fonte controlar informações de que ele precisa para associar a um projeto.

 Essa função é semelhante ao [SccGetProjPath](../extensibility/sccgetprojpath-function.md), exceto pelo fato de que ele não solicita que o usuário selecione um projeto. Ele também nunca cria um novo projeto, mas funciona apenas com um projeto existente.

 Quando `SccGetParentProjectPath` é chamado `lpProjPath` e `lpAuxProjPath` não estará vazio e corresponderá a um projeto válido. Essas cadeias de caracteres geralmente são recebidas pelo IDE de uma chamada anterior para a `SccGetProjPath` função.

 O `lpUser` argumento é o nome de usuário. O IDE passará o mesmo nome de usuário recebido anteriormente da `SccGetProjPath` função, e o plug-in de controle do código-fonte deverá usar o nome como padrão. Se o usuário já tiver uma conexão aberta com o plug-in, o plug-in deverá tentar eliminar todos os prompts para garantir que a função funcione silenciosamente. No entanto, se o logon falhar, o plug-in deverá solicitar ao usuário um logon e, quando receber um logon válido, passar o nome de volta `lpUser` . Como o plug-in pode alterar essa cadeia de caracteres, o IDE sempre aloca um buffer de tamanho ( `SCC_USER_LEN` + 1). Se a cadeia de caracteres for alterada, a nova cadeia de caracteres deverá ser um nome de logon válido (pelo menos tão válido quanto a cadeia de caracteres antiga).

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>Notas técnicas para SccCreateSubProject e SccGetParentProjectPath
 A adição de soluções e projetos ao controle do código-fonte foi simplificada no Visual Studio para minimizar o número de vezes que um usuário é solicitado a selecionar locais no sistema de controle do código-fonte. Essas alterações são ativadas pelo Visual Studio se um plug-in de controle do código-fonte der suporte a ambas as novas funções, [SccCreateSubProject](../extensibility/scccreatesubproject-function.md) e a `SccGetParentProjectPath` função. No entanto, a seguinte entrada de registro pode ser usada para desabilitar essas alterações e reverter para o comportamento anterior do Visual Studio (API de plug-in de controle de origem versão 1,1):

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] "DoNotCreateSolutionRootFolderInSourceControl" = DWORD: 00000001**

 Se essa entrada de registro não existir ou for definida como DWORD: 00000000, o Visual Studio tentará usar as novas funções `SccCreateSubProject` e `SccGetParentProjectPath` .

 Se a entrada do registro for definida como DWORD: 00000001, o Visual Studio não tentará usar essas novas funções e as operações de adição ao controle do código-fonte funcionarão como faziam em versões anteriores do Visual Studio.

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccCreateSubProject](../extensibility/scccreatesubproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)

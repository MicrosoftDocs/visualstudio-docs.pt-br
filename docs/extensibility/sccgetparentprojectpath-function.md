---
description: Essa função determina o caminho do projeto pai de um projeto especificado.
title: Função SccGetParentProjectPath | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: 13a0a77808004c7bc8f408bbf34a3ed4f0715b36
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900129"
---
# <a name="sccgetparentprojectpath-function"></a>Função SccGetParentProjectPath
Essa função determina o caminho do projeto pai de um projeto especificado. Essa função é chamada quando o usuário está adicionando um projeto Visual Studio ao controle do código-fonte.

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

[in] O ponteiro de contexto do plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 lpUser

[in, out] O nome de usuário (até SCC_USER_SIZE, incluindo o terminador NULL).

 lpProjPath

[in] Cadeia de caracteres que identifica o caminho do projeto (até SCC_PRJPATH_SIZE, incluindo o terminador NULL).

 lp LpProjPath

[in, out] Cadeia de caracteres auxiliar que identifica o projeto (até SCC_PRJPATH_SIZE, incluindo o terminador NULL).

 lpParentProjPath

[in, out] Cadeia de caracteres de saída que identifica o caminho do projeto pai (até SCC_PRJPATH_SIZE, incluindo o terminador NULL).

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O caminho do projeto pai foi obtido com êxito.|
|SCC_E_INITIALIZEFAILED|Não foi possível inicializar o projeto.|
|SCC_E_INVALIDUSER|O usuário não pôde fazer logoff no plug-in de controle do código-fonte.|
|SCC_E_UNKNOWNPROJECT|O projeto é desconhecido para o plug-in de controle do código-fonte.|
|SCC_E_INVALIDFILEPATH|Caminho de arquivo inválido ou inutilizável.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar essa operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção. Uma nova tentativa é recomendada.|
|SCC_E_PROJSYNTAXERR|Sintaxe de projeto inválida.|
|SCC_E_CONNECTIONFAILURE|Problema de conexão de armazenamento.|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Essa função retorna um código de êxito ou falha e, se bem-sucedido, preenche a variável com o caminho completo do projeto `lpParentProjPath` para o projeto especificado.

 Essa função retorna o caminho do projeto pai de um projeto existente. Para o projeto raiz, a função retorna o caminho do projeto que foi passado (ou seja, o mesmo caminho do projeto raiz). Observe que um caminho de projeto é uma cadeia de caracteres que é significativa apenas para o plug-in de controle do código-fonte.

 O IDE também está preparado para aceitar alterações `lpUser` nos `lpAuxProjPath` parâmetros e . O IDE persistirá essas cadeias de caracteres e as passará para [o SccOpenProject](../extensibility/sccopenproject-function.md) quando o usuário abrir esse projeto no futuro. Essas cadeias de caracteres, portanto, fornecem uma maneira para o plug-in de controle do código-fonte controlar as informações que ele precisa associar a um projeto.

 Essa função é semelhante ao [SccGetProjPath](../extensibility/sccgetprojpath-function.md), exceto que não solicita que o usuário selecione um projeto. Ele também nunca cria um novo projeto, mas funciona apenas com um projeto existente.

 Quando `SccGetParentProjectPath` é chamado e não estará vazio e `lpProjPath` `lpAuxProjPath` corresponderá a um projeto válido. Essas cadeias de caracteres geralmente são recebidas pelo IDE de uma chamada anterior para a `SccGetProjPath` função.

 O `lpUser` argumento é o nome de usuário. O IDE passará o mesmo nome de usuário que recebeu anteriormente da função e o plug-in de controle do `SccGetProjPath` código-fonte deve usar o nome como padrão. Se o usuário já tiver uma conexão aberta com o plug-in, o plug-in deverá tentar eliminar os prompts para garantir que a função funcione silenciosamente. No entanto, se o logon falhar, o plug-in deverá solicitar ao usuário um logon e, quando receber um logon válido, passe o nome de volta em `lpUser` . Como o plug-in pode alterar essa cadeia de caracteres, o IDE sempre alocará um buffer de tamanho ( `SCC_USER_LEN` +1). Se a cadeia de caracteres for alterada, a nova cadeia de caracteres deverá ser um nome de logon válido (pelo menos tão válido quanto a cadeia de caracteres antiga).

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>Notas técnicas para SccCreateSubProject e SccGetParentProjectPath
 A adição de soluções e projetos ao controle do código-fonte foi simplificada Visual Studio minimizar o número de vezes que um usuário é solicitado a selecionar locais no sistema de controle do código-fonte. Essas alterações serão ativadas por Visual Studio se um plug-in de controle do código-fonte for compatível com ambas as novas funções, [o SccCreateSubProject](../extensibility/scccreatesubproject-function.md) e a `SccGetParentProjectPath` função . No entanto, a seguinte entrada do Registro pode ser usada para desabilitar essas alterações e reverter para o comportamento anterior Visual Studio (API de Plug-in de Controle do Código-Fonte versão 1.1) :

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] "DoNotCreateSolutionRootFolderInSourceControl"=dword:00000001**

 Se essa entrada do Registro não existir ou estiver definida como dword:00000000, o Visual Studio tentará usar as novas funções `SccCreateSubProject` e `SccGetParentProjectPath` .

 Se a entrada do Registro estiver definida como dword:00000001, o Visual Studio não tentará usar essas novas funções e as operações de adição ao controle do código-fonte funcionarão como em versões anteriores do Visual Studio.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccCreateSubProject](../extensibility/scccreatesubproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)

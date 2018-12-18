---
title: Função SccCreateSubProject | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccCreateSubProject
helpviewer_keywords:
- SccCreateSubProject function
ms.assetid: 08154aed-ae5c-463c-8694-745d0e332965
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3aef071d0c124878adf58d8346ad0b50f741300b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49931344"
---
# <a name="scccreatesubproject-function"></a>Função SccCreateSubProject
Essa função cria um subprojeto com o nome fornecido em um projeto existente do pai especificado pelo `lpParentProjPath` argumento.  
  
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
 [in] O ponteiro de contexto de plug-in de controle do código-fonte.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 lpUser  
 [no, out] O nome de usuário (até SCC_USER_SIZE, incluindo o terminador NULL).  
  
 lpParentProjPath  
 [in] Uma cadeia de caracteres que identifica o caminho do projeto pai (até SCC_PRJPATH_SIZE, incluindo o terminador NULL).  
  
 lpSubProjName  
 [in] O nome sugerido subprojeto (até SCC_PRJPATH_SIZE, incluindo o terminador NULL).  
  
 lpAuxProjPath  
 [no, out] Cadeia de caracteres auxiliar que identifica o projeto (até SCC_PRJPATH_SIZE, incluindo o terminador NULL).  
  
 lpSubProjPath  
 [no, out] Cadeia de caracteres de saída identifica o caminho para o subprojeto (até SCC_PRJPATH_SIZE, incluindo o terminador NULL).  
  
## <a name="return-value"></a>Valor retornado  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Subprojeto foi criado com êxito.|  
|SCC_E_INITIALIZEFAILED|Não foi possível inicializar o projeto pai.|  
|SCC_E_INVALIDUSER|O usuário não pôde fazer logon sistema de controle de origem.|  
|SCC_E_COULDNOTCREATEPROJECT|Não é possível criar o subprojeto.|  
|SCC_E_PROJSYNTAXERR|Sintaxe de projeto inválido.|  
|SCC_E_UNKNOWNPROJECT|O projeto pai é desconhecido para o plug-in de controle do código-fonte.|  
|SCC_E_INVALIDFILEPATH|Caminho de arquivo inválido ou inutilizável.|  
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. É recomendável uma nova tentativa.|  
|SCC_E_CONNECTIONFAILURE|Houve um problema de conexão de plug-in de controle do código-fonte.|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Falha não específica.|  
  
## <a name="remarks"></a>Comentários  
 Se um subprojeto com o nome já existir, a função pode alterar o nome padrão para criar um exclusivo, por exemplo, adicionando "_\<número >" para ele. O chamador deve estar preparado para aceitar as alterações `lpUser`, `lpSubProjPath`, e `lpAuxProjPath`. O `lpSubProjPath` e`lpAuxProjPath` argumentos, em seguida, são usados em uma chamada para o [SccOpenProject](../extensibility/sccopenproject-function.md). Eles não devem ser modificados pelo chamador após o retorno. Essas cadeias de caracteres fornecem uma maneira para o plug-in para acompanhar informações que ele precisa ser associado a um projeto de controle de origem. O chamador IDE não exibirá esses dois parâmetros após o retorno, como o plug-in pode usar uma cadeia de caracteres formatada que pode não ser adequada para exibição. A função retorna um código de êxito ou falha e, se for bem-sucedido, preenche a variável `lpSubProjPath` com o caminho completo do projeto para o novo projeto.  
  
 Essa função é semelhante para o [SccGetProjPath](../extensibility/sccgetprojpath-function.md), exceto que ele silenciosamente cria um projeto em vez de solicitar que o usuário selecione um. Quando o `SccCreateSubProject` função é chamada, `lpParentProjName` e `lpAuxProjPath` não estará vazio e corresponderá a um projeto válido. Essas cadeias de caracteres geralmente são recebidas pelo IDE de uma chamada anterior para o `SccGetProjPath` função ou o [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md).  
  
 O `lpUser` argumento é o nome de usuário. O IDE passará o mesmo nome de usuário que ele tivesse sido recebido anteriormente do `SccGetProjPath`, e o plug-in de controle do código-fonte deve usar o nome como padrão. Se o usuário já tiver uma conexão aberta com o plug-in, em seguida, o plug-in deve tentar eliminar os prompts para garantir que a função funciona silenciosamente. No entanto, se o logon falhar, o plug-in deve solicitar ao usuário para um logon e, quando ele recebe um logon válido, passe o nome de volta no `lpUser`. Como o plug-in pode alterar essa cadeia de caracteres, o IDE sempre alocará um buffer de tamanho (SCC_USER_LEN + 1 ou SCC_USER_SIZE, que inclui espaço para o terminador nulo). Se a cadeia de caracteres for alterada, a nova cadeia de caracteres deve ser um nome de logon válido (pelo menos tão válido como a cadeia de caracteres antiga).  
  
## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>Observações técnicas para SccCreateSubProject e SccGetParentProjectPath  
 Adicionando soluções e projetos ao controle de origem foi simplificado no Visual Studio para minimizar o número de vezes que um usuário é solicitado a selecionar locais no sistema de controle de origem. Essas alterações são ativadas pelo Visual Studio, se um plug-in de controle de origem dá suporte às duas novas funções, `SccCreateSubProject` e `SccGetParentProjectPath`. No entanto, a seguinte entrada do registro pode ser usada para desabilitar essas alterações e reverter para o comportamento anterior do Visual Studio (fonte de controle de plug-in API versão 1.1):  
  
 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] "DoNotCreateSolutionRootFolderInSourceControl" = DWORD: 00000001**  
  
 Se essa entrada do registro não existe ou está definida como DWORD: 00000000, Visual Studio tenta usar as novas funções, `SccCreateSubProject` e `SccGetParentProjectPath`.  
  
 Se a entrada do registro é definida como DWORD: 00000001, o Visual Studio não tentará usar essas novas funções e as operações de adição ao controle de origem funcionam como nas versões anteriores do Visual Studio.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in da controle de origem](../extensibility/source-control-plug-in-api-functions.md)   
 [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)   
 [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
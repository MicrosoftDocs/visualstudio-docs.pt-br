---
title: Função SccAddFilesFromSCC | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccAddFilesFromSCC
helpviewer_keywords:
- SccAddFilesFromSCC function
ms.assetid: f21a3500-ade8-4dd8-8647-10e2179be9c1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b827e1f7e26fb98e9d49de4e9fe2388e46ee07cb
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49831166"
---
# <a name="sccaddfilesfromscc-function"></a>Função SccAddFilesFromSCC
Essa função adiciona uma lista de arquivos do controle de origem para o projeto aberto no momento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SCCRTN SccAddFilesFromSCC(  
   LPVOID  pContext,  
   HWND    hWnd,  
   LPSTR   lpUser,  
   LPSTR   lpAuxProjPath,  
   LONG    cFiles,  
   LPCSTR* lpFilePaths,  
   LPCSTR  lpDestination,  
   LPCSTR  lpComment,  
   LPBOOL  pbResults  
);  
```  
  
### <a name="parameters"></a>Parâmetros  
 pContext  
 [in] O ponteiro de contexto de plug-in de controle do código-fonte.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 lpUser  
 [no, out] O nome de usuário (até SCC_USER_SIZE, incluindo o terminador nulo).  
  
 lpAuxProjPath  
 [no, out] Auxiliar cadeia de caracteres que identifica o projeto (até `SCC_PRJPATH_`tamanho, incluindo o terminador nulo).  
  
 cFiles  
 [in] Número de arquivos fornecido por `lpFilePaths`.  
  
 lpFilePaths  
 [no, out] Matriz de nomes de arquivo para adicionar ao projeto atual.  
  
 lpDestination  
 [in] O caminho de destino onde os arquivos devem ser gravados.  
  
 lpComment  
 [in] O comentário a ser aplicado a cada um dos arquivos que está sendo adicionados.  
  
 pbResults  
 [no, out] Matriz de sinalizadores que está definido para indicar êxito (diferente de zero ou TRUE) ou falha (zero ou FALSE) para cada arquivo (tamanho da matriz deve ter pelo menos `cFiles` longo).  
  
## <a name="return-value"></a>Valor retornado  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_E_PROJNOTOPEN|Projeto não está aberto.|  
|SCC_E_OPNOTPERFORMED|Conexão não está no mesmo projeto conforme especificado por `lpAuxProjPath.`|  
|SCC_E_NOTAUTHORIZED|Usuário não está autorizado a atualizar o banco de dados.|  
|SCC_E_NONSPECIFICERROR|Erro desconhecido.|  
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in da controle de origem](../extensibility/source-control-plug-in-api-functions.md)
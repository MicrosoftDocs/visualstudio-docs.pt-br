---
title: Função SccAddFilesFromSCC | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccAddFilesFromSCC
helpviewer_keywords:
- SccAddFilesFromSCC function
ms.assetid: f21a3500-ade8-4dd8-8647-10e2179be9c1
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d5af748c9180644cae928d1b6db3a3f880b6b286
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200914"
---
# <a name="sccaddfilesfromscc-function"></a>Função SccAddFilesFromSCC
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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
  
#### <a name="parameters"></a>Parâmetros  
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
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_E_PROJNOTOPEN|Projeto não está aberto.|  
|SCC_E_OPNOTPERFORMED|Conexão não está no mesmo projeto conforme especificado por `lpAuxProjPath.`|  
|SCC_E_NOTAUTHORIZED|Usuário não está autorizado a atualizar o banco de dados.|  
|SCC_E_NONSPECIFICERROR|Erro desconhecido.|  
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API do plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)

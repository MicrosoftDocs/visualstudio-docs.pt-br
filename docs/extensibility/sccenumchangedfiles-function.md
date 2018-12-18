---
title: Função SccEnumChangedFiles | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccEnumChangedFiles
helpviewer_keywords:
- SccEnumChangedFiles function
ms.assetid: 76cac510-107b-4c1a-ba60-9c39b6db2e71
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7c0284dd268621fddeaa9322c9a3cc17de7a3e71
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49811615"
---
# <a name="sccenumchangedfiles-function"></a>Função SccEnumChangedFiles
Dada uma lista de arquivos locais, esta função determina quais arquivos são diferentes das versões correspondentes no banco de dados de controle de código fonte.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SCCRTN SccEnumChangedFiles(  
   LPVOID  pContext,  
   HWND    hWnd,  
   LONG    cFiles,  
   LPCSTR* lpFileNames,  
   LONG*   plIsFileDifferent  
);  
```  
  
### <a name="parameters"></a>Parâmetros  
 pContext  
 [in] O ponteiro de contexto de plug-in de controle do código-fonte.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 cFiles  
 [in] Número de nomes de arquivo especificados no `lpFileNames` matriz. Também especifica o tamanho do `plIsFileDifferent` matriz.  
  
 lpFileNames  
 [in] Matriz de nomes de arquivo local para verificar.  
  
 plIsFileDifferent  
 [no, out] Matriz de valores que indicam o status de diferença de cada arquivo (matriz deve ter pelo menos `cFiles` entradas). Diferente de zero significa que o arquivo é diferente.  
  
## <a name="return-value"></a>Valor retornado  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Operação concluída com êxito.|  
|SCC_UNSPECIFIEDERROR|Erro genérico.|  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in da controle de origem](../extensibility/source-control-plug-in-api-functions.md)
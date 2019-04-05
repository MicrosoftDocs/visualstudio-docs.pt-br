---
title: Função SccEnumChangedFiles | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccEnumChangedFiles
helpviewer_keywords:
- SccEnumChangedFiles function
ms.assetid: 76cac510-107b-4c1a-ba60-9c39b6db2e71
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 00ef98c93f02aa8e8a1b4ea53f1998d0ab6713a9
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58925068"
---
# <a name="sccenumchangedfiles-function"></a>Função SccEnumChangedFiles
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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
  
#### <a name="parameters"></a>Parâmetros  
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
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Operação concluída com êxito.|  
|SCC_UNSPECIFIEDERROR|Erro genérico.|  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API do plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)

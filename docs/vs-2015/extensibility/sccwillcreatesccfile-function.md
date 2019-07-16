---
title: Função SccWillCreateSccFile | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccWillCreateSccFile
helpviewer_keywords:
- SccWillCreateSccFile function
ms.assetid: 0d7542f0-4351-41b3-b24c-960ab99c05a1
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cb0df475098a0fb0675327cece6dd9c643a0c4d7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68147955"
---
# <a name="sccwillcreatesccfile-function"></a>Função SccWillCreateSccFile
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esta função determina se o plug-in de controle do código-fonte suporta a criação do MSSCCPRJ. Arquivos SCC para cada um dos arquivos de determinado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
SCCRTN SccWillCreateSccFile(  
   LPVOID  pContext,  
   LONG    nFiles,  
   LPCSTR* lpFileNames,  
   LPBOOL  pbSccFiles  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pContext  
 [in] O ponteiro de contexto de plug-in de controle do código-fonte.  
  
 nFiles  
 [in] O número de nomes de arquivos incluídos na `lpFileNames` matriz, bem como o comprimento do `pbSccFiles` matriz.  
  
 lpFileNames  
 [in] Uma matriz de nomes de arquivo totalmente qualificado para verificar (matriz deve ser alocada pelo chamador).  
  
 pbSccFiles  
 [no, out] Matriz na qual armazenar os resultados.  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Êxito.|  
|SCC_E_INVALIDFILEPATH|Um dos caminhos na matriz é inválido.|  
|SCC_E_NONSPECIFICERROR|Falha não específica.|  
  
## <a name="remarks"></a>Comentários  
 Essa função é chamada com uma lista de arquivos para determinar se o plug-in de controle do código-fonte fornece suporte no MSSCCPRJ. Arquivos SCC para cada um dos arquivos de determinado (para obter mais informações sobre o MSSCCPRJ. Arquivos SCC, consulte [MSSCCPRJ. Arquivos SCC](../extensibility/mssccprj-scc-file.md)). Plug-ins de controle de origem pode declarar se eles têm a capacidade de criar MSSCCPRJ. Arquivos SCC, declarando `SCC_CAP_SCCFILE` durante a inicialização. O plug-in retorna `TRUE` ou `FALSE` por arquivo no `pbSccFiles` matriz para indicar quais arquivos de determinado têm MSSCCPRJ. Suporte do SCC. Se o plug-in retorna um código de êxito da função, os valores na matriz de retorno são respeitados. Em caso de falha, a matriz é ignorada.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [Arquivo MSSCCPRJ.SCC](../extensibility/mssccprj-scc-file.md)

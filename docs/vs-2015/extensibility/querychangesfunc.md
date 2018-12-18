---
title: QUERYCHANGESFUNC | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- QUERYCHANGESFUNC
helpviewer_keywords:
- QUERYCHANGESFUNC callback function
- QUERYCHANGESDATA structure
ms.assetid: 9d383e2c-eee1-4996-973a-0652d4c5951c
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: b9a0bbf3c26f797ec1bbf67ad8439e5f5ba05b11
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764217"
---
# <a name="querychangesfunc"></a>QUERYCHANGESFUNC
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa é uma função de retorno de chamada usada pelas [SccQueryChanges](../extensibility/sccquerychanges-function.md) operação para enumerar uma coleção de nomes de arquivo e determinar o status de cada arquivo.  
  
 O `SccQueryChanges` função é fornecida uma lista de arquivos e um ponteiro para o `QUERYCHANGESFUNC` retorno de chamada. O plug-in de controle de origem enumera a lista fornecida e fornece o status (por meio desse retorno de chamada) para cada arquivo na lista.  
  
## <a name="signature"></a>Assinatura  
  
```cpp#  
typedef BOOL (*QUERYCHANGESFUNC)(  
   LPVOID pvCallerData,  
   QUERYCHANGESDATA * pChangesData  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 pvCallerData  
 [in] O `pvCallerData` parâmetro é passado pelo chamador (IDE) para [SccQueryChanges](../extensibility/sccquerychanges-function.md). O plug-in de controle do código-fonte não deve fazer nenhuma suposição sobre o conteúdo desse valor.  
  
 pChangesData  
 [in] Ponteiro para um [QUERYCHANGESDATA estrutura](#LinkQUERYCHANGESDATA) estrutura que descreve as alterações em um arquivo.  
  
## <a name="return-value"></a>Valor de retorno  
 O IDE retorna um código de erro apropriado:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Continue o processamento.|  
|SCC_I_OPERATIONCANCELED|Pare o processamento.|  
|SCC_E_xxx|Qualquer erro de SCC apropriado deve parar o processamento.|  
  
##  <a name="LinkQUERYCHANGESDATA"></a> Estrutura QUERYCHANGESDATA  
 A estrutura passada para cada arquivo é semelhante ao seguinte:  
  
```cpp#  
struct QUERYCHANGESDATA_A  
{  
    DWORD  dwSize;  
    LPCSTR lpFileName;  
    DWORD  dwChangeType;  
    LPCSTR lpLatestName;  
};  
  
typedef struct QUERYCHANGESDATA_A QUERYCHANGESDATA;  
  
struct QUERYCHANGESDATA_W  
{  
    DWORD   dwSize;  
    LPCWSTR lpFileName;  
    DWORD   dwChangeType;  
    LPCWSTR lpLatestName;  
};  
```  
  
 dwSize  
 Tamanho desta estrutura (em bytes).  
  
 lpFileName  
 O nome do arquivo original desse item.  
  
 dwChangeType  
 Código que indica o status do arquivo:  
  
|Código|Descrição|  
|----------|-----------------|  
|`SCC_CHANGE_UNKNOWN`|Não é possível dizer o que mudou.|  
|`SCC_CHANGE_UNCHANGED`|Nenhuma alteração de nome para esse arquivo.|  
|`SCC_CHANGE_DIFFERENT`|Arquivo com uma identidade diferente, mas o mesmo nome existe no banco de dados.|  
|`SCC_CHANGE_NONEXISTENT`|Arquivo não existe no banco de dados ou localmente.|  
|`SCC_CHANGE_DATABASE_DELETED`|Arquivo excluído no banco de dados.|  
|`SCC_CHANGE_LOCAL_DELETED`|Arquivo excluído localmente, mas o arquivo ainda existe no banco de dados. Se isso não puder ser determinado, retornar `SCC_CHANGE_DATABASE_ADDED`.|  
|`SCC_CHANGE_DATABASE_ADDED`|Arquivo adicionado ao banco de dados, mas não existe localmente.|  
|`SCC_CHANGE_LOCAL_ADDED`|Arquivo não existe no banco de dados e é um novo arquivo local.|  
|`SCC_CHANGE_RENAMED_TO`|Arquivo renomeado ou movido no banco de dados `lpLatestName`.|  
|`SCC_CHANGE_RENAMED_FROM`|Arquivo renomeado ou movido no banco de dados do `lpLatestName`; se isso é muito caro para acompanhar, retornam um sinalizador diferente, como `SCC_CHANGE_DATABASE_ADDED`.|  
  
 lpLatestName  
 O nome do arquivo atual para este item.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de retorno de chamada implementadas pelo IDE](../extensibility/callback-functions-implemented-by-the-ide.md)   
 [SccQueryChanges](../extensibility/sccquerychanges-function.md)   
 [Códigos de erro](../extensibility/error-codes.md)


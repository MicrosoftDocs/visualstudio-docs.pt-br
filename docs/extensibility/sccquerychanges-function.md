---
title: Função SccQueryChanges | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccQueryChanges
helpviewer_keywords:
- SccQueryChanges function
ms.assetid: 4cd58eb3-6952-49b1-9620-8682e3eaa604
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: f7b3a9454daa0f2e3c5cf91a9dc483afe1f635a1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49915705"
---
# <a name="sccquerychanges-function"></a>Função SccQueryChanges
Essa função enumera uma determinada lista de arquivos, fornecendo informações sobre as alterações de nome para cada arquivo por meio de uma função de retorno de chamada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SCCRTN SccQueryChanges(  
   LPVOID           pContext,  
   LONG             nFiles,  
   LPCSTR*          lpFileNames,  
   QUERYCHANGESFUNC pfnCallback,  
   LPVOID           pvCallerData  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pContext  
 [in] O ponteiro de contexto de plug-in de controle do código-fonte.  
  
 nFiles  
 [in] Número de arquivos na `lpFileNames` matriz.  
  
 lpFileNames  
 [in] Matriz de nomes de arquivo para obter informações sobre.  
  
 pfnCallback  
 [in] Função de retorno de chamada a ser chamada para cada nome de arquivo na lista (consulte [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md) para obter detalhes).  
  
 pvCallerData  
 [in] Valor que será passado sem alteração para a função de retorno de chamada.  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|O processo de consulta foi concluído com êxito.|  
|SCC_E_PROJNOTOPEN|O projeto não foi aberto no controle de origem.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção.|  
|SCC_E_NONSPECIFICERROR|Ocorreu um erro não especificado ou geral.|  
  
## <a name="remarks"></a>Comentários  
 As alterações que está sendo consultadas para são para o namespace: especificamente, renomear, adicionando e removendo um arquivo.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)   
 [Códigos de erro](../extensibility/error-codes.md)
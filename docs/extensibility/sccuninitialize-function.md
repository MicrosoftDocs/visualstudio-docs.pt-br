---
title: Função SccUninitialize | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccUninitialize
helpviewer_keywords:
- SccUninitialize function
ms.assetid: 17cf5337-d251-4422-bc96-93fe7d48f2ae
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 64e894fe2ce1eaf6f74ed01d2e76f7ce3d33f9fb
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53949635"
---
# <a name="sccuninitialize-function"></a>Função SccUninitialize
Essa função limpa alocações ou abra conexões criadas por uma chamada anterior para o [SccInitialize](../extensibility/sccinitialize-function.md) em preparação para desligar o plug-in de controle do código-fonte.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SCCRTN SccUninitialize (  
   LPVOID pvContext  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] O ponteiro para a estrutura de contexto plug-in de controle do código-fonte criado na [SccInitialize](../extensibility/sccinitialize-function.md).  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|A limpeza foi concluída com êxito.|  
  
## <a name="remarks"></a>Comentários  
 O plug-in de controle do código-fonte é responsável por se preparando para ser desligar e liberar memória que o plug-in foi alocada para a estrutura de contexto. A função é chamada uma vez para cada determinada instância de um plug-in. Uma chamada para o [SccInitialize](../extensibility/sccinitialize-function.md) precede essa chamada. Não há projetos ainda podem ser abertos no momento da chamada para `SccUninitialize`.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [SccInitialize](../extensibility/sccinitialize-function.md)
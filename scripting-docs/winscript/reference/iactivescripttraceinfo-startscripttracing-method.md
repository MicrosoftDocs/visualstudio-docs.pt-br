---
title: 'Método: Startscripttracing | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 90fac5ed-ce15-49b7-a6f1-605ede6f34e2
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e999ad0d40f4d832330fee6db17b64ae9da50f08
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724876"
---
# <a name="iactivescripttraceinfostartscripttracing-method"></a>Método IActiveScriptTraceInfo::StartScriptTracing
Inicia o rastreamento de script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT StartScriptTracing(     [in] IActiveScriptSiteTraceInfo * pSiteTraceInfo,     [in] GUID guidContextID );   
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pSiteTraceInfo`  
 Um ponteiro para IActiveScriptSiteTraceInfo do host.  
  
 `guidContextId`  
 O GUID do contexto.  
  
## <a name="return-value"></a>Valor de retorno  
 Os valores de retorno possíveis para esse método são os seguintes:  
  
1.  S_OK: êxito.  
  
2.  E_POINTER: `pSiteTraceInfo` é um ponteiro NULL.  
  
3.  E_NOTIMPL: Não implementado.
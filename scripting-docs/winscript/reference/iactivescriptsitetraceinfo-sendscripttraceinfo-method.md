---
title: 'Método: Sendscripttraceinfo | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0419e4c5-eb7c-45a3-b6dc-1a5e157d95f9
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5290cc6a92be7c8bc99e4715c77bfe6f8f6abb53
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724836"
---
# <a name="iactivescriptsitetraceinfosendscripttraceinfo-method"></a>Método IActiveScriptSiteTraceInfo::SendScriptTraceInfo
Envia informações de rastreamento que incluem o tipo de evento, o contexto e a instrução de script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT SendScriptTraceInfo(     [in] SCRIPTTRACEINFO stiEventType,     [in] GUID guidContextID,     [in] DWORD dwScriptContextCookie,     [in] LONG lScriptStatementStart,     [in] LONG lScriptStatementEnd,     [in] DWORD64 dwReserved );   
```  
  
#### <a name="parameters"></a>Parâmetros  
 `stiEventType`  
 O tipo de evento.  
  
 `guidContextId`  
 O GUID do contexto.  
  
 `dwScriptContextCookie`  
 O cookie do contexto.  
  
 `lScriptStatementStart`  
 O local de início da instrução de script.  
  
 `lScriptStatementEnd`  
 A localização do final da instrução de script.  
  
 `dwReserved`  
 Reservado.
---
title: SuspendTracking | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
api_name:
- SuspendTracking
api_location:
- filetracker.dll
api_type:
- COM
helpviewer_keywords:
- SuspendTracking
ms.assetid: f5e06e5a-8083-444c-99c1-07ba834226b5
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3b2d7811a40e87cb5fd19785fc387aad02a7ad07
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201741"
---
# <a name="suspendtracking"></a>SuspendTracking
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Suspende o acompanhamento no contexto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT WINAPI SuspendTracking(void);  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um [HRESULT] (<!-- TODO: review code entity reference <xref:assetId:///HRESULT?qualifyHint=False&amp;autoUpgrade=True>  -->) com [êxito] (<!-- TODO: review code entity reference <xref:assetId:///SUCCEEDED?qualifyHint=False&amp;autoUpgrade=True>  -->) conjunto de bits se o rastreamento foi suspenso.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** FileTracker.h  
  
## <a name="see-also"></a>Consulte Também  
 [ResumeTracking](../msbuild/resumetracking.md)

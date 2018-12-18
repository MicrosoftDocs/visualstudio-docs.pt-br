---
title: Enumeração DOCUMENTNAMETYPE | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DOCUMENTNAMETYPE
apilocation:
- scrobj.dll
helpviewer_keywords:
- DOCUMENTNAMETYPE enumeration
ms.assetid: d36d550e-efb4-493d-8971-4de267005654
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a0bd21dddd209f21ae64ea2775bbaa0da226f077
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24640576"
---
# <a name="documentnametype-enumeration"></a>Enumeração DOCUMENTNAMETYPE
Descreve os tipos para se obter um documento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef enum tagDOCUMENTNAMETYPE {  
   DOCUMENTNAMETYPE_APPNODE,  
   DOCUMENTNAMETYPE_TITLE,  
   DOCUMENTNAMETYPE_FILE_TAIL,  
   DOCUMENTNAMETYPE_URL,  
DOCUMENTNAMETYPE_UNIQUE_TITLE,} DOCUMENTNAMETYPE;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Descrição|  
|------------|-----------------|  
|DOCUMENTNAMETYPE_APPNODE|Obtém o nome como ele aparece na árvore do aplicativo.|  
|DOCUMENTNAMETYPE_TITLE|Obtém o nome como ele aparece na barra de título do visualizador.|  
|DOCUMENTNAMETYPE_FILE_TAIL|Obtém o nome do arquivo sem um caminho.|  
|DOCUMENTNAMETYPE_URL|Obtém a URL do documento.|  
|DOCUMENTNAMETYPE_UNIQUE_TITLE|Obtém o título acrescentado com enumeração para identificação.|  
  
## <a name="see-also"></a>Consulte também  
 [Constantes, enumerações e estruturas de depurador do script ativo](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)
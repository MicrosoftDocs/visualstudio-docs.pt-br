---
title: Constantes TEXT_DOC_ATTR | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- TEXT_DOC_ATTR
apilocation:
- scrobj.dll
helpviewer_keywords:
- TEXT_DOC_ATTR constants
ms.assetid: fd9c53a4-8f73-4c6a-abe5-6b831ecd5b1e
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3604c06b6cb36cc4ff7ef6c76348b5ece53bed61
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572990"
---
# <a name="text_doc_attr-constants"></a>Constantes TEXT_DOC_ATTR
Descrevem os atributos do documento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
typedef DWORD TEXT_DOC_ATTR;  
```  
  
## <a name="constants"></a>Constantes  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|TEXT_DOC_ATTR_READONLY|0x00000001|O documento é somente leitura.|  
|TEXT_DOC_ATTR_TYPE_PRIMARY|0x00000002|O documento é o arquivo primário desta árvore de documentos.|  
|TEXT_DOC_ATTR_TYPE_WORKER|0x00000004|O documento é um trabalhador.|  
|TEXT_DOC_ATTR_TYPE_SCRIPT|0x00000008|O documento é um arquivo de script.|  
  
## <a name="see-also"></a>Consulte também  
 [Constantes, enumerações e estruturas de depurador do script ativo](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)
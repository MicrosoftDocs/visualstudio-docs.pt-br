---
title: Estrutura TEXT_DOCUMENT_ARRAY | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- TEXT_DOCUMENT_ARRAY Structure
ms.assetid: 47c08f23-981b-4105-9240-6dfffc6cb91b
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b52b382aa1e91e509672728a3c8f931bfeae27a9
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572977"
---
# <a name="text_document_array-structure"></a>Estrutura TEXT_DOCUMENT_ARRAY
Uma matriz de objetos de [interface IDebugDocumentText](../../winscript/reference/idebugdocumenttext-interface.md) . Os membros são alocados com CoTaskMemAlloc.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
typedef struct tagTEXT_DOCUMENT_ARRAY{    DWORD dwCount;    [size_is(dwCount)] IDebugDocumentText **Members;} TEXT_DOCUMENT_ARRAY;  
```  
  
## <a name="members"></a>Membros  
 `dwCount`  
 O número de documentos.  
  
 `Members`  
 O conjunto de documentos.  
  
## <a name="see-also"></a>Consulte também  
 [Constantes, enumerações e estruturas de depurador do script ativo](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)
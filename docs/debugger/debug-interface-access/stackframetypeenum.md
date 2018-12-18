---
title: StackFrameTypeEnum | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- StackFrameTypeEnum enumeration
ms.assetid: 61e40163-eee0-4c1f-af47-cef3771bdc41
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fcf5e120e769b69c064306432c3026194eb0d851
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49853913"
---
# <a name="stackframetypeenum"></a>StackFrameTypeEnum
Especifica o tipo de quadro de pilha.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
enum StackFrameTypeEnum {  
   FrameTypeFPO,  
   FrameTypeTrap,  
   FrameTypeTSS,  
   FrameTypeStandard,  
   FrameTypeFrameData,  
   FrameTypeUnknown = -1  
};  
```  
  
## <a name="elements"></a>Elementos  
 `FrameTypeFPO`  
 Ponteiro de quadro especificado; Informações de FPO disponíveis.  
  
 `FrameTypeTrap`  
 Quadro de interceptação de kernel.  
  
 `FrameTypeTSS`  
 Quadro de interceptação de kernel.  
  
 `FrameTypeStandard`  
 Quadro de pilha EBP padrão.  
  
 `FrameTypeFrameData`  
 Ponteiro de quadro especificado; Informações de dados de quadro disponíveis.  
  
 `FrameTypeUnknown`  
 Quadro que não tem nenhuma informação de depuração.  
  
## <a name="remarks"></a>Comentários  
 Os valores nesta enumeração são retornados por uma chamada para o [idiastackframe:: Get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md) método.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: cvconst.h  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)
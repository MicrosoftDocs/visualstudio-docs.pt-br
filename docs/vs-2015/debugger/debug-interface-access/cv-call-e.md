---
title: CV_call_e | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_call_e enumeration
ms.assetid: f230560b-4243-432d-8f19-46df112043b9
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cd1ee4c024894e5752277a5000d37745c88c4ac6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442099"
---
# <a name="cvcalle"></a>CV_call_e
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Especifica a convenção de chamada para uma função.  
  
> [!NOTE]
> Somente os valores de enumeração mais comuns são documentados aqui. A enumeração completa está disponível no arquivo de cabeçalho cvconst.h.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
typedef enum CV_call_e {   
   CV_CALL_NEAR_C    = 0x00,  
   CV_CALL_NEAR_FAST = 0x04,  
   CV_CALL_NEAR_STD  = 0x07,  
   CV_CALL_NEAR_SYS  = 0x09,  
   CV_CALL_THISCALL  = 0x0b,  
   CV_CALL_CLRCALL   = 0x16  
} CV_call_e;  
```  
  
## <a name="elements"></a>Elementos  
 CV_CALL_NEAR_C  
 Especifica uma convenção de chamada de função usando um próximo envio por push da direita para esquerda. A função chamada limpa a pilha.  
  
 CV_CALL_NEAR_FAST  
 Especifica uma convenção de chamada de função usando um próximo envio por push da esquerda para a direita com registros. A função chamada usa a soma dos bytes de parâmetro para limpar a pilha.  
  
 CV_CALL_NEAR_STD  
 Especifica uma convenção de chamada de função usando uma chamada padrão quase (push da direita para esquerda).  
  
 CV_CALL_NEAR_SYS  
 Especifica uma convenção de chamada de função usando uma chamada de sistema quase.  
  
 CV_CALL_THISCALL  
 Especifica uma convenção de chamada de função usando `this` chamar (`this` ponteiro passados no registro).  
  
 CV_CALL_CLRCALL  
 Especifica uma convenção de chamada de função usada pelo tempo de execução do CLR (Common Language) (também conhecido como um código gerenciado convenção de chamada).  
  
## <a name="remarks"></a>Comentários  
 Os valores nesta enumeração são retornados por uma chamada para o [idiasymbol:: Get_callingconvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md) método.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: cvconst.h  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)

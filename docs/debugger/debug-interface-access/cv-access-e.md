---
title: CV_access_e | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- CV_access_e enumeration
ms.assetid: 33c05d65-abb4-4800-a382-54a3805ea7b0
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b6de95d74b8d7edc3bde08437c3d018270758112
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49878980"
---
# <a name="cvaccesse"></a>CV_access_e
Especifica o escopo de visibilidade (nível de acesso) de funções de membro e variáveis.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
typedef enum CV_access_e {   
   CV_private   = 1,  
   CV_protected = 2,  
   CV_public    = 3  
} CV_access_e;  
```  
  
## <a name="elements"></a>Elementos  
 CV_private  
 Membro tem acesso privado.  
  
 CV_protected  
 Membro tenha acesso protegido.  
  
 CV_public  
 Membro tem o acesso público.  
  
## <a name="remarks"></a>Comentários  
 O `friend` especificador de acesso não é incluída aqui porque ele é normalmente usado por funções não membro que têm acesso a elementos particulares e protegidos da classe. Use o [idiasymbol:: Get_symtag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md) método para localizar símbolos com `SymTagFriend` acesso.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: cvconst.h  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [Idiasymbol:: Get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)   
 [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)
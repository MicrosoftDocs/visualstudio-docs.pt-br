---
title: CV_access_e | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_access_e enumeration
ms.assetid: 33c05d65-abb4-4800-a382-54a3805ea7b0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 00be9f52b8cac067e1d8482fe0378737c68909c4
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462144"
---
# <a name="cv_access_e"></a>CV_access_e
Especifica o escopo de visibilidade (nível de acesso) de funções e variáveis de membro.

## <a name="syntax"></a>Syntax

```C++
typedef enum CV_access_e {
    CV_private   = 1,
    CV_protected = 2,
    CV_public    = 3
} CV_access_e;
```

## <a name="elements"></a>Elementos
CV_private membro tem acesso privado.

CV_protected membro tem acesso protegido.

CV_public membro tem acesso público.

## <a name="remarks"></a>Comentários
O `friend` especificador de acesso não está incluído aqui porque normalmente é usado por funções que não são membros que têm acesso a elementos privados e protegidos da classe. Use o método [IDiaSymbol:: get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md) para localizar símbolos com `SymTagFriend` acesso.

## <a name="requirements"></a>Requisitos
Cabeçalho: cvconst. h

## <a name="see-also"></a>Veja também
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)
- [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)

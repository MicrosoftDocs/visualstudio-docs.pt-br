---
title: IDiaEnumSectionContribs::get__NewEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::get__NewEnum method
ms.assetid: a16ee92f-3081-416a-98f6-ce6bc8288a8b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4bbd4e2d818fe2e795b03536b514297a05771e92
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744307"
---
# <a name="idiaenumsectioncontribsget__newenum"></a>IDiaEnumSectionContribs::get__NewEnum
Recupera a versão <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> deste enumerador.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get__NewEnum ( 
   IUnknown** pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 pRetVal

fora Retorna a interface de `IUnknown` que representa a versão de <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> deste enumerador.

## <a name="return-value"></a>Valor retornado
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Consulte também
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
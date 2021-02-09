---
title: IDiaEnumSectionContribs::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Clone method
ms.assetid: 81d3f3a7-3684-4e5c-b028-29b268684a2c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: de315b7d44b2156c1f03aedd3cfd78389a2635dc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99856512"
---
# <a name="idiaenumsectioncontribsclone"></a>IDiaEnumSectionContribs::Clone
Cria um enumerador que contém o mesmo estado de enumeração que o enumerador atual.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Clone( 
   IDiaEnumSectionContrib** ppenum
);
```

#### <a name="parameters"></a>Parâmetros
 ppenum

fora Retorna um objeto [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md) que contém uma duplicata do enumerador. As contribuições da seção não são duplicadas, somente o enumerador.

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Consulte também
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
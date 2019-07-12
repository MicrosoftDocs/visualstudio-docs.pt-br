---
title: IDiaSymbol::get_offsetInUdt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_offsetInUdt method
ms.assetid: 442f20d9-9d6a-44a1-83fb-c3f8c14b6c97
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 14832698e186e23b33862ccb1c9f22f3792a6300
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "64793776"
---
# <a name="idiasymbolgetoffsetinudt"></a>IDiaSymbol::get_offsetInUdt
Recupera o deslocamento para o início de um tipo definido pelo usuário (UDT) de um membro no UDT.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_offsetInUdt( 
   DWORD* pRetVal)
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

[out] Retorna o deslocamento em bytes, do local do símbolo.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 Essa função é usada somente em registros locais em uma compilação otimizada.

## <a name="requirements"></a>Requisitos
 Cabeçalho: Dia2.h

 Biblioteca: diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>Consulte também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
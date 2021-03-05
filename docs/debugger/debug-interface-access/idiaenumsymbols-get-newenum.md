---
description: Recupera a versão de System. Runtime. InteropServices. ComTypes. IEnumVARIANT do enumerador de símbolos.
title: IDiaEnumSymbols::get__NewEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols::get__NewEnum method
ms.assetid: 879609ea-8e5a-4fa3-afa6-d24870fb4392
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ec594958912a4f964f876665e229bf66b77b6968
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102148713"
---
# <a name="idiaenumsymbolsget__newenum"></a>IDiaEnumSymbols::get__NewEnum
Recupera a <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> versão deste enumerador.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get__NewEnum ( 
   IUnknown** pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 pRetVal

fora Retorna a `IUnknown` interface que representa a <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> versão deste enumerador.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

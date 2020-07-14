---
title: IDiaReadExeAtRVACallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtRVACallback interface
ms.assetid: b2892513-3952-4f99-9b98-60cb9b1fdc91
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8fc4d27f3ef8c9329feddd6bf7d8342ceae1b263
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466451"
---
# <a name="idiareadexeatrvacallback"></a>IDiaReadExeAtRVACallback
Permite que um aplicativo cliente forneça bytes de um arquivo executável, conforme especificado por um endereço virtual relativo.

## <a name="syntax"></a>Syntax

```
IDiaReadExeAtRVACallback : IUnknown
```

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDiaReadExeAtRVACallback` .

|Método|Descrição|
|------------|-----------------|
|[IDiaReadExeAtRVACallback::ReadExecutableAtRVA](../../debugger/debug-interface-access/idiareadexeatrvacallback-readexecutableatrva.md)|Lê o número especificado de bytes começando no endereço virtual relativo (RVA) especificado do arquivo executável.|

## <a name="remarks"></a>Comentários
 O aplicativo cliente implementa essa interface para fornecer os bytes do executável usando um endereço virtual relativo no arquivo do executável. Para usar um deslocamento de arquivo absoluto, implemente a interface [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md) .

## <a name="notes-for-callers"></a>Observações para chamadores
 Esse método é implementado pelo aplicativo cliente e passado para o método [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) como um método alternativo para ler o arquivo.

## <a name="requirements"></a>Requisitos
 Cabeçalho: dia2. h

 Biblioteca: diaguids. lib

 DLL: msdia80.dll

## <a name="see-also"></a>Veja também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
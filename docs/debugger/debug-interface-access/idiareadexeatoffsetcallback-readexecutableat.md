---
description: Lê o número especificado de bytes começando no deslocamento especificado a partir de um arquivo executável.
title: IDiaReadExeAtOffsetCallback::ReadExecutableAt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtOffsetCallback::ReadExecutableAt method
ms.assetid: 30b1cef0-b366-4712-8e89-d21f640964f8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9986ba6d493353644d8387b2df36a96cbf542933
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102157359"
---
# <a name="idiareadexeatoffsetcallbackreadexecutableat"></a>IDiaReadExeAtOffsetCallback::ReadExecutableAt
Lê o número especificado de bytes começando no deslocamento especificado a partir de um arquivo executável.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT ReadExecutableAt ( 
   DWORDLONG fileOffset,
   DWORD     cbData,
   DWORD*    pcbData,
   BYTE      data[]
);
```

#### <a name="parameters"></a>Parâmetros
 fileOffset

no O deslocamento no arquivo executável para começar a leitura.

 cbData

no Número de bytes a serem lidos.

 pcbData

fora Retorna o número de bytes lidos.

 data[]

[entrada, saída] Uma matriz que é preenchida com bytes lidos do arquivo.

## <a name="remarks"></a>Comentários
 Esse método é chamado pelo código de suporte do DIA para carregar bytes de dados de um executável usando um deslocamento de arquivo absoluto. Esse método é chamado no suporte do método [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) .

## <a name="see-also"></a>Confira também
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)

---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 741fd417fa6ce8e8a2faf714038aaa3d0f798233
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466472"
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

## <a name="see-also"></a>Veja também
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
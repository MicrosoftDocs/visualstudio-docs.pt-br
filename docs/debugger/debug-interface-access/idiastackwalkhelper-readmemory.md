---
description: Lê um bloco de dados da imagem do executável na memória.
title: IDiaStackWalkHelper::readMemory | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::readMemory method
ms.assetid: e1eb90aa-49b7-476c-9e70-7e8f08994cbe
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a70cc9660e872a3e64e202d7498814b3aa24daa3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158883"
---
# <a name="idiastackwalkhelperreadmemory"></a>IDiaStackWalkHelper::readMemory
Lê um bloco de dados da imagem do executável na memória.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT readMemory( 
   enum MemoryTypeEnum type,
   ULONGLONG           va,
   DWORD               cbData,
   DWORD*              pcbData,
   BYTE*               pbData
);
```

#### <a name="parameters"></a>Parâmetros
 `type`

no Um valor da enumeração de [Enumeração MemoryTypeEnum](../../debugger/debug-interface-access/memorytypeenum.md) especificando o tipo de memória a ser lido.

 va

no Endereço virtual na imagem a partir da qual começar a ler.

 `cbData`

no O tamanho do buffer de dados em bytes.

 `pcbData`

fora Retorna o número de bytes realmente lidos. Se `pbData` for `NULL` , este é o número total de bytes de dados disponíveis.

 `pbData`

[entrada, saída] Um buffer que é preenchido com a leitura de memória.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [Enumeração MemoryTypeEnum](../../debugger/debug-interface-access/memorytypeenum.md)

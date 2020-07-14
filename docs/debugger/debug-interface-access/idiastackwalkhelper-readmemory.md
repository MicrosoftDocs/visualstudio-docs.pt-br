---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bc768db3f42f610a8efd30cea567e721929cb291
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464691"
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

## <a name="see-also"></a>Veja também
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [Enumeração MemoryTypeEnum](../../debugger/debug-interface-access/memorytypeenum.md)
---
description: Lê a memória da imagem.
title: 'IDiaStackWalkFrame:: readMemory | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::readMemory method
ms.assetid: 7ab0b525-a5a7-4692-acad-e8c00fa9ab9a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: edfe15c8303236f31ab50a948a8b5506cee0356b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158918"
---
# <a name="idiastackwalkframereadmemory"></a>IDiaStackWalkFrame::readMemory
Lê a memória da imagem.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT readMemory ( 
   MemoryTypeEnum type,
   ULONGLONG va,
   DWORD     cbData,
   DWORD*    pcbData,
   BYTE      data[]
);
```

#### <a name="parameters"></a>Parâmetros
 `type`

no Um dos valores de enumeração de [Enumeração MemoryTypeEnum](../../debugger/debug-interface-access/memorytypeenum.md) que especifica o tipo de memória a ser acessado.

 `va`

no Local de endereço virtual na imagem para começar a leitura.

 `cbData`

no Tamanho do buffer de dados, em bytes.

 `pcbData`

fora Retorna o número de bytes retornados. Se `data` for `NULL` , `pcbData` conterá o número total de bytes de dados disponíveis.

 `data`

fora Um buffer que deve ser preenchido com dados do local especificado.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)

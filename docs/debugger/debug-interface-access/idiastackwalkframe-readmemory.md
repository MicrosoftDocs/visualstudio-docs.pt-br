---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f682f3fe0e300f84dc28b959497138a5019f954b
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464824"
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

## <a name="see-also"></a>Veja também
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
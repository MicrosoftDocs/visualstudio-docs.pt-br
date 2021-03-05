---
description: Define o alinhamento da imagem.
title: IDiaAddressMap::put_imageAlign | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_imageAlign method
ms.assetid: f9ce875d-c263-43e5-a534-f34c37f9866f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0c3027332018441efd132cc941d16aab3bcab594
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158364"
---
# <a name="idiaaddressmapput_imagealign"></a>IDiaAddressMap::put_imageAlign
Define o alinhamento da imagem.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT put_imageAlign ( 
   DWORD NewVal
);
```

#### <a name="parameters"></a>Parâmetros
 NewVal

no O novo valor de alinhamento da imagem para o executável.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Imagens (executáveis carregados) são alinhadas aos limites de memória especificados. Esse alinhamento pode ser afetado pela arquitetura atual do sistema e pelas opções de compilação e link de tempo. O alinhamento da imagem está sempre em limites de byte. Os seguintes valores de alinhamento de imagem são válidos: os limites 1, 2, 4, 8, 16, 32 e 64 bytes.

 O alinhamento da imagem atual pode ser recuperado com uma chamada para o método [IDiaAddressMap:: get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md) .

> [!NOTE]
> A imagem já está carregada no momento em que esse método pode ser chamado. O `put_imageAlign` método normalmente é usado quando a imagem é movida ou alterada e um novo alinhamento é necessário.

## <a name="see-also"></a>Confira também
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)

---
description: Recupera os bytes de soma de verificação.
title: IDiaSourceFile::get_checksum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksum method
ms.assetid: aad63a7e-4e22-44e4-8a5b-81b5174ced1e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8aac5b35c98b8bb5b11bc623a274949ee32d9229
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147593"
---
# <a name="idiasourcefileget_checksum"></a>IDiaSourceFile::get_checksum
Recupera os bytes de soma de verificação.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_checksum ( 
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>Parâmetros
 `cbData`

no Tamanho do buffer de dados, em bytes.

 `pcbData`

fora Retorna o número de bytes de soma de verificação. O parâmetro não pode ser `NULL`.

 `data`

[entrada, saída] Um buffer que é preenchido com os bytes de soma de verificação. Se esse parâmetro for `NULL` , `pcbData` retorna o número de bytes necessários.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Para determinar o tipo de algoritmo de soma de verificação que foi usado para gerar os bytes de soma de verificação, chame o método [IDiaSourceFile:: get_checksumType](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md) .

 A soma de verificação normalmente é gerada a partir da imagem do arquivo de origem para que as alterações no arquivo de origem sejam refletidas nas alterações nos bytes de soma de verificação. Se os bytes de soma de verificação não corresponderem a uma soma de verificação gerada a partir da imagem carregada do arquivo, o arquivo deverá ser considerado danificado ou adulterado.

 As somas de verificação típicas nunca têm mais de 32 bytes, mas não pressupõem que seja o tamanho máximo de uma soma de verificação. Defina o `data` parâmetro como `NULL` para obter o número de bytes necessários para recuperar a soma de verificação. Em seguida, aloque um buffer do tamanho apropriado e chame esse método mais uma vez com o novo buffer.

## <a name="see-also"></a>Confira também
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSourceFile::get_checksumType](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md)

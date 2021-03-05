---
description: Recupera o tipo de soma de verificação.
title: IDiaSourceFile::get_checksumType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksumType method
ms.assetid: 4c363e61-a6a9-409a-9cc0-d06eb2bee645
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 10aa0d0d7273c75bca0f6d3492b1422af08f50d1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147586"
---
# <a name="idiasourcefileget_checksumtype"></a>IDiaSourceFile::get_checksumType
Recupera o tipo de soma de verificação.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_checksumType ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o tipo de soma de verificação.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O tipo de soma de verificação é um valor que pode ser mapeado para um algoritmo de soma de verificação. Por exemplo, o formato de arquivo PDB padrão normalmente pode ter um dos seguintes valores:

|Tipo de soma de verificação|Rótulo de CryptoAPI|Descrição|
|-------------------|---------------------|-----------------|
|0|\<none>|Nenhuma soma de verificação presente.|
|1|`CALG_MD5`|soma de verificação gerada com o algoritmo de hash MD5.|
|2|`CALG_SHA1`|soma de verificação gerada com o algoritmo de hash SHA1.|

 Os `CryptoAPI` Rótulos são da `ALG_ID` enumeração. Para obter mais informações sobre algoritmos de hash, consulte a `CryptoAPI` seção da Microsoft [!INCLUDE[winsdkshort](../../debugger/debug-interface-access/includes/winsdkshort_md.md)] .

 Para obter os bytes de soma de verificação reais para o arquivo de origem, chame o método [IDiaSourceFile:: get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md) .

## <a name="see-also"></a>Confira também
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)

---
title: 'Idiasourcefile:: Get_checksumtype | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksumType method
ms.assetid: 4c363e61-a6a9-409a-9cc0-d06eb2bee645
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 374528b1e48077ba7cd4c1bc25a5cb6d1e87c661
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51724824"
---
# <a name="idiasourcefilegetchecksumtype"></a>IDiaSourceFile::get_checksumType
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Recupera o tipo de soma de verificação.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT get_checksumType (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pRetVal`  
 [out] Retorna o tipo de soma de verificação.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 O tipo de soma de verificação é um valor que pode ser mapeado para um algoritmo de soma de verificação. Por exemplo, o formato de arquivo PDB padrão normalmente pode ter um dos seguintes valores:  
  
|Tipo de soma de verificação|Rótulo de CryptoAPI|Descrição|  
|-------------------|---------------------|-----------------|  
|0|\<Nenhum >|Soma de verificação não presente.|  
|1|`CALG_MD5`|soma de verificação gerada com o algoritmo de hash MD5.|  
|2|`CALG_SHA1`|soma de verificação gerada com o algoritmo de hash SHA1.|  
  
 O `CryptoAPI` rótulos são do `ALG_ID` enumeração. Para obter mais informações sobre algoritmos de hash, consulte o `CryptoAPI` seção do Microsoft [!INCLUDE[winsdkshort](../../includes/winsdkshort-md.md)].  
  
 Para obter os bytes da soma de verificação atual para o arquivo de origem, chame o [idiasourcefile:: Get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)




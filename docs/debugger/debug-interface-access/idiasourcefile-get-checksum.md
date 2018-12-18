---
title: 'Idiasourcefile:: Get_checksum | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksum method
ms.assetid: aad63a7e-4e22-44e4-8a5b-81b5174ced1e
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3f0484fce6f5355361c0c5156cd3c7ad827775c2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49919423"
---
# <a name="idiasourcefilegetchecksum"></a>IDiaSourceFile::get_checksum
Recupera os bytes da soma de verificação.  
  
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
 [in] Tamanho do buffer de dados, em bytes.  
  
 `pcbData`  
 [out] Retorna o número de bytes da soma de verificação. O parâmetro não pode ser `NULL`.  
  
 `data`  
 [no, out] Um buffer é preenchido com os bytes de soma de verificação. Se esse parâmetro for `NULL`, em seguida, `pcbData` retorna o número de bytes necessários.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Para determinar o tipo de algoritmo de soma de verificação que foi usado para gerar os bytes da soma de verificação, chame o [idiasourcefile:: Get_checksumtype](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md) método.  
  
 A soma de verificação normalmente é gerada da imagem do arquivo de origem para que as alterações no arquivo de origem são refletidas em alterações nos bytes de soma de verificação. Se os bytes da soma de verificação não coincidem com uma soma de verificação gerada da imagem carregada do arquivo, em seguida, o arquivo deve ser considerado danificado ou violado.  
  
 As somas de verificação típicas nunca são mais de 32 bytes de tamanho, mas não supõem que seja o tamanho máximo de uma soma de verificação. Defina as `data` parâmetro para `NULL` para obter o número de bytes necessários para recuperar a soma de verificação. Em seguida, aloque um buffer de tamanho apropriado e chamar esse método mais uma vez com o novo buffer.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaSourceFile::get_checksumType](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md)
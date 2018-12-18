---
title: 'Idiaimagedata:: Get_imagebase | Microsoft Docs'
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
- IDiaImageData::get_imageBase method
ms.assetid: 4ba3d9e4-b205-4ee6-a41d-6996972f1f85
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e09fb71294631f95b0d1d39ac6137c2e49b5bdea
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51801297"
---
# <a name="idiaimagedatagetimagebase"></a>IDiaImageData::get_imageBase
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Recupera o local da memória onde a imagem deve ser baseada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT get_imageBase (   
   ULONGLONG* pRetVal  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pRetVal`  
 [out] Retorna o valor de base de imagem sugerida.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Devido a conflitos de base de imagem, uma imagem pode ser base alterada automaticamente para um local de memória não utilizada quando ele for carregado. Esse método retorna a dica de base (local de memória sugerido) que foi armazenada no módulo em tempo de compilação.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)




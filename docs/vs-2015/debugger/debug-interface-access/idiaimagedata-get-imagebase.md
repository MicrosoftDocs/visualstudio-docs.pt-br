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
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fd514011e81e0881012fa5aa6a19570bd76fb9d2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49908897"
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




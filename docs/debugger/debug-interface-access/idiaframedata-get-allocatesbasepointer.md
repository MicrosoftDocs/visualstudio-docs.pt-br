---
title: 'Idiaframedata:: Get_allocatesbasepointer | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_allocatesBasePointer method
ms.assetid: 8a33db5d-008c-4fe5-b64f-210c9b77f686
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e981a29352c5adf192a0eb3cdccd59a088e29db6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49875236"
---
# <a name="idiaframedatagetallocatesbasepointer"></a>IDiaFrameData::get_allocatesBasePointer
Recupera um sinalizador que indica se o ponteiro de base está alocado para o código nesse intervalo de endereço. Esse método é preterido.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT get_allocatesBasePointer (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pRetVal`  
 [out] Retorna `TRUE` se um ponteiro de base é alocado; caso contrário, retornará `FALSE`.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade deve ser usada somente pelo código que anteriormente acessados FPO_DATA ou quando a cadeia de caracteres do programa é retornada pelo [idiaframedata:: Get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md) método é `NULL`. Caso contrário, a cadeia de caracteres do programa contém todas as informações necessárias para computar os valores de registro anterior.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)   
 [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)
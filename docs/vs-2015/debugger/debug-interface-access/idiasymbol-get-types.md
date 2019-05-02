---
title: IDiaSymbol::get_types | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_types method
ms.assetid: 5f056e0c-e15b-4e00-8f78-aadc8574f7ea
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 813dcd692669d823548e52ce6bb7eccc9546de61
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431783"
---
# <a name="idiasymbolgettypes"></a>IDiaSymbol::get_types
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Recupera uma matriz de tipos específicos do compilador para esse símbolo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT get_types (   
   DWORD       cTypes,  
   DWORD*      pcTypes,  
   IDiaSymbol* types[]  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `cTypes`  
 [in] Tamanho do buffer para manter os dados.  
  
 `pcTypes`  
 [out] Retorna o número de tipos escritos, ou, se o `types` parâmetro é `NULL`, em seguida, o número total de tipos disponíveis.  
  
 `types[]`  
 [out] Uma matriz que deve ser preenchido com o [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) objetos que representam todos os tipos para esse símbolo.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna `S_FALSE` ou um código de erro.  
  
> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

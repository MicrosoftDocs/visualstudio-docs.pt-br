---
title: 'Idiasession:: Symsareequiv | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symsAreEquiv method
ms.assetid: 9941d520-e203-46c0-83c3-b3a967f4fc59
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bdaa1ab070b6d95af0f28f5bdaa005b9ac808766
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49850978"
---
# <a name="idiasessionsymsareequiv"></a>IDiaSession::symsAreEquiv
Verifica se dois símbolos são equivalentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT symsAreEquiv (   
   IDiaSymbol* symbolA,  
   IDiaSymbol* symbolB  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `symbolA`  
 [in] A primeira [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) usado na comparação de objeto.  
  
 `symbolB`  
 [in] O segundo `IDiaSymbol` usado na comparação de objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Se os símbolos são equivalentes, retornará `S_OK`; caso contrário, retorna `S_FALSE`, os símbolos não são equivalentes. Caso contrário, retorna um código de erro.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
---
title: IDiaEnumInjectedSources::get__NewEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumInjectedSources::get__NewEnum method
ms.assetid: f56cdcdb-dc71-43c7-82fe-e2500986f5bc
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 408c0038fa302a8ccdaf2066a996262e03882c73
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53902887"
---
# <a name="idiaenuminjectedsourcesgetnewenum"></a>IDiaEnumInjectedSources::get__NewEnum
Recupera o <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> versão este enumerador.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT get__NewEnum (   
   IUnknown** pRetVal  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pRetVal  
 [out, retval] Retorna o `IUnknown` interface que representa o <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> versão este enumerador.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
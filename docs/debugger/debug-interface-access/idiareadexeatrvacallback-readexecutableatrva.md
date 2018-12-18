---
title: 'Idiareadexeatrvacallback:: Readexecutableatrva | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtRVACallback::ReadExecutableAtRVA method
ms.assetid: 3c1e965f-8f05-41a8-86d8-01830b2377c9
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 69afacf68c77dcb2bca7c951dbd2a1ee9a344cfb
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49917267"
---
# <a name="idiareadexeatrvacallbackreadexecutableatrva"></a>IDiaReadExeAtRVACallback::ReadExecutableAtRVA
Lê o número especificado de bytes começando no especificado endereço virtual relativo (RVA) do arquivo executável.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT ReadExecutableAtRVA (   
   DWORD  relativeVirtualAddress,  
   DWORD  cbData,  
   DWORD* pcbData,  
   BYTE   data[]  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `relativeVirtualAddress`  
 [in] O RVA no arquivo executável para iniciar a leitura.  
  
 `cbData`  
 [in] Número de bytes a serem lidos.  
  
 `pcbData`  
 [out] Retorna o número de bytes lidos.  
  
 `data[]`  
 [no, out] Uma matriz que é preenchida com bytes lidos do arquivo.  
  
## <a name="remarks"></a>Comentários  
 Este método é chamado pelo código de suporte do DIA para carregar os bytes de dados de um executável usando um endereço virtual relativo. Esse método é chamado suportados a [idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)   
 [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
---
title: IDiaSymbol::get_acceleratorPointerTags | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 30e13cee-e511-49ec-affd-99b0097071b2
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 24db7164335a8deffbac7cb4f62207a974f6efb9
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31460665"
---
# <a name="idiasymbolgetacceleratorpointertags"></a>IDiaSymbol::get_acceleratorPointerTags
Retorna todos os valores de marca de ponteiro de aceleração que correspondem a uma função de stub do C++ AMP acelerador.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT get_acceleratorPointerTags(   
   DWORD          cnt,  
   DWORD*         pcnt,  
   DWORD*         pPointerTags);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `cnt`  
 [in] O tamanho da matriz de saída `pPointerTags`.  
  
 `pcnt`  
 [out] A contagem de marcas de ponteiro de acelerador na função de stub do acelerador de C++ AMP.  
  
 `pPointerTags`  
 [out] Um `DWORD` ponteiro de matriz que é preenchido com os valores de marca de ponteiro de acelerador na função de stub do acelerador de C++ AMP.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retorna `S_OK`; caso contrário, retorna `S_FALSE` ou um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Esse método é chamado em um `IDiaSymbol` interface que corresponde a uma função de stub do C++ AMP acelerador.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
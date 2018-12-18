---
title: 'Idiastackframe:: Get_rawlvarinstancevalue | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_rawLVarInstanceValue method
ms.assetid: ce526259-85a6-475b-9274-0b3a21d95db2
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7f5e34b766e27693326aba34b7b7259042870f00
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49933489"
---
# <a name="idiastackframegetrawlvarinstancevalue"></a>IDiaStackFrame::get_rawLVarInstanceValue
Esse método recupera o valor da variável local especificada como bytes brutos.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT get_rawLVarInstanceValue(  
   IDiaLVarInstance* pInstance,  
   DWORD             cbDataMax,  
   DWORD*            pcbData,  
   BYTE*             pbData  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pInstance`  
 [in] Um `IDiaLVarInstance` que representa uma instância de variável local para obter o valor do objeto.  
  
 `cbDataMax`  
 [in] Número máximo de bytes no buffer apontado por `pbData`. Isso pode ter um máximo de 8 bytes (`sizeof(ULONGLONG)`).  
  
 `pcbData`  
 [out] Retorna o número real de bytes armazenados no buffer.  
  
 `pbData`  
 [out] Um buffer a ser preenchida com dados. Esse não pode ser `NULL`.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
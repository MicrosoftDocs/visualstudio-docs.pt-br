---
title: IDiaStackWalkHelper::get_registerValue | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::get_registerValue method
ms.assetid: 46ac5eee-73a3-44a1-8635-6c58ba193cb6
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: af5f68aaf5b2caed50d28a1a53022a095d478e60
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49887911"
---
# <a name="idiastackwalkhelpergetregistervalue"></a>IDiaStackWalkHelper::get_registerValue
Recupera o valor de um registro.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT get_registerValue (   
   DWORD      index,  
   ULONGLONG* pRetVal  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `index`  
 [in] Um valor da [enumeração CV_HREG_e](../../debugger/debug-interface-access/cv-hreg-e.md) enumeração que especifica qual registrar para obter o valor.  
  
 `pRetVal`  
 [out] Retorna o valor atual do registro.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Apesar do tamanho do `pRetVal` parâmetro, uma implementação deve armazenar só o que o registro normalmente mantém. Por exemplo, um registro de 8 bits contém apenas o mais baixo 8 bits do valor fornecido. Esse valor de 8 bits é expandido para 64-bits quando retornado deste método.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)   
 [Enumeração CV_HREG_e](../../debugger/debug-interface-access/cv-hreg-e.md)
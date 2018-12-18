---
title: 'Método Ijsdebug: | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJSDebug.OpenVirtualProcess
apilocation:
- jscript9diag.dll
ms.assetid: 5612bf1b-a4e3-4eaf-ac5e-c2e1f147c395
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f5acb137337e46a6e84f7d68c9330a3ca847f2e5
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727356"
---
# <a name="ijsdebugopenvirtualprocess-method"></a>Método IJsDebug::OpenVirtualProcess
Método de fábrica usado para criar um novo objeto de processo virtual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
 HRESULT OpenVirtualProcess(  
   DWORD processId,  
   UINT64 runtimeJsBaseAddress,  
   IJsDebugDataTarget *pDataTarget,  
   IJsDebugProcess **ppProcess  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `processId`  
 [in] Id do processo para anexar o depurador.  
  
 `runtimeJsBaseAddress`  
 [in] O endereço base no qual o tempo de execução do JavaScript tem carregados no processo de destino.  
  
 `pDataTarget`  
 [in] Interface fornecida para consultar o estado do processo do depurador.  
  
 `ppProcess`  
 [out] Novo objeto de processo de depuração  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="remarks"></a>Comentários  
 Retorna E_JsDEBUG_MISMATCHED_RUNTIME se Jscript9diag e Jscript9 não coincidem.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebug](../../winscript/reference/ijsdebug-interface.md)
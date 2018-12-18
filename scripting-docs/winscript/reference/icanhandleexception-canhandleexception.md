---
title: ICanHandleException::CanHandleException | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ICanHandleException.CanHandleException
apilocation:
- scrobj.dll
helpviewer_keywords:
- ICanHandleException::CanHandleException
ms.assetid: 0fc703bf-9518-487e-af20-00e073b640f1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 15612330f160f694202bb2158f970e0633fe53bd
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725266"
---
# <a name="icanhandleexceptioncanhandleexception"></a>ICanHandleException::CanHandleException
Determina se o chamador do mecanismo de script pode manipular uma exceção especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT CanHandleException(  
   EXCEPINFO*  pExcepInfo,  
   VARIANT*    pvar  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pExcepInfo`  
 [in] Ponteiro para um `EXCEPINFO` estrutura que contém as informações que serão reportadas se nenhum manipulador de exceção é encontrada.  
  
 `pvar`  
 [in] Um valor associado com a exceção, como o valor gerada por um `throw` instrução. Esse parâmetro pode ser `NULL`.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O chamador pode lidar com a exceção|  
|`E_FAIL`|O chamador não pode lidar com a exceção.|  
  
## <a name="remarks"></a>Comentários  
 Se uma chamada para `IDispatchEx::InvokeEx`, ou um método similar, resulta em uma exceção, as verificações de mecanismo de script para um chamador na cadeia de chamador do script que ofereça suporte a `ICanHandleException` interface e indica que ele possa manipular a exceção. Se nenhum chamador pode lidar com a exceção, o mecanismo de script é interrompida.  
  
## <a name="see-also"></a>Consulte também  
 [Interface ICanHandleException](../../winscript/reference/icanhandleexception-interface.md)   
 [IDispatchEx::InvokeEx](../../winscript/reference/idispatchex-invokeex.md)
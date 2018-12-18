---
title: IApplicationDebugger::CreateInstanceAtDebugger | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IApplicationDebugger.CreateInstanceAtDebugger
apilocation:
- scrobj.dll
helpviewer_keywords:
- IApplicationDebugger::CreateInstanceAtDebugger
ms.assetid: 6763afac-c86a-4e88-9580-77108fb242fb
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f6495c2d8782d1128700bdfb6d4081b80ffae878
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725766"
---
# <a name="iapplicationdebuggercreateinstanceatdebugger"></a>IApplicationDebugger::CreateInstanceAtDebugger
Permite a criação de objetos no processo de depurador pelo código que é fora de processo para o depurador.  
  
> [!IMPORTANT]
>  Esse método não deve ser implementado, pois ela permite que o código não confiável criar objetos arbitrários em um thread do depurador confiável.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT CreateInstanceAtDebugger(  
   REFCLSID    rclsid,  
   IUnknown*   pUnkOuter,  
   DWORD       dwClsContext,  
   REFIID      riid,  
   IUnknown**  ppvObject  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `rclsid`  
 [in] Identificador de classe (CLSID) do objeto a ser criado.  
  
 `pUnkOuter`  
 [in] Se `NULL`, o objeto não está sendo criado como parte de uma agregação. Caso contrário, `pUnkOuter` é um ponteiro para o objeto de agregação `IUnknown` interface (o controlador `IUnknown`).  
  
 `dwClsContext`  
 [in] Contexto de execução do código executável. Os valores são obtidos a partir da enumeração `CLSCTX`.  
  
 `riid`  
 [in] O identificador da interface usado para se comunicar com o objeto.  
  
 `ppvObject`  
 [out] Endereço da variável de ponteiro que recebe o ponteiro de interface solicitado na `riid`. No retorno bem-sucedido, *`ppvObject` contém o ponteiro de interface solicitada. Em caso de falha, \* `ppvObject` contém `NULL`.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Este método delega para `CoCreateInstance`.  
  
 O método não está implementado atualmente.  
  
## <a name="see-also"></a>Consulte também  
 [IApplicationDebugger Interface](../../winscript/reference/iapplicationdebugger-interface.md)
---
title: IDispatchEx::GetMemberProperties | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetMemberProperties
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetMemberProperties method
ms.assetid: 20d43209-12e2-472a-9bf3-81eced137b71
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0d216bb7b21c8895337b9925007637c00d0deb37
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729656"
---
# <a name="idispatchexgetmemberproperties"></a>IDispatchEx::GetMemberProperties
Recupera as propriedades do membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetMemberProperties(  
   DISPID id,  
   DWORD grfdexFetch,  
   DWORD *pgrfdex  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `id`  
 Identifica o membro. Usa `GetDispID` ou `GetNextDispID` para obter o identificador de distribuição.  
  
 `grfdexFetch`  
 Determina quais propriedades para recuperar. Isso pode ser uma combinação dos valores listados na `pgrfdex` e/ou uma combinação dos seguintes valores:  
  
|Valor|Significado|  
|-----------|-------------|  
|grfdexPropCanAll|Combina fdexPropCanGet, fdexPropCanPut, fdexPropCanPutRef, fdexPropCanCall, fdexPropCanConstruct e fdexPropCanSourceEvents.|  
|grfdexPropCannotAll|Combina fdexPropCannotGet, fdexPropCannotPut, fdexPropCannotPutRef, fdexPropCannotCall, fdexPropCannotConstruct e fdexPropCannotSourceEvents.|  
|grfdexPropExtraAll|Combina fdexPropNoSideEffects e fdexPropDynamicType.|  
|grfdexPropAll|Combina grfdexPropCanAll, grfdexPropCannotAll e grfdexPropExtraAll.|  
  
 `pgrfdex`  
 Endereço de um `DWORD` que recebe as propriedades solicitadas. Isso pode ser uma combinação dos seguintes valores:  
  
|Valor|Significado|  
|-----------|-------------|  
|fdexPropCanGet|O membro pode ser obtido usando DISPATCH_PROPERTYGET.|  
|fdexPropCannotGet|O membro não pode ser obtido usando DISPATCH_PROPERTYGET.|  
|fdexPropCanPut|O membro pode ser definido usando DISPATCH_PROPERTYPUT.|  
|fdexPropCannotPut|O membro não pode ser definido usando DISPATCH_PROPERTYPUT.|  
|fdexPropCanPutRef|O membro pode ser definido usando DISPATCH_PROPERTYPUTREF.|  
|fdexPropCannotPutRef|O membro não pode ser definido usando DISPATCH_PROPERTYPUTREF.|  
|fdexPropNoSideEffects|O membro não tem efeitos colaterais. Por exemplo, um depurador foi com segurança get/set/chamada esse membro sem alterar o estado do script que está sendo depurado.|  
|fdexPropDynamicType|O membro é dinâmico e pode ser alterado durante o tempo de vida do objeto.|  
|fdexPropCanCall|O membro pode ser chamado como um método usando DISPATCH_METHOD.|  
|fdexPropCannotCall|O membro não pode ser chamado como um método usando DISPATCH_METHOD.|  
|fdexPropCanConstruct|O membro pode ser chamado como um construtor usando DISPATCH_CONSTRUCT.|  
|fdexPropCannotConstruct|O membro não pode ser chamado como um construtor usando DISPATCH_CONSTRUCT.|  
|fdexPropCanSourceEvents|O membro pode disparar os eventos.|  
|fdexPropCannotSourceEvents|O membro não pode disparar os eventos.|  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|||  
|-|-|  
|`S_OK`|Êxito.|  
|`DISP_E_UNKNOWNNAME`|O nome não era conhecido.|  
  
## <a name="example"></a>Exemplo  
  
```  
BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;   
   DWORD dwProps;  
  
   // Assign to pdex and bstrName  
   if (SUCCEEDED(pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid)) &&  
      SUCCEEDED(pdex->GetMemberProperties(dispid, grfdexPropAll, &dwProps)) &&  
         (dwProps & fdexPropCanPut))  
   {  
      // Assign to member  
   }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDispatchEx](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx::GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)
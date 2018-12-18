---
title: IDispatchEx::GetNextDispID | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetNextDispID
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetNextDispID method
ms.assetid: 8263d441-85ee-47f4-bdba-fbf2ad07e85f
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ece7bde3230da370c8434cef7f780a92604df34c
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728516"
---
# <a name="idispatchexgetnextdispid"></a>IDispatchEx::GetNextDispID
Enumera os membros do objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetNextDispID(  
   DWORD grfdex,  
   DISPID id,  
   DISPID *pid  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `grfdex`  
 Determina qual conjunto de itens a serem enumerados. Isso pode ser uma combinação dos seguintes valores:  
  
|Valor|Significado|  
|-----------|-------------|  
|fdexEnumDefault|Solicita que o objeto enumera os elementos do padrão. O objeto é permitido para enumerar um conjunto de elementos.|  
|fdexEnumAll|Solicita que o objeto enumera todos os elementos. O objeto é permitido para enumerar um conjunto de elementos.|  
  
 `id`  
 Identifica o membro atual. GetNextDispID recupera o item na enumeração depois deste. Usa GetDispID ou uma chamada anterior a GetNextDispID para obter esse identificador. Usa o valor DISPID_STARTENUM para obter o identificador da primeira do primeiro item.  
  
 `pid`  
 Endereço de uma variável DISPID que recebe o identificador do próximo item na enumeração.  
  
 Se um membro for excluído por `DeleteMemberByName` ou `DeleteMemberByDispID`, o `DISPID` deve permanecer válido para `GetNextDispID`.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|||  
|-|-|  
|`S_OK`|Êxito.|  
|`S_FALSE`|Enumeração é feita.|  
  
## <a name="example"></a>Exemplo  
  
```  
HRESULT hr;  
   BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;  
  
   // Assign to pdex  
   hr = pdex->GetNextDispID(fdexEnumAll, DISPID_STARTENUM, &dispid);  
   while (hr == NOERROR)  
   {  
      hr = pdex->GetMemberName(dispid, &bstrName);  
      if (!wcscmp(bstrName, OLESTR("Bar")))  
      {  
         SysFreeString(bstrName);  
         return TRUE;  
      }  
      SysFreeString(bstrName);  
      hr = pdex->GetNextDispID(fdexEnumAll, dispid, &dispid);  
   }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDispatchEx](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx::GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](#lrfidispatchexgetnextdispid)   
 [IDispatchEx::DeleteMemberByName](../../winscript/reference/idispatchex-deletememberbyname.md)   
 [IDispatchEx::DeleteMemberByDispID](../../winscript/reference/idispatchex-deletememberbydispid.md)
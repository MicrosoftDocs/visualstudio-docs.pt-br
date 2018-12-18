---
title: IDispatchEx::GetDispID | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetDispID
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetDispID method
ms.assetid: a288d63d-b08a-4540-9d9d-0bcd182eff9a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 93595cd2d0f88244866ab7363ecd68c6d8073b48
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729046"
---
# <a name="idispatchexgetdispid"></a>IDispatchEx::GetDispID
Mapeia um nome de membro único para seu DISPID correspondente, que pode ser usada em chamadas subsequentes para `IDispatchEx::InvokeEx`.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
 HRESULT GetDispID(  
   BSTR bstrName,  
   DWORD grfdex,  
   DISPID *pid  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `bstrName`  
 Passado no nome a ser mapeada.  
  
 `grfdex`  
 Determina as opções para obter o identificador de membro. Isso pode ser uma combinação dos seguintes valores:  
  
|Valor|Significado|  
|-----------|-------------|  
|fdexNameCaseSensitive|Solicitações que a pesquisa de nome ser feita de maneira diferencia maiusculas de minúsculas. Pode ser ignorado por objeto que não oferece suporte a pesquisa diferencia maiusculas de minúsculas.|  
|fdexNameEnsure|Solicita que o membro criado se ele ainda não existir. O novo membro deve ser criado com o valor `VT_EMPTY`.|  
|fdexNameImplicit|Indica que o chamador está procurando objetos por um membro de um nome específico quando o objeto base não for especificado explicitamente.|  
|fdexNameCaseInsensitive|Solicitações que a pesquisa de nome ser feita de maneira maiusculas de minúsculas. Pode ser ignorado por objeto que não oferece suporte a pesquisa diferencia maiusculas de minúsculas.|  
  
 `pid`  
 Ponteiro para o local alocada pelo chamador para receber resultados DISPID. Se ocorrer um erro, `pid` contém DISPID_UNKNOWN.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|||  
|-|-|  
|`S_OK`|Êxito.|  
|`E_OUTOFMEMORY`|Sem memória.|  
|`DISP_E_UNKNOWNNAME`|O nome não era conhecido.|  
  
## <a name="remarks"></a>Comentários  
 `GetDispID`pode ser usado em vez de `GetIDsOfNames` para obter o DISPID para um determinado membro.  
  
 Porque `IDispatchEx` permite a adição e exclusão de membros, o conjunto de DISPIDs não permanecer constante para o tempo de vida de um objeto.  
  
 Não usada `riid` parâmetro `IDispatch::GetIDsOfNames` foi removido.  
  
## <a name="example"></a>Exemplo  
  
```  
BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;   
  
   // Assign to pdex and bstrName  
   pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid);  
   // Use dispid  
```  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDispatchEx](../../winscript/reference/idispatchex-interface.md)
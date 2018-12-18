---
title: IDispatchEx::DeleteMemberByName | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.DeleteMemberByName
apilocation:
- scrobj.dll
helpviewer_keywords:
- DeleteMemberByName method
ms.assetid: a01b4e6a-d989-4b29-bb3f-04554f8c39f7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5cb9a9dfd979954c42101fde41819d7e12db59e1
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728126"
---
# <a name="idispatchexdeletememberbyname"></a>IDispatchEx::DeleteMemberByName
Exclui um membro por nome.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT DeleteMemberByName(  
   BSTR bstrName,  
   DWORD grfdex  
  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `bstrName`  
 Nome do membro a ser excluído.  
  
 `grfdex`  
 Determina se o nome do membro diferencia maiusculas de minúsculas. Isso pode ser um dos seguintes valores:  
  
|Valor|Significado|  
|-----------|-------------|  
|fdexNameCaseSensitive|Solicitações que a pesquisa de nome ser feita de maneira diferencia maiusculas de minúsculas. Pode ser ignorado pelo objeto que não oferece suporte a pesquisa diferencia maiusculas de minúsculas.|  
|fdexNameCaseInsensitive|Solicitações que a pesquisa de nome ser feita de maneira maiusculas de minúsculas. Pode ser ignorado pelo objeto que não oferece suporte a pesquisa diferencia maiusculas de minúsculas.|  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|||  
|-|-|  
|`S_OK`|Êxito.|  
|`S_FALSE`|Membro existe, mas não pode ser excluído.|  
  
## <a name="remarks"></a>Comentários  
 Se o membro for excluído, o DISPID deve permanecer válido para `GetNextDispID`.  
  
 Se um membro com um nome fornecido será excluído e posteriormente um membro com o mesmo nome é recriado, o DISPID deve ser o mesmo. (Se os membros que diferenciam somente maiusculas e minúsculas são "mesmo" depende do objeto.)  
  
## <a name="example"></a>Exemplo  
  
```  
BSTR bstrName;  
IDispatchEx *pdex;  
  
// Assign to pdex and bstrName  
pdex->DeleteMemberByName(bstrName, fdexNameCaseSensitive);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDispatchEx](../../winscript/reference/idispatchex-interface.md)
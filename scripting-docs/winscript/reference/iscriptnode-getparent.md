---
title: IScriptNode::GetParent | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.GetParent
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::GetParent
ms.assetid: 0fb813f6-ab94-46b2-b0cf-ef5d1cd38ae4
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1da2f68de40a66b98b97ab7c7eb1d63748f1e07a
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24733636"
---
# <a name="iscriptnodegetparent"></a>IScriptNode::GetParent
Retorna o `IScriptNode` objeto que é o pai de um objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetParent(  
   IScriptNode       **ppsnParent  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppsnParent`  
 [out] O endereço de uma variável que recebe um ponteiro para o `IScriptNode` interface da instância pai.  
  
 Se a classe implementa `IScriptEntry` ou `IScriptScriptlet`, uma `IScriptNode` objeto é retornado.  
  
 Se a classe implementa `IScriptNode` (representando uma página da Web), NULL será retornado.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [IScriptNode Interface](../../winscript/reference/iscriptnode-interface.md)
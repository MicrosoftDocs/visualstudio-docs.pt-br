---
title: 'IScriptNode:: GetLanguage | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.GetLanguage
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::GetLanguage
ms.assetid: 089715fd-6746-474e-94ed-2e57ee4bc0da
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 26fd5db22346292585be3cea751eaa8be1c284a9
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575690"
---
# <a name="iscriptnodegetlanguage"></a>IScriptNode::GetLanguage
Retorna a linguagem de script usada pelo nó de script atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetLanguage(  
   BSTR               *pbstr  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pbstr`  
 fora Retorna "JScript" se o nó do script usar JScript ou "VBScript" se o nó do script usar Visual Basic Scripting Edition (VBScript).  
  
## <a name="return-value"></a>Valor retornado  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [IScriptNode Interface](../../winscript/reference/iscriptnode-interface.md)
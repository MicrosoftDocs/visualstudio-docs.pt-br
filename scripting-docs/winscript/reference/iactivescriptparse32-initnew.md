---
title: 'IActiveScriptParse32:: InitNew | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 7c77aa16-f391-4c93-9f1a-4e529a9930b2
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 887e4ce44662cc591fee64f5e0549edcdcbc14af
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835700"
---
# <a name="iactivescriptparse32initnew"></a>IActiveScriptParse32::InitNew
Inicializa o mecanismo de script.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT InitNew(void);  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna `S_OK` se for bem-sucedido ou `E_FAIL` se ocorrer um erro durante a inicialização.  
  
## <a name="remarks"></a>Comentários  
 Antes que o mecanismo de script possa ser usado, um dos seguintes métodos deve ser chamado: `IPersist*::Load` , `IPersist*::InitNew` ou `IActiveScriptParse32::InitNew` . A semântica desse método é idêntica a, pois `IPersistStreamInit::InitNew` esse método diz ao mecanismo de script para se inicializar. Observe que não é válido chamar `IPersist*::InitNew` or `IActiveScriptParse32::InitNew` e `IPersist*::Load` , nem é válido chamar `IPersist*::InitNew` , `IActiveScriptParse32::InitNew` ou `IPersist*::Load` mais de uma vez.  
  
## <a name="see-also"></a>Confira também  
 [IActiveScriptParse32](../../winscript/reference/iactivescriptparse32.md)
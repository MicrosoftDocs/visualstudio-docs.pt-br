---
title: IActiveScriptParse32::InitNew | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7c77aa16-f391-4c93-9f1a-4e529a9930b2
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 31de8258ae13855741c6dd5ca9e4ff2c589e97bf
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645786"
---
# <a name="iactivescriptparse32initnew"></a>IActiveScriptParse32::InitNew
Inicializa o mecanismo de script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT InitNew(void);  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna `S_OK` se for bem-sucedido, ou `E_FAIL` se ocorreu um erro durante a inicialização.  
  
## <a name="remarks"></a>Comentários  
 Antes do mecanismo de script pode ser usado, um dos métodos a seguir deve ser chamado: `IPersist*::Load`, `IPersist*::InitNew`, ou `IActiveScriptParse32::InitNew`. A semântica desse método é idêntica aos `IPersistStreamInit::InitNew`, em que esse método informa ao mecanismo de script para se inicializar. Observe que não é válido chamar `IPersist*::InitNew` ou `IActiveScriptParse32::InitNew` e `IPersist*::Load`, não é válido chamar `IPersist*::InitNew`, `IActiveScriptParse32::InitNew`, ou `IPersist*::Load` mais de uma vez.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptParse32](../../winscript/reference/iactivescriptparse32.md)
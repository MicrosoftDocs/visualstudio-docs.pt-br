---
title: IActiveScriptParse::InitNew | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptParse.InitNew
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptParse_InitNew
ms.assetid: 3a582bd6-fc0d-43a5-812f-5ea55a8517a1
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e34094bcc25c0316fa670f570d8b2664acc0ba78
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724476"
---
# <a name="iactivescriptparseinitnew"></a>IActiveScriptParse::InitNew
Inicializa o mecanismo de script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT InitNew(void);  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna `S_OK` se for bem-sucedido, ou `E_FAIL` se ocorreu um erro durante a inicialização.  
  
## <a name="remarks"></a>Comentários  
 Antes do mecanismo de script pode ser usado, um dos métodos a seguir deve ser chamado: `IPersist*::Load`, `IPersist*::InitNew`, ou `IActiveScriptParse::InitNew`. A semântica desse método é idêntica aos `IPersistStreamInit::InitNew`, em que esse método informa ao mecanismo de script para se inicializar. Observe que não é válido chamar `IPersist*::InitNew` ou `IActiveScriptParse::InitNew` e `IPersist*::Load`, não é válido chamar `IPersist*::InitNew`, `IActiveScriptParse::InitNew`, ou `IPersist*::Load` mais de uma vez.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptParse](../../winscript/reference/iactivescriptparse.md)
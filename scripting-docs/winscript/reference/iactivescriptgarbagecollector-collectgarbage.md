---
title: IActiveScriptGarbageCollector::CollectGarbage | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 75f77c49-2190-4d49-a3e0-9dcf847c502b
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 478a7a39c69e0c2106e3c6cc308f44f8f7aa3201
ms.sourcegitcommit: 116e9614867e0b3c627ce9001012a4c39435a42b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54097117"
---
# <a name="iactivescriptgarbagecollectorcollectgarbage"></a>IActiveScriptGarbageCollector::CollectGarbage
O host de Script ativo chama esse método para iniciar a coleta de lixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT CollectGarbage(        SCRIPTGCTYPE scriptgctype    );  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `scriptgctype`  
 [in] O [enumeração SCRIPTGCTYPE](../../winscript/reference/scriptgctype-enumeration.md) que especifica se deve fazer a coleta de lixo completa ou normal.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um HRESULT.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptGarbageCollector Interface](../../winscript/reference/iactivescriptgarbagecollector-interface.md)
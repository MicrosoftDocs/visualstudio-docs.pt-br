---
title: IDiaLoadCallback2::RestrictReferencePathAccess | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictReferencePathAccess method
ms.assetid: e20cb45c-0360-4ff0-a92c-b1b6f76d6e85
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ce0f2b896b60a13635818249e9faf552f3070828
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187305"
---
# <a name="idialoadcallback2restrictreferencepathaccess"></a>IDiaLoadCallback2::RestrictReferencePathAccess
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Determina se é permitido procurar um arquivo. pdb no caminho em que o arquivo. exe está localizado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT RestrictReferencePathAccess();  
```  
  
## <a name="return-value"></a>Valor retornado  
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Qualquer código de retorno diferente de `S_OK` para evitar a procura de um arquivo. pdb no caminho em que o arquivo. exe está localizado.  
  
## <a name="see-also"></a>Consulte Também  
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)

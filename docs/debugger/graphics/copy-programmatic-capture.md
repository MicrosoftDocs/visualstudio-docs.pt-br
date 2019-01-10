---
title: Copiar (Captura programática) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 30ec235a-0abb-44b9-8852-61bc9e67ce22
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: aab2b18c8c349211f4b5bd26b055d6ee5b65f0c6
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53990942"
---
# <a name="copy-programmatic-capture"></a>Copiar (captura programática)
Copia o conteúdo do arquivo de log (. vsglog) de elementos gráficos ativos em um novo arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
void Copy(  
  wchar_t const * szNewVSGLog  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `szNewVSGLog`  
 O nome do arquivo do novo arquivo de log de gráficos.  
  
## <a name="remarks"></a>Comentários  
 Para copiar as informações de gráficos para um novo arquivo, você deve já capturou algumas informações de gráficos; Caso contrário, nada acontece.
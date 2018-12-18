---
title: 'VsgDbg:: ~ VsgDbg (destruidor) | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7a3b97fb-d344-4df7-b195-9347d1edfcf7
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ca62daa70602ac48e2b0871f764d0572b9da5f73
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31471594"
---
# <a name="vsgdbgvsgdbg-destructor"></a>VsgDbg::~VsgDbg (Destruidor)
Destrói a uma instância do `VsgDbg` classe. Se as informações de gráficos ativamente está sendo registradas, o arquivo de log do gráfico é finalizado e fechado, e os recursos que foram usados durante a captura ativamente informações de gráficos são liberados.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
~VsgDbg();  
```  
  
## <a name="see-also"></a>Consulte também  
 [VsgDbg::VsgDbg (Construtor)](vsgdbg-vsgdbg-constructor.md)
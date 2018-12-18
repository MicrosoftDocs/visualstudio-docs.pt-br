---
title: 'VsgDbg:: ~ VsgDbg (destruidor) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7a3b97fb-d344-4df7-b195-9347d1edfcf7
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 60dbd0a82bf5fc648982a7ab4a1d71854cfb27bd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51806718"
---
# <a name="vsgdbgvsgdbg-destructor"></a>VsgDbg::~VsgDbg (Destruidor)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Destrói uma instância da `VsgDbg` classe. Se informações de gráficos ativamente está sendo registradas, o arquivo de log de gráficos é finalizado e fechado, e os recursos que foram usados durante a captura ativamente informações gráficas são liberados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
~VsgDbg();  
```  
  
## <a name="see-also"></a>Consulte também  
 [VsgDbg::VsgDbg (Construtor)](../debugger/vsgdbg-vsgdbg-constructor.md)




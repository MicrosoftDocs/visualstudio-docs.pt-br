---
title: Restrições em comprimentos de cadeia de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- source control plug-ins, restrictions on string lengths
ms.assetid: 877173d2-ca27-43b3-b1f4-8379f7c5e268
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: ef31cd75fe6221667026bc7af8f9da1e6ac5e4ec
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51790509"
---
# <a name="restrictions-on-string-lengths"></a>Restrições de comprimentos de cadeia de caracteres
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A API de plug-in de controle do código-fonte limita os comprimentos das cadeias de caracteres usadas em várias funções.  
  
## <a name="string-length-values"></a>Valores de comprimento de cadeia de caracteres  
  
|Constante|Valor|  
|--------------|-----------|  
|`SCC_NAME_LEN`|31|  
|`SCC_AUXLABEL_LEN`|31|  
|`SCC_USER_LEN`|31|  
|`SCC_PRJPATH_LEN`|300|  
  
> [!NOTE]
>  Tamanho não inclui a terminação `null`. Outras constantes com um sufixo tamanho"em vez de"_LEN"incluir espaço para a terminação `null`.  
  
|Constante|Valor|  
|--------------|-----------|  
|SCC_NAME_SIZE|32|  
|SCC_AUXLABEL_SIZE|32|  
|SCC_USER_SIZE|32|  
|SCC_PRJPATH_SIZE|301|  
  
## <a name="see-also"></a>Consulte também  
 [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)


---
title: Diretiva CleanUpBehavior T4 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9e5a211f-a3bf-4229-bff0-7d2e45b71c64
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: ee1882b6b63dbb2729070d32fcee7c1e58d280c5
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49263389"
---
# <a name="t4-cleanupbehavior-directive"></a>Diretiva CleanUpBehavior T4
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para excluir o appDomain depois de processar um modelo de texto, inclua a seguinte linha:  
  
```  
<#@ CleanupBehavior processor="T4VSHost" CleanupAfterProcessingtemplate="true" #>  
```  
  
 Os modelos de texto são processados em um appDomain que é separado do processo do host. Na maioria dos casos, quando um modelo de texto é processado, o appdomain é usado novamente para processar o próximo modelo. Mas se você especificar CleanupBehavior, o appDomain será excluído e o próximo modelo será processado em um novo appDomain.  
  
 Isso reduz o processamento de texto, mas pode ser útil para garantir que os recursos sejam descartados.  
  
 Essa diretiva só funciona no host do Visual Studio.




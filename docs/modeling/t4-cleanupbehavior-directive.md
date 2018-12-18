---
title: Diretiva CleanUpBehavior T4
ms.date: 11/04/2016
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 44d1dc61b1330b344b333b62c30308fdb65494d1
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31946033"
---
# <a name="t4-cleanupbehavior-directive"></a>Diretiva CleanUpBehavior T4

Para excluir o appDomain depois de processar um modelo de texto, inclua a seguinte linha:

```
<#@ CleanupBehavior processor="T4VSHost" CleanupAfterProcessingtemplate="true" #>
```

Os modelos de texto são processados em um appDomain que é separado do processo do host. Na maioria dos casos, quando um modelo de texto é processado, o appdomain é usado novamente para processar o próximo modelo. Mas se você especificar CleanupBehavior, o appDomain será excluído e o próximo modelo será processado em um novo appDomain.

Isso reduz o processamento de texto, mas pode ser útil para garantir que os recursos sejam descartados.

Essa diretiva só funciona no host do Visual Studio.
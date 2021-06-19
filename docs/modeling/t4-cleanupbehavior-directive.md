---
title: Diretiva CleanUpBehavior T4
description: Saiba mais sobre a diretiva CleanUpBehavior e como excluir o appDomain depois de processar um modelo de texto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 078b688c238bea47e4ab38b3302708bf5e5189cf
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386339"
---
# <a name="t4-cleanupbehavior-directive"></a>Diretiva CleanUpBehavior T4

Para excluir o appDomain depois de processar um modelo de texto, inclua a seguinte linha:

```
<#@ CleanupBehavior processor="T4VSHost" CleanupAfterProcessingtemplate="true" #>
```

Os modelos de texto são processados em um appDomain que é separado do processo do host. Na maioria dos casos, quando um modelo de texto é processado, o appdomain é usado novamente para processar o próximo modelo. Mas se você especificar CleanupBehavior, o appDomain será excluído e o próximo modelo será processado em um novo appDomain.

Isso reduz o processamento de texto, mas pode ser útil para garantir que os recursos sejam descartados.

Essa diretiva só funciona no host do Visual Studio.

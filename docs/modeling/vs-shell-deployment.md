---
title: Implantação do VS Shell
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d8793312e0ed022fc7210508efdf20a81b293f0f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535844"
---
# <a name="vs-shell-deployment"></a>Implantação do VS Shell

Um shell isolado permite que você determine qual funcionalidade do Visual Studio você precisa para interagir com sua linguagem específica de domínio e como essa solução deve ser exibida. Para obter mais informações sobre o Shell isolado do Visual Studio, consulte [Personalizando o Shell isolado](https://docs.microsoft.com/visualstudio/extensibility/customizing-the-isolated-shell).

Para definir um shell do Visual Studio como o destino de implantação:

1. No projeto **DslPackage** , abra **Source.Extension.tt**.

2. Em `<SupportedProducts>` Inserir:

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   Substitua *MyIsolatedShell* pelo nome do seu pacote de shell isolado.

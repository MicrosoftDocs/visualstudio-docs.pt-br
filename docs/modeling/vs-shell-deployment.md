---
title: Implantação do VS Shell
description: Saiba como um shell isolado permite determinar qual Visual Studio que você precisa para interagir com sua DSL e como essa solução deve aparecer.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 946cbf99fa7836fa8d7ec5aa1d921e7cda93bf46
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388302"
---
# <a name="vs-shell-deployment"></a>Implantação do VS Shell

Um shell isolado permite determinar qual Visual Studio que você precisa para interagir com seu idioma específico do domínio e como essa solução deve aparecer. Para obter mais informações sobre Visual Studio shell isolado, consulte [Personalização do Shell Isolado.](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

Para definir um shell Visual Studio como o destino de implantação:

1. No projeto **DslPackage,** abra **source.extension.tt**.

2. Em `<SupportedProducts>` Inserir:

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   Substitua *MyIsolatedShell* pelo nome do seu pacote de shell isolado.
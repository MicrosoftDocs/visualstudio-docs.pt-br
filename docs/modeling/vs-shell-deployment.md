---
title: Implantação do VS Shell
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 61cf6e716f082abf28043d56d1a8803853d894aa
ms.sourcegitcommit: ef828606e9758c7a42a2f0f777c57b2d39041ac3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39566667"
---
# <a name="vs-shell-deployment"></a>Implantação do VS Shell

Um shell isolado permite que você determine quais Visual Studio funcionalidade que você precisa interagir com sua linguagem específica do domínio e como essa solução deve ser exibidos. Para obter mais informações sobre o shell isolado do Visual Studio, consulte [personalizar o Shell isolado](../extensibility/customizing-the-isolated-shell.md).

## <a name="to-set-a-visual-studio-shell-as-the-deployment-target"></a>Para definir um Shell do Visual Studio como o destino de implantação

1.  No **DslPackage** projeto, abra **source.extension.tt**.

2.  Sob `<SupportedProducts>` inserir:

    ```xml
    <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
    ```

     Substitua *MyIsolatedShell* com o nome do seu pacote de shell isolado.
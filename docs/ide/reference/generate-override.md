---
title: Gerar uma substituição de método no Visual Studio
ms.date: 01/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 5d51139d2e5197607de2255b267c24bf2a9db2b3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49919059"
---
# <a name="generate-an-override-in-visual-studio"></a>Gerar uma substituição no Visual Studio

Esta geração de código aplica-se a:

- C#

- Visual Basic

**O quê:** permite gerar imediatamente o código para qualquer método que possa ser substituído de uma classe base.

**Quando:** você quer substituir um método de classe base e gerar a assinatura automaticamente.

**Por quê:** você mesmo poderia escrever a assinatura do método, no entanto, esse recurso gerará automaticamente a assinatura.

## <a name="how-to"></a>Como fazer

1. Digite `override` em C# ou `Overrides` em Visual Basic, seguido por um espaço, em que você deseja inserir um método de substituição.

   - C#:

      ![Substituição do IntelliSense em C#](media/override-intellisense-cs.png)

   - Visual Basic:

      ![Substituição do IntelliSense em VB](media/override-intellisense-vb.png)

2. Selecione o método que você deseja substituir da classe base.

   > [!TIP]
   > - Use o ícone de propriedade ![Ícone de propriedade](media/override-property-cs.png) para mostrar ou ocultar propriedades na lista.
   > - Use o ícone de método ![Ícone de método](media/override-method-cs.png) para mostrar ou ocultar métodos na lista.

   A propriedade ou o método selecionado será adicionado à classe como uma substituição, pronta para ser implementada.

   - C#:

       ![Resultado da substituição em C#](media/override-result-cs.png)

   - Visual Basic:

       ![Resultado da substituição em VB](media/override-result-vb.png)

## <a name="see-also"></a>Consulte também

- [Geração de código](../code-generation-in-visual-studio.md)
---
title: Solucionar problemas de extensões para diagramas de dependência
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- dependency diagrams, extension errors
- dependency diagrams, troubleshooting extensions
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 8acde589ebf47d4a67609e847a84bd7c7acd8482
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49899637"
---
# <a name="troubleshoot-extensions-for-dependency-diagrams"></a>Solucionar problemas de extensões para diagramas de dependência

Este tópico aborda alguns problemas que você pode encontrar ao criar extensões do modelo de camada.

## <a name="when-i-press-f5-to-debug-my-extension-my-commands-gesture-handlers-validation-extensions-or-custom-properties-do-not-appear-on-dependency-diagrams-in-the-experimental-instance-of-visual-studio"></a>Quando eu pressiono F5 para depurar minha extensão, Meus comandos, manipuladores de gestos, extensões de validação ou propriedades personalizadas não aparecem em diagramas de dependência na instância Experimental do Visual Studio

1. Abra a solução de extensão na instância Experimental do Visual Studio e nos **Build** menu, clique em **recompilar solução**.

2. Pressione **F5** ou **CTRL + F5** para iniciar a instância experimental do Visual Studio. Abra um diagrama de dependência e testar sua extensão.

   Continue com o próximo procedimento, se necessário.

## <a name="an-old-version-of-my-extension-runs"></a>Uma versão antiga da minha extensão é executado.

1. Certifique-se de que nenhuma instância experimental do Visual Studio está em execução.

2. Exclua a seguinte pasta: %LocalAppData%\Microsoft\VisualStudio\\\ComponentModelCache [versão]

   > [!NOTE]
   > % LocalAppData % é normalmente *DriveName*: \Users\\*UserName*\appdata\local.

   Continue com o próximo procedimento, se necessário.

## <a name="an-old-version-of-my-validation-results-appears-or-my-validation-method-is-not-called"></a>Uma versão antiga do meus resultados de validação é exibido ou meu método de validação não é chamado.

1.  Na instância experimental do Visual Studio, sobre o **construir** menu, clique em **limpar solução**. Isso limpa os resultados em cache de análise de validação anterior.

2.  Certifique-se de que as camadas no seu modelo estão associadas a elementos de código, e se há pelo menos um link de dependência no modelo. Validação não é invocada se não há nada para validar.

3.  Pontos de interrupção regulares podem não funcionar em um método de validação, pois ele é executado em um processo separado. Você deve inserir uma chamada a `System.Diagnostics.Debugger.Launch()` se você quiser depurar seu método.

4.  Na **vsixmanifest** em seu projeto de validação de camada, certifique-se de que você tenha adicionado ambos um **componente MEF** item e uma **tipo personalizado de extensão** item sob **Conteúdo**.

## <a name="see-also"></a>Consulte também

- [Estender diagramas de dependência](../modeling/extend-layer-diagrams.md)

---
title: Solucionar problemas de extensões para diagramas de camada | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- layer diagrams, extension errors
- layer diagrams, troubleshooting extensions
ms.assetid: 1fda4f8a-38b8-482b-87b8-eade1a4e5662
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 6361651672e72df6661f030a4b6c8e451fdaea89
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51738771"
---
# <a name="troubleshoot-extensions-for-layer-diagrams"></a>Solucionar problemas de extensões para diagramas de camada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico aborda alguns problemas que você pode encontrar ao criar extensões do modelo de camada.  
  
#### <a name="when-i-press-f5-to-debug-my-extension-my-commands-gesture-handlers-validation-extensions-or-custom-properties-do-not-appear-on-layer-diagrams-in-the-experimental-instance-of-includevsprvsincludesvsprvs-mdmd"></a>Quando eu pressiono F5 para depurar minha extensão, Meus comandos, manipuladores de gestos, extensões de validação ou propriedades personalizadas não aparecem em diagramas de camada na instância Experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]  
  
1. Abra a solução de extensão na instância Experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]e, na **construir** menu, clique em **recompilar solução**.  
  
2. Pressione **F5** ou **CTRL + F5** para iniciar a instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Abra um diagrama de camada e testar sua extensão.  
  
   Continue com o próximo procedimento, se necessário.  
  
#### <a name="an-old-version-of-my-extension-runs"></a>Uma versão antiga da minha extensão é executado.  
  
1. Certifique-se de que nenhuma instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] está em execução.  
  
2. Exclua a seguinte pasta: %LocalAppData%\Microsoft\VisualStudio\\\ComponentModelCache [versão]  
  
   > [!NOTE]
   >  % LocalAppData % é normalmente *DriveName*: \Users\\*UserName*\appdata\local.  
  
   Continue com o próximo procedimento, se necessário.  
  
#### <a name="an-old-version-of-my-validation-results-appears-or-my-validation-method-is-not-called"></a>Uma versão antiga do meus resultados de validação é exibido ou meu método de validação não é chamado.  
  
1.  Na instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]diante a **construir** menu, clique em **limpar solução**. Isso limpa os resultados em cache de análise de validação anterior.  
  
2.  Certifique-se de que as camadas no seu modelo estão associadas a elementos de código, e se há pelo menos um link de dependência no modelo. Validação não é invocada se não há nada para validar.  
  
3.  Pontos de interrupção regulares podem não funcionar em um método de validação, pois ele é executado em um processo separado. Você deve inserir uma chamada a `System.Diagnostics.Debugger.Launch()` se você quiser depurar seu método.  
  
4.  Na **vsixmanifest** em seu projeto de validação de camada, certifique-se de que você tenha adicionado ambos um **componente MEF** item e uma **tipo personalizado de extensão** item sob **Conteúdo**.  
  
## <a name="see-also"></a>Consulte também  
 [Estender diagramas de camada](../modeling/extend-layer-diagrams.md)




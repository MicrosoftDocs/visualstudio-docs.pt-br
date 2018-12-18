---
title: 'Como: habilitar e desabilitar análise de solução completa para código gerenciado | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full solution analysis
ms.assetid: 04315147-5792-47f0-8b5f-9ac8413c6a57
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: af0aae4020182f6414d44a2004f98a6fc0df23ca
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49221865"
---
# <a name="how-to-enable-and-disable-full-solution-analysis-for-managed-code"></a>Como: habilitar e desabilitar análise de solução completa para código gerenciado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

OBSERVAÇÃO]
>  Este tópico se aplica somente ao Visual Studio 2015 atualização 3 RC e posterior.  
  
 *Análise de solução completa* é um recurso do Visual Studio que permite que você escolha se você vê problemas de análise de código somente em arquivos abertos de Visual c# ou Visual Basic em sua solução, ou em arquivos abertos e fechados, do Visual c# ou Visual Basic em sua solução.  
  
 Embora seja útil ser capaz de ver todos os problemas em todos os arquivos, pode ser perturbador e até mesmo desacelerar os Visual Studio se sua solução for muito grande ou tem muitos arquivos.  Para limitar o número de problemas mostrados e melhorar o desempenho do Visual Studio, você pode desabilitar análise completa da solução. Você pode facilmente habilitar este recurso novamente se você quiser.  
  
#### <a name="to-toggle-full-solution-analysis"></a>Para ativar/desativar a análise de solução completa  
  
1.  No menu principal do Visual Studio, escolha **ferramentas** &#124; **opções** para exibir a **opções** caixa de diálogo.  
  
2.  No **opções** diálogo caixa, escolha **Editor de texto** &#124; **c#** ou **básica** &#124; **avançado**.  
  
3.  Selecione o **habilitar a análise de solução completa** caixa de seleção para habilitar a análise de solução completa, ou desmarque a caixa para desativá-lo. Escolha o **Okey** botão quando terminar.  
  
     ![Habilite a caixa de seleção de análise de solução completa. ](../code-quality/media/fsa-toolsoptions.png "FSA_ToolsOptions")  
  
## <a name="results-of-enabling-and-disabling-full-solution-analysis"></a>Resultados de habilitar e desabilitar análise de solução completa  
 Na seguinte captura de tela, você pode ver os resultados quando a análise de solução completa está habilitada. Todos os erros e problemas de análise de código em *todos os* dos arquivos na solução exibido, independentemente se os arquivos estão abertos ou não.  
  
 ![Análise completa da solução habilitada. ](../code-quality/media/fsa-enabled.png "FSA_Enabled")  
  
 Captura de tela a seguir mostra os resultados da mesma solução depois de desabilitar análise completa da solução. Somente os erros e problemas de análise de código em abrem solução arquivos aparecem na lista de erros.  
  
 ![Análise de solução completa desabilitado. ](../code-quality/media/fsa-disabled.png "FSA_Disabled")  
  
## <a name="automatically-disabling-full-solution-analysis"></a>Desabilitar automaticamente a análise de solução completa  
 Se o Visual Studio detectar que 200MB ou menos da memória do sistema está disponível para ele, ele automaticamente desabilita a análise de solução completa (bem como alguns outros recursos) se ele estiver habilitado. Se isso ocorrer, um alerta será exibida informando isso. Um botão permite que você habilite novamente a análise de solução completa para fazê-lo.  
  
 ![Suspendendo a análise de solução completa de texto de alerta](../code-quality/media/fsa-alert.png "FSA_Alert")  
  
## <a name="additional-details"></a>Detalhes adicionais  
 Por padrão, análise de solução completa é habilitado para o Visual Basic e desabilitada para o Visual c#.  
  
 Visual Studio Update 3 RC inclui um mecanismo de diagnóstico v2 de analisador de código aprimorada que reduz o uso de memória significativamente e diminui o tempo de CPU permanecer ocioso, mesmo se a análise de solução completa está habilitada.




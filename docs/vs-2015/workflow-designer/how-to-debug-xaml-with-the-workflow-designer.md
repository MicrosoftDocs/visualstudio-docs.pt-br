---
title: 'Como: depurar XAML com o Designer de fluxo de trabalho | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: d9305dbc-af62-4bdd-b03f-c54e3fe9ecc7
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 7ac99d5bcacb937db27867a1b02b2076fdce66c0
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49176031"
---
# <a name="how-to-debug-xaml-with-the-workflow-designer"></a>Como: Depuração XAML com designers de Fluxo de Trabalho
Fluxos de trabalho são definidos em termos de XAML. A representação de interface de usuário de fluxo de trabalho é construída sobre a árvore XAML que define o fluxo de trabalho. A experiência de depuração é semelhante a depuração fluxos de trabalho em [!INCLUDE[wfd1](../includes/wfd1-md.md)]. Por exemplo, ao depurar XAML, os locais, a observação, e o trabalho das janelas de segmentos da mesma maneira que faz sobre depuração de [!INCLUDE[wfd2](../includes/wfd2-md.md)] . Além disso, a exibição da pilha de chamadas durante a depuração XAML é uma exibição hierárquica linha com base de fluxo de execução do fluxo de trabalho.  
  
> [!NOTE]
>  Se o XAML para um fluxo de trabalho está localizado no mesmo assembly que as atividades, a parte do assembly de nomes de classe não é incluído. Sem esta parte dos nomes de classe (atividade), o XAML não pode ser carregado no tempo de execução. Não é recomendável definir atividades no mesmo namespace que o projeto pai; caso contrário, o XAML deverá mão- ser editado após ser editado no designer.  
  
### <a name="to-debug-workflow-xaml"></a>Para depurar o fluxo de trabalho XAML  
  
1.  Abrir um projeto de fluxo de trabalho ou de atividade em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
2.  Definir um ponto de interrupção na atividade ou atividades que você deseja depurar, conforme descrito em [como: definir pontos de interrupção em fluxos de trabalho](../workflow-designer/how-to-set-breakpoints-in-workflows.md).  
  
3.  Clique com botão direito no arquivo. XAML que contém a definição de fluxo de trabalho e selecione **Exibir código**. Você verá um ponto de interrupção exibido na mesma linha da declaração de elemento XAML de atividade que você definir o ponto de interrupção sobre no modo design.  
  
4.  Chamar o depurador, conforme descrito em [como: chamar o depurador de fluxo de trabalho](../workflow-designer/how-to-invoke-the-workflow-debugger.md).  
  
5.  Quando a execução de código atinge um de seus pontos de interrupção, o elemento XAML associado com esse ponto de interrupção será realçado. Para mover para o próximo ponto de interrupção, use o **F10** ou **F11** chave.  
  
## <a name="see-also"></a>Consulte também  
 [Como: definir pontos de interrupção em fluxos de trabalho](../workflow-designer/how-to-set-breakpoints-in-workflows.md)   
 [Como invocar o depurador de fluxo de trabalho](../workflow-designer/how-to-invoke-the-workflow-debugger.md)
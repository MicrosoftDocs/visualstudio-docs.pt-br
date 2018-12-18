---
title: 'Como: definir pontos de interrupção em fluxos de trabalho (herdado) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- breakpoints, setting in workflows
- debugging, setting breakpoints in workflows
- debugging workflows, setting breakpoints
- workflows, setting breakpoints
ms.assetid: 78e0be39-3e99-487c-bfef-19db0daf6f42
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 158592ccef331c541bf27494856cfa1314b21f88
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49252541"
---
# <a name="how-to-set-breakpoints-in-workflows-legacy"></a>Como: Definir pontos de interrupção em fluxos de trabalho (o legados)
Este tópico descreve como definir pontos de interrupção na construção de aplicativos de [!INCLUDE[wf](../includes/wf-md.md)] usando [!INCLUDE[wfd1](../includes/wfd1-md.md)]herdado. Use [!INCLUDE[wfd2](../includes/wfd2-md.md)] herdado quando seu aplicativo de [!INCLUDE[wf2](../includes/wf2-md.md)] precisa definir como alvo [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 Quando você usa [!INCLUDE[wfd2](../includes/wfd2-md.md)] herdado em [!INCLUDE[vs2010](../includes/vs2010-md.md)] para criar um aplicativo de [!INCLUDE[wf2](../includes/wf2-md.md)] , você pode definir pontos de interrupção em C# e em código Visual Basic como você faz no Visual Studio. Como esperado, a execução de fluxo de trabalho que ele pare em cada ponto de interrupção esse definido.  
  
 Um ponto de interrupção tem três estados: *pendente*, *associado*, e *erro*. Quando você definir um ponto de interrupção, ele está pendente, e ele é representado por um ícone oco vermelho. Quando o tempo de execução carregado o tipo de fluxo de trabalho, transformações e limite é representado por um ícone vermelho contínuo. Se você especificar um formato incorreto do ponto de interrupção, como um nome de atividade que não é válida, uma janela de erro aparece. O ponto de interrupção é adicionado ainda para a janela de ponto de interrupção, mas é marcado com um pequeno “x”.  
  
 Você pode definir pontos de interrupção em uma atividade na superfície de design de fluxo de trabalho das seguintes maneiras:  
  
-   A atividade com o botão direito e selecione **ponto de interrupção \ Inserir ponto de interrupção**.  
  
-   Selecione a atividade e pressione F9.  
  
-   Selecione **novo ponto de interrupção** da **depurar** menu.  
  
     Você também pode usar esta opção para definir um novo ponto de interrupção a depuração, quando o depurador para em um ponto de interrupção.  
  
    > [!NOTE]
    >  Os pontos de interrupção em fluxos de trabalho chamados não são suportados.  
  
### <a name="to-set-a-breakpoint-using-the-new-breakpoint-option-on-the-debug-menu"></a>Para definir um ponto de interrupção usando a nova opção de ponto de interrupção no menu debug  
  
1.  Sobre o **Debug** menu, selecione **novo ponto de interrupção**.  
  
2.  Clique em **interromper na função**.  
  
     O **novo ponto de interrupção** caixa de diálogo é aberta.  
  
3.  Especifique o nome de uma atividade na **função** caixa de texto usando esta sintaxe: `QualifiedActivityId[:[FullClassName][:InstanceId]]`.  
  
    > [!NOTE]
    >  Opcionalmente, em vez de usar o nome da atividade na **função** caixa de texto, você pode definir um ponto de interrupção, especificando o caminho absoluto da atividade de fluxo de trabalho. Por exemplo, suponha que você tiver uma solução de fluxo de trabalho chamada **WorkflowConsoleApplication1** e um fluxo de trabalho na solução chamada **Workflow1** que usa uma atividade chamada **Delay1**. Você pode usar o nome da atividade **Delay1** ou especifique o caminho como **delay1: workflowconsoleapplication1.workflow1** ou **delay1: workflowconsoleapplication1.workflow1: { 6614886A-608E-412B-BF98-99FF1559DDDF}**.  
  
4.  Selecione o **usar o IntelliSense** caixa de seleção para verificar o nome da função.  
  
     Se esta caixa de seleção não estiver selecionada, nenhuma verificação do nome do ponto de interrupção é executada.  
  
5.  Selecione **fluxo de trabalho** da **idioma** lista.  
  
6.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando fluxos de trabalho herdado](../workflow-designer/debugging-legacy-workflows.md)   
 [Invocando o depurador do Visual Studio para Windows Workflow Foundation (herdado)](../workflow-designer/invoking-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md)
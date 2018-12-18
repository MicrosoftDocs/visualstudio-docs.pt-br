---
title: Depurando fluxos de trabalho herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- workflows, debugging
- debugging, workflows
- debugging workflows
ms.assetid: e6097b47-760a-4b30-a92c-ae70cdbda49f
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 5d835ddc84fae24130035f0664d446a73b7ac3f4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49897700"
---
# <a name="debugging-legacy-workflows"></a>Depurando fluxos de trabalho herdados
Se você estiver usando [!INCLUDE[wfd1](../includes/wfd1-md.md)] herdado no [!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)] para compilar aplicativos [!INCLUDE[wf](../includes/wf-md.md)] destinados ao .NET Framework 3.0 ou 3.5, poderá depurar seus fluxos de trabalho como qualquer outro programa definindo pontos de interrupção, anexando a processos e examinando threads e a pilha de chamadas. Você também tem a opção de depurar remotamente.  
  
> [!NOTE]
>  Se várias versões do Visual Studio tiverem sido instaladas e desinstaladas no computador, a depuração do WF3 poderá falhar com uma das duas possibilidades a seguir:  
> 
> - Os pontos de interrupção não foram atingidos.  
>   -   A seguinte mensagem é exibida:  
> 
>   **Não é possível iniciar a depuração no servidor web. O depurador não está instalado corretamente.  Não é possível depurar o tipo de código solicitado.  Execute a instalação para instalar ou reparar o depurador.**  
> 
>   Se qualquer um desses cenários ocorrer durante a depuração de fluxos de trabalho do .NET Framework 3.0 ou 3.5, execute um reparo da instalação do Visual Studio.  
  
 O [!INCLUDE[wf2](../includes/wf2-md.md)] integra-se com as seguintes janelas de depuração padrão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]:  
  
- **Ponto de interrupção**: funciona conforme o esperado, mas você especifica uma atividade para o nome da função.  
  
- **Pilha de chamadas**: modificado para fornecer uma estrutura de tópicos das atividades que foram executadas em uma instância de fluxo de trabalho. As entradas na **pilha de chamadas** janela são uma pesquisa de profundidade da execução de atividades. Você pode clicar duas vezes em uma entrada para colocar o foco na atividade selecionada.  
  
- **Threads**: fornece a ID da instância do fluxo de trabalho que está sendo depurada.  
  
  O Visual Studio para Windows Foundation Workflow não oferece suporte aos seguintes recursos de depuração:  
  
- Pontos de interrupção condicionais na superfície do designer.  
  
- QuickWatch.  
  
- Definir próxima instrução.  
  
- Executar até o cursor.  
  
- Editar e continuar.  
  
- Depuração just-in-time.  
  
- Depuração de modo misto.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Invocando o depurador do Visual Studio para Windows Workflow Foundation (herdado)](../workflow-designer/invoking-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md)  
  
 [Desabilitando o depurador do Visual Studio para Windows Workflow Foundation (herdado)](../workflow-designer/disabling-the-visual-studio-debugger-for-windows-workflow-foundation-legacy.md)  
  
 [Como depurar fluxos de trabalho baseados em ASP.NET (herdado)](../workflow-designer/how-to-debug-aspnet-based-workflows-legacy.md)  
  
 [Como definir pontos de interrupção em fluxos de trabalho (herdado)](../workflow-designer/how-to-set-breakpoints-in-workflows-legacy.md)  
  
 [Depurando fluxos de trabalho de um computador remoto (herdado)](../workflow-designer/debugging-workflows-from-a-remote-computer-legacy.md)  
  
 [Opções de passo a passo em depuração (herdado)](../workflow-designer/debug-stepping-options-legacy.md)  
  
 [Como alterar a opção de executar a depuração em etapas (herdado)](../workflow-designer/how-to-change-the-debug-stepping-option-legacy.md)
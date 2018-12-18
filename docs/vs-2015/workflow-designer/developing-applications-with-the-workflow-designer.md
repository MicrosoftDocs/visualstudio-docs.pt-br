---
title: Desenvolvimento de aplicativos com o Designer de fluxo de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- DefaultWorkflowDesigner
- DefaultWorkflowDesigner.UI
helpviewer_keywords:
- Visual Studio 2010 Workflow Designer [WFD], overview
- Workflow Designer [WFD]
- Visual Studio 2010 Workflow Designer [WFD]
- Workflow Designer [WFD], overview
ms.assetid: 4cd062b1-b496-4668-bbc1-ee85545e066d
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 71cde900802543a21a20bc02e95bcfedc50d5541
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49259149"
---
# <a name="developing-applications-with-the-workflow-designer"></a>Desenvolvendo aplicativos com designers de Fluxo de Trabalho
[!INCLUDE[wfd1](../includes/wfd1-md.md)] é um designer e um depurador visuais para a compilação e gráficos a depuração de aplicativos de [!INCLUDE[wf](../includes/wf-md.md)] em [!INCLUDE[netfx40_long](../includes/netfx40-long-md.md)] que está hospedada no ambiente de desenvolvimento de [!INCLUDE[vs2010](../includes/vs2010-md.md)] . Permite que você escreve um aplicativo de fluxo de trabalho, uma biblioteca de atividade, ou um serviço composto de [!INCLUDE[indigo1](../includes/indigo1-md.md)] com o uso de modelos e os designers de atividade. [!INCLUDE[crabout](../includes/crabout-md.md)] fluxos de trabalho, consulte o [Windows Workflow Foundation &#91;.NET Framework 4&#93;](http://msdn.microsoft.com/library/9a23ea6b-d600-483e-89cd-8889cfec5f66).  
  
 Os seguintes são vários novos recursos de design esse conjunto essa nova versão de [!INCLUDE[wfd2](../includes/wfd2-md.md)] independentemente das versões anteriores de [!INCLUDE[wfd2](../includes/wfd2-md.md)]:  
  
-   [!INCLUDE[wfd2](../includes/wfd2-md.md)] é compilado usando [!INCLUDE[avalon1](../includes/avalon1-md.md)]. Isso melhora a experiência do designer de atividade e melhora o desempenho para grandes e fluxos de trabalho complexos.  
  
-   As atividades personalizados são criadas agora com [!INCLUDE[avalon2](../includes/avalon2-md.md)], usando XAML e o modelo de programação para criar designer de atividade foi simplificado.  
  
-   Uma atividade do fluxograma era implementado, então você pode visualizar o fluxo de programa usando o fluxograma familiar que modela o estilo.  
  
-   [!INCLUDE[wfd2](../includes/wfd2-md.md)] tem um novo designer variável que permite que você declare e defina o escopo variáveis em seus fluxos de trabalho, associando os às atividades.  
  
-   Em [!INCLUDE[vs2010](../includes/vs2010-md.md)], [!INCLUDE[wfd2](../includes/wfd2-md.md)] fornece recursos do IntelliSense para criar expressões do Visual Basic dentro dos fluxos de trabalho [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] .  
  
-   A experiência de depuração estende agora em XAML, permitindo que você defina pontos de interrupção na definição de fluxo de trabalho XAML e entrar no seu código XAML em tempo de execução, que fornece uma experiência semelhante ao código gerenciado.  
  
-   Rehosting [!INCLUDE[wfd2](../includes/wfd2-md.md)] fora de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é simplificado extremamente em comparação com versões anteriores, que requer agora apenas algumas linhas de código.  
  
-   O novo <xref:System.Activities.Statements.Flowchart> atividade e sua [fluxograma](../workflow-designer/flowchart-activity-designer.md) permitem que você visualize seu fluxo de programa usando o fluxograma familiar que modela o estilo.  
  
-   As atividades de mensagem foram aprimoradas, permitindo que você escreva (nenhum código declarativo completa) serviços de [!INCLUDE[indigo1](../includes/indigo1-md.md)] .  
  
-   O **adicionar referência de serviço...** funcionalidade permite que você gerencia as atividades automaticamente que acessam serviços da Web.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Usando o Designer de Fluxo de Trabalho](../workflow-designer/using-the-workflow-designer.md)  
 Mostra como criar novos atividades e fluxo de trabalho usando os projetos designer internos e como usar outras ferramentas fornecidas pelo designer para argumentos, a variáveis, para expressões, as importações, e a navegação de trilha de manipular.  
  
 [Usando os designers de atividade](../workflow-designer/using-the-activity-designers.md)  
 Descreve as categorias de atividades e modelos e seus designers que são sistema fornecidos.  
  
 [Fluxos de trabalho de depuração com o Designer de Fluxo de Trabalho](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)  
 Descreve como executar procedimentos de depuração bem como a depuração XAML e expressões tradicionais.  
  
 [Ajuda da interface do usuário do Designer de Fluxo de Trabalho](../workflow-designer/workflow-designer-ui-help.md)  
 Contém tópicos da ajuda contextual para as caixas de diálogo fornecidas por [!INCLUDE[wfd1](../includes/wfd1-md.md)], bem como orientação sobre recursos, em atalhos de teclado e de mensagens de erro do shell de designer.  
  
 [Desenvolvendo aplicativos de fluxo de trabalho destinados ao .NET 3.0 ou o .NET Framework 3.5](../workflow-designer/developing-workflow-applications-targeting-the-dotnet-3-0-or-dotnet-3-5-framework.md)  
 Contém a orientação sobre como usar o designer herdado que direciona [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 [O designer que ReHosting &#91;exemplos do WF&#93;](http://msdn.microsoft.com/library/b676ad31-5f64-4d84-9a36-b4d7113a2f4d)  
 Este exemplo mostra como criar o layout de WPF para conter o designer.  
  
 [Designers de atividade personalizada](http://msdn.microsoft.com/library/dcf14dca-ce6d-4278-96ba-062f0a679075)  
 Esta seção contém exemplos de atividade que usam designer personalizadas para exibição no designer de fluxo de trabalho.
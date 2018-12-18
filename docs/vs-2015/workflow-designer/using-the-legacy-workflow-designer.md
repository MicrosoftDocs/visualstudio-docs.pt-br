---
title: Usando o Designer de fluxo de trabalho herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Visual Studio 2005 Extensions for Windows Workflow Foundation, about
ms.assetid: 7af53077-afd7-465f-9c1d-b387e9d4f216
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 012be918b415d863d9f3b2c08fdd1e0636a5da5a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49306196"
---
# <a name="using-the-legacy-workflow-designer"></a>Usando Designer de Fluxo de Trabalho herdado
[!INCLUDE[wfd2](../includes/wfd2-md.md)] herdado fornecido por [!INCLUDE[vs2010](../includes/vs2010-md.md)] pode ser usado para direcionar [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 Ela é acessada selecionando à **.NET Framework 3.0** opção ou o **.NET Framework 3.5** opção na lista suspensa na parte superior da lista da **novo projeto** janela. A opção padrão na [!INCLUDE[vs2010](../includes/vs2010-md.md)] está **.NET Framework 4** que é usado para criar [!INCLUDE[wf](../includes/wf-md.md)] aplicativos que se destinam a [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)].  
  
 [!INCLUDE[wfd2](../includes/wfd2-md.md)] fornece uma maneira de criar aplicativos graficamente de [!INCLUDE[wf](../includes/wf-md.md)] usando a interface do usuário e de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] . aplicativos de[!INCLUDE[wf](../includes/wf-md.md)] são compostos das etapas do processo de fluxo de trabalho chamadas atividades. Para criar um fluxo de trabalho, compor atividades na superfície de design arrastando seus respectivos Designer de atividade de **caixa de ferramentas** na superfície de design.  
  
 A tabela a seguir lista os principais recursos de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para Windows Workflow Foundation.  
  
|Recurso|Descrição|  
|-------------|-----------------|  
|Arrastar e soltar de atividades|Arraste atividades do **caixa de ferramentas** para a superfície de design para criar um fluxo de trabalho.|  
|Pesquisador de Propriedades|O padrão **propriedades** janela no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é usado para configurar as propriedades de uma atividade.|  
|Aplicar Zoom|O botão de binóculos **nível de Zoom** ícone está localizado abaixo da barra de rolagem vertical no lado direito da superfície de design. Clique nos binóculos e selecione uma porcentagem de zoom para fazer com que o elemento gráfico de fluxo de trabalho ampliar ou reduzir fora. Você também pode usar o **panorâmica** opções de cursor de lupa ícone para ampliar e reduzir.|  
|Panorâmica|O **panorâmica** ícone, um círculo que contém quatro setas cruzadas apontando em quatro direções, está localizado abaixo da barra de rolagem vertical no lado direito da superfície de design logo abaixo do ícone de zoom de binóculos. Se você clicar no ícone de bandeja, oferece de um menu pop-up as seguintes opções de cursor:<br /><br /> -A **ampliar** cursor de lupa permite que você ampliar clicando na superfície de design.<br />-A **zoom** cursor de lupa permite que você se clicando na superfície de design.<br />-A **ferramenta de navegação** cursor de mão permite que você agarrar "e" deslocar a exibição de um fluxo de trabalho na superfície de design.<br />-A **padrão** cursor de seta permite que você alterne dos outros cursores volta para o cursor de seta padrão.|  
|Rolagem automático|Se você tiver um grande fluxo de trabalho, convém colocar uma atividade além de exibição da área visível de superfície de design. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] permite que você arraste uma atividade para a borda da superfície de design mais próximo a onde você deseja colocar a atividade. A superfície de design de exibição os rola automaticamente naquela direção.|  
|Marcas inteligentes|As atividades que não são configuradas completamente ou não são configuradas não válida são marcadas com um ícone de ponto de exclamação. Você pode clicar no ícone e ver uma lista suspensa das necessidades de configuração que existem na atividade. Você pode usar o **propriedades** janela para configurar corretamente a atividade. Quando todas as propriedades são válidos para atividades, o ícone de ponto de exclamação desaparece.|  
  
## <a name="in-this-section"></a>Nesta seção  
 [Janelas de fluxo de trabalho do Visual Studio (herdado)](../workflow-designer/visual-studio-workflow-windows-legacy.md)  
  
 [Criando projetos herdados de fluxo de trabalho](../workflow-designer/creating-legacy-workflow-projects.md)  
  
 [Exibições de fluxo de trabalho sequencial (herdado)](../workflow-designer/sequential-workflow-views-legacy.md)  
  
 [Atividades de fluxo de trabalho herdadas](../workflow-designer/legacy-workflow-activities.md)  
  
 [Usando temas em fluxos de trabalho (herdado)](../workflow-designer/using-themes-in-workflows-legacy.md)  
  
 [Usando o Designer de Fluxo de Trabalho da máquina de estado herdado](../workflow-designer/using-the-legacy-state-machine-workflow-designer.md)  
  
 [Usando o designer de atividade herdado](../workflow-designer/using-the-legacy-activity-designer.md)  
  
 [Designer herdado para a ajuda da interface do usuário do Windows Workflow Foundation](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo fluxos de trabalho](http://go.microsoft.com/fwlink?LinkID=65010)
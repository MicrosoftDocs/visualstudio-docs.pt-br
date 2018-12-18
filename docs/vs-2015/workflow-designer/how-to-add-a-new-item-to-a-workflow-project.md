---
title: 'Como: adicionar um novo Item a um projeto de fluxo de trabalho | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: f9dd186c4f9b319b5c4c60fa48d3a32e16c673f3
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49210932"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>Como: Adicionar um novo item em um fluxo de trabalho Projeto
Depois de criar um projeto de fluxo de trabalho, você pode adicionar atividades de fluxo de trabalho, designer, e outros itens de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] familiares ao seu projeto.  
  
 A tabela a seguir lista os itens de [!INCLUDE[wf](../includes/wf-md.md)] que você pode adicionar a um projeto de fluxo de trabalho.  
  
|Nome|Descrição|  
|----------|-----------------|  
|Atividade|Uma atividade a ser composta de outras atividades. Selecionando o item adiciona o mesmo arquivo XAML ao projeto como você obteria quando selecionando o **biblioteca de atividades** modelo para um novo projeto. [!INCLUDE[crabout](../includes/crabout-md.md)] Neste procedimento, consulte [como: criar uma biblioteca de atividade](../workflow-designer/how-to-create-an-activity-library.md).|  
|Designer de Activity|Um designer para personalizar a experiência em tempo de design de uma atividade. Selecionando o item adiciona os mesmos arquivos para o projeto como você obteria quando selecionando o **biblioteca do Designer de atividade** modelo para um novo projeto. [!INCLUDE[crabout](../includes/crabout-md.md)] Neste procedimento, consulte [como: criar uma biblioteca do Designer de atividade](../workflow-designer/how-to-create-an-activity-designer-library.md).|  
|Atividade do código|Uma atividade com a lógica de execução gravar no código. Um arquivo de código-fonte com uma substituição do método de <xref:System.Activities.CodeActivity.Execute%2A> é gerado para você.|  
|WCF Serviço de Fluxo de Trabalho|Um serviço de [!INCLUDE[indigo2](../includes/indigo2-md.md)] compilado usando atividades de fluxo de trabalho. Selecionando o item adiciona os mesmos arquivos para o projeto como você obteria quando selecionando o **aplicativo de serviço de fluxo de trabalho WCF** modelo para um novo projeto. [!INCLUDE[crabout](../includes/crabout-md.md)] Neste procedimento, consulte [como: criar um aplicativo de serviço de fluxo de trabalho WCF](../workflow-designer/how-to-create-a-wcf-workflow-service-application.md).|  
  
### <a name="to-add-a-new-item-to-a-workflow-project"></a>Para adicionar um novo item em um fluxo de trabalho projeto  
  
1.  Sobre o **Project** menu, clique em **Adicionar Novo Item...** .  
  
     O **adicionar um novo Item** caixa de diálogo é aberta.  
  
2.  No **modelos instalados** painel, selecione **fluxo de trabalho** grupo.  
  
3.  Selecione um dos quatro itens. A tabela anterior lista as seleções disponíveis.  
  
4.  Digite um nome apropriado para o item na **nome** caixa na parte inferior da caixa de diálogo.  
  
5.  Clique em **adicionar** para adicionar o item ao projeto de fluxo de trabalho atual.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um projeto de fluxo de trabalho](../workflow-designer/creating-a-workflow-project.md)
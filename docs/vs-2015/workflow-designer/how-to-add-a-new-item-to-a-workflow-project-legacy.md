---
title: 'Como: adicionar um novo Item a um projeto de fluxo de trabalho (herdado) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sequential workflows, adding to workflow projects
- workflows, adding new items
- state machine workflows, adding to workflow projects
- activities, adding to workflow projects
ms.assetid: 130cd83d-942d-437b-bbb5-8088ec0a6d79
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 26be9519a4f9ee496ea36a61debffec7f96ffbe5
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49301152"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project-legacy"></a>Como: Adicionar um novo item em um fluxo de trabalho Project (o legados)
Depois de criar um projeto de fluxo de trabalho usando [!INCLUDE[wfd1](../includes/wfd1-md.md)] herdado fornecido por [!INCLUDE[vs2010](../includes/vs2010-md.md)] que tem como alvo [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)], você pode adicionar itens de [!INCLUDE[wf](../includes/wf-md.md)] e outros itens de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] familiares ao seu projeto.  
  
 A tabela a seguir lista os itens de [!INCLUDE[wf2](../includes/wf2-md.md)] que você pode adicionar a um projeto de fluxo de trabalho.  
  
|Item|Descrição|  
|----------|-----------------|  
|Atividade|Uma atividade com a definição de atividade em um código de arquivo e de usuário do designer de código em um código separado arquivos.|  
|Atividade (com separação de código)|Uma definição de atividade expressa como a marcação de fluxo de trabalho e o código do usuário em um arquivo separado código.|  
|Fluxo de trabalho sequencial (código)|Um trabalho sequenciais com a definição de trabalho em um código de arquivo e de usuário do designer de código em um arquivo separado código.|  
|Fluxo de trabalho sequencial (com separação de código)|Um trabalho sequenciais com a definição de trabalho expressa como a marcação de fluxo de trabalho e o código do usuário em um arquivo separado código.|  
|Fluxo de trabalho do computador de estado (código)|Um trabalho do computador de estado com a definição de trabalho em um código de arquivo e de usuário do designer de código em um arquivo separado código.|  
|Fluxo de trabalho do computador de estado (com separação de código)|Um trabalho do computador de estado com a definição de trabalho expressa como a marcação de fluxo de trabalho e o código do usuário em um arquivo separado código.|  
  
### <a name="to-add-a-new-item-to-a-workflow-project"></a>Para adicionar um novo item em um fluxo de trabalho projeto  
  
1.  Sobre o **Project** menu, clique em **adicionar um novo Item**.  
  
     O **adicionar um novo Item** caixa de diálogo é aberta.  
  
2.  Selecione um item.  
  
     A tabela anterior lista opções disponíveis do Windows Workflow Foundation.  
  
3.  Clique em **adicionar** para adicionar o item ao projeto de fluxo de trabalho.  
  
## <a name="see-also"></a>Consulte também  
 [Criando projetos herdados de fluxo de trabalho](../workflow-designer/creating-legacy-workflow-projects.md)
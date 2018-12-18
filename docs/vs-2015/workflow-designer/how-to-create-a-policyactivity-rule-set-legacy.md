---
title: 'Como: criar um conjunto de regras de PolicyActivity (herdado) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- PolicyActivity activity, creating rule sets
- Rule Set Editor dialog box
- PolicyActivity activity, selecting rule sets
- Select Rule Set dialog box
- rule sets, creating for PolicyActivity
ms.assetid: f272489d-3342-4511-8b59-6a0fd7a42d70
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 7ab49957d830bf558a9dddf55cdc5e8c2f3f75d2
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49194617"
---
# <a name="how-to-create-a-policyactivity-rule-set-legacy"></a>Como: Criar uma regra de PolicyActivity definida (o legados)
Este tópico descreve como criar um conjunto de regras de atividade de política usando o novas [!INCLUDE[wfd1](../includes/wfd1-md.md)] que direciona [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 Após você ter arrastado um **diretiva** item de atividade da **caixa de ferramentas** à superfície de design de fluxo de trabalho, você desejará selecione uma regra existente ou crie uma nova regra definida para o [PolicyActivity ](http://go.microsoft.com/fwlink?LinkID=65019) atividade. Você seleciona uma regra existente definida usando o [regra definir caixa de diálogo Selecionar (herdado)](../workflow-designer/select-rule-set-dialog-box-legacy.md) e criar conjuntos de regras usando o [regra de Editor de caixa de diálogo conjunto (herdado)](../workflow-designer/rule-set-editor-dialog-box-legacy.md).  
  
> [!NOTE]
>  Você pode abrir o [regra de Editor de caixa de diálogo conjunto (herdado)](../workflow-designer/rule-set-editor-dialog-box-legacy.md) caixa de diálogo diretamente clicando duas vezes em um [PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019) atividade que está na superfície de design de fluxo de trabalho.  
  
### <a name="to-select-or-create-a-rule-set-for-a-policyactivity-activity"></a>Para selecionar ou criar uma regra definida para uma atividade de PolicyActivity  
  
1.  Clique com botão direito do [PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019)e, em seguida, clique em **propriedades** para abrir o **propriedades** janela.  
  
2.  Clique o **RuleSetReference** propriedade.  
  
3.  Realize um dos seguintes procedimentos:  
  
    -   Clique o **RuleSetReference** elipses **[...]** e, em seguida, selecione uma regra existente definida de [selecione Definir caixa de diálogo regra (herdado)](../workflow-designer/select-rule-set-dialog-box-legacy.md). Então vá para a etapa 10.  
  
         -ou-  
  
    -   Digite um nome para um conjunto de regras. Clique o **RuleSetReference** elipses **[...]** e, em seguida, selecione **edite** no [selecione Definir caixa de diálogo regra (herdado)](../workflow-designer/select-rule-set-dialog-box-legacy.md).  
  
         -ou-  
  
    -   Digite um nome para um conjunto de regras. Expanda o **RuleSetReference** propriedade e selecione as reticências **[...]**  no **definição de conjunto de regras** propriedade.  
  
         O [regra de Editor de caixa de diálogo conjunto (herdado)](../workflow-designer/rule-set-editor-dialog-box-legacy.md) é aberta.  
  
4.  No [regra de Editor de caixa de diálogo conjunto (herdado)](../workflow-designer/rule-set-editor-dialog-box-legacy.md), clique em **Adicionar regra** para adicionar uma nova regra para o conjunto de regras.  
  
5.  Insira o **nome**, **prioridade**, e **reavaliação** propriedades, ou mantenha os valores padrão.  
  
6.  Digite o texto para o **condição**.  
  
7.  Digite o texto para o **ações Then** e o **ações Else**.  
  
8.  Clique em **Adicionar regra** novamente para adicionar outra regra.  
  
9. Ao terminar, clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019)   
 [Caixa de diálogo Definir selecione regra (herdado)](../workflow-designer/select-rule-set-dialog-box-legacy.md)   
 [(Herdado) caixa de diálogo Editor de conjunto de regras](../workflow-designer/rule-set-editor-dialog-box-legacy.md)   
 [Usando a atividade de política](http://go.microsoft.com/fwlink?LinkID=65004)   
 [Atividades de fluxo de trabalho herdadas](../workflow-designer/legacy-workflow-activities.md)
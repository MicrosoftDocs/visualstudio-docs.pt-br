---
title: Associar a uma atividade&#39;caixa de diálogo de propriedade s (herdado) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Workflow.ComponentModel.Design.ActivityBindForm.UI
helpviewer_keywords:
- Bind to an Activity's Property dialog box
ms.assetid: 19ebb207-e0a9-4642-8f5f-a5e31395c683
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: bbc9c36bec7c01e7a7e771e7f7145da40b84b177
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49211010"
---
# <a name="bind-to-an-activity39s-property-dialog-box-legacy"></a>Associar a uma atividade&#39;caixa de diálogo de propriedade s (herdado)
Este tópico descreve como usar o **associar a propriedade de uma atividade** caixa de diálogo em novas [!INCLUDE[wfd1](../includes/wfd1-md.md)]. Use [!INCLUDE[wfd2](../includes/wfd2-md.md)] herdado quando você precisa definir como alvo [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 Um tipo de instância de propriedade de dependência pode ser associado a propriedade pública ou ao evento de outra atividade. Para obter mais informações sobre associação de atividades, consulte [usando as propriedades de dependência](http://go.microsoft.com/fwlink?LinkID=65007).  
  
 Você seleciona uma propriedade para associar a usar o **associar a propriedade de uma atividade** caixa de diálogo. Abra essa caixa de diálogo clicando nas reticências **[...]**  no final da caixa de texto da propriedade selecionada na **propriedades** janela, ou clicando no ícone de exclamação azul que aparece ao lado do nome da propriedade no navegador de propriedade.  
  
 A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **associar a propriedade de uma atividade** caixa de diálogo.  
  
|Elemento da Interface do Usuário|Descrição|  
|----------------|-----------------|  
|**Associar a um membro existente**|Selecione um membro que você deseja associar no painel modo de exibição de árvore. O painel abaixo de exibição de árvore exibe uma mensagem que indica se o membro é um tipo válido para associar a ou não. Clique em **Okey** para associar ao membro selecionado válido.|  
|**Associar a um novo membro**|Crie um novo campo ou propriedade de membro para associação. Insira um **nome do novo membro**. Escolha se deseja criar uma propriedade de dependência ou um campo público selecionando **criar campo** ou **criar propriedade**. Clique em **Okey** para criar o novo membro.|  
  
## <a name="see-also"></a>Consulte também  
 [Usando propriedades de atividade](http://go.microsoft.com/fwlink?LinkID=65013)   
 [Usando propriedades de dependência](http://go.microsoft.com/fwlink?LinkID=65007)   
 [Designer herdado para a ajuda da interface do usuário do Windows Workflow Foundation](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)
---
title: Designer de atividade de interoperabilidade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Interop.UI
ms.assetid: 800a3403-ba86-41c4-8de1-c4fee9703eb1
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 587f9017e7f2c76018fbb5eb98645f5e4c19216c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49283017"
---
# <a name="interop-activity-designer"></a>Designer de atividade de Interoperabilidade
O **Interop** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.Interop> atividade.  
  
## <a name="the-interop-activity"></a>A atividade de Interoperabilidade  
 A atividade de <xref:System.Activities.Statements.Interop> gerencia a execução de tipos que derivam de <xref:System.Workflow.ComponentModel.Activity?displayProperty=fullName> em um fluxo de trabalho.  
  
### <a name="using-the-interop-activity-designer"></a>Usando o designer de atividade de Interoperabilidade  
 O **Interop** designer de atividade pode ser encontrado na **migração** categoria da **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**guia (como alternativa, selecione **caixa de ferramentas** do **exibição** menu ou CTRL + ALT + X.)  
  
 O [migração](../workflow-designer/migration-activity-designers.md) categoria que contém o <xref:System.Activities.Statements.Interop> atividade aparece apenas no **caixa de ferramentas** se seu projeto está direcionando o completo [!INCLUDE[netfx40_long](../includes/netfx40-long-md.md)].  
  
 Para projetos c#, você pode redirecionar o projeto para usar toda a [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] clicando com o projeto na **Gerenciador de soluções** e selecionando **propriedades**. Sobre o **aplicativo** guia, selecione o **NET Framework 4** opção no **estrutura de destino**. Selecione o **Yes** botão na **modificação do Framework de destino** caixa de diálogo que exibe solicitar que você confirme essa alteração.  
  
 Para projetos do VB, você pode redirecionar o projeto para usar toda a [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] clicando com o projeto na **Gerenciador de soluções** e selecionando **propriedades**. Sobre o **Compile** , clique no **opções avançadas de compilação** botão. Selecione **.Net Framework 4** da **lista do framework de destino** e, em seguida, clique em **Okey**. Clique o **Sim** botão na **modificação do Framework de destino** caixa de diálogo que exibe solicitar que você confirme essa alteração.  
  
 O **Interop** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma <xref:System.Activities.Statements.Interop> atividade com um padrão **DisplayName** de interoperabilidade. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **interoperabilidade** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.  
  
 Clique o **clique para procurar...** texto na **ActivityType** caixa, no **interoperabilidade** atividade do designer ou na grade de propriedade para abrir o **procurar e selecione um .net tipo** caixa de diálogo. Somente tipos para os trabalhos 3,0 ou o trabalho 3,5 atividades são mostrados (isto é, somente os tipos derivados de <xref:System.Workflow.ComponentModel.Activity>). [!INCLUDE[crabout](../includes/crabout-md.md)] usando esta caixa para especificar um tipo, consulte o [navegue e selecione uma caixa de diálogo do tipo .NET](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box.md) tópico.  
  
### <a name="the-interop-properties"></a>As propriedades de Interoperabilidade  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.Interop> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade ou na superfície de [!INCLUDE[wfd2](../includes/wfd2-md.md)] .  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.Interop> . O padrão é Interoperabilidade. Embora o nome para exibição não é necessário restrita, é uma prática recomendada usar um nome para exibição.|  
|<xref:System.Activities.Statements.Interop.ActivityType%2A>|verdadeiro|Especifica o tipo de atividade contida pela atividade de <xref:System.Activities.Statements.Interop> . Este tipo especificado deve derivar de <xref:System.Workflow.ComponentModel.Activity>.|  
  
## <a name="see-also"></a>Consulte também  
 [Migração](../workflow-designer/migration-activity-designers.md)
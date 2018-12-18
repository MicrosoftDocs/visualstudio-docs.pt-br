---
title: Caixa de diálogo de definição de CorrelatesOn | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- CorrelatesOnDefinition.UI
ms.assetid: 8b2b627a-f236-4479-aa09-525df65e3413
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 3171efb985eec54d0e935d2e8499c69631c6dfc8
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49285812"
---
# <a name="correlateson-definition-dialog-box"></a>Caixa de diálogo definição de CorrelatesOn
O **CorrelatesOn** caixa de diálogo é usada em [!INCLUDE[wfd1](../includes/wfd1-md.md)] para editar o <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> propriedade de um <xref:System.ServiceModel.Activities.Receive> atividade. [!INCLUDE[crdefault](../includes/crdefault-md.md)] o [Receive](../workflow-designer/receive-activity-designer.md) tópico.  
  
 Correlação entre atividades de <xref:System.ServiceModel.Activities.Receive> especifica como as operações de serviço diferentes conectam entre si em um fluxo de trabalho.  
  
 A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **CorrelatesOn** caixa de diálogo.  
  
|Elemento da Interface do Usuário|Descrição|  
|----------------|-----------------|  
|**CorrelatesWith**|<xref:System.ServiceModel.Activities.CorrelationHandle> que é usado para rotear a mensagem à instância apropriado de fluxo de trabalho.|  
|**Consultas XPath**|Um par chave/valor que contém as consultas usadas para extrair dados de correlação das mensagens de entrada. Isso corresponde à propriedade de <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> . Consultas XPath estão contidas em um objeto de <xref:System.ServiceModel.MessageQuerySet> .|  
  
## <a name="to-launch-the-correlateson-dialog-box"></a>Para iniciar a caixa de diálogo CorrelatesOn  
 O **Receive** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral. Isso cria uma atividade de <xref:System.ServiceModel.Activities.Receive> com <xref:System.Activities.Activity.DisplayName%2A> padrão Receive. Selecione o **Receive** designer de atividade e clique no botão de reticências ao lado do texto (coleção) para o **CorrelatesOn** propriedade na grade de propriedade para o **definição de CorrelatesOn**  caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.ServiceModel.Activities.Receive>   
 [Adicionar caixa de diálogo CorrelationInitializers](../workflow-designer/add-correlationinitializers-dialog-box.md)   
 [Adicionar caixa de diálogo correlação](http://msdn.microsoft.com/en-us/9e41a149-e8ab-41b1-8886-ea06a63041b6)   
 [Caixa de diálogo Inicializar Correlação](../workflow-designer/initialize-correlation-dialog-box.md)
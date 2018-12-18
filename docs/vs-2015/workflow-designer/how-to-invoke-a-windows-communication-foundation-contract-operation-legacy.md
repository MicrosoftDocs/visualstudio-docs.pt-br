---
title: 'Como: chamar uma operação de contrato Windows Communication Foundation (herdado) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: a9058345-708f-4fcf-8739-2a43e5285b7a
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 5e59d5ed9617d4be71a0542e35dd509d9035ae33
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49181838"
---
# <a name="how-to-invoke-a-windows-communication-foundation-contract-operation-legacy"></a>Como: Chamar uma operação do Windows Communication Foundation (o legados)
Este tópico descreve como chamar uma operação do contrato de [!INCLUDE[indigo1](../includes/indigo1-md.md)] usando o novas [!INCLUDE[wfd1](../includes/wfd1-md.md)] que direciona [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 Após arrastar uma **SendActivity** atividade da caixa de ferramentas para a superfície de design de fluxo de trabalho, você deve importar um contrato existente e determinar qual operação será invocada daquele **SendActivity** atividade. Selecione o contrato e as operações com o [escolha a caixa de diálogo da operação (herdado)](../workflow-designer/choose-operation-dialog-box-legacy.md).  
  
 Além disso, se você estiver usando um arquivo de configuração com o serviço, você precisará especificar <xref:System.Workflow.Activities.ChannelToken>. <xref:System.Workflow.Activities.ChannelToken> identifica a configuração do ponto de extremidade a atividade de enviar usará para se conectar ao serviço de fluxo de trabalho.  
  
### <a name="to-invoke-a-wcf-contract-operation-from-a-sendactivity-activity"></a>Para chamar a reduzir a operação de uma atividade de SendActivity  
  
1.  Clique duas vezes o **SendActivity** atividade no designer ou clique no botão de reticências próximo à **ServiceOperationInfo** propriedade no **propriedades** painel.  
  
2.  Quando o **escolher operação** caixa de diálogo é aberta, clique em **importação** no canto superior direito da caixa de diálogo.  
  
     O [navegue e selecione uma caixa de diálogo do tipo .NET (herdado)](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md) é aberta.  
  
3.  Pesquise por um assembly ou projeto que contém o contrato que você deseja.  
  
4.  Selecione o contrato e clique em **Okey**.  
  
5.  Sob **operações disponíveis**, selecione a operação que você deseja chamar e clique em **Okey**.  
  
### <a name="to-specify-a-channel-token"></a>Para especificar um token de canal  
  
1.  Selecione a atividade de <xref:System.Workflow.Activities.SendActivity> no designer.  
  
2.  No **propriedades** painel, especifique um nome para o <xref:System.Workflow.Activities.ChannelToken>. Este nome identifica unicamente o símbolo do canal.  
  
3.  Expanda o nó simbólico do canal e especifique um nome para o ponto final de cliente que você usará no campo de <xref:System.Workflow.Activities.ChannelToken.EndpointName%2A> . A configuração de ponto de extremidade de mesmo nome no arquivo de configuração será usada para configurar o canal.  
  
4.  Crie a configuração de ponto de extremidade no arquivo de configuração, se ele não existir. Para obter mais informações sobre como configurar seu cliente, consulte [visão geral do cliente WCF](http://msdn.microsoft.com/library/f60d9bc5-8ade-4471-8ecf-5a07a936c82d).  
  
## <a name="see-also"></a>Consulte também  
 [Escolha a caixa de diálogo de operação (herdado)](../workflow-designer/choose-operation-dialog-box-legacy.md)   
 [Como: implementar uma operação de contrato do Windows (legados)](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md)   
 [Atividades de fluxo de trabalho herdadas](../workflow-designer/legacy-workflow-activities.md)
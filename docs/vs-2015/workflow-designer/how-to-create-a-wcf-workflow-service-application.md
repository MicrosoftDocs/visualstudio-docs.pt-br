---
title: 'Como: criar um aplicativo de serviço de fluxo de trabalho WCF | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 12d675ac-27d8-4d86-ba16-6f7688f8c841
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 8632d8cf942fe4a06f12d324fea1f6f567080981
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49228430"
---
# <a name="how-to-create-a-wcf-workflow-service-application"></a>Como: Crie um aplicativo de Serviço WCF de Fluxo de Trabalho
aplicativos de serviço do fluxo de trabalho[!INCLUDE[indigo1](../includes/indigo1-md.md)] são serviços de comunicação distribuídos que transmitem as mensagens entre clientes e eles próprios através dos limites de processo. A implementação do contrato de serviço no lado de serviço é feita declarativamente com as atividades de fluxo de trabalho em [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] de um modo semelhante aos serviços herdados de fluxo de trabalho no .NET Framework 3.5.  
  
### <a name="to-create-a-wcf-workflow-service-application"></a>Para criar um aplicativo de serviço do fluxo de trabalho WCF  
  
1.  Inicie o [!INCLUDE[vs2010](../includes/vs2010-md.md)].  
  
2.  Sobre o **arquivo** , aponte para **New**e, em seguida, selecione **projeto...** .  
  
     A caixa de diálogo **Novo Projeto** é aberta.  
  
3.  No **modelos instalados** painel, selecione **WCF** ou **fluxo de trabalho** de qualquer um de **Visual c#** ou **doVisualBasic** agrupamentos, dependendo de você linguagem de sua escolha.  
  
4.  No painel central, selecione **aplicativo de serviço de fluxo de trabalho WCF**.  
  
5.  No **nome** , digite um nome descritivo para seu projeto para torná-lo mais fácil identificar.  
  
6.  No **local** , digite o diretório no qual você deseja salvar seu projeto, ou clique em **procurar** para navegar até ele.  
  
7.  No **Solution** , selecione para criar uma nova solução e, em seguida, clique em **Okey**.  
  
    > [!NOTE]
    >  Se você deseja adicionar um aplicativo de console do fluxo de trabalho a uma solução existente, abra essa solução na [!INCLUDE[vs2010](../includes/vs2010-md.md)], clique com botão direito na solução **Gerenciador de soluções**e selecione **Add**, em seguida,  **Novo projeto...** Para abrir o **novo projeto** caixa de diálogo. Continuar conforme descrito acima neste procedimento.  
  
8.  O modelo de projeto cria uma definição de serviço como XAML. [!INCLUDE[wfd1](../includes/wfd1-md.md)] abre para o modo design com uma atividade de <xref:System.Activities.Statements.Sequence> que contém um conjunto de <xref:System.ServiceModel.Activities.Receive> e de atividades de <xref:System.ServiceModel.Activities.SendReply> .  
  
## <a name="see-also"></a>Consulte também  
 [Como: criar uma atividade](http://msdn.microsoft.com/library/c09b1e99-21b5-4d96-9c04-ec31db3f4436)   
 [Criando um projeto de fluxo de trabalho](../workflow-designer/creating-a-workflow-project.md)
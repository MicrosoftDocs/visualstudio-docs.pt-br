---
title: Chamando os modelos de objeto do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, client object model
- SharePoint development in Visual Studio, server object model
- SharePoint commands [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, extensibility features
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 3afb988b226ccf62fae92ab02d8380d20b19605b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49853422"
---
# <a name="call-into-the-sharepoint-object-models"></a>Chamar os modelos de objeto do SharePoint
  Ao criar extensões para as ferramentas do SharePoint no Visual Studio, você terá que chamar APIs do SharePoint para executar determinadas tarefas. Por exemplo, se você criar uma etapa de implantação para projetos do SharePoint, você talvez precise chamar APIs para executar algumas das tarefas para implantar soluções do SharePoint.  
  
 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] e [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] fornecem dois modelos de objeto diferentes que você pode usar em extensões de ferramentas do SharePoint: um modelo de objeto de servidor e um modelo de objeto do cliente. Cada modelo de objeto tem vantagens e desvantagens no contexto das extensões de ferramentas do SharePoint.  
  
 Para uma visão geral dos modelos de objeto do SharePoint, consulte [extensões de ferramentas de visão geral do modelo de programação do SharePoint](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md).  
  
## <a name="use-the-client-object-model-in-extension-projects"></a>Use o modelo de objeto do cliente em projetos de extensão
 Quando você desenvolve uma extensão para as ferramentas do SharePoint, você pode usar o modelo de objeto do cliente em seu projeto, como qualquer outro conjunto de APIs gerenciadas. Você pode adicionar referências aos assemblies no modelo de objeto do cliente ao seu projeto, e você pode chamar APIs no modelo de objeto cliente diretamente do seu código.  
  
 No entanto, o modelo de objeto do cliente tem duas desvantagens no contexto das extensões de ferramentas do SharePoint:  
  
- O modelo de objeto do cliente fornece apenas um subconjunto do modelo de objeto de servidor. Se você tiver que usar a funcionalidade do SharePoint que não é exposta no modelo de objeto cliente, você deve usar o modelo de objeto do servidor.  
  
- Embora usando o modelo de objeto de cliente nas extensões de ferramentas do SharePoint deve funcionar na maioria dos casos, você pode encontrar alguns cenários em que chamadas para o modelo de objeto do cliente não funcionam conforme o esperado. O modelo de objeto do cliente foi projetado para ser usado em aplicativos cliente para chamar em sites do SharePoint em um farm ou servidor remoto. As ferramentas do SharePoint no Visual Studio funcionam somente com uma instalação local do SharePoint no computador de desenvolvimento. Portanto, quando você usa o modelo de objeto do cliente em uma extensão de ferramentas do SharePoint, você chamar um site do SharePoint no computador local, que não é como o modelo de objeto do cliente foi projetado para ser usado.  
  
  Para um passo a passo que demonstra como usar o modelo de objeto do cliente em uma extensão das ferramentas do SharePoint no Visual Studio, consulte [instruções passo a passo: chamar o modelo de objeto de cliente do SharePoint em uma extensão do Gerenciador de servidores](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md).  
  
## <a name="use-the-server-object-model-in-extension-projects"></a>Usar o modelo de objeto de servidor em projetos de extensão
 O modelo de objeto de servidor é um superconjunto do modelo de objeto cliente. Quando você usa o modelo de objeto de servidor, você pode usar todos os recursos que [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] e [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] expor por meio de programação.  

 Extensões de ferramentas do SharePoint podem usar as APIs no modelo de objeto de servidor, mas eles não é possível chamar as APIs diretamente. O modelo de objeto de servidor pode ser chamado apenas de um processo de 64 bits que tem como alvo o .NET Framework 3.5. No entanto, extensões de ferramentas do SharePoint exigem o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] e são executados no processo do Visual Studio de 32 bits. Isso impede que as extensões de ferramentas do SharePoint referenciar os assemblies no modelo de objeto do SharePoint server diretamente.  
  
 Se você quiser usar o modelo de objeto de servidor em uma extensão de ferramentas do SharePoint, você deve criar um personalizado *comando do SharePoint* para chamar a API. Você define o comando do SharePoint em um assembly secundário que pode chamar diretamente o modelo de objeto do servidor. Em seu projeto de extensão, você chama o comando do SharePoint indiretamente por meio do método ExecuteCommand de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> objeto.  
  
 Para obter mais informações sobre como criar e usar comandos do SharePoint, consulte [como: criar um comando do SharePoint](../sharepoint/how-to-create-a-sharepoint-command.md) e [como: executar um comando SharePoint](../sharepoint/how-to-execute-a-sharepoint-command.md). Para obter informações sobre como implantar os comandos do SharePoint, consulte [implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).  
  
 Para instruções passo a passo que demonstram como criar e usar comandos do SharePoint, consulte [instruções passo a passo: criar uma etapa de implantação para projetos do SharePoint](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md) e [passo a passo: estenda o Gerenciador de servidores para exibir web parts ](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md).  
  
### <a name="understand-how-sharepoint-commands-are-executed"></a>Entender como os comandos do SharePoint são executados
 Os assemblies que definem os comandos do SharePoint são carregados em um processo de host de 64 bits nomeado *vssphost4.exe*. Depois de chamar um comando do SharePoint em uma extensão de ferramentas do SharePoint, o comando é executado por *vssphost4.exe* em vez de processo do Visual Studio de 32 bits (*devenv.exe*). Você pode controlar alguns aspectos de como os comandos do SharePoint são executados, definindo valores no registro. Para obter mais informações, consulte [depurar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também
 [Como: criar um comando do SharePoint](../sharepoint/how-to-create-a-sharepoint-command.md)   
 [Como: executar um comando do SharePoint](../sharepoint/how-to-execute-a-sharepoint-command.md)   
 [Extensões de ferramentas de visão geral do modelo de programação do SharePoint](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)  
  

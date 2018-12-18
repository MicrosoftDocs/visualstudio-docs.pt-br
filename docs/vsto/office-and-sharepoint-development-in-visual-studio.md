---
title: Desenvolvimento do Office e SharePoint no Visual Studio
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], about developing applications
- Office development in Visual Studio
- Office projects
- Visual Studio Tools for Office, see Office development in Visual Studio
- Office applications [Office development in Visual Studio]
- Office Business Applications
- applications [Office development in Visual Studio]
- programming [Office development in Visual Studio]
- VSTO, see Office development in Visual Studio
- Office, development with Visual Studio
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 38291b46f2f9fee83ba9af0ae553cecca5ee35f6
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671697"
---
# <a name="office-and-sharepoint-development-in-visual-studio"></a>Desenvolvimento do Office e SharePoint no Visual Studio
  Você pode estender o Microsoft Office e SharePoint, criando um aplicativo leve ou suplemento que os usuários baixem do [Office Store](https://store.office.com/) ou um catálogo organizacional, ou criando uma solução baseada no .NET Framework que os usuários de instalar em um computador.  
  
 Neste tópico:  
  
-   [Criar suplementos para Office e SharePoint](#Apps)  
  
-   [Criar um suplemento do VSTO](#Add-ins)  
  
-   [Criar uma solução do SharePoint](#Solutions)  
  
##  <a name="Apps"></a> Criar suplementos para Office e SharePoint  
 Office 2013 e SharePoint 2013 apresentam um novo suplemento do modelo que ajuda você a criar, distribuir e monetizar suplementos que estendem o Office e SharePoint.  Esses suplementos podem executar no Office ou SharePoint Online, e os usuários podem interagir com eles de vários dispositivos.  
  
 Saiba como usar a nova [modelo de suplemento do Office](/office/dev/add-ins/overview/office-add-ins) para estender a experiência do Office para seus usuários.  
  
 Esses suplementos têm pegadas pequeno em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  Para começar, use as ferramentas de desenvolvedor do Office no Visual Studio ou a ferramenta leve baseada na web com o codinome Napa Office 365 ferramentas de desenvolvimento, que lhe permite criar projetos, escrever código e executar seus suplementos em um navegador.  
  
 ![Aplicativos para Office e SharePoint modelo conceitual](../vsto/media/officeandsharepointapps2015.png "aplicativos para o modelo conceitual do Office e SharePoint")  
  
### <a name="build-an-office-add-in"></a>Criar um suplemento do Office  
 Para estender a funcionalidade do Office, crie um suplemento do Office. Ele é basicamente uma página da Web que é hospedada em um aplicativo do Office como Word, Excel, Outlook e PowerPoint. Seu aplicativo pode adicionar funcionalidade a documentos, planilhas, mensagens de email, compromissos, apresentações e projetos.  
  
 Você pode vender seu aplicativo na Office Store.  O [Office Store](https://store.office.com/) facilita a monetizar seus suplementos, atualizações de gerenciar e acompanhar telemetria. Você também pode publicar seu aplicativo para usuários por meio de um aplicativo de aplicativos no SharePoint ou no Exchange Server.  
  
 O seguinte aplicativo do Office mostra os dados da planilha em um mapa do Bing.  
  
 ![Aplicativo de conteúdo para o Office](../vsto/media/appforoffice.png "aplicativo de conteúdo para o Office")  
  
 **Saiba mais**  
  
|Para|Consulte|  
|--------|---------|  
|Saiba mais sobre os suplementos do Office e, em seguida, crie um.|[Suplementos do Office](/office/dev/add-ins/publish/publish)|  
|Compare as diferentes maneiras em que você pode estender o Office e decidir se deve usar um aplicativo ou um suplemento do Office.|[Roteiro para suplementos do Office, VSTO e VBA](https://blogs.msdn.microsoft.com/officeapps/2013/06/18/roadmap-for-apps-for-office-vsto-and-vba/)|  
  
### <a name="build-a-sharepoint-add-in"></a>Criar um suplemento do SharePoint  
 Para estender o SharePoint para seus usuários, crie um suplemento do SharePoint. Ele é basicamente um aplicativo pequeno, fácil de usar, autônomo que resolve a necessidade dos usuários ou negócios.  
  
 Você pode vender seu aplicativo para SharePoint na [Office Store](https://store.office.com/). Você também pode publicar seu suplemento aos usuários por meio de um catálogo de suplemento do SharePoint.  Os proprietários de sites podem instalar, atualizar e desinstalar o suplemento em seus sites do SharePoint sem a Ajuda de um servidor do farm ou administrador de coleção de sites.  
  
 Aqui está um exemplo de um aplicativo do SharePoint que ajuda os usuários a gerenciar contatos de negócios.  
  
 ![Aplicativo do Gerenciador de contatos de negócios para o SharePoint](../vsto/media/appforsharepoint.png "aplicativo do Gerenciador de contatos de negócios para o SharePoint")  
  
 **Saiba mais**  
  
|Para|Consulte|  
|--------|---------|  
|Saiba mais sobre os suplementos do SharePoint e crie um.|[Suplementos do SharePoint](/sharepoint/dev/sp-add-ins/sharepoint-add-ins)|  
|Compare suplementos do SharePoint com soluções tradicionais do SharePoint.|[Suplementos do SharePoint em comparação com soluções do SharePoint](/sharepoint/dev/general-development/sharepoint-server-application-lifecycle-management)|  
|Escolha se deseja criar um suplemento do SharePoint ou uma solução do SharePoint.|[Decidir entre o SharePoint Add-ins e soluções do SharePoint](/sharepoint/dev/general-development/sharepoint-server-application-lifecycle-management)|
  
##  <a name="Add-ins"></a> Criar um suplemento do VSTO  
 Crie um suplemento de VSTO para Office 2007 ou Office 2010 de destino ou para estender o Office 2013 e Office 2016 além do que é possível com os suplementos do Office. Suplementos do VSTO é executado somente na área de trabalho. Os usuários precisam instalar suplementos do VSTO, portanto, eles são geralmente mais difíceis de implantar e dar suporte.  No entanto, seu suplemento do VSTO pode ser integrado mais estreitamente com o Office. Por exemplo, ele pode adicionar controles à Faixa de Opções do Office e executar tarefas de automação avançadas como mesclar documentos ou modificar gráficos. Você pode aproveitar o .NET Framework e usar o C# e o Visual Basic para interagir com objetos do Office.  
  
 Aqui está um exemplo que pode fazer o que um suplemento do VSTO. Este suplemento do VSTO adiciona controles da faixa de opções, um painel de tarefas personalizado e uma caixa de diálogo ao PowerPoint.  
  
 ![Solução de suplemento do PowerPoint](../vsto/media/powerpointaddin.png "solução de suplemento do PowerPoint")  
  
 **Saiba mais**  
  
|Para|Ler|  
|--------|----------|  
|Compare as diferentes maneiras em que você pode estender o Office e decidir se deve usar um suplemento do VSTO ou um suplemento do Office.|[Roteiro para suplementos do Office, VSTO e VBA](https://blogs.msdn.microsoft.com/officeapps/2013/06/18/roadmap-for-apps-for-office-vsto-and-vba/)|  
|Crie um suplemento do VSTO.|[Suplementos do VSTO compilar com o Visual Studio](create-vsto-add-ins-for-office-by-using-visual-studio.md)|  
  
##  <a name="Solutions"></a> Criar uma solução do SharePoint  
 Crie uma solução do SharePoint para SharePoint Foundation 2010 e SharePoint Server 2010 de destino ou para estender o SharePoint 2013 e SharePoint 2016 além do que é possível com um suplemento do SharePoint.  
  
 Soluções do SharePoint exigem servidores de farm do SharePoint no local. Os administradores devem instalá-los e, como soluções são executada no SharePoint, podem afetar o desempenho do servidor. No entanto, soluções fornecem maior acesso a objetos do SharePoint. Além disso, quando você cria uma solução do SharePoint, pode utilizar o .NET Framework e usar C# e Visual Basic para interagir com objetos do SharePoint.  
  
 **Saiba mais**  
  
|Para|Consulte|  
|--------|---------|  
|Compare as soluções do SharePoint com os suplementos do SharePoint.|[Suplementos do SharePoint em comparação com soluções do SharePoint](/sharepoint/dev/general-development/sharepoint-server-application-lifecycle-management)|  
|Criar uma solução do SharePoint.|[Criar soluções do SharePoint](../sharepoint/create-sharepoint-solutions.md)|  
  
  

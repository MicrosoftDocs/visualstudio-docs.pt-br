---
title: Personalização da interface do usuário do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- menus [Office development in Visual Studio], customizing
- actions panes [Office development in Visual Studio], creating
- WPF [Office development in Visual Studio]
- toolbars [Office development in Visual Studio], customizing
- Office applications [Office development in Visual Studio], UI customization
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 48c7fe1948231f88aba8309d6d06186848d32455
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49836756"
---
# <a name="office-ui-customization"></a>Personalização da interface do usuário do Office
  Você pode personalizar a interface do usuário (UI) de aplicativos do Microsoft Office usando as ferramentas de desenvolvedor do Office no Visual Studio. Este tópico descreve os recursos de interface do usuário que você pode personalizar nas seções a seguir:  
  
-   [Comparação dos recursos de interface do usuário](#Comparison)  
  
-   [Painéis de ações e painéis de tarefas personalizados](#Actions)  
  
-   [Faixa de opções personalizada da interface do usuário](#Ribbon)  
  
-   [Modo de exibição Backstage](#Backstage)  
  
-   [Regiões de formulário do Outlook](#FormRegion)  
  
-   [Controles em documentos](#Controls)  
  
-   [Menus de atalho](#Shortcut)  
  
##  <a name="Comparison"></a> Comparação dos recursos de interface do usuário  
 A tabela a seguir compara os principais recursos de interface do usuário que você pode personalizar em projetos do Microsoft Office.  
  
|Recurso|Tipos de projeto com suporte|Aplicativos com suporte do Microsoft Office|  
|-------------|-----------------------------|---------------------------------------------|  
|Painel de ações|Personalizações no nível de documento|Excel<br /><br /> Palavra|  
|Painéis de tarefas personalizados|Suplementos do VSTO|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Palavra<br /><br /> Excel|  
|Faixa de opções personalizada da interface do usuário|Personalizações no nível de documento<br /><br /> Suplementos do VSTO|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Projeto<br /><br /> Palavra<br /><br /> Visio|  
|Modo de exibição Backstage|Personalizações no nível de documento<br /><br /> Suplementos do VSTO|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)].<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Projeto<br /><br /> Palavra<br /><br /> Visio|  
|Regiões de formulário do Outlook|Suplementos do VSTO|Outlook|  
|Controles em documentos|Personalizações no nível de documento<br /><br /> Suplementos do VSTO|Excel<br /><br /> Palavra|  
|Menus de atalho|Personalizações no nível de documento<br /><br /> Suplementos do VSTO|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Projeto<br /><br /> Palavra<br /><br /> Visio<br /><br /> Excel|  
  
##  <a name="Actions"></a> Painéis de ações e painéis de tarefas personalizados  
 Painéis de tarefas estão os painéis de interface do usuário que normalmente são encaixados em um dos lados de uma janela em um aplicativo do Microsoft Office. Quase todos os aplicativos do Microsoft Office incluem painéis de tarefas internas. Um exemplo de um painel de tarefas é o painel de tarefas Ajuda no Word.  
  
 As ferramentas de desenvolvimento do Office no Visual Studio fornecem duas maneiras diferentes de personalizar os painéis de tarefas:  
  
- Você pode adicionar um painel de ações para uma personalização no nível de documento. Por padrão, o painel de ações é exibido no lado direito do aplicativo, à direita do documento. No entanto, o painel de ações também pode ser exibido para a esquerda, superior ou inferior do documento.  
  
- Você pode adicionar um painel de tarefas personalizado para um suplemento do VSTO. Os usuários podem encaixar painéis de tarefas personalizados em diferentes lados da janela do aplicativo, ou pode arrastar painéis de tarefas personalizados em qualquer local na janela.  
  
  Painéis de ações e painéis de tarefas personalizados fornecem funcionalidade hospedando uma variedade de controles para ajudar os usuários com tarefas como a entrada de dados. Em comparação com um grupo de faixa de opções, painéis de ações e painéis de tarefas personalizados fornecem uma área muito maior para incluir o texto e controles.  
  
  Para obter mais informações sobre painéis de ações, consulte [visão geral do painel de ações](../vsto/actions-pane-overview.md). Para obter mais informações sobre painéis de tarefas personalizados, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).  
  
##  <a name="Ribbon"></a> Faixa de opções personalizada da interface do usuário  
 Você pode personalizar a interface do usuário da faixa de opções para expor a funcionalidade que você adicionar a aplicativos do Office. A faixa de opções é uma maneira de organizar os comandos relacionados (na forma de controles) para que eles são mais fáceis de encontrar. Você pode criar seus próprios guias da faixa de opções e grupos para conceder aos usuários acesso à funcionalidade fornecida por você em sua solução. Agora, a maioria dos recursos que foram acessados usando os menus e barras de ferramentas em versões anteriores do Microsoft Office system pode ser acessada por meio da faixa de opções.  
  
 Para obter mais informações, consulte [visão geral da faixa de opções](../vsto/ribbon-overview.md).  
  
##  <a name="Backstage"></a> Modo de exibição Backstage  
 Em aplicativos do Office, clicando na **arquivo** guia abre o modo de exibição Backstage. O modo de exibição Backstage fornece uma interface do usuário que combina ações e tarefas de nível de arquivo e substitui a funcionalidade semelhante disponível no botão Microsoft Office no 2007 Microsoft Office system. O modo de exibição Backstage é totalmente extensível por meio de XML.  
  
 Visual Studio não fornece um designer ou APIs para personalizar o modo de exibição Backstage. No entanto, se você adicionar um **da faixa de opções (XML)** item ao seu projeto do Office, você pode adicionar o XML para o arquivo XML de faixa de opções para personalizar o modo de exibição Backstage. Para obter mais informações sobre **da faixa de opções (XML)** itens, consulte [XML da faixa de opções](../vsto/ribbon-xml.md).  
  
 Para obter mais informações sobre como personalizar o modo de exibição Backstage, consulte [Introdução ao modo de exibição Backstage do Office 2010 para desenvolvedores](http://go.microsoft.com/fwlink/?LinkId=182189) e [personalizar o modo de exibição Backstage do Office 2010 para desenvolvedores](http://go.microsoft.com/fwlink/?LinkId=182188).  
  
##  <a name="FormRegion"></a> Regiões de formulário do Outlook  
 Use as regiões do formulário para adicionar funcionalidade personalizada aos formulários padrão do Microsoft Office Outlook. Você pode criar regiões de formulário que estendem qualquer formulário existente com campos adicionais ou controles. Se você criar uma nova região de formulário usando as ferramentas de desenvolvimento do Office no Visual Studio, você pode usar somente os controles de formulários do Windows na região do formulário. Se você importar uma região de formulário que foi projetada no Outlook, você pode usar apenas controles nativos do Outlook.  
  
 Você pode criar regiões de formulário que ocupam diferentes áreas da interface do usuário do Outlook. Por exemplo, regiões de formulário adjacentes são exibidas na parte inferior da primeira página de um formulário, e cada região do formulário adjacente é recolhível. Você também pode adicionar uma região de formulário separado que é exibido como uma página de forma completa adicional e que podem aparecer em qualquer formulário padrão existente ou um formulário personalizado.  
  
 Para obter mais informações, consulte [regiões de formulário do Outlook criar](../vsto/creating-outlook-form-regions.md).  
  
##  <a name="Controls"></a> Controles em documentos  
 Você pode adicionar uma variedade de controles a documentos do Word e planilhas do Excel. Por exemplo, você talvez queira adicionar um controle de seletor de data a um documento para que o usuário possa inserir datas em um formato padrão ou colocar um botão em uma planilha para enviar dados para um banco de dados.  
  
 Quando você desenvolve projetos no nível de documento para Excel ou Word, você pode usar o designer do Visual Studio para adicionar controles ao documento ou pasta de trabalho em seu projeto em tempo de design, ou você pode adicionar programaticamente os controles em tempo de execução. Ao desenvolver projetos de suplemento do VSTO para Excel ou Word, você pode adicionar controles programaticamente para qualquer documento aberto ou a pasta de trabalho em tempo de execução.  
  
 Para obter mais informações, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md) e [controles na visão geral de documentos do Office do Windows forms](../vsto/windows-forms-controls-on-office-documents-overview.md).  
  
##  <a name="Shortcut"></a> Menus de atalho  
 Um menu de atalho é exibido quando o botão direito do mouse em um documento ou uma janela do aplicativo. Você pode definir um menu de atalho para aparecer após um evento ocorre, como quando um usuário clica um documento, pasta de trabalho ou controle de host. Você pode adicionar um número de comandos de menu diferente ou controles a um menu de atalho. Crie menus de atalho por meio de XML. Se você adicionar um **da faixa de opções (XML)** item ao seu projeto do Office, você pode adicionar o XML para o arquivo XML de faixa de opções para criar menus de atalho. Para obter mais informações sobre como usar XML para criar menus de atalho, consulte [como: adicionar comandos aos menus de atalho](../vsto/how-to-add-commands-to-shortcut-menus.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [Windows forms a controles em Visão geral de documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md)   
 [Visão geral do painel de ações](../vsto/actions-pane-overview.md)   
 [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)   
 [Painéis de tarefas personalizados](../vsto/custom-task-panes.md)   
 [Usar controles WPF em soluções do Office](../vsto/using-wpf-controls-in-office-solutions.md)   
 [Como: Mostrar a guia Desenvolvedor na faixa de opções](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)   
 [Como: Add-in de mostrar erros de interface do usuário](../vsto/how-to-show-add-in-user-interface-errors.md)   
 [Passo a passo: Coletar dados usando um formulário do Windows](../vsto/walkthrough-collecting-data-using-a-windows-form.md)  
  
  
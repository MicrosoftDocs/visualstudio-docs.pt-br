---
title: Recursos disponíveis por tipo de projeto e aplicativo do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio]
- Office development in Visual Studio, features
- Ribbon [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], features available
- document-level customizations [Office development in Visual Studio]
- Office projects [Office development in Visual Studio], features available
- add-ins [Office development in Visual Studio]
- form regions [Office development in Visual Studio], features available
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6fac14df471b0dfcda1d0bf4763158280211bc33
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672440"
---
# <a name="features-available-by-office-application-and-project-type"></a>Recursos disponíveis por tipo de projeto e aplicativo do Office
  Visual Studio tem vários tipos de modelos de projeto que dão suporte a cenários de negócios diferentes para aplicativos do Microsoft Office, incluindo os seguintes tipos:  
  
- Personalizações no nível do documento.  
  
- Suplementos do VSTO.  
  
  Nem todos os aplicativos podem usar cada tipo de projeto. Por exemplo, projetos de nível de documento estão disponíveis somente para o Microsoft Office Word e Microsoft Office Excel. Da mesma forma, alguns recursos estão disponíveis somente para determinados tipos de projetos ou aplicativos. Por exemplo, o painel de ações está disponível apenas no nível de documento e extensões da faixa de opções estão disponíveis apenas para alguns aplicativos. Para obter mais informações sobre os diferentes tipos de projetos, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md).  
  
> [!NOTE]  
>  Modelos de projeto do Office estão disponíveis apenas em algumas edições do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Para obter mais informações, consulte [configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md).  
  
## <a name="project-types-available-for-different-microsoft-office-applications"></a>Tipos de projeto disponíveis para diferentes aplicativos do Microsoft Office  
 A tabela a seguir mostra os aplicativos que você pode usar com cada tipo de projeto.  
  
|Tipos de projeto|Aplicativo do Microsoft Office|  
|-------------------|----------------------------------|  
|Personalizações no nível de documento|Excel<br /><br /> Palavra|  
|Suplementos do VSTO|Excel<br /><br /> InfoPath (InfoPath 2013 e InfoPath 2010 apenas)<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Projeto<br /><br /> Visio<br /><br /> Palavra<br /><br /> Excel|  
  
## <a name="features-available-in-different-project-types"></a>Recursos disponíveis em diferentes tipos de projeto  
 A tabela a seguir mostra quais tipos de projeto fornece cada recurso.  
  
|Recurso|Tipos de projeto que fornecem o recurso|Leitura adicional|  
|-------------|--------------------------------------------|---------------------|  
|Painel de ações.|Projetos de nível de documento.|[Visão geral do painel de ações](../vsto/actions-pane-overview.md)|  
|Implantação do ClickOnce.|VS e projetos no nível de documento.|[Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)|  
|Painéis de tarefas personalizados.|Suplemento projetos do VSTO para os seguintes aplicativos:<br /><br /> -Excel<br />-InfoPath (InfoPath 2013 e InfoPath 2010 apenas)<br />-Outlook<br />-PowerPoint<br />-Word|[Painéis de tarefas personalizados](../vsto/custom-task-panes.md)|  
|Partes XML personalizadas.|Projetos de nível de documento.<br /><br /> Projetos de nível de aplicativo para os seguintes aplicativos:<br /><br /> -Excel<br />-PowerPoint<br />-Word|[Visão geral de partes XML personalizado](../vsto/custom-xml-parts-overview.md)|  
|Cache de dados.|Projetos de nível de documento.|[Dados armazenados em cache em personalizações no nível de documento](../vsto/cached-data-in-document-level-customizations.md)|  
|Expor um objeto em um suplemento do VSTO para outras soluções do Microsoft Office.|Suplemento projetos do VSTO.|[Chamar o código no VSTO Add-ins de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)|  
|Os seguintes controles de host:<br /><br /> -Gráfico<br />-ListObject<br />-NamedRange<br />-Controles de conteúdo<br />-Indicador|Projetos de nível de documento.<br /><br /> Suplemento projetos do VSTO para Word e Excel.|[Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)|  
|Os seguintes controles de host:<br /><br /> -XMLMappedRange<br />-XMLNode<br />-XMLNodes|Projetos de nível de documento.|[Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)|  
|Implantação de vários projeto.|Projetos de nível de documento.<br /><br /> Suplemento projetos do VSTO.|[Passo a passo: Implantar várias soluções do Office em um único instalador do ClickOnce](https://msdn.microsoft.com/051223c0-4082-4799-b78b-a4763a9def55)|  
|Regiões de formulário do Outlook.|Suplemento projetos do VSTO para Outlook.|[Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)|  
|Ações de pós-implantação.|Projetos de nível de documento.<br /><br /> Suplemento projetos do VSTO.|[Passo a passo: Copiar um documento para o computador do usuário final após uma instalação do ClickOnce](https://msdn.microsoft.com/100090f7-bc63-4152-b3e1-19b48bc27466)|  
|Personalizações da faixa de opções.|Projetos de nível de documento.<br /><br /> Suplemento projetos do VSTO para os seguintes aplicativos:<br /><br /> -Excel<br />-InfoPath (InfoPath 2013 e InfoPath 2010 apenas)<br />-Outlook<br />-PowerPoint<br />-Projeto<br />-Visio<br />-Word|[Visão geral da faixa de opções](../vsto/ribbon-overview.md)|  
|Designer visual do documento.|Projetos de nível de documento.|[Projetos do Office no ambiente do Visual Studio](../vsto/office-projects-in-the-visual-studio-environment.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)   
 [Visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)   
 [Visão geral do painel de ações](../vsto/actions-pane-overview.md)   
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Dados armazenados em cache em personalizações no nível de documento](../vsto/cached-data-in-document-level-customizations.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)  
  
  
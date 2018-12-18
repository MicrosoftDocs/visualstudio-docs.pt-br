---
title: Soluções PowerPoint
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office solutions [Office development in Visual Studio], PowerPoint
- templates [Office development in Visual Studio], PowerPoint
- solutions [Office development in Visual Studio], PowerPoint
- projects [Office development in Visual Studio], PowerPoint
- PowerPoint [Office development in Visual Studio]
- Office projects [Office development in Visual Studio], PowerPoint
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d7a2775526a088129060fc6375958b08cf6b19eb
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49906553"
---
# <a name="powerpoint-solutions"></a>Soluções PowerPoint
  Visual Studio fornece modelos de projeto, que você pode usar para criar suplementos do VSTO para PowerPoint do Microsoft Office. Você pode usar suplementos do VSTO para automatizar o PowerPoint, estender os recursos do PowerPoint ou personalizar a interface de usuário (IU) do PowerPoint.  
  
 Para obter mais informações sobre o VSTO Add-ins, consulte [começar a programar VSTO Add-ins](../vsto/getting-started-programming-vsto-add-ins.md) e [arquitetura do VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md). Se você for iniciante em programação com o Microsoft Office, consulte [Introdução &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md).  
  
 [!INCLUDE[appliesto_pptallapp](../vsto/includes/appliesto-pptallapp-md.md)]  
  
> [!NOTE]  
>  Interessado em desenvolver soluções que estendem a experiência do Office em toda [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [como fazer: criar um suplemento para o Microsoft PowerPoint?](http://go.microsoft.com/fwlink/?LinkId=132767).  
  
## <a name="automate-powerpoint-by-using-the-powerpoint-object-model"></a>Automatizar o PowerPoint usando o modelo de objeto do PowerPoint  
 O modelo de objeto do PowerPoint expõe vários tipos que você pode usar para automatizar o PowerPoint. Esses tipos permitem que você escreva código para realizar tarefas comuns:  
  
- Programaticamente, crie e formate apresentações.  
  
- Adicionar ou remover slides de apresentações.  
  
- Adicione ou altere as formas em um slide.  
  
  Para acessar o modelo de objeto do PowerPoint de um suplemento do VSTO, use o `Application` campo do `ThisAddIn` classe em seu projeto. O `Application` campo retorna um <xref:Microsoft.Office.Interop.PowerPoint.Application> objeto que representa a instância atual do PowerPoint. Para obter mais informações, consulte [programa de suplementos do VSTO](../vsto/programming-vsto-add-ins.md).  
  
  Quando você chama o modelo de objeto do PowerPoint, você pode usar os tipos fornecidos no assembly de interoperabilidade primário para o PowerPoint. O assembly de interoperabilidade primário atua como uma ponte entre o código gerenciado em que o suplemento do VSTO e o modelo de objeto COM no PowerPoint. Todos os tipos no assembly de interoperabilidade primário do PowerPoint são definidos na <xref:Microsoft.Office.Interop.PowerPoint> namespace. Para obter mais informações sobre assemblies de interoperabilidade primários, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41; ](../vsto/office-solutions-development-overview-vsto.md) e [assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md).  
  
##  <a name="WordOMDocumentation"></a> Use a documentação de modelo de objeto do PowerPoint  
 Para obter informações completas sobre o modelo de objeto do PowerPoint, você pode consultar para a referência de assembly de interoperabilidade primária (PIA) do PowerPoint e a referência de modelo de objeto do VBA.  
  
### <a name="primary-interop-assembly-reference"></a>Referência de assembly de interoperabilidade primário  
 A documentação de referência de PIA PowerPoint descreve os tipos no assembly de interoperabilidade primário para o PowerPoint. Esta documentação está disponível no seguinte local: [referência de assembly de interoperabilidade primário do PowerPoint 2010](http://go.microsoft.com/fwlink/?LinkId=189588).  
  
 Para obter mais informações sobre o design de PIA o PowerPoint, como as diferenças entre classes e interfaces no PIA e como os eventos no PIA são implementados, consulte [visão geral de classes e interfaces em assemblies de interoperabilidade primários do Office ](http://go.microsoft.com/fwlink/?LinkId=199885).  
  
### <a name="vba-object-model-reference"></a>Referência de modelo de objeto do VBA  
 A referência de modelo de objeto VBA documenta o modelo de objeto do PowerPoint conforme ele é exposto ao Visual Basic para código Applications (VBA). Para obter mais informações, consulte [referência de modelo de objeto do PowerPoint 2010](http://go.microsoft.com/fwlink/?LinkId=199770)  
  
 Todos os objetos e membros na referência de modelo de objeto do VBA correspondem aos tipos e membros no PowerPoint assembly de interoperabilidade primário (PIA). Por exemplo, o objeto de apresentação na referência de modelo de objeto do VBA corresponde à <xref:Microsoft.Office.Interop.PowerPoint.Presentation> tipo no PIA do PowerPoint. Embora a referência de modelo de objeto VBA fornece exemplos de código para a maioria das propriedades, métodos e eventos, você deve converter o código VBA essa referência para o Visual Basic ou Visual c#, se você quiser usá-los em um projeto de suplemento do VSTO do PowerPoint que você cria usando Visual Studio.  
  
## <a name="customize-the-user-interface-of-powerpoint"></a>Personalizar a interface do usuário do PowerPoint  
 Você pode modificar a interface do usuário do PowerPoint das seguintes maneiras.  
  
|Tarefa|Para obter mais informações|  
|----------|--------------------------|  
|Crie um painel de tarefas personalizado.|[Painéis de tarefas personalizados](../vsto/custom-task-panes.md)|  
|Adicione guias personalizadas à faixa de opções.|[Visão geral da faixa de opções](../vsto/ribbon-overview.md)|  
|Adicione grupos personalizados a uma guia interna na faixa de opções.|[Como: personalizar uma guia interna](../vsto/how-to-customize-a-built-in-tab.md)|  
  
 Para obter mais informações sobre como personalizar a interface do usuário do PowerPoint e outros aplicativos do Microsoft Office, consulte [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Criar seu primeiro suplemento VSTO para PowerPoint](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)   
 [Introdução à programação VSTO Add-ins](../vsto/getting-started-programming-vsto-add-ins.md)   
 [Visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)   
 [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)   
 [Assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md)   
 [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)   
 [PowerPoint 2010 no desenvolvimento do Office](http://go.microsoft.com/fwlink/?LinkId=199015)  
  
  
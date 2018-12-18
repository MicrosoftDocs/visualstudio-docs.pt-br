---
title: Soluções de projeto
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [Office development in Visual Studio], Project
- Office solutions [Office development in Visual Studio], Project
- Project [Office development in Visual Studio]
- templates [Office development in Visual Studio], Project
- Office projects [Office development in Visual Studio], Project
- solutions [Office development in Visual Studio], Project
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9be194bb2812f46163a6844a9fa038ee79b5f0e7
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670198"
---
# <a name="project-solutions"></a>Soluções de projeto
  [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] fornece modelos de projeto, que você pode usar para criar suplementos do VSTO para o Microsoft Office Project. Você pode usar suplementos do VSTO para automatizar o projeto, estender os recursos de projeto ou personalizar a interface de usuário (IU) do Project.  
  
 Para obter mais informações sobre o VSTO Add-ins, consulte [começar a programar VSTO Add-ins](../vsto/getting-started-programming-vsto-add-ins.md) e [arquitetura do VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md). Se você for iniciante em programação com o Microsoft Office, consulte [Introdução &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md).  
  
 [!INCLUDE[appliesto_projallapp](../vsto/includes/appliesto-projallapp-md.md)]  
  
> [!NOTE]  
>  Interessado em desenvolver soluções que estendem a experiência do Office em toda [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  
  
## <a name="automate-project-by-using-the-project-object-model"></a>Automatizar o projeto usando o modelo de objeto do projeto  
 O modelo de objeto do projeto expõe vários tipos que você pode usar para automatizar o projeto. Esses tipos permitem que você escrever código para realizar tarefas comuns como criar e modificar tarefas em um projeto de forma programática.  
  
 Para acessar o modelo de objeto do projeto de um suplemento do VSTO, use o `Application` campo do `ThisAddIn` classe em seu projeto. O `Application` campo retorna um `Microsoft.Office.Interop.MsProject.Application` objeto que representa a instância atual do projeto. Para obter mais informações, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
 Quando você chama o modelo de objeto do projeto, você pode usar os tipos fornecidos no assembly de interoperabilidade primário para o projeto. O assembly de interoperabilidade primário atua como uma ponte entre o código gerenciado em que o suplemento do VSTO e o modelo de objeto COM no projeto. Todos os tipos no assembly de interoperabilidade primário do projeto são definidos na `Microsoft.Office.Interop.MSProject` namespace. Para obter mais informações sobre assemblies de interoperabilidade primários, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41; ](../vsto/office-solutions-development-overview-vsto.md) e [assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md).  
  
## <a name="use-the-project-object-model-documentation"></a>Use a documentação de modelo de objeto do projeto  
 Para obter informações completas sobre o modelo de objeto do projeto, você pode consultar a referência de modelo de objeto de projeto VBA. A referência de modelo de objeto VBA documenta o modelo de objeto do projeto conforme ele é exposto ao Visual Basic para código Applications (VBA). Para obter mais informações, consulte [referência de modelo de objeto do Project 2010](http://go.microsoft.com/fwlink/?LinkId=199771).  
  
 Todos os objetos e membros na referência de modelo de objeto do VBA correspondem aos tipos e membros no projeto assembly de interoperabilidade primário (PIA). Por exemplo, o objeto de calendário na referência de modelo de objeto do VBA corresponde à `Microsoft.Office.Interop.MSProject.Calendar` tipo no PIA do projeto. Embora a referência de modelo de objeto VBA fornece exemplos de código para a maioria das propriedades, métodos e eventos, você deve converter o código VBA essa referência para o Visual Basic ou Visual c#, se você quiser usá-los em um projeto de suplemento do VSTO do projeto que você cria usando o Visual Studio.  
  
> [!NOTE]  
>  Neste momento, não há nenhuma documentação de referência para o assembly de interoperabilidade primária do projeto.  
  
### <a name="infrastructure-types-in-the-project-primary-interop-assembly"></a>Tipos de infraestrutura em que o assembly de interoperabilidade primária do projeto  
 Conforme você escreve o código que usa o PIA do projeto, você poderá notar vários tipos que não são descritos na referência do VBA. Esses tipos adicionais ajuda a converter objetos no modelo de objeto baseado em COM de projeto para código gerenciado, não se destina a ser usado diretamente em seu código.  
  
 Para obter mais informações, consulte [visão geral de classes e interfaces em assemblies de interoperabilidade primários do Office](http://go.microsoft.com/fwlink/?LinkId=189592).  
  
## <a name="customize-the-user-interface-of-project"></a>Personalizar a interface do usuário do projeto  
 Você pode personalizar a interface do usuário do projeto das seguintes maneiras.  
  
|Tarefa|Para obter mais informações|  
|----------|--------------------------|  
|Adicionar guias personalizadas à faixa de opções no projeto|[Visão geral da faixa de opções](../vsto/ribbon-overview.md)|  
  
 Para obter mais informações sobre como personalizar a interface do usuário do projeto e outros aplicativos do Microsoft Office, consulte [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Criar seu primeiro suplemento VSTO para o projeto](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)   
 [Introdução à programação VSTO Add-ins](../vsto/getting-started-programming-vsto-add-ins.md)   
 [Visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)   
 [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)   
 [Assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md)   
 [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)   
 [Project 2010 e Project Server 2010 no desenvolvimento do Office](http://go.microsoft.com/fwlink/?LinkId=199016)  
  
  
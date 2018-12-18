---
title: Soluções do Visio
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], Visio
- solutions [Office development in Visual Studio], Visio
- Visio [Office development in Visual Studio]
- templates [Office development in Visual Studio], Visio
- projects [Office development in Visual Studio], Visio
- Office solutions [Office development in Visual Studio], Visio
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c7fc3f699cd33f2bb45487ca1329d812cfbeb950
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671541"
---
# <a name="visio-solutions"></a>Soluções do Visio
  Visual Studio fornece modelos de projeto, que você pode usar para criar suplementos do VSTO para o Microsoft Office Visio. Você pode usar suplementos do VSTO para automatizar o Visio, estender os recursos do Visio ou personalizar a interface de usuário (IU) do Visio.  
  
 Para obter mais informações sobre o VSTO Add-ins, consulte [começar a programar VSTO Add-ins](../vsto/getting-started-programming-vsto-add-ins.md) e [arquitetura do VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md). Se você for iniciante em programação com o Microsoft Office, consulte [Introdução &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md).  
  
 **Aplica-se a:** as informações neste tópico se aplicam a projetos de suplemento do VSTO do Visio 2010. Para obter mais informações, confira [Features Available by Office Application and Project Type](../vsto/features-available-by-office-application-and-project-type.md) (Funcionalidades disponibilizadas pelo aplicativo do Office e pelo tipo de projeto).  
  
> [!NOTE]  
>  Interessado em desenvolver soluções que estendem a experiência do Office em toda [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  
  
## <a name="automate-visio-by-using-the-visio-object-model"></a>Automatizar o Visio usando o modelo de objeto do Visio  
 O modelo de objeto do Visio expõe muitas classes que você pode usar para automatizar o Visio para criar diagramas organogramas, fluxogramas, cronogramas de projeto, diagramas de rede, espaços do office e muito mais. A API permite que você escreva código para realizar tarefas comuns:  
  
- Construir e posicionar o texto e formas em diagramas.  
  
- Gerencie o comportamento de forma com base na lógica de negócios e a entrada do usuário.  
  
- Visualização do diagrama de controle como Panorâmica e zoom.  
  
- Personalize o interface do usuário do aplicativo.  
  
- Importar dados externos para o Visio, vinculá-lo a formas e exibi-la graficamente em uma página.  
  
  Você pode exibir os procedimentos passo a passo e exemplos de código de usando o modelo de objeto do Visio para trabalhar com documentos e formas no [trabalhar com documentos do Visio](../vsto/working-with-visio-documents.md) e [trabalhar com formas do Visio](../vsto/working-with-visio-shapes.md).  
  
  Para acessar o modelo de objeto do Visio de um suplemento do VSTO, use o `Application` campo do `ThisAddIn` classe em seu projeto. O `Application` campo retorna um `Microsoft.Office.Interop.Visio.Application` objeto que representa a instância atual do Visio. Para obter mais informações, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
  Quando você chama o modelo de objeto do Visio, você pode usar os tipos fornecidos no assembly de interoperabilidade primário (PIA) do Visio. O PIA atua como uma ponte entre o código gerenciado em que o suplemento do VSTO e o modelo de objeto COM no Visio. Todos os tipos no PIA do Visio são definidos na `Microsoft.Office.Interop.Visio` namespace. Para obter mais informações sobre assemblies de interoperabilidade primários, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41; ](../vsto/office-solutions-development-overview-vsto.md) e [assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md).  
  
## <a name="visio-object-model-overview"></a>Visão geral do modelo de objeto do Visio  
 Você pode encontrar uma visão geral do modelo de objeto do Visio no [visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md), que inclui links para a referência de modelo de objeto do Visio e os SDKs.  
  
## <a name="customize-the-user-interface-of-visio"></a>Personalizar a interface do usuário do Visio  
 O Visio UI tem as seguintes opções de personalização.  
  
|Tarefa|Para obter mais informações|  
|----------|--------------------------|  
|Personalize a faixa de opções.|[Visão geral da faixa de opções](../vsto/ribbon-overview.md)|  
  
 Para obter informações sobre como personalizar a interface do usuário do Visio, consulte a documentação de referência do VBA para o [Visio.UIObject](/office/vba/api/Visio.UIObject) classe.  
  
## <a name="see-also"></a>Consulte também  
 [Introdução à programação VSTO Add-ins](../vsto/getting-started-programming-vsto-add-ins.md)   
 [Visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)   
 [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)   
 [Assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md)   
 [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)   
 [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)   
 [Visio 2010 no desenvolvimento do Office](http://go.microsoft.com/fwlink/?LinkId=199017)  
  
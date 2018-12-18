---
title: Referência gerenciada (desenvolvimento do Office no Visual Studio)
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- reference [Office development in Visual Studio], 2007 Microsoft Office system
- Office development in Visual Studio, reference
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: a3c991b6507ded441dd37ec92cb5efd0e2167285
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34572186"
---
# <a name="managed-reference-office-development-in-visual-studio"></a>Referência gerenciada (desenvolvimento do Office no Visual Studio)
  Esta seção contém a documentação de referência de API para namespaces e tipos que são usados no Office projetos direcionados a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]. Para obter a documentação de referência de API sobre os namespaces e tipos que são usados em projetos do Office destinados ao .NET Framework 3.5, consulte a seguinte seção de referência na documentação do Visual Studio: [ http://go.microsoft.com/fwlink/?LinkId=160658 ](http://go.microsoft.com/fwlink/?LinkId=160658).  
  
> [!NOTE]  
>  Interessado em desenvolvimento de soluções que estendem a experiência do Office em [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com suplementos do VSTO e soluções, e você pode criá-los usando quase qualquer tecnologia, como JavaScript, HTML5, CSS3 e XML de programação da web.  
  
## <a name="in-this-section"></a>Nesta seção  
 <xref:Microsoft.Office.Tools>  
 Contém classes comuns de programação de soluções do Office. Isso inclui a classe base para suplementos do VSTO, classes para a criação de painéis de tarefas personalizados nos suplementos do VSTO, classes para a criação de marcas inteligentes em soluções do Excel e Word e para a criação de painéis de ações em personalizações no nível do documento.  
  
 <xref:Microsoft.Office.Tools.Excel>  
 Contém os controles de host e itens de host que podem ser usados em soluções do Excel.  
  
 <xref:Microsoft.Office.Tools.Excel.Controls>  
 Contém os controles do Excel e controles de formulários do Windows que podem ser usados em soluções do Excel.  
  
 <xref:Microsoft.Office.Tools.Outlook>  
 Contém classes usadas pelos suplementos do VSTO para Outlook, incluindo classes que são usadas para criar regiões de formulário personalizado.  
  
 <xref:Microsoft.Office.Tools.Ribbon>  
 Contém classes que são usadas para modificar programaticamente personalizações da faixa de opções criadas usando o designer de faixa de opções.  
  
 <xref:Microsoft.Office.Tools.Word>  
 Contém os controles de host e itens de host que podem ser usados em soluções do Word.  
  
 <xref:Microsoft.Office.Tools.Word.Controls>  
 Contém os controles do Word e controles de formulários do Windows que podem ser usados em soluções do Word.  
  
 <xref:Microsoft.VisualStudio.Tools.Applications>  
 Contém o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe e um conjunto de relacionadas classes de dados armazenados em cache. Essas classes podem ser usadas para modificar alguns aspectos das personalizações de nível de documento em computadores que não têm o Microsoft Office instalado.  
  
 <xref:Microsoft.VisualStudio.Tools.Applications.Deployment>  
 Contém o <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> interface (que você pode implementar para criar um *lançar a ação de implantação* para uma solução do Office), exceções que podem ser geradas ao instalar uma solução do Office e outras APIs que fazem parte do Visual Infraestrutura do Studio.  
  
 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime>  
 Contém a maioria das exceções que podem ser geradas pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)], várias classes que podem ser usados para dados de cache em personalizações no nível do documento e outras APIs que fazem parte da infraestrutura do Visual Studio.  
  
 <xref:Microsoft.VisualStudio.Tools.Office.BuildTasks>  
 Contém classes de tarefa MSBuild que são usados para criar projetos do Office.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas do Visual Studio para visão geral de tempo de execução do Office](../vsto/visual-studio-tools-for-office-runtime-overview.md)   
 [Introdução &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)   
 [Explicações passo a passo e exemplos de desenvolvimento do office](../vsto/office-development-samples-and-walkthroughs.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)  
  
  
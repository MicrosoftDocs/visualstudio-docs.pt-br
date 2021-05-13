---
title: Começar a programar os complementos do VSTO
description: Saiba como você pode usar os Complementos do VSTO para automatizar Microsoft Office aplicativos, estender recursos do aplicativo e personalizar a interface do usuário do aplicativo.
ms.custom: SEO-VS-2020
ms.date: 04/28/2021
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.Outlook
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], getting started
- add-ins [Office development in Visual Studio], getting started
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1757dd6042536b6a042e67a8b3dcd9b12a2ea758
ms.sourcegitcommit: 9cb0097c33755a3e5cbadde3b0a6e9e76cee727d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2021
ms.locfileid: "109848286"
---
# <a name="get-started-programming-vsto-add-ins"></a>Começar a programar os complementos do VSTO
> [!IMPORTANT]
> O VSTO depende do [.NET Framework](https://docs.microsoft.com/dotnet/framework/get-started/overview). Os complementos COM também podem ser escritos com o .NET Framework. Os complementos do Office não podem ser criados com o .NET Core e [o .NET 5+](https://docs.microsoft.com/dotnet/core/dotnet-five), as versões mais recentes do .NET. Isso porque o .NET Core/.NET 5+ não pode trabalhar junto com .NET Framework no mesmo processo e pode levar a falhas de carga de complemento. Você pode continuar a usar .NET Framework para gravar os complementos VSTO e COM para o Office. A Microsoft não atualizará o VSTO ou a plataforma de complemento COM para usar o .NET Core ou o .NET 5+. Você pode aproveitar o .NET Core e o .NET 5+, incluindo ASP.NET Core, para criar o lado do servidor dos [complementos da Web do Office.](https://docs.microsoft.com/office/dev/add-ins/overview/office-add-ins)

  Você pode usar os Complementos do VSTO para automatizar Microsoft Office aplicativos, estender recursos do aplicativo e personalizar a interface do usuário do aplicativo. Para obter informações sobre como os complementos vsto se comparam a outros tipos de soluções do Office que você pode criar usando o Visual Studio, consulte Visão geral de desenvolvimento de soluções do Office &#40;[VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md).

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

## <a name="create-vsto-add-in-projects"></a>Criar projetos de complemento do VSTO
 Crie projetos de complemento do VSTO usando um dos modelos de projeto de complemento do VSTO na **caixa de diálogo Novo** Projeto. Esses modelos incluem referências de assembly necessárias e arquivos de projeto. Visual Studio fornece modelos de projeto de complemento do VSTO para a maioria dos aplicativos no Office.

 Para obter mais informações sobre como criar um projeto de complemento do VSTO, consulte [Como criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md). Para obter mais informações sobre os modelos de projeto, consulte Visão geral dos modelos [de projeto do Office.](../vsto/office-project-templates-overview.md)

## <a name="develop-vsto-add-in-projects"></a>Desenvolver projetos de complemento do VSTO
 Quando você cria um projeto de complemento do VSTO, Visual Studio cria automaticamente um arquivo de código *ThisAddIn.vb* (em ) ou [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] *ThisAddIn.cs* (em C#). Esse arquivo contém a `ThisAddIn` classe, que fornece a base para seu suplemento do VSTO. Você pode usar os membros dessa classe para executar o código quando o suplemento do VSTO é carregado ou descarregado, para acessar o modelo de objeto do aplicativo host e para estender recursos do aplicativo. Para obter mais informações, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md).

## <a name="automate-applications-by-using-the-object-models"></a>Automatizar aplicativos usando os modelos de objetos
 Os modelos de objeto do Microsoft Office aplicativos expõem muitos tipos que você pode programar em um suplemento do VSTO. Você pode usar esses tipos para automatizar o aplicativo. Por exemplo, você pode criar e enviar programaticamente uma mensagem de email no Outlook, ou pode abrir um documento e adicionar conteúdo no Word. Para obter mais informações sobre como acessar o modelo de objeto do aplicativo host no código, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md).

 Para obter mais informações sobre os modelos de objeto de aplicativos Microsoft Office específicos, consulte os seguintes tópicos:

- [Visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md)

- [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)

- [Visão geral do modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md)

- [Soluções do InfoPath](../vsto/infopath-solutions.md)

- [Soluções do PowerPoint](../vsto/powerpoint-solutions.md)

- [Soluções de projeto](../vsto/project-solutions.md)

- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)

## <a name="customize-the-user-interface-of-applications"></a>Personalizar a interface do usuário de aplicativos
 Há várias maneiras diferentes de personalizar a interface do usuário do aplicativo host usando um suplemento do VSTO:

- Para Excel e Word, você pode adicionar controles gerenciados a documentos. Para obter mais informações, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

- Você pode personalizar a Faixa de Opções se o aplicativo dá suporte a ela. Para obter mais informações, consulte Visão geral [da faixa de opções.](../vsto/ribbon-overview.md)

- Você pode criar um painel de tarefas personalizado se o aplicativo dá suporte a ele. Para obter mais informações, consulte [Painéis de tarefas personalizados.](../vsto/custom-task-panes.md)

- Para o Outlook, você pode criar uma região de formulário personalizada. Para obter mais informações, consulte [Criar regiões de formulário do Outlook.](../vsto/creating-outlook-form-regions.md)

- Para todos Microsoft Office aplicativos, você pode exibir Windows Forms no seu complemento VSTO.

  Para obter mais informações sobre como personalizar a interface do usuário de Microsoft Office aplicativos, consulte [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md).

## <a name="next-steps"></a>Próximas etapas
 Para saber como criar complementos do VSTO, confira os seguintes passo a passo:

- [Passo a passo: criar seu primeiro complemento VSTO para Excel](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)

- [Passo a passo: criar seu primeiro vsto Add-In para Outlook](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)

- [Passo a passo: criar seu primeiro complemento VSTO para o PowerPoint](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)

- [Passo a passo: criar seu primeiro complemento vsto para projeto](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)

- [Passo a passo: criar seu primeiro complemento do VSTO para Word](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)

  Esses passo a passo apresentam as ferramentas de desenvolvimento do Office no Visual Studio e o modelo de programação para os complementos do VSTO.

  Para ver uma lista de tópicos que explicam algumas das tarefas comuns em projetos do Office, consulte [Tarefas comuns na programação do Office.](../vsto/common-tasks-in-office-programming.md)

## <a name="see-also"></a>Confira também
- [Como criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Começar a &#40;do Office no Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)
- [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)
- [Programar complementos do VSTO](../vsto/programming-vsto-add-ins.md)

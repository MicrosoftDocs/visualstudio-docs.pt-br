---
title: Usar controles WPF em soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- WPF [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5419a715cbe255b5cfc31a113a00e3525d63d827
ms.sourcegitcommit: 96a6d1f16d06ca28d309d05b6e9fbd52f628cdbc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40008197"
---
# <a name="use-wpf-controls-in-office-solutions"></a>Usar controles WPF em soluções do Office

Embora as soluções criadas usando as ferramentas de desenvolvimento do Office no Visual Studio são projetadas para trabalhar com diretamente com os controles dos Windows Forms, você também pode usar controles WPF em suas soluções. Windows Presentation Foundation (WPF) é uma alternativa ao Windows Forms para a criação de interfaces do usuário. WPF usa uma linguagem de marcação chamada de de Extensible Application Markup Language (XAML) para fornecer novas técnicas para incorporação de documentos, mídia e interface do usuário. Para obter mais informações, consulte [visão geral do WPF](../designers/introduction-to-wpf.md).

[!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

Qualquer elemento de interface do usuário que pode hospedar controles de formulários do Windows em uma solução do Office também pode hospedar controles do WPF. Isso inclui os seguintes elementos:

-   Os documentos e planilhas em personalizações no nível do documento.

-   Painéis de ações em personalizações no nível do documento.

-   Painéis de tarefas personalizados nos suplementos do VSTO.

-   Regiões do formulário em suplementos do VSTO para Outlook.

## <a name="add-wpf-controls-to-office-projects-at-design-time"></a>Adicionar controles WPF para projetos do Office em tempo de design

Você não pode adicionar controles do WPF diretamente aos elementos de interface do usuário em soluções do Office. Em vez disso, adicione uma **controle de usuário (WPF)** item ao seu projeto e, em seguida, usá-la como superfície de design para controles do WPF. Em seguida, adicione o controle de usuário do WPF a um elemento de interface do usuário em seu projeto.

### <a name="to-add-wpf-controls-to-an-actions-pane-custom-task-pane-or-form-region"></a>Para adicionar controles WPF a um painel de ações, painel de tarefas personalizado ou região de formulário

1.  Abra um projeto para o qual você deseja adicionar um painel de tarefas personalizado, um painel de ações ou uma região de formulário.

2.  Adicionar um **controle de usuário (WPF)** item ao seu projeto.

3.  Dos **caixa de ferramentas**, adicionar controles WPF para a superfície de design de controle de usuário do WPF.

     Por padrão, quando o designer de controle de usuário do WPF estiver aberto, o **caixa de ferramentas** contém controles do WPF.

4.  Compile o projeto.

5.  Adicione um painel de ações, a região do formulário ou o painel de tarefas personalizado ao seu projeto:

    -   Para regiões de formulário, adicione uma **região de formulário do Outlook** item ao projeto. Para obter mais informações, consulte [como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md).

    -   Para obter os painéis de ações, adicione uma **controle do painel Ações** ou **controle de usuário** item ao projeto. Para obter mais informações, consulte [como: adicionar um painel de ações a documentos do Word ou pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md) e [como: adicionar um painel de ações a documentos do Word ou pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md).

    -   Para obter os painéis de tarefas personalizados, adicione uma **controle de usuário** item ao projeto. Para obter mais informações, consulte [como: adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md).

6.  Do *ProjectName* **controles de usuário WPF** guia da **caixa de ferramentas**, arraste o controle de usuário do WPF para o designer para o painel Ações, a região do formulário ou o painel de tarefas personalizado.

     Visual Studio cria automaticamente um <xref:System.Windows.Forms.Integration.ElementHost> objeto que hospeda o controle de usuário do WPF no elemento de interface do usuário.

7.  Recompile o projeto.

#### <a name="to-add-wpf-controls-to-a-document-or-worksheet-in-a-document-level-project"></a>Para adicionar controles WPF a um documento ou planilha em um projeto de nível de documento

1.  Abra um projeto de nível de documento para Word ou Excel.

2.  Adicionar um **controle de usuário (WPF)** item ao seu projeto.

3.  Dos **caixa de ferramentas**, adicionar controles WPF para a superfície de design de controle de usuário do WPF.

4.  Compile o projeto.

5.  Adicionar um **controle de usuário** item (ou seja, um controle de usuário de formulários do Windows) para o projeto.

6.  Abra o designer para o controle de usuário do Windows Forms.

7.  Do *ProjectName* **controles de usuário WPF** guia do **caixa de ferramentas**, arraste o controle de usuário do WPF para o designer.

     Visual Studio cria automaticamente um <xref:System.Windows.Forms.Integration.ElementHost> objeto que hospeda o controle de usuário do WPF no controle de usuário do Windows Forms.

8.  Escreva código que adiciona programaticamente o controle de usuário de formulários do Windows para o documento ou pasta de trabalho. Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).

    > [!NOTE]
    > Você não pode arrastar o controle de usuário do Windows Forms para o documento ou planilha no designer.

9. Recompile o projeto.

## <a name="host-wpf-controls-by-using-the-elementhost-class"></a>Hospedar controles do WPF usando a classe ElementHost

O Visual Studio fornece recursos que ajudam você a usam controles de formulários do Windows em suas soluções do Office, mas ele não fornece recursos semelhantes para controles do WPF. Por exemplo, você pode adicionar controles dos Windows Forms a documentos e planilhas em tempo de design arrastando controles dos **caixa de ferramentas**, ou em tempo de execução usando os métodos auxiliares. No entanto, essas ferramentas não estão disponíveis para controles do WPF.

Uso de controles WPF a <xref:System.Windows.Forms.Integration.ElementHost> classe como uma camada de integração entre um controle dos Windows Forms ou formulário e os controles do WPF. Quando você adiciona controles do WPF à sua solução em tempo de design, o Visual Studio gera automaticamente um <xref:System.Windows.Forms.Integration.ElementHost> objeto para você.

## <a name="wpf-resources"></a>Recursos do WPF

Para obter mais informações sobre arquitetura e problemas de design para hospedar controles WPF em formulários e controles dos Windows Forms, consulte os tópicos a seguir:

-   [Arquitetura de entrada da interoperabilidade do Windows Forms e WPF](/dotnet/framework/wpf/advanced/windows-forms-and-wpf-interoperability-input-architecture)

-   [Mapeamento de propriedade do Windows Forms e WPF](/dotnet/framework/wpf/advanced/windows-forms-and-wpf-property-mapping)

-   [Interoperação de WPF e Windows Forms](/dotnet/framework/wpf/advanced/wpf-and-windows-forms-interoperation)

-   [Controles dos Windows Forms e controles do WPF equivalentes](/dotnet/framework/wpf/advanced/windows-forms-controls-and-equivalent-wpf-controls)

Para obter mais informações sobre como adicionar controles do WPF para controles dos Windows Forms e formulários no Visual Studio em tempo de design, consulte os tópicos a seguir:

-   [Passo a passo: Criar um novo conteúdo WPF nos Windows Forms em tempo de design](/dotnet/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time)

-   [Passo a passo: Organizar o conteúdo do WPF nos Windows Forms em tempo de design](/dotnet/framework/winforms/advanced/walkthrough-arranging-wpf-content-on-windows-forms-at-design-time)

-   [Passo a passo: Estilo conteúdo do WPF](/dotnet/framework/winforms/advanced/walkthrough-styling-wpf-content)

## <a name="see-also"></a>Consulte também

- [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)
- [Controles de formulários do Windows na visão geral de documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [Visão geral do painel de ações](../vsto/actions-pane-overview.md)
- [Painéis de tarefas personalizados](../vsto/custom-task-panes.md)
- [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)
- [Como: adicionar um painel de ações a documentos do Word ou pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [Como: adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [Como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)

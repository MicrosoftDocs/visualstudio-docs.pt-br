---
title: Programar suplementos do VSTO
description: Saiba como você pode usar a classe ThisAddIn para executar tarefas como acessar o modelo de objeto do aplicativo host Microsoft Office.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.Addin
- VST.ProjectItem.AddinProject
- thisAddIn
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ICustomTaskPaneConsumer interface
- add-ins [Office development in Visual Studio], programming
- IRibbonExtensibility interface
- UI customizing [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], application-level add-ins
- programming [Office development in Visual Studio], application-level add-ins
- ThisAddIn class
- user interfaces [Office development in Visual Studio], customizing
- writing code for Office solutions
- host items [Office development in Visual Studio], AddIn
- application development [Office development in Visual Studio], application-level add-ins
- add-ins [Office development in Visual Studio], ThisAddIn class
- application-level add-ins [Office development in Visual Studio], ThisAddIn class
- FormRegionStartup interface
- ThisAddIn_Startup
- application-level add-ins [Office development in Visual Studio], programming
- ThisAddIn_Shutdown
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 2ee62f35b0626139a8080649076d2ac941366a26
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828703"
---
# <a name="program-vsto-add-ins"></a>Programar suplementos do VSTO
  Ao estender um aplicativo Microsoft Office criando um suplemento do VSTO, você escreve o código diretamente `ThisAddIn` na classe em seu projeto. Você pode usar essa classe para executar tarefas como acessar o modelo de objeto do aplicativo host Microsoft Office, personalizar a interface do usuário do aplicativo e expor objetos em seu suplemento do VSTO a outras soluções do Office.

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

 Alguns aspectos da gravação de código em projetos de suplemento do VSTO são diferentes de outros tipos de projetos no Visual Studio. Muitas dessas diferenças são causadas pela maneira como os modelos de objeto do Office são expostos ao código gerenciado. Para obter mais informações, consulte [escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md).

 Para obter informações gerais sobre os suplementos do VSTO e outros tipos de soluções que você pode criar usando as ferramentas de desenvolvimento do Office no Visual Studio, consulte [visão geral do desenvolvimento de soluções do office &#40;&#41;do VSTO ](../vsto/office-solutions-development-overview-vsto.md).

## <a name="use-the-thisaddin-class"></a>Usar a classe ThisAddIn
 Você pode começar a gravar seu código de suplemento do VSTO na `ThisAddIn` classe. O Visual Studio gera automaticamente essa classe no arquivo de código *ThisAddIn. vb* (no [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] ) ou *ThisAddIn. cs* (em C#) em seu projeto de suplemento do VSTO. O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] instancia automaticamente essa classe para você quando o aplicativo Microsoft Office carrega seu suplemento do VSTO.

 Há dois manipuladores de eventos padrão na `ThisAddIn` classe. Para executar o código quando o suplemento do VSTO for carregado, adicione o código ao `ThisAddIn_Startup` manipulador de eventos. Para executar o código logo antes que o suplemento do VSTO seja descarregado, adicione o código ao `ThisAddIn_Shutdown` manipulador de eventos. Para obter mais informações sobre esses manipuladores de eventos, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).

> [!NOTE]
> No Outlook, por padrão, o `ThisAddIn_Shutdown` manipulador de eventos nem sempre é chamado quando o suplemento do VSTO é descarregado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).

### <a name="access-the-object-model-of-the-host-application"></a>Acessar o modelo de objeto do aplicativo host
 Para acessar o modelo de objeto do aplicativo host, use o `Application` campo da `ThisAddIn` classe. Esse campo retorna um objeto que representa a instância atual do aplicativo host. A tabela a seguir lista o tipo de valor de retorno para o `Application` campo em cada projeto de suplemento do VSTO.

|Aplicativo host|Tipo de valor de retorno|
|----------------------|-----------------------|
|Microsoft Office Excel|<xref:Microsoft.Office.Interop.Excel.Application>|
|Microsoft Office InfoPath|<xref:Microsoft.Office.Interop.InfoPath.Application>|
|Microsoft Office Outlook|<xref:Microsoft.Office.Interop.Outlook.Application>|
|Microsoft Office PowerPoint|[Aplicativo](/previous-versions/office/developer/office-2010/ff764034(v=office.14))|
|Microsoft Office Project|Microsoft. Office. Interop. MSProject. Application|
|Microsoft Office Visio|Microsoft. Office. Interop. Visio. Application|
|Microsoft Office Word|<xref:Microsoft.Office.Interop.Word.Application>|

 O exemplo de código a seguir mostra como usar o `Application` campo para criar uma nova pasta de trabalho em um suplemento do VSTO para Microsoft Office Excel. Este exemplo deve ser executado a partir da `ThisAddIn` classe.

```vb
Dim newWorkbook As Excel.Workbook = Me.Application.Workbooks.Add()
```

```csharp
Excel.Workbook newWorkbook = this.Application.Workbooks.Add(System.Type.Missing);
```

 Para fazer a mesma coisa de fora da `ThisAddIn` classe, use o `Globals` objeto para acessar a `ThisAddIn` classe. Para obter mais informações sobre o `Globals` objeto, consulte [acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).

```vb
Dim newWorkbook As Excel.Workbook = Globals.ThisAddIn.Application.Workbooks.Add()
```

```csharp
Excel.Workbook newWorkbook = Globals.ThisAddIn.Application.Workbooks.Add(System.Type.Missing);
```

 Para obter mais informações sobre os modelos de objeto de aplicativos Microsoft Office específicos, consulte os seguintes tópicos:

- [Visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md)

- [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)

- [Visão geral do modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md)

- [Soluções do InfoPath](../vsto/infopath-solutions.md)

- [Soluções do PowerPoint](../vsto/powerpoint-solutions.md)

- [Soluções de projeto](../vsto/project-solutions.md)

- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)

### <a name="access-a-document-when-the-office-application-starts"></a><a name="AccessingDocuments"></a> Acessar um documento quando o aplicativo do Office for iniciado
 Nem todos os [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] aplicativos abrem automaticamente um documento quando você os inicia, e nenhum dos [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] aplicativos abre um documento quando você os inicia. Portanto, não adicione código no `ThisAdd-In_Startup` manipulador de eventos se o código exigir que um documento seja aberto. Em vez disso, adicione esse código a um evento que o aplicativo do Office gera quando um usuário cria ou abre um documento. Dessa forma, você pode garantir que um documento seja aberto antes que seu código execute operações nele.

 O exemplo de código a seguir funciona com um documento no Word somente quando o usuário cria um documento ou abre um documento existente.

 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_menus.cs/thisaddin.cs" id="Snippet3":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_menus.vb/thisaddin.vb" id="Snippet3":::

### <a name="thisaddin-members-to-use-for-other-tasks"></a>Membros de ThisAddIn a serem usados para outras tarefas
 A tabela a seguir descreve outras tarefas comuns e mostra quais membros da `ThisAddIn` classe você pode usar para executar as tarefas.

|Tarefa|Membro a ser usado|
|----------|-------------------|
|Execute o código para inicializar o suplemento do VSTO quando o suplemento do VSTO for carregado.|Adicione o código ao `ThisAddIn_Startup` método. Esse é o manipulador de eventos padrão para o <xref:Microsoft.Office.Tools.AddInBase.Startup> evento. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).|
|Execute o código para limpar os recursos usados pelo suplemento do VSTO antes que o suplemento do VSTO seja descarregado.|Adicione o código ao `ThisAddIn_Shutdown` método. Esse é o manipulador de eventos padrão para o <xref:Microsoft.Office.Tools.AddInBase.Shutdown> evento. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md). **Observação:**  No Outlook, por padrão, o `ThisAddIn_Shutdown` manipulador de eventos nem sempre é chamado quando o suplemento do VSTO é descarregado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).|
|Exibir um painel de tarefas personalizado.|Use o `CustomTaskPanes` campo. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).|
|Expor objetos em seu suplemento do VSTO para outras soluções de Microsoft Office.|Substitua o método <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A>. Para obter mais informações, consulte [chamar código em suplementos do VSTO de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md).|
|Personalize um recurso no sistema de Microsoft Office implementando uma interface de extensibilidade.|Substitua o <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> método para retornar uma instância de uma classe que implementa a interface. Para obter mais informações, consulte [personalizar recursos da interface do usuário usando interfaces de extensibilidade](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md). **Observação:**  Para personalizar a interface do usuário da faixa de, você também pode substituir o <xref:Microsoft.Office.Tools.AddInBase.CreateRibbonExtensibilityObject%2A> método.|

### <a name="understand-the-design-of-the-thisaddin-class"></a>Entender o design da classe ThisAddIn
 Em projetos direcionados para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] , o <xref:Microsoft.Office.Tools.AddIn> é uma interface. A `ThisAddIn` classe deriva da <xref:Microsoft.Office.Tools.AddInBase> classe. Essa classe base redireciona todas as chamadas para seus membros para uma implementação interna da <xref:Microsoft.Office.Tools.AddIn> interface no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] .

 Em projetos de suplemento do VSTO para Outlook, a `ThisAddIn` classe deriva da `Microsoft.Office.Tools.Outlook.OutlookAddIn` classe em projetos que visam o .NET Framework 3,5 e de <xref:Microsoft.Office.Tools.Outlook.OutlookAddInBase> em projetos que se destinam ao [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] . Essas classes base fornecem algumas funcionalidades adicionais para dar suporte a regiões de formulário. Para obter mais informações sobre regiões de formulário, consulte [criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md).

## <a name="customize-the-user-interface-of-microsoft-office-applications"></a>Personalizar a interface do usuário de aplicativos Microsoft Office
 Você pode personalizar programaticamente a interface do usuário de Microsoft Office aplicativos usando um suplemento do VSTO. Por exemplo, você pode personalizar a faixa de forma, exibir um painel de tarefas personalizado ou criar uma região de formulário personalizada no Outlook. Para obter mais informações, consulte [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).

 O Visual Studio fornece designers e classes que você pode usar para criar painéis de tarefas personalizados, personalizações da faixa de forma e regiões de formulário do Outlook. Esses designers e classes ajudam a simplificar o processo de personalização desses recursos. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md), [Designer de faixa](../vsto/ribbon-designer.md)de formas e [criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md).

 Se você quiser personalizar um desses recursos de uma forma que não seja compatível com as classes e os designers, também poderá personalizar esses recursos implementando uma interface de *extensibilidade* em seu suplemento do VSTO. Para obter mais informações, consulte [personalizar recursos da interface do usuário usando interfaces de extensibilidade](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md).

 Além disso, você pode modificar a interface do usuário de documentos do Word e pastas de trabalho do Excel gerando itens de host que estendem o comportamento de documentos e pastas de trabalho. Isso permite que você adicione controles gerenciados a documentos e planilhas. Para obter mais informações, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

## <a name="call-code-in-vsto-add-ins-from-other-solutions"></a>Chamar código em suplementos do VSTO de outras soluções
 Você pode expor objetos em seu suplemento do VSTO para outras soluções, incluindo outras soluções do Office. Isso será útil se o suplemento do VSTO fornecer um serviço que você deseja permitir que outras soluções usem. Por exemplo, se você tiver um suplemento do VSTO para Microsoft Office Excel que executa cálculos em dados financeiros de um serviço Web, outras soluções poderão executar esses cálculos chamando o suplemento do VSTO do Excel em tempo de execução.

 Para obter mais informações, consulte [chamar código em suplementos do VSTO de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md).

## <a name="see-also"></a>Consulte também
- [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Chamar código em suplementos do VSTO de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)
- [Walkthrough: chamar o código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)
- [Personalizar recursos de interface do usuário usando interfaces de extensibilidade](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)
- [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)
- [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)

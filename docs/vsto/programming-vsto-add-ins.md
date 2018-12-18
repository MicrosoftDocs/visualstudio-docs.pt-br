---
title: Suplementos do VSTO do programa
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 522a3cbac565e217f0b6525fb6288f5b79908a78
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669964"
---
# <a name="program-vsto-add-ins"></a>Suplementos do VSTO do programa
  Quando você estende um aplicativo do Microsoft Office, criando um suplemento do VSTO, você escreve código diretamente no `ThisAddIn` classe em seu projeto. Você pode usar essa classe para executar tarefas como acessar o modelo de objeto do aplicativo host do Microsoft Office, personalizando a interface do usuário (IU) do aplicativo e expor objetos no seu suplemento do VSTO para outras soluções do Office.  
  
 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]  
  
 Alguns aspectos de escrever código em projetos de suplemento do VSTO são diferentes de outros tipos de projetos no Visual Studio. Muitas dessas diferenças são causadas pela maneira como o Office modelos de objeto são expostos ao código gerenciado. Para obter mais informações, consulte [escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md).  
  
 Para obter informações gerais sobre o VSTO Add-ins e outros tipos de soluções que você pode criar usando as ferramentas de desenvolvimento do Office no Visual Studio, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md).  
  
## <a name="use-the-thisaddin-class"></a>Use a classe ThisAddIn  
 Você pode começar a escrever seu código de suplemento do VSTO no `ThisAddIn` classe. Visual Studio gera automaticamente essa classe na *ThisAddIn. vb* (no [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]) ou *ThisAddIn.cs* (em c#) código de arquivo em seu projeto de suplemento do VSTO. O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] automaticamente cria uma instância dessa classe para você quando o aplicativo do Microsoft Office carrega o suplemento do VSTO.  
  
 Há dois manipuladores de eventos padrão no `ThisAddIn` classe. Para executar código quando o suplemento do VSTO é carregado, adicione código para o `ThisAddIn_Startup` manipulador de eventos. Para executar código antes que o suplemento do VSTO é descarregado, adicione código para o `ThisAddIn_Shutdown` manipulador de eventos. Para obter mais informações sobre esses manipuladores de eventos, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).  
  
> [!NOTE]  
>  No Outlook, por padrão o `ThisAddIn_Shutdown` manipulador de eventos não é sempre chamado quando o suplemento do VSTO é descarregado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).  
  
### <a name="access-the-object-model-of-the-host-application"></a>Acessar o modelo de objeto do aplicativo host  
 Para acessar o modelo de objeto do aplicativo host, use o `Application` campo do `ThisAddIn` classe. Esse campo retorna um objeto que representa a instância atual do aplicativo host. A tabela a seguir lista o tipo do valor de retorno para o `Application` campo em cada projeto de suplemento do VSTO.  
  
|Aplicativo de host|Tipo de valor de retorno|  
|----------------------|-----------------------|  
|Microsoft Office Excel|<xref:Microsoft.Office.Interop.Excel.Application>|  
|Microsoft Office InfoPath|<xref:Microsoft.Office.Interop.InfoPath.Application>|  
|Microsoft Office Outlook|<xref:Microsoft.Office.Interop.Outlook.Application>|  
|Microsoft Office PowerPoint|<xref:Microsoft.Office.Interop.PowerPoint.Application>|  
|Microsoft Office Project|Microsoft.Office.Interop.MSProject.Application|  
|Microsoft Office Visio|Microsoft.Office.Interop.Visio.Application|  
|Microsoft Office Word|<xref:Microsoft.Office.Interop.Word.Application>|  
  
 O exemplo de código a seguir mostra como usar o `Application` campo para criar uma nova pasta de trabalho em um suplemento do VSTO para o Microsoft Office Excel. Este exemplo se destina a ser executado a partir de `ThisAddIn` classe.  
  
```vb  
Dim newWorkbook As Excel.Workbook = Me.Application.Workbooks.Add()  
```  
  
```csharp  
Excel.Workbook newWorkbook = this.Application.Workbooks.Add(System.Type.Missing);  
```  
  
 Para fazer a mesma coisa de fora o `ThisAddIn` classe, use o `Globals` do objeto para o acesso a `ThisAddIn` classe. Para obter mais informações sobre o `Globals` do objeto, consulte [Global de acesso a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).  
  
```vb  
Dim newWorkbook As Excel.Workbook = Globals.ThisAddIn.Application.Workbooks.Add()  
```  
  
```csharp  
Excel.Workbook newWorkbook = Globals.ThisAddIn.Application.Workbooks.Add(System.Type.Missing);  
```  
  
 Para obter mais informações sobre os modelos de objeto de aplicativos específicos do Microsoft Office, consulte os tópicos a seguir:  
  
-   [Visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md)  
  
-   [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)  
  
-   [Visão geral de modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md)  
  
-   [Soluções InfoPath](../vsto/infopath-solutions.md)  
  
-   [Soluções PowerPoint](../vsto/powerpoint-solutions.md)  
  
-   [Soluções de projeto](../vsto/project-solutions.md)  
  
-   [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)  
  
###  <a name="AccessingDocuments"></a> Acessar um documento quando inicia o aplicativo do Office  
 Nem todos os [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] aplicativos de abrem um documento automaticamente quando você inicia e nenhum do [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] aplicativos abrem um documento quando você iniciá-los. Portanto, não adicione o código no `ThisAdd-In_Startup` se um documento a ser aberto exige que o código de manipulador de eventos. Em vez disso, adicione esse código para um evento que o aplicativo do Office emite quando um usuário cria ou abre um documento. Dessa forma, você pode garantir que um documento está aberto antes de seu código executa operações nela.  
  
 O exemplo de código a seguir funciona com um documento do Word, somente quando o usuário cria um documento ou abrir um documento existente.  
  
 [!code-csharp[Trin_WordAddIn_Menus#3](../vsto/codesnippet/CSharp/trin_wordaddin_menus.cs/thisaddin.cs#3)]
 [!code-vb[Trin_WordAddIn_Menus#3](../vsto/codesnippet/VisualBasic/trin_wordaddin_menus.vb/thisaddin.vb#3)]  
  
### <a name="thisaddin-members-to-use-for-other-tasks"></a>Membros ThisAddIn a ser usado para outras tarefas  
 A tabela a seguir descreve outras tarefas comuns e mostra quais membros do `ThisAddIn` classe você pode usar para executar as tarefas.  
  
|Tarefa|Membro a ser usado|  
|----------|-------------------|  
|Execute o código para inicializar o suplemento do VSTO, quando o suplemento do VSTO é carregado.|Adicione código para o `ThisAddIn_Startup` método. Isso é o manipulador de eventos padrão para o <xref:Microsoft.Office.Tools.AddInBase.Startup> eventos. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).|  
|Execute o código para limpar os recursos usados pelo suplemento do VSTO antes que o suplemento do VSTO é descarregado.|Adicione código para o `ThisAddIn_Shutdown` método. Isso é o manipulador de eventos padrão para o <xref:Microsoft.Office.Tools.AddInBase.Shutdown> eventos. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md). **Observação:** no Outlook, por padrão o `ThisAddIn_Startup` manipulador de eventos não é sempre chamado quando o suplemento do VSTO é descarregado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).|  
|Exiba um painel de tarefas personalizado.|Use o `CustomTaskPanes` campo. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).|  
|Expor objetos no seu suplemento do VSTO para outras soluções do Microsoft Office.|Substituir o método <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A>. Para obter mais informações, consulte [chamar o código no VSTO Add-ins de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md).|  
|Personalize um recurso no Microsoft Office system com a implementação de uma interface de extensibilidade.|Substituir o <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> método para retornar uma instância de uma classe que implementa a interface. Para obter mais informações, consulte [recursos de interface do usuário personalizar usando interfaces de extensibilidade](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md). **Observação:** para personalizar a interface do usuário da faixa de opções, você também pode substituir o <xref:Microsoft.Office.Tools.AddInBase.CreateRibbonExtensibilityObject%2A> método.|  
  
### <a name="understand-the-design-of-the-thisaddin-class"></a>Entender o design da classe ThisAddIn  
 Em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)], <xref:Microsoft.Office.Tools.AddIn> é uma interface. O `ThisAddIn` classe deriva de <xref:Microsoft.Office.Tools.AddInBase> classe. Essa classe base redireciona todas as chamadas para seus membros para uma implementação interna do <xref:Microsoft.Office.Tools.AddIn> da interface no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)].  
  
 Em projetos de suplemento do VSTO para Outlook, o `ThisAddIn` classe deriva a `Microsoft.Office.Tools.Outlook.OutlookAddIn` classe nos projetos direcionados ao .NET Framework 3.5 e de <xref:Microsoft.Office.Tools.Outlook.OutlookAddInBase> em projetos que segmentam o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]. Essas classes base fornecem algumas funcionalidades adicionais para dar suporte a regiões do formulário. Para obter mais informações sobre regiões de formulário, consulte [regiões de formulário do Outlook criar](../vsto/creating-outlook-form-regions.md).  
  
## <a name="customize-the-user-interface-of-microsoft-office-applications"></a>Personalizar a interface do usuário de aplicativos do Microsoft Office  
 Programaticamente, você pode personalizar os aplicativos de interface do usuário do Microsoft Office usando um suplemento do VSTO. Por exemplo, pode personalizar a faixa de opções, exibir um painel de tarefas personalizado ou criar uma região de formulário personalizada no Outlook. Para obter mais informações, consulte [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).  
  
 Visual Studio oferece designers e as classes que você pode usar para criar painéis de tarefas personalizados, personalizações da faixa de opções e regiões de formulário do Outlook. Essas classes e os designers de ajudam a simplificar o processo de personalização desses recursos. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md), [Designer de faixa de opções](../vsto/ribbon-designer.md), e [regiões de formulário do Outlook criar](../vsto/creating-outlook-form-regions.md).  
  
 Se você desejar personalizar um desses recursos de forma que não é compatível com as classes e os designers, você também pode personalizar esses recursos implementando uma *interface de extensibilidade* no seu suplemento do VSTO. Para obter mais informações, consulte [recursos de interface do usuário personalizar usando interfaces de extensibilidade](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md).  
  
 Além disso, você pode modificar da interface do usuário de documentos do Word e pastas de trabalho do Excel por gerar itens de host que estendem o comportamento de documentos e pastas de trabalho. Isso permite que você adicione controles gerenciados a documentos e planilhas. Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
## <a name="call-code-in-vsto-add-ins-from-other-solutions"></a>Chamar o código no VSTO Add-ins de outras soluções  
 Você pode expor os objetos no seu suplemento do VSTO para outras soluções, incluindo outras soluções do Office. Isso é útil se o suplemento do VSTO fornece um serviço que você deseja habilitar usar outras soluções. Por exemplo, se você tiver um suplemento do VSTO para o Microsoft Office Excel que executa cálculos nos dados financeiros de um serviço web, outras soluções podem executar esses cálculos chamando o suplemento do VSTO do Excel em tempo de execução.  
  
 Para obter mais informações, consulte [chamar o código no VSTO Add-ins de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)   
 [Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)   
 [Chamar o código no VSTO Add-ins de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)   
 [Passo a passo: Chamar o código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)   
 [Personalizar os recursos de interface do usuário usando interfaces de extensibilidade](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)   
 [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)  
  
  
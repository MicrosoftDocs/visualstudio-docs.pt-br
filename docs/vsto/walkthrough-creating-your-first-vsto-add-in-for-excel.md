---
title: 'Passo a passo: Criar seu primeiro suplemento VSTO para Excel'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- add-ins [Office development in Visual Studio], creating your first project
- Excel [Office development in Visual Studio], creating your first project
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6a9b7540a42dbaf7b7079793158d33d761199720
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949897"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-excel"></a>Passo a passo: Criar seu primeiro suplemento VSTO para Excel
  Este passo a passo introdutório mostra como criar um suplemento em nível de aplicativo do Microsoft Office Excel. Os recursos que você criar nesse tipo de solução estão disponíveis para o aplicativo em si, independentemente de qual pastas de trabalho estão abertas.  
  
 [!INCLUDE[appliesto_xlallapp](../vsto/includes/appliesto-xlallapp-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Criando um projeto de suplemento do VSTO do Excel para o Excel.  
  
- Escrevendo código que usa o modelo de objeto do Excel para adicionar texto a uma pasta de trabalho quando ele é salvo.  
  
- Criando e executando o projeto para testá-lo.  
  
- Limpando o projeto concluído para que o suplemento do VSTO não seja executado automaticamente em seu computador de desenvolvimento.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].  
  
## <a name="create-the-project"></a>Criar o projeto  
  
#### <a name="to-create-a-new-excel-vsto-add-in-project-in-visual-studio"></a>Para criar um novo projeto de suplemento do VSTO do Excel no Visual Studio  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
3.  No painel de modelos, expanda **Visual c#** ou **Visual Basic**e, em seguida, expanda **Office/SharePoint**.  
  
4.  Sob o expandida **Office/SharePoint** nó, selecione o **suplementos do Office** nó.  
  
5.  Na lista de modelos de projeto, selecione **suplemento do Excel 2010** ou **suplemento do Excel 2013**.  
  
6.  No **nome** , digite **FirstExcelAddIn**.  
  
7.  Clique em **OK**.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o **FirstExcelAddIn** do projeto e abre o arquivo de código ThisAddIn no editor.  
  
## <a name="write-code-to-add-text-to-the-saved-workbook"></a>Escrever código para adicionar texto à pasta de trabalho salva  
 Em seguida, adicione código ao arquivo de código ThisAddIn. O novo código usa o modelo de objeto do Excel para inserir texto clichê na primeira linha da planilha ativa. A planilha ativa é a planilha que está aberta quando o usuário salva a pasta de trabalho. Por padrão, o arquivo de código ThisAddIn contém o seguinte código gerado:  
  
-   Uma definição parcial do `ThisAddIn` classe. Essa classe fornece um ponto de entrada para seu código e fornece acesso ao modelo de objeto do Excel. Para obter mais informações, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md). O restante do `ThisAddIn` classe é definida em um arquivo de código oculto que você não deve modificar.  
  
-   O `ThisAddIn_Startup` e `ThisAddIn_Shutdown` manipuladores de eventos. Esses manipuladores de eventos são chamados quando o Excel carrega e descarrega o suplemento do VSTO. Use esses manipuladores de eventos para inicializar o suplemento do VSTO quando ele for carregado e para limpar os recursos usados pelo seu suplemento quando ele é descarregado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).  
  
### <a name="to-add-a-line-of-text-to-the-saved-workbook"></a>Para adicionar uma linha de texto para a pasta de trabalho salva  
  
1. No arquivo de código ThisAddIn, adicione o seguinte código para o `ThisAddIn` classe. O novo código define um manipulador de eventos para o <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> evento, que é gerado quando uma pasta de trabalho é salvo.  
  
    Quando o usuário salva uma pasta de trabalho, o manipulador de eventos adiciona o novo texto no início da planilha ativa.  
  
    [!code-vb[Trin_ExcelAddInTutorial#1](../vsto/codesnippet/VisualBasic/Trin_ExcelAddInTutorial/ThisAddIn.vb#1)]
    [!code-csharp[Trin_ExcelAddInTutorial#1](../vsto/codesnippet/CSharp/Trin_ExcelAddInTutorial/ThisAddIn.cs#1)]  
  
2. Se você estiver usando c#, adicione o seguinte código necessário para o `ThisAddIn_Startup` manipulador de eventos. Esse código é usado para se conectar a `Application_WorkbookBeforeSave` manipulador de eventos com o <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> eventos.  
  
    [!code-csharp[Trin_ExcelAddInTutorial#2](../vsto/codesnippet/CSharp/Trin_ExcelAddInTutorial/ThisAddIn.cs#2)]  
  
   Para modificar a pasta de trabalho quando ele for salvo, os exemplos de código anterior usam os seguintes objetos:  
  
-   O `Application` campo do `ThisAddIn` classe. O `Application` campo retorna um <xref:Microsoft.Office.Interop.Excel.Application> objeto que representa a instância atual do Excel.  
  
-   O `Wb` parâmetro do manipulador de eventos para o <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> eventos. O `Wb` parâmetro é um <xref:Microsoft.Office.Interop.Excel.Workbook> objeto que representa a pasta de trabalho salva. Para obter mais informações, consulte [visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md).  
  
## <a name="test-the-project"></a>O projeto de teste  
  
### <a name="to-test-the-project"></a>Para testar o projeto  
  
1.  Pressione **F5** para compilar e executar seu projeto.  
  
     Quando você compila o projeto, o código é compilado em um assembly que está incluído na pasta de saída de compilação para o projeto. Visual Studio também cria um conjunto de entradas do registro que permitem que o Excel descobrir e carregar o suplemento do VSTO e ela define as configurações de segurança no computador de desenvolvimento para habilitar o suplemento do VSTO ser executado. Para obter mais informações, consulte [soluções do Office compilar](../vsto/building-office-solutions.md).  
  
2.  No Excel, salve a pasta de trabalho.  
  
3.  Verifique se o texto a seguir é adicionado à pasta de trabalho.  
  
     **Este texto foi adicionado por meio de código.**  
  
4.  Feche o Excel.  
  
## <a name="clean-up-the-project"></a>Limpar o projeto  
 Quando você concluir o desenvolvimento de um projeto, remova o suplemento do VSTO assembly, as entradas do registro e as configurações de segurança de seu computador de desenvolvimento. Caso contrário, o suplemento do VSTO continuará a executar toda vez que você abrir o Excel em seu computador de desenvolvimento.  
  
### <a name="to-clean-up-the-completed-project-on-your-development-computer"></a>Para limpar o projeto concluído no computador de desenvolvimento  
  
1.  No Visual Studio, sobre o **construir** menu, clique em **limpar solução**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Agora que você criou um básico suplemento VSTO para Excel, você pode aprender mais sobre como desenvolver suplementos do VSTO nesses tópicos:  
  
-   Tarefas gerais de programação que você pode executar nos suplementos do VSTO: [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
-   Tarefas de programação que são específicas para suplementos do VSTO do Excel: [soluções do Excel](../vsto/excel-solutions.md).  
  
-   Usando o modelo de objeto do Excel: [visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md).  
  
-   Personalizando a interface do usuário (IU) do Excel, por exemplo, pela adição de uma guia personalizada à faixa de opções ou criando seu próprio painel de tarefas personalizado: [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).  
  
-   Compilação e depuração de suplementos do VSTO para Excel: [soluções do Office compilar](../vsto/building-office-solutions.md).  
  
-   Implantação de suplementos do VSTO para Excel: [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)   
 [Soluções do Excel](../vsto/excel-solutions.md)   
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md)   
 [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)   
 [Compilar soluções do Office](../vsto/building-office-solutions.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)   
 [Visão geral de modelos de projeto do Office](../vsto/office-project-templates-overview.md)  
  
  
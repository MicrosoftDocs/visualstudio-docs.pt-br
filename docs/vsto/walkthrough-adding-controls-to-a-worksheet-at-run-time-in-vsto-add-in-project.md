---
title: 'Passo a passo: Adicionar controles a uma planilha em tempo de execução no projeto de suplemento do VSTO'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], adding controls
- controls [Office development in Visual Studio], adding to worksheets at run time
- application-level add-ins [Office development in Visual Studio], adding controls
- worksheets, adding controls at run time
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b3671b00ecad0380dd38e770beeef703fa916fac
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49915692"
---
# <a name="walkthrough-add-controls-to-a-worksheet-at-runtime-in-vsto-add-in-project"></a>Passo a passo: Adicionar controles a uma planilha em tempo de execução no projeto de suplemento do VSTO
  Você pode adicionar controles para qualquer planilha aberta usando um suplemento do VSTO do Excel. Este passo a passo demonstra como usar a faixa de opções para permitir que os usuários adicionar um <xref:Microsoft.Office.Tools.Excel.Controls.Button>, um <xref:Microsoft.Office.Tools.Excel.NamedRange>e um <xref:Microsoft.Office.Tools.Excel.ListObject> para uma planilha. Para obter informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
 **Aplica-se a:** as informações neste tópico se aplicam a projetos de suplemento do VSTO para Excel. Para obter mais informações, confira [Features Available by Office Application and Project Type](../vsto/features-available-by-office-application-and-project-type.md) (Funcionalidades disponibilizadas pelo aplicativo do Office e pelo tipo de projeto).  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Fornecendo uma interface do usuário (IU) para adicionar controles à planilha.  
  
- Adicionando controles à planilha.  
  
- Remover controles de planilha.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Excel  
  
## <a name="create-a-new-excel-vsto-add-in-project"></a>Criar um novo projeto de suplemento do VSTO do Excel  
 Comece criando um projeto de suplemento do VSTO do Excel.  
  
### <a name="to-create-a-new-excel-vsto-add-in-project"></a>Para criar um novo projeto de suplemento do VSTO do Excel  
  
1.  Na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], crie um projeto de suplemento do VSTO do Excel com o nome **ExcelDynamicControls**. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
2.  Adicione uma referência para o **Microsoft.Office.Tools.Excel.v4.0.Utilities.dll** assembly. Essa referência é necessário adicionar programaticamente um controle dos Windows Forms a uma planilha posteriormente neste passo a passo.  
  
## <a name="provide-a-ui-to-add-controls-to-a-worksheet"></a>Fornecer uma interface do usuário para adicionar controles a uma planilha  
 Adicione uma guia personalizada à faixa de opções do Excel. Os usuários podem selecionar as caixas de seleção na guia para adicionar controles a uma planilha.  
  
#### <a name="to-provide-a-ui-to-add-controls-to-a-worksheet"></a>Para fornecer uma interface do usuário para adicionar controles a uma planilha  
  
1.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo, selecione **faixa de opções (Visual Designer)** e, em seguida, clique em **adicionar**.  
  
     Um arquivo chamado **Ribbon1.cs** ou **Ribbon1.vb** abre no Designer de faixa de opções e exibe um guia padrão e um grupo.  
  
3.  Do **controles de faixa de opções do Office** guia da **caixa de ferramentas**, arraste um controle caixa de seleção **group1**.  
  
4.  Clique em **CheckBox1** para selecioná-lo.  
  
5.  No **propriedades** janela, altere as propriedades a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**Button**|  
    |**Rótulo**|**Button**|  
  
6.  Adicionar uma segunda caixa de seleção para **group1**e, em seguida, altere as propriedades a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**NamedRange**|  
    |**Rótulo**|**NamedRange**|  
  
7.  Adicionar uma terceira caixa de seleção para **group1**e, em seguida, altere as propriedades a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**ListObject**|  
    |**Rótulo**|**ListObject**|  
  
## <a name="add-controls-to-the-worksheet"></a>Adicionar controles à planilha  
 Controles gerenciados só podem ser adicionados aos itens de host, que atuam como contêineres. Como projetos de suplemento do VSTO funcionam com qualquer pasta de trabalho, o suplemento do VSTO converte a planilha em um item de host ou obtém um item de host existente, antes de adicionar o controle. Adicione código para os manipuladores de eventos de clique de cada controle para gerar um <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host que se baseia na planilha de abrir. Em seguida, adicione uma <xref:Microsoft.Office.Tools.Excel.Controls.Button>, um <xref:Microsoft.Office.Tools.Excel.NamedRange>e um <xref:Microsoft.Office.Tools.Excel.ListObject> na seleção atual na planilha.  
  
### <a name="to-add-controls-to-a-worksheet"></a>Para adicionar controles a uma planilha  
  
1.  No Designer de faixa de opções, clique duas vezes **botão**.  
  
     O <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> manipulador de eventos do **botão** caixa de seleção é aberto no Editor de códigos.  
  
2.  Substitua o `Button_Click` manipulador de eventos com o código a seguir.  
  
     Esse código usa o `GetVstoObject` método para obter um item de host que representa a primeira planilha na pasta de trabalho e, em seguida, adiciona um <xref:Microsoft.Office.Tools.Excel.Controls.Button> controle para a célula selecionada atualmente.  
  
     [!code-csharp[Trin_Excel_Dynamic_Controls#2](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#2)]
     [!code-vb[Trin_Excel_Dynamic_Controls#2](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#2)]  
  
3.  Na **Gerenciador de soluções**, selecione *Ribbon1.cs* ou *Ribbon1.vb*.  
  
4.  Sobre o **modo de exibição** menu, clique em **Designer**.  
  
5.  No Designer de faixa de opções, clique duas vezes **NamedRange**.  
  
6.  Substitua o `NamedRange_Click` manipulador de eventos com o código a seguir.  
  
     Esse código usa o `GetVstoObject` método para obter um item de host que representa a primeira planilha na pasta de trabalho e, em seguida, define um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle para a célula selecionada no momento ou células.  
  
     [!code-csharp[Trin_Excel_Dynamic_Controls#3](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#3)]
     [!code-vb[Trin_Excel_Dynamic_Controls#3](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#3)]  
  
7.  No Designer de faixa de opções, clique duas vezes **ListObject**.  
  
8.  Substitua o `ListObject_Click` manipulador de eventos com o código a seguir.  
  
     Esse código usa o `GetVstoObject` método para obter um item de host que representa a primeira planilha na pasta de trabalho e, em seguida, define um <xref:Microsoft.Office.Tools.Excel.ListObject> para a célula selecionada no momento ou células.  
  
     [!code-csharp[Trin_Excel_Dynamic_Controls#4](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#4)]
     [!code-vb[Trin_Excel_Dynamic_Controls#4](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#4)]  
  
9. Adicione as seguintes instruções à parte superior do arquivo de código da faixa de opções.  
  
     [!code-csharp[Trin_Excel_Dynamic_Controls#1](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs#1)]
     [!code-vb[Trin_Excel_Dynamic_Controls#1](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb#1)]  
  
## <a name="remove-controls-from-the-worksheet"></a>Remova os controles de planilha  
 Controles não são persistidos quando a planilha for salvo e fechada. Programaticamente, você deve remover todos os controles de Windows Forms gerados antes que a planilha é salva ou uma estrutura de tópicos do controle será exibido quando a pasta de trabalho é aberta novamente. Adicione código para o <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> evento que remove os controles de formulários do Windows da coleção de controles de item de host gerados. Para obter mais informações, consulte [persistir controles dinâmicos em documentos do Office](../vsto/persisting-dynamic-controls-in-office-documents.md).  
  
### <a name="to-remove-controls-from-the-worksheet"></a>Para remover os controles de planilha  
  
1.  Na **Gerenciador de soluções**, selecione *ThisAddIn.cs* ou *ThisAddIn. vb*.  
  
2.  Sobre o **modo de exibição** menu, clique em **código**.  
  
3.  Adicione o seguinte método à classe `ThisAddIn`. Esse código obtém a primeira planilha na pasta de trabalho e, em seguida, usa o `HasVstoObject` método para verificar se a planilha tem um objeto de planilha gerado. Se o objeto de planilha gerado tem controles, o código obtém esse objeto de planilha e itera através da coleção de controle, removendo os controles.  
  
     [!code-csharp[Trin_Excel_Dynamic_Controls#6](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#6)]
     [!code-vb[Trin_Excel_Dynamic_Controls#6](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#6)]  
  
4.  No c#, você deve criar um manipulador de eventos para o <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> eventos. Você pode colocar esse código no `ThisAddIn_Startup` método. Para obter mais informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md). Substitua o `ThisAddIn_Startup` método com o código a seguir.  
  
     [!code-csharp[Trin_Excel_Dynamic_Controls#5](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#5)]  
  
## <a name="test-the-solution"></a>Testar a solução  
 Adicione controles a uma planilha selecionando-os em uma guia personalizada na faixa de opções. Quando você salvar a planilha, esses controles são removidos.  
  
### <a name="to-test-the-solution"></a>Para testar a solução.  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Selecione qualquer célula em Sheet1.  
  
3.  Clique o **Add-Ins** guia.  
  
4.  No **group1** , clique em **botão**.  
  
     Um botão aparece na célula selecionada.  
  
5.  Selecione uma célula diferente em Sheet1.  
  
6.  No **group1** , clique em **NamedRange**.  
  
     Um intervalo nomeado é definido para a célula selecionada.  
  
7.  Selecione uma série de células em Sheet1.  
  
8.  No **group1** , clique em **ListObject**.  
  
     Um objeto de lista é adicionado para as células selecionadas.  
  
9. Salve a planilha.  
  
     Os controles que você adicionou ao Sheet1 não aparecem.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre os controles em projetos de suplemento do VSTO do Excel deste tópico:  
  
-   Para saber mais sobre como salvar os controles em uma planilha, consulte o VSTO do Excel Add-in dinâmico Controls Sample em [exemplos de desenvolvimento do Office e instruções passo a passo](../vsto/office-development-samples-and-walkthroughs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Soluções do Excel](../vsto/excel-solutions.md)   
 [Windows forms a controles em Visão geral de documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md)   
 [Controles em documentos do Office](../vsto/controls-on-office-documents.md)   
 [Controle NamedRange](../vsto/namedrange-control.md)   
 [Controle ListObject](../vsto/listobject-control.md)  
  
  
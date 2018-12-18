---
title: 'Passo a passo: Alterar a formatação da planilha usando controles CheckBox'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, changing formatting using managed controls
- worksheets, check box controls
- controls [Office development in Visual Studio], adding to worksheets
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: fae4a6cc21264e62c5a12db79c8a937f0a366314
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49843529"
---
# <a name="walkthrough-change-worksheet-formatting-using-checkbox-controls"></a>Passo a passo: Alterar a formatação da planilha usando controles CheckBox
  Este passo a passo mostra as Noções básicas de como usar caixas de seleção em uma planilha do Microsoft Office Excel para alterar a formatação. Você usará as ferramentas de desenvolvimento do Office no Visual Studio para criar e adicionar código ao seu projeto. Para ver o resultado como um exemplo completo, consulte o exemplo de controles do Excel em [exemplos de desenvolvimento do Office e instruções passo a passo](../vsto/office-development-samples-and-walkthroughs.md).  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 Durante este passo a passo, você aprenderá a:  
  
-   Adicione texto e controles a uma planilha.  
  
-   Formate o texto quando uma opção é selecionada.  
  
-   Teste seu projeto.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].  
  
## <a name="create-the-project"></a>Criar o projeto  
 Nesta etapa, você criará um projeto de pasta de trabalho do Excel usando o Visual Studio.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de pasta de trabalho do Excel com o nome **formatação do Excel meu**. Certifique-se de que **criar um novo documento** está selecionado. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o **formatação do Excel Meus** projeto ao **Gerenciador de soluções**.  
  
## <a name="add-text-and-controls-to-the-worksheet"></a>Adicionar texto e controles à planilha  
 Para este passo a passo, você precisará de três <xref:Microsoft.Office.Tools.Excel.Controls.CheckBox> controles e texto em um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle.  
  
### <a name="to-add-three-check-boxes"></a>Para adicionar três caixas de seleção  
  
1.  Verifique se a pasta de trabalho é aberta no designer do Visual Studio e que `Sheet1` está aberto.  
  
2.  Do **controles comuns** guia da **caixa de ferramentas**, arraste uma <xref:Microsoft.Office.Tools.Excel.Controls.CheckBox> controle para ou perto de célula **B2** na **Sheet1**.  
  
3.  Dos **modo de exibição** menu, selecione **propriedades** janela.  
  
4.  Certifique-se de que **Checkbox1** está visível na caixa de listagem nome do objeto da **propriedades** janela e altere as propriedades a seguir:  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**applyBoldFont**|  
    |**Texto**|**Negrito**|  
  
5.  Arraste uma segunda caixa de seleção em ou próximo da célula **B4** e alterar as propriedades a seguir:  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**applyItalicFont**|  
    |**Texto**|**Itálico**|  
  
6.  Arraste uma terceira caixa de seleção em ou próximo da célula **B6** e alterar as propriedades a seguir:  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**applyUnderlineFont**|  
    |**Texto**|**Sublinhado**|  
  
7.  Selecione todos os controles de caixa de seleção de três ao mesmo tempo mantendo a **Ctrl** chave.  
  
8.  No grupo Organizar da guia formato no Excel, clique em **alinhar**e, em seguida, clique em **Alinhar à esquerda**.  
  
     Os caixa de seleção de três controles são alinhados à esquerda, na posição do primeiro controle selecionado.  
  
     Em seguida, arrastará um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle à planilha.  
  
    > [!NOTE]  
    >  Você também pode adicionar o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle digitando **textFont** para o **nome** caixa.  
  
#### <a name="to-add-text-to-a-namedrange-control"></a>Para adicionar texto a um controle NamedRange  
  
1. Dos **controles do Excel** guia de ferramentas, arraste um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle a célula **B9**.  
  
2. Verifique **$B$ 9** aparece na caixa de texto editável e que a célula **B9** está selecionado. Se não estiver, clique na célula **B9** para selecioná-lo.  
  
3. Clique em **OK**.  
  
4. Célula **B9** torna-se um intervalo nomeado `NamedRange1`.  
  
    Não há nenhuma indicação visível na planilha, mas `NamedRange1` aparece na **caixa nome** (logo acima a planilha no lado esquerdo) quando a célula **B9** está selecionado.  
  
5. Certifique-se de que **NamedRange1** está visível na caixa de listagem nome do objeto da **propriedades** janela e altere as propriedades a seguir:  
  
   |Propriedade|Valor|  
   |--------------|-----------|  
   |**Nome**|**textFont**|  
   |**Value2**|**Clique em uma caixa de seleção para alterar a formatação deste texto.**|  
  
   Em seguida, escreva o código para formatar o texto quando uma opção é selecionada.  
  
## <a name="format-the-text-when-an-option-is-selected"></a>Formatar o texto quando uma opção é selecionada.  
 Nesta seção, você escreverá código para que quando o usuário seleciona uma opção de formatação, o formato do texto na planilha é alterado.  
  
### <a name="to-change-formatting-when-a-check-box-is-selected"></a>Para alterar a formatação quando uma caixa de seleção está selecionada  
  
1.  Clique com botão direito **Sheet1**e, em seguida, clique em **Exibir código** no menu de atalho.  
  
2.  Adicione o seguinte código para o <xref:System.Windows.Forms.Control.Click> manipulador de eventos do `applyBoldFont` caixa de seleção:  
  
     [!code-vb[Trin_VstcoreProgrammingControlsExcel#7](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#7)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#7](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#7)]  
  
3.  Adicione o seguinte código para o <xref:System.Windows.Forms.Control.Click> manipulador de eventos do `applyItalicFont` caixa de seleção:  
  
     [!code-vb[Trin_VstcoreProgrammingControlsExcel#8](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#8)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#8](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#8)]  
  
4.  Adicione o seguinte código para o <xref:System.Windows.Forms.Control.Click> manipulador de eventos do `applyUnderlineFont` caixa de seleção:  
  
     [!code-vb[Trin_VstcoreProgrammingControlsExcel#9](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#9)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#9](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#9)]  
  
5.  No c#, você deve adicionar manipuladores de eventos para as caixas de seleção para o <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> evento, conforme mostrado abaixo. Para obter informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  
  
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#10)]  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Agora você pode testar sua pasta de trabalho para certificar-se de que o texto está formatado corretamente quando você marca ou desmarca uma caixa de seleção.  
  
### <a name="to-test-your-workbook"></a>Para testar a sua pasta de trabalho  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Marque ou desmarque uma caixa de seleção.  
  
3.  Confirme que o texto está formatado corretamente.  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo mostra as Noções básicas do uso de caixas de seleção e formatação de texto em planilhas do Excel. Estas são algumas tarefas que podem vir a seguir:  
  
-   Implantar o projeto. Para obter mais informações, consulte [implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).  
-   Usar um botão para preencher uma caixa de texto. Para obter mais informações, consulte [instruções passo a passo: exibir texto em uma caixa de texto em uma planilha usando um botão](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo usando o Excel](../vsto/walkthroughs-using-excel.md)   
 [Controle NamedRange](../vsto/namedrange-control.md)   
 [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)  
  
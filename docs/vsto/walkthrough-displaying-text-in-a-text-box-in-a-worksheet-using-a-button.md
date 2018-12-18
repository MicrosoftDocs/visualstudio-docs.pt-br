---
title: 'Passo a passo: Exibir texto em uma caixa de texto em uma planilha usando um botão'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text [Office development in Visual Studio], displaying worksheets
- worksheets, displaying text
- text boxes, displaying text in worksheets
- text [Office development in Visual Studio], text boxes
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 25294e9cb8f57036603ec4817fcbd59976a358a3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49840279"
---
# <a name="walkthrough-display-text-in-a-text-box-in-a-worksheet-using-a-button"></a>Passo a passo: Exibir texto em uma caixa de texto em uma planilha usando um botão
  Este passo a passo mostra as Noções básicas de como usar os botões e caixas de texto em planilhas do Microsoft Office Excel e como criar projetos do Excel usando ferramentas de desenvolvimento do Office no Visual Studio. Para ver o resultado como um exemplo completo, consulte o exemplo de controles do Excel em [exemplos de desenvolvimento do Office e instruções passo a passo](../vsto/office-development-samples-and-walkthroughs.md).  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 Durante este passo a passo, você aprenderá a:  
  
-   Adicione controles a uma planilha.  
  
-   Preencha uma caixa de texto quando um botão é clicado.  
  
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
  
1.  Criar um projeto de pasta de trabalho do Excel com o nome **My Button Excel**. Certifique-se de que **criar um novo documento** está selecionado. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o **meu botão do Excel** projeto ao **Gerenciador de soluções**.  
  
## <a name="add-controls-to-the-worksheet"></a>Adicionar controles à planilha  
 Para este passo a passo, você precisará de um botão e uma caixa de texto na primeira planilha.  
  
### <a name="to-add-a-button-and-a-text-box"></a>Para adicionar um botão e uma caixa de texto  
  
1. Verificar se o **Button.xlsx de Excel Meus** pasta de trabalho é aberta no designer do Visual Studio, com `Sheet1` exibido.  
  
2. Dos **controles comuns** guia de ferramentas, arraste um <xref:Microsoft.Office.Tools.Excel.Controls.TextBox> para `Sheet1`.  
  
3. Dos **modo de exibição** menu, selecione **janela propriedades**.  
  
4. Certifique-se de que **TextBox1** está visível na **propriedades** caixa de lista suspensa da janela e altere a **nome** propriedade da caixa de texto para **displayText**.  
  
5. Arraste uma **botão** controle para `Sheet1` e altere as propriedades a seguir:  
  
   |Propriedade|Valor|  
   |--------------|-----------|  
   |**Nome**|**insertText**|  
   |**Texto**|**Inserir texto**|  
  
   Agora escreva o código para ser executado quando o botão é clicado.  
  
## <a name="populate-the-text-box-when-the-button-is-clicked"></a>Preencha a caixa de texto quando o botão é clicado  
 Cada vez que o usuário clica no botão, **Olá, mundo!** é acrescentado à caixa de texto.  
  
### <a name="to-write-to-the-text-box-when-the-button-is-clicked"></a>Para gravar a caixa de texto quando o botão é clicado  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **Sheet1**e, em seguida, clique em **Exibir código** no menu de atalho.  
  
2.  Adicione o seguinte código para o <xref:System.Windows.Forms.Control.Click> manipulador de eventos do botão:  
  
     [!code-vb[Trin_VstcoreProgrammingControlsExcel#11](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#11)]
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#11](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#11)]  
  
3.  No c#, você deve adicionar um manipulador de eventos para o <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> evento, conforme mostrado abaixo. Para obter informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  
  
     [!code-csharp[Trin_VstcoreProgrammingControlsExcel#12](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#12)]  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Agora você pode testar sua pasta de trabalho para certificar-se de que a mensagem **Olá, mundo!** é exibida na caixa de texto quando você clica no botão.  
  
### <a name="to-test-your-workbook"></a>Para testar a sua pasta de trabalho  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Clique no botão.  
  
3.  Confirme se **Olá, mundo!** é exibida na caixa de texto.  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo mostra as Noções básicas de como usar os botões e caixas de texto em planilhas do Excel. Estas são algumas tarefas que podem vir a seguir:  
  
-   Implantar o projeto. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  
  
-   Usando as caixas de seleção para alterar a formatação. Para obter mais informações, consulte [instruções passo a passo: formatação de planilha de alteração usando controles CheckBox](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como: adicionar controles dos Windows Forms a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)   
 [Instruções passo a passo usando o Excel](../vsto/walkthroughs-using-excel.md)   
 [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)  
  
  
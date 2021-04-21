---
title: Alterar a formatação da planilha usando controles de caixa de seleção
description: Saiba como você pode usar as ferramentas de desenvolvimento do Office no Visual Studio para criar e adicionar código ao seu projeto.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, changing formatting using managed controls
- worksheets, check box controls
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6f649fad99b8d94cc650ecda57e10b423b14194e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826428"
---
# <a name="walkthrough-change-worksheet-formatting-using-checkbox-controls"></a>Walkthrough: alterar a formatação da planilha usando controles CheckBox
  Este tutorial mostra as noções básicas do uso de caixas de seleção em uma Microsoft Office planilha do Excel para alterar a formatação. Você usará as ferramentas de desenvolvimento do Office no Visual Studio para criar e adicionar código ao seu projeto. Para ver o resultado como um exemplo completo, consulte o exemplo de controles do Excel em [exemplos de desenvolvimento do Office e passo a passos](../vsto/office-development-samples-and-walkthroughs.md).

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Durante este passo a passo, você aprenderá a:

- Adicionar texto e controles a uma planilha.

- Formate o texto quando uma opção for selecionada.

- Teste seu projeto.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

## <a name="create-the-project"></a>Criar o projeto
 Nesta etapa, você criará um projeto de pasta de trabalho do Excel usando o Visual Studio.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de pasta de trabalho do Excel com o nome **minha formatação do Excel**. Verifique se **a seleção criar um novo documento** está selecionada. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o projeto de **formatação meu Excel** a **Gerenciador de soluções**.

## <a name="add-text-and-controls-to-the-worksheet"></a>Adicionar texto e controles à planilha
 Para esta explicação, você precisará de três <xref:Microsoft.Office.Tools.Excel.Controls.CheckBox> controles e algum texto em um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle.

### <a name="to-add-three-check-boxes"></a>Para adicionar três caixas de seleção

1. Verifique se a pasta de trabalho está aberta no designer do Visual Studio e se `Sheet1` está aberta.

2. Na guia **controles comuns** da caixa de **ferramentas**, arraste um <xref:Microsoft.Office.Tools.Excel.Controls.CheckBox> controle para ou próximo à célula **B2** em **Sheet1**.

3. No menu **Exibir** , selecione janela **Propriedades** .

4. Certifique-se de que **checkBox1** esteja visível na caixa de listagem nome do objeto da janela **Propriedades** e altere as seguintes propriedades:

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**applyBoldFont**|
    |**Text**|**Negrito**|

5. Arraste uma segunda caixa de seleção para a célula **B4** ou próximo dela e altere as seguintes propriedades:

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**applyItalicFont**|
    |**Text**|**Itálico**|

6. Arraste uma terceira caixa de seleção para ou próxima à célula **B6** e altere as seguintes propriedades:

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**applyUnderlineFont**|
    |**Text**|**Aplicar**|

7. Selecione todos os três controles de caixa de seleção mantendo a tecla **Ctrl** pressionada.

8. No grupo organizar da guia formato no Excel, clique em **alinhar** e, em seguida, clique em **alinhar à esquerda**.

     Os três controles de caixa de seleção são alinhados no lado esquerdo, na posição do primeiro controle selecionado.

     Em seguida, você arrastará um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle para a planilha.

    > [!NOTE]
    > Você também pode adicionar o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle digitando **TextFont** na caixa **nome** .

#### <a name="to-add-text-to-a-namedrange-control"></a>Para adicionar texto a um controle NamedRange

1. Na guia **controles do Excel** da caixa de ferramentas, arraste um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle para a célula **B9**.

2. Verifique se **$B $9** aparece na caixa de texto editável e se a célula **B9** está selecionada. Se não estiver, clique em célula **B9** para selecioná-la.

3. Clique em **OK**.

4. A célula **B9** se torna um intervalo chamado `NamedRange1` .

    Não há nenhuma indicação visível na planilha, mas `NamedRange1` aparece na **caixa nome** (logo acima da planilha no lado esquerdo) quando a célula **B9** é selecionada.

5. Verifique se **NamedRange1** está visível na caixa de listagem nome do objeto da janela **Propriedades** e altere as seguintes propriedades:

   |Propriedade|Valor|
   |--------------|-----------|
   |**Nome**|**TextFont**|
   |**Value2**|**Clique em uma caixa de seleção para alterar a formatação desse texto.**|

   Em seguida, escreva o código para formatar o texto quando uma opção for selecionada.

## <a name="format-the-text-when-an-option-is-selected"></a>Formatar o texto quando uma opção for selecionada
 Nesta seção, você escreverá o código para que, quando o usuário selecionar uma opção de formatação, o formato do texto na planilha seja alterado.

### <a name="to-change-formatting-when-a-check-box-is-selected"></a>Para alterar a formatação quando uma caixa de seleção estiver marcada

1. Clique com o botão direito do mouse em **Plan1** e clique em **Exibir código** no menu de atalho.

2. Adicione o seguinte código ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos da `applyBoldFont` caixa de seleção:

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet7":::

3. Adicione o seguinte código ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos da `applyItalicFont` caixa de seleção:

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet8":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet8":::

4. Adicione o seguinte código ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos da `applyUnderlineFont` caixa de seleção:

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet9":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet9":::

5. No C#, você deve adicionar manipuladores de eventos para as caixas de seleção ao <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> evento, conforme mostrado abaixo. Para obter informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet10":::

## <a name="test-the-application"></a>Testar o aplicativo
 Agora você pode testar sua pasta de trabalho para certificar-se de que o texto está formatado corretamente quando você marca ou desmarca uma caixa de seleção.

### <a name="to-test-your-workbook"></a>Para testar sua pasta de trabalho

1. Pressione **F5** para executar o projeto.

2. Marque ou desmarque a caixa de seleção.

3. Confirme se o texto está formatado corretamente.

## <a name="next-steps"></a>Próximas etapas
 Este tutorial mostra as noções básicas do uso de caixas de seleção e formatação de texto em planilhas do Excel. Estas são algumas tarefas que podem vir a seguir:

- Implantando o projeto. Para obter mais informações, consulte [implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).
- Usar um botão para preencher uma caixa de texto. Para obter mais informações, consulte [Walkthrough: exibir texto em uma caixa de texto em uma planilha usando um botão](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md).

## <a name="see-also"></a>Consulte também
- [Passo a passos usando o Excel](../vsto/walkthroughs-using-excel.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)

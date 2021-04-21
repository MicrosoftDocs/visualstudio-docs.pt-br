---
title: Exibir texto na caixa de texto na planilha usando o botão
description: Aprenda as noções básicas do uso de botões e caixas de texto em planilhas do Microsoft Excel. Além disso, crie projetos do Excel usando as ferramentas de desenvolvimento do Office no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text [Office development in Visual Studio], displaying worksheets
- worksheets, displaying text
- text boxes, displaying text in worksheets
- text [Office development in Visual Studio], text boxes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b1209bf903f5a5b9c0005d9ba4ba6a891752aedd
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827780"
---
# <a name="walkthrough-display-text-in-a-text-box-in-a-worksheet-using-a-button"></a>Walkthrough: exibir texto em uma caixa de texto em uma planilha usando um botão
  Este tutorial mostra as noções básicas de como usar botões e caixas de texto em Microsoft Office planilhas do Excel e como criar projetos do Excel usando as ferramentas de desenvolvimento do Office no Visual Studio. Para ver o resultado como um exemplo completo, consulte o exemplo de controles do Excel em [exemplos de desenvolvimento do Office e passo a passos](../vsto/office-development-samples-and-walkthroughs.md).

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Durante este passo a passo, você aprenderá a:

- Adicionar controles a uma planilha.

- Popular uma caixa de texto quando um botão é clicado.

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

1. Crie um projeto de pasta de trabalho do Excel com o **botão nome My Excel**. Verifique se **a seleção criar um novo documento** está selecionada. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o projeto de **botão meu Excel** a **Gerenciador de soluções**.

## <a name="add-controls-to-the-worksheet"></a>Adicionar controles à planilha
 Para esta explicação, você precisará de um botão e uma caixa de texto na primeira planilha.

### <a name="to-add-a-button-and-a-text-box"></a>Para adicionar um botão e uma caixa de texto

1. Verifique se a pasta de trabalho **meu Excel Button.xlsx** está aberta no designer do Visual Studio, com `Sheet1` exibido.

2. Na guia **controles comuns** da caixa de ferramentas, arraste um <xref:Microsoft.Office.Tools.Excel.Controls.TextBox> para `Sheet1` .

3. No menu **Exibir** , selecione **janela Propriedades**.

4. Certifique-se de que **TextBox1** esteja visível na caixa suspensa janela de **Propriedades** e altere a propriedade **Name** da caixa de texto para **exibirtexto**.

5. Arraste um controle de **botão** para `Sheet1` e altere as seguintes propriedades:

   |Propriedade|Valor|
   |--------------|-----------|
   |**Nome**|**insertText**|
   |**Text**|**Inserir texto**|

   Agora, escreva o código para ser executado quando o botão for clicado.

## <a name="populate-the-text-box-when-the-button-is-clicked"></a>Preencher a caixa de texto quando o botão for clicado
 Cada vez que o usuário clica no botão, **Olá, mundo!** é anexado à caixa de texto.

### <a name="to-write-to-the-text-box-when-the-button-is-clicked"></a>Para gravar na caixa de texto quando o botão é clicado

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **Plan1** e clique em **Exibir código** no menu de atalho.

2. Adicione o seguinte código ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos do botão:

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet11":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet11":::

3. No C#, você deve adicionar um manipulador de eventos ao <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> evento, conforme mostrado abaixo. Para obter informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet12":::

## <a name="test-the-application"></a>Testar o aplicativo
 Agora você pode testar sua pasta de trabalho para certificar-se de que a mensagem **Olá, mundo!** aparece na caixa de texto quando você clica no botão.

### <a name="to-test-your-workbook"></a>Para testar sua pasta de trabalho

1. Pressione **F5** para executar o projeto.

2. Clique no botão.

3. Confirme se **Olá, mundo!** aparece na caixa de texto.

## <a name="next-steps"></a>Próximas etapas
 Este tutorial mostra as noções básicas de como usar botões e caixas de texto em planilhas do Excel. Estas são algumas tarefas que podem vir a seguir:

- Implantando o projeto. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).

- Usando as caixas de seleção para alterar a formatação. Para obter mais informações, consulte [Walkthrough: alterar a formatação da planilha usando controles CheckBox](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md).

## <a name="see-also"></a>Consulte também
- [Como: adicionar controles de Windows Forms a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [Passo a passos usando o Excel](../vsto/walkthroughs-using-excel.md)
- [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)

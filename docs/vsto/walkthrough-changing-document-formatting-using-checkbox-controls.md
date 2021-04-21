---
title: Alterar a formatação do documento usando controles CheckBox
description: Saiba como usar os controles de Windows Forms em uma personalização em nível de documento para o Microsoft Word alterar a formatação de texto.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word documents, changing formatting using controls
- documents [Office development in Visual Studio], formatting
- check boxes, Word documents
- documents [Office development in Visual Studio], check box controls
- controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3f6fbb91c37fd8956860eed8e4d39f8b0a8c1a0e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824413"
---
# <a name="walkthrough-change-document-formatting-using-checkbox-controls"></a>Walkthrough: alterar a formatação do documento usando controles CheckBox
  Este tutorial demonstra como usar Windows Forms controles em uma personalização em nível de documento para Microsoft Office Word para alterar a formatação de texto.

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Adicionar texto e um controle ao documento em um projeto de nível de documento em tempo de design.

- Formatando o texto quando uma opção é selecionada.

  Para ver o resultado como um exemplo completo, consulte o exemplo de controles do Word em [exemplos de desenvolvimento do Office e passo a passos](../vsto/office-development-samples-and-walkthroughs.md).

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].

## <a name="create-the-project"></a>Criar o projeto
 A primeira etapa é criar um projeto de Documento do Word.

### <a name="create-a-new-project"></a>Criar um novo projeto

1. Crie um projeto de documento do Word com o nome **minha formatação de palavra**. No assistente, selecione **criar um novo documento**.

     Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre o novo documento do Word no designer e adiciona o projeto de **formatação meu Word** a **Gerenciador de soluções**.

## <a name="add-text-and-controls-to-the-word-document"></a>Adicionar texto e controles ao documento do Word
 Para esta explicação, adicione três caixas de seleção e algum texto em um <xref:Microsoft.Office.Tools.Word.Bookmark> controle ao documento do Word. As caixas de seleção apresentarão opções ao usuário para formatar o texto.

### <a name="add-three-check-boxes"></a>Adicionar três caixas de seleção

1. Verifique se o documento está aberto no designer do Visual Studio.

2. Na guia **controles comuns** da caixa de **ferramentas**, arraste o primeiro <xref:Microsoft.Office.Tools.Word.Controls.CheckBox> controle para o documento.

3. Na janela **Propriedades** , altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**applyBoldFont**|
    |**Text**|**Negrito**|

4. Pressione **Enter** para mover o ponto de inserção para baixo da primeira caixa de seleção.

5. Adicione uma segunda caixa de seleção ao documento abaixo da `ApplyBoldFont` caixa de seleção e altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**applyItalicFont**|
    |**Text**|**Itálico**|

6. Pressione **Enter** para mover o ponto de inserção para baixo da segunda caixa de seleção.

7. Adicione uma terceira caixa de seleção ao documento abaixo da `ApplyItalicFont` caixa de seleção e altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**applyUnderlineFont**|
    |**Text**|**Aplicar**|

### <a name="add-text-and-a-bookmark-control"></a>Adicionar texto e um controle de indicador

1. Mova o ponto de inserção para baixo nos controles da caixa de seleção e digite o seguinte texto:

    **Clique em uma caixa de seleção para alterar a formatação desse texto.**

2. Na guia **controles do Word** da **caixa de ferramentas**, arraste um <xref:Microsoft.Office.Tools.Word.Bookmark> controle para o documento.

    A caixa de diálogo **Adicionar controle de indicadores** é exibida.

3. Selecione o texto que você adicionou ao documento e clique em **OK**.

    Um <xref:Microsoft.Office.Tools.Word.Bookmark> controle chamado **Bookmark1** é adicionado ao texto selecionado no documento.

4. Na janela **Propriedades** , altere o valor da propriedade **(Name)** para **fontText.**

   Em seguida, escreva o código para formatar o texto quando uma caixa de seleção estiver marcada ou desmarcada.

## <a name="format-the-text-when-a-check-box-is-checked-or-cleared"></a>Formatar o texto quando uma caixa de seleção estiver marcada ou desmarcada
 Quando o usuário seleciona uma opção de formatação, altere o formato do texto no documento.

### <a name="change-formatting-when-a-check-box-is-selected"></a>Alterar a formatação quando uma caixa de seleção estiver marcada

1. Clique com o botão direito do mouse `ThisDocument` em **Gerenciador de soluções** e clique em **Exibir código** no menu de atalho.

2. Somente para C#, adicione as constantes a seguir à classe **ThisDocument** .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet2":::

3. Adicione o código a seguir ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos da `applyBoldFont` caixa de seleção.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet3":::

4. Adicione o código a seguir ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos da `applyItalicFont` caixa de seleção.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet4":::

5. Adicione o código a seguir ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos da `applyUnderlineFont` caixa de seleção.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet5":::

6. No C#, você deve adicionar manipuladores de eventos para as caixas de texto ao <xref:Microsoft.Office.Tools.Word.Document.Startup> evento. Para obter informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet6":::

## <a name="test-the-application"></a>Testar o aplicativo
 Agora você pode testar seu documento para verificar se o texto está formatado corretamente quando você marca ou desmarca uma caixa de seleção.

### <a name="test-your-document"></a>Testar seu documento

1. Pressione **F5** para executar o projeto.

2. Marque ou desmarque a caixa de seleção.

3. Confirme se o texto está formatado corretamente.

## <a name="next-steps"></a>Próximas etapas
 Este tutorial mostra as noções básicas do uso de caixas de seleção e a alteração programática da formatação de texto em documentos do Word. Estas são algumas tarefas que podem vir a seguir:

- Use um botão para preencher uma caixa de texto. Para obter mais informações, consulte [Walkthrough: exibir texto em uma caixa de texto em um documento usando um botão](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md).

- Usando botões de opção para selecionar estilos de gráfico. Para obter mais informações, consulte [Walkthrough: atualizar um gráfico em um documento usando botões de opção](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md).

## <a name="see-also"></a>Consulte também
- [Passo a passos usando o Word](../vsto/walkthroughs-using-word.md)
- [Exemplos e orientações de desenvolvimento do Office](../vsto/office-development-samples-and-walkthroughs.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)

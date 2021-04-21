---
title: Adicionar controles ao documento em tempo de execução no suplemento do VSTO
description: Saiba como usar a faixa de faixas para permitir que os usuários adicionem uma classe de botão ou uma interface RichTextContentControl a um documento.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], adding controls
- application-level add-ins [Office development in Visual Studio], adding controls
- controls [Office development in Visual Studio], adding to documents at run time
- documents [Office development in Visual Studio], adding controls at run time
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c2088a4d2ca81418ca16b51b53b0af38595d75b2
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825388"
---
# <a name="walkthrough-add-controls-to-a-document-at-run-time-in-a-vsto-add-in"></a>Walkthrough: adicionar controles a um documento em tempo de execução em um suplemento do VSTO
  Você pode adicionar controles a qualquer documento do Word aberto Microsoft Office usando um suplemento do VSTO. Este tutorial demonstra como usar a faixa de faixas para permitir que os usuários adicionem um <xref:Microsoft.Office.Tools.Word.Controls.Button> ou um <xref:Microsoft.Office.Tools.Word.RichTextContentControl> documento.

 **Aplica-se a:** As informações neste tópico se aplicam a projetos de suplemento do VSTO para Word 2010. Para obter mais informações, confira [Features Available by Office Application and Project Type](../vsto/features-available-by-office-application-and-project-type.md) (Funcionalidades disponibilizadas pelo aplicativo do Office e pelo tipo de projeto).

 Este passo a passo ilustra as seguintes tarefas:

- Criando um novo projeto de suplemento do VSTO do Word.

- Fornecer uma interface do usuário para adicionar controles ao documento.

- Adicionar controles ao documento em tempo de execução.

- Removendo controles do documento.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].

## <a name="create-a-new-word-add-in-project"></a>Criar um novo projeto de suplemento do Word
 Comece criando um projeto de suplemento do VSTO do Word.

### <a name="to-create-a-new-word-vsto-add-in-project"></a>Para criar um novo projeto de suplemento do VSTO do Word

1. Crie um projeto de suplemento do VSTO para Word com o nome **WordDynamicControls**. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

2. Adicione uma referência ao assembly **Microsoft.Office.Tools.Word.v4.0.Utilities.dll** . Essa referência é necessária para adicionar programaticamente um controle de Windows Forms ao documento mais adiante neste guia.

## <a name="provide-a-ui-to-add-controls-to-a-document"></a>Fornecer uma interface do usuário para adicionar controles a um documento
 Adicione uma guia personalizada à faixa de palavras no Word. Os usuários podem Marcar caixas de seleção na guia para adicionar controles a um documento.

### <a name="to-provide-a-ui-to-add-controls-to-a-document"></a>Para fornecer uma interface do usuário para adicionar controles a um documento

1. No menu **Projeto** , clique em **Adicionar Novo Item**.

2. Na caixa de diálogo **Adicionar novo item** , selecione **faixa de opções (designer visual)**.

3. Altere o nome da nova faixa de forma para **MyRibbon** e clique em **Adicionar**.

    O arquivo **MyRibbon. cs** ou **MyRibbon. vb** é aberto no designer de faixa de faixas e exibe uma guia e um grupo padrão.

4. No designer de faixa de faixas, clique no grupo **grupo1** .

5. Na janela **Propriedades** , altere a propriedade **rótulo** para **grupo1** para **Adicionar controles**.

6. Na guia **controles da faixa** de **ferramentas** do Office, arraste um controle de **caixa de seleção** para o **grupo1**.

7. Clique em **checkBox1** para selecioná-lo.

8. Na janela **Propriedades** , altere as propriedades a seguir.

   | Propriedade | Valor |
   |-----------|-----------------------|
   | **Nome** | **addButtonCheckBox** |
   | **Rótulo** | **Botão Adicionar** |

9. Adicione uma segunda caixa de seleção a **grupo1** e, em seguida, altere as propriedades a seguir.

   | Propriedade | Valor |
   |-----------|---------------------------|
   | **Nome** | **addRichTextCheckBox** |
   | **Rótulo** | **Adicionar controle de Rich Text** |

10. No designer de faixa de faixas, clique duas vezes no **botão Adicionar**.

     O <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> manipulador de eventos da caixa de seleção **Adicionar botão** é aberto no editor de códigos.

11. Retorne ao designer de faixa de faixas e clique duas vezes em **Adicionar controle de Rich Text**.

     O <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> manipulador de eventos da caixa de seleção **Adicionar controle de Rich Text** é aberto no editor de códigos.

    Mais adiante neste tutorial, você adicionará código a esses manipuladores de eventos para adicionar e remover controles no documento ativo.

## <a name="add-and-remove-controls-on-the-active-document"></a>Adicionar e remover controles no documento ativo
 No código do suplemento do VSTO, você deve converter o documento ativo em um <xref:Microsoft.Office.Tools.Word.Document> *item de host* antes de poder adicionar um controle. Em soluções do Office, os controles gerenciados podem ser adicionados somente a itens de host, que atuam como contêineres para os controles. Em projetos de suplemento do VSTO, os itens de host podem ser criados em tempo de execução usando o `GetVstoObject` método.

 Adicione métodos à `ThisAddIn` classe que pode ser chamada para adicionar ou remover um <xref:Microsoft.Office.Tools.Word.Controls.Button> ou <xref:Microsoft.Office.Tools.Word.RichTextContentControl> no documento ativo. Mais adiante neste tutorial, você chamará esses métodos nos <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> manipuladores de eventos das caixas de seleção na faixa de quadros.

### <a name="to-add-and-remove-controls-on-the-active-document"></a>Para adicionar e remover controles no documento ativo

1. Em **Gerenciador de soluções**, clique duas vezes em *ThisAddIn. cs* ou em *ThisAddIn. vb* para abrir o arquivo no editor de código.

2. Adicione o código a seguir à classe `ThisAddIn` . Esse código declara <xref:Microsoft.Office.Tools.Word.Controls.Button> e <xref:Microsoft.Office.Tools.Word.RichTextContentControl> objetos que representam os controles que serão adicionados ao documento.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs" id="Snippet1":::

3. Adicione o método a seguir à classe `ThisAddIn`. Quando o usuário clicar na caixa de seleção **Adicionar botão** na faixa de opção, esse método adicionará um <xref:Microsoft.Office.Tools.Word.Controls.Button> à seleção atual no documento se a caixa de seleção estiver marcada ou removerá o <xref:Microsoft.Office.Tools.Word.Controls.Button> se a caixa de seleção estiver desmarcada.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs" id="Snippet2":::

4. Adicione o método a seguir à classe `ThisAddIn`. Quando o usuário clica na caixa de seleção **Adicionar controle de Rich Text** na faixa de opção, esse método adiciona um <xref:Microsoft.Office.Tools.Word.RichTextContentControl> à seleção atual no documento se a caixa de seleção estiver marcada ou removerá o <xref:Microsoft.Office.Tools.Word.RichTextContentControl> se a caixa de seleção estiver desmarcada.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs" id="Snippet3":::

## <a name="remove-the-button-control-when-the-document-is-saved"></a>Remover o controle de botão quando o documento for salvo
 Windows Forms controles não são persistidos quando o documento é salvo e fechado. No entanto, um wrapper ActiveX para cada controle permanece no documento e a borda desse wrapper pode ser vista pelos usuários finais quando o documento é reaberto. Há várias maneiras de limpar controles de Windows Forms criados dinamicamente em suplementos do VSTO. Neste tutorial, você remove programaticamente o <xref:Microsoft.Office.Tools.Word.Controls.Button> controle quando o documento é salvo.

### <a name="to-remove-the-button-control-when-the-document-is-saved"></a>Para remover o controle de botão quando o documento é salvo

1. No arquivo de código *ThisAddIn. cs* ou *ThisAddIn. vb* , adicione o método a seguir à `ThisAddIn` classe. Esse método é um manipulador de eventos para o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> evento. Se o documento salvo tiver um <xref:Microsoft.Office.Tools.Word.Document> item de host associado a ele, o manipulador de eventos obterá o item de host e removerá o <xref:Microsoft.Office.Tools.Word.Controls.Button> controle, se ele existir.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs" id="Snippet4":::

2. No C#, adicione o código a seguir ao `ThisAddIn_Startup` manipulador de eventos. Esse código é necessário em C# para conectar o `Application_DocumentBeforeSave` manipulador de eventos ao <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> evento.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/ThisAddIn.cs" id="Snippet5":::

## <a name="add-and-remove-controls-when-the-user-clicks-the-check-boxes-on-the-ribbon"></a>Adicionar e remover controles quando o usuário clica nas caixas de seleção na faixa de quadros
 Por fim, modifique os <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> manipuladores de eventos das caixas de seleção que você adicionou à faixa de lista para adicionar ou remover controles no documento.

### <a name="to-add-or-remove-controls-when-the-user-clicks-the-check-boxes-on-the-ribbon"></a>Para adicionar ou remover controles quando o usuário clica nas caixas de seleção na faixa de quadros

1. No arquivo de código *MyRibbon. cs* ou *MyRibbon. vb* , substitua os `addButtonCheckBox_Click` `addRichTextCheckBox_Click` manipuladores de eventos e gerados pelo código a seguir. Esse código redefine esses manipuladores de eventos para chamar os `ToggleButtonOnDocument` `ToggleRichTextControlOnDocument` métodos e que você adicionou à `ThisAddIn` classe anteriormente neste guia.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_WordAddInDynamicControlsWalkthrough/MyRibbon.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControlsWalkthrough/MyRibbon.cs" id="Snippet6":::

## <a name="test-the-solution"></a>Testar a solução
 Adicione controles a um documento selecionando-os na guia personalizado na faixa de faixas. Quando você salva o documento, o <xref:Microsoft.Office.Tools.Word.Controls.Button> controle é removido.

### <a name="to-test-the-solution"></a>Para testar a solução.

1. Pressione **F5** para executar o projeto.

2. No documento ativo, pressione **Enter** várias vezes para adicionar novos parágrafos vazios ao documento.

3. Selecione o primeiro parágrafo.

4. Clique na guia **suplementos** .

5. No grupo **Adicionar controles** , clique no **botão Adicionar**.

     Um botão aparece no primeiro parágrafo.

6. Selecione o último parágrafo.

7. No grupo **Adicionar controles** , clique em **Adicionar controle de Rich Text**.

     Um controle de conteúdo de Rich Text é adicionado ao último parágrafo.

8. Salve o documento.

     O botão é removido do documento.

## <a name="next-steps"></a>Próximas etapas
 Você pode saber mais sobre os controles nos suplementos do VSTO a partir destes tópicos:

- Para obter um exemplo que demonstra como adicionar muitos outros tipos de controles a um documento em tempo de execução e recriar os controles quando o documento é reaberto, consulte a palavra Add-In exemplo de controles dinâmicos em [exemplos de desenvolvimento do Office e passo a passos](../vsto/office-development-samples-and-walkthroughs.md).

- Para obter instruções que demonstram como adicionar controles a uma planilha usando um suplemento do VSTO para Excel, consulte [passo a passos: adicionar controles a uma planilha em tempo de execução no projeto de suplemento do VSTO](../vsto/walkthrough-adding-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project.md).

## <a name="see-also"></a>Consulte também
- [Soluções do Word](../vsto/word-solutions.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Persistir controles dinâmicos em documentos do Office](../vsto/persisting-dynamic-controls-in-office-documents.md)
- [Como: adicionar controles de Windows Forms a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [Como: adicionar controles de conteúdo a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)

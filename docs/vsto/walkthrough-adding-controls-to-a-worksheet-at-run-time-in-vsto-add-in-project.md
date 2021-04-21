---
title: Adicionar controles à planilha em tempo de execução no projeto de suplemento do VSTO
description: Saiba como usar a faixa de faixas para permitir que os usuários adicionem um botão, um NamedRange e um ListObject a uma planilha.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], adding controls
- controls [Office development in Visual Studio], adding to worksheets at run time
- application-level add-ins [Office development in Visual Studio], adding controls
- worksheets, adding controls at run time
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 178180e8c698ca56b15e46bcbe65877d68c6b2a1
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824673"
---
# <a name="walkthrough-add-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project"></a>Walkthrough: adicionar controles a uma planilha em tempo de execução no projeto de suplemento do VSTO
  Você pode adicionar controles a qualquer planilha aberta usando um suplemento do VSTO do Excel. Este tutorial demonstra como usar a faixa de faixas para permitir que os usuários adicionem um <xref:Microsoft.Office.Tools.Excel.Controls.Button> , um <xref:Microsoft.Office.Tools.Excel.NamedRange> e um <xref:Microsoft.Office.Tools.Excel.ListObject> a uma planilha. Para obter informações, consulte [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).

 **Aplica-se a:** As informações neste tópico se aplicam a projetos de suplemento do VSTO para Excel. Para obter mais informações, confira [Features Available by Office Application and Project Type](../vsto/features-available-by-office-application-and-project-type.md) (Funcionalidades disponibilizadas pelo aplicativo do Office e pelo tipo de projeto).

 Este passo a passo ilustra as seguintes tarefas:

- Fornecer uma interface do usuário para adicionar controles à planilha.

- Adicionando controles à planilha.

- Removendo controles da planilha.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Excel

## <a name="create-a-new-excel-vsto-add-in-project"></a>Criar um novo projeto de suplemento do VSTO do Excel
 Comece criando um projeto de suplemento do VSTO do Excel.

### <a name="to-create-a-new-excel-vsto-add-in-project"></a>Para criar um novo projeto de suplemento do VSTO do Excel

1. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , crie um projeto de suplemento do VSTO do Excel com o nome **ExcelDynamicControls**. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

2. Adicione uma referência ao assembly **Microsoft.Office.Tools.Excel.v4.0.Utilities.dll** . Essa referência é necessária para adicionar programaticamente um controle de Windows Forms a uma planilha mais adiante neste guia.

## <a name="provide-a-ui-to-add-controls-to-a-worksheet"></a>Fornecer uma interface do usuário para adicionar controles a uma planilha
 Adicione uma guia personalizada à faixa de, do Excel. Os usuários podem marcar as caixas de seleção na guia para adicionar controles a uma planilha.

#### <a name="to-provide-a-ui-to-add-controls-to-a-worksheet"></a>Para fornecer uma interface do usuário para adicionar controles a uma planilha

1. No menu **Projeto** , clique em **Adicionar Novo Item**.

2. Na caixa de diálogo **Adicionar novo item** , selecione **faixa de opções (designer visual)** e clique em **Adicionar**.

     Um arquivo chamado **Ribbon1. cs** ou **Ribbon1. vb** é aberto no designer de faixa de faixas e exibe uma guia e um grupo padrão.

3. Na guia **controles da faixa** de **ferramentas** do Office, arraste um controle de caixa de seleção para o **grupo1**.

4. Clique em **checkBox1** para selecioná-lo.

5. Na janela **Propriedades** , altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**Botão**|
    |**Rótulo**|**Botão**|

6. Adicione uma segunda caixa de seleção a **grupo1** e, em seguida, altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**NamedRange**|
    |**Rótulo**|**NamedRange**|

7. Adicione uma terceira caixa de seleção a **grupo1** e, em seguida, altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**ListObject**|
    |**Rótulo**|**ListObject**|

## <a name="add-controls-to-the-worksheet"></a>Adicionar controles à planilha
 Os controles gerenciados só podem ser adicionados a itens de host, que atuam como contêineres. Como os projetos do suplemento do VSTO funcionam com qualquer pasta de trabalho aberta, o suplemento do VSTO converte a planilha em um item de host ou Obtém um item de host existente, antes de adicionar o controle. Adicione código aos manipuladores de eventos de clique de cada controle para gerar um <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host baseado na planilha aberta. Em seguida, adicione um <xref:Microsoft.Office.Tools.Excel.Controls.Button> , um <xref:Microsoft.Office.Tools.Excel.NamedRange> e um <xref:Microsoft.Office.Tools.Excel.ListObject> na seleção atual na planilha.

### <a name="to-add-controls-to-a-worksheet"></a>Para adicionar controles a uma planilha

1. No designer de faixa de faixas, clique duas vezes em **botão**.

     O <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> manipulador de eventos da caixa de seleção do **botão** é aberto no editor de códigos.

2. Substitua o `Button_Click` manipulador de eventos pelo código a seguir.

     Esse código usa o `GetVstoObject` método para obter um item de host que representa a primeira planilha na pasta de trabalho e, em seguida, adiciona um <xref:Microsoft.Office.Tools.Excel.Controls.Button> controle à célula atualmente selecionada.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb" id="Snippet2":::

3. Em **Gerenciador de soluções**, selecione *Ribbon1. cs* ou *Ribbon1. vb*.

4. No menu **Exibir** , clique em **Designer**.

5. No designer de faixa de faixas, clique duas vezes em **NamedRange**.

6. Substitua o `NamedRange_Click` manipulador de eventos pelo código a seguir.

     Esse código usa o `GetVstoObject` método para obter um item de host que representa a primeira planilha na pasta de trabalho e, em seguida, define um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle para a célula ou células selecionadas no momento.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb" id="Snippet3":::

7. No designer de faixa de faixas, clique duas vezes em **ListObject**.

8. Substitua o `ListObject_Click` manipulador de eventos pelo código a seguir.

     Esse código usa o `GetVstoObject` método para obter um item de host que representa a primeira planilha na pasta de trabalho e, em seguida, define um <xref:Microsoft.Office.Tools.Excel.ListObject> para a célula ou células selecionadas no momento.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb" id="Snippet4":::

9. Adicione as instruções a seguir à parte superior do arquivo de código da faixa de opções.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb" id="Snippet1":::

## <a name="remove-controls-from-the-worksheet"></a>Remover controles da planilha
 Os controles não são persistidos quando a planilha é salva e fechada. Você deve remover programaticamente todos os controles de Windows Forms gerados antes que a planilha seja salva, ou apenas uma estrutura de tópicos do controle será exibida quando a pasta de trabalho for aberta novamente. Adicione código ao <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> evento que remove Windows Forms controles da coleção Controls do item de host gerado. Para obter mais informações, consulte [manter controles dinâmicos em documentos do Office](../vsto/persisting-dynamic-controls-in-office-documents.md).

### <a name="to-remove-controls-from-the-worksheet"></a>Para remover controles da planilha

1. Em **Gerenciador de soluções**, selecione *ThisAddIn. cs* ou *ThisAddIn. vb*.

2. No menu **Exibir** , clique em **Código**.

3. Adicione o método a seguir à classe `ThisAddIn`. Esse código obtém a primeira planilha na pasta de trabalho e, em seguida, usa o `HasVstoObject` método para verificar se a planilha tem um objeto de planilha gerado. Se o objeto de planilha gerado tiver controles, o código obterá esse objeto de planilha e iterará pela coleção de controle, removendo os controles.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet6":::

4. No C#, você deve criar um manipulador de eventos para o <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> evento. Você pode posicionar esse código no `ThisAddIn_Startup` método. Para obter mais informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md). Substitua o método `ThisAddIn_Startup` pelo seguinte código.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet5":::

## <a name="test-the-solution"></a>Testar a solução
 Adicione controles a uma planilha selecionando-os em uma guia personalizada na faixa de faixas. Quando você salva a planilha, esses controles são removidos.

### <a name="to-test-the-solution"></a>Para testar a solução.

1. Pressione **F5** para executar o projeto.

2. Selecione qualquer célula em Sheet1.

3. Clique na guia **suplementos** .

4. No grupo **grupo1** , clique no **botão**.

     Um botão aparece na célula selecionada.

5. Selecione uma célula diferente em Plan1.

6. No grupo **grupo1** , clique em **NamedRange**.

     Um intervalo nomeado é definido para a célula selecionada.

7. Selecione uma série de células em Sheet1.

8. No grupo **grupo1** , clique em **ListObject**.

     Um objeto de lista é adicionado para as células selecionadas.

9. Salve a planilha.

     Os controles que você adicionou a Sheet1 não aparecem mais.

## <a name="next-steps"></a>Próximas etapas
 Você pode saber mais sobre os controles em projetos do suplemento do VSTO do Excel deste tópico:

- Para saber mais sobre como salvar controles em uma planilha, confira o exemplo de controles dinâmicos do suplemento VSTO do Excel em [exemplos de desenvolvimento do Office e passo a passos](../vsto/office-development-samples-and-walkthroughs.md).

## <a name="see-also"></a>Consulte também
- [Soluções do Excel](../vsto/excel-solutions.md)
- [Visão geral dos controles do Windows Forms em documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Controle ListObject](../vsto/listobject-control.md)

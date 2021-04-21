---
title: 'Walkthrough: atualizar um gráfico em um documento usando botões de opção'
description: Saiba como você pode usar botões de opção em uma personalização em nível de documento para o Microsoft Word para dar aos usuários a opção de selecionar estilos de gráfico no documento.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], updating using controls
- controls [Office development in Visual Studio], updating documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4d6689d82051ef5f8c887c19ec91cbb6d513b8b8
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828196"
---
# <a name="walkthrough-update-a-chart-in-a-document-using-radio-buttons"></a>Walkthrough: atualizar um gráfico em um documento usando botões de opção
  Esse passo a passo demonstra como usar os botões de opção em uma personalização ao nível do documento do Microsoft Office Word para fornecer aos usuários a opção de selecionar estilos de gráficos no documento.

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Adicionar um gráfico ao documento em um projeto ao nível do documento no tempo de design.

- Agrupamento dos botões de opção adicionando-os a um controle de usuário.

- Alterando o estilo do gráfico quando uma opção ser selecionada.

  Para ver o resultado como um exemplo completo, consulte o exemplo de controles do Word em [exemplos de desenvolvimento do Office e passo a passos](../vsto/office-development-samples-and-walkthroughs.md).

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].

## <a name="create-the-project"></a>Criar o projeto
 A primeira etapa é criar um projeto de Documento do Word.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de documento do Word com o nome **minhas opções de gráfico**. No assistente, selecione **criar um novo documento**. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre o novo documento do Word no designer e adiciona o projeto de **Opções meu gráfico** a **Gerenciador de soluções**.

## <a name="add-a-chart-to-the-document"></a>Adicionar um gráfico ao documento

### <a name="to-add-a-chart"></a>Para adicionar um gráfico

1. No documento do Word que está hospedado no Visual Studio Designer, na faixa de palavras, clique na guia **Inserir** .

2. No grupo de **texto** , clique no botão suspenso **Inserir objeto** e clique em **objeto**.

     A caixa de diálogo **objeto** é aberta.

3. Na lista **tipo de objeto** da guia **criar nova** , selecione **Microsoft Graph gráfico** e clique em **OK**.

     Um gráfico é adicionado ao documento no ponto de inserção e a janela **folha** de dados é exibida com algum dado padrão.

4. Feche a janela **folha** de documentos para aceitar os valores padrão no gráfico e clique dentro do documento para mover o foco para longe do gráfico.

5. Clique com o botão direito do mouse no gráfico e clique em **Formatar objeto**.

6. Na guia **layout** da caixa de diálogo **Formatar objeto** , selecione **quadrado** e clique em **OK**.

## <a name="add-a-user-control-to-the-project"></a>Adicionar um controle de usuário ao projeto
 Os botões de opção em um documento não são mutuamente excludentes por padrão. É possível fazê-los funcionar corretamente adicionando-os a um controle de usuário e, em seguida, escrevendo o código para controlar a seleção.

### <a name="to-add-a-user-control"></a>Para adicionar um controle de usuário

1. Selecione o projeto **minhas opções de gráfico** no **Gerenciador de soluções**.

2. No menu **Projeto** , clique em **Adicionar Novo Item**.

3. Na caixa de diálogo **Adicionar novo item** , clique em **controle de usuário**, nomeie o controle **gráficooptions** e clique em **Adicionar**.

### <a name="to-add-windows-form-controls-to-the-user-control"></a>Para adicionar os controles Windows Form ao controle de usuário

1. Se o controle de usuário não estiver visível no designer, clique duas vezes em **ChartOptions** em **Gerenciador de soluções**.

2. Na guia **controles comuns** da caixa de **ferramentas**, arraste o primeiro controle de **botão de opção** para o controle de usuário e altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**columnChart**|
    |**Text**|**Gráfico de colunas**|

3. Adicione um segundo **botão de opção** ao controle de usuário e altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**barChart**|
    |**Text**|**Gráfico de barras**|

4. Adicione um terceiro **botão de opção** ao controle de usuário e altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**lineChart**|
    |**Text**|**Gráfico de linhas**|

5. Adicione um quarto **botão de opção** ao controle de usuário e altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**areaBlockChart**|
    |**Text**|**Gráfico de Blocos de Área**|

## <a name="add-references"></a>Adicionar referências
 Para acessar o gráfico do controle de usuário em um documento, você deve ter uma referência ao `Microsoft.Office.Interop.Graph` assembly em seu projeto.

### <a name="to-add-a-reference-to-the-microsoftofficeinteropgraph-assembly"></a>Para adicionar uma referência ao assembly Microsoft.Office.Interop.Graph

1. No menu **Projeto**, clique em **Adicionar Referência**.

     A caixa de diálogo **Adicionar Referência** é exibida.

2. Na guia **.net** , selecione **Microsoft. Office. Interop. Graph** e clique em **OK**. Selecione a versão 14.0.0.0 do assembly.

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>Alterar o estilo do gráfico quando um botão de opção for selecionado
 Para fazer os botões funcionarem corretamente, crie um evento público no controle de usuário, adicione uma propriedade para definir o tipo de seleção e crie um procedimento para o evento `CheckedChanged` de cada um dos botões de opção.

### <a name="to-create-an-event-and-property-on-a-user-control"></a>Para criar um evento e uma propriedade em um controle de usuário

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no controle de usuário e clique em **Exibir código**.

2. Adicione um código para criar um evento `SelectionChanged` e a propriedade `Selection` à classe `ChartOptions`.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb" id="Snippet9":::

### <a name="to-handle-the-checkedchange-event-of-the-radio-buttons"></a>Para tratar o evento CheckedChange dos botões de opção

1. Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `areaBlockChart` e, em seguida, gere o evento.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb" id="Snippet10":::

2. Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `barChart`.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb" id="Snippet11":::

3. Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `columnChart`.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb" id="Snippet12":::

4. Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `lineChart`.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet13":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb" id="Snippet13":::

5. No C#, é necessário adicionar manipuladores de eventos aos botões de opção. É possível adicionar o código ao construtor `ChartOptions`, abaixo da chamada para `InitializeComponent`. Para obter informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet14":::

## <a name="add-the-user-control-to-the-document"></a>Adicionar o controle de usuário ao documento
 Quando você cria a solução, o novo controle de usuário é adicionado automaticamente à **caixa de ferramentas**. Em seguida, você pode arrastar o controle da **caixa de ferramentas** para seu documento.

### <a name="to-add-the-user-control-your-document"></a>Para adicionar o controle de usuário ao seu documento

1. No menu **Compilar**, clique em **Compilar Solução**.

     O controle de usuário **ChartOptions** é adicionado à **caixa de ferramentas**.

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **ThisDocument. vb** ou **ThisDocument. cs** e clique em **Designer de exibição**.

3. Arraste o `ChartOptions` controle da **caixa de ferramentas** para o documento.

     Na janela **Propriedades** , nomeie o controle que você acabou de adicionar ao documento  `ChartOptions1` .

## <a name="change-the-chart-type"></a>Alterar o tipo de gráfico
 Crie um manipulador de eventos para alterar o tipo de gráfico de acordo com a opção selecionada no controle de usuário.

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-document"></a>Para alterar o tipo de gráfico exibido o documento

1. Adicione o manipulador de eventos a seguir à classe `ThisDocument`.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet15":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet15":::

2. No C#, é necessário adicionar um manipulador de eventos do controle de usuário ao evento <xref:Microsoft.Office.Tools.Word.Document.Startup>.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet16":::

## <a name="test-the-application"></a>Testar o aplicativo
 Agora é possível testar seu documento para certificar-se de que o estilo gráfico está atualizado corretamente ao selecionar um botão de opção.

### <a name="to-test-your-document"></a>Para testar o documento

1. Pressione **F5** para executar o projeto.

2. Selecione diversos botões de opção.

3. Confirme se as alterações no estilo gráfico correspondem à seleção.

## <a name="next-steps"></a>Próximas etapas
 Estas são algumas tarefas que podem vir a seguir:

- Usar um botão para preencher uma caixa de texto. Para obter mais informações, consulte [Walkthrough: exibir texto em uma caixa de texto em um documento usando um botão](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md).

- Alterar a formatação selecionando um estilo de uma caixa de combinação. Para obter mais informações, consulte [Walkthrough: alterar a formatação do documento usando controles CheckBox](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md).

## <a name="see-also"></a>Consulte também
- [Passo a passos usando o Word](../vsto/walkthroughs-using-word.md)
- [Exemplos e orientações de desenvolvimento do Office](../vsto/office-development-samples-and-walkthroughs.md)
- [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)

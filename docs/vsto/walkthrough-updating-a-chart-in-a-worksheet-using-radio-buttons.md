---
title: Atualizar o gráfico na planilha usando botões de opção
description: Aprenda as noções básicas do uso de botões de opção em uma planilha do Microsoft Excel para dar ao usuário uma maneira de alternar rapidamente entre as opções.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, updating using managed controls
- controls [Office development in Visual Studio], updating worksheets
- worksheets, using radio buttons
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3d61579181f00d97a74cc48e022bb5d93a05c0f0
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828170"
---
# <a name="walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons"></a>Instruções passo a passo: atualizando um gráfico em uma planilha usando botões de opção
  Este tutorial mostra as noções básicas de como usar botões de opção em uma Microsoft Office planilha do Excel para dar ao usuário uma maneira de alternar rapidamente entre as opções. Nesse caso, as opções alteram o estilo de um gráfico.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Para ver o resultado como um exemplo completo, consulte o exemplo de controles do Excel em [exemplos de desenvolvimento do Office e passo a passos](../vsto/office-development-samples-and-walkthroughs.md).

 Este passo a passo ilustra as seguintes tarefas:

- Adicionar um grupo de botões de opção a uma planilha.

- Alterando o estilo do gráfico quando uma opção ser selecionada.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

## <a name="add-a-chart-to-a-worksheet"></a>Adicionar um gráfico a uma planilha
 Você pode criar um projeto de pasta de trabalho do Excel que personalize uma pasta de trabalho existente. Neste tutorial, você adicionará um gráfico a uma pasta de trabalho e usará essa pasta de trabalho em uma nova solução do Excel. A fonte de dados neste passo a passo é uma planilha denominada **dados para o gráfico**.

### <a name="to-add-the-data"></a>Para adicionar os dados

1. Abra o Microsoft Excel.

2. Clique com o botão direito do mouse na guia **Sheet3** e, em seguida, clique em **renomear** no menu de atalho.

3. Renomeie a planilha para **dados do gráfico**.

4. Adicione os dados a seguir aos **dados do gráfico** com a célula A4 sendo o canto superior esquerdo e e8 o canto inferior direito.

   |Região/trimestre|Q1|T2|T3|T4|
   |-|--------|--------|--------|--------|
   |Oeste|500|550|550|600|
   |Leste|600|625|675|700|
   |Norte|450|470|490|510|
   |Sul|800|750|775|790|

   Em seguida, adicione um gráfico à primeira planilha para exibir os dados.

### <a name="to-add-a-chart-in-excel"></a>Para adicionar um gráfico no Excel

1. Na guia **Inserir** , no grupo **gráficos** , clique em **coluna** e em **todos os tipos de gráfico**.

2. Na caixa de diálogo **Inserir gráfico** , clique em **OK**.

3. Na guia **design** , no grupo de **dados** , clique em **selecionar dados**.

4. Na caixa de diálogo **selecionar fonte de dados** , clique na caixa **intervalo de ChartData** e desmarque qualquer seleção padrão.

5. Na folha **dados para o gráfico** , selecione o bloco de células que contém os números, que inclui a4 no canto superior esquerdo para e8 no canto inferior direito.

6. Na caixa de diálogo **selecionar fonte de dados** , clique em **OK**.

7. Reposicione o gráfico para que o canto superior direito fique alinhado com a célula **E2**.

8. Salve o arquivo na unidade C e nomeie-o **ExcelChart.xlsx**.

9. Saia do Excel.

## <a name="create-a-new-project"></a>Criar um novo projeto
 Nesta etapa, você criará um projeto de pasta de trabalho do Excel com base na pasta de trabalho do **ExcelChart** .

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de pasta de trabalho do Excel com o nome **meu gráfico do Excel**. No assistente, selecione **copiar um documento existente**.

     Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

2. Clique no botão **procurar** e navegue até a pasta de trabalho que você criou anteriormente neste tutorial.

3. Clique em **OK**.

     O Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o projeto de **gráfico meu Excel** a **Gerenciador de soluções**.

## <a name="set-properties-of-the-chart"></a>Definir as propriedades do gráfico
 Quando você cria um novo projeto de pasta de trabalho do Excel que usa uma pasta de trabalho existente, os controles de host são criados automaticamente para todos os intervalos nomeados, objetos de lista e gráficos na pasta de trabalho. Você pode alterar o nome do <xref:Microsoft.Office.Tools.Excel.Chart> controle usando a janela **Propriedades** .

### <a name="to-change-the-name-of-the-chart-control"></a>Para alterar o nome do controle de gráfico

1. Selecione o <xref:Microsoft.Office.Tools.Excel.Chart> controle no designer e altere as propriedades a seguir na janela **Propriedades** .

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**Gráfico de gráficos**|
    |**HasLegend**|**false**|

## <a name="add-controls"></a>Adicionar controles
 Essa planilha usa botões de opção para fornecer aos usuários uma maneira de alterar rapidamente o estilo do gráfico. No entanto, os botões de opção precisam ser exclusivos — quando um botão é selecionado, nenhum outro botão no grupo pode ser selecionado ao mesmo tempo. Esse comportamento não acontece por padrão quando você adiciona vários botões de opção a uma planilha.

 Uma maneira de adicionar esse comportamento é agrupar os botões de opção em um controle de usuário, escrever seu código por trás do controle de usuário e, em seguida, adicionar o controle de usuário à planilha.

### <a name="to-add-a-user-control"></a>Para adicionar um controle de usuário

1. Selecione o **meu** projeto de gráfico do Excel em **Gerenciador de soluções**.

2. No menu **Projeto** , clique em **Adicionar Novo Item**.

3. Na caixa de diálogo **Adicionar novo item** , clique em **controle de usuário**, nomeie o controle **gráficooptions** e clique em **Adicionar**.

### <a name="to-add-radio-buttons-to-the-user-control"></a>Para adicionar botões de opção ao controle de usuário

1. Se o controle de usuário não estiver visível no designer, clique duas vezes em **ChartOptions** em **Gerenciador de soluções**.

2. Na guia **controles comuns** da caixa de **ferramentas**, arraste um controle de **botão de opção** para o controle de usuário e altere as propriedades a seguir.

   | Propriedade | Valor |
   |----------|------------------|
   | **Nome** | **columnChart** |
   | **Text** | **Gráfico de colunas** |

3. Adicione um segundo botão de opção ao controle de usuário e altere as propriedades a seguir.

   | Propriedade | Valor |
   |----------|---------------|
   | **Nome** | **barChart** |
   | **Text** | **Gráfico de barras** |

4. Adicione um terceiro botão de opção ao controle de usuário e altere as propriedades a seguir.

   | Propriedade | Valor |
   |----------|----------------|
   | **Nome** | **lineChart** |
   | **Text** | **Gráfico de linhas** |

5. Adicione um quarto botão de opção ao controle de usuário e altere as propriedades a seguir.

   |Propriedade|Valor|
   |--------------|-----------|
   |**Nome**|**areaBlockChart**|
   |**Text**|**Gráfico de Blocos de Área**|

   Em seguida, escreva o código para atualizar o gráfico quando um botão de opção é clicado.

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>Alterar o estilo do gráfico quando um botão de opção for selecionado
 Agora você pode adicionar o código para alterar o estilo do gráfico. Para fazer isso, crie um evento público no controle de usuário, adicione uma propriedade para definir o tipo de seleção e crie um manipulador de eventos para o `CheckedChanged` evento de cada um dos botões de opção.

### <a name="to-create-an-event-and-property-on-a-user-control"></a>Para criar um evento e uma propriedade em um controle de usuário

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no controle de usuário e clique em **Exibir código**.

2. Adicione o código à `ChartOptions` classe para criar um `SelectionChanged` evento e a `Selection` propriedade.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet13":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet13":::

### <a name="to-handle-the-checkedchanged-event-of-the-radio-buttons"></a>Para manipular o evento CheckedChanged dos botões de opção

1. Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `areaBlockChart` e, em seguida, gere o evento.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet14":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet14":::

2. Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `barChart`.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet15":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet15":::

3. Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `columnChart`.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet16":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet16":::

4. Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `lineChart`.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet17":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet17":::

5. No C#, é necessário adicionar manipuladores de eventos aos botões de opção. É possível adicionar o código ao construtor `ChartOptions`, abaixo da chamada para `InitializeComponent`. Para obter informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet18":::

## <a name="add-the-user-control-to-the-worksheet"></a>Adicionar o controle de usuário à planilha
 Quando você cria a solução, o novo controle de usuário é adicionado automaticamente à **caixa de ferramentas**. Em seguida, você pode arrastar o controle da **caixa de ferramentas** para sua planilha.

### <a name="to-add-the-user-control-your-worksheet"></a>Para adicionar o controle de usuário à sua planilha

1. No menu **Compilar**, clique em **Compilar Solução**.

     O controle de usuário **ChartOptions** é adicionado à **caixa de ferramentas**.

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **Plan1. vb** ou **Plan1. cs** e clique em **Designer de exibição**.

3. Arraste o controle **ChartOptions** da **caixa de ferramentas** para a planilha.

     Um novo controle chamado `my_Excel_Chart_ChartOptions1` é adicionado ao seu projeto.

4. Altere o nome do controle para **ChartOptions1**.

## <a name="change-the-chart-type"></a>Alterar o tipo de gráfico
 Para alterar o tipo de gráfico, crie um manipulador de eventos que defina o estilo de acordo com a opção selecionada no controle de usuário.

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-worksheet"></a>Para alterar o tipo de gráfico que é exibido na planilha

1. Adicione o manipulador de eventos a seguir à classe `Sheet1`.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet19":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet19":::

2. No C#, você deve adicionar um manipulador de eventos para o controle de usuário ao <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> evento, conforme mostrado abaixo. Para obter informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet20":::

## <a name="test-the-application"></a>Testar o aplicativo
 Agora você pode testar sua pasta de trabalho para verificar se o gráfico está com o estilo correto quando você seleciona um botão de opção.

### <a name="to-test-your-workbook"></a>Para testar sua pasta de trabalho

1. Pressione **F5** para executar o projeto.

2. Selecione diversos botões de opção.

3. Confirme se as alterações no estilo gráfico correspondem à seleção.

## <a name="next-steps"></a>Próximas etapas
 Este tutorial mostra as noções básicas de como usar botões de opção e estilos de gráfico em planilhas. Estas são algumas tarefas que podem vir a seguir:

- Implantando o projeto. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).

- Usar um botão para preencher uma caixa de texto. Para obter mais informações, consulte [Walkthrough: exibir texto em uma caixa de texto em uma planilha usando um botão](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md).

- Altere a formatação em uma planilha usando as caixas de seleção. Para obter mais informações, consulte [Walkthrough: alterar a formatação da planilha usando controles CheckBox](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md).

## <a name="see-also"></a>Consulte também
- [Passo a passos usando o Excel](../vsto/walkthroughs-using-excel.md)

---
title: 'Instruções passo a passo: atualizando um gráfico em uma planilha usando botões de opção'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, updating using managed controls
- controls [Office development in Visual Studio], updating worksheets
- worksheets, using radio buttons
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5aff631d8c9b6bd65b8ae91c5d936d2669764791
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49866435"
---
# <a name="walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons"></a>Instruções passo a passo: atualizando um gráfico em uma planilha usando botões de opção
  Este passo a passo mostra as Noções básicas de como usar botões de opção em uma planilha do Microsoft Office Excel para dar ao usuário uma maneira de alternar rapidamente entre as opções. Nesse caso, as opções de alterar o estilo de um gráfico.  

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  

 Para ver o resultado como um exemplo completo, consulte o exemplo de controles do Excel em [exemplos de desenvolvimento do Office e instruções passo a passo](../vsto/office-development-samples-and-walkthroughs.md).  

 Esta explicação passo a passo ilustra as seguintes tarefas:  

-   Adicionando um grupo de botões de opção em uma planilha.  

-   Alterando o estilo do gráfico quando uma opção ser selecionada.  

> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  

## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  

-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  

-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].  

## <a name="add-a-chart-to-a-worksheet"></a>Adicionar um gráfico em uma planilha  
 Você pode criar um projeto de pasta de trabalho do Excel que personaliza a uma pasta de trabalho existente. Neste passo a passo, você irá adicionar um gráfico a uma pasta de trabalho e, em seguida, usar essa pasta de trabalho em uma nova solução do Excel. A fonte de dados neste passo a passo é uma planilha denominada **dados de gráfico**.  

### <a name="to-add-the-data"></a>Para adicionar os dados  

1. Abra o Microsoft Excel.  

2. Clique com botão direito do **Sheet3** guia e, em seguida, clique em **Renomear** no menu de atalho.  

3. Renomear a planilha para **dados de gráfico**.  

4. Adicione os seguintes dados para **dados de gráfico** com célula A4 sendo o canto superior esquerdo canto e E8 o canto inferior direito.  

   ||1º TRIMESTRE|2º TRIMESTRE|3º TRIMESTRE|4º TRIMESTRE|  
   |-|--------|--------|--------|--------|  
   |Oeste|500|550|550|600|  
   |Leste|600|625|675|700|  
   |Centro-Norte|450|470|490|510|  
   |Sul da Índia|800|750|775|790|  

   Em seguida, adicione um gráfico para a primeira planilha para exibir os dados.  

### <a name="to-add-a-chart-in-excel"></a>Para adicionar um gráfico no Excel  

1.  No **inserir** guia, o **gráficos** , clique em **coluna**e, em seguida, clique em **todos os tipos de gráfico**.  

2.  No **Inserir gráfico** caixa de diálogo, clique em **Okey**.  

3.  No **Design** guia, o **dados** , clique em **selecionar dados**.  

4.  No **Selecionar fonte de dados** caixa de diálogo, clique no **Chartdata intervalo** caixa e limpar qualquer seleção padrão.  

5.  No **dados de gráfico** da folha, selecione o bloco de células que contém os números, que inclui A4 no canto superior esquerdo para E8 no canto inferior direito.  

6.  No **Selecionar fonte de dados** caixa de diálogo, clique em **Okey**.  

7.  Reposicionar o gráfico de forma que o canto superior direito se alinha com a célula **E2**.  

8.  Salve o arquivo para a unidade C e o nomeie **ExcelChart.xlsx**.  

9. Saia do Excel.  

## <a name="create-a-new-project"></a>Criar um novo projeto  
 Nesta etapa, você criará um projeto de pasta de trabalho do Excel com base nas **ExcelChart** pasta de trabalho.  

### <a name="to-create-a-new-project"></a>Para criar um novo projeto  

1.  Criar um projeto de pasta de trabalho do Excel com o nome **meu gráfico do Excel**. No assistente, selecione **copiar um documento existente**.  

     Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  

2.  Clique o **procurar** botão e navegue até a pasta de trabalho que você criou anteriormente neste passo a passo.  

3.  Clique em **OK**.  

     Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o **meu gráfico do Excel** projeto ao **Gerenciador de soluções**.  

## <a name="set-properties-of-the-chart"></a>Definir propriedades do gráfico  
 Quando você cria um novo projeto de pasta de trabalho do Excel que usa uma pasta de trabalho, controles de host são criados automaticamente para os intervalos nomeados de todos os objetos da lista e gráficos na pasta de trabalho. Você pode alterar o nome da <xref:Microsoft.Office.Tools.Excel.Chart> controle usando o **propriedades** janela.  

### <a name="to-change-the-name-of-the-chart-control"></a>Para alterar o nome do controle do gráfico  

1.  Selecione o <xref:Microsoft.Office.Tools.Excel.Chart> no designer de controle e alterar as propriedades a seguir na **propriedades** janela.  

    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**dataChart**|  
    |**HasLegend**|**false**|  

## <a name="add-controls"></a>Adicionar controles  
 Essa planilha usa os botões de opção para dar aos usuários uma maneira de alterar rapidamente o estilo do gráfico. No entanto, os botões de opção precisam ser exclusivo — quando um botão é selecionado, nenhum outro botão no grupo pode ser selecionado ao mesmo tempo. Esse comportamento não acontece por padrão quando você adiciona vários botões de opção em uma planilha.  

 Uma maneira de adicionar esse comportamento é agrupar os botões de opção em um controle de usuário, escreva seu código por trás do controle de usuário e, em seguida, adicionar o controle de usuário à planilha.  

### <a name="to-add-a-user-control"></a>Para adicionar um controle de usuário  

1.  Selecione o **meu gráfico do Excel** project no **Gerenciador de soluções**.  

2.  No menu **Projeto**, clique em **Adicionar Novo Item**.  

3.  No **Adicionar Novo Item** caixa de diálogo, clique em **controle de usuário**, nomeie o controle **ChartOptions** e clique em **adicionar**.  

### <a name="to-add-radio-buttons-to-the-user-control"></a>Para adicionar botões de opção ao controle de usuário  

1. Se o controle de usuário não estiver visível no designer, clique duas vezes **ChartOptions** na **Gerenciador de soluções**.  

2. Dos **controles comuns** guia da **caixa de ferramentas**, arraste uma **botão de opção** o controle para o controle de usuário e alterar as propriedades a seguir.  


   | Propriedade | Valor |
   |----------|------------------|
   | **Nome** | **columnChart** |
   | **Texto** | **Gráfico de colunas** |


3. Adicionar um segundo botão de opção ao controle de usuário e alterar as propriedades a seguir.  


   | Propriedade | Valor |
   |----------|---------------|
   | **Nome** | **barChart** |
   | **Texto** | **Gráfico de barras** |


4. Adicionar um terceiro botão de opção ao controle de usuário e alterar as propriedades a seguir.  


   | Propriedade | Valor |
   |----------|----------------|
   | **Nome** | **lineChart** |
   | **Texto** | **Gráfico de linhas** |


5. Adicionar um quarto botão de opção ao controle de usuário e alterar as propriedades a seguir.  

   |Propriedade|Valor|  
   |--------------|-----------|  
   |**Nome**|**areaBlockChart**|  
   |**Texto**|**Gráfico de blocos de área**|  

   Em seguida, escreva o código para atualizar o gráfico quando um botão de opção é clicado.  

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>Alterar o estilo do gráfico quando um botão de opção está selecionado  
 Agora você pode adicionar o código para alterar o estilo do gráfico. Para fazer isso, crie um evento público no controle de usuário, adicione uma propriedade para definir o tipo de seleção e crie um manipulador de eventos para o `CheckedChanged` eventos de cada um dos botões de opção.  

### <a name="to-create-an-event-and-property-on-a-user-control"></a>Para criar um evento e uma propriedade em um controle de usuário  

1.  Na **Gerenciador de soluções**, clique com botão direito no controle de usuário e, em seguida, clique em **Exibir código**.  

2.  Adicione código para o `ChartOptions` classe para criar um `SelectionChanged` evento e o `Selection` propriedade.  

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#13](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#13)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#13](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#13)]  

### <a name="to-handle-the-checkedchanged-event-of-the-radio-buttons"></a>Para manipular o evento CheckedChanged dos botões de opção  

1.  Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `areaBlockChart` e, em seguida, gere o evento.  

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#14](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#14)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#14](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#14)]  

2.  Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `barChart`.  

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#15](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#15)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#15](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#15)]  

3.  Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `columnChart`.  

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#16](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#16)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#16](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#16)]  

4.  Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `lineChart`.  

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#17](../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb#17)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#17](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#17)]  

5.  No C#, é necessário adicionar manipuladores de eventos aos botões de opção. É possível adicionar o código ao construtor `ChartOptions`, abaixo da chamada para `InitializeComponent`. Para obter informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  

     [!code-cs[Trin_VstcoreProgrammingControlsExcel#18](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs#18)]  

## <a name="add-the-user-control-to-the-worksheet"></a>Adicionar o controle de usuário à planilha  
 Quando você compila a solução, o novo controle de usuário é adicionado automaticamente para o **caixa de ferramentas**. Em seguida, você pode arrastar o controle a partir o **caixa de ferramentas** à sua planilha.  

### <a name="to-add-the-user-control-your-worksheet"></a>Para adicionar o controle de usuário em sua planilha  

1.  No menu **Compilar**, clique em **Compilar Solução**.  

     O **ChartOptions** controle de usuário é adicionado para o **caixa de ferramentas**.  

2.  Na **Gerenciador de soluções**, clique com botão direito **Sheet1.vb** ou **Sheet1.cs**e, em seguida, clique em **View Designer**.  

3.  Arraste o **ChartOptions** controlar da **caixa de ferramentas** à planilha.  

     Um novo controle chamado `my_Excel_Chart_ChartOptions1` é adicionado ao seu projeto.  

4.  Altere o nome do controle a ser **ChartOptions1**.  

## <a name="change-the-chart-type"></a>Alterar o tipo de gráfico  
 Para alterar o tipo de gráfico, crie um manipulador de eventos que define o estilo de acordo com a opção selecionada no controle de usuário.  

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-worksheet"></a>Para alterar o tipo de gráfico que é exibido na planilha  

1.  Adicione o manipulador de eventos a seguir à classe `Sheet1`.  

     [!code-vb[Trin_VstcoreProgrammingControlsExcel#19](../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb#19)]
     [!code-cs[Trin_VstcoreProgrammingControlsExcel#19](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#19)]  

2.  No c#, você deve adicionar um manipulador de eventos para o controle de usuário para o <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> evento, conforme mostrado abaixo. Para obter informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  

     [!code-cs[Trin_VstcoreProgrammingControlsExcel#20](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs#20)]  

## <a name="test-the-application"></a>Testar o aplicativo  
 Agora você pode testar sua pasta de trabalho para verificar que o gráfico é estilizado corretamente quando você seleciona um botão de opção.  

### <a name="to-test-your-workbook"></a>Para testar a sua pasta de trabalho  

1.  Pressione **F5** para executar o projeto.  

2.  Selecione diversos botões de opção.  

3.  Confirme se as alterações no estilo gráfico correspondem à seleção.  

## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo mostra as Noções básicas de como usar os botões de opção e estilos de gráfico em planilhas. Estas são algumas tarefas que podem vir a seguir:  

-   Implantar o projeto. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  

-   Usar um botão para preencher uma caixa de texto. Para obter mais informações, consulte [instruções passo a passo: exibir texto em uma caixa de texto em uma planilha usando um botão](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md).  

-   Alterar a formatação em uma planilha usando as caixas de seleção. Para obter mais informações, consulte [instruções passo a passo: formatação de planilha de alteração usando controles CheckBox](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md).  

## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo usando o Excel](../vsto/walkthroughs-using-excel.md)  


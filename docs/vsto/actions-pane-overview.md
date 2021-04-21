---
title: Visão geral do painel Ações
description: Saiba como um painel Ações é um painel de tarefas de ações de documento personalizável que é anexado a um documento Microsoft Office do Word específico ou a uma pasta de trabalho do Excel.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- actions panes [Office development in Visual Studio], about actions panes
- actions panes [Office development in Visual Studio]
- smart documents [Office development in Visual Studio]
- user controls [Office development in Visual Studio], actions panes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 61e7ab9f00db6036d3bc8e41b9a2f19cf51f5511
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828144"
---
# <a name="actions-pane-overview"></a>Visão geral do painel Ações
  Um painel Ações é um painel de tarefas de **ações de documento** personalizável que é anexado a um documento do Word Microsoft Office específico ou Microsoft Office pasta de trabalho do Excel. O painel Ações é hospedado no painel de tarefas do Office junto com outros painéis de tarefas internos, como o painel de tarefas **origem XML** no Excel ou o painel de tarefas **estilos e formatação** no Word. Você pode usar controles de Windows Forms ou controles WPF para criar a interface do usuário do painel Ações.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Você pode criar um painel de ações somente em uma personalização no nível do documento do Word ou Excel. Você não pode criar um painel de ações em um suplemento do VSTO. Para obter mais informações, consulte [recursos disponíveis por aplicativo do Office e tipo de projeto](../vsto/features-available-by-office-application-and-project-type.md).

> [!NOTE]
> O painel Ações difere dos painéis de tarefas personalizados. Os painéis de tarefas personalizados são associados ao aplicativo, não a um documento específico. Você pode criar painéis de tarefas personalizados em suplementos do VSTO para alguns Microsoft Office aplicativos. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).

## <a name="display-the-actions-pane"></a>Exibir o painel Ações
 O painel Ações é representado pela <xref:Microsoft.Office.Tools.ActionsPane> classe. Quando você cria um projeto de nível de documento, uma instância dessa classe está disponível para seu código usando o `ActionsPane` campo da `ThisWorkbook` classe (para Excel) ou `ThisDocument` (para Word) em seu projeto. Para exibir o painel Ações, adicione um controle de Windows Forms à <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> Propriedade do `ActionsPane` campo. O exemplo de código a seguir adiciona um controle chamado `actions` ao painel Ações.

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet7":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet7":::

 O painel ações se torna visível em tempo de execução assim que você adiciona explicitamente um controle a ele. Depois que o painel Ações for exibido, você poderá adicionar ou remover dinamicamente os controles em resposta às ações do usuário. Normalmente, você adiciona o código para exibir o painel Ações no `Startup` manipulador de eventos do `ThisDocument` ou `ThisWorkbook` para que o painel Ações fique visível quando o usuário abrir o documento pela primeira vez. No entanto, talvez você queira exibir o painel Ações somente em resposta à ação de um usuário no documento. Por exemplo, você pode adicionar o código ao `Click` evento de um controle no documento.

### <a name="add-multiple-controls-to-the-actions-pane"></a>Adicionar vários controles ao painel Ações
 Quando você adiciona vários controles ao painel Ações, deve agrupar os controles em um controle de usuário e, em seguida, adicionar o controle de usuário à <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> propriedade. Este processo inclui as seguintes etapas:

1. Crie a interface do usuário (IU) do painel Ações adicionando um **controle painel de ações** ou um item de **controle de usuário** ao seu projeto. Ambos os dois itens incluem uma classe de Windows Forms personalizada <xref:System.Windows.Forms.UserControl> . O **controle do painel Ações** e os itens de **controle de usuário** são equivalentes; a única diferença é seu nome.

2. Adicione controles de Windows Forms ao <xref:System.Windows.Forms.UserControl> usando o designer ou escrevendo código.

   > [!NOTE]
   > Você também pode adicionar controles WPF ao painel Ações adicionando um WPF <xref:System.Windows.Controls.UserControl> ao Windows Forms <xref:System.Windows.Forms.UserControl> . Para obter mais informações, consulte [usar controles WPF em soluções do Office](../vsto/using-wpf-controls-in-office-solutions.md).

3. Adicione uma instância do controle de usuário personalizado aos controles contidos no `ActionsPane` campo da `ThisWorkbook` classe (para Excel) ou `ThisDocument` (para Word) em seu projeto.

   Para obter exemplos que demonstram esse processo mais detalhadamente, consulte [como adicionar um painel ações a documentos do Word ou pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md).

## <a name="hide-the-actions-pane"></a>Ocultar o painel Ações
 Embora a <xref:Microsoft.Office.Tools.ActionsPane> classe tenha um <xref:Microsoft.Office.Tools.ActionsPane.Hide%2A> método e uma <xref:Microsoft.Office.Tools.ActionsPane.Visible%2A> propriedade, você não pode remover o painel ações da interface do usuário usando todos os membros da <xref:Microsoft.Office.Tools.ActionsPane> própria classe. Chamar o <xref:Microsoft.Office.Tools.ActionsPane.Hide%2A> método ou definir a <xref:Microsoft.Office.Tools.ActionsPane.Visible%2A> propriedade como **false** oculta somente os controles no painel Ações; ele não oculta o painel de tarefas.

 Para ocultar o painel de tarefas em sua solução, você tem várias opções:

- Para o Word, defina a <xref:Microsoft.Office.Interop.Word.TaskPane.Visible%2A> Propriedade do <xref:Microsoft.Office.Interop.Word.TaskPane> objeto que representa o painel de tarefas ações do documento como **falso**. O exemplo de código a seguir deve ser executado da `ThisDocument` classe em seu projeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet34":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet34":::

- Para o Excel, defina a <xref:Microsoft.Office.Interop.Excel._Application.DisplayDocumentActionTaskPane%2A> Propriedade do <xref:Microsoft.Office.Tools.Excel.Workbook.Application%2A> objeto como **false**. O exemplo de código a seguir deve ser executado da `ThisWorkbook` classe em seu projeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet11":::

- Para o Word ou Excel, você pode definir como alternativa a <xref:Microsoft.Office.Core.CommandBar.Visible%2A> propriedade da barra de comandos que representa o painel de tarefas como **false**. O exemplo de código a seguir deve ser executado a partir `ThisDocument` da `ThisWorkbook` classe ou no seu projeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet9":::

### <a name="clear-the-actions-pane-when-the-document-is-opened"></a>Limpar o painel ações quando o documento é aberto
 Quando um usuário salva o documento enquanto o painel Ações está visível, o painel Ações fica visível toda vez que o documento é aberto, independentemente de o painel Ações conter ou não controles. Se você quiser controlar quando ele aparece, chame o <xref:Microsoft.Office.Tools.ActionsPane.Clear%2A> método do `ActionsPane` campo no `Startup` manipulador de eventos do `ThisDocument` ou `ThisWorkbook` para garantir que o painel ações não esteja visível quando o documento for aberto.

### <a name="determine-when-the-actions-pane-is-closed"></a>Determinar quando o painel de ações é fechado
 Não há evento que seja gerado quando o painel Ações for fechado. Embora a <xref:Microsoft.Office.Tools.ActionsPane> classe tenha um <xref:Microsoft.Office.Tools.ActionsPane.VisibleChanged> evento, esse evento não é gerado quando o usuário final fecha o painel Ações. Em vez disso, esse evento é gerado quando os controles no painel ações são ocultados chamando o <xref:Microsoft.Office.Tools.ActionsPane.Hide%2A> método ou definindo a <xref:Microsoft.Office.Tools.ActionsPane.Visible%2A> propriedade como **false**.

 Quando o usuário fecha o painel Ações, o usuário pode exibi-lo novamente executando um dos procedimentos a seguir na interface do usuário do aplicativo.

##### <a name="to-display-the-actions-pane-by-using-the-ui-of-word-or-excel"></a>Para exibir o painel ações usando a interface do usuário do Word ou Excel

1. Na faixa de visão, clique na guia **Exibir** .

2. No grupo **Mostrar/ocultar** , clique no botão de alternância **ações do documento** .

## <a name="program-actions-pane-events"></a>Eventos do painel Ações do programa
 Você pode adicionar vários controles de usuário ao painel Ações e, em seguida, escrever código para responder a eventos no documento mostrando e ocultando os controles de usuário. Se você mapear elementos de esquema XML para o documento, poderá mostrar determinados controles de usuário no painel ações sempre que o ponto de inserção estiver dentro de um dos elementos XML. Para obter mais informações, consulte [como Mapear esquemas para documentos do Word dentro do Visual Studio](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md) e [como Mapear esquemas para planilhas dentro do Visual Studio](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md).

 Você também pode escrever código para responder aos eventos de qualquer objeto, incluindo eventos de controle de host, aplicativo ou documento. Para obter mais informações, consulte [Walkthrough: programa em relação a eventos de um controle NamedRange](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md).

## <a name="bind-data-to-controls-on-the-actions-pane"></a>Associar dados a controles no painel Ações
 Os controles no painel Ações têm os mesmos recursos de vinculação de dados que os controles em Windows Forms. Você pode associar os controles a fontes de dados, como conjuntos de dados, conjuntos de dados tipados e XML. Para obter mais informações, consulte [vinculação de dados e Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms).

 Você pode associar controles no painel Ações e controles no documento para o mesmo conjunto de mesmos. Por exemplo, você pode criar uma relação de mestre/detalhes entre os controles no painel Ações e os controles na planilha. Para obter mais informações, consulte [Walkthrough: associar dados a controles em um painel de ações do Excel](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md).

## <a name="validate-data-in-actions-pane-controls"></a>Validar dados em controles do painel Ações
 Se você exibir uma caixa de mensagem no <xref:System.Windows.Forms.Control.Validating> manipulador de eventos de um controle no painel Ações, o evento poderá ser gerado uma segunda vez quando o foco for movido do controle para a caixa de mensagem. Para evitar esse problema, use um <xref:System.Windows.Forms.ErrorProvider> controle para exibir todas as mensagens de erro de validação.

## <a name="user-control-stacking-order"></a>Ordem de empilhamento de controle de usuário
 Se você estiver usando vários controles de usuário, poderá escrever código para empilhar corretamente os controles de usuário no painel ações se ele estiver encaixado verticalmente ou horizontalmente. Você pode definir a ordem de empilhamento dos controles de usuário no painel ações usando a <xref:Microsoft.Office.Tools.StackStyle> enumeração da <xref:Microsoft.Office.Tools.ActionsPane.StackOrder%2A> propriedade. Para obter mais informações, consulte [como: gerenciar o layout de controle em painéis de ações](../vsto/how-to-manage-control-layout-on-actions-panes.md).

 A <xref:Microsoft.Office.Tools.ActionsPane.StackOrder%2A> propriedade pode assumir os valores de enumeração a seguir <xref:Microsoft.Office.Tools.StackStyle> .

|Estilo de empilhamento|Definição|
|--------------------|----------------|
|FromBottom|Empilhar na parte inferior do painel de ações.|
|FromLeft|Empilhar na parte esquerda do painel de ações.|
|FromRight|Empilhar na parte direita do painel de ações.|
|FromTop|Empilhar na parte superior do painel de ações.|
|Nenhum|Nenhuma ordem de empilhamento definida, a ordem é controlada pelo desenvolvedor.|

 O código a seguir define a <xref:Microsoft.Office.Tools.ActionsPane.StackOrder%2A> propriedade para empilhar os controles de usuário da parte superior do painel Ações.

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet10":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet10":::

## <a name="anchor-controls"></a>Controles de âncora
 Se o usuário redimensionar o painel Ações em tempo de execução, os controles poderão ser redimensionados com o painel Ações. Você pode usar a <xref:System.Windows.Forms.Control.Anchor%2A> propriedade de um controle de Windows Forms para ancorar controles no painel Ações. Você também pode ancorar os controles de Windows Forms no controle de usuário da mesma maneira. Para obter mais informações, consulte [como: ancorar controles em Windows Forms](/dotnet/framework/winforms/controls/how-to-anchor-controls-on-windows-forms).

## <a name="resize-the-actions-pane"></a>Redimensionar o painel Ações
 Não é possível alterar diretamente o tamanho de um <xref:Microsoft.Office.Tools.ActionsPane> porque o <xref:Microsoft.Office.Tools.ActionsPane> está inserido no painel de tarefas. No entanto, você pode alterar programaticamente a largura do painel de tarefas definindo a <xref:Microsoft.Office.Core.CommandBar.Width%2A> Propriedade do <xref:Microsoft.Office.Core.CommandBar> que representa o painel de tarefas. Você pode alterar a altura do painel de tarefas se ele estiver encaixado horizontalmente ou flutuando.

 O redimensionamento programático do painel de tarefas não é recomendado porque o usuário deve ser capaz de selecionar o tamanho do painel de tarefas que melhor atenda às suas necessidades. No entanto, se for necessário redimensionar a largura do painel de tarefas, você poderá usar o código a seguir para obter essa tarefa.

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet102":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet102":::

## <a name="reposition-the-actions-pane"></a>Reposicionar o painel Ações
 Não é possível reposicionar diretamente o <xref:Microsoft.Office.Tools.ActionsPane> porque ele está inserido no painel de tarefas. No entanto, você pode mover o painel de tarefas programaticamente definindo a <xref:Microsoft.Office.Core.CommandBar.Position%2A> Propriedade do <xref:Microsoft.Office.Core.CommandBar> que representa o painel de tarefas.

 O reposicionamento programático do painel de tarefas não é recomendado porque o usuário deve ser capaz de escolher a posição do painel de tarefas na tela que melhor atenda às suas necessidades. No entanto, se for necessário mover o painel de tarefas para uma determinada posição, você poderá usar o código a seguir para obter essa tarefa.

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet100":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet100":::

> [!NOTE]
> Os usuários finais podem reposicionar manualmente o painel de tarefas a qualquer momento. Não há como garantir que o painel de tarefas permanecerá encaixado na posição que você indicar programaticamente. No entanto, você pode verificar se há alterações de orientação e garantir que os controles no painel ações sejam empilhados na direção correta. Para obter mais informações, consulte [como: gerenciar o layout de controle em painéis de ações](../vsto/how-to-manage-control-layout-on-actions-panes.md).

 Definir as <xref:Microsoft.Office.Tools.ActionsPane.Top%2A> <xref:Microsoft.Office.Tools.ActionsPane.Left%2A> Propriedades e de <xref:Microsoft.Office.Tools.ActionsPane> não altera sua posição porque o <xref:Microsoft.Office.Tools.ActionsPane> objeto está inserido no painel de tarefas.

 Se o painel de tarefas não estiver encaixado, você poderá definir as <xref:Microsoft.Office.Core.CommandBar.Top%2A> <xref:Microsoft.Office.Core.CommandBar.Left%2A> Propriedades e do <xref:Microsoft.Office.Core.CommandBar> que representa o painel de tarefas. O código a seguir move um painel de tarefas desencaixado para o canto superior esquerdo do documento.

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet101":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet101":::

## <a name="see-also"></a>Consulte também
- [Usar controles WPF em soluções do Office](../vsto/using-wpf-controls-in-office-solutions.md)
- [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)
- [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)
- [Como: adicionar um painel de ações a documentos do Word ou a pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [Walkthrough: inserir texto em um documento a partir de um painel Ações](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [Walkthrough: associar dados a controles em um painel de ações do Word](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)
- [Walkthrough: associar dados a controles em um painel de ações do Excel](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)
- [Como: gerenciar o layout de controle em painéis de ações](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [Walkthrough: inserir texto em um documento a partir de um painel Ações](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)

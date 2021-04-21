---
title: 'Walkthrough: programa em relação a eventos de um controle NamedRange'
description: Saiba como você pode adicionar um controle NamedRange a uma planilha e programa do Microsoft Excel em relação a seus eventos usando as ferramentas de desenvolvimento do Office no Visual Studio.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, programming against events
- worksheets, changing cell values
- NamedRange control, events
- worksheets, events
- worksheets, automating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ec1c670867fae277a3c3c8290cd34d0d4be7ddf3
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824959"
---
# <a name="walkthrough-program-against-events-of-a-namedrange-control"></a>Walkthrough: programa em relação a eventos de um controle NamedRange
  Este tutorial demonstra como adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle a uma Microsoft Office planilha e programa do Excel em relação a seus eventos usando as ferramentas de desenvolvimento do Office no Visual Studio.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Durante este passo a passo, você aprenderá a:

- Adicione um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle a uma planilha.

- Programa contra <xref:Microsoft.Office.Tools.Excel.NamedRange> eventos de controle.

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

1. Crie um projeto de pasta de trabalho do Excel com o nome **meus eventos de intervalo nomeado**. Verifique se **a seleção criar um novo documento** está selecionada. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o projeto **meus eventos de intervalo nomeado** ao **Gerenciador de soluções**.

## <a name="add-text-and-named-ranges-to-the-worksheet"></a>Adicionar texto e intervalos nomeados à planilha
 Como os controles de host são objetos estendidos do Office, você pode adicioná-los ao documento da mesma maneira que adicionaria o objeto nativo. Por exemplo, você pode adicionar um controle do Excel <xref:Microsoft.Office.Tools.Excel.NamedRange> a uma planilha abrindo o **menu Inserir** , apontando para **nome** e escolhendo **definir**. Você também pode adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle arrastando-o da **caixa de ferramentas** para a planilha.

 Nesta etapa, você adicionará dois controles de intervalo nomeados à planilha usando a **caixa de ferramentas** e, em seguida, adicionará texto à planilha.

### <a name="to-add-a-range-to-your-worksheet"></a>Para adicionar um intervalo à sua planilha

1. Verifique se o *meu intervalo nomeado* pasta de trabalho Events.xlsxestá aberto no designer do Visual Studio, com `Sheet1` exibido.

2. Na guia **controles do Excel** da caixa de ferramentas, arraste um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle para a célula **a1** em `Sheet1` .

     A caixa de diálogo **Adicionar controle de NamedRange** é exibida.

3. Verifique se **$A $1** aparece na caixa de texto editável e se a célula **a1** está selecionada. Se não estiver, clique na célula **a1** para selecioná-la.

4. Clique em **OK**.

     A célula **a1** se torna um intervalo chamado `namedRange1` . Não há nenhuma indicação visível na planilha, mas `namedRange1` aparece na caixa **nome** (localizada logo acima da planilha no lado esquerdo) quando a célula **a1** é selecionada.

5. Adicione outro <xref:Microsoft.Office.Tools.Excel.NamedRange> controle à célula **B3**.

6. Verifique se **$B $3** aparece na caixa de texto editável e se a célula **B3** está selecionada. Se não estiver, clique na célula **B3** para selecioná-la.

7. Clique em **OK**.

     A célula **B3** torna-se um intervalo chamado `namedRange2` .

### <a name="to-add-text-to-your-worksheet"></a>Para adicionar texto à sua planilha

1. Na célula **a1**, digite o seguinte texto:

    **Este é um exemplo de um controle NamedRange.**

2. Na célula **a3** (à esquerda de `namedRange2` ), digite o seguinte texto:

    **LostFocus**

   Nas seções a seguir, você escreverá um código que insere texto em `namedRange2` e modifica as propriedades do `namedRange2` controle em resposta aos <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> eventos, <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> e <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> de `namedRange1` .

## <a name="add-code-to-respond-to-the-beforedoubleclick-event"></a>Adicionar código para responder ao evento BeforeDoubleClick

### <a name="to-insert-text-into-namedrange2-based-on-the-beforedoubleclick-event"></a>Para inserir texto em NamedRange2 com base no evento BeforeDoubleClick

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **Plan1. vb** ou **Plan1. cs** e selecione **Exibir código**.

2. Adicione o código para que o `namedRange1_BeforeDoubleClick` manipulador de eventos fique semelhante ao seguinte:

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet24":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet24":::

3. No C#, você deve adicionar manipuladores de eventos para o intervalo nomeado, conforme mostrado no <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> evento abaixo. Para obter informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet25":::

## <a name="add-code-to-respond-to-the-change-event"></a>Adicionar código para responder ao evento de alteração

### <a name="to-insert-text-into-namedrange2-based-on-the-change-event"></a>Para inserir texto em namedRange2 com base no evento de alteração

1. Adicione o código para que o `NamedRange1_Change` manipulador de eventos fique semelhante ao seguinte:

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet26":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet26":::

    > [!NOTE]
    > Como clicar duas vezes em uma célula em um intervalo do Excel entra no modo de edição, um <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> evento ocorre quando a seleção é movida para fora do intervalo, mesmo que nenhuma alteração no texto tenha ocorrido.

## <a name="add-code-to-respond-to-the-selectionchange-event"></a>Adicionar código para responder ao evento SelectionChange

### <a name="to-insert-text-into-namedrange2-based-on-the-selectionchange-event"></a>Para inserir texto em namedRange2 com base no evento SelectionChange

1. Adicione o código para que o manipulador de eventos de **NamedRange1_SelectionChange** se pareça com o seguinte:

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet27":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet27":::

    > [!NOTE]
    > Como clicar duas vezes em uma célula em um intervalo do Excel faz com que a seleção seja movida para o intervalo, um <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> evento ocorre antes do <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> evento ocorrer.

## <a name="test-the-application"></a>Testar o aplicativo
 Agora você pode testar sua pasta de trabalho para verificar se o texto que descreve os eventos de um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle é inserido em outro intervalo nomeado quando os eventos são gerados.

### <a name="to-test-your-document"></a>Para testar o documento

1. Pressione **F5** para executar o projeto.

2. Coloque o cursor em `namedRange1` e verifique se o texto referente ao <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> evento é inserido e se um comentário é inserido na planilha.

3. Clique duas vezes dentro `namedRange1` e verifique se o texto referente a <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> eventos é inserido com texto em itálico vermelho em `namedRange2` .

4. Clique fora do `namedRange1` e observe que o evento de alteração ocorre ao sair do modo de edição, embora nenhuma alteração no texto tenha sido feita.

5. Altere o texto em `namedRange1` .

6. Clique fora do e `namedRange1` Verifique se o texto referente ao <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> evento é inserido com texto azul no `namedRange2` .

## <a name="next-steps"></a>Próximas etapas
 Este tutorial mostra as noções básicas de programação em relação a eventos de um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle. Aqui está uma tarefa que pode vir a seguir:

- Implantando o projeto. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).

## <a name="see-also"></a>Consulte também
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Controle NamedRange](../vsto/namedrange-control.md)
- [Como: redimensionar controles NamedRange](../vsto/how-to-resize-namedrange-controls.md)
- [Como: adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md)

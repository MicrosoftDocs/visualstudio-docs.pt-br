---
title: 'Passo a passo: Programa contra eventos de um controle NamedRange'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 3f8b55cda9576a0203857b3fdaeccbb205b42168
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812512"
---
# <a name="walkthrough-program-against-events-of-a-namedrange-control"></a>Passo a passo: Programa contra eventos de um controle NamedRange
  Este passo a passo demonstra como adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle para uma planilha do Microsoft Office Excel e o programa em relação a seus eventos, usando ferramentas de desenvolvimento do Office no Visual Studio.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 Durante este passo a passo, você aprenderá a:  
  
-   Adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle em uma planilha.  
  
-   Programar <xref:Microsoft.Office.Tools.Excel.NamedRange> controlar eventos.  
  
-   Teste seu projeto.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].  
  
## <a name="create-the-project"></a>Criar o projeto  
 Nesta etapa, você criará um projeto de pasta de trabalho do Excel usando o Visual Studio.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de pasta de trabalho do Excel com o nome **Meus eventos de intervalo nomeado**. Certifique-se de que **criar um novo documento** está selecionado. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o **Meus eventos de intervalo nomeado** projeto ao **Gerenciador de soluções**.  
  
## <a name="add-text-and-named-ranges-to-the-worksheet"></a>Adicionar texto e intervalos nomeados para a planilha  
 Como hospedar controles são estendidos de objetos do Office, você pode adicioná-los ao documento da mesma maneira, você adicionaria o objeto nativo. Por exemplo, você pode adicionar um Excel <xref:Microsoft.Office.Tools.Excel.NamedRange> controle em uma planilha, abrindo o **inserir** menu, apontando para **nome**e escolhendo **definir**. Você também pode adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle arrastando-o do **caixa de ferramentas** na planilha.  
  
 Nesta etapa, você adicionará dois controles de intervalo nomeado para a planilha usando o **caixa de ferramentas**e, em seguida, adicionar texto à planilha.  
  
### <a name="to-add-a-range-to-your-worksheet"></a>Para adicionar um intervalo à sua planilha  
  
1.  Verifique se que o *Meus Events.xlsx de intervalo nomeado* pasta de trabalho é aberta no designer do Visual Studio, com `Sheet1` exibido.  
  
2.  Do **controles do Excel** guia de ferramentas, arraste um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle a célula **A1** em `Sheet1`.  
  
     O **adicionar NamedRange controle** caixa de diálogo é exibida.  
  
3.  Verifique **$A$ 1** aparece na caixa de texto editável e que a célula **A1** está selecionado. Se não estiver, clique na célula **A1** para selecioná-lo.  
  
4.  Clique em **OK**.  
  
     Célula **A1** torna-se um intervalo nomeado `namedRange1`. Não há nenhuma indicação visível na planilha, mas `namedRange1` aparece na **nome** caixa (localizada imediatamente acima da planilha no lado esquerdo) quando a célula **A1** está selecionado.  
  
5.  Adicione outro <xref:Microsoft.Office.Tools.Excel.NamedRange> controle a célula **B3**.  
  
6.  Verifique **$B US $3** aparece na caixa de texto editável e que a célula **B3** está selecionado. Se não estiver, clique na célula **B3** para selecioná-lo.  
  
7.  Clique em **OK**.  
  
     Célula **B3** torna-se um intervalo nomeado `namedRange2`.  
  
### <a name="to-add-text-to-your-worksheet"></a>Para adicionar texto à sua planilha  
  
1. Na célula **A1**, digite o seguinte texto:  
  
    **Este é um exemplo de um controle NamedRange.**  
  
2. Na célula **A3** (à esquerda do `namedRange2`), digite o seguinte texto:  
  
    **Eventos:**  
  
   As seções a seguir, você irá escrever código que insere o texto no `namedRange2` e modifica as propriedades do `namedRange2` controle em resposta ao <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick>, <xref:Microsoft.Office.Tools.Excel.NamedRange.Change>, e <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> eventos de `namedRange1`.  
  
## <a name="add-code-to-respond-to-the-beforedoubleclick-event"></a>Adicione código para responder ao evento BeforeDoubleClick  
  
### <a name="to-insert-text-into-namedrange2-based-on-the-beforedoubleclick-event"></a>Para inserir texto em NamedRange2 baseado no evento BeforeDoubleClick  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **Sheet1.vb** ou **Sheet1.cs** e selecione **Exibir código**.  
  
2.  Adicione código para que o `namedRange1_BeforeDoubleClick` manipulador de eventos é semelhante ao seguinte:  
  
     [!code-csharp[Trin_VstcoreHostControlsExcel#24](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#24)]
     [!code-vb[Trin_VstcoreHostControlsExcel#24](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#24)]  
  
3.  No c#, você deve adicionar manipuladores de eventos para o intervalo nomeado conforme o <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> evento abaixo. Para obter informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  
  
     [!code-csharp[Trin_VstcoreHostControlsExcel#25](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#25)]  
  
## <a name="add-code-to-respond-to-the-change-event"></a>Adicionar código para responder ao evento de alteração  
  
### <a name="to-insert-text-into-namedrange2-based-on-the-change-event"></a>Para inserir texto em namedRange2 com base no evento de alteração  
  
1.  Adicione código para que o `NamedRange1_Change` manipulador de eventos é semelhante ao seguinte:  
  
     [!code-csharp[Trin_VstcoreHostControlsExcel#26](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#26)]
     [!code-vb[Trin_VstcoreHostControlsExcel#26](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#26)]  
  
    > [!NOTE]  
    >  Porque duas vezes em uma célula em um intervalo do Excel entra em modo de edição, um <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> evento ocorre quando a seleção é movida de fora do intervalo, mesmo se nenhuma alteração no texto ocorreu.  
  
## <a name="add-code-to-respond-to-the-selectionchange-event"></a>Adicione código para responder ao evento SelectionChange  
  
### <a name="to-insert-text-into-namedrange2-based-on-the-selectionchange-event"></a>Para inserir texto em namedRange2 baseado no evento SelectionChange  
  
1.  Adicione código para que o **NamedRange1_SelectionChange** manipulador de eventos é semelhante ao seguinte:  
  
     [!code-csharp[Trin_VstcoreHostControlsExcel#27](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#27)]
     [!code-vb[Trin_VstcoreHostControlsExcel#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#27)]  
  
    > [!NOTE]  
    >  Porque duas vezes em uma célula em um intervalo do Excel faz com que a seleção mover para o intervalo, uma <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> evento ocorre antes do <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> evento ocorre.  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Agora você pode testar sua pasta de trabalho para verificar que o texto que descreve os eventos de um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle é inserido em outro intervalo nomeado quando os eventos são gerados.  
  
### <a name="to-test-your-document"></a>Para testar o documento  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Coloque o cursor na `namedRange1`e verificar se o texto em relação a <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> eventos é inserido, e um comentário é inserido na planilha.  
  
3.  Clique duas vezes dentro `namedRange1`, verifique se o texto em relação ao <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> eventos é inserido com o texto em itálico vermelho no `namedRange2`.  
  
4.  Clique fora do `namedRange1` e observe que o evento de alteração ocorre quando você sair do modo de edição, embora não foi feita nenhuma alteração no texto.  
  
5.  Alterar o texto dentro do `namedRange1`.  
  
6.  Clicar fora da `namedRange1`, verifique se o texto em relação ao <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> eventos é inserido com o texto azul em `namedRange2`.  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo mostra as Noções básicas de programação em eventos de um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle. Aqui está uma tarefa que pode vir a seguir:  
  
-   Implantar o projeto. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)   
 [Controle NamedRange](../vsto/namedrange-control.md)   
 [Como: redimensionar controles NamedRange](../vsto/how-to-resize-namedrange-controls.md)   
 [Como: adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md)  
  
  
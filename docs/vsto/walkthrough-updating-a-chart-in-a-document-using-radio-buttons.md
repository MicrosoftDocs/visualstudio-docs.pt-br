---
title: 'Explicação passo a passo: Um gráfico em um documento usando botões de opção de atualização'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], updating using controls
- controls [Office development in Visual Studio], updating documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5e82c50c83a8824b4570779034b0480aa0615a30
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49904668"
---
# <a name="walkthrough-update-a-chart-in-a-document-using-radio-buttons"></a>Explicação passo a passo: Um gráfico em um documento usando botões de opção de atualização
  Esse passo a passo demonstra como usar os botões de opção em uma personalização ao nível do documento do Microsoft Office Word para fornecer aos usuários a opção de selecionar estilos de gráficos no documento.  
  
 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Adicionar um gráfico ao documento em um projeto ao nível do documento no tempo de design.  
  
- Agrupamento dos botões de opção adicionando-os a um controle de usuário.  
  
- Alterando o estilo do gráfico quando uma opção ser selecionada.  
  
  Para ver o resultado como um exemplo completo, consulte o Word Controls Sample em [exemplos de desenvolvimento do Office e instruções passo a passo](../vsto/office-development-samples-and-walkthroughs.md).  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].  
  
## <a name="create-the-project"></a>Criar o projeto  
 A primeira etapa é criar um projeto de Documento do Word.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de documento do Word com o nome **minhas opções de gráficos**. No assistente, selecione **criar um novo documento**. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     Visual Studio abre o novo documento do Word no designer e adiciona o **minhas opções de gráficos** projeto ao **Gerenciador de soluções**.  
  
## <a name="add-a-chart-to-the-document"></a>Adicionar um gráfico ao documento  
  
### <a name="to-add-a-chart"></a>Para adicionar um gráfico  
  
1.  No documento do Word que está hospedado no designer do Visual Studio, na faixa de opções, clique no **inserir** guia.  
  
2.  No **texto** , clique no **Inserir objeto** botão suspenso e clique em **objeto**.  
  
     O **objeto** caixa de diálogo é aberta.  
  
3.  No **tipo de objeto** lista os **criar nova** guia, selecione **gráfico do Microsoft Graph** e, em seguida, clique em **Okey**.  
  
     Um gráfico é adicionado ao documento no ponto de inserção e o **folha de dados** janela aparece com alguns dados padrão.  
  
4.  Fechar o **folha de dados** janela para aceitar os valores padrão no gráfico e clique dentro do documento para mover o foco para longe do gráfico.  
  
5.  Clique com botão direito do gráfico e, em seguida, clique em **Formatar objeto**.  
  
6.  Sobre o **Layout** guia da **Formatar objeto** caixa de diálogo, selecione **quadrado** e clique em **Okey**.  
  
## <a name="add-a-user-control-to-the-project"></a>Adicionar um controle de usuário ao projeto  
 Os botões de opção em um documento não são mutuamente excludentes por padrão. É possível fazê-los funcionar corretamente adicionando-os a um controle de usuário e, em seguida, escrevendo o código para controlar a seleção.  
  
### <a name="to-add-a-user-control"></a>Para adicionar um controle de usuário  
  
1.  Selecione o **minhas opções de gráficos** project no **Gerenciador de soluções**.  
  
2.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
3.  No **Adicionar Novo Item** caixa de diálogo, clique em **controle de usuário**, nomeie o controle **ChartOptions** e clique em **adicionar**.  
  
### <a name="to-add-windows-form-controls-to-the-user-control"></a>Para adicionar os controles Windows Form ao controle de usuário  
  
1.  Se o controle de usuário não estiver visível no designer, clique duas vezes **ChartOptions** na **Gerenciador de soluções**.  
  
2.  Dos **controles comuns** guia da **caixa de ferramentas**, arraste o primeiro **botão de opção** o controle para o controle de usuário e alterar as propriedades a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**columnChart**|  
    |**Texto**|**Gráfico de colunas**|  
  
3.  Adicione um segundo **botão de opção** ao usuário controlar e alterar as propriedades a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**barChart**|  
    |**Texto**|**Gráfico de barras**|  
  
4.  Adicionar um terceiro **botão de opção** ao usuário controlar e alterar as propriedades a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**lineChart**|  
    |**Texto**|**Gráfico de linhas**|  
  
5.  Adicionar uma quarta **botão de opção** ao usuário controlar e alterar as propriedades a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**areaBlockChart**|  
    |**Texto**|**Gráfico de blocos de área**|  
  
## <a name="add-references"></a>Adicionar referências  
 Para acessar o gráfico de controle de usuário em um documento, você deve ter uma referência para o `Microsoft.Office.Interop.Graph` assembly em seu projeto.  
  
### <a name="to-add-a-reference-to-the-microsoftofficeinteropgraph-assembly"></a>Para adicionar uma referência ao assembly Microsoft.Office.Interop.Graph  
  
1.  No menu **Projeto**, clique em **Adicionar Referência**.  
  
     A caixa de diálogo **Adicionar Referência** é exibida.  
  
2.  Sobre o **.NET** guia, selecione **Microsoft.Office.Interop.Graph** e clique em **Okey**. Selecione a versão 14.0.0.0 do assembly.  
  
## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>Alterar o estilo do gráfico quando um botão de opção está selecionado  
 Para fazer os botões funcionarem corretamente, crie um evento público no controle de usuário, adicione uma propriedade para definir o tipo de seleção e crie um procedimento para o evento `CheckedChanged` de cada um dos botões de opção.  
  
### <a name="to-create-an-event-and-property-on-a-user-control"></a>Para criar um evento e uma propriedade em um controle de usuário  
  
1.  Na **Gerenciador de soluções**, clique com botão direito no controle de usuário e, em seguida, clique em **Exibir código**.  
  
2.  Adicione um código para criar um evento `SelectionChanged` e a propriedade `Selection` à classe `ChartOptions`.  
  
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#9](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#9)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#9](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#9)]  
  
### <a name="to-handle-the-checkedchange-event-of-the-radio-buttons"></a>Para tratar o evento CheckedChange dos botões de opção  
  
1.  Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `areaBlockChart` e, em seguida, gere o evento.  
  
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#10](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#10)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#10](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#10)]  
  
2.  Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `barChart`.  
  
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#11](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#11)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#11](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#11)]  
  
3.  Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `columnChart`.  
  
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#12](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#12)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#12](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#12)]  
  
4.  Defina o tipo de gráfico no manipulador de eventos `CheckedChanged` do botão de opção `lineChart`.  
  
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#13](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#13)]
     [!code-vb[Trin_VstcoreProgrammingControlsWord#13](../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb#13)]  
  
5.  No C#, é necessário adicionar manipuladores de eventos aos botões de opção. É possível adicionar o código ao construtor `ChartOptions`, abaixo da chamada para `InitializeComponent`. Para obter informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  
  
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#14](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs#14)]  
  
## <a name="add-the-user-control-to-the-document"></a>Adicione o controle de usuário ao documento  
 Quando você compila a solução, o novo controle de usuário é adicionado automaticamente para o **caixa de ferramentas**. Você pode, em seguida, arraste o controle dos **caixa de ferramentas** ao documento.  
  
### <a name="to-add-the-user-control-your-document"></a>Para adicionar o controle de usuário ao seu documento  
  
1.  No menu **Compilar**, clique em **Compilar Solução**.  
  
     O **ChartOptions** controle de usuário é adicionado para o **caixa de ferramentas**.  
  
2.  Na **Gerenciador de soluções**, clique com botão direito **ThisDocument. vb** ou **ThisDocument.cs**e, em seguida, clique em **View Designer**.  
  
3.  Arraste o `ChartOptions` controlar do **caixa de ferramentas** ao documento.  
  
     No **propriedades** janela, o nome que o controle recém adicionado ao documento `ChartOptions1`.  
  
## <a name="change-the-chart-type"></a>Alterar o tipo de gráfico  
 Crie um manipulador de eventos para alterar o tipo de gráfico de acordo com a opção selecionada no controle de usuário.  
  
### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-document"></a>Para alterar o tipo de gráfico exibido o documento  
  
1.  Adicione o manipulador de eventos a seguir à classe `ThisDocument`.  
  
     [!code-vb[Trin_VstcoreProgrammingControlsWord#15](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#15)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#15](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#15)]  
  
2.  No C#, é necessário adicionar um manipulador de eventos do controle de usuário ao evento <xref:Microsoft.Office.Tools.Word.Document.Startup>.  
  
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#16](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#16)]  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Agora é possível testar seu documento para certificar-se de que o estilo gráfico está atualizado corretamente ao selecionar um botão de opção.  
  
### <a name="to-test-your-document"></a>Para testar o documento  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Selecione diversos botões de opção.  
  
3.  Confirme se as alterações no estilo gráfico correspondem à seleção.  
  
## <a name="next-steps"></a>Próximas etapas  
 Estas são algumas tarefas que podem vir a seguir:  
  
-   Usar um botão para preencher uma caixa de texto. Para obter mais informações, consulte [instruções passo a passo: exibir texto em uma caixa de texto em um documento usando um botão](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md).  
  
-   Alterar a formatação selecionando um estilo de uma caixa de combinação. Para obter mais informações, consulte [instruções passo a passo: formatação de documento de alteração usando controles CheckBox](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo usando o Word](../vsto/walkthroughs-using-word.md)   
 [Instruções passo a passo e exemplos de desenvolvimento do office](../vsto/office-development-samples-and-walkthroughs.md)   
 [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)  
  
  
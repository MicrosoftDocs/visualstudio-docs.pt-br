---
title: 'Passo a passo: Inserir texto em um documento de um painel de ações'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- smart documents [Office development in Visual Studio], creating in Word
- smart documents [Office development in Visual Studio], adding controls
- actions panes [Office development in Visual Studio], creating in Word
- actions panes [Office development in Visual Studio], adding controls
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b3b9683c5f41b81d529ad6f3347b54131f32f011
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948719"
---
# <a name="walkthrough-insert-text-into-a-document-from-an-actions-pane"></a>Passo a passo: Inserir texto em um documento de um painel de ações
  Este passo a passo demonstra como criar um painel de ações em um documento do Microsoft Office Word. O painel de ações contém dois controles que coletar entrada e, em seguida, enviar o texto para o documento.  
  
 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Crie uma interface por meio de controles de formulários do Windows em um controle do painel Ações.  
  
-   Exiba o painel de ações quando o aplicativo é aberto.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].  
  
## <a name="create-the-project"></a>Criar o projeto  
 A primeira etapa é criar um projeto de Documento do Word.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de documento do Word com o nome **meu painel de ações básicas**. No assistente, selecione **criar um novo documento**. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     Visual Studio abre o novo documento do Word no designer e adiciona o **meu painel de ações básicas** projeto ao **Gerenciador de soluções**.  
  
## <a name="add-text-and-bookmarks-to-the-document"></a>Adicionar texto e indicadores no documento  
 O painel de ações enviará texto para indicadores no documento. Para criar o documento, digite algum texto para criar um formulário básico.  
  
### <a name="to-add-text-to-your-document"></a>Para adicionar texto ao documento  
  
1. Digite o seguinte texto no documento do Word:  
  
    **21 de março de 2008**  
  
    **Nome**  
  
    **Endereço**  
  
    **Este é um exemplo de um painel de ações básicas no Word.**  
  
   Você pode adicionar um <xref:Microsoft.Office.Tools.Word.Bookmark> controle ao documento, arrastando-o do **caixa de ferramentas** no Visual Studio ou usando o **indicador** caixa de diálogo do Word.  
  
### <a name="to-add-a-bookmark-control-to-your-document"></a>Para adicionar um controle de indicador para o seu documento  
  
1.  Dos **controles do Word** guia da **caixa de ferramentas**, arraste um <xref:Microsoft.Office.Tools.Word.Bookmark> controle ao documento.  
  
     O **adicionar controle de indicador** caixa de diálogo é exibida.  
  
2.  Selecionar a palavra **nome**, sem selecionar a marca de parágrafo e clique em **Okey**.  
  
    > [!NOTE]  
    >  A marca de parágrafo deve estar fora do indicador. Se as marcas de parágrafo não estiverem visíveis no documento, clique no **ferramentas** , aponte para **ferramentas do Microsoft Office Word** e, em seguida, clique em **opções**. Clique no **modo de exibição** guia e, em seguida, selecione o **marcas de parágrafo** caixa de seleção na **marcas de formatação** seção o **opções** caixa de diálogo.  
  
3.  No **propriedades** janela, altere o **nome** propriedade de **Bookmark1** para **showName**.  
  
4.  Selecionar a palavra **endereço**, sem selecionar a marca de parágrafo.  
  
5.  Sobre o **inserir** guia da faixa de opções, no **Links** agrupar, clique em **indicador**.  
  
6.  No **indicador** caixa de diálogo, digite **showAddress** no **nome do indicador** caixa e clique em **adicionar**.  
  
## <a name="add-controls-to-the-actions-pane"></a>Adicionar controles ao painel de ações  
 Para criar a interface do painel Ações, adicione um controle do painel Ações para o projeto e, em seguida, adicionar controles de formulários do Windows para o controle do painel Ações.  
  
### <a name="to-add-an-actions-pane-control"></a>Para adicionar um controle do painel Ações  
  
1.  Selecione o **meu painel de ações básicas** project no **Gerenciador de soluções**.  
  
2.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
3.  No **Adicionar Novo Item** caixa de diálogo, clique em **controle do painel Ações**, nomeie o controle **InsertTextControl,** e clique em **adicionar**.  
  
#### <a name="to-add-windows-form-controls-to-the-actions-pane-control"></a>Para adicionar controles de formulário do Windows para o controle do painel Ações  
  
1.  Se o controle do painel de ações não estiver visível no designer, clique duas vezes **InsertTextControl**.  
  
2.  Do **controles comuns** guia da **caixa de ferramentas**, arraste uma **rótulo** controle para o controle do painel Ações.  
  
3.  Alterar o **texto** propriedade do controle de rótulo à **nome**.  
  
4.  Adicionar um **caixa de texto** o controle para o controle do painel Ações e altere as propriedades a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**GetName**|  
    |**Size**|**130, 20**|  
  
5.  Adicione um segundo **etiqueta** o controle para o controle do painel Ações e altere o **texto** propriedade a ser **endereço**.  
  
6.  Adicione um segundo **caixa de texto** o controle para o controle do painel Ações e altere as propriedades a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**GetAddress**|  
    |**Aceita o retorno**|**True**|  
    |**Multilinha**|**True**|  
    |**Size**|**130, 40**|  
  
7.  Adicionar um **botão** o controle para o controle do painel Ações e altere as propriedades a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**addText**|  
    |**Texto**|**Inserir**|  
  
## <a name="add-code-to-insert-text-into-the-document"></a>Adicione código para inserir texto no documento  
 No painel de ações, escrever um código que insere o texto de caixas de texto em apropriado <xref:Microsoft.Office.Tools.Word.Bookmark> controles no documento. Você pode usar o `Globals` classe para acessar os controles no documento dos controles no painel de ações. Para obter mais informações, consulte [Global de acesso a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).  
  
### <a name="to-insert-text-from-the-actions-pane-in-a-bookmark-in-the-document"></a>Para inserir texto no painel de ações em um indicador no documento  
  
1.  Adicione o seguinte código para o <xref:System.Windows.Forms.Control.Click> manipulador de eventos do **addText** botão.  
  
     [!code-csharp[Trin_VstcoreActionsPaneWord#8](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs#8)]
     [!code-vb[Trin_VstcoreActionsPaneWord#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/InsertTextControl.vb#8)]  
  
2.  No c#, você deve adicionar um manipulador de eventos para o clique do botão. Você pode colocar esse código na `InsertTextControl` construtor após a chamada para `InitializeComponent`. Para obter informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  
  
     [!code-csharp[Trin_VstcoreActionsPaneWord#9](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs#9)]  
  
## <a name="add-code-to-show-the-actions-pane"></a>Adicione código para mostrar o painel de ações  
 Para mostrar o painel de ações, adicione o controle que você criou para a coleção de controle.  
  
### <a name="to-show-the-actions-pane"></a>Para mostrar o painel de ações  
  
1.  Criar uma nova instância do controle do painel Ações no `ThisDocument` classe.  
  
     [!code-csharp[Trin_VstcoreActionsPaneWord#10](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#10)]
     [!code-vb[Trin_VstcoreActionsPaneWord#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#10)]  
  
2.  Adicione o seguinte código para o <xref:Microsoft.Office.Tools.Word.Document.Startup> manipulador de eventos do `ThisDocument`.  
  
     [!code-csharp[Trin_VstcoreActionsPaneWord#11](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#11)]
     [!code-vb[Trin_VstcoreActionsPaneWord#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#11)]  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Teste seu documento para verificar se o painel de ações é aberto quando o documento é aberto e que o texto digitado nas caixas de texto é inserido em indicadores quando o botão é clicado.  
  
### <a name="to-test-your-document"></a>Para testar o documento  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Confirme se o painel de ações está visível.  
  
3.  Digite seu nome e endereço nas caixas de texto no painel de ações e clique em **inserir**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Estas são algumas tarefas que podem vir a seguir:  
  
-   Crie um painel de ações no Excel. Para obter mais informações, consulte [como: adicionar um painel de ações para pastas de trabalho do Excel](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100)).  
  
-   Associe dados a controles em um painel de ações. Para obter mais informações, consulte [instruções passo a passo: associar dados a controles em um painel de ações do Word](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do painel de ações](../vsto/actions-pane-overview.md)   
 [Como: adicionar um painel de ações a documentos do Word ou pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)   
 [Como: adicionar um painel de ações para pastas de trabalho do Excel](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))   
 [Como: gerenciar o layout do controle em painéis de ações](../vsto/how-to-manage-control-layout-on-actions-panes.md)   
 [Controle de indicador](../vsto/bookmark-control.md)  
  
  
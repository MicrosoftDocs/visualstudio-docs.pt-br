---
title: 'Como: gerenciar o layout do controle em painéis de ações'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- actions panes [Office development in Visual Studio], control layout
- controls [Office development in Visual Studio], layout on actions panes
- smart documents [Office development in Visual Studio], control layout
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f523d56b189fb1517df7e22d18cd689e9300eff3
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35255909"
---
# <a name="how-to-manage-control-layout-on-actions-panes"></a>Como: gerenciar o layout do controle em painéis de ações
  Um painel de ações é encaixado à direita de um documento ou planilha, por padrão. No entanto, pode ser encaixado à esquerda, superior ou inferior. Se você estiver usando vários controles de usuário, você pode escrever código para os controles de usuário no painel de ações de pilha corretamente. Para obter mais informações, consulte [visão geral do painel de ações](../vsto/actions-pane-overview.md).  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 A ordem de pilha dos controles depende se o painel de ações é encaixado vertical ou horizontalmente.  
  
> [!NOTE]  
>  Se o usuário redimensiona o painel de ações em tempo de execução, você pode definir os controles seja redimensionada com o painel de ações. Você pode usar o <xref:System.Windows.Forms.Control.Anchor%2A> propriedade de um controle Windows Forms a controles de âncora para o painel de ações. Para obter mais informações, consulte [como: ancorar controles nos Windows Forms](/dotnet/framework/winforms/controls/how-to-anchor-controls-on-windows-forms).  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="to-set-the-stack-order-of-the-actions-pane-controls"></a>Para definir a ordem de pilha dos controles do painel de ações  
  
1.  Abra um projeto de nível de documento para o Microsoft Office Word que inclui um painel de ações com vários controles de usuário ou controles de painel de ações aninhadas. Para obter mais informações, consulte [como: adicionar um painel de ações a documentos do Word ou pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md).  
  
2.  Clique com botão direito **ThisDocument.cs** ou **ThisDocument. vb** na **Gerenciador de soluções** e, em seguida, clique em **Exibir código**.  
  
3.  No <xref:Microsoft.Office.Tools.ActionsPane.OrientationChanged> manipulador de eventos do painel Ações, verifique se a orientação do painel Ações é horizontal.  
  
     [!code-csharp[Trin_VstcoreActionsPaneWord#30](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#30)]
     [!code-vb[Trin_VstcoreActionsPaneWord#30](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#30)]  
  
4.  Se a orientação é horizontal, os controles do painel de ação da esquerda; de pilha Caso contrário, empilhá-los na parte superior.  
  
     [!code-csharp[Trin_VstcoreActionsPaneWord#31](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#31)]
     [!code-vb[Trin_VstcoreActionsPaneWord#31](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#31)]  
  
5.  No c#, você deve adicionar um manipulador de eventos para o `ActionsPane` para o <xref:Microsoft.Office.Tools.Word.Document.Startup> manipulador de eventos. Para obter informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  
  
     [!code-csharp[Trin_VstcoreActionsPaneWord#32](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#32)]  
  
6.  Execute o projeto e verifique se que os controles do painel de ações são empilhados esquerda para a direita quando o painel de ações é encaixado na parte superior do documento, e os controles são empilhados de cima para baixo quando o painel de ações é encaixado à direita do documento.  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[Trin_VstcoreActionsPaneWord#29](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#29)]
 [!code-vb[Trin_VstcoreActionsPaneWord#29](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#29)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer:  
  
-   Controla a um projeto de nível de documento do Word com um painel de ações que contém vários controles de usuário ou o painel de ações aninhadas.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do painel de ações](../vsto/actions-pane-overview.md)   
 [Como: adicionar um painel de ações a documentos do Word ou pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)   
 [Como: adicionar um painel de ações a documentos do Word ou Excel para pastas de trabalho](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)   
 [Passo a passo: Inserir texto em um documento de um painel de ações](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)   
 [Passo a passo: Inserir texto em um documento de um painel de ações](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)  
  
  
---
title: Adicionar o painel ações a documentos do Word ou a pastas de trabalho do Excel
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- smart documents [Office development in Visual Studio], creating in Word
- smart documents [Office development in Visual Studio], adding controls
- actions panes [Office development in Visual Studio], creating in Word
- actions panes [Office development in Visual Studio], adding controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2d24ec3a17c9e0824c6b7aaffeaaac02c1c4f76e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546218"
---
# <a name="how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks"></a>Como adicionar um painel Ações a documentos do Word ou pastas de trabalho do Excel
  Para adicionar um painel ações a um Microsoft Office documento do Word ou uma pasta de trabalho do Microsoft Excel, primeiro crie um controle de usuário Windows Forms. Em seguida, adicione o controle de usuário à <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> Propriedade do `ThisDocument.ActionsPane` campo (palavra) ou `ThisWorkbook.ActionsPane` campo (Excel) em seu projeto.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="creating-the-user-control"></a>Criando o controle de usuário
 O procedimento a seguir mostra como criar um controle de usuário em um projeto do Word ou do Excel. Ele também adiciona um botão ao controle de usuário que grava texto no documento ou pasta de trabalho quando ele é clicado.

#### <a name="to-create-the-user-control"></a>Para criar o controle de usuário

1. Abra seu projeto de nível de documento do Word ou Excel no Visual Studio.

2. No menu **Projeto** , clique em **Adicionar Novo Item**.

3. Na caixa de diálogo **Adicionar novo item** , selecione **controle do painel Ações**, nomeie-o **HelloControl**e clique em **Adicionar**.

    > [!NOTE]
    > Como alternativa, você pode adicionar um item de **controle de usuário** ao seu projeto. As classes geradas pelo **controle do painel Ações** e itens de **controle de usuário** são funcionalmente equivalentes.

4. Na guia **Windows Forms** da caixa de **ferramentas,** arraste um controle de **botão** para o controle.

    > [!NOTE]
    > Se o controle não estiver visível no designer, clique duas vezes em **HelloControl** em **Gerenciador de soluções**.

5. Adicione o código ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos do botão. O exemplo a seguir mostra o código de um Microsoft Office documento do Word.

     [!code-csharp[Trin_VstcoreActionsPaneWord#12](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/HelloControl.cs#12)]
     [!code-vb[Trin_VstcoreActionsPaneWord#12](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/HelloControl.vb#12)]

6. No C#, você deve adicionar um manipulador de eventos para o clique do botão. Você pode posicionar esse código no `HelloControl` Construtor após a chamada para `InitializeComponent` .

     Para obter informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     [!code-csharp[Trin_VstcoreActionsPaneWord#13](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/HelloControl.cs#13)]

## <a name="add-the-user-control-to-the-actions-pane"></a>Adicionar o controle de usuário ao painel Ações
 Para mostrar o painel Ações, adicione o controle de usuário à <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> Propriedade do `ThisDocument.ActionsPane` campo (palavra) ou `ThisWorkbook.ActionsPane` campo (Excel).

### <a name="to-add-the-user-control-to-the-actions-pane"></a>Para adicionar o controle de usuário ao painel Ações

1. Adicione o seguinte código à `ThisDocument` classe ou `ThisWorkbook` como uma declaração de nível de classe (não adicione este código a um método).

     [!code-csharp[Trin_VstcoreActionsPaneWord#14](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#14)]
     [!code-vb[Trin_VstcoreActionsPaneWord#14](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#14)]

2. Adicione o código a seguir ao `ThisDocument_Startup` manipulador de eventos da `ThisDocument` classe ou do `ThisWorkbook_Startup` manipulador de eventos da `ThisWorkbook` classe.

     [!code-csharp[Trin_VstcoreActionsPaneWord#15](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#15)]
     [!code-vb[Trin_VstcoreActionsPaneWord#15](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#15)]

## <a name="see-also"></a>Confira também
- [Visão geral do painel Ações](../vsto/actions-pane-overview.md)
- [Walkthrough: inserir texto em um documento a partir de um painel Ações](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [Como: gerenciar o layout de controle em painéis de ações](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [Walkthrough: inserir texto em um documento a partir de um painel Ações](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)

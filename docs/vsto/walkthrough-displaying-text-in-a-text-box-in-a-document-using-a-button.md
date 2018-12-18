---
title: 'Passo a passo: Exibir texto em uma caixa de texto em um documento usando um botão'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text boxes, displaying text in documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 132a94b6e91148d943d998ab7e4aab96d0d74960
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49822548"
---
# <a name="walkthrough-display-text-in-a-text-box-in-a-document-using-a-button"></a>Passo a passo: Exibir texto em uma caixa de texto em um documento usando um botão
  Este passo a passo demonstra como usar os botões e caixas de texto em uma personalização no nível de documento para o Microsoft Office Word.  
  
 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Adicionando controles ao documento do Word em um projeto de nível de documento em tempo de design.  
  
- Preenchendo uma caixa de texto quando um botão é clicado.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Microsoft Word  
  
## <a name="create-the-project"></a>Criar o projeto  
 A primeira etapa é criar um projeto de Documento do Word.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de documento do Word com o nome **My Button Word**. No assistente, selecione **criar um novo documento**.  
  
     Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     Visual Studio abre o novo documento do Word no designer e adiciona o **My Button do Word** projeto ao **Gerenciador de soluções**.  
  
## <a name="add-controls-to-the-word-document"></a>Adicionar controles ao documento do Word  
 Os controles de interface de usuário consistem em um botão e uma caixa de texto no documento do Word.  
  
### <a name="to-add-a-button-and-a-text-box"></a>Para adicionar um botão e uma caixa de texto  
  
1. Verifique se o documento é aberto no designer do Visual Studio.  
  
2. Dos **controles comuns** guia da **caixa de ferramentas**, arraste um <xref:Microsoft.Office.Tools.Word.Controls.TextBox> controle ao documento.  
  
   > [!NOTE]  
   >  No Word, os controles são descartados em linha com o texto por padrão. Você pode modificar os maneira como os controles e objetos shape são inseridos, alterando o padrão no **edite** guia da **opções** caixa de diálogo do Word.  
  
3. Sobre o **modo de exibição** menu, clique em **janela propriedades**.  
  
4. Encontrar **TextBox1** na **propriedades** caixa de lista suspensa da janela e altere a **nome** propriedade da caixa de texto para **displayText**.  
  
5. Arraste uma **botão** controlar o documento e alterar as propriedades a seguir.  
  
   |Propriedade|Valor|  
   |--------------|-----------|  
   |**Nome**|**insertText**|  
   |**Texto**|**Inserir texto**|  
  
   Agora você pode escrever o código que será executado quando o botão é clicado.  
  
## <a name="populate-the-text-box-when-the-button-is-clicked"></a>Preencha a caixa de texto quando o botão é clicado  
 Sempre que o usuário clica no botão, **Olá, mundo!** é adicionado à caixa de texto.  
  
### <a name="to-write-to-the-text-box-when-the-button-is-clicked"></a>Para gravar a caixa de texto quando o botão é clicado  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **ThisDocument**e, em seguida, clique em **Exibir código** no menu de atalho.  
  
2.  Adicione o seguinte código para o <xref:System.Windows.Forms.Control.Click> manipulador de eventos do botão.  
  
     [!code-vb[Trin_VstcoreProgrammingControlsWord#7](../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb#7)]
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#7](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#7)]  
  
3.  No c#, você deve adicionar um manipulador de eventos para o botão a <xref:Microsoft.Office.Tools.Word.Document.Startup> eventos. Para obter informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  
  
     [!code-csharp[Trin_VstcoreProgrammingControlsWord#8](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs#8)]  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Agora você pode testar seu documento para certificar-se de que a mensagem **Olá, mundo!** é exibida na caixa de texto quando você clica no botão.  
  
### <a name="to-test-your-document"></a>Para testar o documento  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Clique no botão.  
  
3.  Confirme se **Olá, mundo!** é exibida na caixa de texto.  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo mostra as Noções básicas de como usar os botões e caixas de texto em documentos do Word. Estas são algumas tarefas que podem vir a seguir:  
  
-   Usando uma caixa de combinação para alterar a formatação. Para obter mais informações, consulte [instruções passo a passo: formatação de documento de alteração usando controles CheckBox](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md).  
  
-   Usando botões de opção para selecionar estilos de gráfico. Para obter mais informações, consulte [instruções passo a passo: atualizar um gráfico em um documento usando botões de opção](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md).  
  
## <a name="see-also"></a>Consulte também  
 [Controles de formulários do Windows na visão geral de documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md)   
 [Instruções passo a passo usando o Word](../vsto/walkthroughs-using-word.md)   
 [Instruções passo a passo e exemplos de desenvolvimento do office](../vsto/office-development-samples-and-walkthroughs.md)   
 [Como: adicionar controles dos Windows Forms a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)  
  
  
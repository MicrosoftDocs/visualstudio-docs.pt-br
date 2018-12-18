---
title: 'Passo a passo: Associar a dados de um serviço em um projeto de suplemento do VSTO'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Office development in Visual Studio], scrolling records
- records [Office development in Visual Studio], scrolling
- data [Office development in Visual Studio], scrolling database records
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c4ebf998dc7c278fda1e605d18198945958a7fed
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49933177"
---
# <a name="walkthrough-bind-to-data-from-a-service-in-a-vsto-add-in-project"></a>Passo a passo: Associar a dados de um serviço em um projeto de suplemento do VSTO
  Você pode associar dados a controles de host em projetos de suplemento do VSTO. Este passo a passo demonstra como adicionar controles a um documento do Microsoft Office Word, ligar os controles a dados recuperados do serviço de conteúdo do MSDN e responder a eventos em tempo de execução.  
  
 **Aplica-se a:** as informações neste tópico se aplicam a projetos no nível de aplicativo para Word 2010. Para obter mais informações, confira [Features Available by Office Application and Project Type](../vsto/features-available-by-office-application-and-project-type.md) (Funcionalidades disponibilizadas pelo aplicativo do Office e pelo tipo de projeto).  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Adicionando um <xref:Microsoft.Office.Tools.Word.RichTextContentControl> controle a um documento em tempo de execução.  
  
- Associando a <xref:Microsoft.Office.Tools.Word.RichTextContentControl> controle aos dados de um serviço web.  
  
- Responder para o <xref:Microsoft.Office.Tools.Word.ContentControlBase.Entering> eventos de um <xref:Microsoft.Office.Tools.Word.RichTextContentControl> controle.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].  
  
## <a name="create-a-new-project"></a>Criar um novo projeto  
 A primeira etapa é criar um projeto de suplemento do VSTO do Word.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de suplemento do VSTO do Word com o nome **serviço de conteúdo MTPS**, usando o Visual Basic ou c#.  
  
     Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     O Visual Studio abre o `ThisAddIn.vb` ou `ThisAddIn.cs` de arquivos e adiciona o projeto ao **Gerenciador de soluções**.  
  
## <a name="add-a-web-service"></a>Adicionar um serviço web  
 Para este passo a passo, use um serviço web chamado serviço MTPS conteúdo. Esse serviço web retorna informações de um artigo do MSDN especificado na forma de uma cadeia de caracteres XML ou texto sem formatação. Uma etapa posterior mostra como exibir as informações retornadas em um controle de conteúdo.  
  
### <a name="to-add-the-mtps-content-service-to-the-project"></a>Para adicionar o serviço MTPS de conteúdo para o projeto  
  
1.  Sobre o **dados** menu, clique em **Add New Data Source**.  
  
2.  No **Data Source Configuration Wizard**, clique em **Service**e, em seguida, clique em **próxima**.  
  
3.  No **endereço** campo, digite a seguinte URL:  
  
     **http://services.msdn.microsoft.com/ContentServices/ContentService.asmx**  
  
4.  Clique em **acesse**.  
  
5.  No **Namespace** , digite **ContentService**e clique em **Okey**.  
  
6.  No **Assistente para adição de referência** caixa de diálogo, clique em **concluir**.  
  
## <a name="add-a-content-control-and-bind-to-data-at-runtime"></a>Adicione um controle de conteúdo e associar a dados em tempo de execução  
 Em projetos de suplemento do VSTO, adicionar e associar os controles em tempo de execução. Para este passo a passo, configure o controle de conteúdo para recuperar dados do serviço da web quando um usuário clica dentro do controle.  
  
### <a name="to-add-a-content-control-and-bind-to-data"></a>Para adicionar um controle de conteúdo e associar a dados  
  
1.  No `ThisAddIn` de classe, declare as variáveis para o serviço MTPS do conteúdo, o controle de conteúdo e a vinculação de dados.  
  
     [!code-csharp[Trin_WordAddIn_BindingDataToContentControl#2](../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs#2)]
     [!code-vb[Trin_WordAddIn_BindingDataToContentControl#2](../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb#2)]  
  
2.  Adicione o seguinte método à classe `ThisAddIn`. Esse método cria um controle de conteúdo no início do documento ativo.  
  
     [!code-csharp[Trin_WordAddIn_BindingDataToContentControl#4](../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs#4)]
     [!code-vb[Trin_WordAddIn_BindingDataToContentControl#4](../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb#4)]  
  
3.  Adicione o seguinte método à classe `ThisAddIn`. Esse método inicializa os objetos necessários para criar e enviar uma solicitação para o serviço web.  
  
     [!code-csharp[Trin_WordAddIn_BindingDataToContentControl#6](../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs#6)]
     [!code-vb[Trin_WordAddIn_BindingDataToContentControl#6](../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb#6)]  
  
4.  Crie um manipulador de eventos para recuperar o documento da biblioteca MSDN sobre o conteúdo de controles quando um usuário clica dentro do conteúdo de controle e associar os dados para o controle de conteúdo.  
  
     [!code-csharp[Trin_WordAddIn_BindingDataToContentControl#5](../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs#5)]
     [!code-vb[Trin_WordAddIn_BindingDataToContentControl#5](../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb#5)]  
  
5.  Chame o `AddRichTextControlAtRange` e `InitializeServiceObjects` métodos a partir de `ThisAddIn_Startup` método. Para programadores de c#, adicione um manipulador de eventos.  
  
     [!code-csharp[Trin_WordAddIn_BindingDataToContentControl#3](../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs#3)]
     [!code-vb[Trin_WordAddIn_BindingDataToContentControl#3](../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb#3)]  
  
## <a name="test-the-add-in"></a>Testar o suplemento  
 Quando você abre o Word, o <xref:Microsoft.Office.Tools.Word.RichTextContentControl> controle aparece. O texto do controle muda quando você clica nele.  
  
### <a name="to-test-the-vsto-add-in"></a>Para testar o suplemento do VSTO  
  
1.  Pressione **F5**.  
  
2.  Clique dentro do controle de conteúdo.  
  
     Informações são baixadas do serviço de conteúdo MTPS e exibidas dentro do controle de conteúdo.  
  
## <a name="see-also"></a>Consulte também  
 [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)  
  
  
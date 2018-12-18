---
title: 'Como: proteger partes de documentos usando controles de conteúdo'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- restricted permissions [Office development in Visual Studio]
- partial document protection [Office development in Visual Studio]
- content controls [Office development in Visual Studio], protecting documents
- Word [Office development in Visual Studio], partial document protection
- document protection [Office development in Visual Studio]
- Word [Office development in Visual Studio], restricted permissions
- GroupContentControl
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: beee4dd4a67b03f278a296d4b5f129100212fd25
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49850354"
---
# <a name="how-to-protect-parts-of-documents-by-using-content-controls"></a>Como: proteger partes de documentos usando controles de conteúdo
  Quando você protege a parte de um documento, você impedir usuários de alterar ou excluir o conteúdo nessa parte do documento. Há várias maneiras que você pode proteger partes de um documento do Microsoft Office Word usando controles de conteúdo:  
  
- Você pode proteger um controle de conteúdo.  
  
- Você pode proteger uma parte de um documento que não está em um controle de conteúdo.  
  
  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
##  <a name="EditDeleteControl"></a> Proteger um controle de conteúdo  
 Você pode impedir que os usuários editando ou excluindo um controle de conteúdo, definindo propriedades do controle em um projeto de nível de documento em tempo de design ou em tempo de execução.  
  
 Você também pode proteger os controles de conteúdo que você adiciona a um documento em tempo de execução usando um projeto de suplemento do VSTO. Para obter mais informações, consulte [como: adicionar controles content a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md).  
  
### <a name="to-protect-a-content-control-at-design-time"></a>Para proteger um controle de conteúdo em tempo de design  
  
1.  No documento que está hospedado no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] designer, selecione o controle de conteúdo que você deseja proteger.  
  
2.  No **propriedades** janela, defina uma ou ambas as propriedades a seguir:  
  
    -   Para impedir que os usuários o controle de edição, defina **LockContents** à **verdadeiro**.  
  
    -   Para impedir que os usuários a exclusão do controle, defina **LockContentControl** à **verdadeiro**.  
  
3.  Clique em **OK**.  
  
### <a name="to-protect-a-content-control-at-runtime"></a>Para proteger um controle de conteúdo em tempo de execução  
  
1.  Definir o `LockContents` propriedade do controle de conteúdo para **verdadeiro** para impedir que os usuários o controle de edição e definir a `LockContentControl` propriedade a ser **true** para impedir que os usuários excluam o controle.  
  
     O exemplo de código a seguir demonstra como usar o <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContents%2A> e <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContentControl%2A> propriedades de dois diferentes <xref:Microsoft.Office.Tools.Word.RichTextContentControl> objetos em um projeto de nível de documento. Para executar esse código, adicione o código para o `ThisDocument` classe em seu projeto e chame o `AddProtectedContentControls` método o `ThisDocument_Startup` manipulador de eventos.  
  
     [!code-csharp[Trin_ContentControlHowToProtect#2](../vsto/codesnippet/CSharp/Trin_ContentControlHowToProtect/ThisDocument.cs#2)]
     [!code-vb[Trin_ContentControlHowToProtect#2](../vsto/codesnippet/VisualBasic/Trin_ContentControlHowToProtect/ThisDocument.vb#2)]  
  
     O exemplo de código a seguir demonstra como usar o <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContents%2A> e <xref:Microsoft.Office.Tools.Word.RichTextContentControl.LockContentControl%2A> propriedades de dois diferentes <xref:Microsoft.Office.Tools.Word.RichTextContentControl> objetos em um projeto de suplemento do VSTO. Para executar esse código, adicione o código para o `ThisAddIn` classe em seu projeto e chame o `AddProtectedContentControls` método o `ThisAddIn_Startup` manipulador de eventos.  
  
     [!code-vb[Trin_WordAddInDynamicControls#14](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#14)]
     [!code-csharp[Trin_WordAddInDynamicControls#14](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#14)]  
  
## <a name="protect-a-part-of-a-document-that-is-not-in-a-content-control"></a>Proteger uma parte de um documento que não está em um controle de conteúdo  
 Você pode impedir que os usuários alterem uma área de um documento, colocando a área um <xref:Microsoft.Office.Tools.Word.GroupContentControl>. Isso é útil nos seguintes cenários:  
  
-   Você deseja proteger uma área que não contém controles de conteúdo.  
  
-   Você deseja proteger uma área que já contém controles de conteúdo, mas o texto ou outros itens que você deseja proteger não estão em controles de conteúdo.  
  
> [!NOTE]  
>  Se você criar um <xref:Microsoft.Office.Tools.Word.GroupContentControl> que contém os controles de conteúdo incorporados, os controles de conteúdo inseridos não são protegidos automaticamente. Para impedir que os usuários da edição de um controle de conteúdo inserido, use o **LockContents** propriedade do controle.  
  
### <a name="to-protect-an-area-of-a-document-at-design-time"></a>Para proteger uma área de um documento em tempo de design  
  
1.  No documento que está hospedado no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] designer, selecione a área que você deseja proteger.  
  
2.  Na faixa de opções, clique no **desenvolvedor** guia.  
  
    > [!NOTE]  
    >  Se o **desenvolvedor** guia não estiver visível, você deve primeiro Mostrar. Para obter mais informações, consulte [como: Mostrar a guia Desenvolvedor na faixa de opções](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).  
  
3.  No **controles** , clique no **grupo** botão suspenso e clique **grupo**.  
  
     Um <xref:Microsoft.Office.Tools.Word.GroupContentControl> que contém o protegido região é gerada automaticamente no `ThisDocument` classe em seu projeto. Uma borda que representa o controle de grupo é visível em tempo de design, mas não há nenhuma borda visível em tempo de execução.  
  
### <a name="to-protect-an-area-of-a-document-at-runtime"></a>Para proteger uma área de um documento em tempo de execução  
  
1.  Por meio de programação, selecione a área que você deseja proteger e, em seguida, chame o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddGroupContentControl%2A> método para criar um <xref:Microsoft.Office.Tools.Word.GroupContentControl>.  
  
     O exemplo de código a seguir para um projeto de nível de documento adiciona texto ao primeiro parágrafo no documento, seleciona o primeiro parágrafo e, em seguida, cria uma instância de um <xref:Microsoft.Office.Tools.Word.GroupContentControl>. Para executar esse código, adicione o código para o `ThisDocument` classe em seu projeto e chame o `ProtectFirstParagraph` método o `ThisDocument_Startup` manipulador de eventos.  
  
     [!code-csharp[Trin_ContentControlHowToProtect#1](../vsto/codesnippet/CSharp/Trin_ContentControlHowToProtect/ThisDocument.cs#1)]
     [!code-vb[Trin_ContentControlHowToProtect#1](../vsto/codesnippet/VisualBasic/Trin_ContentControlHowToProtect/ThisDocument.vb#1)]  
  
     O exemplo de código a seguir para um projeto de suplemento do VSTO adiciona texto ao primeiro parágrafo no documento ativo, seleciona o primeiro parágrafo e, em seguida, cria uma instância de um <xref:Microsoft.Office.Tools.Word.GroupContentControl>. Para executar esse código, adicione o código para o `ThisAddIn` classe em seu projeto e chame o `ProtectFirstParagraph` método o `ThisAddIn_Startup` manipulador de eventos.  
  
     [!code-vb[Trin_WordAddInDynamicControls#15](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#15)]
     [!code-csharp[Trin_WordAddInDynamicControls#15](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#15)]  
  
## <a name="see-also"></a>Consulte também  
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Controles de conteúdo](../vsto/content-controls.md)   
 [Como: adicionar controles content a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)  
   
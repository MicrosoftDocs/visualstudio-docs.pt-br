---
title: 'Como: redimensionar controles de indicador'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- Bookmark control, resizing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 57b6d6a089570c52607cf73eeed4fc00978ab251
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49924831"
---
# <a name="how-to-resize-bookmark-controls"></a>Como: redimensionar controles de indicador
  Definir o tamanho de um <xref:Microsoft.Office.Tools.Word.Bookmark> controle quando você adiciona a um documento do Microsoft Office Word. Você também pode redimensioná-lo em um momento posterior.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 Há três maneiras de redimensionar um indicador:  
  
- Adicionar ou remover o texto no <xref:Microsoft.Office.Tools.Word.Bookmark> controle.  
  
   Sempre que você adiciona texto em um indicador, o tamanho do indicador automaticamente aumenta para conter o novo texto. Quando você exclui o texto, o tamanho do indicador diminui automaticamente.  
  
- Alterar o <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> e <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> propriedades do <xref:Microsoft.Office.Tools.Word.Bookmark> controle.  
  
   Isso é útil se você estiver alterando o tamanho por apenas alguns caracteres.  
  
- Recrie o <xref:Microsoft.Office.Tools.Word.Bookmark> controle.  
  
   Isso será útil se houver uma alteração significativa no tamanho ou local de um indicador.  
  
  Em projetos de nível de documento, você pode adicionar <xref:Microsoft.Office.Tools.Word.Bookmark> controles para o documento no seu projeto em tempo de design ou em tempo de execução. Em projetos de suplemento do VSTO, você pode adicionar <xref:Microsoft.Office.Tools.Word.Bookmark> controles para qualquer documento aberto no tempo de execução. Para obter mais informações, consulte [como: Adicionar indicador controles a documentos do Word](../vsto/how-to-add-bookmark-controls-to-word-documents.md).  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="change-the-start-and-end-properties"></a>Alterar as propriedades de início e término  
  
### <a name="to-resize-a-bookmark-in-a-document-level-project-at-design-time"></a>Para redimensionar um indicador em um projeto de nível de documento em tempo de design  
  
1.  Selecione o indicador a **propriedades** janela.  
  
2.  Aumente ou diminua o valor da <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> propriedade.  
  
3.  Aumente ou diminua o valor da <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> propriedade.  
  
### <a name="to-resize-a-bookmark-in-a-document-level-project-at-runtime"></a>Para redimensionar um indicador em um projeto de nível de documento em tempo de execução  
  
1.  Modificar a <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> e <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> propriedades de um <xref:Microsoft.Office.Tools.Word.Bookmark> criado em tempo de execução ou em tempo de design.  
  
     O exemplo de código a seguir adiciona cinco caracteres ao início de um indicador chamado `SampleBookmark`. Esse código supõe que há pelo menos cinco caracteres de texto antes do indicador.  
  
     [!code-csharp[Trin_VstcoreHostControlsWord#2](../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs#2)]
     [!code-vb[Trin_VstcoreHostControlsWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb#2)]  
  
     O exemplo de código a seguir adiciona cinco caracteres ao final do mesmo indicador. Esse código supõe que há pelo menos cinco caracteres de texto depois do indicador.  
  
     [!code-csharp[Trin_VstcoreHostControlsWord#3](../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs#3)]
     [!code-vb[Trin_VstcoreHostControlsWord#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb#3)]  
  
### <a name="to-resize-a-bookmark-in-a-vsto-add-in-project-at-runtime"></a>Para redimensionar um indicador em um projeto de suplemento do VSTO em tempo de execução  
  
1.  Modificar a <xref:Microsoft.Office.Tools.Word.Bookmark.Start%2A> e <xref:Microsoft.Office.Tools.Word.Bookmark.End%2A> propriedades de um <xref:Microsoft.Office.Tools.Word.Bookmark> criado em tempo de execução.  
  
     O exemplo de código a seguir cria uma <xref:Microsoft.Office.Tools.Word.Bookmark> que contém o texto do primeiro parágrafo do documento ativo e, em seguida, remove cinco caracteres do início e fim do <xref:Microsoft.Office.Tools.Word.Bookmark>.  
  
     [!code-vb[Trin_WordAddInDynamicControls#16](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#16)]
     [!code-csharp[Trin_WordAddInDynamicControls#16](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#16)]  
  
## <a name="recreate-the-bookmark"></a>Recrie o indicador  
 Você pode redimensionar um indicador em um projeto de nível de documento, adicionando um novo indicador que tem o mesmo nome que o indicador existente, mas que tem um tamanho diferente.  
  
### <a name="to-recreate-a-bookmark-in-a-document-level-project-at-design-time"></a>Para recriar um indicador em um projeto de nível de documento em tempo de design  
  
1.  Selecione o texto a ser incluído no novo <xref:Microsoft.Office.Tools.Word.Bookmark> controle.  
  
2.  Sobre o **inserir** menu, clique em **indicador**.  
  
3.  No **indicador** diálogo caixa, selecione o nome do indicador que você deseja redimensionar e clique em **Add**.  
  
## <a name="see-also"></a>Consulte também  
 [Como: adicionar controles de indicador a documentos do Word](../vsto/how-to-add-bookmark-controls-to-word-documents.md)   
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Como: redimensionar controles NamedRange](../vsto/how-to-resize-namedrange-controls.md)   
 [Como: redimensionar controles ListObject](../vsto/how-to-resize-listobject-controls.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  
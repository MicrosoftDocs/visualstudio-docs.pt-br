---
title: 'Como: adicionar controles XMLNode a documentos do Word'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNode control, adding to documents
- controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bd0429374b175da3260c3605f39c90cf2dffb841
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544892"
---
# <a name="how-to-add-xmlnode-controls-to-word-documents"></a>Como: adicionar controles XMLNode a documentos do Word
  **Importante** As informações definidas neste tópico sobre o Microsoft Word são apresentadas exclusivamente para o benefício e o uso de indivíduos e organizações que estão localizados fora do Estados Unidos e de seus territórios ou que estão usando ou desenvolvendo programas que são executados em produtos do Microsoft Word que foram licenciados pela Microsoft antes de janeiro de 2010, quando a Microsoft removeu uma implementação de funcionalidades específicas relacionadas ao XML personalizado do Microsoft Word. Essas informações sobre o Microsoft Word podem não ser lidas ou usadas por indivíduos ou organizações na Estados Unidos ou em seus territórios que estão usando ou desenvolvendo programas que são executados no, produtos do Microsoft Word que foram licenciados pela Microsoft após 10 de janeiro de 2010; esses produtos não se comportarão da mesma forma que os produtos licenciados antes dessa data ou comprados e licenciados para uso fora do Estados Unidos.

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Quando você mapeia um elemento de esquema XML não repetitivo para um Microsoft Office documento do Word, o Visual Studio adiciona automaticamente um <xref:Microsoft.Office.Tools.Word.XMLNode> controle ao seu documento. Para obter informações sobre como mapear elementos de esquema XML repetitivos, consulte [como: adicionar controles de XMLNodes a documentos do Word](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md).

> [!NOTE]
> O <xref:Microsoft.Office.Tools.Word.XMLNode> controle não está disponível na **caixa de ferramentas** ou na janela **fontes de dados** e não pode ser criado programaticamente.

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-an-xmlnode-control-to-a-document"></a>Para adicionar um controle XMLNode a um documento

1. No documento do Visual Studio Designer, na faixa de faixas, clique na guia **desenvolvedor** .

    > [!NOTE]
    > Se a guia **desenvolvedor** não estiver visível, você deverá primeiro mostrá-la. Para obter mais informações, consulte [como: mostrar a guia Desenvolvedor na faixa de faixas](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).

2. No grupo **XML** , clique em **esquema**.

     A caixa de diálogo **modelos e suplementos** é aberta.

3. Clique na guia **esquema XML** .

4. Clique em **Adicionar esquema**.

     A caixa de diálogo **Adicionar esquema** é aberta.

5. Selecione um esquema XML que contenha elementos de esquema não repetidos na caixa de diálogo **Adicionar esquema** e clique em **abrir**.

     A caixa de diálogo **configurações de esquema** é exibida.

6. Atribua um alias ou clique em **OK** para adicionar o esquema sem um alias.

     O esquema é adicionado à caixa de diálogo **Adicionar esquema** .

7. Na caixa de diálogo **Adicionar esquema** , clique em **OK**.

8. O painel de tarefas **estrutura XML** é aberto.

9. Clique no elemento esquema não repetitivo no painel de tarefas **estrutura XML** para adicioná-lo ao documento.

     Um <xref:Microsoft.Office.Tools.Word.XMLNode> controle é criado e adicionado ao projeto.

## <a name="see-also"></a>Confira também
- [Controle XMLNode](../vsto/xmlnode-control.md)
- [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)

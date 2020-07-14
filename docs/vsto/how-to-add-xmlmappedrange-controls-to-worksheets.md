---
title: 'Como: adicionar controles XMLMappedRange a planilhas'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLMappedRange control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1d69e705e8f537ba3636422ad6883a7633e03322
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544879"
---
# <a name="how-to-add-xmlmappedrange-controls-to-worksheets"></a>Como: adicionar controles XMLMappedRange a planilhas
  Quando você mapeia um elemento XML para uma célula no Microsoft Office Excel, o Visual Studio adiciona automaticamente um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle à sua planilha.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> O <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle não está disponível na **caixa de ferramentas** ou na janela fontes de **dados** . Além disso, você não pode criar <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controles programaticamente.

## <a name="to-add-an-xmlmappedrange-control-to-a-worksheet"></a>Para adicionar um controle XMLMappedRange a uma planilha

1. Abra a pasta de trabalho do Excel no designer do Visual Studio.

2. Abra a planilha onde você deseja adicionar o controle.

3. Na guia **desenvolvedor** , clique em **origem**.

    > [!NOTE]
    > Se a guia **desenvolvedor** não estiver visível na faixa de faixas, você deverá habilitá-la. Para obter mais informações, consulte [como: mostrar a guia Desenvolvedor na faixa de faixas](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).

     O painel de tarefas **origem XML** é exibido.

4. No painel de tarefas **origem XML** , clique em **mapas XML**.

5. Na caixa de diálogo **mapas XML** , clique em **Adicionar**.

     A caixa de diálogo **origem XML** é exibida.

6. Selecione um esquema XML na caixa de diálogo **origem XML** e clique em **abrir**.

     O esquema é adicionado à caixa de diálogo **mapas XML** .

7. Na caixa de diálogo **mapas XML** , clique em **OK**.

8. Arraste um elemento do painel de tarefas **origem XML** para uma célula na planilha.

     Um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> é criado e adicionado ao projeto.

    > [!NOTE]
    > Se você arrastar um elemento pai do painel de tarefas **origem XML** , um <xref:Microsoft.Office.Tools.Excel.ListObject> controle será criado.

## <a name="see-also"></a>Consulte também
- [Controle XmlMappedRange](../vsto/xmlmappedrange-control.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Como Mapear esquemas para planilhas dentro do Visual Studio](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)

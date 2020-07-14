---
title: Como Mapear esquemas para planilhas dentro do Visual Studio
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio], mapping
- mappings [Office development in Visual Studio], XML schemas to Excel worksheets
- Excel [Office development in Visual Studio], XML schemas
- worksheets [Office development in Visual Studio], XML schemas
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c8a0437b940953e89e24969314f63df34d223496
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538132"
---
# <a name="how-to-map-schemas-to-worksheets-inside-visual-studio"></a>Como Mapear esquemas para planilhas dentro do Visual Studio
  Você pode mapear um esquema XML para uma planilha enquanto a planilha está aberta no Visual Studio. Use as mesmas Microsoft Office ferramentas do Excel que você usa quando a pasta de trabalho está aberta fora do Visual Studio. O projeto do Office cria os mesmos objetos se você mapear o esquema para a planilha antes ou depois de criar sua solução do Excel.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> Você não pode usar esquemas XML com várias partes em soluções do Excel.

## <a name="to-map-an-xml-schema-to-an-excel-worksheet-in-visual-studio"></a>Para mapear um esquema XML para uma planilha do Excel no Visual Studio

1. Abra a pasta de trabalho do Excel ou o projeto de modelo dentro do Visual Studio.

2. Clique na planilha para mover o foco para o designer.

3. Na faixa de faixas, clique na guia **desenvolvedor** .

    > [!NOTE]
    > Se a guia **desenvolvedor** não estiver visível, você deverá primeiro mostrá-la. Para obter mais informações, consulte [como: mostrar a guia Desenvolvedor na faixa de faixas](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).

4. No grupo **XML** , clique em **origem**.

     A janela de **origem XML** é aberta.

5. Na janela **origem XML** , clique em **mapas XML**.

     A caixa de diálogo **mapas XML** é aberta.

6. Na caixa de diálogo **mapas XML** , clique em **Adicionar**.

7. Navegue até o arquivo de esquema, selecione-o e clique em **abrir**.

8. Clique em **OK**.

     O esquema é representado na janela de **origem XML** . Em seu projeto, um tipo <xref:System.Data.DataSet> é gerado com base no esquema e um <xref:System.Windows.Forms.BindingSource> é criado.

9. Arraste elementos da janela de **origem XML** para os locais na planilha em que você deseja que os controles correspondentes sejam criados.

     Se você arrastar um elemento de esquema não repetitivo, o projeto do Office gerará um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle que será associado automaticamente ao <xref:System.Windows.Forms.BindingSource> .

     Se você arrastar um elemento de esquema repetitivo, o projeto do Office gerará um <xref:Microsoft.Office.Tools.Excel.ListObject> controle que não está associado automaticamente a uma fonte de dados. Para obter mais informações, consulte [esquemas e dados XML em personalizações em nível de documento](../vsto/xml-schemas-and-data-in-document-level-customizations.md).

## <a name="see-also"></a>Confira também
- [Como Mapear esquemas para documentos do Word dentro do Visual Studio](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [Esquemas e dados XML em personalizações em nível de documento](../vsto/xml-schemas-and-data-in-document-level-customizations.md)

---
title: 'Como: mapear esquemas para planilhas dentro do Visual Studio'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio], mapping
- mappings [Office development in Visual Studio], XML schemas to Excel worksheets
- Excel [Office development in Visual Studio], XML schemas
- worksheets [Office development in Visual Studio], XML schemas
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 8b95e24d151ef6bf8a0083d130c4e38f3f33d480
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35256039"
---
# <a name="how-to-map-schemas-to-worksheets-inside-visual-studio"></a>Como: mapear esquemas para planilhas dentro do Visual Studio
  Você pode mapear um esquema XML para uma planilha enquanto a planilha estiver aberta no Visual Studio. Você usa as mesmas ferramentas do Microsoft Office Excel que você usa quando a pasta de trabalho é aberta fora do Visual Studio. O projeto do Office cria os objetos de mesmos se você mapear o esquema para a planilha antes ou depois de criar sua solução do Excel.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
> [!NOTE]  
>  É possível usar os esquemas XML com diversas partes em soluções do Excel.  
  
## <a name="to-map-an-xml-schema-to-an-excel-worksheet-in-visual-studio"></a>Para mapear um esquema XML para uma planilha do Excel no Visual Studio  
  
1.  Abra o projeto de modelo ou a pasta de trabalho do Excel dentro do Visual Studio.  
  
2.  Clique na planilha para mover o foco para o designer.  
  
3.  Na faixa de opções, clique no **desenvolvedor** guia.  
  
    > [!NOTE]  
    >  Se o **desenvolvedor** guia não estiver visível, você deve primeiro Mostrar. Para obter mais informações, consulte [como: Mostrar a guia Desenvolvedor na faixa de opções](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).  
  
4.  No **XML** , clique em **origem**.  
  
     O **código-fonte XML** janela é aberta.  
  
5.  No **origem XML** janela, clique em **mapas XML**.  
  
     O **mapas XML** caixa de diálogo é aberta.  
  
6.  No **mapas XML** caixa de diálogo, clique em **Add**.  
  
7.  Navegue até o arquivo de esquema, selecione-o e, em seguida, clique em **aberto**.  
  
8.  Clique em **OK**.  
  
     O esquema é representado na **código-fonte XML** janela. Em seu projeto, com um tipo <xref:System.Data.DataSet> é gerado com base no esquema e um <xref:System.Windows.Forms.BindingSource> é criado.  
  
9. Arrastar os elementos do **código-fonte XML** janela para os locais em sua planilha onde você deseja que os controles correspondentes a serem criados.  
  
     Se você arrastar um elemento de esquema não repetitivo, o Office project gera uma <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle que é associada automaticamente a <xref:System.Windows.Forms.BindingSource>.  
  
     Se você arrastar um elemento de esquema repetido, o Office project gera um <xref:Microsoft.Office.Tools.Excel.ListObject> controle que não é automaticamente associado a uma fonte de dados. Para obter mais informações, consulte [esquemas XML e dados no nível de documento personalizações](../vsto/xml-schemas-and-data-in-document-level-customizations.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como: mapear esquemas para documentos do Word dentro do Visual Studio](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)   
 [Esquemas e dados em personalizações no nível de documento XML](../vsto/xml-schemas-and-data-in-document-level-customizations.md)  
  
  
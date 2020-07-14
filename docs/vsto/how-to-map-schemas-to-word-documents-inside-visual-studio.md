---
title: Como Mapear esquemas para documentos do Word dentro do Visual Studio
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio], mapping
- mappings [Office development in Visual Studio], XML schemas to Word documents
- Word [Office development in Visual Studio], mapping XML schemas
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 281d9dc18ae1d0550ba844e58d4e39c3723c8dfb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538145"
---
# <a name="how-to-map-schemas-to-word-documents-inside-visual-studio"></a>Como Mapear esquemas para documentos do Word dentro do Visual Studio
  **Importante** As informações definidas neste tópico sobre o Microsoft Word são apresentadas exclusivamente para o benefício e o uso de indivíduos e organizações que estão localizados fora do Estados Unidos e de seus territórios ou que estão usando ou desenvolvendo programas que são executados em produtos do Microsoft Word que foram licenciados pela Microsoft antes de janeiro de 2010, quando a Microsoft removeu uma implementação de funcionalidades específicas relacionadas ao XML personalizado do Microsoft Word. Essas informações sobre o Microsoft Word podem não ser lidas ou usadas por indivíduos ou organizações na Estados Unidos ou em seus territórios que estão usando ou desenvolvendo programas que são executados no, produtos do Microsoft Word que foram licenciados pela Microsoft após 10 de janeiro de 2010; esses produtos não se comportarão da mesma forma que os produtos licenciados antes dessa data ou comprados e licenciados para uso fora do Estados Unidos.

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Você pode mapear um esquema XML para um documento enquanto o documento estiver aberto no Visual Studio. Use as mesmas Microsoft Office ferramentas do Word que você usa quando o documento está aberto fora do Visual Studio. O projeto do Office cria os mesmos objetos se você mapear o esquema para o documento antes ou depois de criar sua solução do Word.

## <a name="to-map-an-xml-schema-to-a-word-document-in-visual-studio"></a>Para mapear um esquema XML para um documento do Word no Visual Studio

1. Abra o documento do Word ou o projeto de modelo dentro do Visual Studio.

2. Clique no documento para mover o foco para o designer.

3. Na faixa de faixas, clique na guia **desenvolvedor** .

    > [!NOTE]
    > Se a guia **desenvolvedor** não estiver visível, você deverá primeiro mostrá-la. Para obter mais informações, consulte [como: mostrar a guia Desenvolvedor na faixa de faixas](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).

4. No grupo **XML** , clique em **esquema**.

     A caixa de diálogo **modelos e suplementos** é aberta.

5. Clique na guia **esquema XML** .

6. Clique em **Adicionar esquema**.

     A caixa de diálogo **Adicionar esquema** é aberta.

7. Navegue até o arquivo de esquema, selecione-o e clique em **abrir**.

     A caixa de diálogo **configurações de esquema** é aberta.

8. Atribua um alias ou clique em **OK** para adicionar o esquema sem um alias.

9. Clique em **OK**.

     A janela **estrutura XML** é aberta.

10. Arraste os elementos da janela **estrutura XML** para os locais no documento em que você deseja que os controles correspondentes sejam criados.

## <a name="see-also"></a>Confira também
- [Como Mapear esquemas para planilhas dentro do Visual Studio](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
- [Esquemas e dados XML em personalizações em nível de documento](../vsto/xml-schemas-and-data-in-document-level-customizations.md)

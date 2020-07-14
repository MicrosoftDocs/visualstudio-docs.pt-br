---
title: Como exportar uma faixa de faixas do designer de faixa de das faixas para XML da faixa de modo
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, XML
- customizing the Ribbon, XML
- Ribbon [Office development in Visual Studio], XML
- Ribbon [Office development in Visual Studio], exporting
- XML [Office development in Visual Studio], Ribbon
- Ribbon Designer [Office development in Visual Studio]
- exporting Ribbon
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 57918e8a51a3948a2c69eb0c8ab5438b147e44f0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543462"
---
# <a name="how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>Como exportar uma faixa de faixas do designer de faixa de das faixas para XML da faixa de modo
  O item **da faixa de tipos (Visual Designer)** não dá suporte a todos os tipos possíveis de personalização da faixa de medida. Para personalizar a faixa de opções de maneiras avançadas, você pode exportar a faixa do designer para o XML da faixa e editar o XML diretamente.

> [!NOTE]
> Nem todos os valores de propriedade aparecem no arquivo XML da faixa de faixas. Para obter mais informações, consulte [visão geral da faixa](../vsto/ribbon-overview.md)de visualização.

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>Para exportar uma faixa de faixas do designer de faixa de das para XML da faixa de para

1. Clique com o botão direito do mouse no arquivo de código da faixa de bits em **Gerenciador de soluções**e clique em **Designer de exibição**.

2. Clique com o botão direito do mouse no designer de faixa de faixas e clique em **Exportar faixa de bits para XML**.

     O Visual Studio adiciona um arquivo XML da faixa de faixas e um arquivo de código XML da faixa de uma Ribbon ao seu projeto.

3. Na classe de código da faixa de, localize os comentários que começam com `TODO:` .

4. Copie o bloco de código nesses comentários para a classe **ThisAddIn**, **ThisWorkbook**ou **ThisDocument** , dependendo do tipo de solução que você está desenvolvendo.

     Esse código permite que o aplicativo Microsoft Office descubra e carregue sua faixa de faixas personalizada. Para obter mais informações, consulte [Ribbon XML](../vsto/ribbon-xml.md).

5. Na classe **ThisAddIn**, **ThisWorkbook**ou **ThisDocument** , remova a marca de comentário do bloco de código.

     Depois que você remover o comentário do código, ele deverá ser semelhante ao exemplo a seguir. Neste exemplo, a classe Ribbon é chamada `MyRibbon` .

     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs#1)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb#1)]

6. Alterne para o arquivo de código XML da faixa de opções e localize a `Ribbon Callbacks` região.

     É aí que você escreve métodos de retorno de chamada para manipular ações do usuário, como clicar em um botão.

7. Crie um método de retorno de chamada para cada manipulador de eventos que você escreveu no código do designer de faixa de Ribbon.

8. Mova todo o código do manipulador de eventos dos manipuladores de eventos para os métodos de retorno de chamada e modifique o código para trabalhar com o modelo de programação do RibbonX (extensibilidade de faixa de medida).

     Para obter informações sobre como escrever métodos de retorno de chamada e usar o modelo de programação do RibbonX, consulte [Ribbon XML](../vsto/ribbon-xml.md).

## <a name="see-also"></a>Confira também
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [Designer de faixa de das](../vsto/ribbon-designer.md)
- [XML da faixa de opções](../vsto/ribbon-xml.md)
- [Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [Walkthrough: criar uma guia personalizada usando o XML da faixa de uma](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)

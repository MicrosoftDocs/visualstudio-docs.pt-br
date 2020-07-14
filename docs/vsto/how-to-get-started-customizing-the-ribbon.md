---
title: 'Como: começar a personalizar a faixa de faixas'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, adding Ribbon to project
- Ribbon [Office development in Visual Studio], adding
- Ribbon [Office development in Visual Studio], customizing
- customizing the Ribbon, adding Ribbon to project
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: be311f87862f4447d903294508927735d3507b08
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520062"
---
# <a name="how-to-get-started-customizing-the-ribbon"></a>Como: começar a personalizar a faixa de faixas
  Para personalizar a faixa de visualização de um aplicativo Microsoft Office, adicione um item **da faixa de Ribbon (designer visual)** ou de **faixa (XML)** a um projeto do Office.

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-a-ribbon-to-a-project"></a>Para adicionar uma faixa de faixas a um projeto

1. No menu **projeto** , clique em **Adicionar novo item**.

2. Na caixa de diálogo **Adicionar novo item** , selecione **faixa de opções (designer visual)** ou **faixa de opções (XML)**. Para obter mais informações sobre esses modelos, consulte [visão geral da faixa](../vsto/ribbon-overview.md)de visualização.

3. Na caixa **nome** , digite um nome para o item da faixa de tipos.

    Nomes não podem conter os seguintes caracteres:

   - Cerquilha (#)

   - Porcentagem (%)

   - E comercial (&)

   - Asterisco (*)

   - Barra vertical (|)

   - Barra invertida (\\)

   - Dois-pontos (:)

   - Aspas duplas (")

   - Menor que (\<)

   - Maior que (>)

   - Ponto de interrogação (?)

   - Barra (/)

   - Espaços iniciais ou finais (' ')

   - Nomes reservados para Windows ou DOS, como ("nul", "AUX", "con", "COM1", "LPT1" e assim por diante)

4. Clique em **OK**.

   O item da faixa de faixas aparece em **Gerenciador de soluções**. Para obter informações sobre as próximas etapas, consulte [visão geral da faixa](../vsto/ribbon-overview.md)de visualização.

## <a name="see-also"></a>Confira também
- [Acessar a faixa de faixas em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)
- [Designer de faixa de das](../vsto/ribbon-designer.md)
- [XML da faixa de opções](../vsto/ribbon-xml.md)
- [Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [Walkthrough: criar uma guia personalizada usando o XML da faixa de uma](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)

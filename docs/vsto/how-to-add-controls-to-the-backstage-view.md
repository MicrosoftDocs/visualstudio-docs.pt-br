---
title: 'Como: adicionar controles ao modo de exibição de Backstage '
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- customizing the Ribbon, menus
- controls, Ribbon
- menus, customizing
- Microsoft Office Button
- custom Ribbon, menus
- Ribbon, customizing
- Office button
- Ribbon, menus
- Microsoft Office Menu
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5b4ea5cdcd869f16f987e9431359511831af9573
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538340"
---
# <a name="how-to-add-controls-to-the-backstage-view"></a>Como: adicionar controles ao modo de exibição de Backstage
  Você pode usar o designer de faixa de Ribbon para adicionar controles ao menu que é aberto quando você clica na guia **arquivo** . Quando você executa o aplicativo, os controles que você adiciona à guia **arquivo** aparecem um grupo chamado **suplementos**.

 Você não pode posicionar os controles antes ou depois dos controles internos usando o designer de faixa de bits no Visual Studio. Um controle interno é um controle que já aparece no modo de exibição de Backstage. Se você quiser posicionar controles antes ou depois de controles internos, deverá usar um XML da faixa de bits. Para obter mais informações sobre a **faixa de faixas (XML)**, consulte [XML da faixa](../vsto/ribbon-xml.md)de para. Para obter mais informações sobre como personalizar o modo de exibição de Backstage, consulte [introdução ao modo de exibição de Backstage do office 2010 para desenvolvedores](/previous-versions/office/developer/office-2010/ee691833(v=office.14)) e [Personalizar o modo de exibição do Backstage do Office 2010 para desenvolvedores](/previous-versions/office/developer/office-2010/ee815851(v=office.14)).

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-controls-to-backstage-view"></a>Para adicionar controles à exibição de Backstage

1. Abra o item da faixa de faixas no modo de exibição de Design.

     Para obter informações sobre como adicionar um item **da faixa de Ribbon (designer visual)** ao seu projeto, consulte [como: introdução à personalização da faixa de faixas](../vsto/how-to-get-started-customizing-the-ribbon.md).

2. No designer de faixa de faixas, clique na guia **arquivo** .

     Um designer de menu é exibido. Esta superfície de design não contém nenhum controle.

3. Na guia **controles da faixa** de opções do Office da **caixa de ferramentas**, arraste qualquer um dos seguintes controles para o designer de menu:

    - Botão

    - CheckBox

    - Galeria

    - Menu

    - Separador

    - SplitButton

    - ToggleButton

4. Arraste os controles para movê-los para novas posições no menu.

## <a name="see-also"></a>Consulte também
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [Designer de faixa de das](../vsto/ribbon-designer.md)
- [XML da faixa de opções](../vsto/ribbon-xml.md)
- [Como: começar a personalizar a faixa de faixas](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)

---
title: 'Como: personalizar uma guia interna'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
- built-in tabs [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5f73ec7a8555a5e5d569d4316ca619747550bf11
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547180"
---
# <a name="how-to-customize-a-built-in-tab"></a>Como: personalizar uma guia interna
  Você pode adicionar grupos e controles a uma guia interna. Uma guia interna é uma guia que já está na faixa de bits de um aplicativo Microsoft Office. Por exemplo, a guia **dados** é uma guia interna no Excel. Quando você cria um grupo personalizado, ele aparece por último na guia, mas você pode mover o grupo para qualquer lugar na guia.

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

> [!NOTE]
> Você pode adicionar grupos a uma guia interna, mas não pode remover grupos internos de uma guia interna.

### <a name="to-add-groups-to-a-built-in-tab"></a>Para adicionar grupos a uma guia interna

1. Clique com o botão direito do mouse no arquivo de código da faixa de bits em **Gerenciador de soluções**e clique em **Designer de exibição**.

    > [!NOTE]
    > Se o arquivo de código da faixa de Ribbon não aparecer no **Gerenciador de soluções**, você deverá adicionar um **item da faixa** de uma ao seu projeto. Consulte [como: começar a personalizar a faixa de faixas](../vsto/how-to-get-started-customizing-the-ribbon.md).

2. Clique com o botão direito do mouse em qualquer guia no designer de faixa de faixas e clique em **Propriedades**.

3. Na janela **Propriedades** , expanda a propriedade **ControlID** e defina a propriedade **ControlIdType** como **Office**.

4. Defina a propriedade **OfficeId** como a *ID de controle* da guia interna que você deseja personalizar.

     A ID de controle é o nome que identifica com exclusividade guias, grupos e controles que são criados em Microsoft Office aplicativos.

     Para obter uma lista de IDs de controle, consulte [arquivos de ajuda do office 2010: identificadores de controle de interface do usuário Fluent do Office](https://www.microsoft.com/download/details.aspx?id=6627).

5. Na guia **controles da faixa** de **ferramentas**do Office, arraste grupos para a guia.

    > [!NOTE]
    > Os grupos internos não aparecem no designer. Portanto, a única maneira de determinar se você está trabalhando com uma guia interna é examinar a propriedade **ControlID** da guia.

### <a name="to-position-groups-on-a-built-in-tab"></a>Para posicionar grupos em uma guia interna

1. No designer de faixa de opções, selecione um grupo personalizado.

2. Na janela **Propriedades** , expanda a propriedade **posição** .

3. Defina a propriedade **PositionType** como o valor apropriado:

    - **BeforeOfficeId** posiciona o grupo antes de um grupo interno especificado.

    - **AfterOfficeId** posiciona o grupo após um grupo interno especificado.

4. Defina a propriedade **OfficeId** como a ID de controle de um grupo interno.

     Para obter uma lista de IDs de controle, consulte [arquivos de ajuda do office 2010: identificadores de controle de interface do usuário Fluent do Office](https://www.microsoft.com/download/details.aspx?id=6627).

## <a name="see-also"></a>Confira também
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [Designer de faixa de das](../vsto/ribbon-designer.md)
- [XML da faixa de opções](../vsto/ribbon-xml.md)
- [Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [Walkthrough: criar uma guia personalizada usando o XML da faixa de uma](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
- [Como: começar a personalizar a faixa de faixas](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [Como alterar a posição de uma guia na faixa de forma](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [Como: adicionar controles ao modo de exibição de Backstage](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [Como mostrar erros de interface do usuário do suplemento](../vsto/how-to-show-add-in-user-interface-errors.md)

---
title: Como alterar a posição de uma guia na faixa de forma
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8f821ea2a469fc06f80a7aaea96d07274d02a81d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544853"
---
# <a name="how-to-change-the-position-of-a-tab-on-the-ribbon"></a>Como alterar a posição de uma guia na faixa de forma
  Você pode alterar a ordem das guias personalizadas em uma faixa de forma usando o **Editor de coleção de guias**. Você pode posicionar guias personalizadas antes ou depois de uma guia interna na faixa de bits. Uma guia interna é uma guia que já está na faixa de bits de um aplicativo Microsoft Office. Por exemplo, a guia **dados** é uma guia interna no Excel.

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-change-the-order-of-tabs-on-the-ribbon"></a>Para alterar a ordem das guias na faixa de faixas

1. Selecione o arquivo de código da faixa de opções (arquivo *. vb* ou *. cs* ) em **Gerenciador de soluções**.

2. No menu **Exibir** , clique em **Designer**.

3. Clique com o botão direito do mouse no designer de faixa de faixas e clique em **Propriedades**.

4. Na janela **Propriedades** , selecione a propriedade **guias** e, em seguida, clique no botão de reticências (![elipse do designer móvel ASP.net](../sharepoint/media/mwellipsis.gif "Elipse do designer móvel ASP.NET")).

     O **Editor de coleção de guias** é exibido.

5. No **Editor de coleção de guias**, na lista **Membros** , selecione a guia que você deseja mover e clique nas setas para cima ou para baixo para alterar a ordem de tabulação.

### <a name="to-position-a-tab-before-or-after-a-built-in-tab-on-the-ribbon"></a>Para posicionar uma guia antes ou depois de uma guia interna na faixa de bits

1. No designer de faixa de opções, selecione uma guia personalizada.

2. Na janela **Propriedades** , expanda a propriedade **ControlID** e verifique se o valor da propriedade **ControlIdType** está definido como **personalizado**.

3. Na janela **Propriedades** , expanda a propriedade **posição** .

4. Defina a propriedade **PositionType** como o valor apropriado:

    - **BeforeOfficeId** posiciona o grupo antes de uma guia interna especificada.

    - **AfterOfficeId** posiciona o grupo após uma guia interna especificada.

5. Defina a propriedade **OfficeId** como a ID de controle de uma guia interna.

     Para obter uma lista de IDs de controle, consulte [arquivos de ajuda do office 2010: identificadores de controle de interface do usuário Fluent do Office](https://www.microsoft.com/download/details.aspx?id=6627).

## <a name="see-also"></a>Consulte também
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [Designer de faixa de das](../vsto/ribbon-designer.md)
- [XML da faixa de opções](../vsto/ribbon-xml.md)
- [Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [Walkthrough: criar uma guia personalizada usando o XML da faixa de uma](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)

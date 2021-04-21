---
title: Personalizar uma faixa de faixas para o Outlook
description: Saiba que, ao personalizar a faixa de faixas no Microsoft Office Outlook, você deve considerar onde sua faixa de faixas personalizada aparecerá no aplicativo.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Inspectors [Office development in Visual Studio]
- Outlook [Office development in Visual Studio], Ribbon
- customizing the Ribbon, about customizing the Ribbon
- custom Ribbon, about customizing the Ribbon
- Ribbon [Office development in Visual Studio], Outlook
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: df28de0f8a9497fabecff816c26db7593bf349bd
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828053"
---
# <a name="customize-a-ribbon-for-outlook"></a>Personalizar uma faixa de faixas para o Outlook
  Ao personalizar a faixa de faixas no Microsoft Office Outlook, você deve considerar onde sua faixa de faixas personalizada aparecerá no aplicativo. O Outlook exibe a faixa de tipos na interface do usuário do aplicativo principal e no Windows que é aberta quando os usuários executam determinadas tarefas, como a criação de mensagens de email. Essas janelas de aplicativos são identificadas como inspetores.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="add-a-custom-ribbon-to-the-main-application-ui"></a>Adicionar uma faixa de faixas personalizada à interface do usuário do aplicativo principal
 A interface do usuário principal do aplicativo no Outlook é chamada de Gerenciador. Se você estiver usando o item **da faixa de visualização (Visual Designer)** , poderá adicionar uma faixa de lista ao Explorer clicando na propriedade **RibbonType** da faixa de lista na janela **Propriedades** e, em seguida, selecionando **Microsoft. Outlook. Explorer**.

## <a name="assign-a-ribbon-to-an-inspector"></a>Atribuir uma faixa de faixas a um inspetor
 Você identifica o inspetor que deseja personalizar especificando o tipo de faixa de tipos que corresponde à classe de mensagem para o Inspetor.

 Se você estiver usando o item **da faixa de opções (Visual Designer)** , clique na propriedade **faixa** de opções da faixa de opções na janela **Propriedades** e selecione uma ou mais IDs da faixa de opções na lista de valores.

 Você pode adicionar mais de uma faixa de faixas a um projeto. Se mais de uma faixa de forma compartilhar uma ID da faixa de uma, substitua o `CreateRibbonExtensibilityObject` método na `ThisAddin` classe do seu projeto para especificar qual faixa de forma exibir em tempo de execução. Para obter mais informações, consulte [visão geral da faixa](../vsto/ribbon-overview.md)de visualização. Para obter mais informações sobre cada tipo de faixa de tipos, consulte o artigo técnico [Personalizar a faixa de visualização no Outlook 2007](/previous-versions/office/developer/office-2007/bb226712(v=office.12)).

## <a name="specify-the-ribbon-type-by-using-ribbon-xml"></a>Especificar o tipo de faixa de tipos usando o XML da faixa de faixas
 Se você estiver usando o item da faixa de seleção **(XML)** , verifique o valor do parâmetro *RibbonId* no <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> método e retorne a faixa de forma apropriada.

 O <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> método é gerado automaticamente pelo Visual Studio no arquivo de código da faixa de Ribbon. O parâmetro *RibbonId* é uma cadeia de caracteres que identifica o Gerenciador ou um tipo específico de Inspetor. Para obter uma lista completa dos possíveis valores do parâmetro *RibbonId* , consulte o artigo técnico [Personalizar a faixa de visualização no Outlook 2007](/previous-versions/office/developer/office-2007/bb226712(v=office.12)).

 O exemplo de código a seguir demonstra como exibir uma faixa de opções personalizada somente no `Microsoft.Outlook.Mail.Compose` inspetor. Este é o inspetor que é aberto quando um usuário cria uma nova mensagem de email. A faixa de visualização a ser exibida é especificada no `GetResourceText()` método, que é gerado na classe **Ribbon** . Para obter mais informações sobre a classe **Ribbon** , consulte [Ribbon XML](../vsto/ribbon-xml.md).

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_RibbonOutlookBasic/Ribbon1.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_RibbonOutlookBasic/Ribbon1.vb" id="Snippet1":::

## <a name="see-also"></a>Consulte também
- [Acessar a faixa de faixas em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [Designer de faixa de das](../vsto/ribbon-designer.md)
- [XML da faixa de opções](../vsto/ribbon-xml.md)

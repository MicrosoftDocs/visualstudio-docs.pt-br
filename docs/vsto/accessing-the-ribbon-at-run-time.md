---
title: Acessar a faixa de faixas em tempo de execução
description: Você pode escrever código para mostrar, ocultar e modificar a faixa de faixas e permitir que os usuários executem o código de controles em um painel de tarefas personalizado, no painel ações ou na região de formulário do Outlook.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Globals class, Ribbon
- Ribbon [Office development in Visual Studio], accessing
- RibbonManager class
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e20c9a54d2fa352c51d5ae5383f5c5b7861e0fdf
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825219"
---
# <a name="access-the-ribbon-at-run-time"></a>Acessar a faixa de faixas em tempo de execução
  Você pode escrever código para mostrar, ocultar e modificar a faixa de faixas e permitir que os usuários executem o código de controles em um painel de tarefas personalizado, no painel ações ou na região de formulário do Outlook.

 Você pode acessar a faixa de faixas usando a `Globals` classe. Para projetos do Outlook, você pode acessar as faixas de as que aparecem em um inspetor específico do Outlook ou em uma janela do Explorer do Outlook.

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

## <a name="access-the-ribbon-by-using-the-globals-class"></a>Acessar a faixa de faixas usando a classe Globals
 Você pode usar a `Globals` classe para acessar a faixa de bits em um projeto de nível de documento ou de suplemento do VSTO de qualquer lugar no projeto.

 Para obter mais informações sobre a `Globals` classe, consulte [acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).

 O exemplo a seguir usa a `Globals` classe para acessar uma faixa de opções personalizada chamada `Ribbon1` e definir o texto que aparece em uma caixa de combinação na faixa de opções para `Hello World` .

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb" id="Snippet4":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs" id="Snippet4":::

## <a name="access-a-collection-of-ribbons-that-appear-in-a-specific-outlook-inspector-window"></a>Acessar uma coleção de faixas de faixa que aparecem em uma janela específica do Inspetor do Outlook
 Você pode acessar uma coleção de faixas de faixa que aparecem nos *inspetores* do Outlook. Um inspetor é uma janela que é aberta no Outlook quando os usuários executam determinadas tarefas, como a criação de mensagens de email. Para acessar a faixa de uma janela de Inspetor, chame a `Ribbons` propriedade da `Globals` classe e passe um <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto que represente o Inspetor.

 O exemplo a seguir obtém a coleção da faixa de opções do inspetor que tem foco no momento. Em seguida, este exemplo acessa uma faixa de uma chamada `Ribbon1` e define o texto que aparece em uma caixa de combinação na faixa de para `Hello World` .

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb" id="Snippet5":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs" id="Snippet5":::

## <a name="access-a-collection-of-ribbons-that-appear-for-a-specific-outlook-explorer"></a>Acessar uma coleção de faixas de faixa que aparecem para um Gerenciador do Outlook específico
 Você pode acessar uma coleção de faixas de faixa que aparecem em um *Gerenciador* do Outlook. Um Gerenciador é a interface do usuário do aplicativo principal para uma instância do Outlook. Para acessar a faixa de faixas de uma janela do Explorer, chame a `Ribbons` propriedade da `Globals` classe e passe um <xref:Microsoft.Office.Interop.Outlook.Explorer> objeto que represente o Gerenciador.

 O exemplo a seguir obtém a coleção da faixa de opções do Gerenciador que tem o foco no momento. Em seguida, este exemplo acessa uma faixa de uma chamada `Ribbon1` e define o texto que aparece em uma caixa de combinação na faixa de para `Hello World` .

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb" id="Snippet6":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs" id="Snippet6":::

## <a name="see-also"></a>Consulte também
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [Designer da faixa de opções](../vsto/ribbon-designer.md)
- [XML da faixa de opções](../vsto/ribbon-xml.md)
- [Visão geral do modelo de objeto Ribbon](../vsto/ribbon-object-model-overview.md)
- [Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [Walkthrough: atualizar os controles em uma faixa de faixas em tempo de execução](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)
- [Personalizar uma faixa de faixas para o Outlook](../vsto/customizing-a-ribbon-for-outlook.md)
- [Acessar uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)

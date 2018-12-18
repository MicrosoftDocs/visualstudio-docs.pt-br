---
title: Acesso a faixa de opções em tempo de execução
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
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
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9a20297ee0d60173cbd0513f3d34e12f12388bdb
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304617"
---
# <a name="access-the-ribbon-at-runtime"></a>Acesso a faixa de opções em tempo de execução
  Você pode escrever código para mostrar, ocultar e modificar a faixa de opções e permitir que os usuários executar o código de controles em um painel de tarefas personalizado, o painel de ações ou a região de formulário do Outlook.  

 Você pode acessar a faixa de opções usando o `Globals` classe. Para projetos do Outlook, você pode acessar as faixas de opções que aparecem em uma janela do Inspetor do Outlook ou Outlook Explorer específica.  

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  

## <a name="access-the-ribbon-by-using-the-globals-class"></a>Acesso a faixa de opções usando a classe Globals  
 Você pode usar o `Globals` classe para acessar a faixa de opções em um projeto de nível de documento ou projeto de suplemento do VSTO em qualquer lugar no projeto.  

 Para obter mais informações sobre o `Globals` classe, consulte [Global de acesso a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).  

 O exemplo a seguir usa o `Globals` classe para acessar uma faixa de opções personalizada denominada `Ribbon1` e defina o texto que aparece em uma caixa de combinação na faixa de opções para `Hello World`.  

 [!code-vb[Trin_Outlook_FR_Access#4](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb#4)]
 [!code-csharp[Trin_Outlook_FR_Access#4](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs#4)]  

## <a name="access-a-collection-of-ribbons-that-appear-in-a-specific-outlook-inspector-window"></a>Acessar uma coleção de faixas de opções que aparecem em uma janela específica do Inspetor do Outlook  
 Você pode acessar uma coleção de faixas de opções que aparecem no Outlook *inspetores*. Um Inspector é uma janela que abre no Outlook quando os usuários executam determinadas tarefas, como a criação de mensagens de email. Para acessar a faixa de opções de uma janela de inspeção, chame o `Ribbons` propriedade do `Globals` classe e passar um <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto que representa o Inspetor.  

 O exemplo a seguir obtém a coleção de faixa de opções do Inspetor de que tem o foco no momento. Neste exemplo, em seguida, acessa uma faixa de opções chamada `Ribbon1` e define o texto que aparece em uma caixa de combinação na faixa de opções para `Hello World`.  

 [!code-vb[Trin_Outlook_FR_Access#5](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb#5)]
 [!code-csharp[Trin_Outlook_FR_Access#5](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs#5)]  

## <a name="access-a-collection-of-ribbons-that-appear-for-a-specific-outlook-explorer"></a>Acessar uma coleção de faixas de opções que aparecem para um navegador específico do Outlook  
 Você pode acessar uma coleção de faixas de opções que aparecem no Outlook *Explorer*. Um Explorer é a interface do usuário (IU) principal do aplicativo para uma instância do Outlook. Para acessar a faixa de opções de uma janela do Explorer, chame o `Ribbons` propriedade do `Globals` classe e passe um <xref:Microsoft.Office.Interop.Outlook.Explorer> objeto que representa o Gerenciador.  

 O exemplo a seguir obtém a coleção de faixa de opções do Explorer que tem o foco no momento. Neste exemplo, em seguida, acessa uma faixa de opções chamada `Ribbon1` e define o texto que aparece em uma caixa de combinação na faixa de opções para `Hello World`.  

 [!code-vb[Trin_Outlook_FR_Access#6](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb#6)]
 [!code-csharp[Trin_Outlook_FR_Access#6](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs#6)]  

## <a name="see-also"></a>Consulte também  
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [Designer de faixa de opções](../vsto/ribbon-designer.md)   
 [XML da faixa de opções](../vsto/ribbon-xml.md)   
 [Visão geral do modelo de objeto da faixa de opções](../vsto/ribbon-object-model-overview.md)   
 [Passo a passo: Criar uma guia personalizada usando o Designer de faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)   
 [Explicação passo a passo: Os controles em uma faixa de opções em tempo de execução de atualização](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)   
 [Personalizar uma faixa de opções do Outlook](../vsto/customizing-a-ribbon-for-outlook.md)   
 [Acessar uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)  

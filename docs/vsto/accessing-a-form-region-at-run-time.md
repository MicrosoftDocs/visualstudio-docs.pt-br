---
title: Acessar uma região de formulário em tempo de execução
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Inspectors [Office development in Visual Studio]
- Explorers [Office development in Visual Studio]
- form regions [Office development in Visual Studio], accessing at runtime
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: f2c1f3e80f5ca4015a19b5eee7f2f4c673dcc615
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304474"
---
# <a name="access-a-form-region-at-runtime"></a>Acessar uma região de formulário em tempo de execução

|Aplica-se a|  
|----------------|  
|As informações neste tópico se aplicam somente aos tipos e versões de projetos do Microsoft Office a seguir. Para obter mais informações, consulte [recursos disponíveis por tipo de projeto e aplicativo do Office](../vsto/features-available-by-office-application-and-project-type.md).<br /><br /> **Tipo de projeto**<br /><br /> -Projetos de suplemento do VSTO<br /><br /> **Versão do Microsoft Office**<br /><br /> -   [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)]|  

 Use o `Globals` classe para regiões de formulário de acesso em qualquer lugar dentro de seu projeto do Outlook. Para obter mais informações sobre o `Globals` classe, consulte [Global de acesso a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).  

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  

## <a name="access-form-regions-that-appear-in-a-specific-outlook-inspector-window"></a>Regiões de formulário de acesso que aparecem em uma janela específica do Inspetor do Outlook  
 Para acessar todas as regiões de formulário que aparecem em um inspetor do Outlook específico, chame o `FormRegions` propriedade do `Globals` classe e passar um <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto que representa o Inspetor.  

 O exemplo a seguir obtém a coleção de regiões de formulário que aparecem no Inspetor de que tem o foco no momento. Neste exemplo, em seguida, acessa uma região de formulário na coleção denominada `formRegion1` e define o texto que aparece em uma caixa de texto para `Hello World`.  

 [!code-vb[Trin_Outlook_FR_Access#2](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb#2)]
 [!code-csharp[Trin_Outlook_FR_Access#2](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs#2)]  

## <a name="access-form-regions-that-appear-in-a-specific-outlook-explorer-window"></a>Regiões de formulário de acesso que aparecem em uma janela específica do Explorer do Outlook  
 Para acessar todas as regiões de formulário que aparecem em um navegador específico do Outlook, chame o `FormRegions` propriedade do `Globals` classe e passe um <xref:Microsoft.Office.Interop.Outlook.Explorer> objeto que representa o Gerenciador.  

 O exemplo a seguir obtém a coleção de regiões de formulário que aparece no Gerenciador de que tem o foco no momento. Neste exemplo, em seguida, acessa uma região de formulário na coleção denominada `formRegion1` e define o texto que aparece em uma caixa de texto para `Hello World`.  

 [!code-vb[Trin_Outlook_FR_Access#3](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb#3)]
 [!code-csharp[Trin_Outlook_FR_Access#3](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs#3)]  

## <a name="access-all-form-regions"></a>Acessar todas as regiões de formulário  
 Para acessar todas as regiões de formulário que aparecem em todos os Explorers e todos os inspetores, chame o `FormRegions` propriedade do `Globals` classe.  

 O exemplo a seguir obtém a coleção de regiões de formulário que aparecem em todos os Explorers e todos os inspetores. Neste exemplo, em seguida, acessa uma região de formulário nomeada `formRegion1` e define o texto que aparece em uma caixa de texto para `Hello World`.  

 [!code-vb[Trin_Outlook_FR_Access#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb#1)]
 [!code-csharp[Trin_Outlook_FR_Access#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs#1)]  

## <a name="access-controls-on-a-form-region"></a>Controles de acesso em uma região de formulário  
 Para controles de acesso em uma região de formulário usando o `Globals` classe, você deve fazer os controles acessíveis para código fora do arquivo de código de região do formulário.  

### <a name="form-regions-designed-in-the-form-region-designer"></a>Regiões de formulário projetadas no designer de região de formulário  
 Para c#, altere o modificador de cada controle que você deseja acessar. Para fazer isso, selecione cada controle no designer de região de formulário e altere o **modificadores** propriedade **interno** ou **público** no **propriedades** janela. Por exemplo, se você alterar o **modificador** propriedade de `textBox1` ao **Internal**, você pode acessar `textBox1` digitando `Globals.FormRegions.FormRegion1.textBox1`.  

 Para o Visual Basic, você não precisa alterar o modificador.  

### <a name="imported-form-regions"></a>Regiões do formulário importado  
 Quando você importa uma região de formulário que foi projetada no Outlook, o modificador de acesso de cada controle na região do formulário se torna privado. Porque você não pode usar o designer de região de formulário para modificar uma região do formulário importado, não é possível alterar o modificador de um controle na **propriedades** janela.  

 Para habilitar o acesso a um controle de fora o arquivo de código de região do formulário, crie uma propriedade no arquivo de código de região de formulário para retornar o controle.  

 Para obter mais informações sobre como criar propriedades no C#, consulte [como: declarar e usar ler gravar propriedades &#40;C&#35; guia de programação do&#41;](/dotnet/csharp/programming-guide/classes-and-structs/how-to-declare-and-use-read-write-properties).  

 Para obter mais informações sobre como criar propriedades no Visual Basic, consulte [como: criar uma propriedade (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/procedures/how-to-create-a-property).  

## <a name="see-also"></a>Consulte também  
 [Diretrizes para criar regiões de formulário do Outlook](../vsto/guidelines-for-creating-outlook-form-regions.md)   
 [Passo a passo: Criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)   
 [Como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)   
 [Personalizar ações em regiões de formulário do Outlook](../vsto/custom-actions-in-outlook-form-regions.md)   
 [Associar uma região de formulário uma classe de mensagem do Outlook](../vsto/associating-a-form-region-with-an-outlook-message-class.md)   
 [Passo a passo: Importar de uma região de formulário projetada no Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)   
 [Como: evitar que o Outlook exiba uma região de formulário](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)   
 [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)   
 [Acesso a faixa de opções em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)  

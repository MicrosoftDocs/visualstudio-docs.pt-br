---
title: Personalizar uma faixa de faixas para o InfoPath
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- InfoPath [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], InfoPath
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 76ec069ef71890a69fdbd41f40bd91cf75d93cd4
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255514"
---
# <a name="customize-a-ribbon-for-infopath"></a>Personalizar uma faixa de faixas para o InfoPath
  Ao personalizar a faixa de faixas no Microsoft Office InfoPath, você deve considerar onde sua faixa de faixas personalizada aparecerá no aplicativo. [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]pode exibir a faixa de opções nos três seguintes tipos de janelas de aplicativo do InfoPath:

- Janelas que exibem um modelo de formulário que é aberto no modo de design.

- Janelas que exibem um formulário baseado em um modelo de formulário.

- A janela de visualização de impressão.

  **Aplica-se a:** As informações neste tópico se aplicam a projetos de suplemento do VSTO para o InfoPath 2010. Para obter mais informações, consulte [recursos disponíveis por aplicativo do Office e tipo de projeto](../vsto/features-available-by-office-application-and-project-type.md).

  Os usuários e designers abrem um modelo de formulário no modo de design para modificar a aparência e o layout do modelo. Os usuários abrem formulários baseados em um modelo de formulário para adicionar conteúdo.

  A janela de visualização de impressão permite que designers e usuários visualizem as páginas de um formulário ou modelo de formulário antes de imprimi-los.

> [!NOTE]
> A guia **suplementos** não aparece na janela de visualização de impressão. Se você quiser que uma guia personalizada apareça na janela de visualização de impressão, verifique se a propriedade **OfficeId** da guia não está definida como **TabAddins**.

 Você deve especificar o tipo de faixa de tipos de cada janela na qual você deseja que sua faixa de forma apareça.

## <a name="specify-the-ribbon-type-in-the-ribbon-designer"></a>Especificar o tipo de faixa de tipos no designer de faixa de faixas
 Se você estiver usando o item **da faixa de opções (Visual Designer)** , clique na propriedade **RibbonType** da faixa de opções na janela **Propriedades** e selecione qualquer uma das IDs da faixa de opções descritas na tabela a seguir.

|ID da faixa de Ribbon|Janela na qual a faixa de faixas será exibida quando você executar o projeto|
|---------------|---------------------------------------------------------------------|
|**Microsoft.InfoPath.Designer**|Janelas que exibem um modelo de formulário que é aberto no modo de design.|
|**Microsoft.InfoPath.Editor**|Janelas que exibem um formulário baseado em um modelo de formulário.|
|**Microsoft.InfoPath.PrintPreview**|A janela de visualização de impressão.|

 Você pode adicionar mais de uma faixa de faixas a um projeto. Se mais de uma faixa de forma compartilhar uma ID da faixa `CreateRibbonExtensibilityObject` de uma, `ThisAddin` substitua o método na classe do seu projeto para especificar qual faixa de forma exibir em tempo de execução. Para obter mais informações, consulte [visão geral da faixa](../vsto/ribbon-overview.md)de visualização.

## <a name="specify-the-ribbon-type-by-using-ribbon-xml"></a>Especificar o tipo de faixa de tipos usando o XML da faixa de faixas
 Se você estiver usando o item da faixa de seleção **(XML)** , verifique o valor do <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> parâmetro *RibbonId* no método e retorne a faixa de forma apropriada.

 O <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> método é gerado automaticamente pelo Visual Studio no arquivo de código da faixa de Ribbon. O parâmetro *RibbonId* é uma cadeia de caracteres que identifica o tipo de janela do InfoPath que está sendo aberto.

 O exemplo de código a seguir demonstra como exibir uma faixa de opções personalizada somente em uma janela que exibe um modelo de formulário no modo de design. A faixa de visualização a ser exibida é `GetResourceText()` especificada no método, que é gerado na classe Ribbon. Para obter mais informações sobre a classe Ribbon, consulte [Ribbon XML](../vsto/ribbon-xml.md).

 [!code-csharp[Trin_RibbonInfoPathBasic#1](../vsto/codesnippet/CSharp/myinfopathproject/ribbon.cs#1)]
 [!code-vb[Trin_RibbonInfoPathBasic#1](../vsto/codesnippet/VisualBasic/myinfopathproject/ribbon.vb#1)]

## <a name="see-also"></a>Consulte também
- [Acessar a faixa de faixas em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [Designer de faixa de das](../vsto/ribbon-designer.md)
- [XML da faixa de opções](../vsto/ribbon-xml.md)

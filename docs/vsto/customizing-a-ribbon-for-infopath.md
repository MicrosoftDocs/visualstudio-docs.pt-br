---
title: Personalizar uma faixa de opções para InfoPath
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- InfoPath [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], InfoPath
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f0a6a50ca1e84d9b1f5508cccbad24607f36b3f7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942056"
---
# <a name="customize-a-ribbon-for-infopath"></a>Personalizar uma faixa de opções para InfoPath
  Quando você personaliza a faixa de opções no Microsoft Office InfoPath, você deve considerar onde sua faixa de opções personalizada será exibida no aplicativo. [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)] pode exibir a faixa de opções em três tipos de janelas de aplicativo do InfoPath:  
  
- Windows que exibem um modelo de formulário é aberto no modo de design.  
  
- Windows que exibem um formulário que é baseado em um modelo de formulário.  
  
- A janela de visualização de impressão.  
  
  **Aplica-se a:** as informações neste tópico se aplicam a projetos de suplemento do VSTO para InfoPath 2010. Para obter mais informações, consulte [recursos disponíveis por tipo de projeto e aplicativo do Office](../vsto/features-available-by-office-application-and-project-type.md).  
  
  Os usuários e designers de abrem um modelo de formulário no modo de design para modificar a aparência e o layout do modelo. Os usuários abrem os formulários baseados em um modelo de formulário para adicionar conteúdo.  
  
  A janela de visualização de impressão permite que os designers e os usuários visualizar as páginas de um formulário ou modelo de formulário antes que eles imprimirem-los.  
  
> [!NOTE]  
>  O **AddIns** guia não aparece na janela de visualização de impressão. Se você quiser uma guia personalizada para aparecer na janela de visualização de impressão, verifique se o **OfficeId** da guia não está definida **TabAddIns**.  
  
 Você deve especificar o tipo de faixa de opções de cada janela no qual você deseja que apareçam da faixa de opções.  
  
## <a name="specify-the-ribbon-type-in-the-ribbon-designer"></a>Especifique o tipo de faixa de opções no designer de faixa de opções  
 Se você estiver usando o **faixa de opções (Visual Designer)** item, clique no **RibbonType** propriedade da faixa de opções no **propriedades** janela e, em seguida, selecione qualquer uma das IDs da faixa de opções descrito na tabela a seguir.  
  
|ID da faixa de opções|Janela em que a faixa de opções será exibida quando você executa o projeto|  
|---------------|---------------------------------------------------------------------|  
|**Microsoft.InfoPath.Designer**|Windows que exibem um modelo de formulário é aberto no modo de design.|  
|**Microsoft.InfoPath.Editor**|Windows que exibem um formulário que é baseado em um modelo de formulário.|  
|**Microsoft.InfoPath.PrintPreview**|A janela de visualização de impressão.|  
  
 Você pode adicionar mais de uma faixa de opções para um projeto. Se mais de uma faixa de opções compartilha uma ID da faixa de opções, substituir os `CreateRibbonExtensibilityObject` método no `ThisAddin` classe do seu projeto para especificar quais da faixa de opções para exibir no tempo de execução. Para obter mais informações, consulte [visão geral da faixa de opções](../vsto/ribbon-overview.md).  
  
## <a name="specify-the-ribbon-type-by-using-ribbon-xml"></a>Especifique o tipo de faixa de opções usando XML da faixa de opções  
 Se você estiver usando o **da faixa de opções (XML)** item, verifique o valor da *ribbonID* parâmetro no <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> método e retorne a faixa de opções apropriada.  
  
 O <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> método é gerado automaticamente pelo Visual Studio no arquivo de código da faixa de opções. O *ribbonID* parâmetro é uma cadeia de caracteres que identifica o tipo de janela do InfoPath que está sendo aberto.  
  
 O exemplo de código a seguir demonstra como exibir uma faixa de opções personalizada apenas em uma janela que exibe um modelo de formulário no modo de design. Especificada na faixa de opções para exibir o `GetResourceText()` método, que é gerado na classe da faixa de opções. Para obter mais informações sobre a classe da faixa de opções, consulte [XML da faixa de opções](../vsto/ribbon-xml.md).  
  
 [!code-csharp[Trin_RibbonInfoPathBasic#1](../vsto/codesnippet/CSharp/myinfopathproject/ribbon.cs#1)]
 [!code-vb[Trin_RibbonInfoPathBasic#1](../vsto/codesnippet/VisualBasic/myinfopathproject/ribbon.vb#1)]  
  
## <a name="see-also"></a>Consulte também  
 [Acesso a faixa de opções em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)   
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [Designer de faixa de opções](../vsto/ribbon-designer.md)   
 [XML da faixa de opções](../vsto/ribbon-xml.md)  
  
  
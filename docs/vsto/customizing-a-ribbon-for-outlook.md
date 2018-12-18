---
title: Personalizar uma faixa de opções do Outlook
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 035a38abc2285f744841b1d095387f61a21335a7
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671528"
---
# <a name="customize-a-ribbon-for-outlook"></a>Personalizar uma faixa de opções do Outlook
  Quando você personaliza a faixa de opções no Microsoft Office Outlook, você deve considerar onde sua faixa de opções personalizada será exibida no aplicativo. O Outlook exibe a faixa de opções na interface do usuário principal do aplicativo (UI) e no windows que são abertos quando os usuários executam determinadas tarefas, como a criação de mensagens de email. Essas janelas de aplicativo são nomeadas inspetores.  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [How do i: Use o designer de faixa de opções para personalizar a faixa de opções no Outlook?](http://go.microsoft.com/fwlink/?LinkID=130312).  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
## <a name="add-a-custom-ribbon-to-the-main-application-ui"></a>Adicionar uma faixa de opções personalizada ao aplicativo principal da interface do usuário  
 O aplicativo principal da interface do usuário no Outlook é chamado o Explorer. Se você estiver usando o **faixa de opções (Visual Designer)** item, você pode adicionar uma faixa de opções para o Explorer clicando o **RibbonType** propriedade da faixa de opções no **propriedades** janela, e, em seguida, selecionando **Microsoft.Outlook.Explorer**.  
  
## <a name="assign-a-ribbon-to-an-inspector"></a>Atribuir uma faixa de opções a um Inspetor  
 Identifique o Inspetor de que deseja personalizar, especificando o tipo de faixa de opções que corresponde à classe de mensagem para o Inspetor.  
  
 Se você estiver usando o **faixa de opções (Visual Designer)** item, clique no **RibbonType** propriedade da faixa de opções no **propriedades** janela e, em seguida, selecione uma ou mais IDs de faixa de opções a lista de valores.  
  
 Você pode adicionar mais de uma faixa de opções para um projeto. Se mais de uma faixa de opções compartilha uma ID da faixa de opções, substituir os `CreateRibbonExtensibilityObject` método no `ThisAddin` classe do seu projeto para especificar qual faixa de opções para exibir no tempo de execução. Para obter mais informações, consulte [visão geral da faixa de opções](../vsto/ribbon-overview.md). Para obter mais informações sobre cada tipo de faixa de opções, consulte o artigo técnico [personalizar a faixa de opções no Outlook 2007](/previous-versions/office/developer/office-2007/bb226712(v=office.12)).  
  
## <a name="specify-the-ribbon-type-by-using-ribbon-xml"></a>Especifique o tipo de faixa de opções usando XML da faixa de opções  
 Se você estiver usando o **da faixa de opções (XML)** item, verifique o valor da *ribbonID* parâmetro no <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> método e retorne a faixa de opções apropriada.  
  
 O <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> método é gerado automaticamente pelo Visual Studio no arquivo de código da faixa de opções. O *ribbonID* parâmetro é uma cadeia de caracteres que identifica o Explorer ou um tipo específico de Inspetor. Para obter uma lista completa de possíveis valores da *ribbonID* parâmetro, consulte o artigo técnico [personalizar a faixa de opções no Outlook 2007](/previous-versions/office/developer/office-2007/bb226712(v=office.12)).  
  
 O exemplo de código a seguir demonstra como exibir um personalizado somente na faixa de opções de `Microsoft.Outlook.Mail.Compose` Inspetor. Esse é o Inspetor que é aberta quando um usuário cria uma nova mensagem de email. Especificada na faixa de opções para exibir o `GetResourceText()` método, que é gerado na **faixa de opções** classe. Para obter mais informações sobre o **faixa de opções** classe, consulte [XML da faixa de opções](../vsto/ribbon-xml.md).  
  
 [!code-csharp[Trin_RibbonOutlookBasic#1](../vsto/codesnippet/CSharp/Trin_RibbonOutlookBasic/Ribbon1.cs#1)]
 [!code-vb[Trin_RibbonOutlookBasic#1](../vsto/codesnippet/VisualBasic/Trin_RibbonOutlookBasic/Ribbon1.vb#1)]  
  
## <a name="see-also"></a>Consulte também  
 [Acesso a faixa de opções em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)   
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [Designer de faixa de opções](../vsto/ribbon-designer.md)   
 [XML da faixa de opções](../vsto/ribbon-xml.md)  
  
  
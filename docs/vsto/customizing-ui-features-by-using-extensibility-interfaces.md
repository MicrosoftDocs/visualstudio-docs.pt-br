---
title: Personalizar recursos de interface do usuário usando interfaces de extensibilidade
description: Saiba que as ferramentas de desenvolvimento do Office no Visual Studio fornecem interfaces de extensibilidade que ajudam você a personalizar os recursos da interface do usuário.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ICustomTaskPaneConsumer interface
- IRibbonExtensibility interface
- UI customizing [Office development in Visual Studio]
- user interfaces [Office development in Visual Studio], customizing
- application-level add-ins [Office development in Visual Studio], extensibility interfaces
- customizing UI features [Office development in Visual Studio]
- FormRegionStartup interface
- add-ins [Office development in Visual Studio], extensibility interfaces
- extensibility interfaces [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 86f4e5f286d817fb3f657e40399eccd3a2b4de73
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828027"
---
# <a name="customize-ui-features-by-using-extensibility-interfaces"></a>Personalizar recursos de interface do usuário usando interfaces de extensibilidade
  As ferramentas de desenvolvimento do Office no Visual Studio fornecem classes e designers que lidam com muitos detalhes de implementação ao usá-los para criar painéis de tarefas personalizados, personalizações da faixa de forma e regiões de formulário do Outlook em um suplemento do VSTO. No entanto, você também pode implementar a *interface de extensibilidade* para cada recurso se tiver requisitos especiais.

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

## <a name="overview-of-extensibility-interfaces"></a>Visão geral das interfaces de extensibilidade
 Microsoft Office define um conjunto de interfaces de extensibilidade que os suplementos do VSTO do COM podem implementar para personalizar determinados recursos, como a faixa de faixas. Essas interfaces fornecem controle total sobre os recursos aos quais fornecem acesso. No entanto, a implementação dessas interfaces requer algum conhecimento da interoperabilidade COM em código gerenciado. Em alguns casos, o modelo de programação dessas interfaces também não é intuitivo para os desenvolvedores acostumados com o .NET Framework.

 Quando você cria um suplemento do VSTO usando os modelos de projeto do Office no Visual Studio, não é necessário implementar as interfaces de extensibilidade para personalizar recursos como a faixa de bits. O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] implementa essas interfaces para você. Em vez disso, você pode usar classes e designers mais intuitivos fornecidos pelo Visual Studio. No entanto, você ainda pode implementar as interfaces de extensibilidade diretamente em seu suplemento do VSTO, se desejar.

 Para obter mais informações sobre as classes e os designers que o Visual Studio fornece para esses recursos, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md), [Designer de faixa](../vsto/ribbon-designer.md)de [formas e criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md).

## <a name="extensibility-interfaces-you-can-implement-in-a-vsto-add-in"></a>Interfaces de extensibilidade que podem ser implementadas em um suplemento do VSTO
 A tabela a seguir lista as interfaces de extensibilidade que você pode implementar e os aplicativos que dão suporte a elas.

|Interface|Descrição|Aplicativos|
|---------------|-----------------|------------------|
|<xref:Microsoft.Office.Core.IRibbonExtensibility>|Implemente essa interface para personalizar a interface do usuário da faixa de faixas. **Observação:**  Você pode adicionar um item **da faixa de bits (XML)** a um projeto para gerar uma <xref:Microsoft.Office.Core.IRibbonExtensibility> implementação padrão em seu suplemento do VSTO. Para obter mais informações, consulte [Ribbon XML](../vsto/ribbon-xml.md).|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> InfoPath 2010<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Project<br /><br /> Visio<br /><br /> Word|
|<xref:Microsoft.Office.Core.ICustomTaskPaneConsumer>|Implemente essa interface para criar um painel de tarefas personalizado.|Excel<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Word|
|<xref:Microsoft.Office.Interop.Outlook.FormRegionStartup>|Implemente essa interface para criar uma região de formulário do Outlook.|Outlook|

 Há várias outras interfaces de extensibilidade que são definidas por Microsoft Office, como <xref:Microsoft.Office.Core.IBlogExtensibility> , <xref:Microsoft.Office.Core.EncryptionProvider> e <xref:Microsoft.Office.Core.SignatureProvider> . O Visual Studio não oferece suporte à implementação dessas interfaces em um suplemento do VSTO criado usando os modelos de projeto do Office.

## <a name="use-extensibility-interfaces"></a>Usar interfaces de extensibilidade
 Para personalizar um recurso de interface do usuário usando uma interface de extensibilidade, implemente a interface apropriada em seu projeto de suplemento do VSTO. Em seguida, substitua o <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> método para retornar uma instância da classe que implementa a interface.

 Para um aplicativo de exemplo que demonstra como implementar as <xref:Microsoft.Office.Core.IRibbonExtensibility> <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer> interfaces, e <xref:Microsoft.Office.Interop.Outlook.FormRegionStartup> em um suplemento do VSTO para Outlook, consulte o exemplo do Gerenciador de interface do usuário em [exemplos de desenvolvimento do Office](../vsto/office-development-samples.md).

### <a name="example-of-implementing-an-extensibility-interface"></a>Exemplo de implementação de uma interface de extensibilidade
 O exemplo de código a seguir demonstra uma implementação simples da <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer> interface para criar um painel de tarefas personalizado. Este exemplo define duas classes:

- A `TaskPaneHelper` classe implementa <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer> para criar e exibir um painel de tarefas personalizado.

- A `TaskPaneUI` classe fornece a interface do usuário do painel de tarefas. Os atributos da `TaskPaneUI` classe tornam a classe visível para com, o que permite que Microsoft Office aplicativos descubram a classe. Neste exemplo, a interface do usuário está vazia <xref:System.Windows.Forms.UserControl> , mas você pode adicionar controles modificando o código.

  > [!NOTE]
  > Para expor a `TaskPaneUI` classe a com, você também deve definir a propriedade **Register for com Interop** para o projeto.

  :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_SimpleExtensibilityInterface/ThisAddIn.vb" id="Snippet1":::
  :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_SimpleExtensibilityInterface/ThisAddIn.cs" id="Snippet1":::

  Para obter mais informações sobre como implementar <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer> o, consulte [criar painéis de tarefas personalizados no sistema do Office 2007](/previous-versions/office/developer/office-2007/aa338197(v=office.12)) na documentação do Microsoft Office.

### <a name="example-of-overriding-the-requestservice-method"></a>Exemplo de substituição do método RequestService
 O exemplo de código a seguir demonstra como substituir o <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> método para retornar uma instância da `TaskPaneHelper` classe do exemplo de código anterior. Ele verifica o valor do parâmetro do *perguid* para determinar qual interface está sendo solicitada e, em seguida, retorna um objeto que implementa essa interface.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_SimpleExtensibilityInterface/ThisAddIn.vb" id="Snippet2":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_SimpleExtensibilityInterface/ThisAddIn.cs" id="Snippet2":::

## <a name="see-also"></a>Consulte também
- [Exemplos e orientações de desenvolvimento do Office](../vsto/office-development-samples-and-walkthroughs.md)
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)
- [Chamar código em suplementos do VSTO de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)
- [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)

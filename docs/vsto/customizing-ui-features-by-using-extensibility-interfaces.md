---
title: Personalizar os recursos de interface do usuário usando interfaces de extensibilidade
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ec1f538515c8765629e812b8d7f4070476dd95ba
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670829"
---
# <a name="customize-ui-features-by-using-extensibility-interfaces"></a>Personalizar os recursos de interface do usuário usando interfaces de extensibilidade
  As ferramentas de desenvolvimento do Office no Visual Studio fornecem classes e designers que lidar com muitos detalhes de implementação quando usá-los para criar painéis de tarefas personalizados, personalizações da faixa de opções e regiões de formulário do Outlook em um suplemento do VSTO. No entanto, você também pode implementar o *interface de extensibilidade* para cada recurso por conta própria, se você tiver requisitos especiais.  
  
 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]  
  
## <a name="overview-of-extensibility-interfaces"></a>Visão geral das interfaces de extensibilidade  
 Microsoft Office define um conjunto de interfaces de extensibilidade COM VSTO Add-ins podem ser implementados para personalizar determinados recursos, como a faixa de opções. Essas interfaces fornecem controle total sobre os recursos que eles fornecem acesso ao. No entanto, a implementação dessas interfaces requer algum conhecimento de interoperabilidade COM em código gerenciado. Em alguns casos, o modelo de programação dessas interfaces também não é intuitivo para os desenvolvedores que estão acostumados com o .NET Framework.  
  
 Quando você cria um suplemento do VSTO usando os modelos de projeto do Office no Visual Studio, não é necessário que implementar as interfaces de extensibilidade para personalizar os recursos, como a faixa de opções. O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] implementa essas interfaces para você. Em vez disso, você pode usar classes de mais intuitivo e designers fornecidos pelo Visual Studio. No entanto, você ainda pode implementar as interfaces de extensibilidade diretamente no seu suplemento do VSTO se você quiser.  
  
 Para obter mais informações sobre as classes e os designers que o Visual Studio fornece para esses recursos, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md), [designer de faixa de opções](../vsto/ribbon-designer.md), e [Criar formulário do Outlook](../vsto/creating-outlook-form-regions.md).  
  
## <a name="extensibility-interfaces-you-can-implement-in-a-vsto-add-in"></a>Interfaces de extensibilidade que você pode implementar em um suplemento do VSTO  
 A tabela a seguir lista as interfaces de extensibilidade que você pode implementar e os aplicativos que dão suporte a eles.  
  
|Interface|Descrição|Aplicativos|  
|---------------|-----------------|------------------|  
|<xref:Microsoft.Office.Core.IRibbonExtensibility>|Implemente essa interface para personalizar a interface do usuário da faixa de opções. **Observação:** você pode adicionar uma **da faixa de opções (XML)** item a um projeto para gerar um padrão <xref:Microsoft.Office.Core.IRibbonExtensibility> implementação no seu suplemento do VSTO. Para obter mais informações, consulte [XML da faixa de opções](../vsto/ribbon-xml.md).|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> InfoPath 2010<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Projeto<br /><br /> Visio<br /><br /> Palavra|  
|<xref:Microsoft.Office.Core.ICustomTaskPaneConsumer>|Implemente essa interface para criar um painel de tarefas personalizado.|Excel<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Palavra|  
|<xref:Microsoft.Office.Interop.Outlook.FormRegionStartup>|Implemente essa interface para criar uma região de formulário do Outlook.|Outlook|  
  
 Existem várias outras interfaces de extensibilidade que são definidos pelo Microsoft Office, como <xref:Microsoft.Office.Core.IBlogExtensibility>, <xref:Microsoft.Office.Core.EncryptionProvider>, e <xref:Microsoft.Office.Core.SignatureProvider>. Visual Studio não oferece suporte para a implementação dessas interfaces em um suplemento VSTO criado usando os modelos de projeto do Office.  
  
## <a name="use-extensibility-interfaces"></a>Use interfaces de extensibilidade  
 Para personalizar um recurso de interface do usuário usando uma interface de extensibilidade, implemente a interface apropriada em seu projeto de suplemento do VSTO. Em seguida, substituir o <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> método para retornar uma instância da classe que implementa a interface.  
  
 Para um aplicativo de exemplo que demonstra como implementar o <xref:Microsoft.Office.Core.IRibbonExtensibility>, <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer>, e <xref:Microsoft.Office.Interop.Outlook.FormRegionStartup> interfaces em um suplemento do VSTO para Outlook, consulte o exemplo do Gerenciador de interface do usuário no [amostras de desenvolvimento do Office](../vsto/office-development-samples.md).  
  
### <a name="example-of-implementing-an-extensibility-interface"></a>Exemplo de implementação de uma interface de extensibilidade  
 O exemplo de código a seguir demonstra uma implementação simples dos <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer> interface para criar um painel de tarefas personalizado. Este exemplo define duas classes:  
  
- O `TaskPaneHelper` implementos de classe <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer> para criar e exibir um painel de tarefas personalizado.  
  
- O `TaskPaneUI` classe fornece a interface do usuário do painel de tarefas. Os atributos para o `TaskPaneUI` classe torná-la visível para COM, que permite que os aplicativos do Microsoft Office descobrir a classe. Neste exemplo, a interface do usuário é um vazio <xref:System.Windows.Forms.UserControl>, mas você pode adicionar controles ao modificar o código.  
  
  > [!NOTE]  
  >  Para expor os `TaskPaneUI` classe ao COM, você também deve definir o **registrar para interoperabilidade COM** propriedade para o projeto.  
  
  [!code-vb[Trin_SimpleExtensibilityInterface#1](../vsto/codesnippet/VisualBasic/Trin_SimpleExtensibilityInterface/ThisAddIn.vb#1)]
  [!code-csharp[Trin_SimpleExtensibilityInterface#1](../vsto/codesnippet/CSharp/Trin_SimpleExtensibilityInterface/ThisAddIn.cs#1)]  
  
  Para obter mais informações sobre como implementar <xref:Microsoft.Office.Core.ICustomTaskPaneConsumer>, consulte [criar painéis de tarefas personalizados no 2007 Office system](/previous-versions/office/developer/office-2007/aa338197(v=office.12)) na documentação do Microsoft Office.  
  
### <a name="example-of-overriding-the-requestservice-method"></a>Exemplo de substituição do método RequestService  
 O exemplo de código a seguir demonstra como substituir a <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> método para retornar uma instância da `TaskPaneHelper` classe do exemplo de código anterior. Ele verifica o valor de *serviceGuid* parâmetro para determinar qual interface está sendo solicitada e, em seguida, retorna um objeto que implementa a interface.  
  
 [!code-vb[Trin_SimpleExtensibilityInterface#2](../vsto/codesnippet/VisualBasic/Trin_SimpleExtensibilityInterface/ThisAddIn.vb#2)]
 [!code-csharp[Trin_SimpleExtensibilityInterface#2](../vsto/codesnippet/CSharp/Trin_SimpleExtensibilityInterface/ThisAddIn.cs#2)]  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo e exemplos de desenvolvimento do office](../vsto/office-development-samples-and-walkthroughs.md)   
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)   
 [Chamar o código no VSTO Add-ins de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)  
  
  
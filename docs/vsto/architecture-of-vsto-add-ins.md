---
title: Arquitetura de suplementos do VSTO
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VSTOLoader.dll
- architecture [Office development in Visual Studio], application-level add-ins
- vstoee.dll
- application-level add-ins [Office development in Visual Studio], architecture
- add-ins [Office development in Visual Studio], architecture
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: dccfd3a3344ef9bde46b0b1e6bed50294d832acb
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248157"
---
# <a name="architecture-of-vsto-add-ins"></a>Arquitetura de suplementos do VSTO
  Suplementos do VSTO criados usando as ferramentas de desenvolvedor do Office no Visual Studio tem recursos de arquitetura que enfatizam a estabilidade e segurança e permitem que eles trabalham em conjunto com o Microsoft Office. Este tópico descreve os seguintes aspectos de suplementos do VSTO:  
  
- [Entender os suplementos do VSTO](#UnderstandingAddIns)  
  
- [Componentes de suplementos do VSTO](#AddinComponents)  
  
- [Como o VSTO Add-ins funcionam com aplicativos do Microsoft Office](#HowAddinsWork)  
  
  [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]  
  
  Para obter informações gerais sobre a criação de suplementos do VSTO, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41; ](../vsto/office-solutions-development-overview-vsto.md) e [começar a programar VSTO Add-ins](../vsto/getting-started-programming-vsto-add-ins.md).  
  
##  <a name="UnderstandingAddIns"></a> Entender os suplementos do VSTO  
 Quando você usa o Office developer tools no Visual Studio para criar um suplemento do VSTO, você criará um assembly de código gerenciado que é carregado por um aplicativo do Microsoft Office. Depois que o assembly é carregado, o suplemento do VSTO pode responder a eventos que são gerados no aplicativo (por exemplo, quando um usuário clica em um item de menu). O suplemento do VSTO também pode chamar o modelo de objeto para automatizar e estender o aplicativo e ele pode usar qualquer uma das classes no [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)].  
  
 O assembly se comunica com componentes do aplicativo por meio do assembly de interoperabilidade primário do aplicativo. Para obter mais informações, consulte [assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md) e [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md).  
  
 Se vários suplementos do VSTO são instalados para um aplicativo, cada suplemento do VSTO é carregado em um domínio de aplicativo diferente. Isso significa que um suplemento VSTO que se comporte incorretamente não pode causar outros suplementos do VSTO falhe. Ele também ajuda a garantir que, quando o aplicativo é fechado, todos os do suplemento do VSTO assemblies são descarregados da memória. Para obter mais informações sobre domínios de aplicativo, consulte [domínios de aplicativo](/dotnet/framework/app-domains/application-domains).  
  
> [!NOTE]  
>  Suplementos do VSTO que você criar usando as ferramentas de desenvolvedor do Office no Visual Studio são projetados para ser usado somente quando o host de aplicativo do Microsoft Office é iniciado por um usuário final. Se o aplicativo for iniciado por meio de programação (por exemplo, usando a automação), o suplemento do VSTO pode não funcionar conforme o esperado.  
  
##  <a name="AddinComponents"></a> Componentes de suplementos do VSTO  
 Embora o assembly do suplemento do VSTO é o componente principal, há vários outros componentes que desempenham um papel importante na maneira como os aplicativos do Microsoft Office descobrirem e carregar suplementos do VSTO.  
  
### <a name="registry-entries"></a>Entradas do registro  
 Aplicativos do Microsoft Office descobrem VSTO Add-ins procurando por um conjunto de entradas do registro. Para obter uma lista completa das entradas do registro usadas pelos suplementos do VSTO, consulte [entradas do registro para suplementos VSTO](../vsto/registry-entries-for-vsto-add-ins.md).  
  
 Quando você compila sua solução, o Visual Studio cria todas as entradas de registro necessárias no computador de desenvolvimento para que você possa depurar e executar seu suplemento do VSTO. Para obter mais informações, consulte [soluções do Office compilar](../vsto/building-office-solutions.md).  
  
 Se você usar o ClickOnce para implantar sua solução, o programa de instalação gerado automaticamente pelo processo de publicação cria as chaves do registro no computador do usuário final. Para obter mais informações, consulte [implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).  
  
### <a name="deployment-manifest-and-application-manifest"></a>Manifesto de implantação e o manifesto do aplicativo  
 Suplementos do VSTO usarem manifestos de aplicativo e manifestos de implantação para identificar e carregar a versão mais atual do assembly do suplemento do VSTO. O manifesto de implantação aponta para o manifesto do aplicativo atual. O manifesto do aplicativo para indicar o assembly do suplemento do VSTO e especifica a classe de ponto de entrada para executar no assembly. Para obter mais informações, consulte [manifestos do aplicativo e implantação em soluções do Office](../vsto/application-and-deployment-manifests-in-office-solutions.md).  
  
### <a name="visual-studio-tools-for-office-runtime"></a>Visual Studio Tools for Office Runtime  
 Para executar o VSTO Add-ins que são criados usando as ferramentas de desenvolvedor do Office no Visual Studio, os computadores do usuário final devem ter o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] instalado. O tempo de execução inclui componentes não gerenciados e um conjunto de assemblies gerenciados. Os componentes não gerenciados carregar o assembly do suplemento do VSTO. Os assemblies gerenciados fornecem o modelo de objeto que usa o seu código de suplemento do VSTO para automatizar e estender o aplicativo host.  
  
 Para obter mais informações, consulte [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md).  
  
##  <a name="HowAddinsWork"></a> Como o VSTO Add-ins funcionam com aplicativos do Microsoft Office  
 Quando um usuário inicia um aplicativo do Microsoft Office, o aplicativo usa o manifesto de implantação e o manifesto do aplicativo para localizar e carregar a versão mais atual do assembly do suplemento do VSTO. A ilustração a seguir mostra a arquitetura básica desses suplementos do VSTO.  
  
 ![Arquitetura de suplemento do office de 2007](../vsto/media/office07addin.png "arquitetura de suplemento do Office de 2007")  
  
> [!NOTE]  
>  Em soluções do Office que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)], soluções chamam o modelo de objeto do aplicativo host, usando as informações de tipo PIA que estão incorporadas no assembly de solução, em vez de chamar o PIA diretamente. Para obter mais informações, consulte [Design e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md).  
  
### <a name="loading-process"></a>Processo de carregamento  
 Quando um usuário inicia um aplicativo, ocorrem as seguintes etapas:  
  
1.  O aplicativo verifica o registro para as entradas que identificam o VSTO Add-ins que foram criados usando as ferramentas de desenvolvedor do Office no Visual Studio.  
  
2.  Se o aplicativo encontrar essas entradas do registro, o aplicativo carrega vstoee, que carrega o vstoloader. dll. Eles não são gerenciados DLLs que são os componentes do carregador para o Visual Studio 2010 Tools for Office Runtime. Para obter mais informações, consulte [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md).  
  
3.  *Vstoloader. dll* carrega o [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] e começa a parte gerenciada do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)].  
  
4.  O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] verifica se há atualizações de manifesto e baixa os manifestos de aplicativo e implantação mais recentes.  
  
5.  O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] executa uma série de verificações de segurança. Para obter mais informações, consulte [soluções do Office Secure](../vsto/securing-office-solutions.md).  
  
6.  Se o suplemento do VSTO é confiável para ser executado, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] usa o manifesto de implantação e o manifesto do aplicativo para verificar se há atualizações do assembly. Se uma nova versão do assembly estiver disponível, o tempo de execução baixa a nova versão do assembly a ser o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] cache no computador cliente. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  
  
7.  O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] cria um novo domínio de aplicativo no qual carregar o assembly do suplemento do VSTO.  
  
8.  O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] carrega o assembly do suplemento do VSTO para o domínio do aplicativo.  
  
9. O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama o <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> método no seu suplemento VSTO, se você tiver substituído a ele.  
  
     Opcionalmente, você pode substituir esse método para expor um objeto no seu suplemento do VSTO para outras soluções do Microsoft Office. Para obter mais informações, consulte [chamar o código no VSTO Add-ins de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md).  
  
10. O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama o <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> método no seu suplemento VSTO, se você tiver substituído a ele.  
  
     Opcionalmente, você pode substituir esse método para estender um recurso do Microsoft Office, retornando um objeto que implementa uma interface de extensibilidade. Para obter mais informações, consulte [recursos de interface do usuário personalizar usando interfaces de extensibilidade](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md).  
  
    > [!NOTE]  
    >  O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] faz chamadas separadas para o <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> método para cada interface de extensibilidade que tem suporte pelo aplicativo host. Embora a primeira chamada para o <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> método geralmente acontece antes da chamada para o `ThisAddIn_Startup` método, o suplemento do VSTO não faça suposições sobre quando o <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> método será chamado ou quantas vezes ele será chamado.  
  
11. O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama o `ThisAddIn_Startup` método no seu suplemento do VSTO. Esse método é o manipulador de eventos padrão para o <xref:Microsoft.Office.Tools.AddInBase.Startup> eventos. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).  
  
## <a name="see-also"></a>Consulte também  
 [Arquitetura de soluções do Office no Visual Studio](../vsto/architecture-of-office-solutions-in-visual-studio.md)   
 [Arquitetura de personalizações no nível do documento](../vsto/architecture-of-document-level-customizations.md)   
 [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md)   
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)   
 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)  
  
  
---
title: Visual Studio Tools for Office runtime overview
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office runtime [Office development in Visual Studio], about Office runtime
- VSTOLoader.dll
- runtime loader [Office development in Visual Studio]
- Office runtime [Office development in Visual Studio], assemblies
- Office runtime [Office development in Visual Studio]
- runtime [Office development in Visual Studio], assemblies
- vstoee.dll
- Visual Studio Tools for Office runtime
- Office solutions [Office development in Visual Studio], runtime
- solutions [Office development in Visual Studio], runtime
- versions [Office development in Visual Studio], runtime
- assemblies [Office development in Visual Studio], runtime
- runtime [Office development in Visual Studio], about VSTO runtime
- solution loader [Office development in Visual Studio]
- runtime [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b169242b9828f47f1ecfb87ebf02a9f86234699f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49836990"
---
# <a name="visual-studio-tools-for-office-runtime-overview"></a>Visual Studio Tools for Office runtime overview
  Para executar soluções criadas usando o Microsoft Office developer tools no Visual Studio, o Visual Studio 2010 Tools for Office runtime deve ser instalado nos computadores dos usuários finais. Para obter mais informações, consulte [como: instalar o Visual Studio Tools for Office runtime redistribuível](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md). O Visual Studio 2010 Tools for Office runtime consiste em dois componentes principais:  
  
- As extensões do Office para o .NET Framework. Esses componentes são assemblies gerenciados que fornecem a camada de comunicação entre a sua solução e o aplicativo do Microsoft Office. Para obter mais informações, consulte [entender as extensões do Office para o .NET Framework](#officeextensions).  
  
- O carregador de solução do Office. Esse componente é um conjunto de DLLs não gerenciadas que os aplicativos do Office usam para carregar o tempo de execução e suas soluções. Para obter mais informações, consulte [entender o carregador de solução do Office](#UnmanagedLoader).  
  
  O tempo de execução pode ser instalado de várias maneiras diferentes. Dependendo da configuração do computador, os diferentes componentes de tempo de execução são instalados durante a instalação do tempo de execução. Para obter mais informações, consulte [ferramentas do Visual Studio para cenários de instalação do Office em tempo de execução](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md).  
  
##  <a name="officeextensions"></a> Entender as extensões do Office para o .NET Framework  
 O Visual Studio 2010 Tools for Office runtime inclui extensões do Office para o .NET Framework 3.5, o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] e versões posteriores. As soluções que se destinam a cada versão do .NET Framework usam as extensões apropriadas para a versão em questão.  
  
 Essas extensões consistem em assemblies que suas soluções usam para automatizar e estender os aplicativos do Office. Quando você cria um projeto do Office, o Visual Studio adiciona automaticamente as referências aos assemblies que são usados para o tipo de projeto e o .NET Framework de destino do projeto. Para obter mais informações sobre os assemblies nas extensões do Office, consulte [Assemblies no Visual Studio Tools para Office runtime](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md).  
  
### <a name="design-differences-in-the-office-extensions"></a>Diferenças de design nas extensões do Office  
 A maioria dos tipos usados por você nas extensões do Office para o .NET Framework 3.5 é de classes. Essas são as mesmas classes que foram incluídas nas versões anteriores do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]. Por outro lado, a maioria dos tipos que você usa nas extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posteriores são interfaces. Por exemplo, quando você seleciona os [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, o <xref:Microsoft.Office.Tools.Excel.Worksheet> e <xref:Microsoft.Office.Tools.Word.Document> tipos são interfaces em vez de classes.  
  
 Na maioria dos casos, o código que você escreve em soluções do Office será igual, mesmo se sua solução se destinar ao .NET Framework 3.5 ou ao [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]. No entanto, alguns recursos exigem um código diferente quando você tem como destino versões diferentes do .NET Framework. Para obter mais informações, consulte [soluções do Office de migrar para o .NET Framework 4 ou posterior](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md).  
  
### <a name="interfaces-in-the-office-extensions-for-the-net-framework-4-or-later"></a>Interfaces nas extensões do Office para o .NET Framework 4 ou posterior  
 A maioria das interfaces nas extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posteriormente não se destinam a ser implementada pelo código do usuário. As únicas interfaces que você pode implementar diretamente têm nomes que começam com a letra **eu**, como <xref:Microsoft.Office.Tools.Excel.ISmartTagExtension>.  
  
 Todas as interfaces que não começam com a letra **I** são implementados internamente pelo Visual Studio 2010 Tools para Office runtime, e essas interfaces podem mudar em versões futuras. Para criar objetos que implementam essas interfaces, use os métodos fornecidos pelo objeto `Globals.Factory` no seu projeto. Por exemplo, para obter um objeto que implemente a interface <xref:Microsoft.Office.Tools.Excel.SmartTag>, use o método `Globals.Factory.CreateSmartTag`. Para obter mais informações sobre `Globals.Factory`, consulte [Global de acesso a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).  
  
### <a name="enable-type-equivalence-and-embedded-types-in-projects-that-target-the-net-framework-4-or-later"></a>Habilitar a equivalência de tipo e tipos inseridos em projetos que segmentam o .NET Framework 4 ou posterior  
 Porque o modelo de objeto das extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior se baseiam em interfaces, você pode usar o recurso de equivalência de tipo no Visual c# e Visual Basic no Visual Studio para inserir informações de tipo a [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] em sua solução . Esse recurso permite que as soluções do Office e o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] sejam distribuídos em versões independentes umas das outras. Por exemplo, se sua solução usar a interface <xref:Microsoft.Office.Tools.Word.Document> como um tipo inserido e a próxima versão de tempo de execução adicionar membros à interface <xref:Microsoft.Office.Tools.Word.Document>, sua solução ainda funcionará com a próxima versão de tempo de execução. Se sua solução não usa o <xref:Microsoft.Office.Tools.Word.Document> interface como um tipo inserido, em seguida, sua solução não funcionará mais com a próxima versão do tempo de execução.  
  
 Por padrão, o recurso de equivalência de tipo não é habilitado quando você cria um projeto do Office que se destina a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. Se você quiser habilitar esse recurso, defina as **Embed Interop Types** propriedade de qualquer uma das seguintes referências de assembly em seu projeto para **verdadeiro**:  
  
- Microsoft.Office.Tools.dll  
  
- Microsoft.Office.Tools.Common.dll  
  
- Microsoft.Office.Tools.Excel.dll  
  
- Microsoft.Office.Tools.Outlook.dll  
  
- Microsoft.Office.Tools.Word.dll  
  
  Depois de fazer essa alteração, as informações de tipo para todos os tipos de tempo de execução usados pelo projeto são inseridas no assembly da solução quando você compila o projeto. Informações de tipo inseridas, em vez das informações de tipo nos assemblies referenciados, são usadas pela solução em tempo de execução.  
  
##  <a name="UnmanagedLoader"></a> Entender o carregador de solução do Office  
 O Visual Studio Tools for Office runtime inclui várias DLLs não gerenciadas que os aplicativos do Office usam para carregar o tempo de execução e as soluções do Office. Embora você nunca deva ter que trabalhar com essas DLL diretamente, saber as finalidades delas podem ajudar a compreender melhor a arquitetura das soluções do Office.  
  
 Para obter informações sobre como esses componentes são usados durante o processo de carregamento, consulte [arquitetura de personalizações no nível do documento](../vsto/architecture-of-document-level-customizations.md) e [arquitetura do VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md).  
  
### <a name="vstoeedll"></a>VSTOEE.dll  
 Quando um usuário abre uma personalização no nível de documento ou inicia um suplemento do VSTO, o aplicativo do Office chama *vstoee* para executar as tarefas necessárias para carregar o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)].  
  
 *Vstoee* torna-se de que a versão correta do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] é carregado para a solução e a versão instalada do Office. Embora várias versões dos [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] pode ser instalado no mesmo computador, apenas uma instância do *vstoee* é instalado por vez. Esse é o *vstoee* que foi incluída com a versão mais recente do tempo de execução instalado no computador. Para obter mais informações sobre as diferentes versões dos [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] que pode ser usado para outras soluções, consulte [executar soluções em diferentes versões do Microsoft Office](../vsto/running-solutions-in-different-versions-of-microsoft-office.md).  
  
### <a name="vstoloaderdll"></a>VSTOLoader.dll  
 Após *vstoee* carrega a versão apropriada do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)], *vstoloader. dll* executa a maior parte do trabalho que é necessário para carregar o assembly da solução. *Vstoloader. dll* faz várias coisas:  
  
- Cria um domínio de aplicativo para cada assembly da solução.  
  
- Executa um conjunto de verificações de segurança para verificar se o assembly da solução tem permissão para executar.  
  
- Carrega a versão das extensões do Office para o .NET Framework que é exigida pela solução.  
  
  *Vstoloader. dll* também faz várias coisas que são específicas para suplementos do VSTO:  
  
- Implementa a interface <xref:Extensibility.IDTExtensibility2>. <xref:Extensibility.IDTExtensibility2> é uma interface COM que todos os suplementos do VSTO para aplicativos do Microsoft Office devem implementar. Essa interface define os métodos que o aplicativo chama para se comunicar com o suplemento do VSTO.  
  
- Ele implementa a interface IManagedAddin. Essa interface é usada pelos aplicativos do Office para ajudar a carregar suplementos do VSTO. Para obter mais informações, consulte [interface IManagedAddin](../vsto/imanagedaddin-interface.md).  
  
## <a name="understand-the-32-bit-and-64-bit-versions-of-the-runtime"></a>Entender as versões de 32 bits e 64 bits do tempo de execução  
 Há versões de 64 bits e 32 bits separadas do Visual Studio 2010 Tools para Office runtime. Essas versões do tempo de execução são usados para executar soluções em edições de 64 bits e 32 bits Office. A tabela a seguir mostra qual versão do tempo de execução é necessária para cada combinação de Windows e do Office.  
  
|Edição do Windows|Edição do Microsoft Office|Versão necessária do Visual Studio Tools for Office Runtime|  
|------------------------|---------------------------------|--------------------------------------------------------------------|  
|32 bits|32 bits|32 bits|  
|64 bits|32 bits|64 bits|  
|64 bits|64 bits|64 bits|  
  
 Quando você instala o Office, a versão necessária do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] é instalado junto com o Office. Por exemplo, quando você instala a edição de 64 bits do Office em uma versão de 64 bits do Windows, a versão de 64 bits do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] também é instalado. Para obter mais informações sobre como instalar o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] com o Office, consulte [ferramentas do Visual Studio para cenários de instalação do Office em tempo de execução](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md).  
  
 A versão de 64 bits do Office também pode executar soluções do Office que foram criadas usando modelos de projeto para o 2007 Microsoft Office system no Visual Studio 2008. No entanto, ela não pode executar soluções do Office criadas com modelos de projeto do Microsoft Office 2003 no Visual Studio 2008 nem soluções do Office criadas com o Visual Studio 2005. Para obter mais informações, consulte [executar soluções em diferentes versões do Microsoft Office](../vsto/running-solutions-in-different-versions-of-microsoft-office.md).  
  
## <a name="repair-the-visual-studio-2010-tools-for-office-runtime"></a>Reparar o Visual Studio 2010 Tools for Office runtime  
 Se você precisar reparar o tempo de execução, abra **programas e recursos** ou **adicionar ou remover programas** no painel de controle, selecione **Microsoft Visual Studio 2010 Tools for Office Runtime**na lista de programas e clique **desinstalação**. O programa de instalação que é executado permite que você repare o tempo de execução. Se você clicar **alteração**, você não terá uma opção para reparar o tempo de execução.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas do Visual Studio para cenários de instalação de tempo de execução do Office](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)   
 [Assemblies no Visual Studio Tools para Office runtime](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)   
 [Arquitetura de soluções do Office no Visual Studio](../vsto/architecture-of-office-solutions-in-visual-studio.md)   
 [Arquitetura de personalizações no nível do documento](../vsto/architecture-of-document-level-customizations.md)   
 [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Atualizar e migrar soluções do Office](../vsto/upgrading-and-migrating-office-solutions.md)  
  
  
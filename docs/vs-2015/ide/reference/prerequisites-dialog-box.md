---
title: Caixa de diálogo Pré-requisitos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Microsoft.VisualStudio.Publish.BaseProvider.Dialog.Bootstrapper
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Prerequisites dialog box
ms.assetid: 53ac863c-77a0-409b-91e5-7a4bd8b8474e
caps.latest.revision: 79
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 6aff33e7129123e2f910116a5d9352944e1c064a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49183944"
---
# <a name="prerequisites-dialog-box"></a>Caixa de diálogo Pré-requisitos
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Essa caixa de diálogo especifica quais componentes de pré-requisito são instalados, como eles são instalados e em qual ordem os pacotes são instalados.  
  
 Para acessar essa caixa de diálogo, selecione um nó do projeto no **Gerenciador de Soluções** e, no menu **Projeto**, clique em **Propriedades**. Quando o **Designer de Projeto** for exibido, clique na guia **Publicar**. Na página **Publicar**, clique em **Pré-requisitos**. Para projetos de Instalação, no menu **Projeto**, clique em **Propriedades**. Quando a caixa de diálogo **Páginas de Propriedades** for exibida, clique em **Pré-requisitos**.  
  
## <a name="uielement-list"></a>Lista UIElement  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|**Criar programa de instalação para instalar os componentes de pré-requisitos**|Inclui os componentes de pré-requisito no programa de instalação do aplicativo (Setup.exe) para que eles sejam instalados antes do aplicativo, na ordem de dependência. Por padrão, essa opção é selecionada. Se ela não for selecionada, nenhum Setup.exe será criado.|  
|**Escolher quais pré-requisitos serão instalados**|Especifica se os componentes são instalados, como [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], Crystal Reports e assim por diante.<br /><br /> Por exemplo, ao selecionar a caixa de seleção ao lado de **SQL Server 2005 Express Edition SP2**, você especifica que o programa de instalação verifica se esse componente é instalado no computador de destino e o instala se ele ainda não estiver instalado.<br /><br /> Para obter informações detalhadas sobre cada pacote de pré-requisitos, consulte a tabela de Informações de pré-requisitos adiante neste tópico.|  
|**Verificar mais componentes redistribuíveis no Microsoft Update**|Ao clicar nesse link, você será levado para o site [pacotes de bootstrapper para redistribuir componentes](http://go.microsoft.com/fwlink/?LinkId=208835) para verificar se há atualizações.|  
|**Baixar os pré-requisitos no site do fornecedor do componente**|Especifica que os componentes de pré-requisitos são instalados por meio do site do fornecedor. Esta é a opção padrão.|  
|**Baixar os pré-requisitos no mesmo local do meu aplicativo**|Especifica que os componentes de pré-requisitos são instalados por meio do mesmo local que o aplicativo. Isso copia todos os pacotes de pré-requisitos no local de publicação. Para que essa opção funcione, os pacotes do pré-requisito devem estar no computador de desenvolvimento.|  
|**Baixar os pré-requisitos no seguinte local**|Especifica que os componentes de pré-requisitos são instalados por meio do local selecionado. É possível usar o botão **Procurar** para selecionar um local.|  
  
## <a name="prerequisites-information"></a>Informações de pré-requisitos  
 Os componentes de pré-requisitos exibidos na caixa de diálogo **Pré-requisitos** podem ser diferentes daqueles da lista a seguir. Os pacotes de pré-requisitos listados na **Caixa de diálogo Pré-requisitos** são definidos automaticamente na primeira vez em que a caixa de diálogo é aberta. Se você alterar posteriormente a estrutura de destino do projeto, será necessário selecionar os pré-requisitos manualmente para corresponder à nova estrutura de destino.  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|**.NET Framework 3.5 SP1**|Esse pacote instala o seguinte:<br /><br /> -   .NET Framework versões 2.0, 3.0 e 3.5.<br />-   Suporte para todas as versões do .NET Framework em sistemas operacionais de 32 bits (x86) e 64 bits (x64).<br />-   Pacotes de idiomas para cada versão do .NET Framework que é instalada com o pacote.<br />-   Service packs para o .NET Framework 2.0 e 3.0.<br /><br /> O .NET Framework 3.0 está incluído no Windows Vista e o .NET Framework 3.5 está incluído no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. O .NET Framework 3.5 é necessário para todos os projetos do Visual Basic e Visual C# que são compilados para sistemas operacionais de 32 bits e para quais a estrutura de destino é definida como **.NET Framework 3.5**, bem como para projetos do Visual Basic e Visual C# compilados para sistemas operacionais de 64 bits. (Não há suporte para o IA64.) Observe que os projetos do Visual Basic e do Visual C# são compilados para qualquer arquitetura de CPU, por padrão. Para obter mais informações, consulte [Visão geral do Visual Studio Multi-Targeting](../../ide/visual-studio-multi-targeting-overview.md), [Redistribuindo o .NET Framework](http://msdn.microsoft.com/en-us/a18d0456-fd89-493e-97f4-756505bfe287), e [Implantando pré-requisitos de aplicativos de 64 bits](../../deployment/deploying-prerequisites-for-64-bit-applications.md).<br /><br /> Por padrão, esse item está selecionado.|  
|**.NET Framework 3.5 SP1 Client Profile**|O .NET Framework Client Profile é um subconjunto do .NET Framework 3.5 SP1 completo que tem aplicativos cliente como destino. Ele fornece um subconjunto simplificado de recursos do WPF (Windows Presentation Foundation), Windows Forms, WCF (Windows Communication Foundation) e ClickOnce. Isso possibilita cenários de implantação rápida para o WPF, Windows Forms, WCF e aplicativos de console que têm o .NET Framework Client Profile como destino. Para obter mais informações, consulte [.NET Framework Client Profile](http://msdn.microsoft.com/library/f0219919-1f02-4588-8704-327a62fd91f1).|  
|**Microsoft .NET Framework 4 (x86 e x64)**|Esse pacote instala o .NET Framework 4 para as plataformas x86 e x64.<br /><br /> Para obter mais informações, consulte [Visão geral do Visual Studio Multi-Targeting](../../ide/visual-studio-multi-targeting-overview.md), [Redistribuindo o .NET Framework](http://msdn.microsoft.com/en-us/a18d0456-fd89-493e-97f4-756505bfe287), e [Implantando pré-requisitos de aplicativos de 64 bits](../../deployment/deploying-prerequisites-for-64-bit-applications.md).<br /><br /> Por padrão, esse item está selecionado.|  
|**Microsoft .NET Framework 4 Client Profile (x86 e x64)**|O .NET Framework 4 Client Profile é um subconjunto do .NET Framework 4 completo que tem aplicativos cliente como destino. Ele fornece um subconjunto simplificado de recursos do WPF (Windows Presentation Foundation), Windows Forms, WCF (Windows Communication Foundation) e ClickOnce. Isso possibilita cenários de implantação rápida para o WPF, Windows Forms e aplicativos de console que têm o .NET Framework 4 Client Profile como destino. Para obter mais informações, consulte [.NET Framework Client Profile](http://msdn.microsoft.com/library/f0219919-1f02-4588-8704-327a62fd91f1).|  
|**Assemblies de interoperabilidade primários do Microsoft Office 2007**|Esse pacote instala os Assemblies de Interoperabilidade Primários para produtos do Microsoft Office 2007. O assembly de interoperabilidade primário permite que o código gerenciado interaja com o modelo de objeto baseado em COM de um aplicativo do Microsoft Office. Para obter mais informações, consulte [Assemblies de interoperabilidade primários do Office](http://msdn.microsoft.com/library/aa29d12c-185f-4558-a7cd-3d85f924203d).|  
|**Microsoft Visual Basic PowerPacks versão 10.0**|Power Packs são suplementos, controles, componentes e ferramentas para ajudar você a desenvolver aplicativos do Visual Basic. Essa versão contém o componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>, que permite imprimir o conteúdo de um Windows Form e a Biblioteca de Compatibilidade da Impressora, que permite que o código da impressora do Visual Basic 6.0 seja executado sem modificação.|  
|**Tempo de Execução do Microsoft Visual F# para .NET 2.0**|Esse pacote instala as bibliotecas em tempo de execução Visual F# dos sistemas operacionais x86 e x64, que fornecem suporte para programação funcional, bem como para programação imperativa (de procedimento) e tradicional orientada a objeto. Esse pacote deve ser instalado se o aplicativo ou seus componentes são criados no Visual F# e .NET Framework 2.0, .NET Framework 3.0 ou .NET Framework 3.5.<br /><br /> Para obter mais informações, consulte [Referência da linguagem F#](http://msdn.microsoft.com/library/16b706f8-b5f2-4ff7-b2c1-64df33cd6adf).|  
|**Tempo de Execução do Microsoft Visual F# para .NET 4.0**|Esse pacote instala as bibliotecas em tempo de execução Visual F# dos sistemas operacionais x86 e x64, que fornecem suporte para programação funcional, bem como para programação imperativa (de procedimento) e tradicional orientada a objeto. Esse pacote deve ser instalado se o aplicativo ou seus componentes são criados no Visual F# e .NET Framework 4.<br /><br /> Para obter mais informações, consulte [Referência da linguagem F#](http://msdn.microsoft.com/library/16b706f8-b5f2-4ff7-b2c1-64df33cd6adf).|  
|**Visualizador de Relatórios do Microsoft Visual Studio 2010**|Esse pacote instala controles do visualizador de relatórios que podem ser usados para adicionar relatórios de dados avançados ao Windows Forms e a aplicativos ASP.NET.|  
|**Microsoft Visual Studio 2010 para o Tempo de Execução do Office (x86 e x64)**|As Office Developer Tools no Visual Studio oferecem ferramentas integradas e fáceis de usar para a criação de soluções comerciais personalizadas com o Microsoft Office. É possível criar soluções cliente inteligentes e gerenciadas que usam aplicativos do Office como uma interface do usuário. As ferramentas permitem aos desenvolvedores criar soluções seguras que são fáceis de serem implantadas e mantidas.<br /><br /> Para obter mais informações, consulte [Como publicar uma solução do Office usando o ClickOnce](http://msdn.microsoft.com/en-us/2b6c247e-bc04-4ce4-bb64-c4e79bb3d5b8).|  
|**SQL Server 2005 Express Edition SP2 (x86)**|Esse pacote instala o Microsoft SQL Server 2005 Express Edition SP2, um aplicativo de banco de dados baseado no [!INCLUDE[sqprsqext](../../includes/sqprsqext-md.md)]. O SQL Server Express é uma substituição do MSDE (Microsoft SQL Server Desktop Engine). O SQL Server Express é gratuito e pode ser redistribuído (sujeito a contrato) e funciona como um banco de dados cliente e um banco de dados de servidor básico. É o mesmo que o SQL Server 2005, com exceção das seguintes diferenças:<br /><br /> -   Sem suporte a recursos corporativos.<br />-   Limitado a uma CPU.<br />-   Limite de memória de 1 GB (gigabyte) para o pool de buffers.<br />-   Tamanho máximo de 4 GB para bancos de dados.|  
|**SQL Server 2008 Express**|Esse pacote instala o Microsoft SQL Server 2008 Express, uma edição gratuita do Microsoft SQL Server 2008, um banco de dados ideal para aplicativos Web, de servidor ou de área de trabalho pequenos. Pode ser usado gratuitamente para desenvolvimento e produção. Um [registro](http://go.microsoft.com/fwlink/?LinkId=130380) gratuito é necessário para distribuir o SQL Server 2008 Express com o aplicativo.<br /><br /> O comportamento do bootstrapper é o seguinte:<br /><br /> -   Se o computador já tiver o SQL Server 2008 Express ou posterior, o computador permanecerá no SQL Server 2008 Express ou posterior.<br />-   Se o computador não tiver nenhuma versão do SQL Server 2008 Express ou posterior, o pacote instalará a última versão do SQL Server 2008 Express SP1.<br /><br /> Para saber mais sobre o SQL Server 2008 Express, visite [ http://go.microsoft.com/fwlink/?LinkId=183586 ](http://go.microsoft.com/fwlink/?LinkId=183586).|  
|**Bibliotecas em tempo de execução do Visual C++ 2010 (IA64)**|Esse pacote instala as bibliotecas em tempo de execução Visual C++ para a arquitetura Itanium, que fornecem rotinas de programação para o sistema operacional Microsoft Windows. Essas rotinas automatizam várias tarefas comuns de programação que não são fornecidas pelas linguagens C e C++.<br /><br /> Para obter mais informações, consulte [Referência da biblioteca em tempo de execução C](http://msdn.microsoft.com/library/a503e11c-8dca-4846-84fb-025a826c32b8).|  
|**Bibliotecas em tempo de execução Visual C++ 2010 (x64)**|Esse pacote instala as bibliotecas em tempo de execução Visual C++ para os sistemas operacionais x64, que fornecem rotinas de programação para o sistema operacional Microsoft Windows. Essas rotinas automatizam várias tarefas comuns de programação que não são fornecidas pelas linguagens C e C++.<br /><br /> Para obter mais informações, consulte [Referência da biblioteca em tempo de execução C](http://msdn.microsoft.com/library/a503e11c-8dca-4846-84fb-025a826c32b8).|  
|**Bibliotecas em tempo de execução Visual C++ 2010 (x86)**|Esse pacote instala as bibliotecas em tempo de execução Visual C++ para os sistemas operacionais x86, que fornecem rotinas de programação para o sistema operacional Microsoft Windows. Essas rotinas automatizam várias tarefas comuns de programação que não são fornecidas pelas linguagens C e C++.<br /><br /> Para obter mais informações, consulte [Referência da biblioteca em tempo de execução C](http://msdn.microsoft.com/library/a503e11c-8dca-4846-84fb-025a826c32b8).|  
|**Windows Installer 3.1**|Esse pacote instala o Microsoft Windows Installer redistribuível, versão 3.1, que permite a instalação de projetos de Instalação do Windows Installer. Ele é pré-instalado no Windows Server 2003 com SP1 e posterior.<br /><br /> Por padrão, esse item está selecionado.|  
|**Windows Installer 4.5**|Esse pacote instala o Microsoft Windows Installer redistribuível, versão 4.5, que permite a instalação de projetos de Instalação do Windows Installer.|  
  
## <a name="see-also"></a>Consulte também  
 [Página Publicar, Designer de Projeto](../../ide/reference/publish-page-project-designer.md)   
 [Pré-requisitos de implantação do aplicativo](../../deployment/application-deployment-prerequisites.md)   
 [Redistribuindo o .NET Framework](http://msdn.microsoft.com/en-us/a18d0456-fd89-493e-97f4-756505bfe287)   
 [Implantando pré-requisitos para aplicativos de 64 bits](../../deployment/deploying-prerequisites-for-64-bit-applications.md)   
 [Visão Geral do Visual Studio Multiplataforma](../../ide/visual-studio-multi-targeting-overview.md)




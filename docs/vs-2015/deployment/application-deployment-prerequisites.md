---
title: Pré-requisitos de implantação de aplicativo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, platform detection
- ClickOnce deployment, prerequisites
- ClickOnce deployment, dependencies
- prerequisites, ClickOnce
- dependencies, ClickOnce
ms.assetid: fc6e047e-ad94-44e8-8ff5-b6d1f4ca7735
caps.latest.revision: 53
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: e382c5d312a2de69281bdeda92e9c275e2877932
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49890980"
---
# <a name="application-deployment-prerequisites"></a>Pré-requisitos de implantação de aplicativos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para garantir que seu aplicativo será instalado e executará com êxito, você deve primeiro garantir que todos os componentes dos quais o aplicativo depende já estejam instalados no computador de destino. Por exemplo, a maioria dos aplicativos criados usando o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] tem uma dependência sobre o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]; a versão correta do tempo de execução de linguagem comum deve estar presente no computador de destino antes a instalação do aplicativo.  
  
 Você pode selecionar esses pré-requisitos a **caixa de diálogo de pré-requisitos** e instalar o .NET Framework e outros redistribuíveis como parte de sua instalação. Essa prática é conhecida como *inicialização*. Em seguida, [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] gera um programa executável do Windows chamado Setup.exe, também conhecido como um *bootstrapper*. O bootstrapper é responsável pela instalação desses pré-requisitos antes de executar o aplicativo. Para obter mais informações sobre como selecionar esses pré-requisitos, consulte [caixa de diálogo de pré-requisitos](../ide/reference/prerequisites-dialog-box.md).  
  
 Cada pré-requisito é um pacote de bootstrapper. Um pacote de bootstrapper é um grupo de diretórios e arquivos que contém arquivos de manifesto que descrevem como o pré-requisito deve ser instalado. Se os pré-requisitos do aplicativo não estão listados na **caixa de diálogo pré-requisito**, você pode criar pacotes de bootstrapper personalizados e adicioná-los para o Visual Studio. Em seguida, você pode selecionar os pré-requisitos a **caixa de diálogo de pré-requisitos**. Para obter mais informações, consulte [criação de pacotes de Bootstrapper](../deployment/creating-bootstrapper-packages.md).  
  
 Por padrão, a inicialização está habilitada para implantação do ClickOnce. O bootstrapper gerado para implantação do ClickOnce é assinado. Você pode desabilitar a inicialização de um componente, mas deve fazer isso somente se tiver certeza de que a versão correta do componente já esteja instalada em todos os computadores de destino.  
  
## <a name="bootstrapping-and-clickonce-deployment"></a>Inicialização e implantação do ClickOnce  
 Antes de instalar um aplicativo em um computador cliente, o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] examinará o cliente para garantir que ele tenha determinados requisitos especificados no manifesto do aplicativo. Eles incluem o seguinte:  
  
- A versão mínima necessária do tempo de execução da linguagem comum, que está especificada como uma dependência do assembly no manifesto do aplicativo.  
  
- A versão mínima necessária do sistema operacional Windows exigida pelo aplicativo, conforme especificado no manifesto do aplicativo usando o elemento `<osVersionInfo>`. (Consulte [ \<dependência > elemento](../deployment/dependency-element-clickonce-application.md))  
  
- A versão mínima de todos os assemblies que devem ser pré-instalados no cache do assembly global (GAC), conforme especificado pelas declarações de dependência do assembly no manifesto do assembly.  
  
  [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] pode detectar pré-requisitos ausentes, e você pode instalar os pré-requisitos usando um bootstrapper. Para obter mais informações, consulte [como: instalar pré-requisitos com um aplicativo ClickOnce](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md).  
  
> [!NOTE]
>  Para alterar os valores nos manifestos gerados pelas ferramentas, tais como [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e MageUI.exe, você precisa editar o manifesto do aplicativo em um editor de texto e assinar novamente os manifestos do aplicativo e de implantação. Para obter mais informações, consulte [como: assinar novamente os manifestos de aplicativo e implantação](../deployment/how-to-re-sign-application-and-deployment-manifests.md).  
  
 Se você usar o Visual Studio e o ClickOnce para implantar seu aplicativo, os pacotes do bootstrapper selecionados por padrão dependerão da versão do .NET Framework na solução. No entanto, se você alterar a versão do .NET Framework de destino, você deve atualizar as opções de **caixa de diálogo de pré-requisitos** manualmente.  
  
|.NET Framework de Destino|Pacotes do Bootstrapper Selecionados|  
|---------------------------|------------------------------------|  
|.NET Framework 4 Client Profile|.NET Framework 4 Client Profile<br /><br /> Windows Installer 3.1|  
|.NET Framework 4|.NET Framework 4<br /><br /> Windows Installer 3.1|  
  
 Com a implantação do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)], a página Publish.htm gerada pelo Assistente de Publicação do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aponta para um link que instala somente o aplicativo ou para um link que instala o aplicativo e os componentes inicializados.  
  
 Se você gerar o bootstrapper usando o Assistente de Publicação do ClickOnce ou a Página de Publicação no Visual Studio, o Setup.exe será assinado automaticamente. No entanto, se desejar usar o certificado do cliente para assinar o bootstrapper, você poderá assinar o arquivo mais tarde.  
  
## <a name="bootstrapping-and-msbuild"></a>Inicialização e MSBuild  
 Se você não usar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], mas compilar seus aplicativos na linha de comando, poderá criar o aplicativo de inicialização do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] usando uma tarefa do Microsoft Build Engine (MSBuild). Para obter mais informações, consulte [tarefa GenerateBootstrapper](../msbuild/generatebootstrapper-task.md).  
  
 Como alternativa para a inicialização, você pode pré-implantar componentes usando um sistema de distribuição de software eletrônico, tal como o Microsoft Systems Management Server (SMS).  
  
## <a name="bootstrapper-setupexe-command-line-arguments"></a>Argumentos da linha de comando do bootstrapper (Setup.exe)  
 O Setup.exe gerado por [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e as tarefas do MSBuild oferecem suporte ao pequeno conjunto de argumentos da linha de comando a seguir. Quaisquer argumentos fornecidos ao aplicativo de inicialização além desses são encaminhados ao instalador do aplicativo.  
  
 Se você alterar quaisquer opções do bootstrapper, deverá alterar o bootstrapper não assinado e assinar o arquivo de bootstrapper posteriormente.  
  
|Argumento da linha de comando|Descrição|  
|---------------------------|-----------------|  
|**-?, -h, - ajuda**|Exibe uma caixa de diálogo de Ajuda.|  
|**-url, - componentsurl**|Mostra a URL armazenada e a URL dos componentes para esta configuração.|  
|**-url =** `location`|Configura a URL em que Setup.exe consultará o aplicativo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)].|  
|**-componentsurl =** `location`|Configura a URL em que Setup.exe consultará as dependências, tais como o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].|  
|**-homesite =** `true`**&#124;** `false`|Quando `true`, baixa as dependências do local preferido no site do fornecedor. Isso substitui o **- componentsurl** configuração. Quando `false`, baixe as dependências da URL especificada por **- componentsurl**.|  
  
## <a name="operating-system-support"></a>Suporte a sistemas operacionais  
 O bootstrapper do Visual Studio não é compatível com o Windows Server 2008 Server Core ou o Windows Server 2008 R2 Server Core, que fornece um ambiente de servidor de baixa manutenção com funcionalidade limitada. Por exemplo, a opção de instalação do Server Core oferece suporte somente ao perfil do .NET Framework 3.5 Server Core, de modo que os recursos do Visual Studio que dependem do .NET Framework completo não poderão ser executados.  
  
## <a name="see-also"></a>Consulte também  
 [Escolhendo uma estratégia de implantação do ClickOnce](../deployment/choosing-a-clickonce-deployment-strategy.md)   
 [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)




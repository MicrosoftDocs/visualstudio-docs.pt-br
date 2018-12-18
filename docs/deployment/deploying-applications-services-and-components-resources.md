---
title: Visão geral da implantação – Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2018
ms.technology: vs-ide-deployment
ms.topic: overview
dev_langs:
- FSharp
- VB
- CSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1d5b15af932f8d796a27dfc060128617816b9234
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39232167"
---
# <a name="overview-of-deployment-in-visual-studio"></a>Visão geral da implantação no Visual Studio

Ao implantar um aplicativo, serviço ou componente, você o distribui para instalação em outros computadores, dispositivos, servidores ou na nuvem. Você escolhe o método apropriado no Visual Studio para o tipo de implantação que deseja.

Para muitos tipos comuns de aplicativo, é possível implantar seu aplicativo diretamente do Gerenciador de Soluções no Visual Studio. Para fazer um tour rápido sobre essa funcionalidade, confira [First look at deployment](../deployment/deploying-applications-services-and-components.md) (Introdução à implantação).

![Escolher uma opção de publicação](../deployment/media/quickstart-publish-azure.png)

## <a name="what-publishing-options-are-right-for-me"></a>Quais opções de publicação são adequadas para mim?

De dentro do Visual Studio, os aplicativos podem ser publicados diretamente nos seguintes destinos:

- [Serviço de Aplicativo do Azure](#azure-app-service)
- [Máquinas Virtuais do Azure](#azure-virtual-machines)
- [Sistema de arquivos](#file-system)
- [Destinos personalizados (IIS, FTP, etc.) ](#custom-targets), que inclui todos os servidores Web arbitrários.

Na guia **Publicar** é possível selecionar um perfil de publicação existente, importar um perfil existente ou criar um novo perfil usando as opções descritas aqui. Para fazer um tour pelas opções de publicação no IDE para diferentes tipos de aplicativos, confira [Introdução à implantação](../deployment/deploying-applications-services-and-components.md).

## <a name="azure-app-service"></a>Serviço de Aplicativo do Azure

O [Serviço de Aplicativo do Azure](/azure/app-service/app-service-web-overview) e o [Serviço de Aplicativo no Linux](/azure/app-service/containers/app-service-linux-intro) ajudam os desenvolvedores a criar rapidamente uma variedade de serviços e aplicativos Web escalonáveis sem infraestrutura de manutenção.

Você determina a capacidade de computação que um Serviço de Aplicativo tem escolhendo um [plano ou tipo de preço](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) para o Serviço de Aplicativo recipiente. É possível ter vários aplicativos Web (e outros tipos de aplicativos) compartilhando o mesmo Serviço de Aplicativo sem alterar o tipo de preço. Por exemplo, é possível hospedar o desenvolvimento, o preparo e a produção de aplicativos Web juntos no mesmo Serviço de Aplicativo.

Um Serviço de Aplicativo é executado em máquinas virtuais hospedadas na nuvem no Azure, mas essas máquinas virtuais são gerenciadas para você. Cada aplicativo em um Serviço de Aplicativo receberá uma URL \*.azurewebsites.net exclusiva; todos os tipos de preço diferentes de Gratuito também permitem a atribuição de nomes de domínio personalizados ao site.

### <a name="when-to-choose-azure-app-service"></a>Quando escolher o Serviço de Aplicativo do Azure

- Você deseja implantar um aplicativo Web que é acessível pela Internet.
- Você deseja escalonar automaticamente seu aplicativo Web de acordo com a demanda sem a necessidade de reimplantar.
- Você não deseja manter uma infraestrutura de servidor (incluindo atualizações de software).
- Você não precisa de nenhuma personalização de nível de computador nos servidores que hospedam seu aplicativo Web.

> Se quiser usar o Serviço de Aplicativo do Azure em seu próprio datacenter ou em outros computadores locais, você poderá fazer isso usando o [Azure Stack](https://azure.microsoft.com/overview/azure-stack/).

Para saber mais sobre como publicar no Serviço de Aplicativo, confira [Início Rápido – Publicar no Serviço de Aplicativo do Azure](quickstart-deploy-to-azure.md) e [Início Rápido – Publicar ASP.NET Core no Linux](quickstart-deploy-to-linux.md).

## <a name="azure-virtual-machines"></a>Máquinas Virtuais do Azure

As [Máquinas Virtuais (VMs) do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) permitem criar e gerenciar qualquer número de recursos de computação na nuvem. Ao assumir a responsabilidade por todos os softwares e atualizações nas VMs, é possível personalizá-los tanto quanto desejar conforme exigido pelo seu aplicativo. Você pode acessar as máquinas virtuais diretamente por meio da Área de Trabalho Remota e cada uma delas manterá seu endereço IP atribuído por quanto tempo for desejado.

O dimensionamento de um aplicativo hospedado em máquinas virtuais envolve a criação VMs adicionais de acordo com a demanda e, em seguida, a implantação do software necessário. Esse nível adicional de controle permite você escalonar de maneira diferente em diferentes regiões globais. Por exemplo, se seu aplicativo estiver atendendo a funcionários em uma diversos escritórios regionais, será possível escalonar suas VMs de acordo com o número de funcionários nessas regiões, potencialmente reduzindo os custos.

Para obter informações adicionais, consulte a [comparação detalhada](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) entre o Serviço de Aplicativo do Azure, as Máquinas Virtuais do Azure e outros serviços do Azure que podem ser usados como destinos de implantação, usando a opção Personalizar no Visual Studio.

### <a name="when-to-choose-azure-app-virtual-machines"></a>Quando escolher Máquinas Virtuais de Aplicativo do Azure

- Você deseja implantar um aplicativo Web que é acessível pela Internet, com controle total sobre o tempo de vida dos endereços IP atribuídos.
- Você precisa de personalizações em nível de computador em seus servidores que incluem: software adicional, como um sistema de banco de dados especializado, configurações de rede específicas, partições de disco e assim por diante.
- Você deseja um nível de controle refinado sobre o escalonamento de seu aplicativo Web.
- Você precisa ter acesso direto aos servidores que hospedam seu aplicativo por qualquer outro motivo.

> Se quiser usar as Máquinas Virtuais do Azure em seu próprio datacenter ou em outros computadores locais, você poderá fazer isso usando o [Azure Stack](https://azure.microsoft.com/overview/azure-stack/).

## <a name="file-system"></a>Sistema de arquivos

A implantação no sistema de arquivos significa simplesmente copiar os arquivos do seu aplicativo para uma pasta específica em seu próprio computador. Isso geralmente é usado para fins de teste ou para implantar o aplicativo para uso por um número limitado de pessoas, caso o computador também esteja executando um servidor. Se a pasta de destino for compartilhada em uma rede, a implantação no sistema de arquivos poderá disponibilizar os arquivos do aplicativo Web para outras pessoas que poderão, por sua vez, implantá-la em servidores específicos.

Todas os computadores locais que estão executando um servidor podem disponibilizar seu aplicativo através da Internet ou de uma Intranet, dependendo de como estiver configurado e das redes às quais estiver conectado. (Se você conectar um computador diretamente à Internet, seja muito cuidado protegendo-o contra ameaças externas.) Como você gerencia esses computadores, você está no controle total das configurações de hardware e software.

Observe que se, por algum motivo (como acesso ao computador), não for possível usar os serviços de nuvem como o Serviço de Aplicativo do Azure ou as Máquinas Virtuais do Azure, você poderá usar o [Azure Stack](https://azure.microsoft.com/overview/azure-stack/) em seu próprio datacenter. O Azure Stack permite gerenciar e usar recursos de computação por meio do Serviço de Aplicativo do Azure e das Máquinas Virtuais do Azure e ainda manter tudo localmente.

### <a name="when-to-choose-file-system-deployment"></a>Quando escolher a implantação de sistema de arquivos

- Você só precisa implantar o aplicativo em um compartilhamento de arquivos do qual outras pessoas vão implantá-lo em servidores diferentes.
- Você precisa apenas de uma implantação de teste local.
- Você deseja examinar e potencialmente modificar os arquivos do aplicativo independentemente, antes de enviá-los a outro destino de implantação.

Para saber mais, confira [Início Rápido – Implantar em uma pasta local](quickstart-deploy-to-local-folder.md)

## <a name="custom-targets-iis-ftp"></a>Destinos personalizados (IIS, FTP)

Um destino personalizado permite que você implante seu aplicativo em um destino diferente do Serviço de Aplicativo do Azure, das Máquinas Virtuais do Azure ou do sistema de arquivos local. Ele pode ser implantado em um sistema de arquivos ou qualquer outro servidor (Internet ou Intranet) ao qual você tem acesso, inclusive aqueles em outros serviços de nuvem. Ele pode funcionar com a Implantação da Web (arquivos ou .ZIP) e FTP.

Ao escolher um destino personalizado, o Visual Studio solicitará um nome de perfil e, em seguida, coletará informações de **Conexão** adicionais, incluindo o servidor de destino ou o local, um nome de site e as credenciais. É possível controlar os seguintes comportamentos na guia **Configurações**:

- A configuração que você deseja implantar.
- Se os arquivos existentes serão removidos do destino.
- Se a pré-compilação será feita durante a publicação.
- Se os arquivos serão excluídos da pasta App_Data da implantação.

É possível criar vários perfis de implantação Personalizados no Visual Studio, possibilitando o gerenciamento dos perfis com configurações diferentes.

### <a name="when-to-choose-custom-deployment"></a>Quando escolher a implantação personalizada

- Você está usando serviços de nuvem em um provedor diferente do Azure que pode ser acessado por meio de URLs.
- Você deseja implantar usando credenciais diferentes das que você usa no Visual Studio ou daquelas diretamente ligadas às suas contas do Azure.
- Você deseja excluir os arquivos do destino a cada vez que implantar.

Para saber mais, confira [Início Rápido – Implantar em um site](quickstart-deploy-to-a-web-site.md)

## <a name="next-steps"></a>Próximas etapas

Tutoriais:

- [Implantar um aplicativo .NET Core com a ferramenta de publicação](/dotnet/core/deploying/deploy-with-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Publicar um aplicativo ASP.NET Core no Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Implantação no Visual C++](/cpp/ide/deployment-in-visual-cpp)
- [Implantar aplicativos UWP](/windows/uwp/packaging/packaging-uwp-apps?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Publicar um aplicativo Node.js no Azure usando a Implantação da Web](https://github.com/Microsoft/nodejstools/wiki/Publish-to-Azure-Website-using-Web-Deploy?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Publicar um aplicativo Python no Serviço de Aplicativo do Azure](/visualstudio/python/publishing-python-web-applications-to-azure-from-visual-studio?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)

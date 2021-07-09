---
title: Implantar seu Visual Studio aplicativo em uma pasta, IIS, Azure ou outro destino
titleSuffix: ''
description: Saiba mais sobre as opções de publicação para seu aplicativo usando a ferramenta Publicar.
ms.custom:
- SEO-VS-2020
- contperf-fy21q1
ms.date: 08/21/2020
ms.topic: troubleshooting
f1_keywords:
- vs.publish
dev_langs:
- FSharp
- VB
- CSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 099bd2c6cc47895c913b3f852835d2fd09d0f9c3
ms.sourcegitcommit: 4e09130bcd55bb9cb8ad157507c23b67aa209fad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2021
ms.locfileid: "113549479"
---
# <a name="deploy-your-app-to-a-folder-iis-azure-or-another-destination"></a>Implantar seu aplicativo em uma pasta, IIS, Azure ou outro destino

Ao implantar um aplicativo, serviço ou componente, você o distribui para instalação em outros computadores, dispositivos, servidores ou na nuvem. Você escolhe o método apropriado no Visual Studio para o tipo de implantação que deseja.

Obter ajuda para sua tarefa de implantação:

- Não tem certeza de qual opção de implantação escolher? Confira [Quais opções de publicação são certas para mim?](#what-publishing-options-are-right-for-me)
- Para ajudar com problemas de implantação para Serviço de Aplicativo do Azure ou IIS, consulte [Solucionar problemas ASP.NET Core no Serviço de Aplicativo do Azure e no IIS.](/aspnet/core/test/troubleshoot-azure-iis)
- Para saber mais sobre como definir as configurações de implantação do .NET, confira [Definir configurações de implantação do .NET.](#configure-net-deployment-settings)
- Para implantar em um novo destino, se você  já tiver  criado um perfil de publicação, selecione Novo na janela Publicar para um perfil configurado.

   ![Criar um novo perfil de publicação](../deployment/media/create-a-new-publish-profile.png)

   Em seguida, escolha uma opção de implantação na janela Publicar. Para obter informações sobre suas opções de publicação, consulte as seções a seguir.

## <a name="what-publishing-options-are-right-for-me"></a>Quais opções de publicação são adequadas para mim?

De dentro do Visual Studio, os aplicativos podem ser publicados diretamente nos seguintes destinos:

::: moniker range=">=vs-2019"
- [Azure](#azure)
- [Registro de Contêiner do Docker](#docker-container-registry)
- [Pasta](#folder)
- [Servidor FTP/FTPS](#ftpftps-server)
- [Servidor Web (IIS)](#web-server-iis)
- [Importar perfil](#import-profile)
::: moniker-end
::: moniker range="vs-2017"
- [Serviço de Aplicativo](#azure-app-service)
- [Serviço de Aplicativo Linux](#azure-app-service)
- [IIS (escolha IIS, FTP etc.)](#web-server-iis)
- [FTP/FTPS (escolha IIS, FTP etc.)](#ftpftps-server)
- [Pasta](#folder)
- [Importar perfil](#import-profile)
::: moniker-end

As opções anteriores aparecem conforme mostrado na ilustração a seguir quando você cria um novo perfil de publicação.

::: moniker range=">=vs-2019"
![Selecione uma opção de publicação](../deployment/media/quickstart-publish-dialog.png)
::: moniker-end
::: moniker range="vs-2017"
![Selecione uma opção de publicação](../deployment/media/quickstart-publish-dialog-vs-2017.png)
::: moniker-end

Para obter um tour rápido das opções mais gerais de implantação de aplicativos, confira [Primeira pesquisa sobre a implantação.](../deployment/deploying-applications-services-and-components.md)

## <a name="azure"></a>Azure 

Ao escolher o Azure, você pode escolher entre:

- [Serviço de Aplicativo do Azure](#azure-app-service) em execução Windows, Linux ou como uma imagem do Docker
- Uma imagem do Docker implantada [no Registro de Contêiner do Azure](#azure-container-registry)
- Uma [máquina virtual do Azure](#azure-virtual-machine)

![Escolher um serviço do Azure](../deployment/media/quickstart-choose-azure-service.png)

### <a name="azure-app-service"></a>Serviço de aplicativo do Azure

[Serviço de Aplicativo do Azure](/azure/app-service/app-service-web-overview) ajuda os desenvolvedores a criar rapidamente aplicativos Web e serviços escalonáveis sem manter a infraestrutura. Um Serviço de Aplicativo é executado em máquinas virtuais hospedadas na nuvem no Azure, mas essas máquinas virtuais são gerenciadas para você. Cada aplicativo em um Serviço de Aplicativo receberá uma URL \*.azurewebsites.net exclusiva; todos os tipos de preço diferentes de Gratuito também permitem a atribuição de nomes de domínio personalizados ao site.

Você determina a capacidade de computação que um Serviço de Aplicativo tem escolhendo um [plano ou tipo de preço](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) para o Serviço de Aplicativo recipiente. É possível ter vários aplicativos Web (e outros tipos de aplicativos) compartilhando o mesmo Serviço de Aplicativo sem alterar o tipo de preço. Por exemplo, é possível hospedar o desenvolvimento, o preparo e a produção de aplicativos Web juntos no mesmo Serviço de Aplicativo.

#### <a name="when-to-choose-azure-app-service"></a>Quando escolher o Serviço de Aplicativo do Azure

- Você deseja implantar um aplicativo Web que é acessível pela Internet.
- Você deseja escalonar automaticamente seu aplicativo Web de acordo com a demanda sem a necessidade de reimplantar.
- Você não deseja manter uma infraestrutura de servidor (incluindo atualizações de software).
- Você não precisa de nenhuma personalização de nível de computador nos servidores que hospedam seu aplicativo Web.

> Se quiser usar o Serviço de Aplicativo do Azure em seu próprio datacenter ou em outros computadores locais, você poderá fazer isso usando o [Azure Stack](https://azure.microsoft.com/overview/azure-stack/).

Para obter mais informações sobre como publicar no Serviço de Aplicativo, confira:
- [Início Rápido – Publicar no Serviço de Aplicativo do Azure](quickstart-deploy-to-azure.md)
- [Início Rápido – Publicar ASP.NET Core no Linux.](quickstart-deploy-to-linux.md)
- [Publicar um ASP.NET Core para Serviço de Aplicativo do Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)
- [Solucionar ASP.NET Core no Serviço de Aplicativo do Azure e no IIS.](/aspnet/core/test/troubleshoot-azure-iis)

### <a name="azure-container-registry"></a>Registro de Contêiner do Azure

[Registro de Contêiner do Azure](/azure/container-registry/) permite que você crie, armazene e gerencie artefatos e imagens de contêiner do Docker em um registro privado para todos os tipos de implantações de contêiner.

#### <a name="when-to-choose-azure-container-registry"></a>Quando escolher Registro de Contêiner do Azure

- Quando você tem um pipeline de desenvolvimento e implantação de contêineres do Docker existente.
- Quando você deseja criar imagens de contêiner do Docker no Azure.

Para mais informações:

- [Implantar um ASP.NET contêiner em um registro de contêiner](../containers/hosting-web-apps-in-docker.md)

### <a name="azure-virtual-machine"></a>Máquina Virtual do Azure

[As VMs (Máquinas Virtuais) do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) permitem que você crie e gerencie qualquer número de recursos de computação na nuvem. Ao assumir a responsabilidade por todos os softwares e atualizações nas VMs, é possível personalizá-los tanto quanto desejar conforme exigido pelo seu aplicativo. Você pode acessar as máquinas virtuais diretamente por meio da Área de Trabalho Remota e cada uma delas manterá seu endereço IP atribuído por quanto tempo for desejado.

O dimensionamento de um aplicativo hospedado em máquinas virtuais envolve a criação VMs adicionais de acordo com a demanda e, em seguida, a implantação do software necessário. Esse nível adicional de controle permite você escalonar de maneira diferente em diferentes regiões globais. Por exemplo, se seu aplicativo estiver atendendo a funcionários em uma diversos escritórios regionais, será possível escalonar suas VMs de acordo com o número de funcionários nessas regiões, potencialmente reduzindo os custos.

Para obter informações [](/azure/architecture/guide/technology-choices/compute-decision-tree) adicionais, consulte a comparação detalhada entre Serviço de Aplicativo do Azure, Máquinas Virtuais do Azure e outros serviços do Azure que você pode usar como um destino de implantação usando a opção Personalizado no Visual Studio.

#### <a name="when-to-choose-azure-virtual-machines"></a>Quando escolher máquinas virtuais do Azure

- Você deseja implantar um aplicativo Web que é acessível pela Internet, com controle total sobre o tempo de vida dos endereços IP atribuídos.
- Você precisa de personalizações no nível do computador em seus servidores, que incluem software adicional, como um sistema de banco de dados especializado, configurações de rede específicas, partições de disco e assim por diante.
- Você deseja um nível de controle refinado sobre o escalonamento de seu aplicativo Web.
- Você precisa ter acesso direto aos servidores que hospedam seu aplicativo por qualquer outro motivo.

> Se quiser usar as Máquinas Virtuais do Azure em seu próprio datacenter ou em outros computadores locais, você poderá fazer isso usando o [Azure Stack](https://azure.microsoft.com/overview/azure-stack/).

## <a name="docker-container-registry"></a>Registro de contêiner do Docker

Se seu aplicativo estiver usando o Docker, você poderá publicar seu aplicativo em contêineres em um registro de contêiner do Docker.

### <a name="when-to-choose-docker-container-registry"></a>Quando escolher o Registro de Contêiner do Docker

- Você deseja implantar um aplicativo em contêineres

Para saber mais, consulte o seguinte:

- [Implantar um ASP.NET contêiner em um registro de contêiner](../containers/hosting-web-apps-in-docker.md)
- [Implantar no Docker Hub](../containers/deploy-docker-hub.md)

## <a name="folder"></a>Pasta

Implantar no sistema de arquivos significa copiar os arquivos do aplicativo para uma pasta específica em seu próprio computador. A implantação em uma pasta geralmente é usada para fins de teste ou para implantar o aplicativo para uso por um número limitado de pessoas se o computador também estiver executando um servidor. Se a pasta de destino for compartilhada em uma rede, a implantação no sistema de arquivos poderá disponibilizar os arquivos do aplicativo Web para outras pessoas que poderão, por sua vez, implantá-la em servidores específicos.
::: moniker range=">=vs-2019"
A partir do Visual Studio 2019 16.8, o destino da pasta inclui a capacidade de publicar um aplicativo .Net Windows usando ClickOnce.

Se você quiser publicar um aplicativo .NET Core 3.1 ou mais novo com Windows com ClickOnce, consulte Implantar um aplicativo [.NET Windows](quickstart-deploy-using-clickonce-folder.md)usando ClickOnce .
::: moniker-end
Todas os computadores locais que estão executando um servidor podem disponibilizar seu aplicativo através da Internet ou de uma Intranet, dependendo de como estiver configurado e das redes às quais estiver conectado. (Se você conectar um computador diretamente à Internet, tenha especialmente cuidado para protegê-lo contra ameaças de segurança externas.) Como você gerencia esses máquinas, tem controle total das configurações de software e hardware.

Se, por qualquer motivo (como acesso ao computador), você não conseguir usar serviços de nuvem como Serviço de Aplicativo do Azure ou Máquinas Virtuais do Azure, poderá usar o [Azure Stack](https://azure.microsoft.com/overview/azure-stack/) em seu próprio datacenter. O Azure Stack permite gerenciar e usar recursos de computação por meio do Serviço de Aplicativo do Azure e das Máquinas Virtuais do Azure e ainda manter tudo localmente.

### <a name="when-to-choose-file-system-deployment"></a>Quando escolher a implantação de sistema de arquivos

- Você só precisa implantar o aplicativo em um compartilhamento de arquivos do qual outras pessoas vão implantá-lo em servidores diferentes.
::: moniker range=">=vs-2019"
- Você deseja implantar um aplicativo .NET Windows usando ClickOnce
::: moniker-end
- Você precisa apenas de uma implantação de teste local.
- Você deseja examinar e potencialmente modificar os arquivos do aplicativo independentemente, antes de enviá-los a outro destino de implantação.

Para obter mais informações, consulte [Início Rápido – Implantar em uma pasta local.](quickstart-deploy-to-local-folder.md)
::: moniker range=">=vs-2019"
Para obter mais informações sobre como implantar um aplicativo .NET Windows usando ClickOnce, consulte Implantar um [aplicativo .NET Windows usando](quickstart-deploy-using-clickonce-folder.md)ClickOnce .
::: moniker-end

Para obter ajuda adicional para escolher suas configurações, confira o seguinte:

- [Implantação dependente de estrutura versus autossuporte](/dotnet/core/deploying/)
- [Identificadores de runtime de destino (RID portátil, et al)](/dotnet/core/rid-catalog)
- [Configurações de depuração e versão](../ide/understanding-build-configurations.md)

## <a name="ftpftps-server"></a>Servidor FTP/FTPS

Um servidor FTP/FTPS permite implantar seu aplicativo em um servidor diferente do Azure. Ele pode ser implantado em um sistema de arquivos ou qualquer outro servidor (Internet ou Intranet) ao qual você tem acesso, inclusive aqueles em outros serviços de nuvem. Ele pode funcionar com a Implantação da Web (arquivos ou .ZIP) e FTP.

Ao escolher um servidor FTP/FTPS, Visual Studio solicita um nome de perfil  e, em seguida, coleta informações de conexão adicionais, incluindo o servidor de destino ou o local, um nome do site e credenciais. É possível controlar os seguintes comportamentos na guia **Configurações**:

- A configuração que você deseja implantar.
- Se os arquivos existentes serão removidos do destino.
- Se a pré-compilação será feita durante a publicação.
- Se os arquivos serão excluídos da pasta App_Data da implantação.

Você pode criar qualquer número de perfis de implantação FTP/FTPS no Visual Studio, possibilitando gerenciar perfis com configurações diferentes.

### <a name="when-to-choose-ftpftps-server-deployment"></a>Quando escolher a implantação do servidor FTP/FTPS

- Você está usando serviços de nuvem em um provedor diferente do Azure que pode ser acessado por meio de URLs.
- Você deseja implantar usando credenciais diferentes das que você usa no Visual Studio ou daquelas diretamente ligadas às suas contas do Azure.
- Você deseja excluir os arquivos do destino a cada vez que implantar.

## <a name="web-server-iis"></a>Servidor Web (IIS)

Um servidor Web do IIS permite implantar seu aplicativo em um servidor Web diferente do Azure. Ele pode ser implantado em um servidor IIS (Internet ou Intranet) ao qual você tem acesso, incluindo aqueles em outros serviços de nuvem. Ele pode funcionar com Implantação da Web ou um Implantação da Web pacote.

Ao escolher um servidor Web do IIS, Visual Studio solicita um nome de  perfil e, em seguida, coleta informações de conexão adicionais, incluindo o servidor ou o local de destino, um nome do site e credenciais. É possível controlar os seguintes comportamentos na guia **Configurações**:

- A configuração que você deseja implantar.
- Se os arquivos existentes serão removidos do destino.
- Se a pré-compilação será feita durante a publicação.
- Se os arquivos serão excluídos da pasta App_Data da implantação.

Você pode criar qualquer número de perfis de implantação de servidor Web do IIS Visual Studio, possibilitando o gerenciamento de perfis com configurações diferentes.

### <a name="when-to-choose-web-server-iis-deployment"></a>Quando escolher a implantação do servidor Web (IIS)

- Você está usando o IIS para publicar um site ou serviço que pode ser acessado por meio de URLs.
- Você deseja implantar usando credenciais diferentes das que você usa no Visual Studio ou daquelas diretamente ligadas às suas contas do Azure.
- Você deseja excluir os arquivos do destino a cada vez que implantar.

Para obter mais informações, consulte [Início Rápido – Implantar em um site da Web.](quickstart-deploy-to-a-web-site.md)

Para ajudar com a solução de ASP.NET Core no IIS, consulte [Solucionar problemas ASP.NET Core no Serviço de Aplicativo do Azure e no IIS.](/aspnet/core/test/troubleshoot-azure-iis)

## <a name="import-profile"></a>Importar Perfil

Você pode importar um perfil ao publicar no IIS ou Serviço de Aplicativo do Azure. Você pode configurar a implantação usando *um arquivo de configurações de publicação* (*\* .publishsettings*). Um arquivo de configurações de publicação é criado pelo IIS ou pelo Serviço de Aplicativo do Azure ou pode ser criado manualmente e, em seguida, pode ser importado para o Visual Studio.

O uso de um arquivo de configurações de publicação pode simplificar a configuração de implantação e funciona melhor em um ambiente de equipe em vez de configurar manualmente cada perfil de implantação.

### <a name="when-to-choose-import-profile"></a>Quando escolher o perfil de importação

- Você está publicando no IIS e deseja simplificar a configuração da implantação.
- Você está publicando no IIS ou Serviço de Aplicativo do Azure e deseja acelerar a configuração de implantação para reutilização ou para a publicação de membros da equipe no mesmo serviço.

Para saber mais, consulte o seguinte:

- [Importar configurações de publicação e implantar no IIS](tutorial-import-publish-settings-iis.md)
- [Importar configurações de publicação e implantar no Azure](tutorial-import-publish-settings-azure.md)

## <a name="configure-net-deployment-settings"></a>Definir configurações de implantação do .NET

Para obter ajuda adicional para escolher suas configurações, confira o seguinte:

- [Implantação dependente de estrutura versus autossuporte](/dotnet/core/deploying/)
- [Identificadores de runtime de destino (RID portátil, et al)](/dotnet/core/rid-catalog)
- [Configurações de depuração e versão](../ide/understanding-build-configurations.md)

## <a name="next-steps"></a>Próximas etapas

Tutoriais:

- [Implantar um aplicativo .NET Core com a ferramenta de publicação](/dotnet/core/deploying/deploy-with-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Publicar um ASP.NET principal no Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Implantação no Visual C++](/cpp/windows/deployment-in-visual-cpp)
- [Implantar aplicativos UWP](/windows/uwp/packaging/packaging-uwp-apps?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Publicar um aplicativo Node.js no Azure usando a Implantação da Web](https://github.com/Microsoft/nodejstools/wiki/Publish-to-Azure-Website-using-Web-Deploy?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Publicar um aplicativo do Python no Serviço de Aplicativo do Azure](../python/publishing-python-web-applications-to-azure-from-visual-studio.md?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)

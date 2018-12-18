---
title: Instalar Ferramentas de Build do Visual Studio em um contêiner
titleSuffix: ''
description: Saiba como instalar as Ferramentas de Build do Visual Studio em um contêiner do Windows para oferecer suporte a fluxos de trabalho de CI e CD (integração contínua e entrega contínua).
ms.date: 04/18/2018
ms.technology: vs-acquisition
ms.custom: seodec18
ms.prod: visual-studio-dev15
ms.topic: conceptual
ms.assetid: d5c038e2-e70d-411e-950c-8a54917b578a
author: heaths
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 37ce2fc60ac2a57baddf62e68a900349ed072f4d
ms.sourcegitcommit: 0cdd8e8a53fb4fd5e869f07c35204419fa12783d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160082"
---
# <a name="install-build-tools-into-a-container"></a>Instalar Ferramentas de Build em um contêiner

É possível instalar as Ferramentas de Build do Visual Studio em um contêiner do Windows para oferecer suporte a fluxos de trabalho de CI e CD (integração contínua e entrega contínua). Este artigo orienta sobre quais alterações de configuração do Docker são necessárias, bem como quais [cargas de trabalho e componentes](workload-component-id-vs-build-tools.md) podem ser instalados em um contêiner.

Os [contêineres](https://www.docker.com/what-container) são uma ótima maneira de empacotar um sistema de build consistente e podem ser usados não somente em um ambiente de servidor CI/CD, mas também em ambientes de desenvolvimento. Por exemplo, é possível pode montar o código-fonte em um contêiner a ser criado por um ambiente personalizado e, ao mesmo tempo, continuar a usar o Visual Studio ou outras ferramentas para escrever o código. Caso o fluxo de trabalho CI/CD use a mesma imagem de contêiner, fique tranquilo, o código será compilado de forma consistente. Também é possível usar os contêineres para obter consistência em tempo de execução, o que é comum em microsserviços que usam vários contêineres com um sistema de orquestração, mas está fora do escopo deste artigo.

Se as Ferramentas de Build do Visual Studio não têm o que você precisa para compilar o código-fonte, estas etapas podem ser usadas em outros produtos do Visual Studio. Vale ressaltar, no entanto, que os contêineres do Windows não têm suporte para uma interface do usuário interativo, então, todos os comandos devem ser automatizados.

## <a name="overview"></a>Visão geral

Por meio do [Docker](https://www.docker.com/what-docker), é possível criar uma imagem da qual pode-se criar contêineres que compilam o código-fonte. O Dockerfile de exemplo instala as Ferramentas de Build do Visual Studio 2017 mais recentes e outros programas úteis, geralmente utilizados para compilar código-fonte. É possível modificar ainda mais o Dockerfile para incluir outras ferramentas e scripts para executar testes, publicar saída de build e muito mais.

Se o Docker para Windows já estiver instalado, pule para a etapa 3.

## <a name="step-1-enable-hyper-v"></a>Etapa 1. Habilitar o Hyper-V

O Hyper-V não está habilitado por padrão. Ele deve ser habilitado para inicializar o Docker para Windows, pois, atualmente, apenas o isolamento de Hyper-V tem suporte no Windows 10.

* [Habilitar o Hyper-V no Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)
* [Habilitar o Hyper-V no Windows Server 2016](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server)

> [!NOTE]
> A virtualização deve ser habilitada no computador. Normalmente, ela está habilitada por padrão; no entanto, se a instalação do Hyper-V falhar, consulte a documentação do sistema para saber como habilitar a virtualização.

## <a name="step-2-install-docker-for-windows"></a>Etapa 2. Instalar o Docker para Windows

Caso você use o Windows 10, é possível baixar e instalar a [Docker Community Edition](https://docs.docker.com/docker-for-windows/install). Se usar o Windows Server 2016, siga as [instruções para instalar o Docker Enterprise Edition](https://docs.docker.com/install/windows/docker-ee).

## <a name="step-3-switch-to-windows-containers"></a>Etapa 3. Alternar para os contêineres do Windows

Só é possível instalar as Ferramentas de Build 2017 no Windows, o que requer [alternar para os contêineres do Windows](https://docs.docker.com/docker-for-windows/#getting-started-with-windows-containers). Os contêineres do Windows no Windows 10 têm suporte somente para o [isolamento do Hyper-V](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/hyperv-container), enquanto os contêineres do Windows no Windows Server 2016 oferecem suporte para Hyper-V e isolamento de processo.

## <a name="step-4-expand-maximum-container-disk-size"></a>Etapa 4. Expandir o tamanho de disco máximo do contêiner

As Ferramentas de Build do Visual Studio e, em grande medida, o Visual Studio, exigem muito espaço em disco para todas as ferramentas que são instaladas. Embora o Dockerfile de exemplo desabilite o cache do pacote, o tamanho do disco das imagens de contêiner deve ser aumentado para acomodar o espaço necessário. No Windows, atualmente, é possível aumentar o tamanho do disco somente alterando a configuração do Docker.

**No Windows 10**:

1. [Clique com o botão direito do mouse no ícone do Docker for Windows](https://docs.docker.com/docker-for-windows/#docker-settings) na bandeja do sistema e clique em **Configurações**.
2. [Clique na seção Daemon](https://docs.docker.com/docker-for-windows/#docker-daemon).
3. [Alterne o botão de **Básico**](https://docs.docker.com/docker-for-windows/#edit-the-daemon-configuration-file) para **Avançado**.
4. Adicione a seguinte propriedade de matriz JSON para aumentar o espaço em disco para 120 GB, mais que o suficiente para Ferramentas de Build com espaço para expansão.

   ```json
   {
     "storage-opts": [
       "size=120GB"
     ]
   }
   ```

   Essa propriedade é adicionada a qualquer coisa que você já tiver. Por exemplo, com essas alterações aplicadas ao arquivo de configuração daemon padrão, agora você verá:

   ```json
   {
     "registry-mirrors": [],
     "insecure-registries": [],
     "debug": true,
     "experimental": true,
     "storage-opts": [
       "size=120GB"
     ]
   }
   ```

5. Clique em **Aplicar**.

**No Windows Server 2016**:

1. Interrompa o serviço de "docker":

   ```shell
   sc.exe stop docker
   ```

2. Em um prompt de comandos com privilégios elevados, edite "%ProgramData%\Docker\config\daemon.json" ou o que você especificou para `dockerd --config-file`.
3. Adicione a seguinte propriedade de matriz JSON para aumentar o espaço em disco para 120 GB, mais que o suficiente para Ferramentas de Build com espaço para expansão.

   ```json
   {
     "storage-opts": [
       "size=120GB"
     ]
   }
   ```

   Essa propriedade é adicionada a qualquer coisa que você já tiver.
4. Salve e feche o arquivo.
5. Inicie o serviço de "docker":

   ```shell
   sc.exe start docker
   ```

## <a name="step-5-create-and-build-the-dockerfile"></a>Etapa 5. Criar e compilar o Dockerfile

Salve o Dockerfile de exemplo a seguir em um novo arquivo no disco. Se o nome do arquivo é simplesmente "Dockerfile", ele será reconhecido por padrão.

> [!NOTE]
> Este Dockerfile de exemplo apenas exclui SDKs do Windows mais antigas que não podem ser instaladas nos contêineres. Versões mais antigas fazem com que o comando de build falhe.

1. Abra um prompt de comando.
2. Crie um novo diretório (recomendado):

   ```shell
   mkdir C:\BuildTools
   ```

3. Altere os diretórios para este novo diretório:

   ```shell
   cd C:\BuildTools
   ```

3. Salve o conteúdo a seguir em C:\BuildTools\Dockerfile.

   ```dockerfile
   # escape=`

   # Use the latest Windows Server Core image with .NET Framework 4.7.1.
   FROM microsoft/dotnet-framework:4.7.1

   # Restore the default Windows shell for correct batch processing below.
   SHELL ["cmd", "/S", "/C"]

   # Download the Build Tools bootstrapper.
   ADD https://aka.ms/vs/15/release/vs_buildtools.exe C:\TEMP\vs_buildtools.exe

   # Install Build Tools excluding workloads and components with known issues.
   RUN C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache `
       --installPath C:\BuildTools `
       --all `
       --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
       --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
       --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
       --remove Microsoft.VisualStudio.Component.Windows81SDK `
    || IF "%ERRORLEVEL%"=="3010" EXIT 0

   # Start developer command prompt with any other commands specified.
   ENTRYPOINT C:\BuildTools\Common7\Tools\VsDevCmd.bat &&

   # Default to PowerShell if no other command specified.
   CMD ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
   ```

   > [!NOTE]
   > Se você basear sua imagem diretamente no microsoft/windowsservercore, o .NET Framework poderá não ser instalado corretamente e nenhum erro de instalação será indicado. Código gerenciado não poderá ser executado depois que a instalação for concluída. Em vez disso, baseie sua imagem no [microsoft/dotnet-framework:4.7.1](https://hub.docker.com/r/microsoft/dotnet-framework) ou mais recente. Observe também que imagens mais recentes podem usar o PowerShell como o `SHELL` padrão, o que causará uma falha nas instruções `RUN` e `ENTRYPOINT`.

4. Execute o seguinte comando nesse diretório.

   ```shell
   docker build -t buildtools2017:latest -m 2GB .
   ```

   Este comando cria o Dockerfile no diretório atual usando 2 GB de memória. O 1 GB padrão não é suficiente quando algumas cargas de trabalho são instaladas. No entanto, é possível criar com apenas 1 GB de memória, de acordo com os requisitos de build.

   A imagem final contém uma marca "buildtools2017:latest", então, é possível executá-la facilmente em um contêiner como "buildtools2017", visto que a marca "mais recente" é o padrão se nenhuma marca for especificada. Caso queira utilizar uma versão específica das Ferramentas de Build do Visual Studio 2017 em um [cenário mais avançado](advanced-build-tools-container.md), em vez disso, é possível marcar o contêiner com um número de build específico do Visual Studio, assim como "mais recente", para que os contêineres usem uma versão específica constantemente.

## <a name="step-6-using-the-built-image"></a>Etapa 6. Usar a imagem criada

Agora que a imagem foi criada, é possível executá-la em um contêiner para fazer builds interativos e automatizados. O exemplo usa o Prompt de Comando do Desenvolvedor, assim, PATH e outras variáveis de ambiente já estão configuradas.

1. Abra um prompt de comando.
2. Execute o contêiner para iniciar um ambiente do PowerShell com as variáveis de ambiente de desenvolvedor configuradas:

   ```shell
   docker run -it buildtools2017
   ```

Para usar essa imagem no fluxo de trabalho CI/CD, publique-a no seu próprio [Registro de Contêiner do Azure](https://azure.microsoft.com/services/container-registry) ou em outro [registro Docker](https://docs.docker.com/registry/deploying) interno, assim, os servidores só precisarão efetuar pull.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Exemplo avançado para contêineres](advanced-build-tools-container.md)
* [Problemas Conhecidos de Contêineres](build-tools-container-issues.md)
* [IDs de carga de trabalho e de componente das Ferramentas de Build do Visual Studio 2017](workload-component-id-vs-build-tools.md)

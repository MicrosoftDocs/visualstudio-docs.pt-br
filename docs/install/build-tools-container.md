---
title: Instalar Ferramentas de Build do Visual Studio em um contêiner
titleSuffix: ''
description: Saiba como instalar as Ferramentas de Build do Visual Studio em um contêiner do Windows para oferecer suporte a fluxos de trabalho de CI e CD (integração contínua e entrega contínua).
ms.date: 03/25/2020
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: d5c038e2-e70d-411e-950c-8a54917b578a
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: dcf28f818760320b215cbff0d3a2eb5ad6d9f623
ms.sourcegitcommit: 55b99dbce29d19e493feae9b8d2fdac73718e4de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873062"
---
# <a name="install-build-tools-into-a-container"></a>Instalar Ferramentas de Build em um contêiner

É possível instalar as Ferramentas de Build do Visual Studio em um contêiner do Windows para oferecer suporte a fluxos de trabalho de CI e CD (integração contínua e entrega contínua). Este artigo orienta sobre quais alterações de configuração do Docker são necessárias, bem como quais [cargas de trabalho e componentes](workload-component-id-vs-build-tools.md) podem ser instalados em um contêiner.

Os [contêineres](https://www.docker.com/what-container) são uma ótima maneira de empacotar um sistema de build consistente e podem ser usados não somente em um ambiente de servidor CI/CD, mas também em ambientes de desenvolvimento. Por exemplo, é possível pode montar o código-fonte em um contêiner a ser criado por um ambiente personalizado e, ao mesmo tempo, continuar a usar o Visual Studio ou outras ferramentas para escrever o código. Caso o fluxo de trabalho CI/CD use a mesma imagem de contêiner, fique tranquilo, o código será compilado de forma consistente. Também é possível usar os contêineres para obter consistência em runtime, o que é comum em microsserviços que usam vários contêineres com um sistema de orquestração, mas está fora do escopo deste artigo.

Se as Ferramentas de Build do Visual Studio não têm o que você precisa para compilar o código-fonte, estas etapas podem ser usadas em outros produtos do Visual Studio. Vale ressaltar, no entanto, que os contêineres do Windows não têm suporte para uma interface do usuário interativo, então, todos os comandos devem ser automatizados.

## <a name="before-you-begin"></a>Antes de começar

É esperada alguma familiaridade com o [Docker](https://www.docker.com/what-docker) abaixo. Se você ainda não estiver familiarizado com a execução do Docker no Windows, leia como [instalar e configurar o mecanismo do Docker no Windows](/virtualization/windowscontainers/manage-docker/configure-docker-daemon).

A imagem de base abaixo é uma amostra e pode não funcionar no seu sistema. Leia [Compatibilidade da versão do contêiner do Windows ](/virtualization/windowscontainers/deploy-containers/version-compatibility) para determinar qual imagem de base você deve usar para o seu ambiente.

## <a name="create-and-build-the-dockerfile"></a>Criar e compilar o Dockerfile

Salve o Dockerfile de exemplo a seguir em um novo arquivo no disco. Se o nome do arquivo é simplesmente "Dockerfile", ele será reconhecido por padrão.

> [!WARNING]
> Este Dockerfile de exemplo exclui apenas SDKs do Windows anteriores que não podem ser instalados em contêineres. As versões anteriores causam uma falha no comando de build.

1. Abra um prompt de comando.

1. Crie um novo diretório (recomendado):

   ```shell
   mkdir C:\BuildTools
   ```

1. Altere os diretórios para este novo diretório:

   ```shell
   cd C:\BuildTools
   ```

1. Salve o conteúdo a seguir em C:\BuildTools\Dockerfile.
 
   ::: moniker range="vs-2017"

   ```dockerfile
   # escape=`

   # Use the latest Windows Server Core image with .NET Framework 4.7.2.
   FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

   # Restore the default Windows shell for correct batch processing.
   SHELL ["cmd", "/S", "/C"]

   # Download the Build Tools bootstrapper.
   ADD https://aka.ms/vs/15/release/vs_buildtools.exe C:\TEMP\vs_buildtools.exe

   # Install Build Tools with the Microsoft.VisualStudio.Workload.AzureBuildTools workload, excluding workloads and components with known issues.
   RUN start /wait C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache `
       --installPath C:\BuildTools `
       --add Microsoft.VisualStudio.Workload.AzureBuildTools `
       --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
       --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
       --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
       --remove Microsoft.VisualStudio.Component.Windows81SDK `
    || IF "%ERRORLEVEL%"=="3010" EXIT 0

   # Define the entry point for the Docker container.
   # This entry point starts the developer command prompt and launches the PowerShell shell.
   ENTRYPOINT ["C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
   ```

   > [!TIP]
   > Para obter uma lista de cargas de trabalho e componentes, consulte o [diretório de componentes ferramentas de Build do Visual Studio](workload-component-id-vs-build-tools.md).
   >

   > [!WARNING]
   > Se você basear sua imagem diretamente no microsoft/windowsservercore ou mcr.microsoft.com/windows/servercore (confira [Microsoft distribui o catálogo de contêiner](https://azure.microsoft.com/blog/microsoft-syndicates-container-catalog/)), pode ser que o .NET Framework não seja instalado corretamente e nenhum erro de instalação será indicado. Código gerenciado não poderá ser executado depois que a instalação for concluída. Em vez disso, baseie a imagem no [microsoft/dotnet-framework:4.7.2](https://hub.docker.com/r/microsoft/dotnet-framework) ou posterior. Além disso, as imagens marcadas com a versão 4.7.2 ou posterior podem usar o PowerShell como o `SHELL` padrão, o que causará uma falha nas instruções `RUN` e `ENTRYPOINT`.
   >
   > O Visual Studio 2017 versão 15.8 ou anterior (qualquer produto) não será instalado corretamente no mcr.microsoft.com/windows/servercore:1809 ou posterior. Nenhum erro é exibido.
   >
   > Confira [Compatibilidade da versão de contêiner do Windows](/virtualization/windowscontainers/deploy-containers/version-compatibility) para ver quais versões do sistema operacional do contêiner são compatíveis em quais versões do sistema operacional host e os [Problemas conhecidos de contêineres](build-tools-container-issues.md) para se informar a respeito.
   
   ::: moniker-end

   ::: moniker range="vs-2019"

   ```dockerfile
   # escape=`

   # Use the latest Windows Server Core image with .NET Framework 4.8.
   FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

   # Restore the default Windows shell for correct batch processing.
   SHELL ["cmd", "/S", "/C"]

   # Download the Build Tools bootstrapper.
   ADD https://aka.ms/vs/16/release/vs_buildtools.exe C:\TEMP\vs_buildtools.exe

   # Install Build Tools with the Microsoft.VisualStudio.Workload.AzureBuildTools workload, excluding workloads and components with known issues.
   RUN C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache `
       --installPath C:\BuildTools `
       --add Microsoft.VisualStudio.Workload.AzureBuildTools `
       --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
       --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
       --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
       --remove Microsoft.VisualStudio.Component.Windows81SDK `
    || IF "%ERRORLEVEL%"=="3010" EXIT 0

   # Define the entry point for the docker container.
   # This entry point starts the developer command prompt and launches the PowerShell shell.
   ENTRYPOINT ["C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
   ```

   > [!TIP]
   > Para obter uma lista de cargas de trabalho e componentes, consulte o [diretório de componentes ferramentas de Build do Visual Studio](workload-component-id-vs-build-tools.md).
   >

   > [!WARNING]
   > Se você basear sua imagem diretamente no microsoft/windowsservercore, o .NET Framework poderá não ser instalado corretamente e nenhum erro de instalação será indicado. Código gerenciado não poderá ser executado depois que a instalação for concluída. Em vez disso, baseie a imagem no [microsoft/dotnet-framework:4.8](https://hub.docker.com/r/microsoft/dotnet-framework) ou posterior. As imagens marcadas com a versão 4.8 ou posterior também podem usar o PowerShell como o `SHELL` padrão, o que causará uma falha nas instruções `RUN` e `ENTRYPOINT`.
   >
   > Confira [Compatibilidade da versão de contêiner do Windows](/virtualization/windowscontainers/deploy-containers/version-compatibility) para ver quais versões do sistema operacional do contêiner são compatíveis em quais versões do sistema operacional host e os [Problemas conhecidos de contêineres](build-tools-container-issues.md) para se informar a respeito.

   ::: moniker-end
   
   > [!NOTE]
   > O código `3010` de erro é usado para indicar êxito com uma reinicialização necessária, consulte [MsiExec.exe mensagens de erro](/windows/win32/msi/error-codes) para obter mais informações.

1. Execute o seguinte comando nesse diretório.

   ::: moniker range="vs-2017"

   ```shell
   docker build -t buildtools2017:latest -m 2GB .
   ```

   Este comando cria o Dockerfile no diretório atual usando 2 GB de memória. O 1 GB padrão não é suficiente quando algumas cargas de trabalho são instaladas. No entanto, é possível compilar com apenas 1 GB de memória, de acordo com os requisitos de build.

   A imagem final contém uma marca "buildtools2017:latest", então, é possível executá-la facilmente em um contêiner como "buildtools2017", visto que a marca "mais recente" é o padrão se nenhuma marca for especificada. Caso queira utilizar uma versão específica das Ferramentas de Build do Visual Studio 2017 em um [cenário mais avançado](advanced-build-tools-container.md), em vez disso, é possível marcar o contêiner com um número de build específico do Visual Studio, assim como "mais recente", para que os contêineres usem uma versão específica constantemente.

   ::: moniker-end

   ::: moniker range="vs-2019"

   ```shell
   docker build -t buildtools2019:latest -m 2GB .
   ```

   Este comando cria o Dockerfile no diretório atual usando 2 GB de memória. O 1 GB padrão não é suficiente quando algumas cargas de trabalho são instaladas. No entanto, é possível compilar com apenas 1 GB de memória, de acordo com os requisitos de build.

   A imagem final contém uma marca "buildtools2019:latest", então, é possível executá-la facilmente em um contêiner como "buildtools2019", visto que a marca "mais recente" é o padrão se nenhuma marca é especificada. Caso queira utilizar uma versão específica das Ferramentas de Build do Visual Studio 2019 em um [cenário mais avançado](advanced-build-tools-container.md), em vez disso, é possível marcar o contêiner com um número de build específico do Visual Studio, assim como "mais recente", para que os contêineres usem uma versão específica constantemente.

   ::: moniker-end

## <a name="using-the-built-image"></a>Usar a imagem criada

Agora que a imagem foi criada, é possível executá-la em um contêiner para fazer builds interativos e automatizados. O exemplo usa o Prompt de Comando do Desenvolvedor, assim, PATH e outras variáveis de ambiente já estão configuradas.

1. Abra um prompt de comando.

1. Execute o contêiner para iniciar um ambiente do PowerShell com as variáveis de ambiente de desenvolvedor configuradas:

   ::: moniker range="vs-2017"

   ```shell
   docker run -it buildtools2017
   ```

   ::: moniker-end

   ::: moniker range="vs-2019"

   ```shell
   docker run -it buildtools2019
   ```

   ::: moniker-end

Para usar essa imagem no fluxo de trabalho CI/CD, publique-a no seu próprio [Registro de Contêiner do Azure](https://azure.microsoft.com/services/container-registry) ou em outro [registro Docker](https://docs.docker.com/registry/deploying) interno, assim, os servidores só precisarão efetuar pull dessa imagem.

   > [!NOTE]
   > Se o contêiner do Docker não for iniciado, provavelmente haverá um problema de instalação do Visual Studio. Você pode atualizar o Dockerfile para remover a etapa que chama o comando de lote do Visual Studio. Isso permite que você inicie o contêiner do Docker e leia os logs de erros da instalação.
   >
   > No arquivo Dockerfile, remova os `C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat` parâmetros e `&&` do `ENTRYPOINT` comando. O comando deve ser agora `ENTRYPOINT ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]` . Em seguida, recompile o Dockerfile e execute o `run` comando para acessar os arquivos de contêiner. Para localizar os logs de erros de instalação, vá para o `$env:TEMP` diretório e localize o `dd_setup_<timestamp>_errors.log` arquivo.
   >
   > Depois de identificar e corrigir o problema de instalação, você pode adicionar `C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat` os `&&` parâmetros e de volta ao `ENTRYPOINT` comando e recriar o Dockerfile.
   >
   > Para obter mais informações, veja [Problemas conhecidos de contêineres](build-tools-container-issues.md).

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Exemplo avançado para contêineres](advanced-build-tools-container.md)
* [Problemas conhecidos para contêineres](build-tools-container-issues.md)
* [IDs de carga de trabalho e de componente das Ferramentas de Build do Visual Studio](workload-component-id-vs-build-tools.md)

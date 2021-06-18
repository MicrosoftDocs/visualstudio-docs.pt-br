---
title: Exemplo avançado para contêineres
description: Saiba mais sobre um exemplo avançado para contêineres do Docker. Este exemplo Dockerfile usa uma marca de versão específica da imagem Microsoft/DOTNET-Framework.
ms.custom: SEO-VS-2020
ms.date: 03/25/2020
ms.topic: conceptual
ms.assetid: e03835db-a616-41e6-b339-92b41d0cfc70
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 2860a19592667008f585a4608eab23e0180dd2ac
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307694"
---
# <a name="advanced-example-for-containers"></a>Exemplo avançado para contêineres

::: moniker range="vs-2017"

O Dockerfile de exemplo em [Instalar Ferramentas de Build em um contêiner](build-tools-container.md) sempre usa a imagem [microsoft/dotnet-framework:4.7.2](https://hub.docker.com/r/microsoft/dotnet-framework) baseada na imagem microsoft/windowsservercore e o instalador mais recente das Ferramentas de Build do Visual Studio. Se essa imagem for publicada em um [registro do Docker](https://azure.microsoft.com/services/container-registry) para que outras pessoas efetuem pull, a imagem poderá ser boa para vários cenários. Entretanto, na prática, é mais comum especificar qual imagem base você usa, quais binários você baixa e quais versões de ferramenta você instala.

::: moniker-end

::: moniker range=">=vs-2022"

>[!IMPORTANT]
> O Visual Studio 2022 está atualmente em visualização e não é [licenciado](https://visualstudio.microsoft.com/license-terms/vs2022-prerelease/) para uso em ambientes de produção.

::: moniker-end

::: moniker range=">=vs-2019"

O Dockerfile de exemplo em [Instalar Ferramentas de Build em um contêiner](build-tools-container.md) sempre usa a imagem [microsoft/dotnet-framework:4.8](https://hub.docker.com/r/microsoft/dotnet-framework) baseada na imagem microsoft/windowsservercore e o instalador mais recente das Ferramentas de Build do Visual Studio. Se essa imagem for publicada em um [registro do Docker](https://azure.microsoft.com/services/container-registry) para que outras pessoas efetuem pull, a imagem poderá ser boa para vários cenários. Entretanto, na prática, é mais comum especificar qual imagem base você usa, quais binários você baixa e quais versões de ferramenta você instala.

::: moniker-end

O Dockerfile de exemplo a seguir usa uma marca de versão específica da imagem microsoft/dotnet-framework. Usar uma marca específica para uma imagem base é comum e torna mais fácil lembrar dessa compilação ou recriar imagens que sempre têm a mesma base.

> [!NOTE]
> Não é possível instalar o Visual Studio no microsoft/windowsservercore:10.0.14393.1593 ou em qualquer imagem baseada nele, que tem problemas conhecidos ao iniciar o instalador em um contêiner. Para obter mais informações, veja [Problemas conhecidos de contêineres](build-tools-container-issues.md).

O exemplo a seguir faz o download da versão mais recente das Ferramentas de Build. Caso deseje usar uma versão anterior das Ferramentas de Build que possa ser instalada em um contêiner posteriormente, primeiro você precisará [criar](create-an-offline-installation-of-visual-studio.md) e [manter](update-a-network-installation-of-visual-studio.md) um layout.

## <a name="install-script"></a>Script de instalação

Para coletar logs quando ocorrerem erros de instalação, no diretório de trabalho, crie um script em lotes chamado "Install.cmd" com o seguinte conteúdo:

```shell
@if not defined _echo echo off
setlocal enabledelayedexpansion

call %*
if "%ERRORLEVEL%"=="3010" (
    exit /b 0
) else (
    if not "%ERRORLEVEL%"=="0" (
        set ERR=%ERRORLEVEL%
        call C:\TEMP\collect.exe -zip:C:\vslogs.zip

        exit /b !ERR!
    )
)
```

## <a name="dockerfile"></a>Dockerfile

No diretório de trabalho, crie o "Dockerfile" com o seguinte conteúdo:

::: moniker range="vs-2017"

```dockerfile
# escape=`

# Use a specific tagged image.
ARG FROM_IMAGE=mcr.microsoft.com/dotnet/framework/runtime:4.8
FROM ${FROM_IMAGE}

# Restore the default Windows shell for correct batch processing.
SHELL ["cmd", "/S", "/C"]

# Copy our Install script.
COPY Install.cmd C:\TEMP\

# Download collect.exe in case of an install failure.
ADD https://aka.ms/vscollect.exe C:\TEMP\collect.exe

# Use the latest release channel. For more control, specify the location of an internal layout.
ARG CHANNEL_URL=https://aka.ms/vs/15/release/channel
ADD ${CHANNEL_URL} C:\TEMP\VisualStudio.chman

# Install Build Tools with the Microsoft.VisualStudio.Workload.AzureBuildTools workload, excluding workloads and components with known issues.
ADD https://aka.ms/vs/15/release/vs_buildtools.exe C:\TEMP\vs_buildtools.exe
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache `
    --installPath C:\BuildTools `
    --channelUri C:\TEMP\VisualStudio.chman `
    --installChannelUri C:\TEMP\VisualStudio.chman `
    --add Microsoft.VisualStudio.Workload.AzureBuildTools `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
    --remove Microsoft.VisualStudio.Component.Windows81SDK

# Define the entry point for the Docker container.
# This entry point starts the developer command prompt and launches the PowerShell shell.
ENTRYPOINT ["C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
```

   > [!WARNING]
   > O Visual Studio 2017 versão 15.8 ou anterior (qualquer produto) não será instalado corretamente no mcr\.microsoft\.com\/windows\/servercore:1809 ou posterior. Nenhum erro é exibido.
   >
   > Confira [Problemas conhecidos de contêineres](build-tools-container-issues.md) para obter mais informações.

::: moniker-end

::: moniker range="vs-2019"

```dockerfile
# escape=`

# Use a specific tagged image. Tags can be changed, though that is unlikely for most images.
# You could also use the immutable tag @sha256:324e9ab7262331ebb16a4100d0fb1cfb804395a766e3bb1806c62989d1fc1326
ARG FROM_IMAGE=mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019
FROM ${FROM_IMAGE}

# Restore the default Windows shell for correct batch processing.
SHELL ["cmd", "/S", "/C"]

# Copy our Install script.
COPY Install.cmd C:\TEMP\

# Download collect.exe in case of an install failure.
ADD https://aka.ms/vscollect.exe C:\TEMP\collect.exe

# Use the latest release channel. For more control, specify the location of an internal layout.
ARG CHANNEL_URL=https://aka.ms/vs/16/release/channel
ADD ${CHANNEL_URL} C:\TEMP\VisualStudio.chman

# Install Build Tools with the Microsoft.VisualStudio.Workload.AzureBuildTools workload, excluding workloads and components with known issues.
ADD https://aka.ms/vs/16/release/vs_buildtools.exe C:\TEMP\vs_buildtools.exe
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache `
    --installPath C:\BuildTools `
    --channelUri C:\TEMP\VisualStudio.chman `
    --installChannelUri C:\TEMP\VisualStudio.chman `
    --add Microsoft.VisualStudio.Workload.AzureBuildTools `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
    --remove Microsoft.VisualStudio.Component.Windows81SDK

# Define the entry point for the Docker container.
# This entry point starts the developer command prompt and launches the PowerShell shell.
ENTRYPOINT ["C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
```

::: moniker-end

::: moniker range=">=vs-2022"

>[!IMPORTANT]
> O Visual Studio 2022 está atualmente em visualização e não é [licenciado](https://visualstudio.microsoft.com/license-terms/vs2022-prerelease/) para uso em ambientes de produção.

```dockerfile
# escape=`

# Use a specific tagged image. Tags can be changed, though that is unlikely for most images.
# You could also use the immutable tag @sha256:324e9ab7262331ebb16a4100d0fb1cfb804395a766e3bb1806c62989d1fc1326
ARG FROM_IMAGE=mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019
FROM ${FROM_IMAGE}

# Restore the default Windows shell for correct batch processing.
SHELL ["cmd", "/S", "/C"]

# Copy our Install script.
COPY Install.cmd C:\TEMP\

# Download collect.exe in case of an install failure.
ADD https://aka.ms/vscollect.exe C:\TEMP\collect.exe

# Use the latest release channel. For more control, specify the location of an internal layout.
ARG CHANNEL_URL=https://aka.ms/vs/17/preview/channel
ADD ${CHANNEL_URL} C:\TEMP\VisualStudio.chman

# Install Build Tools with the Microsoft.VisualStudio.Workload.AzureBuildTools workload, excluding workloads and components with known issues.
ADD https://aka.ms/vs/17/preview/vs_buildtools.exe C:\TEMP\vs_buildtools.exe
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache `
    --installPath C:\BuildTools `
    --channelUri C:\TEMP\VisualStudio.chman `
    --installChannelUri C:\TEMP\VisualStudio.chman `
    --add Microsoft.VisualStudio.Workload.AzureBuildTools `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
    --remove Microsoft.VisualStudio.Component.Windows81SDK

# Define the entry point for the Docker container.
# This entry point starts the developer command prompt and launches the PowerShell shell.
ENTRYPOINT ["C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
```

::: moniker-end

Execute o seguinte comando para criar a imagem no diretório de trabalho atual:

::: moniker range="vs-2017"

```shell
docker build -t buildtools2017:15.6.27428.2037 -t buildtools2017:latest -m 2GB .
```

::: moniker-end

::: moniker range="vs-2019"

```shell
docker build -t buildtools2019:16.0.28714.193 -t buildtools2019:latest -m 2GB .
```

::: moniker-end

::: moniker range=">=vs-2022"

```shell
docker build -t buildtools2022:17.0 -t buildtools2022:latest -m 2GB .
```

::: moniker-end

Opcionalmente, passar um ou os dois argumentos `FROM_IMAGE` e `CHANNEL_URL` usando a opção de linha de comando `--build-arg` para especificar uma imagem de base diferente ou o local de um layout interno para manter uma imagem fixa.

> [!TIP]
> Para obter uma lista de cargas de trabalho e componentes, consulte o [diretório de componentes ferramentas de Build do Visual Studio](workload-component-id-vs-build-tools.md).
>

## <a name="diagnosing-install-failures"></a>Diagnosticando falhas de instalação

Este exemplo baixa ferramentas específicas e valida as correspondência dos hashes. Ele também baixa o Visual Studio e o utilitário de coleção de logs do .NET, assim, se ocorrer uma falha na instalação, será possível copiar os logs para o computador host, a fim de analisar a falha.

::: moniker range="vs-2017"

```shell
> docker build -t buildtools2017:15.6.27428.2037 -t buildtools2017:latest -m 2GB .
Sending build context to Docker daemon

...
Step 8/10 : RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache ...
 ---> Running in 4b62b4ce3a3c
The command 'cmd /S /C C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe ...' returned a non-zero code: 1603

> docker cp 4b62b4ce3a3c:C:\vslogs.zip "%TEMP%\vslogs.zip"
```

::: moniker-end

::: moniker range="vs-2019"

```shell
> docker build -t buildtools2019:16.0.28714.193 -t buildtools2019:latest -m 2GB .
Sending build context to Docker daemon

...
Step 8/10 : RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache ...
 ---> Running in 4b62b4ce3a3c
The command 'cmd /S /C C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe ...' returned a non-zero code: 1603

> docker cp 4b62b4ce3a3c:C:\vslogs.zip "%TEMP%\vslogs.zip"
```

::: moniker-end

::: moniker range=">=vs-2022"

```shell
> docker build -t buildtools2022:17.0 -t buildtools2022:latest -m 2GB .
Sending build context to Docker daemon

...
Step 8/10 : RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache ...
 ---> Running in 4b62b4ce3a3c
The command 'cmd /S /C C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe ...' returned a non-zero code: 1603

> docker cp 4b62b4ce3a3c:C:\vslogs.zip "%TEMP%\vslogs.zip"
```

::: moniker-end

Depois do fim da execução da última linha, abra "%TEMP%\vslogs.zip" no computador ou envie um problema no site da [Comunidade de Desenvolvedores](https://aka.ms/feedback/suggest?space=8).

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Instalar ferramentas de build em um contêiner](build-tools-container.md)
* [Problemas conhecidos para contêineres](build-tools-container-issues.md)
* [IDs de carga de trabalho e de componente das Ferramentas de Build do Visual Studio](workload-component-id-vs-build-tools.md)

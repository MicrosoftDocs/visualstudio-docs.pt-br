---
title: Exemplo avançado para contêineres
description: ''
ms.date: 04/18/2018
ms.technology: vs-acquisition
ms.custom: ''
ms.prod: visual-studio-dev15
ms.topic: conceptual
ms.assetid: e03835db-a616-41e6-b339-92b41d0cfc70
author: heaths
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e1c79051627bd59ae48b0ad88411a94f4cb36c78
ms.sourcegitcommit: 0cdd8e8a53fb4fd5e869f07c35204419fa12783d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53159809"
---
# <a name="advanced-example-for-containers"></a>Exemplo avançado para contêineres

O Dockerfile de exemplo em [Instalar Ferramentas de Build em um contêiner](build-tools-container.md) sempre usa a imagem [microsoft/dotnet-framework:4.7.1](https://hub.docker.com/r/microsoft/dotnet-framework) baseada na imagem microsoft/windowsservercore e o instalador mais recente das Ferramentas de Build do Visual Studio 2017. Se essa imagem for publicada em um [registro do Docker](https://azure.microsoft.com/services/container-registry) para que outras pessoas efetuem pull, a imagem podem ser boa para vários cenários. Entretanto, na prática, é mais comum especificar qual imagem base você usa, quais binários você baixa e quais versões de ferramenta você instala.

O Dockerfile de exemplo a seguir usa uma marca de versão específica da imagem microsoft/dotnet-framework. Usar uma marca específica para uma imagem base é comum e torna mais fácil lembrar dessa compilação ou recriar imagens que sempre têm a mesma base.

> [!NOTE]
> Não é possível instalar o Visual Studio no microsoft/windowsservercore:10.0.14393.1593 ou em qualquer imagem baseada nele, que tem problemas conhecidos ao iniciar o instalador em um contêiner. Para saber mais, confira os [problemas conhecidos](build-tools-container-issues.md).

O exemplo a seguir faz o download da versão mais recente das Ferramentas de Build 2017. Se quiser usar uma versão anterior das Ferramentas de Build que você pode instalar em um contêiner posteriormente, você deve primeiro [criar](create-an-offline-installation-of-visual-studio.md) e [manter](update-a-network-installation-of-visual-studio.md) um layout.

## <a name="install-script"></a>Script de instalação

Para coletar logs quando ocorrerem erros de instalação, no diretório de trabalho, crie um script em lotes chamado "install.cmd" com o seguinte conteúdo:

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

```dockerfile
# escape=`

# Use a specific tagged image. Tags can be changed, though that is unlikely for most images.
# You could also use the immutable tag @sha256:1a66e2b5f3a5b8b98ac703a8bfd4902ae60d307ed9842978df40dbc04ac86b1b
ARG FROM_IMAGE=microsoft/dotnet-framework:4.7.1-20180410-windowsservercore-1709
FROM ${FROM_IMAGE}

# Copy our Install script.
COPY Install.cmd C:\TEMP\

# Download collect.exe in case of an install failure.
ADD https://aka.ms/vscollect.exe C:\TEMP\collect.exe

# Use the latest release channel. For more control, specify the location of an internal layout.
ARG CHANNEL_URL=https://aka.ms/vs/15/release/channel
ADD ${CHANNEL_URL} C:\TEMP\VisualStudio.chman

# Download and install Build Tools excluding workloads and components with known issues.
ADD https://aka.ms/vs/15/release/vs_buildtools.exe C:\TEMP\vs_buildtools.exe
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache `
    --installPath C:\BuildTools `
    --channelUri C:\TEMP\VisualStudio.chman `
    --installChannelUri C:\TEMP\VisualStudio.chman `
    --all `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
    --remove Microsoft.VisualStudio.Component.Windows81SDK

# Start developer command prompt with any other commands specified.
ENTRYPOINT C:\BuildTools\Common7\Tools\VsDevCmd.bat &&

# Default to PowerShell if no other command specified.
CMD ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
```

Execute o seguinte comando para criar a imagem no diretório de trabalho atual:

```shell
docker build -t buildtools2017:15.6.27428.2037 -t buildtools2017:latest -m 2GB .
```

Opcionalmente, passar um ou os dois argumentos `FROM_IMAGE` e `CHANNEL_URL` usando a opção de linha de comando `--build-arg` para especificar uma imagem de base diferente ou o local de um layout interno para manter uma imagem fixa.

## <a name="diagnosing-install-failures"></a>Diagnosticando falhas de instalação

Este exemplo baixa ferramentas específicas e valida as correspondência dos hashes. Ele também baixa o Visual Studio e o utilitário de coleção de logs do .NET, assim, se ocorrer uma falha na instalação, será possível copiar os logs para o computador host, a fim de analisar a falha.

```shell
> docker build -t buildtools2017:15.6.27428.2037 -t buildtools2017:latest -m 2GB .
Sending build context to Docker daemon
...
Step 8/10 : RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache ...
 ---> Running in 4b62b4ce3a3c
The command 'cmd /S /C C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe ...' returned a non-zero code: 1603

> docker cp 4b62b4ce3a3c:C:\vslogs.zip "%TEMP%\vslogs.zip"
```

Depois do fim da execução da última linha, abra "%TEMP%\vslogs.zip" no computador ou envie um problema no site da [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com).

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Instalar ferramentas de build em um contêiner](build-tools-container.md)
* [Problemas Conhecidos de Contêineres](build-tools-container-issues.md)
* [IDs de carga de trabalho e de componente das Ferramentas de Build do Visual Studio 2017](workload-component-id-vs-build-tools.md)

---
title: Problemas conhecidos de contêineres
description: Saiba mais sobre os problemas conhecidos que podem ocorrer quando as Ferramentas de Build do Visual Studio são instaladas em um contêiner do Windows.
ms.date: 02/18/2020
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: 140083f1-05bc-4014-949e-fb5802397c7a
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: a56d820805fa97f3672480c063ebfcc0fdc96fb6
ms.sourcegitcommit: 0499d813d5c24052c970ca15373d556a69507250
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2021
ms.locfileid: "113046086"
---
# <a name="known-issues-for-containers"></a>Problemas conhecidos de contêineres

Há alguns problemas ao instalar o Visual Studio em um contêiner do Docker.

## <a name="windows-container"></a>Contêiner do Windows

Estes problemas conhecidos ocorrem quando as Ferramentas de Build do Visual Studio são instaladas em um contêiner do Windows.

::: moniker range="vs-2017"

* Não é possível instalar o Visual Studio em um contêiner com base na imagem mcr.microsoft.com/windows/servercore:10.0.14393.1593. As imagens marcadas com versões do Windows anteriores ou posteriores à versão 10.0.14393 deverão funcionar.

* Não é possível instalar o SDK do Windows versão 10.0.14393 ou anterior. A instalação de certos pacotes falha e as cargas de trabalho que dependem desses pacotes não funcionarão.

::: moniker-end

* Passe `-m 2GB` (ou mais) ao compilar a imagem. Algumas cargas de trabalho exigem mais memória que o padrão de 1 GB quando instaladas.
* Configure o Docker para usar discos maiores que o padrão de 20 GB.
* Passe `--norestart` na linha de comando. A partir dessa gravação, tentar reiniciar um contêiner do Windows dentro do contêiner retorna `ERROR_TOO_MANY_OPEN_FILES` para o host.
* Se você basear sua imagem diretamente no mcr.microsoft.com/windows/servercore, o .NET Framework poderá não ser instalado corretamente e nenhum erro de instalação será indicado. Código gerenciado não poderá ser executado depois que a instalação for concluída. Em vez disso, baseie a imagem no [microsoft/dotnet-framework:4.7.1](https://hub.docker.com/r/microsoft/dotnet-framework) ou posterior. Por exemplo, ao compilar com o MSBuild, você poderá ver um erro semelhante ao seguinte:

  > C:\BuildTools\MSBuild\15.0\bin\Roslyn\Microsoft.CSharp.Core.targets(84,5): erro MSB6003: Não foi possível executar o executável da tarefa especificado "csc.exe". Não foi possível carregar o arquivo ou assembly “System.IO.FileSystem, Version=4.0.1.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" ou uma de suas dependências. O sistema não pode encontrar o arquivo especificado.

::: moniker range="vs-2017"

* Não é possível instalar o Visual Studio 2017 versão 15.8 ou anterior (qualquer produto) no mcr.microsoft.com/windows/servercore:1809 ou posterior. Consulte https://aka.ms/setup/containers/servercore1809 para obter mais informações.

::: moniker-end

## <a name="build-tools-container"></a>Contêiner das Ferramentas de Build

Os problemas conhecidos a seguir podem ocorrer ao usar o contêiner das Ferramentas de Build. Para ver se os problemas foram corrigidos ou se há outros problemas conhecidos, visite [comunidade de desenvolvedores](https://aka.ms/feedback/suggest?space=8).

* O IntelliTrace pode não funcionar em [alguns cenários](https://github.com/Microsoft/vstest/issues/940) dentro de um contêiner.
* Em versões mais antigas do Docker for Windows, o tamanho da imagem de contêiner padrão é de apenas 20 GB e não cabe nas Ferramentas de Criação. Siga as [instruções para alterar o tamanho da imagem](/virtualization/windowscontainers/manage-containers/container-storage#storage-limits) para 127 GB ou mais.
Para confirmar um problema de espaço em disco, verifique os arquivos de log para obter mais informações. O `vslogs\dd_setup_<timestamp>_errors.log` arquivo incluirá o seguinte se você ficar sem espaço em disco: 
```
Pre-check verification: Visual Studio needs at least 91.99 GB of disk space. Try to free up space on C:\ or change your target drive.
Pre-check verification failed with error(s) :  SizePreCheckEvaluator.
```
[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Instalar ferramentas de build em um contêiner](build-tools-container.md)
* [Exemplo avançado para contêineres](advanced-build-tools-container.md)
* [IDs de carga de trabalho e de componente das Ferramentas de Build do Visual Studio](workload-component-id-vs-build-tools.md)

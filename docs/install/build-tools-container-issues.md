---
title: Problemas conhecidos de contêineres
description: Saiba mais sobre os problemas conhecidos que podem ocorrer quando as Ferramentas de Build do Visual Studio 2017 são instaladas em um contêiner do Windows.
ms.custom: ''
ms.date: 04/18/2018
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: conceptual
ms.assetid: 140083f1-05bc-4014-949e-fb5802397c7a
author: heaths
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c94c6756e1272b08136f624e9cde63523d630b35
ms.sourcegitcommit: 6b092e7d466377f06913d49d183dbbdca16730f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2018
ms.locfileid: "43139139"
---
# <a name="known-issues-for-containers"></a>Problemas conhecidos de contêineres

Há alguns problemas ao instalar o Visual Studio em um contêiner do Docker.

## <a name="windows-container"></a>Contêiner do Windows

Estes problemas conhecidos ocorrem quando as Ferramentas de Build do Visual Studio 2017 são instaladas em um contêiner do Windows.

* Não é possível instalar o Visual Studio em um contêiner com base na imagem microsoft/windowsservercore:10.0.14393.1593. Imagens marcadas com as versões mais antigas ou mais recentes do Windows devem funcionar.
* Não é possível instalar versões do SDK do Windows mais antigas que a 10.0.14393. A instalação de certos pacotes falha e as cargas de trabalho que dependem desses pacotes não funcionarão.
* Passe `-m 2GB` (ou mais) ao compilar a imagem. Algumas cargas de trabalho exigem mais memória que o padrão de 1 GB quando instaladas.
* Configure o Docker para usar discos maiores que o padrão de 20 GB.
* Passe `--norestart` na linha de comando. A partir dessa gravação, tentar reiniciar um contêiner do Windows dentro do contêiner retorna `ERROR_TOO_MANY_OPEN_FILES` para o host.
* Se você basear sua imagem diretamente no microsoft/windowsservercore, o .NET Framework poderá não ser instalado corretamente e nenhum erro de instalação será indicado. Código gerenciado não poderá ser executado depois que a instalação for concluída. Em vez disso, baseie sua imagem no [microsoft/dotnet-framework:4.7.1](https://hub.docker.com/r/microsoft/dotnet-framework) ou mais recente. Por exemplo, você poderá ver um erro ao compilar com o MSBuild, como:

  > C:\BuildTools\MSBuild\15.0\bin\Roslyn\Microsoft.CSharp.Core.targets(84,5): erro MSB6003: Não foi possível executar o executável da tarefa especificado "csc.exe". Não foi possível carregar o arquivo ou assembly “System.IO.FileSystem, Version=4.0.1.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" ou uma de suas dependências. O sistema não pode encontrar o arquivo especificado.

## <a name="build-tools-container"></a>Contêiner das Ferramentas de Build

Os problemas conhecidos a seguir podem ocorrer ao usar o contêiner das Ferramentas de Build. Para ver se os problemas foram corrigidos ou se há outros problemas conhecidos, visite https://developercommunity.visualstudio.com.

* O IntelliTrace pode não funcionar em [alguns cenários](https://github.com/Microsoft/vstest/issues/940) dentro de um contêiner.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Instalar ferramentas de build em um contêiner](build-tools-container.md)
* [Exemplo avançado para contêineres](advanced-build-tools-container.md)
* [IDs de carga de trabalho e de componente das Ferramentas de Build do Visual Studio 2017](workload-component-id-vs-build-tools.md)

---
title: Propriedades de compilação das ferramentas de contêiner do Visual Studio
author: ghogen
description: Visão geral do processo de Build das ferramentas de contêiner
ms.author: ghogen
ms.date: 06/06/2019
ms.technology: vs-azure
ms.topic: reference
ms.openlocfilehash: 427a70d9bc4f6ef326ffb16e7d26df9d8fae2365
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283197"
---
# <a name="container-tools-build-properties"></a>Propriedades de compilação das ferramentas de contêiner

Você pode personalizar como o Visual Studio cria seus projetos de contêiner definindo as propriedades que o MSBuild usa para criar seu projeto. Por exemplo, você pode alterar o nome do Dockerfile, especificar marcas e rótulos para suas imagens, fornecer argumentos adicionais passados para comandos do Docker e controlar se o Visual Studio realiza determinadas otimizações de desempenho, como a criação fora do ambiente de contêiner. Você também pode definir propriedades de depuração, como o nome do executável a ser iniciado, e os argumentos de linha de comando a serem fornecidos.

Para definir o valor de uma propriedade, edite o arquivo de projeto. Por exemplo, suponha que seu Dockerfile seja chamado de *MyDockerfile*. Você pode definir a `DockerfileFile` propriedade no arquivo de projeto da seguinte maneira.

```xml
<PropertyGroup>
   <DockerfileFile>MyDockerfile</DockerfileFile>
</PropertyGroup>
```

Você pode adicionar a configuração de propriedade a um `PropertyGroup` elemento existente ou, se não houver um, crie um novo `PropertyGroup` elemento.

A tabela a seguir mostra as propriedades do MSBuild disponíveis para projetos de contêiner. A versão do pacote NuGet aplica-se a [Microsoft. VisualStudio. Azure. containers. Tools. targets](https://www.nuget.org/packages/Microsoft.VisualStudio.Azure.Containers.Tools.Targets/).

| Nome da propriedade | Descrição | Valor padrão  | Versão do pacote NuGet|
|---------------|-------------|----------------|----------------------|
| ContainerDevelopmentMode | Controla se a otimização "Build-on-host" (depuração "modo rápido") está habilitada.  Os valores permitidos são **rápido** e **regular**. | Rápido |1.0.1872750 ou mais recente|
| ContainerVsDbgPath | O caminho para o depurador VSDBG. | `%USERPROFILE%\vsdbg\vs2017u5` |1.0.1985401 ou mais recente|
| DockerDebuggeeArguments | Durante a depuração, o depurador é instruído a passar esses argumentos para o executável iniciado. | Não aplicável a projetos de .NET Framework ASP.NET |1.7.8 ou mais recente|
| DockerDebuggeeProgram | Durante a depuração, o depurador é instruído a iniciar este executável. | Para projetos do .NET Core: dotnet, ASP.NET .NET Framework projetos: não aplicável (o IIS é sempre usado) |1.7.8 ou mais recente|
| DockerDebuggeeKillProgram | Esse comando é usado para eliminar o processo em execução em um contêiner. | Não aplicável a projetos de .NET Framework ASP.NET |1.7.8 ou mais recente|
| DockerDebuggeeWorkingDirectory | Durante a depuração, o depurador é instruído a usar esse caminho como o diretório de trabalho. | C:\app (Windows) ou/app (Linux) |1.7.8 ou mais recente|
| DockerDefaultTargetOS | O sistema operacional de destino padrão usado ao criar a imagem do Docker. | Definido pelo Visual Studio. |1.0.1985401 ou mais recente|
| DockerImageLabels | O conjunto padrão de rótulos aplicados à imagem do Docker. | com. Microsoft. Created-by = Visual-Studio; com. Microsoft. Visual-Studio. Project-Name = $ (MSBuildProjectName) |1.5.4 ou mais recente|
| DockerFastModeProjectMountDirectory|No **modo rápido**, essa propriedade controla onde o diretório de saída do projeto é montado em volume no contêiner em execução.|C:\app (Windows) ou/app (Linux)|1.9.2 ou mais recente|
| DockerfileBuildArguments | Argumentos adicionais passados para o comando de [Build do Docker](https://docs.docker.com/engine/reference/commandline/build/) . | Não aplicável. |1.0.1872750 ou mais recente|
| DockerfileContext | O contexto padrão usado ao criar a imagem do Docker, como um caminho relativo ao Dockerfile. | Definido pelo Visual Studio. |1.0.1872750 ou mais recente|
| DockerfileFastModeStage | O estágio Dockerfile (ou seja, Target) a ser usado ao criar a imagem no modo de depuração. | Primeiro estágio encontrado no Dockerfile (base) |
| DockerfileFile | Descreve o Dockerfile padrão que será usado para compilar/executar o contêiner para o projeto. Isso também pode ser um caminho. | Dockerfile |1.0.1872750 ou mais recente|
| DockerfileRunArguments | Argumentos adicionais passados para o comando de [execução do Docker](https://docs.docker.com/engine/reference/commandline/run/) . | Não aplicável. |1.0.1872750 ou mais recente|
| DockerfileRunEnvironmentFiles | Lista delimitada por ponto e vírgula dos arquivos de ambiente aplicados durante a execução do Docker. | Não aplicável. |1.0.1872750 ou mais recente|
| DockerfileTag | A marca que será usada ao criar a imagem do Docker. Na depuração, um ":d EV" é acrescentado à marca. | Nome do assembly após a remoção de caracteres não alfanuméricos com as seguintes regras: <br/> Se a marca resultante for todos numéricas, "Image" será inserida como um prefixo (por exemplo, image2314) <br/> Se a marca resultante for uma cadeia de caracteres vazia, "Image" será usada como a marca. |1.0.1872750 ou mais recente|

## <a name="example"></a>Exemplo

O arquivo de projeto a seguir mostra exemplos de algumas dessas configurações.

```xml
 <Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp3.1</TargetFramework>
    <UserSecretsId>feae72bf-2368-4487-b6c6-546c19338cb1</UserSecretsId>
    <DockerDefaultTargetOS>Linux</DockerDefaultTargetOS>
    <!-- In CI/CD scenarios, you might need to change the context. By default, Visual Studio uses the
         folder above the Dockerfile. The path is relative to the Dockerfile, so here the context is
         set to the same folder as the Dockerfile. -->
    <DockerfileContext>.</DockerfileContext>
    <!-- Set `docker run` arguments to mount a volume -->
    <DockerfileRunArguments>-v $(pwd)/host-folder:/container-folder:ro</DockerfileRunArguments>
    <!-- Set `docker build` arguments to add a custom tag -->
    <DockerfileBuildArguments>-t contoso/front-end:v2.0</DockerfileBuildArguments>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.VisualStudio.Azure.Containers.Tools.Targets" Version="1.10.6" />
  </ItemGroup>

</Project>
```

## <a name="next-steps"></a>Próximas etapas

Para obter informações sobre propriedades do MSBuild em geral, consulte [Propriedades do MSBuild](../msbuild/msbuild-properties.md).

## <a name="see-also"></a>Veja também

[Docker Compose Propriedades de compilação](docker-compose-properties.md)

[Configurações de inicialização das ferramentas de contêiner](container-launch-settings.md)

[Propriedades reservadas e conhecidas do MSBuild](../msbuild/msbuild-reserved-and-well-known-properties.md)

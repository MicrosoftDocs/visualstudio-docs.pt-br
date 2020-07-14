---
title: Ferramentas de contêiner do Visual Studio Docker Compose configurações de compilação
author: ghogen
description: Visão geral do processo de Build das ferramentas de contêiner
ms.author: ghogen
ms.date: 08/12/2019
ms.technology: vs-azure
ms.topic: reference
ms.openlocfilehash: 6d352461fd6ad96ae40d9c38a250c93018b1cd9a
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283145"
---
# <a name="docker-compose-build-properties"></a>Docker Compose Propriedades de compilação

Além das propriedades que controlam projetos individuais do Docker, descritas em [ferramentas de contêiner Propriedades de compilação](container-msbuild-properties.md), você também pode personalizar como o Visual Studio cria seus projetos de Docker Compose definindo as propriedades de Docker Compose que o MSBuild usa para criar sua solução. Você também pode controlar como o depurador do Visual Studio executa seus aplicativos Docker Compose definindo rótulos de arquivo em Docker Compose arquivos de configuração.

## <a name="how-to-set-the-msbuild-properties"></a>Como definir as propriedades do MSBuild

Para definir o valor de uma propriedade, edite o arquivo de projeto. Para propriedades Docker Compose, esse arquivo de projeto é aquele com uma extensão. dcproj, a menos que indicado em contrário na tabela na próxima seção. Por exemplo, suponha que você queira especificar para iniciar o navegador quando iniciar a depuração. Você pode definir a `DockerLaunchAction` propriedade no arquivo de projeto. dcproj da seguinte maneira.

```xml
<PropertyGroup>
   <DockerLaunchAction>LaunchBrowser</DockerLaunchAction>
</PropertyGroup>
```

Você pode adicionar a configuração de propriedade a um `PropertyGroup` elemento existente ou, se não houver um, crie um novo `PropertyGroup` elemento.

## <a name="docker-compose-msbuild-properties"></a>Propriedades do Docker Compose no MSBuild

A tabela a seguir mostra as propriedades do MSBuild disponíveis para projetos Docker Compose.

| Nome da propriedade | Location | Descrição | Valor padrão  |
|---------------|----------|-------------|----------------|
|AdditionalComposeFilePaths|dcproj|Especifica arquivos de composição adicionais em uma lista delimitada por ponto-e-vírgula a serem enviados para docker-compose.exe para todos os comandos. São permitidos caminhos relativos do arquivo de projeto Docker-Compose (dcproj).|-|
|DockerComposeBaseFilePath|dcproj|Especifica a primeira parte dos nomes de arquivo dos arquivos Docker-Compose, sem a extensão *. yml* . Por exemplo: <br>1. DockerComposeBaseFilePath = NULL/undefined: Use o caminho do arquivo base *Docker-Compose*, e os arquivos serão nomeados *Docker-Compose. yml* e *Docker-Compose. Override. yml*<br>2. DockerComposeBaseFilePath = *mydockercompose*: os arquivos serão nomeados *mydockercompose. yml* e *mydockercompose. Override. yml*<br> 3. DockerComposeBaseFilePath = *.. \mydockercompose*: os arquivos terão um nível acima. |Docker-Compose|
|DockerComposeBuildArguments|dcproj|Especifica os parâmetros extras a serem passados para o `docker-compose build` comando. Por exemplo, `--parallel --pull` |
|DockerComposeDownArguments|dcproj|Especifica os parâmetros extras a serem passados para o `docker-compose down` comando. Por exemplo, `--timeout 500`|-|  
|DockerComposeProjectPath|csproj ou vbproj|O caminho relativo para o arquivo de projeto do Docker-Compose (dcproj). Defina essa propriedade ao publicar o projeto de serviço para localizar as configurações de Build de imagem associadas armazenadas no arquivo Docker-Compose. yml.|-|
|DockerComposeUpArguments|dcproj|Especifica os parâmetros extras a serem passados para o `docker-compose up` comando. Por exemplo, `--timeout 500`|-|
|DockerDevelopmentMode|dcproj| Controla se a otimização "Build-on-host" (depuração "modo rápido") está habilitada.  Os valores permitidos são **rápido** e **regular**. | Rápido |
|DockerLaunchAction| dcproj | Especifica a ação de inicialização a ser executada em F5 ou CTRL + F5.  Os valores permitidos são None, LaunchBrowser e LaunchWCFTestClient|Nenhum|
|DockerLaunchBrowser| dcproj | Indica se o navegador deve ser iniciado. Ignorado se DockerLaunchAction for especificado. | Falso |
|DockerServiceName| dcproj|Se DockerLaunchAction ou DockerLaunchBrowser forem especificados, DockerServiceName será o nome do serviço que deve ser iniciado.  Use essa propriedade para determinar qual dos possíveis projetos que podem ser referenciados por um arquivo Docker-Compose será iniciado.|-|
|DockerServiceUrl| dcproj | A URL a ser usada ao iniciar o navegador.  Os tokens de substituição válidos são "{% IPAddress}", "{ServicePortal}" e "{Scheme}".  Por exemplo: {Scheme}://{ServiceIPAddress}: {ServicePortal}|-|
|DockerTargetOS| dcproj | O sistema operacional de destino usado ao criar a imagem do Docker.|-|

## <a name="example"></a>Exemplo

Se você alterar o local dos arquivos do Docker Compose, definindo `DockerComposeBaseFilePath` para um caminho relativo, você também precisará certificar-se de que o contexto de compilação foi alterado para que ele faça referência à pasta da solução. Por exemplo, se o arquivo do Docker Compose for uma pasta chamada *DockerComposeFiles*, o arquivo Docker Compose deverá definir o contexto de compilação como ".." ou ".. /.. ", dependendo de onde ele é relativo à pasta da solução.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="15.0" Sdk="Microsoft.Docker.Sdk">
  <PropertyGroup Label="Globals">
    <ProjectVersion>2.1</ProjectVersion>
    <DockerTargetOS>Windows</DockerTargetOS>
    <ProjectGuid>154022c1-8014-4e9d-bd78-6ff46670ffa4</ProjectGuid>
    <DockerLaunchAction>LaunchBrowser</DockerLaunchAction>
    <DockerServiceUrl>{Scheme}://{ServiceIPAddress}{ServicePort}</DockerServiceUrl>
    <DockerServiceName>webapplication1</DockerServiceName>
    <DockerComposeBaseFilePath>DockerComposeFiles\mydockercompose</DockerComposeBaseFilePath>
    <AdditionalComposeFilePaths>AdditionalComposeFiles\myadditionalcompose.yml</AdditionalComposeFilePaths>
  </PropertyGroup>
  <ItemGroup>
    <None Include="DockerComposeFiles\mydockercompose.override.yml">
      <DependentUpon>DockerComposeFiles\mydockercompose.yml</DependentUpon>
    </None>
    <None Include="DockerComposeFiles\mydockercompose.yml" />
    <None Include=".dockerignore" />
  </ItemGroup>
</Project>
```

O arquivo *mydockercompose. yml* deve ter a seguinte aparência, com o contexto de compilação definido como o caminho relativo da pasta da solução (nesse caso, `..` ).

```yml
version: '3.4'

services:
  webapplication1:
    image: ${DOCKER_REGISTRY-}webapplication1
    build:
      context: ..
      dockerfile: WebApplication1\Dockerfile
```

> [!NOTE]
> DockerComposeBuildArguments, DockerComposeDownArguments e DockerComposeUpArguments são novos no Visual Studio 2019 versão 16,3.

## <a name="docker-compose-file-labels"></a>Docker Compose rótulos de arquivo

Você também pode substituir determinadas configurações colocando um arquivo chamado *Docker-Compose. vs. Debug. yml* (para a configuração de **depuração** ) ou *Docker-Compose. vs. Release. yml* (para a configuração de **versão** ) no mesmo diretório que o arquivo *Docker-Compose. yml* .  Nesse arquivo, você pode especificar as configurações da seguinte maneira:

```yml
services:
  webapplication1:
    labels:
      com.microsoft.visualstudio.debuggee.workingdirectory: "C:\\my_app_folder"
```

Use aspas duplas em volta dos valores, como no exemplo anterior, e use a barra invertida como um caractere de escape para barras invertidas em caminhos.

|Nome do rótulo|Descrição|
|----------|-----------|
|com. Microsoft. VisualStudio. Depurando. Arguments|Os argumentos passados para o programa ao iniciar a depuração. Para aplicativos .NET Core, esses argumentos normalmente são caminhos de pesquisa adicionais para pacotes NuGet seguidos pelo caminho para o assembly de saída do projeto.|
|com. Microsoft. VisualStudio. Depurando. killprogram|Esse comando é usado para parar o programa que está sendo depurado em execução dentro do contêiner (quando necessário).|
|com. Microsoft. VisualStudio. Depurando. programa|O programa foi iniciado ao iniciar a depuração. Para aplicativos .NET Core, essa configuração normalmente é **dotnet**.|
|com. Microsoft. VisualStudio. Depurando. WorkingDirectory|O diretório usado como o diretório inicial ao iniciar a depuração. Essa configuração normalmente é */app* para contêineres do Linux ou *C:\app* para contêineres do Windows.|

## <a name="customize-the-app-startup-process"></a>Personalizar o processo de inicialização do aplicativo

Você pode executar um comando ou script personalizado antes de iniciar seu aplicativo usando a `entrypoint` configuração e tornando-o dependente da configuração. Por exemplo, se você precisar configurar um certificado somente no modo de **depuração** executando `update-ca-certificates` , mas não no modo de **liberação** , poderá adicionar o código a seguir somente em *Docker-Compose. vs. Debug. yml*:

```yml
services:
  webapplication1:
    entrypoint: "sh -c 'update-ca-certificates && tail -f /dev/null'"
    labels:
      ...
```

Se você omitir *Docker-Compose. vs. Release. yml* ou *Docker-Compose. vs. Debug. yml* , o Visual Studio gerará um com base nas configurações padrão.

## <a name="next-steps"></a>Próximas etapas

Para obter informações sobre propriedades do MSBuild em geral, consulte [Propriedades do MSBuild](../msbuild/msbuild-properties.md).

## <a name="see-also"></a>Veja também

[Propriedades de compilação das ferramentas de contêiner](container-msbuild-properties.md)

[Configurações de inicialização das ferramentas de contêiner](container-launch-settings.md)

[Propriedades reservadas e conhecidas do MSBuild](../msbuild/msbuild-reserved-and-well-known-properties.md)

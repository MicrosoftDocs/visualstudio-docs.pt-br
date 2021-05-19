---
title: Docker Compose configurações de build
author: ghogen
description: Saiba como editar as propriedades Docker Compose build para personalizar como o Visual Studio cria e executa um Docker Compose aplicativo.
ms.custom: SEO-VS-2020
ms.author: ghogen
ms.date: 04/06/2021
ms.technology: vs-azure
ms.topic: reference
ms.openlocfilehash: b3744640aada798179c86cc60d2c8ce7b02ccfaa
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2021
ms.locfileid: "109973473"
---
# <a name="docker-compose-build-properties"></a>Docker Compose de build

Além das propriedades que controlam projetos individuais do Docker, descritas em Propriedades de [build](container-msbuild-properties.md)das Ferramentas de Contêiner, você também pode personalizar como o Visual Studio cria seus projetos Docker Compose definindo as propriedades Docker Compose que o MSBuild usa para criar sua solução. Você também pode controlar como o depurador Visual Studio executa seus aplicativos Docker Compose configurando rótulos de arquivo Docker Compose arquivos de configuração.

## <a name="how-to-set-the-msbuild-properties"></a>Como definir as propriedades do MSBuild

Para definir o valor de uma propriedade, edite o arquivo de projeto. Para Docker Compose propriedades, esse arquivo de projeto é aquele com uma extensão .dcproj, a menos que indicado de outra forma na tabela na próxima seção. Por exemplo, suponha que você queira especificar para iniciar o navegador ao iniciar a depuração. Você pode definir `DockerLaunchAction` a propriedade no arquivo de projeto .dcproj da seguinte forma.

```xml
<PropertyGroup>
   <DockerLaunchAction>LaunchBrowser</DockerLaunchAction>
</PropertyGroup>
```

Você pode adicionar a configuração de propriedade a um elemento existente ou, se `PropertyGroup` não houver um, crie um novo `PropertyGroup` elemento.

## <a name="docker-compose-msbuild-properties"></a>Propriedades do Docker Compose no MSBuild

A tabela a seguir mostra as propriedades do MSBuild disponíveis para Docker Compose projetos.

| Nome da propriedade | Location | Descrição | Valor padrão  |
|---------------|----------|-------------|----------------|
|AdditionalComposeFilePaths|dcproj|Especifica arquivos de composição adicionais em uma lista delimitada por ponto e vírgula a ser enviada para docker-compose.exe para todos os comandos. Caminhos relativos do arquivo de projeto docker-compose (dcproj) são permitidos.|-|
|DockerComposeBaseFilePath|dcproj|Especifica a primeira parte dos nomes de arquivo dos arquivos docker-compose, sem a *extensão .yml.* Por exemplo: <br>1. DockerComposeBaseFilePath = null/undefined: use o caminho *docker-compose* do arquivo base e os arquivos serão nomeados *docker-compose.yml* e *docker-compose.override.yml*.<br>2. DockerComposeBaseFilePath = *mydockercompose*: os arquivos serão nomeados *mydockercompose. yml* e *mydockercompose. Override. yml*.<br> 3. DockerComposeBaseFilePath = *.. \mydockercompose*: os arquivos terão um nível acima. |Docker-Compose|
|DockerComposeBuildArguments|dcproj|Especifica os parâmetros extras a serem passados para o `docker-compose build` comando. Por exemplo, `--parallel --pull`. |
|DockerComposeDownArguments|dcproj|Especifica os parâmetros extras a serem passados para o `docker-compose down` comando. Por exemplo, `--timeout 500`.|-|  
|DockerComposeProjectName| dcproj | Se especificado, substitui o nome do projeto para um projeto de composição do Docker. | "dockercompose" + hash gerado automaticamente |
|DockerComposeProjectPath|csproj ou vbproj|O caminho relativo para o arquivo de projeto do Docker-Compose (dcproj). Defina essa propriedade ao publicar o projeto de serviço para localizar as configurações de Build de imagem associadas armazenadas no arquivo Docker-Compose. yml.|-|
|DockerComposeProjectsToIgnore|dcproj| Especifica os projetos a serem ignorados pelas ferramentas de composição do Docker durante a depuração. Essa propriedade pode ser usada para qualquer projeto. Os caminhos de arquivo podem ser especificados de duas maneiras: <br> 1. Relativo a dcproj. Por exemplo, `<DockerComposeProjectsToIgnore>path\to\AngularProject1.csproj</DockerComposeProjectsToIgnore>`. <br> 2. Caminhos absolutos.<br> **Observação:** os caminhos devem ser separados pelo caractere delimidor `;` .|-|
|DockerComposeUpArguments|dcproj|Especifica os parâmetros extras a passar para o `docker-compose up` comando. Por exemplo, `--timeout 500`.|-|
|DockerDevelopmentMode| dcproj | Controla se o projeto de usuário é criado no contêiner. Os valores permitidos de **controle Rápido** **ou Regular** [quais estágios são construídos](https://aka.ms/containerfastmode) em um Dockerfile. A configuração de Depuração é o modo Rápido por padrão e o modo Regular, caso contrário. | Rápido |
|DockerLaunchAction| dcproj | Especifica a ação de lançamento a ser executar em F5 ou Ctrl+F5.  Os valores permitidos são None, LaunchBrowser e LaunchWCFTestClient. | Nenhum |
|DockerLaunchBrowser| dcproj | Indica se o navegador deve ser lançado. Ignorado se DockerLaunchAction for especificado. | Falso |
|DockerServiceName| dcproj| Se DockerLaunchAction ou DockerLaunchBrowser forem especificados, DockerServiceName especificará qual serviço referenciado no arquivo Docker-Compose será iniciado.|-|
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

## <a name="overriding-visual-studios-docker-compose-configuration"></a>Substituindo a configuração de Docker Compose do Visual Studio

Você pode substituir determinadas configurações colocando um arquivo chamado *Docker-Compose. vs. Debug. yml* (para o modo **rápido** ) ou *Docker-Compose. vs. Release. yml* (para o modo **normal** ) no mesmo diretório que o arquivo *Docker-Compose. yml* . 

>[!TIP] 
>Para descobrir os valores padrão para qualquer uma dessas configurações, examine *Docker-Compose. vs. Debug. g. yml* ou *Docker-Compose. vs. Release. g. yml*.

### <a name="docker-compose-file-labels"></a>Docker Compose rótulos de arquivo

 No *docker-compose.vs.debug.yml* ou *docker-compose.vs.release.yml,* você pode definir rótulos específicos de substituição da seguinte forma:

```yml
services:
  webapplication1:
    labels:
      com.microsoft.visualstudio.debuggee.workingdirectory: "C:\\my_app_folder"
```

Use aspas duplas em torno dos valores, como no exemplo anterior, e use a faixa invertida como um caractere de escape para malhas invertidas em caminhos.

|Nome do rótulo|Descrição|
|----------|-----------|
|com.microsoft.visualstudio.debuggee.arguments|Os argumentos passados para o programa ao iniciar a depuração. Para aplicativos .NET Core, esses argumentos normalmente são caminhos de pesquisa adicionais para pacotes NuGet seguidos pelo caminho para o assembly de saída do projeto.|
|com.microsoft.visualstudio.debuggee.program|O programa foi lançado ao iniciar a depuração. Para aplicativos .NET Core, essa configuração normalmente é **dotnet**.|
|com.microsoft.visualstudio.debuggee.workingdirectory|O diretório usado como o diretório inicial ao iniciar a depuração. Essa configuração normalmente é */app* para contêineres do Linux ou *C:\app* para contêineres do Windows.|
|com.microsoft.visualstudio.debuggee.killprogram|Esse comando é usado para interromper o programa de depuração que está sendo executado dentro do contêiner (quando necessário).|

### <a name="customize-the-docker-build-process"></a>Personalizar o processo de build do Docker

Você pode declarar qual estágio criar em seu Dockerfile usando a `target` configuração na `build` propriedade . Essa substituição pode ser usada apenas no *docker-compose.vs.debug.yml* ou *docker-compose.vs.release.yml* 

```yml
services:
  webapplication1:
    build:
      target: customStage
    labels:
      ...
```

### <a name="customize-the-app-startup-process"></a>Personalizar o processo de inicialização do aplicativo

Você pode executar um comando ou script personalizado antes de iniciar seu aplicativo usando a configuração `entrypoint` e tornando-o dependente do `DockerDevelopmentMode` . Por exemplo, se você precisar configurar  um certificado somente no modo Rápido executando , mas não no modo Regular, poderá adicionar o seguinte código somente `update-ca-certificates` em  *docker-compose.vs.debug.yml*: 

```yml
services:
  webapplication1:
    entrypoint: "sh -c 'update-ca-certificates && tail -f /dev/null'"
    labels:
      ...
```

## <a name="next-steps"></a>Próximas etapas

Para obter informações sobre as propriedades do MSBuild em geral, consulte [Propriedades do MSBuild.](../msbuild/msbuild-properties.md)

## <a name="see-also"></a>Confira também

[Propriedades de compilação das ferramentas de contêiner](container-msbuild-properties.md)

[Configurações de inicialização das ferramentas de contêiner](container-launch-settings.md)

[Gerenciar perfis de inicialização para Docker Compose no Visual Studio](launch-profiles.md)

[Propriedades reservadas e conhecidas do MSBuild](../msbuild/msbuild-reserved-and-well-known-properties.md)

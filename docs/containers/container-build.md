---
title: Visão geral de compilação e depuração das ferramentas de contêiner do Visual Studio
author: ghogen
description: Visão geral do processo de compilação e depuração das ferramentas de contêiner
ms.author: ghogen
ms.date: 11/20/2019
ms.technology: vs-azure
ms.topic: conceptual
ms.openlocfilehash: 004427ced7d18d9a5af5c863172416fd8637aa69
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536858"
---
# <a name="how-visual-studio-builds-containerized-apps"></a>Como o Visual Studio cria aplicativos em contêineres

Quer você esteja criando a partir do IDE do Visual Studio ou configurando uma compilação de linha de comando, você precisa saber como o Visual Studio usa o Dockerfile para criar seus projetos.  Por motivos de desempenho, o Visual Studio segue um processo especial para aplicativos em contêineres. Entender como o Visual Studio cria seus projetos é especialmente importante quando você personaliza o processo de compilação modificando o Dockerfile.

Quando o Visual Studio cria um projeto que não usa contêineres do Docker, ele invoca o MSBuild no computador local e gera os arquivos de saída em uma pasta (normalmente `bin` ) em sua pasta de solução local. No entanto, para um projeto em contêineres, o processo de compilação conta com as instruções do Dockerfile para criar o aplicativo em contêineres. O Dockerfile que o Visual Studio usa é dividido em vários estágios. Esse processo depende do recurso de Build de vários *estágios* do Docker.

## <a name="multistage-build"></a>Build de multiestágio

O recurso de compilação de vários estágios ajuda a tornar o processo de criação de contêineres mais eficiente e torna os contêineres menores, permitindo que eles contenham apenas os bits de que seu aplicativo precisa em tempo de execução. A compilação de vários estágios é usada para projetos do .NET Core, não .NET Framework projetos.

O Build de multiestágio permite que as imagens de contêiner sejam criadas em estágios que produzem imagens intermediárias. Como exemplo, considere um típico Dockerfile gerado pelo Visual Studio – o primeiro estágio é `base` :

```
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
```

As linhas no Dockerfile começam com a imagem Debian do mcr.microsoft.com (registro de contêiner da Microsoft) e criam uma imagem intermediária `base` que expõe as portas 80 e 443 e define o diretório de trabalho como `/app` .

O próximo estágio é `build` , que aparece da seguinte maneira:

```
FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["WebApplication43/WebApplication43.csproj", "WebApplication43/"]
RUN dotnet restore "WebApplication43/WebApplication43.csproj"
COPY . .
WORKDIR "/src/WebApplication43"
RUN dotnet build "WebApplication43.csproj" -c Release -o /app
```

Você pode ver que o `build` estágio inicia de uma imagem original diferente do registro ( `sdk` em vez de `aspnet` ), em vez de continuar da base.  A `sdk` imagem tem todas as ferramentas de compilação e, por esse motivo, é muito maior do que a imagem ASPNET, que contém apenas componentes de tempo de execução. O motivo para usar uma imagem separada fica claro quando você examina o restante do Dockerfile:

```
FROM build AS publish
RUN dotnet publish "WebApplication43.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication43.dll"]
```

O estágio final inicia novamente de `base` e inclui o `COPY --from=publish` para copiar a saída publicada para a imagem final. Esse processo possibilita que a imagem final seja muito menor, pois não precisa incluir todas as ferramentas de compilação que estavam na `sdk` imagem.

## <a name="building-from-the-command-line"></a>Criando a partir da linha de comando

Se você quiser criar fora do Visual Studio, poderá usar `docker build` ou `MSBuild` para criar a partir da linha de comando.

### <a name="docker-build"></a>docker build

Para criar uma solução em contêiner a partir da linha de comando, você geralmente pode usar o comando `docker build <context>` para cada projeto na solução. Você fornece o argumento de *contexto de compilação* . O *contexto de compilação* para um Dockerfile é a pasta no computador local que é usada como a pasta de trabalho para gerar a imagem. Por exemplo, é a pasta da qual você copia arquivos quando você copia para o contêiner.  Em projetos do .NET Core, use a pasta que contém o arquivo de solução (. sln).  Expresso como um caminho relativo, esse argumento normalmente é ".." para um Dockerfile em uma pasta de projeto e o arquivo de solução em sua pasta pai.  Para projetos .NET Framework, o contexto de compilação é a pasta do projeto, não a pasta da solução.

```cmd
docker build -f Dockerfile ..
```

### <a name="msbuild"></a>MSBuild

Dockerfiles criados pelo Visual Studio para projetos de .NET Framework (e para projetos do .NET Core criados com versões do Visual Studio anteriores ao Visual Studio 2017 atualização 4) não são Dockerfiles de vários estágios.  As etapas nesses Dockerfiles não compilam seu código.  Em vez disso, quando o Visual Studio cria um .NET Framework Dockerfile, ele primeiro compila seu projeto usando o MSBuild.  Quando isso for executado com sucesso, o Visual Studio criará o Dockerfile, que simplesmente copia a saída da compilação do MSBuild para a imagem do Docker resultante.  Como as etapas para compilar seu código não estão incluídas no Dockerfile, você não pode criar .NET Framework Dockerfiles usando `docker build` a partir da linha de comando. Você deve usar o MSBuild para compilar esses projetos.

Para criar uma imagem para um único projeto de contêiner do Docker, você pode usar o MSBuild com a `/t:ContainerBuild` opção de comando. Por exemplo:

```cmd
MSBuild MyProject.csproj /t:ContainerBuild /p:Configuration=Release
```

Você verá uma saída semelhante à que você vê na janela de **saída** ao compilar sua solução no IDE do Visual Studio. Sempre use `/p:Configuration=Release` , como nos casos em que o Visual Studio usa a otimização de compilação de multiestágio, os resultados na criação da configuração de **depuração** podem não ser conforme o esperado. Consulte [depuração](#debugging).

Se você estiver usando um projeto Docker Compose, use este comando para criar imagens:

```cmd
msbuild /p:SolutionPath=<solution-name>.sln /p:Configuration=Release docker-compose.dcproj
```

## <a name="project-warmup"></a>Aquecimento do projeto

O *projeto aquecimento* refere-se a uma série de etapas que ocorrem quando o perfil do Docker é selecionado para um projeto (ou seja, quando um projeto é carregado ou o suporte do Docker é adicionado) para melhorar o desempenho das execuções subsequentes (**F5** ou **Ctrl** + **F5**). Isso é configurável em **ferramentas**  >  **Opções**  >  **contêiner ferramentas**. Aqui estão as tarefas que são executadas em segundo plano:

- Verifique se o Docker Desktop está instalado e em execução.
- Verifique se o Docker Desktop está definido para o mesmo sistema operacional que o projeto.
- Efetuar pull das imagens no primeiro estágio do Dockerfile (o `base` estágio na maioria dos Dockerfiles).  
- Crie o Dockerfile e inicie o contêiner.

O aquecimento só acontecerá no modo **rápido** , portanto, o contêiner em execução terá a pasta de aplicativo montada em volume. Isso significa que qualquer alteração no aplicativo não invalidará o contêiner. Isso, portanto, melhora significativamente o desempenho da depuração e diminui o tempo de espera para tarefas de longa duração, como a extração de imagens grandes.

## <a name="volume-mapping"></a>Mapeamento de volume

Para que a depuração funcione em contêineres, o Visual Studio usa o mapeamento de volume para mapear as pastas do depurador e do NuGet do computador host. O mapeamento de volume é descrito na documentação do Docker [aqui](https://docs.docker.com/storage/volumes/). Aqui estão os volumes que são montados em seu contêiner:

|Volume|Descrição|
|-|-|
| **Depurador remoto** | Contém os bits necessários para executar o depurador no contêiner, dependendo do tipo de projeto. Isso é explicado em mais |detalhes na seção de [depuração](#debugging) .
| **Pasta do aplicativo** | Contém a pasta do projeto onde o Dockerfile está localizado.|
| **Pasta de origem** | Contém o contexto de compilação que é passado para comandos do Docker.|
| **Pastas de pacotes NuGet** | Contém os pacotes NuGet e as pastas de fallback que são lidas no arquivo *obj \{ projeto}. csproj. NuGet. g. props* no projeto. |

Para aplicativos Web ASP.NET Core, pode haver duas pastas adicionais para o certificado SSL e os segredos do usuário, que são explicados com mais detalhes na próxima seção.

## <a name="ssl-enabled-aspnet-core-apps"></a>Aplicativos ASP.NET Core habilitados para SSL

As ferramentas de contêiner no Visual Studio dão suporte à depuração de um aplicativo ASP.NET Core habilitado para SSL com um certificado de desenvolvimento, da mesma forma que você esperaria que ele funcionasse sem contêineres. Para fazer isso acontecer, o Visual Studio adiciona mais algumas etapas para exportar o certificado e disponibilizá-lo para o contêiner. Este é o fluxo que o Visual Studio manipula para você durante a depuração no contêiner:

1. Garante que o certificado de desenvolvimento local esteja presente e seja confiável no computador host por meio da `dev-certs` ferramenta.
2. Exporta o certificado para%APPDATA%\ASP.NET\Https com uma senha segura que é armazenada no repositório de segredos do usuário para este aplicativo específico.
3. Volume – monta os seguintes diretórios:

   - *%APPDATA%\Microsoft\UserSecrets*
   - *%APPDATA%\ASP.NET\Https*

ASP.NET Core procura um certificado que corresponda ao nome do assembly na pasta *https* , que é o motivo pelo qual ele é mapeado para o contêiner nesse caminho. O caminho e a senha do certificado podem ser definidos como alternativa usando variáveis de ambiente (ou seja, `ASPNETCORE_Kestrel__Certificates__Default__Path` e `ASPNETCORE_Kestrel__Certificates__Default__Password` ) ou no arquivo JSON de segredos do usuário, por exemplo:

```json
{
  "Kestrel": {
    "Certificates": {
      "Default": {
        "Path": "c:\\app\\mycert.pfx",
        "Password": "strongpassword"
      }
    }
  }
}
```

Se sua configuração der suporte a compilações em contêiner e não contêineras, você deverá usar as variáveis de ambiente, pois os caminhos são específicos para o ambiente de contêiner.

Para obter mais informações sobre como usar o SSL com aplicativos ASP.NET Core em contêineres, consulte [hospedando imagens ASP.NET Core com o Docker via HTTPS](/aspnet/core/security/docker-https)).

## <a name="debugging"></a>Depuração

Ao criar na configuração de **depuração** , há várias otimizações que o Visual Studio faz para ajudar com o desempenho do processo de compilação para projetos em contêineres. O processo de compilação para aplicativos em contêineres não é tão simples quanto a simples seguir as etapas descritas no Dockerfile. A criação de um contêiner é muito mais lenta do que a criação no computador local.  Portanto, quando você cria a configuração de **depuração** , o Visual Studio realmente cria seus projetos no computador local e compartilha a pasta de saída para o contêiner usando a montagem de volume. Uma compilação com essa otimização habilitada é chamada de compilação de modo *rápido* .

No modo **rápido** , o Visual Studio chama `docker build` um argumento que informa ao Docker para compilar apenas o `base` estágio.  O Visual Studio lida com o restante do processo sem considerar o conteúdo do Dockerfile. Portanto, quando você modifica seu Dockerfile, como para personalizar o ambiente de contêiner ou instalar dependências adicionais, você deve colocar suas modificações no primeiro estágio.  Todas as etapas personalizadas colocadas nos estágios do Dockerfile `build` , `publish` ou `final` não serão executadas.

Essa otimização de desempenho ocorre apenas quando você cria na configuração de **depuração** . Na configuração da **versão** , a compilação ocorre no contêiner, conforme especificado no Dockerfile.

Se você quiser desabilitar a otimização de desempenho e compilar como o Dockerfile especifica, defina a propriedade **ContainerDevelopmentMode** como **regular** no arquivo de projeto da seguinte maneira:

```xml
<PropertyGroup>
   <ContainerDevelopmentMode>Regular</ContainerDevelopmentMode>
</PropertyGroup>
```

Para restaurar a otimização de desempenho, remova a propriedade do arquivo de projeto.

 Quando você inicia a depuração (**F5**), um contêiner iniciado anteriormente é reutilizado, se possível. Se você não quiser reutilizar o contêiner anterior, poderá usar os comandos **recriar** ou **limpar** no Visual Studio para forçar o Visual Studio a usar um contêiner novo.

O processo de execução do depurador depende do tipo de projeto e do sistema operacional do contêiner:

|Cenário|Processo do depurador|
|-|-|
| **Aplicativos .NET Core (contêineres do Linux)**| O Visual Studio baixa `vsdbg` e mapeia-o para o contêiner, ele é chamado com seu programa e argumentos (ou seja, `dotnet webapp.dll` ) e, em seguida, o depurador é anexado ao processo. |
| **Aplicativos .NET Core (contêineres do Windows)**| O Visual Studio usa `onecoremsvsmon` e mapeia-o para o contêiner, executa-o como o ponto de entrada e, em seguida, o Visual Studio se conecta a ele e se anexa ao seu programa. Isso é semelhante a como você normalmente configuraria a depuração remota em outro computador ou máquina virtual.|
| **.NET Framework aplicativos** | O Visual Studio usa `msvsmon` e mapeia-o para o contêiner, executa-o como parte do ponto de entrada onde o Visual Studio pode se conectar a ele e anexa ao seu programa.|

Para obter informações sobre o `vsdbg.exe` , consulte [depuração offroad do .NET Core no Linux e OSX do Visual Studio](https://github.com/Microsoft/MIEngine/wiki/Offroad-Debugging-of-.NET-Core-on-Linux---OSX-from-Visual-Studio).

## <a name="container-entry-point"></a>Ponto de entrada do contêiner

O Visual Studio usa um ponto de entrada de contêiner personalizado dependendo do tipo de projeto e do sistema operacional do contêiner, aqui estão as diferentes combinações:

|Tipo de contêiner|Ponto de entrada|
|-|-|
| **Contêineres do Linux** | O ponto de entrada é `tail -f /dev/null` , que é uma espera infinita para manter o contêiner em execução. Quando o aplicativo é iniciado por meio do depurador, é o depurador que é responsável por executar o aplicativo (ou seja, `dotnet webapp.dll` ). Se for iniciado sem depuração, as ferramentas executarão um `docker exec -i {containerId} dotnet webapp.dll` para executar o aplicativo.|
| **Contêineres do Windows**| O ponto de entrada é algo como o `C:\remote_debugger\x64\msvsmon.exe /noauth /anyuser /silent /nostatus` que executa o depurador, portanto, ele está escutando conexões. O mesmo se aplica que o depurador execute o aplicativo e um `docker exec` comando quando iniciado sem depuração. Para .NET Framework aplicativos Web, o ponto de entrada é ligeiramente diferente, em que `ServiceMonitor` é adicionado ao comando.|

O ponto de entrada de contêiner só pode ser modificado em projetos de composição de Docker, não em projetos de contêiner único.

## <a name="next-steps"></a>Próximas etapas

Saiba como personalizar ainda mais suas compilações definindo propriedades adicionais do MSBuild em seus arquivos de projeto. Consulte [Propriedades do MSBuild para projetos de contêiner](container-msbuild-properties.md).

## <a name="see-also"></a>Confira também

[MSBuild](../msbuild/msbuild.md) 
 [Dockerfile no Windows](/virtualization/windowscontainers/manage-docker/manage-windows-dockerfile) 
 [Contêineres do Linux no Windows](/virtualization/windowscontainers/deploy-containers/linux-containers)

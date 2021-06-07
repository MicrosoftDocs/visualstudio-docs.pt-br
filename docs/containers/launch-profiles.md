---
title: Gerenciar perfis de lançamento para Docker Compose projetos
description: Saiba como usar perfis Docker Compose iniciar e controlar quais serviços são lançados quando você usa Docker Compose no Visual Studio.
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.devlang: dotnet
ms.topic: how-to
ms.date: 05/10/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: e740ea3b7950c14bf11522c4e438a105b09eb7f6
ms.sourcegitcommit: ab5735d64a6ad7aecabf5d6df159888e3246bff5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111433695"
---
# <a name="manage-launch-profiles-for-docker-compose"></a>Gerenciar perfis de lançamento para Docker Compose

Se você tiver um aplicativo que consiste em vários serviços e usa Docker Compose, poderá configurar quais serviços são executados e depurados criando ou editando um perfil de lançamento existente Docker Compose configurações de lançamento. Os perfis de lançamento permitem que você execute dinamicamente apenas os serviços que são importantes para seu cenário atual. Você pode criar e selecionar perfis de início para personalizar sua experiência de depuração e definir ações de lançamento específicas, como `Browser Launch URL` . Você também terá a opção de escolher cada serviço individualmente ou escolher um perfil de Docker Compose, que também analisa o arquivo Compose para determinar o grupo de serviços a ser executado.

Para obter informações sobre Docker Compose, consulte [Usando perfis com o Compose](https://docs.docker.com/compose/profiles/).
 
## <a name="prerequisites"></a>Pré-requisitos

- [Visual Studio 2019 versão 16.10](https://visualstudio.microsoft.com/vs/) ou posterior
- Uma solução com [Orquestração de Contêineres com Docker Compose](tutorial-multicontainer.md)

## <a name="manage-launch-settings"></a>Gerenciar configurações de lançamento

Considere o seguinte Docker Compose projeto no qual *o docker-compose.yml* tem cinco serviços e três perfis do Compose (web, web1 e web2).

```yml
version: '3.9'

services:
  webapplication1:
    image: ${DOCKER_REGISTRY-}webapplication1
    profiles: [web, web1]
    build:
      context: .
      dockerfile: WebApplication1/Dockerfile

  webapplication2:
    image: ${DOCKER_REGISTRY-}webapplication2
    profiles: [web, web2]
    build:
      context: .
      dockerfile: WebApplication2/Dockerfile

  webapplication3:
    image: ${DOCKER_REGISTRY-}webapplication3
    profiles: [web]
    build:
      context: .
      dockerfile: WebApplication3/Dockerfile

  external1:
    image: redis

  external2:
    image: redis

```

Há algumas opções para abrir a caixa de diálogo Docker Compose configurações de lançamento:
- No Visual Studio, escolha **Depurar**  >  **Gerenciar Docker Compose Configurações de Início:**

    ![Captura de tela do item de menu Gerenciar Configurações de Composição de Depuração](media/launch-settings/debug-dropdown-manage-compose.png)

- Clique com o botão direito do mouse no projeto Visual Studio `docker-compose` e selecione Gerenciar Docker Compose **configurações de início**

    ![Captura de tela do item de menu de contexto](media/launch-settings/launch-settings-context-menu.png)

- Use o Início Rápido (**Ctrl** Q ) e pesquise Docker Compose para encontrar + o comando mencionado acima. 

No exemplo a seguir, o perfil Compor é selecionado, que filtra a lista Serviços para apenas os três entre cinco `web1` incluídos nesse  perfil:

!["Captura de tela da caixa de diálogo configurações de lançamento"](media/launch-settings/launch-settings-create-profile.png)

A Docker Compose de perfis somente será exibida se houver perfis definidos nos arquivos *docker-compose.yml.*

O exemplo a seguir demonstra a seleção entre serviços individuais em vez de filtrar para os serviços em um perfil do Compose. Aqui, mostraremos a aparência da caixa de diálogo se você tiver criado um novo perfil de lançamento chamado que inicia apenas dois dos cinco serviços, com depuração e sem `test2` `webapplication1` `webapplication2` depuração.  Esse perfil de lançamento também inicia um navegador quando o aplicativo é iniciado e o abre no home page do `webapplication1` . 

![Captura de tela da caixa de diálogo de configurações de lançamento com alguns serviços desseletórios](media/launch-settings/launch-settings-selected.png)

E essas informações serão salvas em *launchSettings.json,* conforme mostrado abaixo

```json
{
    "profiles": {
      "test2": {
        "commandName": "DockerCompose",
        "composeLaunchServiceName": "webapplication1",
        "serviceActions": {
          "external1": "DoNotStart",
          "external2": "DoNotStart",
          "webapplication1": "StartDebugging",
          "webapplication2": "StartWithoutDebugging",
          "webapplication3": "DoNotStart"
        },
        "composeLaunchAction": "LaunchBrowser",
        "commandVersion": "1.0",
        "composeLaunchUrl": "{Scheme}://localhost:{ServicePort}"
      }
   }
}
```

## <a name="create-a-launch-profile-that-uses-a-docker-compose-profile"></a>Criar um perfil de lançamento que usa um Docker Compose perfil

Você também pode personalizar ainda mais os comportamentos de lançamento criando Visual Studio de lançamento que usam os perfis do Compose.

Para criar outro perfil que use o perfil do Compose, **selecione Usar Docker Compose perfis** e escolha `web1` . Agora, o perfil de lançamento inclui três serviços `webapplication1` – (que pertencem aos perfis `web` e `web1` Compose) e `external1` `external2` . Por padrão, os serviços sem código-fonte como e têm a `external1` ação padrão Iniciar sem  `external2` **depurar**. Os aplicativos .NET com código-fonte terão como padrão **Iniciar depuração.**

> [!IMPORTANT]
> Se um serviço não especificar um perfil do Compose, ele será incluído em todos os perfis do Compose implicitamente.

![Captura de tela da caixa de diálogo de configurações de lançamento com outro perfil criado](media/launch-settings/launch-settings-create-profile.png)

Essas informações serão salvas conforme mostrado no código a seguir. A configuração do serviço e sua ação padrão não são salvas, a menos que você altere a ação padrão.

```json
{
  "profiles": {
    "test1": {
      "commandName": "DockerCompose",
      "composeProfile": {
         "includes": [
            "web1"
         ]
      },
      "commandVersion": "1.0"
    }
  }
}
```

Você também pode alterar a ação de webapplication1 para **Iniciar sem depurar**. As configurações em *launchSettings.jsem seguida,* se parecem com o seguinte código:

```json
{
  "profiles": {
    "test1": {
        "commandName": "DockerCompose",
        "composeProfile": {
          "includes": [
              "web1"
              ],
          "serviceActions": {
              "webapplication1": "StartWithoutDebugging"
          }
        },
    "commandVersion": "1.0"
    }
  }
}
```

## <a name="properties"></a>Propriedades

Aqui está uma descrição de cada propriedade no *launchSettings.jsem*:

|Propriedade| Descrição|
| - | - |
|Commandname| Nome do comando. O padrão é "DockerCompose"|
|commandVersion| Número de versão usado para gerenciar o esquema do perfil de lançamento do DockerCompose.|
|composeProfile| Propriedade pai que define a definição do perfil de lançamento. Suas propriedades filho são `includes` e `serviceActions`|
|composeProfile – inclui | Lista de nomes de perfil do Compose que compõem um perfil de lançamento.|
|composeProfile – serviceActions | Lista os perfis, serviços e a ação de lançamento de cada serviço selecionados|
|serviceActions | Lista os serviços selecionados e a ação de lançamento.|
|composeLaunchServiceName| Se DockerLaunchAction ou DockerLaunchBrowser for especificado, DockerServiceName será o nome do serviço que deve ser lançado. Use essa propriedade para determinar qual serviço dentro do arquivo Docker Compose será lançado.|
|composeLaunchAction| Especifica a ação de lançamento a ser executar em **F5** ou **Ctrl** + **F5.** Os valores permitidos são None, LaunchBrowser e LaunchWCFTestClient.|
|composeLaunchUrl| A URL a ser usada ao iniciar o navegador. Os tokens de substituição válidos são "{ServiceIPAddress}", "{ServicePort}" e "{Scheme}". Por exemplo: {Scheme}://{ServiceIPAddress}:{ServicePort}|

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como as Ferramentas de Contêiner funcionam lendo Visual Studio de build e [depuração](container-build.md)das Ferramentas de Contêiner.

## <a name="see-also"></a>Confira também

- [Visual Studio configurações de início das Ferramentas de Contêiner](container-launch-settings.md)

- [Docker Compose configurações de build](docker-compose-properties.md)

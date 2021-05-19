---
title: Gerenciar perfis de inicialização para projetos de Docker Compose
description: Saiba como usar Docker Compose perfis de inicialização e controlar quais serviços são iniciados quando você usa Docker Compose no Visual Studio.
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.devlang: dotnet
ms.topic: how-to
ms.date: 05/10/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 003205525f883b010f897e6e47d4cab92a31b8a1
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2021
ms.locfileid: "110018489"
---
# <a name="manage-launch-profiles-for-docker-compose-preview"></a>Gerenciar perfis de inicialização para Docker Compose (versão prévia)

Se você tiver um aplicativo que consiste em vários serviços e usar Docker Compose, poderá configurar quais serviços são executados e depurados criando ou editando um perfil de inicialização existente nas configurações de inicialização Docker Compose. Os perfis de inicialização permitem que você execute dinamicamente apenas os serviços que são importantes para o seu cenário atual. Você pode criar e selecionar de perfis de inicialização para personalizar sua experiência de depuração e definir ações de inicialização específicas, como `Browser Launch URL` . Você também terá a opção de escolher cada serviço individualmente ou escolhendo um perfil de Docker Compose, que também examina seu arquivo de composição para determinar o grupo de serviços a serem executados.

Para obter informações sobre perfis de Docker Compose, consulte [usando perfis com o Compose](https://docs.docker.com/compose/profiles/).
 
## <a name="prerequisites"></a>Pré-requisitos

- [Visual Studio 2019 versão 16,10 Preview](https://visualstudio.microsoft.com/vs/preview/) ou posterior
- Uma solução com [orquestração de contêiner com Docker Compose](tutorial-multicontainer.md)

## <a name="manage-launch-settings"></a>Gerenciar configurações de inicialização

Considere o seguinte projeto de Docker Compose no qual o *Docker-Compose. yml* tem cinco serviços e três perfis de Compose (Web, web1 e web2).

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

Há algumas opções para abrir a caixa de diálogo Configurações de inicialização de Docker Compose:
- No Visual Studio, escolha **depurar**  >  **gerenciar Docker Compose configurações de inicialização**:

    ![Captura de tela do item de menu de configurações de composição de gerenciamento de depuração](media/launch-settings/debug-dropdown-manage-compose.png)

- Clique com o botão direito do mouse no projeto do Visual Studio `docker-compose` e selecione **gerenciar Docker Compose configurações de inicialização**

    ![Captura de tela do item de menu de contexto](media/launch-settings/launch-settings-context-menu.png)

- Use o início rápido (**Ctrl** + **Q**) e pesquise **Docker Compose** para localizar o comando mencionado anteriormente.

No exemplo abaixo, o `web1` perfil compor está selecionado, que filtra a lista de **Serviços** para apenas os três dos cinco incluídos nesse perfil:

!["Captura de tela da caixa de diálogo Configurações de inicialização"](media/launch-settings/launch-settings-create-profile.png)

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
|commandVersion| Número de versão usado para gerenciar o esquema do perfil de inicialização DockerCompose.|
|composeProfile| Propriedade pai que define a definição do perfil de inicialização. Suas propriedades filho são `includes` e `serviceActions`|
|composeProfile-inclui | Lista de nomes de perfil de composição que compõem um perfil de inicialização.|
|composeProfile-peractions | Lista os perfis de composição selecionados, os serviços e a ação de inicialização de cada serviço|
|Ações | Lista os serviços selecionados e a ação de inicialização.|
|composeLaunchServiceName| Se DockerLaunchAction ou DockerLaunchBrowser forem especificados, DockerServiceName será o nome do serviço que deve ser iniciado. Use essa propriedade para determinar qual serviço dentro do arquivo de Docker Compose será iniciado.|
|composeLaunchAction| Especifica a ação de inicialização a ser executada em **F5** ou **Ctrl** + **F5**. Os valores permitidos são None, LaunchBrowser e LaunchWCFTestClient.|
|composeLaunchUrl| A URL a ser usada ao iniciar o navegador. Os tokens de substituição válidos são "{ServiceIPAddress}", "{ServicePort}" e "{Scheme}". Por exemplo: {Scheme}://{ServiceIPAddress}:{ServicePort}|

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como as Ferramentas de Contêiner funcionam lendo Visual Studio de build e [depuração](container-build.md)das Ferramentas de Contêiner.

## <a name="see-also"></a>Confira também

- [Visual Studio configurações de início das Ferramentas de Contêiner](container-launch-settings.md)

- [Docker Compose configurações de build](docker-compose-properties.md)

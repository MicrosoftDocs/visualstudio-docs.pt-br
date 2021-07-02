---
title: 'Tutorial do Docker-parte 7: usar Docker Compose'
description: Descreve como instalar e usar Docker Compose.
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 645d168aefe05040193d564d5c158acfb6688c11
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222741"
---
# <a name="use-docker-compose"></a>Como usar o Docker Compose

[Docker Compose](https://docs.docker.com/compose/) é uma ferramenta desenvolvida para ajudar a definir e compartilhar aplicativos com vários contêineres. Com o Compose, você pode criar um arquivo YAML para definir os serviços e com um único comando, pode girar tudo ou desmontar tudo isso.

A *grande* vantagem de usar o Compose é que você pode definir a pilha de aplicativos em um arquivo, mantê-lo na raiz do seu repositório de projetos (agora é controlado por versão) e permitir que outra pessoa contribua com facilidade para o seu projeto. Alguém precisaria apenas clonar seu repositório e iniciar o aplicativo de composição. na verdade, você pode ver alguns projetos em GitHub/GitLab fazendo exatamente isso agora.

Então, como começar?

## <a name="install-docker-compose"></a>Instalar o Docker Compose

se você instalou o docker Desktop para Windows ou Mac, você já tem Docker Compose! As instâncias de Play com Docker já têm o Docker Compose instalado também. Se você estiver em um computador Linux, será necessário instalar Docker Compose usando [as instruções aqui](https://docs.docker.com/compose/install/).

Após a instalação, você deve ser capaz de executar o seguinte e ver as informações de versão.

```bash
docker-compose version
```

## <a name="create-the-compose-file"></a>Criar o arquivo de composição

1. Na raiz do projeto de aplicativo, crie um arquivo chamado `docker-compose.yml` .

1. No arquivo de composição, começaremos definindo a versão do esquema. Na maioria dos casos, é melhor usar a versão mais recente com suporte. Você pode examinar a [referência de arquivo de composição](https://docs.docker.com/compose/compose-file/) para as versões de esquema atuais e a matriz de compatibilidade.

    ```yaml
    version: "3.7"
    ```

1. Em seguida, defina a lista de serviços (ou contêineres) que você deseja executar como parte do seu aplicativo.

    ```yaml hl_lines="3"
    version: "3.7"

    services:
    ```

E agora, você começará a migrar um serviço por vez para o arquivo de composição.

## <a name="define-the-app-service"></a>Definir o serviço de aplicativo

Para se lembrar, esse foi o comando usado para definir o contêiner do aplicativo (substitua os ` \ ` caracteres por `` ` `` em Windows PowerShell).

```bash
docker run -dp 3000:3000 \
  -w /app -v ${PWD}:/app \
  --network todo-app \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=secret \
  -e MYSQL_DB=todos \
  node:12-alpine \
  sh -c "yarn install && yarn run dev"
```

1. Primeiro, defina a entrada de serviço e a imagem para o contêiner. Você pode escolher qualquer nome para o serviço. O nome se tornará automaticamente um alias de rede, que será útil ao definir o serviço MySQL.

    ```yaml hl_lines="4 5"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
    ```

1. Normalmente, você verá o comando próximo à `image` definição, embora não haja nenhum requisito de ordenação. Então, vá em frente e mova-o para o arquivo.

    ```yaml hl_lines="6"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
    ```

1. Migre a `-p 3000:3000` parte do comando definindo o `ports` para o serviço. Você usará a [sintaxe curta](https://docs.docker.com/compose/compose-file/#short-syntax-1) aqui, mas também há uma [sintaxe longa](https://docs.docker.com/compose/compose-file/#long-syntax-1) mais detalhada disponível também.

    ```yaml hl_lines="7 8"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
    ```

1. Em seguida, migre o diretório de trabalho ( `-w /app` ) e o mapeamento de volume ( `-v ${PWD}:/app` ) usando `working_dir` as `volumes` definições e. Os volumes também têm uma sintaxe [curta](https://docs.docker.com/compose/compose-file/#short-syntax-3) e [longa](https://docs.docker.com/compose/compose-file/#long-syntax-3) .

   Uma vantagem de Docker Compose definições de volume é que você pode usar caminhos relativos do diretório atual.

    ```yaml hl_lines="9 10 11"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
        working_dir: /app
        volumes:
          - ./:/app
    ```

1. Por fim, migre as definições de variável de ambiente usando a `environment` chave.

    ```yaml hl_lines="12 13 14 15 16"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
        working_dir: /app
        volumes:
          - ./:/app
        environment:
          MYSQL_HOST: mysql
          MYSQL_USER: root
          MYSQL_PASSWORD: secret
          MYSQL_DB: todos
    ```

### <a name="define-the-mysql-service"></a>Definir o serviço MySQL

Agora, é hora de definir o serviço MySQL. O comando que você usou para esse contêiner foi o seguinte (substitua os ` \ ` caracteres por `` ` `` em Windows PowerShell):

```bash
docker run -d \
  --network todo-app --network-alias mysql \
  -v todo-mysql-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=secret \
  -e MYSQL_DATABASE=todos \
  mysql:5.7
```

1. Primeiro, defina o novo serviço e nomeie-o `mysql` para que ele obtenha automaticamente o alias de rede. Especifique a imagem a ser usada também.

    ```yaml hl_lines="6 7"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
    ```

1. Em seguida, defina o mapeamento de volume. Quando você executou o contêiner com `docker run` , o volume nomeado foi criado automaticamente. No entanto, isso não acontece ao executar with compor. Você precisa definir o volume na seção de nível superior `volumes:` e, em seguida, especificar o mountpoint na configuração do serviço. Ao simplesmente fornecer apenas o nome do volume, as opções padrão são usadas. No entanto, há [muitas outras opções disponíveis](https://github.com/compose-spec/compose-spec/blob/master/spec.md#volumes-top-level-element) .

    ```yaml hl_lines="8 9 10 11 12"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
        volumes:
          - todo-mysql-data:/var/lib/mysql
    
    volumes:
      todo-mysql-data:
    ```

1. Por fim, você só precisa especificar as variáveis de ambiente.

    ```yaml hl_lines="10 11 12"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
        volumes:
          - todo-mysql-data:/var/lib/mysql
        environment: 
          MYSQL_ROOT_PASSWORD: secret
          MYSQL_DATABASE: todos
    
    volumes:
      todo-mysql-data:
    ```

Neste ponto, o completo `docker-compose.yml` deve ter a seguinte aparência:

```yaml
version: "3.7"

services:
  app:
    image: node:12-alpine
    command: sh -c "yarn install && yarn run dev"
    ports:
      - 3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: secret
      MYSQL_DB: todos

  mysql:
    image: mysql:5.7
    volumes:
      - todo-mysql-data:/var/lib/mysql
    environment: 
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: todos

volumes:
  todo-mysql-data:
```

## <a name="run-the-application-stack"></a>Executar a pilha de aplicativos

Agora que você tem o `docker-compose.yml` arquivo, você pode iniciá-lo!

1. Primeiro, certifique-se de que nenhuma outra cópia do aplicativo e do banco de dados esteja em execução ( `docker ps` e `docker rm -f <ids>` ).

1. Inicie a pilha de aplicativos usando o `docker-compose up` comando. Adicione o `-d` sinalizador para executar tudo em segundo plano. como alternativa, você pode clicar com o botão direito do mouse no arquivo de composição e selecionar a opção **compor** para a barra lateral de VS Code. 

    ```bash
    docker-compose up -d
    ```

    Ao executar isso, você deverá ver uma saída como esta:

    ```plaintext
    Creating network "app_default" with the default driver
    Creating volume "app_todo-mysql-data" with default driver
    Creating app_app_1   ... done
    Creating app_mysql_1 ... done
    ```

    Você observará que o volume foi criado, bem como uma rede! Por padrão, o Docker Compose cria automaticamente uma rede especificamente para a pilha de aplicativos (motivo pelo qual você não definiu um no arquivo de composição).

1. Examine os logs usando o `docker-compose logs -f` comando. Você verá os logs de cada um dos serviços intercalados em um único fluxo. Isso é incrivelmente útil quando você deseja observar problemas relacionados a tempo. O `-f` sinalizador "segue" o log, portanto, dará a você a saída ao vivo à medida que ele é gerado.

    Se você ainda não fez isso, verá uma saída parecida com esta:

    ```plaintext
    mysql_1  | 2019-10-03T03:07:16.083639Z 0 [Note] mysqld: ready for connections.
    mysql_1  | Version: '5.7.27'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)
    app_1    | Connected to mysql db at host mysql
    app_1    | Listening on port 3000
    ```

    O nome do serviço é exibido no início da linha (geralmente colorido) para ajudar a distinguir mensagens. Se você quiser exibir os logs de um serviço específico, poderá adicionar o nome do serviço ao final do comando logs (por exemplo, `docker-compose logs -f app` ).

    > [!TIP]
    > **Aguardando o banco de BD antes de iniciar o aplicativo** Quando o aplicativo está sendo inicializado, na verdade ele fica e aguarda que o MySQL fique ativo e pronto antes de tentar se conectar ao it.DocKer não tem suporte interno para aguardar que outro contêiner esteja totalmente ativo, em execução e pronto antes de iniciar outro contêiner. Para projetos baseados em nó, você pode usar a dependência de [porta de espera](https://github.com/dwmkerr/wait-port) . Existem projetos semelhantes para outras linguagens/estruturas.

1. Neste ponto, você deve ser capaz de abrir seu aplicativo e vê-lo em execução. E Ei! Você está pronto para um único comando!

## <a name="see-the-app-stack-in-the-docker-extension"></a>Consulte a pilha de aplicativos na extensão do Docker

Se você examinar a extensão do Docker, poderá alterar as opções de agrupamento usando ' engrenagem ' e ' Group by '. nessa instância, você deseja ver os contêineres agrupados por nome de Project de composição:

![Extensão VS com Compose](media/vs-app-project-collapsed.png)

Se você torcer a rede, verá os dois contêineres que você definiu no arquivo de composição.

![Extensão VS com Compose expandida](media/vs-app-project-expanded.png)

## <a name="tear-it-all-down"></a>Desmontar tudo

quando estiver pronto para desmontar tudo, basta executar `docker-compose down` ou clicar com o botão direito do mouse no aplicativo na lista contêineres na extensão VS Code docker e selecionar **compor**. Os contêineres serão interrompidos e a rede será removida.

> [!WARNING]
> **Removendo volumes** Por padrão, os volumes nomeados no arquivo de composição não são removidos durante a execução `docker-compose down` . Se você quiser remover os volumes, será necessário adicionar o `--volumes` sinalizador.

Depois de interrompida, você pode alternar para outro projeto, executar `docker-compose up` e estar pronto para contribuir para o projeto! Na verdade, ele não fica muito mais simples do que isso!

## <a name="recap"></a>Recapitulação

Nesta seção, você aprendeu sobre Docker Compose e como ele ajuda a simplificar drasticamente a definição e o compartilhamento de aplicativos de vários serviços. Você criou um arquivo de composição traduzindo os comandos que você estava usando no formato de composição apropriado.

Neste ponto, você está começando a concluir o tutorial. No entanto, há algumas práticas recomendadas sobre a criação de imagens a serem abordadas, pois há um grande problema com o Dockerfile que você esteve usando. Vamos dar uma olhada!

## <a name="next-steps"></a>Próximas etapas

Continue com o tutorial!

> [!div class="nextstepaction"]
> [Práticas recomendadas de criação de imagem](image-building-best-practices.md)

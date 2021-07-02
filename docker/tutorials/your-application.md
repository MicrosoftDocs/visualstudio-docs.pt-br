---
title: 'Tutorial do Docker-parte 1: compilar e executar o aplicativo de exemplo de lista de tarefas'
description: Visão geral do aplicativo de exemplo de lista de tarefas que é executado no Node.js.
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 9229c3717b686a3f08ef49e7912ac0515864d793
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222806"
---
# <a name="build-and-run-the-todo-sample-app"></a>Compilar e executar o aplicativo de exemplo todo

Para o restante deste tutorial, você trabalhará com um Gerenciador de lista de tarefas simples em execução no Node.js. Se você não estiver familiarizado com Node.js, não se preocupe! Nenhuma experiência real de JavaScript é necessária!

Neste ponto, sua equipe de desenvolvimento é bem pequena e você está simplesmente criando um aplicativo para provar seu MVP (produto viável mínimo). Você quer mostrar como ele funciona e o que ele é capaz de fazer sem a necessidade de pensar em como ele funcionará para uma equipe grande, vários desenvolvedores e assim por diante.

![Captura de tela todo do Gerenciador de lista](media/todo-list-sample.png)

## <a name="get-the-app"></a>Obtenha o aplicativo

Antes de executar o aplicativo, você precisa obter o código-fonte do aplicativo em seu computador. Para projetos reais, você normalmente clonará o repositório. Mas, para este tutorial, criamos um arquivo ZIP que contém o aplicativo.

1. verifique se você tem o Docker for Windows ou o docker Community Edition instalado no computador local. consulte [Docker for Windows documentação de instalação](https://docs.docker.com/docker-for-windows/install/). O processo de instalação torna o arquivo ZIP contendo o exemplo disponível no endereço localhost.

1. Baixe a origem do aplicativo do repositório do [Docker](https://github.com/docker/getting-started) . Você pode baixar o arquivo ZIP para o repositório. Para baixar o arquivo ZIP, use o botão **código** verde e escolha **baixar zip**. Abra o arquivo ZIP e Extraia todos para extrair a origem do aplicativo da pasta do *aplicativo* para uma pasta no disco rígido.

   ![Captura de tela mostrando o botão de código verde e a opção de baixar ZIP](media/download-zip.png)

1. Depois de extraído, use seu editor de código favorito para abrir o projeto. se você for precisar de um editor, poderá usar [Visual Studio Code](https://code.visualstudio.com/). Você deve ver o `package.json` e dois subdiretórios ( `src` e `spec` ).

    ![captura de tela de Visual Studio Code aberta com o aplicativo carregado](media/ide-screenshot.png)

## <a name="building-the-apps-container-image"></a>Criando a imagem de contêiner do aplicativo

Para criar o aplicativo, você precisa usar um `Dockerfile` . Um Dockerfile é simplesmente um script de instruções baseado em texto que é usado para criar uma imagem de contêiner. Se você tiver criado o Dockerfiles antes, poderá ver algumas falhas na Dockerfile abaixo. Mas não se preocupe! Vamos passar por eles.

1. Crie um arquivo chamado `Dockerfile` na mesma pasta que o arquivo `package.json` com o conteúdo a seguir.

    ```dockerfile
    FROM node:12-alpine
    WORKDIR /app
    COPY . .
    RUN yarn install --production
    CMD ["node", "/app/src/index.js"]
    ```

    Verifique se o arquivo `Dockerfile` não tem nenhuma extensão de arquivo como `.txt` . Alguns editores podem acrescentar essa extensão de arquivo automaticamente e isso resultaria em um erro na próxima etapa.

1. Se você ainda não tiver feito isso, abra um terminal e vá para o `app` diretório com o `Dockerfile` . Agora, crie a imagem de contêiner usando o `docker build` comando.

    ```bash
    docker build -t getting-started .
    ```

    Como alternativa, você também pode clicar com o botão direito do mouse no Dockerfile e escolher **Compilar imagem...** e, em seguida, especificar a marca no prompt.

    Esse comando usou o Dockerfile para criar uma nova imagem de contêiner. Talvez você tenha notado que muitas "camadas" foram baixadas. Isso ocorre porque você instruiu o construtor que desejava iniciar a partir da `node:12-alpine` imagem. Mas, como você não tinha isso em seu computador, essa imagem precisava ser baixada.

    Depois que a imagem foi baixada, você copiou em seu aplicativo e usou `yarn` para instalar as dependências do aplicativo. A `CMD` diretiva especifica o comando padrão a ser executado ao iniciar um contêiner a partir desta imagem.

    Por fim, o `-t` sinalizador marca sua imagem. Imagine isso simplesmente como um nome legível para a imagem final. Como você nomeou a imagem `getting-started` , pode consultar essa imagem ao executar um contêiner.

    O `.` no final do `docker build` comando informa que o Docker deve procurar o `Dockerfile` no diretório atual.

## <a name="starting-an-app-container"></a>Iniciando um contêiner de aplicativo

Agora que você tem uma imagem, execute o aplicativo! Para fazer isso, use o `docker run` comando (Lembre-se de que de antes?).

1. Inicie o contêiner usando o `docker run` comando e especifique o nome da imagem que você acabou de criar:

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

    Lembra dos `-d` `-p` sinalizadores e? Você está executando o novo contêiner no modo "desanexado" (em segundo plano) e criando um mapeamento entre a porta 3000 do host para a porta 3000 do contêiner. Sem o mapeamento de porta, você não poderá acessar o aplicativo.

1. Depois de alguns segundos, abra o navegador da Web para [http://localhost:3000](http://localhost:3000) .
    Você deve ver o aplicativo!

    ![Lista de tarefas vazia](media/todo-list-empty.png)

1. Vá em frente e adicione um ou dois itens e veja que ele funciona conforme o esperado. Você pode marcar itens como concluídos e remover itens. O front-end está armazenando os itens no back-end com êxito! Muito rápido e fácil, não é?

Neste ponto, você deve ter um gerente de lista de tarefas em execução com alguns itens, todos criados por você! Agora, vamos fazer algumas alterações e aprender sobre o gerenciamento de seus contêineres.

se você olhar rapidamente a extensão de VS Code, verá que os dois contêineres estão em execução agora (este tutorial e seu contêiner de aplicativo iniciado recentemente)!

![Extensão do Docker com tutorial e contêineres de aplicativo em execução](media/vs-two-containers.png)

## <a name="recap"></a>Recapitulação

Nesta seção curta, você aprendeu as noções básicas sobre a criação de uma imagem de contêiner e criou um Dockerfile para fazer isso. Depois de criar uma imagem, você iniciou o contêiner e viu o aplicativo em execução!

Em seguida, você fará uma modificação no aplicativo e aprenderá a atualizar o aplicativo em execução com uma nova imagem. Ao longo do caminho, você aprenderá alguns outros comandos úteis.

## <a name="next-steps"></a>Próximas etapas

Continue com o tutorial!

> [!div class="nextstepaction"]
> [Atualizando seu aplicativo](update-your-app.md)

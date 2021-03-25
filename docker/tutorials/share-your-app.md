---
title: 'Tutorial do Docker-parte 3: compartilhar seu aplicativo'
description: Descreve como compartilhar imagens do Docker usando o registro do Hub do Docker.
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: ad9f7d329bf00e3fadd665cefea22a2301fdf695
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061778"
---
# <a name="share-your-app"></a>Compartilhar seu aplicativo

Agora que criamos uma imagem, vamos compartilhar! Para compartilhar imagens do Docker, você precisa usar um registro do Docker. O registro padrão é o Hub do Docker e é onde vêm todas as imagens que usamos.

## <a name="create-a-repo"></a>Criar um repositório

Para enviar uma imagem por push, primeiro, você precisa criar um repositório no Hub do Docker.

1. Vá para o [Hub do Docker](https://hub.docker.com/signup/msftedge?utm_source=msftedge) e faça logon se necessário.

1. Clique no botão **criar repositório** .

1. Para o nome do repositório, use `getting-started` . Verifique se a visibilidade é `Public` .

1. Clique no botão **criar** !

Se você olhar o lado direito da página, verá uma seção chamada **comandos do Docker**. Isso fornece um comando de exemplo que será necessário executar para enviar por push para este repositório.

![Comando Docker com exemplo de push](media/push-command.png)

## <a name="push-the-image"></a>Enviar a imagem por push

1. Na linha de comando, tente executar o comando push que você vê no Hub do Docker. Observe que o comando usará o namespace, não o "Docker".

    ```plaintext
    $ docker push docker/getting-started
    The push refers to repository [docker.io/docker/getting-started]
    An image does not exist locally with the tag: docker/getting-started
    ```

    Por que houve falha? O comando Push estava procurando uma imagem chamada Docker/Getting-Started, mas não encontrou uma. Se você executar `docker image ls` o, não verá um.

    Para corrigir isso, você precisa "marcar" sua imagem existente que criamos para dar outro nome.

1. Entre no Hub do Docker usando o comando `docker login -u <username>` .

1. Use o `docker tag` comando para dar `getting-started` um novo nome à imagem. Não deixe de alternar `<username>` com a ID do Docker.

    ```bash
    docker tag getting-started <username>/getting-started
    ```

1. Agora, tente o comando Push novamente. Se você estiver copiando o valor do Hub do Docker, poderá descartar a `tagname` parte, pois não adicionou uma marca ao nome da imagem. Se você não especificar uma marca, o Docker usará uma marca chamada `latest` .

    ```bash
    docker push <username>/getting-started
    ```

    Em vez da linha de comando, você também pode clicar com o botão direito do mouse na marca da imagem na seção **imagens** do modo de exibição do Docker e escolher **enviar por push...** e, em seguida, escolher **conectar registro...** e Hub do **Docker**.

## <a name="run-the-image-on-a-new-instance"></a>Executar a imagem em uma nova instância

Agora que sua imagem foi criada e enviada por push para um registro, tente executar o aplicativo em uma nova instância do que nunca viu essa imagem de contêiner! Para fazer isso, você usará o play com o Docker.

1. Abra o navegador para [brincar com o Docker](http://play-with-docker.com).

1. Entre com sua conta do Hub do Docker.

1. Quando você estiver conectado, clique no link "+ Adicionar nova instância" na barra do lado esquerdo. (Se você não o vir, torne seu navegador um pouco mais largo.) Depois de alguns segundos, uma janela de terminal será aberta no navegador.

    ![Reproduzir com o Docker Adicionar nova instância](media/pwd-add-new-instance.png)

1. No terminal, inicie seu aplicativo enviado por push recentemente.

    ```bash
    docker run -dp 3000:3000 <username>/getting-started
    ```

    Você deve ver a imagem ser retirada e, eventualmente, iniciar!

1. Clique na notificação 3000 quando ela aparecer e você deverá ver o aplicativo com suas modificações! Alegria! Se o emblema 3000 não aparecer, você poderá clicar no botão **abrir porta** e digitar 3000.

## <a name="recap"></a>Recapitulação

Nesta seção, você aprendeu a compartilhar imagens enviando-as por push para um registro. Em seguida, você passou para uma instância totalmente nova e conseguiu executar a imagem enviada por push recentemente. Isso é muito comum em pipelines de CI, em que o pipeline criará a imagem e a enviará por push para um registro e, em seguida, o ambiente de produção poderá usar a versão mais recente da imagem.

Agora que isso foi descoberto, lembre-se de que no final da última seção, quando você reiniciou o aplicativo, perdeu todos os itens da lista de tarefas. Obviamente, isso não é uma excelente experiência do usuário, então você aprenderá a seguir como você pode manter os dados entre as reinicializações!

## <a name="next-steps"></a>Próximas etapas

Continue com o tutorial!

> [!div class="nextstepaction"]
> [Persistindo seu banco de dados](persist-your-data.md)

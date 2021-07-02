---
title: 'Tutorial do Docker – Parte 3: Compartilhar seu aplicativo'
description: Descreve como compartilhar imagens do Docker usando o Docker Hub registro.
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: d64d10c7abefc14f31c39c3b8397e95cec67e9f4
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222780"
---
# <a name="share-your-app"></a>Compartilhar seu aplicativo

Agora que fizemos uma imagem, vamos compartilhá-la! Para compartilhar imagens do Docker, você precisa usar um registro do Docker. O registro padrão é Docker Hub e é de onde todas as imagens usadas foram fornecidas.

## <a name="create-a-repo"></a>Criar um repo

Para fazer push de uma imagem, primeiro, você precisa criar um Docker Hub.

1. Vá para [Docker Hub](https://hub.docker.com/signup/msftedge?utm_source=msftedge) e faça logoff, se necessário.

1. Clique no **botão Criar Repositório.**

1. Para o nome do repo, use `getting-started` . Certifique-se de que a Visibilidade seja `Public` .

1. Clique no **botão** Criar!

Se você procurar no lado direito da página, verá uma seção chamada **Comandos do Docker**. Isso fornece um exemplo de comando que você precisará executar para fazer push para esse repo.

![Comando do Docker com exemplo de push](media/push-command.png)

## <a name="push-the-image"></a>Enviar a imagem por push

1. Na linha de comando, tente executar o comando push que você vê no Docker Hub. Observe que o comando estará usando seu namespace, não "docker".

    ```plaintext
    $ docker push docker/getting-started
    The push refers to repository [docker.io/docker/getting-started]
    An image does not exist locally with the tag: docker/getting-started
    ```

    Por que ele falhou? O comando push estava procurando uma imagem chamada docker/getting-started, mas não encontrou uma. Se você `docker image ls` executar , também não verá um.

    Para corrigir isso, você precisa "marcar" sua imagem existente criada para dar a ela outro nome.

1. Entre no Docker Hub usando o comando `docker login -u <username>` .

1. Use o `docker tag` comando para dar um novo nome à `getting-started` imagem. Certifique-se de trocar `<username>` com sua ID do Docker.

    ```bash
    docker tag getting-started <username>/getting-started
    ```

1. Agora, tente o comando push novamente. Se você estiver copiando o valor de Docker Hub, poderá soltar a parte, pois não adicionou uma `tagname` marca ao nome da imagem. Se você não especificar uma marca, o Docker usará uma marca chamada `latest` .

    ```bash
    docker push <username>/getting-started
    ```

    Em vez da linha de comando, você também pode  clicar com o botão direito do mouse na marca de imagem na seção Imagens da exibição do Docker e escolher **Push...** e, em seguida, escolher **Conexão Registro...** e, em **seguida,** Docker Hub .

## <a name="run-the-image-on-a-new-instance"></a>Executar a imagem em uma nova instância

Agora que sua imagem foi criada e esguia em um registro, tente executar o aplicativo em uma nova instância que nunca viu essa imagem de contêiner! Para fazer isso, você usará o Play with Docker.

1. Abra o navegador para [Reproduzir com o Docker.](http://play-with-docker.com)

1. Entre com sua conta Docker Hub conta.

1. Quando você estiver conectado, clique no link "+ ADICIONAR NOVA INSTÂNCIA" na barra do lado esquerdo. (Se você não o vir, faça com que seu navegador seja um pouco mais amplo.) Após alguns segundos, uma janela de terminal será aberta no navegador.

    ![Reproduzir com o Docker adicionar nova instância](media/pwd-add-new-instance.png)

1. No terminal, inicie seu aplicativo recém-pressionado.

    ```bash
    docker run -dp 3000:3000 <username>/getting-started
    ```

    Você deve ver a imagem ser retirada e, eventualmente, iniciar!

1. Clique no selo 3000 quando ele aparecer e você deverá ver o aplicativo com suas modificações! Viva! Se o selo 3000 não aparecer, você  poderá clicar no botão Abrir Porta e digitar 3000.

## <a name="recap"></a>Recapitulação

Nesta seção, você aprendeu a compartilhar imagens e a esvasá-las para um registro. Em seguida, você foi para uma nova instância e conseguiu executar a imagem recém-pressionada. Isso é muito comum em pipelines de CI, em que o pipeline criará a imagem e a por pushá para um registro e, em seguida, o ambiente de produção poderá usar a versão mais recente da imagem.

Agora que você descobriu isso, lembre-se de que, no final da última seção, ao reiniciar o aplicativo, você perdeu todos os itens da lista de itens de todo o trabalho. Obviamente, essa não é uma ótima experiência do usuário, portanto, você aprenderá a seguir como persistir os dados entre as reinicializações!

## <a name="next-steps"></a>Próximas etapas

Continue com o tutorial!

> [!div class="nextstepaction"]
> [Persistir seu banco de dados](persist-your-data.md)

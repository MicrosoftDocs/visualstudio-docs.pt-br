---
title: 'Tutorial do Docker-parte 4: manter seus dados'
description: Saiba como manter os dados em um banco e compartilhar diretórios em um contêiner montando um volume.
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: c9408e099caaef097be3fc4eea26cee2b1889e8e
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222897"
---
# <a name="persist-your-data"></a> Manter seus dados

Caso você não tenha notado, a lista de tarefas pendentes será apagada todas as vezes que você iniciar o contêiner. Por que é isso? Vamos nos aprofundar em como o contêiner está funcionando.

## <a name="the-containers-filesystem"></a>O sistema de arquivos do contêiner

Quando um contêiner é executado, ele usa as várias camadas de uma imagem para seu sistema de arquivos. Cada contêiner também obtém seu próprio "espaço transitório" para criar, atualizar ou remover arquivos. As alterações não serão vistas em outro contêiner, *mesmo se* estiverem usando a mesma imagem.

### <a name="see-this-in-practice"></a>Veja isso na prática

Para ver isso em ação, você vai iniciar dois contêineres e criar um arquivo em cada um. O que você verá é que os arquivos criados em um contêiner não estão disponíveis em outro.

1. Inicie um `ubuntu` contêiner que criará um arquivo chamado `/data.txt` com um número aleatório entre 1 e 10000.

    ```bash
    docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"
    ```

    Caso esteja curioso sobre o comando, você está iniciando um shell bash e invocando dois comandos (por que ele tem o `&&` ). A primeira parte escolhe um único número aleatório e grava-o em `/data.txt` . O segundo comando está simplesmente assistindo a um arquivo para manter o contêiner em execução.

1. Validar você pode ver a saída usando `exec` para entrar no contêiner. para fazer isso, abra a extensão VS Code e clique na opção **anexar Shell** . isso usará `exec` para abrir um shell no contêiner dentro do VS Code terminal.

    ![VS Code abrir a CLI no contêiner do ubuntu](media/attach_shell.png)

    Você verá um terminal que está executando um shell no contêiner do Ubuntu. Execute o comando a seguir para ver o conteúdo do `/data.txt` arquivo. Feche este terminal mais tarde.

    ```bash
    cat /data.txt
    ```

    Se você preferir a linha de comando, poderá usar o `docker exec` comando para fazer o mesmo. Você precisa obter a ID do contêiner (use `docker ps` para obtê-lo) e obter o conteúdo com o comando a seguir.

    ```bash
    docker exec <container-id> cat /data.txt
    ```

    Você deve ver um número aleatório!

1. Agora, inicie outro `ubuntu` contêiner (a mesma imagem) e você verá que não tem o mesmo arquivo.

    ```bash
    docker run -it ubuntu ls /
    ```

    E olhe! Não há nenhum `data.txt` arquivo lá! Isso ocorre porque ele foi gravado no espaço transitório apenas para o primeiro contêiner.

1. Vá em frente e remova o primeiro contêiner usando o `docker rm -f` comando.

## <a name="container-volumes"></a>Volumes de contêiner

Com o experimento anterior, você viu que cada contêiner inicia na definição da imagem sempre que ele é iniciado. Embora os contêineres possam criar, atualizar e excluir arquivos, essas alterações são perdidas quando o contêiner é removido e todas as alterações são isoladas nesse contêiner. Com os volumes, você pode alterar tudo isso.

Os [volumes](https://docs.docker.com/storage/volumes/) fornecem a capacidade de conectar caminhos específicos do sistema de arquivos do contêiner de volta ao computador host. Se um diretório no contêiner for montado, as alterações nesse diretório também serão vistas no computador host. Se você montar esse mesmo diretório em reinicializações de contêiner, verá os mesmos arquivos.

Há dois tipos principais de volumes. você eventualmente usará ambos, mas começará com **volumes nomeados**.

## <a name="persist-your-todo-data"></a>Manter seus dados de todo

Por padrão, o aplicativo todo armazena seus dados em um [banco](https://www.sqlite.org/index.html) de dados SQLite em `/etc/todos/todo.db` . Se você não estiver familiarizado com o SQLite, nenhuma preocupação! Ele é simplesmente um banco de dados relacional no qual todos eles são armazenados em um único arquivo. Embora esse não seja o melhor para aplicativos em grande escala, ele funciona para demonstrações pequenas. Falaremos sobre como mudar isso para um mecanismo de banco de dados real mais tarde.

Com o banco de dados sendo um único arquivo, se você puder persistir esse arquivo no host e disponibilizá-lo para o próximo contêiner, ele deverá ser capaz de selecionar onde o último parou. Ao criar um volume e anexá-lo (geralmente chamado de "montagem") no diretório em que os dados são armazenados, você pode manter os dados. Como o contêiner grava no `todo.db` arquivo, ele é mantido para o host no volume.

Conforme mencionado, você vai usar um **volume nomeado**. Imagine um volume nomeado como simplesmente um Bucket de dados. O Docker mantém o local físico no disco e você só precisa se lembrar do nome do volume. Toda vez que você usar o volume, o Docker garantirá que os dados corretos sejam fornecidos.

1. Crie um volume usando o `docker volume create` comando.

    ```bash
    docker volume create todo-db
    ```

1. Pare o contêiner de aplicativo todo novamente no modo de exibição do Docker (ou com `docker rm -f <id>` ), pois ele ainda está em execução sem usar o volume persistente.

1. Inicie o contêiner de aplicativo todo, mas adicione o `-v` sinalizador para especificar uma montagem de volume. Você usará o volume nomeado e o montará para `/etc/todos` o, que capturará todos os arquivos criados no caminho.

    ```bash
    docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
    ```

1. Depois que o contêiner for iniciado, abra o aplicativo e adicione alguns itens à sua lista de tarefas pendentes.

    ![Itens adicionados à lista de tarefas pendentes](media/items-added.png)

1. Remova o contêiner do aplicativo de tarefas pendentes. Use a exibição do Docker ou `docker ps` para obter a ID e, em seguida, `docker rm -f <id>` removê-la.

1. Inicie um novo contêiner usando o mesmo comando acima.

1. abra o aplicativo. Você deve ver seus itens ainda em sua lista!

1. Vá em frente e remova o contêiner quando terminar de verificar sua lista.

Alegria! Agora você aprendeu a manter os dados!

> [!TIP]
> Embora os volumes nomeados e as montagens de ligação (que falaremos em um minuto) sejam os dois tipos principais de volumes com suporte em uma instalação padrão do mecanismo do Docker, há muitos plug-ins de driver de volume disponíveis para dar suporte a NFS, SFTP, NetApp e muito mais! Isso será especialmente importante quando você começar a executar contêineres em vários hosts em um ambiente clusterizado com Swarm, kubernetes e assim por diante.

## <a name="dive-into-your-volume"></a>Aprofunde-se no seu volume

Muitas pessoas freqüentemente perguntam "onde o Docker *realmente* armazena meus dados quando uso um volume nomeado?" Se você quiser saber, poderá usar o `docker volume inspect` comando.

```bash
docker volume inspect todo-db
[
    {
        "CreatedAt": "2019-09-26T02:18:36Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/todo-db/_data",
        "Name": "todo-db",
        "Options": {},
        "Scope": "local"
    }
]
```

O `Mountpoint` é o local real no disco onde os dados são armazenados. Observe que na maioria das máquinas, você precisará ter acesso de raiz para acessar esse diretório do host. Mas é aí que está!

> [!NOTE]
> **Acessando dados de volume diretamente no Docker desktop** Durante a execução no Docker desktop, os comandos do Docker são realmente executados dentro de uma VM pequena em seu computador. Se você quisesse examinar o conteúdo real do diretório *mountpoint* , precisaria primeiro entrar dentro da VM. No WSL 2, ele está dentro de um WSL 2 distribuição e pode ser acessado por meio do explorador de arquivos.

## <a name="recap"></a>Recapitulação

Neste ponto, você tem um aplicativo funcional que pode sobreviver a reinicializações! Você pode mostrá-lo para seus investidores e esperar que eles possam pegar sua visão!

No entanto, você viu anteriormente que a recriação de imagens para cada alteração leva bastante tempo. Precisa ser uma maneira melhor de fazer alterações, certo? Com montagens de associação (que mencionamos anteriormente), há uma maneira melhor! Vamos dar uma olhada agora!

## <a name="next-steps"></a>Próximas etapas

Continue com o tutorial!

> [!div class="nextstepaction"]
> [Usando montagens de associação](use-bind-mounts.md)

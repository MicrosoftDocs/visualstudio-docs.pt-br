---
title: 'Tutorial do Docker-parte 6: aplicativos com vários contêineres'
description: Como configurar a rede entre contêineres e adicionar um contêiner para um banco de dados MySQL.
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: d23d1f5d94729741630ee76263fd5b32041e9cfd
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222910"
---
# <a name="multi-container-apps"></a>Aplicativos com vários contêineres

Até este ponto, você esteve trabalhando com aplicativos de contêiner único. Mas, agora você adicionará o MySQL à pilha de aplicativos. A pergunta a seguir geralmente surge: "onde o MySQL será executado? Instalá-lo no mesmo contêiner ou executá-lo separadamente? " Em geral, **cada contêiner deve fazer uma coisa e fazê-lo bem.** Alguns motivos:

- Há uma boa chance de que você precise dimensionar as APIs e front-ends de forma diferente dos bancos de dados
- Contêineres separados permitem que você dê versão e atualize versões isoladamente
- Embora você possa usar um contêiner para o banco de dados localmente, talvez queira usar um serviço gerenciado para o banco de dados em produção. Você não quer enviar seu mecanismo de banco de dados com seu aplicativo.
- A execução de vários processos exigirá um Gerenciador de processos (o contêiner só inicia um processo), o que adiciona complexidade à inicialização/desligamento do contêiner.

E há mais motivos. Portanto, você atualizará seu aplicativo para que ele funcione da seguinte maneira:

![Aplicativo todo conectado ao contêiner MySQL](media/multi-app-architecture.png)

## <a name="container-networking"></a>Rede de contêineres

Lembre-se de que os contêineres, por padrão, são executados isoladamente e não sabem nada sobre outros processos ou contêineres no mesmo computador. Então, como permitir que um contêiner se comunique com outro? A resposta é **rede**. Agora, você não precisa ser um engenheiro de rede (alegria!). Basta lembrar esta regra...

> [!NOTE]
> Se dois contêineres estiverem na mesma rede, eles poderão se comunicar entre si. Se não forem, eles não poderão.

## <a name="start-mysql"></a>Iniciar o MySQL

Há duas maneiras de colocar um contêiner em uma rede: atribuí-lo em iniciar ou conectar um contêiner existente. Por enquanto, você criará a rede primeiro e anexará o contêiner do MySQL na inicialização.

1. Crie a rede.

    ```bash
    docker network create todo-app
    ```

1. Inicie um contêiner do MySQL e anexe-o à rede. Também vamos definir algumas variáveis de ambiente que o banco de dados usará para inicializar o banco de dados (consulte a seção "variáveis de ambiente" na [listagem do Hub do Docker do MySQL](https://hub.docker.com/_/mysql/)) (substitua os ` \ ` caracteres por `` ` `` em Windows PowerShell).

    ```bash
    docker run -d \
        --network todo-app --network-alias mysql \
        -v todo-mysql-data:/var/lib/mysql \
        -e MYSQL_ROOT_PASSWORD=secret \
        -e MYSQL_DATABASE=todos \
        mysql:5.7
    ```

    Você também verá que especificou o `--network-alias` sinalizador. Voltaremos a isso daqui a pouco.

    > [!TIP]
    > Você notará que está usando um nome de volume `todo-mysql-data` aqui e montando-o em `/var/lib/mysql` , que é onde o MySQL armazena seus dados. No entanto, você nunca executou um `docker volume create` comando. O Docker reconhece que você deseja usar um volume nomeado e cria um automaticamente para você.

1. Para confirmar se o banco de dados está em execução, conecte-se ao banco de dados e verifique se ele se conecta.

    ```bash
    docker exec -it <mysql-container-id> mysql -p
    ```

    Quando o prompt de senha aparecer, digite **segredo**. No Shell do MySQL, liste os bancos de dados e verifique se você vê o `todos` Database.

    ```cli
    mysql> SHOW DATABASES;
    ```

    Você deverá ver uma saída semelhante a esta:

    ```plaintext
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | mysql              |
    | performance_schema |
    | sys                |
    | todos              |
    +--------------------+
    5 rows in set (0.00 sec)
    ```

    Alegria! Você tem seu `todos` banco de dados e ele está pronto para uso!

## <a name="connect-to-mysql"></a>Conectar-se ao MySQL

Agora que você sabe que o MySQL está em execução, vamos usar! Mas, a pergunta é... Qual? Se você executar outro contêiner na mesma rede, como encontrará o contêiner (Lembre-se de que cada contêiner tem seu próprio endereço IP)?

Para descobrir, você usará o contêiner [nicolaka/netacertar](https://github.com/nicolaka/netshoot) , que é fornecido com *muitas* ferramentas úteis para solucionar problemas ou depurar os erros de rede.

1. Inicie um novo contêiner usando a `nicolaka/netshoot` imagem. Certifique-se de conectá-lo à mesma rede.

    ```bash
    docker run -it --network todo-app nicolaka/netshoot
    ```

1. Dentro do contêiner, use o `dig` comando, que é uma ferramenta de DNS útil. Procure o endereço IP do nome do host `mysql` .

    ```bash
    dig mysql
    ```

    E você obterá uma saída como esta...

    ```text
    ; <<>> DiG 9.14.1 <<>> mysql
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 32162
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

    ;; QUESTION SECTION:
    ;mysql.             IN  A

    ;; ANSWER SECTION:
    mysql.          600 IN  A   172.23.0.2

    ;; Query time: 0 msec
    ;; SERVER: 127.0.0.11#53(127.0.0.11)
    ;; WHEN: Tue Oct 01 23:47:24 UTC 2019
    ;; MSG SIZE  rcvd: 44
    ```

    Na "seção de resposta", você verá um `A` registro para o `mysql` que resolve para `172.23.0.2` (seu endereço IP provavelmente terá um valor diferente). Embora `mysql` normalmente não seja um nome de host válido, o Docker foi capaz de resolvê-lo para o endereço IP do contêiner que tinha esse alias de rede (Lembre-se do `--network-alias` sinalizador usado anteriormente?).

    O que isso significa é... seu aplicativo apenas precisa apenas se conectar a um host chamado `mysql` e ele se comunicará com o banco de dados! Não é muito mais simples do que isso!

## <a name="run-your-app-with-mysql"></a>Executar seu aplicativo com o MySQL

O aplicativo todo oferece suporte à configuração de algumas variáveis de ambiente para especificar as configurações de conexão do MySQL. São eles:

- `MYSQL_HOST` -o nome do host para o servidor MySQL em execução
- `MYSQL_USER` -o nome de usuário a ser usado para a conexão
- `MYSQL_PASSWORD` -a senha a ser usada para a conexão
- `MYSQL_DB` -o banco de dados a ser usado uma vez conectado

> [!WARNING]
> **definindo Configurações de conexão por meio de variáveis de ambiente** Embora o uso de variáveis de ambiente para definir as configurações de conexão seja geralmente um problema para o desenvolvimento, ele é altamente desencorajado durante a execução de aplicativos em produção. Para entender o porquê, veja [por que você não deve usar variáveis de ambiente para dados secretos](https://diogomonica.com/2017/03/27/why-you-shouldnt-use-env-variables-for-secret-data/).
> Um mecanismo mais seguro é usar o suporte de segredo fornecido pela estrutura de orquestração de contêiner. Na maioria dos casos, esses segredos são montados como arquivos no contêiner em execução. Você verá que muitos aplicativos (incluindo a imagem do MySQL e o aplicativo de tarefas) também dão suporte a env VARs com um `_FILE` sufixo para apontar para um arquivo que contém o arquivo.
> Por exemplo, definir o `MYSQL_PASSWORD_FILE` var fará com que o aplicativo use o conteúdo do arquivo referenciado como a senha de conexão. O Docker não faz nada para dar suporte a esses VARs de env. Seu aplicativo precisará saber procurar a variável e obter o conteúdo do arquivo.

Com tudo isso explicado, inicie seu contêiner pronto para desenvolvimento!

1. Especifique cada uma das variáveis de ambiente acima e conecte o contêiner à sua rede de aplicativos (substitua os ` \ ` caracteres por `` ` `` em Windows PowerShell).

    ```bash hl_lines="3 4 5 6 7"
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

1. Se você examinar os logs do contêiner ( `docker logs <container-id>` ), verá uma mensagem indicando que está usando o banco de dados MySQL.

    ```plaintext hl_lines="7"
    # Previous log messages omitted
    $ nodemon src/index.js
    [nodemon] 1.19.2
    [nodemon] to restart at any time, enter `rs`
    [nodemon] watching dir(s): *.*
    [nodemon] starting `node src/index.js`
    Connected to mysql db at host mysql
    Listening on port 3000
    ```

1. Abra o aplicativo em seu navegador e adicione alguns itens à sua lista de tarefas pendentes.

1. Conexão ao banco de dados MySQL e provar que os itens estão sendo gravados no banco de dados. Lembre-se de que a senha é **secreta**.

    ```bash
    docker exec -ti <mysql-container-id> mysql -p todos
    ```

    E no Shell do MySQL, execute o seguinte:

    ```plaintext
    mysql> select * from todo_items;
    +--------------------------------------+--------------------+-----------+
    | id                                   | name               | completed |
    +--------------------------------------+--------------------+-----------+
    | c906ff08-60e6-44e6-8f49-ed56a0853e85 | Do amazing things! |         0 |
    | 2912a79e-8486-4bc3-a4c5-460793a575ab | Be awesome!        |         0 |
    +--------------------------------------+--------------------+-----------+
    ```

    Obviamente, sua tabela terá uma aparência diferente porque tem seus itens. Mas você deve vê-los armazenados lá!

Se você olhar rapidamente a extensão do Docker, verá que você tem dois contêineres de aplicativo em execução. Mas, não há nenhuma indicação real de que eles são agrupados em um único aplicativo. Você verá como tornar isso melhor em breve!

![Extensão do Docker mostrando dois contêineres de aplicativo desagrupados](media/vs-multi-container-app.png)

## <a name="recap"></a>Recapitulação

Neste ponto, você tem um aplicativo que agora armazena seus dados em um banco de dado externo em execução em um contêiner separado. Você aprendeu um pouco sobre a rede de contêineres e viu como a descoberta de serviço pode ser executada usando o DNS.

Mas há uma boa chance de que você esteja começando a se sentir um pouco sobrecarregado com tudo o que você precisa fazer para iniciar este aplicativo. Você precisa criar uma rede, iniciar contêineres, especificar todas as variáveis de ambiente, expor portas e muito mais! Isso é muito para se lembrar e, certamente, tornar as coisas mais difíceis de passar para outra pessoa.

Na próxima seção, falaremos sobre Docker Compose. Com o Docker Compose, você pode compartilhar suas pilhas de aplicativos de uma maneira muito mais fácil e deixar que outras as girem com um único comando (e simples)!

## <a name="next-steps"></a>Próximas etapas

Continue com o tutorial!

> [!div class="nextstepaction"]
> [Usando Docker Compose](use-docker-compose.md)

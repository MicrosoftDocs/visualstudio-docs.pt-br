---
title: 'Tutorial do Docker-parte 2: atualizar seu aplicativo'
description: Descreve como atualizar um aplicativo Docker.
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 43034ff2e65564cc8af2710b796b76996f21f4c8
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222767"
---
# <a name="update-the-app"></a>Atualizar o aplicativo

Como uma pequena solicitação de recursos, você foi solicitado pela equipe de produto a alterar o "texto vazio" quando não há nenhum item de lista de tarefas. Eles gostariam de fazer a transição para o seguinte:

> Você ainda não tem itens de tarefas pendentes! Adicione um acima!

Muito simples, certo? Vamos fazer a alteração.

## <a name="update-the-source-code"></a>Atualizar o código-fonte

1. No `src/static/js/app.js` arquivo, atualize a linha 56 para usar o novo texto vazio.

    ```diff
    -                <p className="text-center">No items yet! Add one above!</p>
    +                <p className="text-center">You have no todo items yet! Add one above!</p>
    ```

1. Crie a versão atualizada da imagem, usando o mesmo comando usado anteriormente.

    ```bash
    docker build -t getting-started .
    ```

1. Inicie um novo contêiner usando o código atualizado.

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

**Oh!** Você provavelmente viu um erro como este (as IDs serão diferentes):

```bash
docker: Error response from daemon: driver failed programming external connectivity on endpoint laughing_burnell 
(bb242b2ca4d67eba76e79474fb36bb5125708ebdabd7f45c8eaf16caaabde9dd): Bind for 0.0.0.0:3000 failed: port is already allocated.
```

O que aconteceu? Não foi possível iniciar o novo contêiner, pois o contêiner antigo ainda está em execução. O motivo disso é que isso é um problema porque esse contêiner está usando a porta 3000 do host e apenas um processo no computador (contêineres incluídos) pode escutar uma porta específica. Para corrigir isso, remova o contêiner antigo.

## <a name="replace-the-old-container"></a>Substituir o contêiner antigo

Para remover um contêiner, primeiro ele precisa ser parado. Depois que ele for interrompido, ele poderá ser removido. Você tem duas maneiras de remover o contêiner antigo. Fique à vontade para escolher o caminho com o qual você está mais confortável.

### <a name="remove-a-container-using-the-cli"></a>Remover um contêiner usando a CLI

1. Obtenha a ID do contêiner usando o `docker ps` comando.

    ```bash
    docker ps
    ```

1. Use o `docker stop` comando para parar o contêiner.

    ```bash
    # Swap out <the-container-id> with the ID from docker ps
    docker stop <the-container-id>
    ```

1. Depois que o contêiner for interrompido, você poderá removê-lo usando o `docker rm` comando.

    ```bash
    docker rm <the-container-id>
    ```

> [!TIP]
> Você pode parar e remover um contêiner em um único comando adicionando o sinalizador "Force" ao `docker rm` comando. Por exemplo: `docker rm -f <the-container-id>`

### <a name="remove-a-container-using-the-docker-view"></a>Remover um contêiner usando o modo de exibição do Docker

se você abrir a extensão VS Code, poderá remover um contêiner com dois cliques! Certamente é muito mais fácil do que ter de Pesquisar a ID do contêiner e removê-la.

1. Com a extensão aberta, navegue até o contêiner e clique com o botão direito do mouse.

1. Clique na opção **remover** .

1. Confirme a remoção e você terminou!

![Exibição do Docker-removendo um contêiner](media/vs-removing-container.png)

### <a name="start-the-updated-app-container"></a>Iniciar o contêiner de aplicativo atualizado

1. Agora, inicie seu aplicativo atualizado.

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

1. Atualize seu navegador no [http://localhost:3000](http://localhost:3000) e você deverá ver o texto de ajuda atualizado!

![Aplicativo atualizado com texto vazio atualizado](media/todo-list-updated-empty-text.png)

## <a name="recap"></a>Recapitulação

Embora você pudesse criar uma atualização, havia duas coisas que você talvez tenha notado:

- Todos os itens existentes em sua lista de tarefas pendentes! Esse não é um aplicativo muito bom! Falaremos sobre isso em breve.
- Houve *muitas* etapas envolvidas para uma alteração tão pequena. Em uma próxima seção, você aprenderá a ver as atualizações de código sem a necessidade de recompilar e iniciar um novo contêiner sempre que fizer uma alteração.

Antes de aprender sobre a persistência, você verá rapidamente como compartilhar essas imagens com outras pessoas.

## <a name="next-steps"></a>Próximas etapas

Continue com o tutorial!

> [!div class="nextstepaction"]
> [Compartilhando seu aplicativo](share-your-app.md)

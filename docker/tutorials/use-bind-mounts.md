---
title: 'Tutorial do Docker – Parte 5: Usar montagens de vinculação'
description: Descreve como usar montagens de vinculação para controlar o ponto de montagem no host.
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: ad3737ccfa4b0dae8ad427bd79e4adeb2756795b
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222754"
---
# <a name="use-bind-mounts"></a>Usar montagens de vinculação

No capítulo anterior, você aprendeu e usou um **volume nomeado** para persistir os dados em seu banco de dados. Volumes nomeados serão ótimos se você simplesmente quiser armazenar dados, pois não precisa se preocupar com o *local* em que os dados são armazenados.

Com **montagens de vinculação**, você controla o ponto de montagem exato no host. Você pode usar isso para persistir dados, mas geralmente é usado para fornecer dados adicionais em contêineres. Ao trabalhar em um aplicativo, você pode usar uma montagem de vinculação para montar o código-fonte no contêiner para permitir que ele veja alterações de código, responda e deixe que você veja as alterações imediatamente.

Para aplicativos baseados em [Nó, nodemon](https://npmjs.com/package/nodemon) é uma ótima ferramenta para observar as alterações de arquivo e reiniciar o aplicativo. Há ferramentas equivalentes na maioria das outras linguagens e estruturas.

## <a name="quick-volume-type-comparisons"></a>Comparações rápidas de tipo de volume

Montagens de vinculação e volumes nomeados são os dois tipos principais de volumes que vêm com o mecanismo do Docker. No entanto, drivers de volume adicionais estão disponíveis para dar suporte a outros casos de uso[(SFTP,](https://github.com/vieux/docker-volume-sshfs) [Ceph,](https://ceph.com/geen-categorie/getting-started-with-the-docker-rbd-volume-plugin/) [NetApp,](https://netappdvp.readthedocs.io/en/stable/) [S3](https://github.com/elementar/docker-s3-volume)e muito mais).

| Propriedade | Volumes nomeados | Montagens por associação |
| -------- | ------------- | ----------- |
| Local do host | Escolha do Docker | Você controla |
| Exemplo de montagem (usando `-v` ) | my-volume:/usr/local/data | /path/to/data:/usr/local/data |
| Popula o novo volume com o conteúdo do contêiner | Sim | Não |
| Dá suporte a drivers de volume | Sim | Não |

## <a name="start-a-dev-mode-container"></a>Iniciar um contêiner de modo dev

Para executar seu contêiner para dar suporte a um fluxo de trabalho de desenvolvimento, você fará o seguinte:

- Montar o código-fonte no contêiner
- Instalar todas as dependências, incluindo as dependências de "dev"
- Inicie nodemon para observar as alterações do sistema de arquivos

1. Certifique-se de que você não tenha nenhum contêiner `getting-started` anterior em execução.

1. Execute o comando a seguir (substitua os ` \ ` caracteres `` ` `` por em Windows PowerShell). Você aprenderá o que está acontecendo depois:

    ```bash
    docker run -dp 3000:3000 \
        -w /app \
        -v "%cd%:/app" \
        node:12-alpine \
        sh -c "yarn install && yarn run dev"
    ```

    - `-dp 3000:3000` - o mesmo que antes. Executar no modo de detached (plano de fundo) e criar um mapeamento de porta
    - `-w /app` – define o "diretório de trabalho" ou o diretório atual do qual o comando será executado
    - `-v "%cd%:/app"` – a fim de vincular a montagem do diretório atual do host no contêiner ao `/app` diretório
    - `node:12-alpine` - a imagem a ser usada. Observe que essa é a imagem base para seu aplicativo do Dockerfile
    - `sh -c "yarn install && yarn run dev"` - o comando . Estamos iniciando um shell usando (alpine não tem ) e executando para instalar todas as `sh` `bash` dependências e, em `yarn install` seguida, executando  `yarn run dev` . Se você procurar no `package.json` , veremos que o script está `dev` iniciando `nodemon` .

1. Você pode observar os logs usando `docker logs -f <container-id>` . Você vai saber que está pronto para começar quando vir isso:

    ```bash
    docker logs -f <container-id>
    $ nodemon src/index.js
    [nodemon] 1.19.2
    [nodemon] to restart at any time, enter `rs`
    [nodemon] watching dir(s): *.*
    [nodemon] starting `node src/index.js`
    Using sqlite database at /etc/todos/todo.db
    Listening on port 3000
    ```

    Quando terminar de observar os logs, saia clicando em `Ctrl` + `C` .

1. Agora, faça uma alteração no aplicativo. No `src/static/js/app.js` arquivo, altere o **botão Adicionar Item** para simplesmente dizer **Adicionar**. Essa alteração estará na linha 109.

    ```diff
    -                         {submitting ? 'Adding...' : 'Add Item'}
    +                         {submitting ? 'Adding...' : 'Add'}
    ```

1. Basta atualizar a página (ou abri-la) e você verá a alteração refletida no navegador quase imediatamente. Pode levar alguns segundos para que o servidor Node seja reiniciado, portanto, se você receber um erro, tente atualizar após alguns segundos.

    ![Captura de tela do rótulo atualizado para o botão Adicionar](media/updated-add-button.png)

1. Sinta-se à vontade para fazer outras alterações que você gostaria de fazer. Quando terminar, pare o contêiner e crie sua nova imagem usando `docker build -t getting-started .` .

O uso de montagens de *vinculação é muito* comum para configurações de desenvolvimento local. A vantagem é que o computador dev não precisa ter todas as ferramentas de build e ambientes instalados. Com um único `docker run` comando, o ambiente dev é esvasado e pronto para uso. Você aprenderá sobre Docker Compose em uma etapa futura, pois isso ajudará a simplificar seus comandos (você já está recebendo muitos sinalizadores).

## <a name="recap"></a>Recapitulação

Neste ponto, você pode persistir seu banco de dados e responder rapidamente às necessidades e às demandas de seus diretores e seus criadores. Viva! Mas, adivinha o quê? Você recebeu ótimas notícias!

**Seu projeto foi selecionado para desenvolvimento futuro!**

Para se preparar para produção, você precisa migrar seu banco de dados do trabalho no SQLite para algo que possa ser dimensionado um pouco melhor. Para simplificar, você manterá um banco de dados relacional e alterna o aplicativo para usar o MySQL. Mas, como você deve executar o MySQL? Como você permite que os contêineres se comumentem entre si? Você aprenderá sobre isso em seguida!

## <a name="next-steps"></a>Próximas etapas

Continue com o tutorial!

> [!div class="nextstepaction"]
> [Aplicativos com vários contêineres](multi-container-apps.md)
---
title: 'Tutorial do Docker – Parte 9: Implantar na nuvem'
description: Implante um aplicativo do Docker em um serviço de nuvem para hospedagem.
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: da38b7482396b0bf46f5566c0c4a5416c94e83eb
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222819"
---
# <a name="deploy-to-the-cloud"></a>Implantar na nuvem

Agora que você executa seu aplicativo localmente, pode começar a pensar em executar na nuvem para que outras pessoas possam acessá-lo e usá-lo. Para fazer isso, você usará contextos do Docker. Um contexto é o local em que você está trabalhando atualmente com contêineres. No momento, você tem apenas o contexto "padrão", portanto, você precisará adicionar uma nuvem e implantar seu aplicativo nele.

## <a name="create-your-cloud-context"></a>Criar seu contexto de nuvem

1. Para começar, você pode ver quais contextos você tem observando a seção de contextos do painel do Docker:

   ![Mostra apenas o contexto padrão](media/defaultcontext.png)

Você só deve ver o contexto padrão para o trabalho local.

1. Para implantar na nuvem, você precisa criar um novo contexto de ACI, mas para fazer isso, primeiro você precisa da extensão de conta do Azure para autenticar com o Azure.

   ![Adicionando a extensão do Azure](media/addazureextension.png)

Você precisará configurar uma conta do Azure se ainda não tiver uma.

1. Agora você pode criar seu novo contexto de ACI. Você pode fazer isso clicando no botão a mais na seção **Contextos** da exibição do Docker.

   ![Criando seu contexto de ACI](media/createnewcontext.png)

Isso perguntará em qual grupo de recursos você deseja executar esses contêineres. Selecione um grupo existente usando as teclas de direção ou use a opção padrão para usar o novo grupo.

![Selecionando seu grupo de recursos](media/selectresourcegroup.png)

Agora você pode ver seu contexto de ACI listado e pode clicar com o botão direito do mouse para torná-lo seu contexto de foco/em uso atual:

![Novo contexto de ACI pode ser selecionado](media/listofcontexts.png)

## <a name="run-containers-in-the-cloud"></a>Executar contêineres na nuvem

1. Agora, use o contexto de ACI e execute o contêiner.

   ```bash
   docker context use myacicontext
   docker run  -dp 3000:3000 <username>/getting-started
   ```

1. Depois de executar isso, agora, veja o contêiner em seu contexto.

   ![Contêiner em execução no contexto da ACI](media/contextcontainer.png)

1. Para verificar se tudo está funcionando corretamente, você pode clicar com o botão direito do mouse no contêiner em execução e escolher **Exibir no navegador**.

   ![Contêiner na ACI com IP público](media/containerinaci.png)

E você pode ver que o contêiner está em execução em um IP público e funcionando corretamente!

1. Agora, você pode dar uma olhada em nosso contêiner em execução para ver como ele está funcionando. Você pode começar a dar uma olhada nos logs de contêiner:
 
 ```bash
   docker logs distracted-jackson
   ```

1. Você também pode entrar em seu contêiner como faria com um contêiner local.
 
 ```bash
   docker exec -it distracted-jackson sh
   ```

1. Por fim, para limpar o espaço de trabalho e garantir que você não esteja sendo cobrado por continuar a executar o contêiner de teste, basta clicar com o botão direito do mouse no contêiner em execução e escolher **Remover**.

## <a name="recap"></a>Recapitulação

Incrível, agora você levou sua carga de trabalho e a implantou na nuvem com êxito pela primeira vez. Você pode fazer tudo isso na linha de comando, bem como de dentro de seu contexto de ACI usando e também usando para `docker run` `docker compose up` executar seus aplicativos de vários contêineres. Para saber mais sobre como executar seus contêineres na nuvem, leia a documentação [estendida sobre como usar a ACI](https://docs.docker.com/engine/context/aci-integration/).

## <a name="next-steps"></a>Próximas etapas

Continue com o tutorial!

> [!div class="nextstepaction"]
> [O que vem a seguir](whats-next.md)

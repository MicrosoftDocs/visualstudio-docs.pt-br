---
title: 'Tutorial: conectar computadores de desenvolvimento com o Bridge ao kubernetes'
ms.technology: vs-azure
ms.date: 03/24/2021
ms.topic: tutorial
description: Conecte seu computador de desenvolvimento a um cluster kubernetes com ponte para kubernetes com o Visual Studio.
keywords: Ponte para kubernetes, Azure Dev Spaces, espaços de desenvolvimento, Docker, kubernetes, Azure, contêineres
monikerRange: '>=vs-2019'
ms.author: ghogen
author: ghogen
manager: jmartens
ms.openlocfilehash: b8d6c98d2e2146ad57871b74cd2d522ed2b04259
ms.sourcegitcommit: 0499d813d5c24052c970ca15373d556a69507250
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2021
ms.locfileid: "113046112"
---
# <a name="tutorial-use-bridge-to-kubernetes-to-connect-your-clusters-and-your-development-computers"></a>Tutorial: usar o Bridge para kubernetes para conectar seus clusters e seus computadores de desenvolvimento

Neste tutorial, você aprenderá a usar o Bridge para kubernetes para redirecionar o tráfego entre o cluster do kubernetes e o código em execução no seu computador de desenvolvimento. 

Este guia também fornece um script para implantar um aplicativo de exemplo grande com vários microserviços em um cluster kubernetes.

Saiba mais sobre o Bridge para kubernetes com o artigo [como funciona a ponte para o kubernetes](overview-bridge-to-kubernetes.md).

## <a name="prerequisites"></a>Pré-requisitos

- Um cluster kubernetes
- [Visual Studio 2019][visual-studio] versão 16,7 Preview 4 ou superior em execução no Windows 10.
- [Ponte para a extensão kubernetes instalada][btk-extension]

## <a name="about-the-data"></a>Sobre os dados

Este tutorial usa o Bridge para kubernetes para desenvolver uma versão de microatendimento de um aplicativo de exemplo simples TODO em qualquer cluster kubernetes. Este [aplicativo de exemplo de aplicativo todo][todo-app-github], usando o Visual Studio, foi adaptado do código fornecido pelo [TodoMVC](http://todomvc.com). 

 Essas etapas devem funcionar com qualquer cluster kubernetes. Portanto, se você já tiver seu próprio aplicativo em execução em um cluster kubernetes, ainda poderá seguir as etapas abaixo e usar os nomes dos seus próprios serviços.

O exemplo de aplicativo TODO é composto de um frontend e um back-end que fornece armazenamento persistente. Esse exemplo estendido adiciona um componente de estatísticas e divide o aplicativo em vários microserviços, especificamente:

- O front-end chama a API de banco de dados para persistir e atualizar itens de tarefas pendentes;
- O serviço de API de banco de dados depende de um banco de dados Mongo para manter itens de tarefas pendentes;
- O front-end grava os eventos adicionar, concluir e excluir em uma fila do RabbitMQ;
- Um trabalhador de estatísticas recebe eventos da fila RabbitMQ e atualiza um cache Redis;
- Uma API de estatísticas expõe as estatísticas armazenadas em cache para o front-end mostrar.

De todo, esse aplicativo estendido TODO é composto por seis componentes inter-relacionados.


## <a name="check-the-cluster"></a>Verificar o cluster

Abra um prompt de comando e verifique se o `kubectl` está instalado e no caminho, se o cluster que você deseja usar está disponível e pronto e defina o contexto para esse cluster.

```cmd
kubectl cluster-info
kubectl config use-context {context-name}
```

em que {Context-Name} é o nome do contexto para o cluster que você deseja usar para o exemplo de todo-aplicativo.

## <a name="deploy-the-application"></a>Implantar o aplicativo

Clone o [repositório mindaro](https://github.com/Microsoft/mindaro) e abra uma janela de comando com a pasta de trabalho atual para *Samples/todo-app*.

Crie um namespace para o exemplo.

```cmd
kubectl create namespace todo-app
```

Em seguida, aplique o manifesto de implantação:

```cmd
kubectl apply -n todo-app -f deployment.yaml
```

Essa é uma implantação simples que expõe o frontend usando um serviço do tipo `LoadBalancer` . Aguarde até que todos os pods estejam em execução e para que o IP externo do `frontend` serviço fique disponível.

Se você estiver testando com o MiniKube, será necessário usar `minikube tunnel` para resolver um IP externo. Se você estiver usando o AKS ou outro provedor kubernetes baseado em nuvem, um IP externo será atribuído automaticamente. Use o comando a seguir para monitorar o `frontend` serviço para aguardar até que ele esteja em execução:

```output
kubectl get service -n todo-app frontend --watch

NAME       TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)        AGE
frontend   LoadBalancer   10.0.245.78   20.73.226.228   80:31910/TCP   6m26s
```

Navegue até o aplicativo usando o IP externo e a porta local (o primeiro número na coluna porta (S)).

```
http://{external-ip}:{local-port}
```

Teste o aplicativo em execução no navegador. Conforme você adiciona, completa e exclui itens de tarefas pendentes, observe que a página de estatísticas é atualizada com as métricas esperadas.

## <a name="connect-to-your-cluster-and-debug-a-service"></a>Conectar-se ao cluster e depurar um serviço

Abra o *samples\todo-app\database-api\database-API.csproj* no Visual Studio. No projeto, selecione **ponte para kubernetes** na lista suspensa configurações de inicialização, conforme mostrado abaixo.

![Escolha ponte para kubernetes](media/bridge-to-kubernetes/choose-bridge-to-kubernetes.png)

Clique no botão iniciar ao lado de *ponte para kubernetes*. Na caixa de diálogo **Criar perfil para a ponte para o kubernetes** :

- Selecione o nome do cluster.
- Selecione *todo-aplicativo* para seu namespace.
- Selecione *Database-API* para o serviço redirecionar.
- Selecione a mesma URL que você usou anteriormente para iniciar o navegador, http://{External-IP}: {local-Port}

![Escolha a ponte para o cluster kubernetes](media/bridge-to-kubernetes/configure-bridge-debugging.png)

Escolha se deseja ou não ser executado de forma isolada, o que significa que outras pessoas que estão usando o cluster não serão afetadas pelas suas alterações. Esse modo de isolamento é realizado roteando suas solicitações para a cópia de cada serviço afetado, mas roteando todos os outros tráfego normalmente. Mais explicações sobre como isso é feito pode ser encontrado em [como a ponte para o kubernetes funciona][btk-overview-routing].

Clique em **OK**. Todo o tráfego no cluster kubernetes é redirecionado para o serviço de *API de banco de dados* para a versão do seu aplicativo em execução no seu computador de desenvolvimento. A ponte para o kubernetes também roteia todo o tráfego de saída do aplicativo de volta para o cluster kubernetes.

> [!NOTE]
> Você receberá uma solicitação para permitir que o *EndpointManager* seja executado com privilégios elevados e modificará o arquivo de hosts.

Seu computador de desenvolvimento está conectado quando a barra de status mostra que você está conectado ao `database-api` serviço.

![Computador de desenvolvimento conectado](media/bridge-to-kubernetes/development-computer-connected.png)

> [!NOTE]
> Em inicializações subsequentes, você não será avisado com a caixa de diálogo **Criar perfil para a ponte para kubernetes** . Você atualiza essas configurações na **depuração** nas propriedades do projeto.

Quando o computador de desenvolvimento estiver conectado, o tráfego começará a redirecionar para o seu computador de desenvolvimento para o serviço que você está substituindo.

> [!NOTE]
> Para editar o perfil de depuração mais tarde, por exemplo, se você quiser testar com um serviço kubernetes diferente, escolha **depurar**  >  **Propriedades de depuração** e clique no botão **alterar** .

## <a name="set-a-break-point"></a>Definir um ponto de interrupção

Abra MongoHelper. cs e clique em algum lugar na linha 68 no método CreateTask para colocar o cursor lá. Defina um ponto de interrupção pressionando *F9* ou selecionando **depurar**  >  **alternância de ponto de interrupção**.

Navegue até o aplicativo de exemplo abrindo a URL pública (o endereço IP externo para o serviço de front-end). Para retomar o serviço, pressione **F5** ou clique em **depurar**  >  **continuar**.

Remova o ponto de interrupção, colocando o cursor na linha com o ponto de interrupção e pressionando **F9**.

> [!NOTE]
> Por padrão, a interrupção da tarefa de depuração também desconecta o computador de desenvolvimento do cluster kubernetes. Você pode alterar esse comportamento alterando **desconectar após a depuração** `false` no na seção **ferramentas de depuração kubernetes** da caixa de diálogo opções de **ferramentas**  >   . Depois de atualizar essa configuração, o computador de desenvolvimento permanecerá conectado quando você parar e iniciar a depuração. Para desconectar seu computador de desenvolvimento do cluster, clique no botão **Desconectar** na barra de ferramentas.
>
>![Captura de tela de opções de depuração kubernetes](media/bridge-to-kubernetes/kubernetes-debugging-options.png)

## <a name="additional-configuration"></a>Configuração adicional

A ponte para kubernetes pode manipular o tráfego de roteamento e replicar variáveis de ambiente sem nenhuma configuração adicional. Se precisar baixar todos os arquivos que são montados no contêiner em seu cluster kubernetes, como um arquivo ConfigMap, você pode criar um `KubernetesLocalProcessConfig.yaml` para baixar esses arquivos em seu computador de desenvolvimento. Para obter mais informações, consulte [usando KubernetesLocalProcessConfig. YAML para configuração adicional com for Bridge para kubernetes][kubernetesLocalProcessConfig-yaml].

## <a name="using-logging-and-diagnostics"></a>Usando log e diagnóstico

Você pode encontrar os logs de diagnóstico no `Bridge to Kubernetes` diretório no diretório *temporário* do seu computador de desenvolvimento.

## <a name="next-steps"></a>Próximas etapas

Saiba como o Bridge to kubernetes funciona.

> [!div class="nextstepaction"]
> [Como funciona a Ponte para Kubernetes](overview-bridge-to-kubernetes.md)

[todo-app-github]: https://github.com/Microsoft/mindaro
[supported-regions]: https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service
[troubleshooting]: /azure/dev-spaces/troubleshooting#fail-to-restore-original-configuration-of-deployment-on-cluster
[visual-studio]: https://www.visualstudio.com/vs/
[btk-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.mindaro
[kubernetesLocalProcessConfig-yaml]: configure-bridge-to-kubernetes.md
[btk-overview-routing]: overview-bridge-to-kubernetes.md#using-routing-capabilities-for-developing-in-isolation

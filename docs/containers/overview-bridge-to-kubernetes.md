---
title: Como funciona a Ponte para Kubernetes
ms.technology: vs-azure
ms.date: 11/19/2020
ms.topic: conceptual
description: Descreve os processos para usar o Bridge para kubernetes para conectar seu computador de desenvolvimento ao cluster kubernetes
keywords: Ponte para kubernetes, Docker, kubernetes, Azure, contêineres
monikerRange: '>=vs-2019'
manager: jmartens
author: ghogen
ms.author: ghogen
ms.openlocfilehash: d44dc484da904d2692b90e23d10db6edc6f6e7b8
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223154"
---
# <a name="how-bridge-to-kubernetes-works"></a>Como funciona a Ponte para Kubernetes

O Bridge para o kubernetes permite que você execute e depure o código em seu computador de desenvolvimento, enquanto ainda está conectado ao cluster do kubernetes com o restante do seu aplicativo ou serviços. Por exemplo, se você tiver uma grande arquitetura de microserviços com muitos bancos de dados e serviços interdependentes, é difícil replicar essas dependências no seu computador de desenvolvimento. Além disso, a criação e a implantação de código em seu cluster kubernetes para cada alteração de código durante o desenvolvimento de loop interno podem ser lentas, demoradas e difíceis de usar com um depurador.

A ponte para o kubernetes evita que você precise compilar e implantar seu código no cluster, em vez de criar uma conexão diretamente entre o computador de desenvolvimento e o cluster. Conectar seu computador de desenvolvimento ao cluster durante a depuração permite que você teste e desenvolva rapidamente seu serviço no contexto do aplicativo completo sem criar nenhuma configuração de Docker ou kubernetes.

A ponte para o kubernetes redireciona o tráfego entre o cluster kubernetes conectado e o computador de desenvolvimento. Esse redirecionamento de tráfego permite que o código em seu computador de desenvolvimento e serviços em execução no cluster kubernetes se comuniquem como se estivessem no mesmo cluster kubernetes. O Bridge to kubernetes também fornece uma maneira de replicar as variáveis de ambiente e os volumes montados disponíveis para pods no seu cluster kubernetes em seu computador de desenvolvimento. Fornecer acesso a variáveis de ambiente e volumes montados em seu computador de desenvolvimento permite que você trabalhe rapidamente em seu código sem ter que replicar essas dependências manualmente.

> [!WARNING]
> O Bridge to kubernetes destina-se ao uso somente em cenários de desenvolvimento e teste. Ele não se destina ou tem suporte para uso com clusters de produção ou serviços dinâmicos em uso ativo.

## <a name="using-bridge-to-kubernetes"></a>Usando o Bridge para kubernetes

Para usar o Bridge para kubernetes no Visual Studio, você precisa do [visual studio 2019][visual-studio] versão 16,7 Preview 4 ou superior em execução no Windows 10 com a carga de trabalho de *desenvolvimento da web e do ASP.net* instalada e a [ponte para a extensão kubernetes][btk-extension] instalada. Ao usar o Bridge para kubernetes para estabelecer uma conexão com o cluster do kubernetes, você tem a opção de redirecionar todo o tráfego para e de um pod existente no cluster para seu computador de desenvolvimento.

> [!NOTE]
> Ao usar a ponte para kubernetes, será solicitado que você forneça o nome do serviço para redirecionar para o computador de desenvolvimento. Essa opção é uma maneira conveniente de identificar um pod para redirecionamento. Todo o redirecionamento entre o cluster kubernetes e o computador de desenvolvimento é para um pod.

Quando o Bridge para kubernetes estabelece uma conexão com o cluster, ele:

* Solicita que você configure o serviço a ser substituído no cluster, a porta no computador de desenvolvimento a ser usada para seu código e a tarefa de inicialização para seu código como uma ação única.
* Substitui o contêiner no pod no cluster por um contêiner de agente remoto que redireciona o tráfego para o computador de desenvolvimento.
* Executa o [kubectl Port-Forward][kubectl-port-forward] no computador de desenvolvimento para encaminhar o tráfego do seu computador de desenvolvimento para o agente remoto em execução no cluster.
* Coleta informações de ambiente do seu cluster usando o agente remoto. Essas informações de ambiente incluem variáveis de ambiente, serviços visíveis, montagens de volume e montagens secretas.
* Configura o ambiente no Visual Studio para que o serviço no seu computador de desenvolvimento possa acessar as mesmas variáveis como se estivesse em execução no cluster.
* Atualiza o arquivo de hosts para mapear serviços no cluster para endereços IP locais em seu computador de desenvolvimento. Essas entradas de arquivo de hosts permitem que o código em execução no computador de desenvolvimento faça solicitações a outros serviços em execução no cluster. Para atualizar o arquivo de hosts, o Bridge para kubernetes solicitará acesso de administrador em seu computador de desenvolvimento ao se conectar ao cluster.
* Inicia a execução e a depuração do código no computador de desenvolvimento. Se necessário, a ponte para o kubernetes liberará as portas necessárias no computador de desenvolvimento, interrompendo os serviços ou processos que estão usando essas portas no momento.

Depois de estabelecer uma conexão com o cluster, você pode executar e depurar o código nativamente em seu computador, sem a Containerização, e o código pode interagir diretamente com o restante do cluster. Qualquer tráfego de rede que o agente remoto recebe é redirecionado para a porta local especificada durante a conexão para que seu código em execução nativamente possa aceitar e processar esse tráfego. As variáveis de ambiente, os volumes e os segredos do seu cluster são disponibilizados para o código em execução no seu computador de desenvolvimento. Além disso, devido às entradas de arquivo de hosts e encaminhamento de porta adicionados ao computador do desenvolvedor por ponte para kubernetes, seu código pode enviar tráfego de rede para serviços em execução no cluster usando os nomes de serviço do cluster e esse tráfego é encaminhado para os serviços em execução no cluster. O tráfego é roteado entre o computador de desenvolvimento e o cluster todo o tempo que você está conectado.

Além disso, o Bridge para o kubernetes fornece uma maneira de replicar as variáveis de ambiente e os arquivos montados disponíveis para pods no seu cluster em seu computador de desenvolvimento por meio do `KubernetesLocalProcessConfig.yaml` arquivo. Você também pode usar esse arquivo para criar novas variáveis de ambiente e montagens de volume.

> [!NOTE]
> Para a duração da conexão com o cluster (mais 15 minutos adicionais), a ponte para kubernetes executa um processo chamado *EndpointManager* com permissões de administrador no computador local.

## <a name="additional-configuration-with-kuberneteslocalprocessconfigyaml"></a>Configuração adicional com KubernetesLocalProcessConfig. YAML

O `KubernetesLocalProcessConfig.yaml` arquivo permite replicar as variáveis de ambiente e os arquivos montados disponíveis para o pods em seu cluster. Para obter mais informações sobre as opções de configuração adicionais, consulte [Configure Bridge to kubernetes][using-config-yaml].

## <a name="using-routing-capabilities-for-developing-in-isolation"></a>Usando recursos de roteamento para o desenvolvimento em isolamento

Por padrão, a ponte para o kubernetes redireciona todo o tráfego de um serviço para o seu computador de desenvolvimento. Você também tem a opção de usar os recursos de roteamento para redirecionar apenas as solicitações para um serviço proveniente de um subdomínio para seu computador de desenvolvimento. Esses recursos de roteamento permitem que você use o Bridge para kubernetes para desenvolver em isolamento e evitar a interrupção de outro tráfego no cluster.

A animação a seguir mostra dois desenvolvedores que trabalham no mesmo cluster isoladamente:

![Isolamento animado de ilustração de GIF](media/bridge-to-kubernetes/btk-graphic-isolated.gif)

Quando você habilita o trabalho em isolamento, o Bridge to kubernetes faz o seguinte, além de se conectar ao seu cluster kubernetes:

* Verifica se o cluster kubernetes não tem Azure Dev Spaces habilitado.
* Replica o serviço escolhido no cluster no mesmo namespace e adiciona um rótulo *Routing.VisualStudio.Io/Route-from=service_name* e *Routing.VisualStudio.Io/Route-on-header=kubernetes-Route-as: GENERATED_NAME* anotação.
* Configura e inicia o Gerenciador de roteamento no mesmo namespace no cluster kubernetes. O Gerenciador de roteamento usa um seletor de rótulo para procurar o rótulo *Routing.VisualStudio.Io/Route-from=service_name* e  *Routing.VisualStudio.Io/Route-on-header=kubernetes-Route-as: GENERATED_NAME* anotação ao configurar o roteamento em seu namespace.

Se o Bridge para o kubernetes detectar que Azure Dev Spaces está habilitado no cluster do kubernetes, será solicitado que você desabilite Azure Dev Spaces antes de poder usar a ponte para o kubernetes.

O Gerenciador de roteamento faz o seguinte quando é iniciado:

* Duplica todas as insere (incluindo insere do balanceador de carga) encontradas no namespace usando o *GENERATED_NAME* para o subdomínio.
* Cria um pod Envoy para cada serviço associado ao insere duplicado com o subdomínio *GENERATED_NAME* .
* Cria um pod Envoy adicional para o serviço no qual você está trabalhando isoladamente. Isso permite que as solicitações com o subdomínio sejam roteadas para o computador de desenvolvimento.
* Configura as regras de roteamento para cada pod Envoy para manipular o roteamento de serviços com o subdomínio.

O diagrama a seguir mostra um cluster kubernetes antes que o Bridge para kubernetes se conecte ao seu cluster:

![Diagrama de cluster sem ponte para kubernetes](media/bridge-to-kubernetes/kubr-cluster.svg)

O diagrama a seguir mostra o mesmo cluster com ponte para kubernetes habilitado no modo de isolamento. Aqui, você pode ver o serviço duplicado e os pods Envoy que dão suporte ao roteamento em isolamento.

![Diagrama de cluster com ponte para kubernetes habilitado](media/bridge-to-kubernetes/kubr-cluster-devcomputer.svg)

Quando uma solicitação com o subdomínio *GENERATED_NAME* é recebida no cluster, um cabeçalho *kubernetes-Route-as = GENERATED_NAME* é adicionado à solicitação. O Envoy pods manipula o roteamento dessa solicitação para o serviço apropriado no cluster. Se a solicitação for roteada para o serviço que está sendo trabalhado no isolamento, essa solicitação será redirecionada para o computador de desenvolvimento pelo agente remoto.

Quando uma solicitação sem o subdomínio *GENERATED_NAME* é recebida no cluster, nenhum cabeçalho é adicionado à solicitação. O Envoy pods manipula o roteamento dessa solicitação para o serviço apropriado no cluster. Se a solicitação for roteada para o serviço que está sendo substituído, essa solicitação será roteada para o serviço original em vez do agente remoto.

> [!IMPORTANT]
> Cada serviço no cluster deve encaminhar o cabeçalho *kubernetes-Route-as = GENERATED_NAME* ao fazer solicitações adicionais. Por exemplo, quando o *servicea* recebe uma solicitação, ele faz uma solicitação para *serviceB* antes de retornar uma resposta. Neste exemplo, o *servicea* precisa encaminhar o cabeçalho *kubernetes-Route-as = GENERATED_NAME* em sua solicitação para *serviceB*. Algumas linguagens, como [ASP.net][asp-net-header], podem ter métodos para manipular a propagação do cabeçalho.

Quando você se desconecta do cluster, por padrão, a ponte para kubernetes removerá todos os pods de envoy e o serviço duplicado.

> [!NOTE]
> A implantação e o serviço do Gerenciador de roteamento permanecerão em execução no seu namespace. Para remover a implantação e o serviço, execute os comandos a seguir para seu namespace.
>
> ```azurecli
> kubectl delete deployment routingmanager-deployment -n NAMESPACE
> kubectl delete service routingmanager-service -n NAMESPACE
> ```

## <a name="diagnostics-and-logging"></a>Diagnóstico e registro em log

Ao usar o Bridge para kubernetes para se conectar ao cluster, os logs de diagnóstico do cluster são registrados no diretório *Temp* do seu computador de desenvolvimento na pasta *ponte para kubernetes* .

## <a name="rbac-authorization"></a>Autorização de RBAC

O kubernetes fornece o RBAC (controle de acesso baseado em função) para gerenciar permissões para usuários e grupos. Para obter informações, consulte a [documentação do kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) você pode definir as permissões para um cluster habilitado para RBAC criando um arquivo YAML e usando `kubectl` para aplicá-lo ao cluster. 

Para definir permissões no cluster, crie ou modifique um arquivo YAML, como *Permissions. yml* como o seguinte, usando seu próprio namespace para `<namespace>` e os assuntos (usuários e grupos) que precisam de acesso.

```yml
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: bridgetokubernetes-<namespace>
  namespace: development
subjects:
  - kind: User
    name: jane.w6wn8.k8s.ginger.eu-central-1.aws.gigantic.io
    apiGroup: rbac.authorization.k8s.io
  - kind: Group
    name: dev-admin
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: admin
  apiGroup: rbac.authorization.k8s.io
```

Aplique as permissões usando o comando:

```cmd
kubectl -n <namespace> apply -f <yaml file name>
```

## <a name="limitations"></a>Limitações

A ponte para o kubernetes tem as seguintes limitações:

* Um serviço deve ser apoiado por um único pod para se conectar a esse serviço. Você não pode se conectar a um serviço com vários pods, como um serviço com réplicas.
* Um pod pode ter apenas um único contêiner em execução nesse pod para que a ponte para kubernetes se conecte com êxito. A ponte para o kubernetes não pode se conectar a serviços com pods que têm contêineres adicionais, como contêineres sidecar injetados por malhas de serviços.
* Atualmente, a ponte para kubernetes pods deve ser contêineres do Linux. Contêineres do Windows não têm suporte.
* O isolamento não pode ser usado com HTTPS quando você usa a ponte para kubernetes com o Visual Studio. Somente há suporte para HTTPS no modo de isolamento quando você usa Visual Studio Code.
* O Bridge para kubernetes precisa de permissões elevadas para ser executado em seu computador de desenvolvimento para editar o arquivo de hosts.
* A ponte para kubernetes não pode ser usada em clusters com Azure Dev Spaces habilitado.

### <a name="bridge-to-kubernetes-and-clusters-with-azure-dev-spaces-enabled"></a>Ponte para kubernetes e clusters com Azure Dev Spaces habilitado

Não é possível usar a ponte para kubernetes em um cluster com Azure Dev Spaces habilitado. Se você quiser usar a ponte para kubernetes em um cluster com Azure Dev Spaces habilitado, será necessário desabilitar o Azure Dev Spaces antes de se conectar ao cluster.

## <a name="next-steps"></a>Próximas etapas

Para começar a usar o Bridge para kubernetes para se conectar ao seu computador de desenvolvimento local ao cluster, consulte [usar o Bridge para o kubernetes](bridge-to-kubernetes.md).

[asp-net-header]: https://www.nuget.org/packages/Microsoft.AspNetCore.HeaderPropagation/
[azds-cli]: /azure/dev-spaces/how-to/install-dev-spaces#install-the-client-side-tools
[azds-tmp-dir]: /azure/dev-spaces/troubleshooting#before-you-begin
[azure-cli]: /cli/azure/install-azure-cli?view=azure-cli-latest&preserve-view=true
[bridge-to-kubernetes-vs]: bridge-to-kubernetes.md
[kubectl-port-forward]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#port-forward
[visual-studio]: https://visualstudio.microsoft.com/downloads/
[btk-extension]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.mindaro
[using-config-yaml]: configure-bridge-to-kubernetes.md

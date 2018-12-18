---
title: Configurar controladores e agentes de teste para testes de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, test agents and controllers
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 363aac5bc07b49670cb35f5f1080f7835e7c4701
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895633"
---
# <a name="configure-test-agents-and-test-controllers-for-running-load-tests"></a>Configurar controladores e agentes de teste para executar testes de carga

O Visual Studio pode gerar uma carga simulada para seu aplicativo usando máquinas virtuais ou físicas. Esses computadores devem ser configurados como um único controlador de teste e um ou mais agentes de teste. Você pode usar o controlador de teste e os agentes de teste para gerar mais carga do que um único computador pode gerar sozinho.

> [!NOTE]
> Também é possível usar o teste de carga baseado em nuvem para fornecer máquinas virtuais que gerenciem a carga de muitos usuários que acessam o site ao mesmo tempo. Saiba mais sobre teste de carga baseado em nuvem em [Executar testes de carga usando o Azure Test Plans](/azure/devops/test/load-test/get-started-simple-cloud-load-test?view=vsts).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="load-simulation-architecture"></a>Arquitetura de simulação de carga

A arquitetura de simulação da carga consiste em um cliente do Visual Studio, um controlador de teste e agentes de teste.

-   O cliente é usado para desenvolver testes, executar testes e exibir resultados do teste.

-   O controlador de teste é usado para administrar os agentes de teste e coletar resultados do teste.

-   Os agentes de teste são usados para executar testes e coletar dados que incluem informações do sistema e dados de criação de perfil do ASP.NET definidos na configuração de teste.

Essa arquitetura oferece os seguintes benefícios:

- A capacidade de expandir a geração de carga incluindo agentes de teste adicionais em um controlador de teste.

- Flexibilidade para instalar o cliente, o controlador de teste e o software do agente de teste no mesmo computador ou em computadores diferentes. Por exemplo:

   **Configuração local:**

  - Machine1: Visual Studio, controlador, agente.

    ![Computador local usando controlador e agente](./media/load-test-configa.png)

    **Configuração remota típica:**

  - Machine1 e 2: Visual Studio (vários testadores podem usar o mesmo controlador).

  - Machine3: controlador (pode ter agentes instalados também).

  - Machine4-n: Agente ou agentes, todos associados ao controlador no Machine3.

    ![Computadores remotos usando controlador e agentes](./media/load-test-configb.png)

Mesmo que um controlador de teste normalmente gerencie diversos agentes de teste, um agente só pode ser associado a um único controlador. Cada agente de teste pode ser compartilhado por uma equipe de desenvolvedores. Essa arquitetura facilita aumentar o número de agentes de teste, gerando, assim, cargas maiores.

## <a name="test-agent-and-test-controller-interaction"></a>Interação entre o agente de teste e o controlador de teste

O controlador de teste gerencia um conjunto de agentes de teste para executar testes. O controlador de teste se comunica com os agentes de teste para iniciar testes, parar testes, acompanhar o status do agente de teste e coletar resultados de teste.

### <a name="test-controller"></a>Controlador de teste

O controlador de teste fornece uma arquitetura geral para executar testes e inclui recursos especiais para executar testes de carga. O controlador de teste envia o teste de carga para todos os agentes de teste e aguarda até que todos os agentes de teste tenham inicializado o teste. Quando todos os agentes de teste estiverem prontos, o controlador de teste enviará uma mensagem aos agentes de teste para iniciá-lo.

### <a name="test-agent"></a>Agente de teste

O agente de teste é executado como um serviço que escuta solicitações do controlador de teste para iniciar um novo teste. Quando um agente de teste recebe uma solicitação, o serviço do agente de teste inicia um processo no qual executa os testes. Cada agente de teste executa o mesmo teste de carga.

 Os agentes de teste recebem um peso do administrador, e a carga é distribuída de acordo com a importância de um agente de teste. Por exemplo, se o agente de teste 1 tiver uma importância 30, o agente de teste 2 tiver uma importância 70 e a carga estiver definida como 1.000 usuários, o agente de teste 1 simulará 300 usuários virtuais, e o agente de teste 2 simulará 700 usuários virtuais. Confira [Gerenciar controladores e agentes de teste com o Visual Studio](../test/manage-test-controllers-and-test-agents.md).

 O agente de teste utiliza um conjunto de testes e um conjunto de parâmetros de simulação como entrada. Um conceito fundamental é que os testes são independentes do computador em que são executados.

## <a name="test-controller-and-test-agent-connection-points"></a>Pontos de conexão entre o controlador de teste e o agente de teste

A ilustração a seguir mostra os pontos de conexão entre o controlador de teste, o agente de teste e o cliente. Ela descreve quais portas são usadas em conexões de entrada e saída, bem como restrições de segurança usadas nessas portas.

 ![Portas e segurança do controlador de teste e do agente de teste](./media/test-controller-agent-firewall.png)

 Para obter mais informações, confira [Configurar portas para controladores de teste e agentes de teste](../test/configure-ports-for-test-controllers-and-test-agents.md).

## <a name="test-controller-and-agent-installation-information"></a>Informações sobre a instalação do controlador e do agente de teste

Para obter informações importantes sobre os requisitos de hardware e software para controladores de teste e agentes de teste, os procedimentos para instalá-los e configurar o ambiente tendo em vista o desempenho ideal, consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).

## <a name="use-the-test-controller-and-test-agent-with-unit-tests"></a>Usar o agente de teste e o controlador de teste com testes de unidade

Depois de instalar um controlador de teste e um ou mais agentes, você poderá especificar se deseja usar uma execução remota com o controlador de teste na configuração de teste para os testes de carga. Além disso, você pode especificar os dados e os adaptadores de diagnóstico a serem usados com a função associada aos agentes na configuração de teste.

## <a name="see-also"></a>Consulte também

- [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md)
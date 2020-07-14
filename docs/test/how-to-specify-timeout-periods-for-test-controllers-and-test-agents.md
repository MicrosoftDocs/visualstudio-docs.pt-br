---
title: Períodos de tempo limite para controladores de teste e agentes de teste
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- agents, configuring
- agetns, timeouts
- controllers, configuring
- controllers, timeouts
ms.assetid: 777d0db5-0073-458a-a2a3-58b1c1f24c60
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7b06dc7d363cefd568a6e1432582744f486fa222
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287279"
---
# <a name="how-to-specify-timeout-periods-for-test-controllers-and-test-agents"></a>Como especificar períodos de tempo limite para controladores e agentes de teste

O controlador de teste e o agente de teste têm várias configurações de tempo limite que especificam quanto tempo devem aguardar por respostas um do outro, ou de uma fonte de dados antes de falhar com um erro. Em determinadas circunstâncias, pode ser necessário editar valores de tempo limite para atender às necessidades de sua topologia ou outros problemas de ambiente. Para editar os valores de tempo limite, edite o arquivo de configuração XML que está associado ao controlador de teste ou com o agente de teste, conforme abordado nos procedimentos a seguir.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Para editar várias configurações de tempo limite de um controlador de teste ou de um agente de teste, modifique os seguintes arquivos de configuração usando os nomes de chaves e valores nas tabelas:

- Controlador de teste: *QTController.exe.config*

    |Nome da chave|Descrição|Valor|
    |-|-----------------|-|
    |AgentConnectionTimeoutInSeconds|O número de segundos para aguardar a solicitação de ping do agente antes de a conexão ser considerada perdida.|"n" segundos.|
    |AgentSyncTimeoutInSeconds|Quando iniciar uma execução de teste de sincronização, número de segundos para aguardar a sincronização de todos os agentes antes de anular a execução.|"n" segundos.|
    |AgentInitializeTimeout|Número de segundos da espera pela inicialização de todos os agentes e seus coletores de dados no início de uma execução de teste, antes de cancelar a execução. Esse valor deverá ser bastante grande se forem usados coletores de dados.|"n" segundos. Padrão: "120" (dois minutos).|
    |AgentCleanupTimeout|Número de segundos da espera pela limpeza de todos os agentes e seus coletores de dados, antes de concluir a execução do teste. Esse valor deverá ser bastante grande se forem usados coletores de dados.|"n" segundos. Padrão: "120" (dois minutos).|

- Test Agent: *QTAgentService.exe.config*

    |Nome da chave|Descrição|Valor|
    |-|-----------------|-|
    |ControllerConnectionPeriodInSeconds|Número de segundos entre as tentativas de se conectar ao controlador.|"n" segundos. Padrão: "30" (trinta segundos).|
    |RemotingTimeoutSeconds|O tempo máximo que uma chamada remota pode durar em segundos.|"n" segundos. Padrão: "600" (dez minutos).|
    |StopTestRunCallTimeoutInSeconds|Número de segundos da espera pela interrupção da execução do teste pela chamada.|"n" segundos. Padrão: "120" (dois minutos).|
    |GetCollectorDataTimeout|Número de segundos da espera pelo coletor de dados.|"n" segundos. Padrão: "300" (cinco minutos).|

## <a name="to-specify-agent-timeout-options-for-a-test-controller"></a>Para especificar opções de tempo limite de agente para um controlador de teste

1. Abra o arquivo de configuração XML *QTCcontroller.exe.config* localizado em *% ProgramFiles (x86)% \ Microsoft Visual Studio\2017\Enterprise\Common7\IDE*.

2. Localize a marcação `<appSettings>`.

    ```xml
    <appSettings>
      <add key="LogSizeLimitInMegs" value="20"/>
      <add key="AgentConnectionTimeoutInSeconds" value="120"/>
      <add key="AgentSyncTimeoutInSeconds" value="300"/>
      <add key="ControllerServicePort" value="6901"/>
      <add key="ControllerUsersGroup" value="TeamTestControllerUsers"/>
      <add key="ControllerAdminsGroup" value="TeamTestControllerAdmins"/>
      <add key="CreateTraceListener" value="no"/>
    </appSettings>
    ```

3. Edite um valor existente para uma das chaves de tempo limite do controlador de teste. Por exemplo, você pode alterar o valor padrão da chave `AgentConnectionTimeoutInSeconds` de dois minutos para três minutos:

    ```xml
    <add key="AgentConnectionTimeoutInSeconds" value="180"/>
    ```

    -ou-

    Adicione uma chave extra e especifique um valor de tempo limite. Por exemplo, você pode adicionar a chave `AgentInitializeTimeout` na seção `<appSettings>` e especificar um valor de cinco minutos:

    ```xml
    <appSettings>
            <add key="AgentInitializeTimeout" value="300"/>
    </appSettings>
    ```

## <a name="to-specify-agent-timeout-options-for-a-test-agent"></a>Para especificar opções de tempo limite de agente para um agente de teste

1. Abra o arquivo de configuração XML *QTAgentService.exe.config* localizado em *% ProgramFiles (x86)% \ Microsoft Visual Studio\2017\Enterprise\Common7\IDE*.

2. Localize a marcação `<appSettings>`.

    ```xml
    <appSettings>
      <appSettings>
      <add key="LogSizeLimitInMegs" value="20"/>
      <add key="AgentServicePort" value="6910"/>
      <add key="ControllerConnectionPeriodInSeconds" value="30"/>
      <add key="StopTestRunCallTimeoutInSeconds" value="120"/>
      <add key="CreateTraceListener" value="no"/>
      <add key="GetCollectorDataTimeout" value="300"/>
    </appSettings>  </appSettings>
    ```

3. Edite um valor existente para uma das chaves de tempo limite do agente de teste. Por exemplo, você pode alterar o valor padrão da chave `ControllerConnectionPeriodInSeconds` de trinta segundos para um minuto:

    ```xml
    <add key="ControllerConnectionPeriodInSeconds" value="60"/>
    ```

    -ou-

    Adicione uma chave extra e especifique um valor de tempo limite. Por exemplo, você pode adicionar a chave `RemotingTimeoutSeconds` na seção `<appSettings>` e especificar um valor de quinze minutos:

    ```xml
    <appSettings>
            <add key=" RemotingTimeoutSeconds " value="900"/>
    </appSettings>
    ```

## <a name="see-also"></a>Veja também

- [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md)
- [Modificar configurações de registro em log de testes de carga](../test/modify-load-test-logging-settings.md)
- [Configurar portas para controladores e agentes de teste](../test/configure-ports-for-test-controllers-and-test-agents.md)
- [Como associar um controlador de teste ou um agente de teste a um adaptador de rede](../test/how-to-bind-a-test-controller-or-test-agent-to-a-network-adapter.md)

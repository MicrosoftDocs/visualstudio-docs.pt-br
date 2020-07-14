---
title: Associar um controlador de teste ou um agente de teste a um adaptador de rede
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- controllers, netwrok adapter
- agents, configuring
- agents, network adapter
- controllers, configuring
ms.assetid: 7eb9290a-f9f6-4e41-9caa-796fcfaf0610
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 925df819b903be3de3d44127243f3b18d1e9aff5
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288241"
---
# <a name="how-to-bind-a-test-controller-or-test-agent-to-a-network-adapter"></a>Como associar um controlador de teste ou agente de teste a um adaptador de rede

Se um computador com o software de controlador de teste ou agente de teste instalado tiver vários adaptadores de rede, você precisará especificar o endereço IP em vez do nome do computador para identificar o controlador ou agente de teste.

> [!WARNING]
> Quando tentar configurar um agente de teste, você pode receber o seguinte erro:
>
> **Erro 8110. Não é possível se conectar ao computador do controlador especificado ou acessar o objeto do controlador**
>
> Esse erro pode ser causado pela instalação do controlador de teste em um computador que tenha mais de um adaptador de rede. Também é possível instalar agentes com êxito e não ver esse problema até tentar executar um teste.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="bind-a-test-controller-to-a-specific-network-adapter"></a>Associar um controlador de teste a um adaptador de rede específico

### <a name="to-obtain-the-ip-addresses-of-the-network-adapters"></a>Para obter os endereços IP dos adaptadores de rede

1. No Microsoft Windows, escolha **Iniciar**, entre na caixa **Iniciar Pesquisa**, digite **cmd** e escolha **Enter**.

2. Digite **ipconfig/all**.

     Os endereços IP de seus adaptadores de rede são exibidos. Registre o endereço IP do adaptador de rede ao qual você deseja associar o controlador.

### <a name="to-bind-a-network-adapter-to-a-test-controller"></a>Para associar um adaptador de rede a um controlador de teste

1. No Microsoft Windows, escolha **Iniciar**, entre na caixa **Iniciar Pesquisa**, digite **services.cmd** e escolha **Enter**.

     A caixa de diálogo **Serviços** é exibida.

2. No painel de resultados, na coluna **Nome**, clique com o botão direito do mouse no serviço **Controlador de Teste do Visual Studio** e escolha **Parar**.

     -ou-

     Abra um prompt de comando elevado e execute o seguinte comando em um comando:

     `net stop vsttcontroller`

3. Abra o arquivo de configuração XML *QTCcontroller.exe.config* localizado em *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\\\<edition>\Common7\IDE*.

4. localize a marca `<appSettings>`.

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

5. Adicione a chave `BindTo` para especificar qual adaptador de rede será usado na seção `<appSettings>`.

    ```xml
            <add key="BindTo" value="<YOUR IP ADDRESS>"/>
    </appSettings>
    ```

6. Inicie o serviço do controlador de teste. Para fazer isso, execute o seguinte comando em um prompt de comando:

    `net start vsttcontroller`

    > [!WARNING]
    > Você deve executar a instalação do agente de teste novamente para conectar o agente de teste ao controlador. Desta vez, especifique o endereço IP do controlador em vez do nome do controlador.

     Isso se aplica ao controlador, ao serviço de agente e ao processo de agente. A propriedade `BindTo` deve ser definida para cada processo em execução em um computador que tem mais de um adaptador de rede. O procedimento para definir a propriedade `BindTo` é o mesmo para todos os três processos, como especificado anteriormente neste tópico para o controlador de teste.

### <a name="to-bind-a-network-interface-card-to-a-test-agent"></a>Para associar um cartão de interface de rede ao agente de teste

1. No Microsoft Windows, escolha **Iniciar**, entre na caixa **Iniciar Pesquisa**, digite **services.cmd** e escolha **Enter**.

    A caixa de diálogo **Serviços** é exibida.

2. No painel de resultados, na coluna **Nome**, clique com o botão direito do mouse no serviço **Agente de Teste do Visual Studio** e escolha **Parar**.

     -ou-

     Abra um prompt de comando elevado e execute o seguinte comando em um comando:

     **net stop vsttagent**

3. Abra o arquivo de configuração XML *QTAgentService.exe.config* localizado em *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\\\<edition>\Common7\IDE*.

4. localize a marca `<appSettings>`.

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

5. Adicione a chave `BindTo` para especificar qual adaptador de rede será usado na seção `<appSettings>`.

    ```xml
            <add key="BindTo" value="<YOUR IP ADDRESS>"/>
    </appSettings>
    ```

6. Inicie o serviço do agente de teste. Para fazer isso, execute o seguinte comando em um prompt de comando:

    `net start vsttagent`

## <a name="see-also"></a>Veja também

- [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md)
- [Modificar configurações de registro em log de testes de carga](../test/modify-load-test-logging-settings.md)
- [Configurar portas para controladores e agentes de teste](../test/configure-ports-for-test-controllers-and-test-agents.md)
- [Como especificar períodos de tempo limite para controladores de teste e agentes de teste](../test/how-to-specify-timeout-periods-for-test-controllers-and-test-agents.md)

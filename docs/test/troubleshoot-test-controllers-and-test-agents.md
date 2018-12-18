---
title: Solução de problemas com controladores e agentes de teste
ms.date: 10/20/2016
ms.topic: troubleshooting
helpviewer_keywords:
- load tests, test controllers
- load tests, troubleshooting
- load tests, test agents
- troubleshooting, test controllers and agents in load tests
ms.assetid: 77329348-3a5d-43de-b6cb-90f93296a081
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 274585d864393877b225fe6231c1f775342620f6
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894736"
---
# <a name="strategies-for-troubleshooting-test-controllers-and-test-agents-in-load-tests"></a>Estratégias para solução de problemas em controladores e agentes de teste em testes de carga

Este artigo aborda alguns problemas comuns que você pode encontrar ao trabalhar com controladores e agentes de teste no Visual Studio.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

##  <a name="unable-to-collect-performance-counters-on-test-agent-computer"></a>Não é possível coletar contadores de desempenho no computador do agente de teste

Ao executar um teste de carga, você pode receber erros ao tentar se conectar a um computador do agente de teste e coletar contadores de desempenho. O serviço Registro Remoto é o serviço responsável por fornecer dados do contador de desempenho a um computador remoto. Em alguns sistemas operacionais, o serviço Registro Remoto não é iniciado automaticamente. Para corrigir esse problema, inicie manualmente o serviço Registro Remoto.

> [!NOTE]
> É possível acessar o serviço Registro Remoto no **Painel de Controle.** Escolha **Ferramentas Administrativas** e **Serviços**.

Outra causa desse problema é que você não tem permissões suficientes para ler os contadores de desempenho. Para execuções de teste locais, a conta de usuário que está executando o teste deverá ser membro do grupo Usuários Avançados ou superior, ou ser membro do grupo Usuários do Monitor de Desempenho. Para execuções de teste remotas, a conta que o controlador está configurado para executar deve ser membro do grupo Usuários Avançados ou superior, ou ser membro do grupo Usuários do Monitor de Desempenho.

## <a name="set-the-logging-level-on-a-test-controller-computer"></a>Definir o nível de log em um computador do controlador de teste

Você pode controlar o nível de registro em log em um computador do controlador de teste. Isso é útil quando você está tentando diagnosticar um problema ao executar um teste de carga em um ambiente.

### <a name="to-set-the-logging-level-on-a-test-controller-computer"></a>Para definir o nível de registro em log em um computador do controlador de teste

1.  Interrompa o serviço do controlador de teste. Em um prompt de comando, digite `net stop vsttcontroller`.

2.  Abra o arquivo *QTController.exe.config*. Esse arquivo está localizado no diretório de instalação do controlador.

3.  Edite a entrada da opção `EqtTraceLevel` na seção de diagnóstico do sistema do arquivo. Seu código deve se parecer com este:

    ```xml
    <system.diagnostics>
        <trace autoflush="true" indentsize="4">
            <listeners>
                <add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="d:\VSTestHost.log" />
            </listeners>
        </trace>
        <switches>
            <!-- You must use integral values for "value":
                    0 = off,
                    1 = error,
                    2 = warn,
                    3 = info,
                    4 = verbose. -->
            <add name="EqtTraceLevel" value="4" />
        </switches>
    </system.diagnostics>
    ```

4.  Salve o arquivo.

5.  Inicie o serviço do controlador. Em um prompt de comando, digite `net start vsttcontroller`.

Isso se aplica ao controlador de teste, ao serviço do agente de teste e ao processo do agente de teste. Ao diagnosticar problemas, é útil habilitar o registro em log desses três processos. O procedimento para definir o nível de registro em log é o mesmo para os três processos, conforme especificado anteriormente para o controlador de teste. Para definir níveis de registro em log para o serviço do agente de teste e o processo de agente, use os seguintes arquivos de configuração:

-   *QTController.exe.config* Serviço do controlador

-   *QTAgentService.exe.config* Serviço do agente

-   *QTDCAgent(32).exe.config* Processo do adaptador de dados do agente para uma arquitetura de 32 bits.

-   *QTDCAgent(64).exe.config* Processo do adaptador de dados do agente para uma arquitetura de 64 bits.

-   *QTAgent(32).exe.config* Processo de teste do agente para uma arquitetura de 32 bits.

-   *QTAgent(64).exe.config* Processo de teste do agente para uma arquitetura de 64 bits.

## <a name="bind-a-test-controller-to-a-network-adapter"></a>Associar um controlador de teste a um adaptador de rede

Quando tentar configurar um agente de teste, você pode receber o seguinte erro:

**Erro 8110. Não é possível se conectar ao computador do controlador especificado nem acessar o objeto do controlador.**

Esse erro pode ser causado pela instalação do controlador de teste em um computador que tenha mais de um adaptador de rede.

> [!NOTE]
> Também é possível instalar agentes de teste com êxito e não ver esse problema até tentar executar um teste.

Para corrigir este erro, você deve associar o controlador de teste a um dos adaptadores de rede. Você precisa definir a propriedade `BindTo` no controlador de teste e alterar o agente de teste para se referir ao controlador de teste por endereço IP, e não por nome. As etapas são fornecidas nos procedimentos a seguir.

### <a name="to-obtain-the-ip-address-of-the-network-adapter"></a>Para obter o endereço IP do adaptador de rede

1.  Escolha **Iniciar** e **Executar**.

     A caixa de diálogo **Executar** é exibida.

2.  Digite `cmd` e escolha **OK**.

     Um prompt de comando é aberto.

3.  Digite `ipconfig /all` no terminal integrado.

     Os endereços IP de seus adaptadores de rede são exibidos. Registre o endereço IP do adaptador de rede ao qual você deseja associar o controlador.

### <a name="to-bind-a-test-controller-to-a-network-adapter"></a>Para associar um controlador de teste a um adaptador de rede

1.  Interrompa o serviço do controlador de teste. Em um prompt de comando, digite `net stop vsttcontroller`.

2.  Abra o arquivo *QTController.exe.config*. Esse arquivo está localizado em *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE*.

3.  Adicione uma entrada para a propriedade `BindTo` nas configurações do aplicativo. Especifique o endereço IP do adaptador de rede ao qual deseja associar o controlador. Seu código deve se parecer com este:

    ```xml
    <appSettings>
        <add key="LogSizeLimitInMegs" value="20" />
        <add key="AgentSyncTimeoutInSeconds" value="120" />
        <add key="ControllerServicePort" value="6901" />
        <add key="ControllerUsersGroup" value="TeamTestControllerUsers" />
        <add key="ControllerAdminsGroup" value="TeamTestControllerAdmins" />
        <add key="CreateTraceListener" value="no" />
        <add key="BindTo" value="<YOUR IP ADDRESS>" />
    </appSettings>
    ```

4.  Salve o arquivo.

5.  Inicie o serviço do controlador de teste. Em um prompt de comando, digite `net start vsttcontroller`.

### <a name="to-connect-a-test-agent-to-a-bound-controller"></a>Para conectar um agente de teste a um controlador associado

-   Execute a instalação do agente de teste novamente. Dessa vez, especifique o endereço IP do controlador de teste em vez do nome do controlador de teste.

Isso se aplica ao controlador de teste, ao serviço do agente de teste e ao processo do agente de teste. A propriedade `BindTo` deve ser definida para cada processo em execução em um computador que tem mais de um adaptador de rede. O procedimento para definir a propriedade `BindTo` é o mesmo para os três processos, conforme especificado anteriormente para o controlador de teste. Para definir os níveis de log para o serviço e o processo do agente de teste, use os arquivos de configuração listados em [Definir o nível de log em um computador do controlador de teste](#set-the-logging-level-on-a-test-controller-computer).

## <a name="see-also"></a>Consulte também

- [Controladores e agentes de teste](../test/configure-test-agents-and-controllers-for-load-tests.md)

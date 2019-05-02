---
title: Configurar portas para controladores e agentes de teste
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- firewalls, configuring for test agents
- firewalls, configuring for test controllers
- test agents, firewalls
- test controllers, firewalls
- agents, firewalls
- controllers, firewalls
ms.assetid: 211edbd7-9fe4-4251-ba85-8bec4363261b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bd66bcb3615477abc2fc9a8122f2ec4675f37bbb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62965637"
---
# <a name="configure-ports-for-test-controllers-and-test-agents"></a>Configurar portas para controladores e agentes de teste

Você pode alterar as portas de entrada padrão usadas pelo controlador de teste, pelo agente de teste e pelo cliente. Isso poderá ser necessário se você estiver tentando usar o controlador de teste, o agente de teste ou o cliente com qualquer outro software que esteja em conflito com as configurações de porta. Outro motivo para alterar as portas é devido à restrição de firewall entre o controlador de teste e o cliente. Nesse caso, você talvez queira configurar manualmente a porta para acomodar a habilitação dela para um firewall de forma que o controlador de teste possa enviar resultados para o cliente.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

A ilustração a seguir mostra os pontos de conexão entre o controlador de teste, o agente de teste e o cliente. Ela descreve quais portas são usadas em conexões de entrada e saída, bem como restrições de segurança usadas nessas portas.

![Portas e segurança do controlador de teste e do agente de teste](../test/media/test-controller-agent-firewall.png)

## <a name="incoming-connections"></a>Conexões de entrada

A porta padrão usada pelo controlador de teste é 6901 e a porta padrão do agente de teste é 6910. O cliente usa uma porta aleatória por padrão, usada para receber os resultados de teste do controlador de teste. Em todas as conexões de entrada, o controlador de teste autentica a parte que está chamando e verifica se ela pertence a um grupo de segurança específico.

- **Controlador de teste** As conexões de entrada estão na porta TCP 6901. Se precisar, você poderá configurar a porta de entrada. Para saber mais, confira [Configurar as portas de entrada](#configure-the-incoming-ports).

    O controlador de teste precisa conseguir estabelecer a conexão de saída com agentes de teste e com o cliente.

    > [!NOTE]
    > O controlador de teste precisa de uma conexão de entrada de **Compartilhamento de Arquivos e Impressoras** aberta.

- **Agente de teste** As conexões de entrada estão na porta TCP 6910. Se precisar, você poderá configurar a porta de entrada. Para saber mais, confira [Configurar as portas de entrada](#configure-the-incoming-ports).

   O agente de teste precisa conseguir estabelecer conexão de saída com o controlador de teste.

- **Cliente** Por padrão, uma porta TCM aleatória é usada em conexões de entrada. Se precisar, você poderá configurar a porta de entrada. Para saber mais, confira [Configurar as portas de entrada](#configure-the-incoming-ports).

   Você poderá receber notificações de firewall quando o controlador de teste tentar se conectar ao cliente pela primeira vez.

   No Windows Server 2008, as notificações de firewall permanecem desabilitadas por padrão e você deve adicionar manualmente exceções de firewall para programas cliente (*devenv.exe*, *mstest.exe*, *mlm.exe*) para que seja possível aceitar conexões de entrada.

## <a name="outgoing-connections"></a>Conexões de saída

Portas TCP aleatórias são usadas em todas as conexões de saída.

- **Controlador de teste** O controlador de teste precisa conseguir estabelecer a conexão de saída com os agentes e o cliente.

- **Agente de teste** O agente de teste precisa conseguir estabelecer a conexão de saída com o controlador.

- **Cliente** O cliente precisa conseguir estabelecer a conexão de saída com o controlador.

## <a name="configure-the-incoming-ports"></a>Configurar as portas de entrada

Siga as instruções para configurar as portas para um controlador de testes e agentes de teste.

- **Serviço de Controlador** Modifique o valor da porta editando o arquivo *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\QTCcontroller.exe.config*:

    ```xml
    <appSettings>
      <add key="ControllerServicePort" value="6901"/>
    </appSettings>
    ```

- **Serviço de Agente** Modifique o valor da porta editando o arquivo *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\QTAgentService.exe.config*:

    ```xml
    <appSettings>
      <add key="AgentServicePort" value="6910"/>
    </appSettings>
    ```

- **Cliente** Use o editor de registro para adicionar os seguintes valores de registro (**DWORD**). O cliente usará uma das portas do intervalo especificado para receber dados do controlador de teste:

     **HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\VisualStudio\12.0\EnterpriseTools\QualityTools\ListenPortRange\PortRangeStart**

     **HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\VisualStudio\12.0\EnterpriseTools\QualityTools\ListenPortRange\PortRangeEnd**

## <a name="see-also"></a>Consulte também

- [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md)
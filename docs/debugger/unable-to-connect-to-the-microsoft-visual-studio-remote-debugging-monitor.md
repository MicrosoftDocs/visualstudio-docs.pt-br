---
title: Não é possível conectar o Monitor de depuração remota do Studio Visual da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.remote_debug
- vs.debug.error.firewall.remotemachine
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1096188a6cf6be34d56c6330d588e56e0c306581
ms.sourcegitcommit: 50b19010b2e2b4736835350710e2edf93b980b56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2018
ms.locfileid: "49073929"
---
# <a name="unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor"></a>Não foi possível se conectar ao Monitor de Depuração Remota do Microsoft Visual Studio
Essa mensagem pode ocorrer porque o monitor de depuração remota não está corretamente configurado no computador remoto ou o computador remoto está inacessível devido a problemas de rede ou a presença de um firewall.
  
> [!IMPORTANT]
>  Se você acredita ter recebido esta mensagem devido a um bug do produto, por favor [relate este problema](../ide/how-to-report-a-problem-with-visual-studio-2017.md) para o Visual Studio. Se você precisar de mais ajuda, consulte [Fale conosco](../ide/talk-to-us.md) maneiras de entrar em contato com a Microsoft.

## <a name="specificerrors"></a>O que é a mensagem de erro detalhadas?

O `Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor` mensagem é genérica. Normalmente, uma mensagem mais específica está incluída na cadeia de caracteres de erro e que podem ajudá-lo a identificar a causa do problema ou pesquisar para uma correção mais exata. Aqui estão algumas das mensagens de erro mais comuns que são acrescentadas à mensagem de erro principal:

- [O depurador não pode se conectar ao computador remoto. O depurador não conseguiu resolver o nome do computador especificado](#cannot_connect)
- [Solicitação de Conexão foi rejeitada pelo depurador remoto](#rejected)
- [Acesso inválido ao local de memória](#invalid_access)
- [Não há nenhum servidor pelo nome especificado em execução no computador remoto](#no_server)
- [O nome solicitado era válido, mas nenhum dado do tipo solicitado foi encontrado](#valid_name)
- [O depurador remoto Visual Studio no computador de destino não é possível conectar-se reconectar a este computador](#cant_connect_back)
- [Acesso negado](#access_denied)
- [Ocorreu um erro específico do pacote de segurança](#security_package)

## <a name="cannot_connect"></a> O depurador não pode se conectar ao computador remoto. O depurador não conseguiu resolver o nome do computador especificado

Repita estas etapas:

1. Certifique-se de que você insira um nome de computador válido e o número da porta na **anexar ao processo** caixa de diálogo ou nas propriedades do projeto (para definir propriedades, consulte [essas etapas](#server_incorrect)). O nome do computador deve ser o seguinte formato:

    `computername:port`

    > [!NOTE]
    > O número da porta deve coincidir com o [número do depurador remoto da porta](../debugger/remote-debugger-port-assignments.md), que *deve estar em execução* no computador de destino.

2. Se o nome do computador não funcionar, tente o endereço IP e número da porta em vez disso.

3. Certifique-se de que a versão do depurador remoto em execução no computador de destino corresponde à sua versão do Visual Studio. Para obter a versão correta do depurador remoto, consulte [depuração remota](../debugger/remote-debugging.md).

    > [!TIP]
    > Se você estiver anexando ao processo e você se conectar com êxito, mas não vejo o processo que você deseja, selecione a **Mostrar processos de caixa de seleção de todos os usuários**. Isso mostrará processos se você estiver conectado em uma conta de usuário diferente.

4. Se essas etapas não resolverem esse erro, consulte [o computador remoto não está acessível](#dns).

## <a name="rejected"></a> Solicitação de Conexão foi rejeitada pelo depurador remoto

No **anexar ao processo** caixa de diálogo caixa ou nas propriedades do projeto, certifique-se de que o nome do computador remoto e o número da porta corresponde ao número de porta e o nome mostrado na janela do depurador remoto. Se estiver incorreta, corrija e tente novamente.

Se esses valores estão corretos e a mensagem menciona **autenticação do Windows** modo, verifique se o depurador remoto está no modo de autenticação correto (**Ferramentas > Opções**).

## <a name="invalid_access"></a> Acesso inválido ao local de memória

Ocorreu um erro interno. Reinicie o Visual Studio e tente novamente.

## <a name="no_server"></a> Não há nenhum servidor pelo nome especificado em execução no computador remoto

Visual Studio não pôde se conectar ao depurador remoto. Essa mensagem pode ocorrer por vários motivos:

- O depurador remoto pode estar em execução em uma conta de usuário diferente. Consulte [estas etapas](#user_accounts)

- A porta está bloqueada no firewall. Verifique se o firewall está [sua solicitação de bloqueio não](#firewall), especialmente se você estiver usando um firewall de terceiros.

- A versão do depurador remoto não coincide com o Visual Studio. Para obter a versão correta do depurador remoto, consulte [depuração remota](../debugger/remote-debugging.md)


## <a name="valid_name"></a> O nome solicitado era válido, mas nenhum dado do tipo solicitado foi encontrado

O computador remoto existe, mas o Visual Studio não pôde se conectar ao depurador remoto. Essa mensagem pode ocorrer por vários motivos:

- Um problema de DNS está impedindo a conexão. Ver [essas etapas](#dns).

- O depurador remoto pode estar em execução em uma conta de usuário diferente. Siga [essas etapas](#user_accounts).

- A porta está bloqueada no firewall. Verifique se o firewall está [sua solicitação de bloqueio não](#firewall), especialmente se você estiver usando um firewall de terceiros.

- A versão do depurador remoto não coincide com o Visual Studio. Para obter a versão correta do depurador remoto, consulte [depuração remota](../debugger/remote-debugging.md).

## <a name="cant_connect_back"></a> O depurador remoto Visual Studio no computador de destino não é possível conectar-se reconectar a este computador

O depurador remoto pode estar em execução em uma conta de usuário diferente. No depurador remoto, abra **Ferramentas > permissões** para adicionar o usuário para permissões de usuário do depurador remoto. Para obter mais informações, consulte [o depurador remoto está em execução em uma conta de usuário diferente](#user_accounts).

Se a mensagem de erro também menciona um firewall, o firewall no computador local pode estar impedindo a comunicação do computador remoto para o Visual Studio. Ver [essas etapas](#firewall).

## <a name="access_denied"></a> Acesso negado

Você poderá ver esse erro se você tentar depurar em um computador remoto de 64 bits em um computador de 32 bits (sem suporte).

## <a name="security_package"></a> Ocorreu um erro específico do pacote de segurança

Isso pode ser um problema de herdados específico para o Windows XP e Windows 7. Consulte este [informações](https://stackoverflow.com/questions/4786016/unable-to-connect-to-the-microsoft-remote-debugging-monitor-a-security-package). 

## <a name="causes-and-recommendations"></a>As causas e as recomendações

### <a name="dns"></a> O computador remoto não está acessível 

Se você não pode se conectar usando o nome do computador remoto, tente usar o endereço IP. Você pode usar `ipconfig` em uma linha de comando no computador remoto para obter o endereço IPv4. Se você estiver usando um arquivo de HOSTS, verifique se ele está configurado corretamente.

Se isso falhar, verifique se o computador remoto está acessível na rede ([ping](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee624059(v=ws.10)) máquina remota). Não há suporte para a depuração remota pela Internet, exceto em alguns cenários do Microsoft Azure.
  
### <a name="server_incorrect"></a> O nome do servidor está incorreto ou software de terceiros está interferindo com o depurador remoto

No Visual Studio, examine as propriedades do projeto e verifique se que o nome do servidor está correto. Consulte os tópicos para [em C# e Visual Basic](../debugger/remote-debugging-csharp.md#remote_csharp) e [C++](../debugger/remote-debugging-cpp.md#remote_cplusplus). Para o ASP.NET, abra **propriedades / Web / servidores** ou **propriedades / Depurar** dependendo do seu tipo de projeto.

> [!NOTE]
> Se você estiver anexando ao processo, as configurações remotas nas propriedades do projeto não são usadas.

Se o nome do servidor está correto, um firewall de terceiros ou de seu software antivírus pode estar bloqueando o depurador remoto. Quando estiver depurando localmente, isso pode acontecer porque o Visual Studio é um aplicativo de 32 bits, portanto, ele usa a versão de 64 bits do depurador remoto para depurar aplicativos de 64 bits. Os processos de 32 bits e 64 bits se comunicam usando a rede local no computador local. Nenhum tráfego de rede deixa o computador, mas é possível que o software de segurança de terceiros pode bloquear a comunicação.

### <a name="user_accounts"></a> O depurador remoto está em execução em uma conta de usuário diferente 

O depurador remoto, por padrão, só aceitará conexões de usuário que iniciou o depurador remoto e os membros do grupo Administradores. Usuários adicionais devem ser explicitamente concedidos permissões. 
 
Você pode resolver isso em uma das seguintes maneiras:  

-   Adicionar usuário do Visual Studio para permissões de usuário do depurador remoto (na janela do depurador remoto, escolha **Ferramentas > permissões**).

-   No computador remoto, reinicie o depurador remoto sob a mesma conta de usuário e senha que você está usando no computador do Visual Studio.

    > [!NOTE]
    > Se você estiver executando o depurador remoto em um servidor remoto, o aplicativo depurador remoto com o botão direito e escolha **executar como administrador** (ou, você pode executar o depurador remoto como um serviço). Se você não estiver executando-lo em um servidor remoto, apenas iniciá-lo normalmente.
  
-   Você pode iniciar o depurador remoto na linha de comando com o **/Allow \<nome de usuário >** parâmetro: `msvsmon /allow <username@computer>`. 
  
-   Como alternativa, você pode permitir que qualquer usuário faça a depuração remota. Na janela do depurador remoto, vá para o **Ferramentas > Opções** caixa de diálogo. Quando você seleciona **sem autenticação**, em seguida, você pode verificar **permitem que qualquer usuário depure**. No entanto, você deve tentar esta opção apenas se as demais opções falhem ou se você estiver usando uma rede privada.

### <a name="firewall"></a> O firewall no computador remoto não permite conexões de entrada para o depurador remoto  
 O firewall no computador do Visual Studio e o firewall no computador remoto devem ser configurados para permitir a comunicação entre o Visual Studio e o depurador remoto. Para obter informações sobre as portas que o depurador remoto está usando, consulte [as atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md). Para obter informações sobre como configurar o firewall do Windows, consulte [configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md).
  
### <a name="the-version-of-the-remote-debugger-doesnt-match-the-version-of-visual-studio"></a>A versão do depurador remoto não corresponde à versão do Visual Studio  
 A versão do Visual Studio que você estiver executando localmente precisa corresponder à versão do monitor de depuração remota que está em execução no computador remoto. Para corrigir esse problema, baixe e instale a versão correspondente do monitor de depuração remota. Para obter a versão correta do depurador remoto, consulte [depuração remota](../debugger/remote-debugging.md).
  
### <a name="the-local-and-remote-machines-have-different-authentication-modes"></a>As máquinas locais e remotas têm diferentes modos de autenticação  
 As máquinas locais e remotas precisam usar o mesmo modo de autenticação. Para corrigir esse problema, certifique-se de que ambos os computadores estão usando o mesmo modo de autenticação. Você pode alterar o modo de autenticação. Na janela do depurador remoto, vá para o **Ferramentas > Opções** caixa de diálogo.
  
 Para obter mais informações sobre modos de autenticação, consulte [visão geral da autenticação do Windows](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831472(v=ws.11)).   
  
### <a name="anti-virus-software-is-blocking-the-connections"></a>Um software antivírus está bloqueando as conexões  
 Software de antivírus do Windows permite conexões do depurador remoto, mas alguns softwares antivírus de terceiros podem bloqueá-los. Verifique a documentação do seu software antivírus saber como permitir que essas conexões.  
  
### <a name="network-security-policy-is-blocking-communication-between-the-remote-machine-and-visual-studio"></a>Política de segurança de rede está bloqueando a comunicação entre o computador remoto e o Visual Studio  
 Revise a segurança de sua rede para certificar-se de que ele não está bloqueando a comunicação. Para obter mais informações sobre a política de segurança de rede do Windows, consulte [configurações de política de segurança](/windows/device-security/security-policy-settings/security-policy-settings).  
  
### <a name="the-network-is-too-busy-to-support-remote-debugging"></a>A rede está muito ocupada para dar suporte à depuração remota  
 Você talvez precise fazer a depuração remota em um momento diferente ou reagendar o trabalho na rede para um momento diferente.  
  
## <a name="more-help"></a>Mais ajuda  
 Para obter ajuda do depurador mais remota, abra a página de Ajuda do depurador remoto (**Ajuda > uso** no depurador remoto).
  
## <a name="see-also"></a>Consulte também  
 [Depuração remota](../debugger/remote-debugging.md)

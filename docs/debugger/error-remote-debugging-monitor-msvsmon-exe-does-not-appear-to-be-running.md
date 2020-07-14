---
title: Erro-o Monitor de Depuração Remota de Microsoft Visual Studio (MSVSMON.EXE) não parece estar em execução no computador remoto.
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.server_machine_no_default
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6ba7fb30bcb5ac04a823b4ba654382ac23a966fe
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460605"
---
# <a name="error-the-microsoft-visual-studio-remote-debugging-monitor-msvsmonexe-does-not-appear-to-be-running-on-the-remote-computer"></a>Erro: o Monitor de Depuração Remota do Microsoft Visual Studio (MSVSMON.EXE) parece não estar sendo executado no computador remoto.
Essa mensagem de erro significa que o Visual Studio não pôde localizar a instância correta do Visual Studio Monitor de Depuração Remota no computador remoto. O Monitor de Depuração Remota do Visual Studio deve ser instalado para que a depuração remota funcione. Para obter informações sobre como baixar e configurar o depurador remoto, consulte [depuração remota](../debugger/remote-debugging.md).

> [!IMPORTANT]
> Se você acreditar que recebeu esta mensagem por causa de um bug do produto, [relate esse problema ao Visual Studio](../ide/how-to-report-a-problem-with-visual-studio.md). Se precisar de mais ajuda, consulte [Fale conosco](../ide/feedback-options.md) para obter formas de entrar em contato com a Microsoft.

## <a name="i-got-this-message-while-i-was-debugging-in-visual-studio-2010-or-earlier"></a>Eu recebi essa mensagem enquanto estava Depurando no Visual Studio 2010 ou anterior
 Se a versão do Visual Studio que você está usando for o Visual Studio 2010 ou anterior, você também poderá receber esse erro se o compartilhamento de arquivos e impressoras não estiver habilitado. Para saber mais sobre esse problema, veja a versão do Visual Studio 2010 desta documentação: [erro: o monitor de depuração remota de Microsoft Visual Studio (MSVSMON.EXE) não parece estar em execução no computador remoto.-Visual Studio 2010](/previous-versions/visualstudio/visual-studio-2010/ms164726(v=vs.100))

## <a name="i-got-this-message-while-i-was-debugging-locally"></a>Recebi essa mensagem enquanto eu estava Depurando localmente
 Se você estiver recebendo essa mensagem enquanto estiver Depurando localmente, o software antivírus ou um firewall de terceiros poderá ser a culpa. O Visual Studio é um aplicativo de 32 bits, portanto, ele usa a versão de 64 bits do depurador remoto para depurar aplicativos de 64 bits. Os dois processos se comunicam usando a rede local no computador local. Nenhum tráfego deixa o computador, mas é possível que softwares de segurança de terceiros possam bloquear a comunicação.

 As seções a seguir listam algumas outras razões pelas quais você pode ter chegado a essa mensagem e o que você pode fazer para corrigir o problema.

## <a name="the-remote-machine-is-not-reachable"></a>O computador remoto não está acessível
 Tente [executar o ping](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee624059(v=ws.10)) no computador remoto. Se ele não responder ao ping, as ferramentas remotas não poderão se conectar. Tente reinicializar o computador remoto e, caso contrário, verifique se ele está configurado corretamente na rede.

## <a name="the-version-of-the-remote-debugger-doesnt-match-the-version-of-visual-studio"></a>A versão do depurador remoto não corresponde à versão do Visual Studio
 A versão do Visual Studio que você está executando localmente precisa corresponder à versão do monitor de depuração remota em execução no computador remoto. Para corrigir isso, baixe e instale a versão correspondente do monitor de depuração remota. Vá para o [centro de download](https://www.microsoft.com/download) para encontrar a versão correta do depurador remoto.

## <a name="the-local-and-remote-machines-have-different-authentication-modes"></a>As máquinas locais e remotas têm modos de autenticação diferentes
 Os computadores locais e remotos precisam usar o mesmo modo de autenticação. Para corrigir isso, verifique se ambos os computadores estão usando o mesmo modo de autenticação. Para obter mais informações sobre modos de autenticação, consulte [visão geral da autenticação do Windows](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831472(v=ws.11)).

## <a name="the-remote-debugger-is-running-under-a-different-user-account"></a>O depurador remoto está sendo executado em uma conta de usuário diferente
 Você pode resolver isso de uma das seguintes maneiras:

- Você pode interromper o depurador remoto e reiniciá-lo com a conta que você está usando no computador local.

- Você pode iniciar o depurador remoto a partir da linha de comando com o parâmetro **/Allow \<username> ** :`msvsmon /allow <username@computer>`

- Você pode adicionar o usuário às permissões do depurador remoto (na janela do depurador remoto, **ferramentas > permissões**).

- Se você não puder usar os métodos nas etapas anteriores, poderá permitir que qualquer usuário faça a depuração remota. Na janela depurador remoto, vá para a caixa de diálogo **ferramentas > opções** . Quando você **não seleciona nenhuma autenticação**, pode então verificar **permitir que qualquer usuário depure**. No entanto, você deve usar essa opção somente se não tiver nenhuma opção ou se estiver em uma rede privada.

## <a name="the-firewall-on-the-remote-machine-doesnt-allow-incoming-connections-to-the-remote-debugger"></a>O firewall no computador remoto não permite conexões de entrada para o depurador remoto
 O firewall no computador do Visual Studio e o firewall no computador remoto devem ser configurados para permitir a comunicação entre o Visual Studio e o depurador remoto. Para obter informações sobre as portas que o depurador remoto está usando, consulte [atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md). Para obter informações sobre como configurar o Firewall do Windows, consulte [Configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md).

## <a name="anti-virus-software-is-blocking-the-connections"></a>O software antivírus está bloqueando as conexões
 O software antivírus do Windows permite conexões de depurador remoto, mas algum software antivírus de terceiros pode bloqueá-las. Verifique a documentação do seu software antivírus para saber como permitir essas conexões.

## <a name="network-security-policy-is-blocking-communication-between-the-remote-machine-and-visual-studio"></a>A política de segurança de rede está bloqueando a comunicação entre o computador remoto e o Visual Studio
 Examine a segurança da rede para certificar-se de que ela não está bloqueando a comunicação. Para obter mais informações sobre a política de segurança de rede do Windows, consulte [configurações de política de segurança](/windows/device-security/security-policy-settings/security-policy-settings).

## <a name="the-network-is-too-busy-to-support-remote-debugging"></a>A rede está muito ocupada para dar suporte à depuração remota
 Talvez seja necessário fazer a depuração remota em um momento diferente ou reagendar o trabalho na rede por um horário diferente.

## <a name="more-help"></a>Mais ajuda
 Para obter mais ajuda do depurador remoto, incluindo opções de linha de comando, clique em **ajuda > uso** na janela do depurador remoto. Se você não o tiver aberto, poderá ver a página da Web copiando a linha a seguir para uma janela do **Explorador de arquivos** . (Você precisa substituir \<Visual Studio installation directory> pelo local da instalação do Visual Studio.)

 res:// *\<Visual Studio installation directory>* \Common7\IDE\Remote% 20Debugger\x64\msvsmon.exe/help.htm

## <a name="see-also"></a>Veja também
- [Erros de depuração remota e solução de problemas](../debugger/remote-debugging-errors-and-troubleshooting.md)

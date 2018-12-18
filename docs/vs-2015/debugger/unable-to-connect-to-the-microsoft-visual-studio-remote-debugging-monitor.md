---
title: Não é possível conectar o Monitor de depuração remota do Studio Visual da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.error.remote_debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: a1d959fc-3817-491c-831b-e6b768a3877a
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 139c650ac61b9312b069cc2e19fa66d3673ca30f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51733012"
---
# <a name="unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor"></a>Não foi possível se conectar ao Monitor de Depuração Remota do Microsoft Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa mensagem de erro aparece quando você insere um nome inválido do Visual Studio Remote Debugging Monitor na **anexar ao processo** caixa de diálogo. O nome do Monitor de Depuração Remota geralmente é igual ao computador você está tentando conectar para a depuração remota. Essa mensagem pode ocorrer porque o computador remoto não existe na rede, o monitor de depuração remota não está configurado corretamente no computador remoto ou o computador remoto está inacessível devido a problemas de rede ou à presença de um firewall.  
  
> [!IMPORTANT]
>  Se você acredita ter recebido esta mensagem devido a um bug do produto, relate esse problema para o Visual Studio [enviar um Smiley](http://msdn.microsoft.com/library/5cc9b67a-54d0-41b0-aa8f-80dff4475a6b). Se você precisar de mais ajuda, consulte [Fale conosco](../ide/talk-to-us.md) maneiras de entrar em contato com a Microsoft.  
  
## <a name="i-got-this-message-while-i-was-debugging-locally"></a>Recebi a seguinte mensagem enquanto eu estava depurando localmente  
 Se você estiver recebendo essa mensagem enquanto você estiver depurando localmente, o software antivírus ou um firewall de terceiros pode ser a causa. Visual Studio é um aplicativo de 32 bits, portanto, ele usa a versão de 64 bits do depurador remoto para depurar aplicativos de 64 bits. Os dois processos se comunicam usando a rede local no computador local. Nenhum tráfego de rede deixa o computador, mas é possível que o software de segurança de terceiros pode bloquear a comunicação.  
  
 As seções a seguir listam alguns outros motivos por que você pode ter recebido essa mensagem e o que você pode fazer para corrigir o problema.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Verifique se o Monitor de Depuração Remota do Visual Studio está instalado e em execução no computador remoto. Para obter informações sobre o depurador remoto e como instalá-lo, consulte [depuração remota](../debugger/remote-debugging.md).  
  
-   No Visual Studio, examine as propriedades do projeto (**projeto / propriedades / depuração**). Verifique se o **nome do servidor remoto** está correto.  
  
-   Verifique se o computador remoto está acessível na rede.  
  
## <a name="the-remote-machine-is-not-reachable"></a>O computador remoto não está acessível  
 Tentar [ping](https://technet.microsoft.com/library/ee624059\(v=ws.10\).aspx) o computador remoto. Se ele não responder ao ping, as ferramentas remotas não será capazes de se conectar a qualquer um. Tente reiniciar o computador remoto e caso contrário, certificando-se de que ele está configurado corretamente na rede.  
  
## <a name="the-version-of-the-remote-debugger-doesnt-match-the-version-of-visual-studio"></a>A versão do depurador remoto não corresponde à versão do Visual Studio  
 A versão do Visual Studio que você estiver executando localmente precisa corresponder à versão do monitor de depuração remota que está em execução no computador remoto. Para corrigir esse problema, baixe e instale a versão correspondente do monitor de depuração remota. Vá para o [Centro de Download](http://www.microsoft.com/download) para localizar a versão correta do depurador remoto.  
  
## <a name="the-local-and-remote-machines-have-different-authentication-modes"></a>As máquinas locais e remotas têm diferentes modos de autenticação  
 As máquinas locais e remotas precisam usar o mesmo modo de autenticação. Para corrigir esse problema, certifique-se de que ambos os computadores estão usando o mesmo modo de autenticação. Você pode alterar o modo de autenticação sobre o depurador remoto na **Ferramentas / opções** caixa de diálogo.  
  
 Para obter mais informações sobre modos de autenticação, consulte [visão geral da autenticação do Windows](https://technet.microsoft.com/library/hh831472.aspx).  
  
## <a name="the-remote-debugger-is-running-under-a-different-user-account"></a>O depurador remoto está em execução em uma conta de usuário diferente  
 Você pode resolver isso em uma das seguintes maneiras:  
  
-   Você pode parar o depurador remoto e reiniciá-lo com a conta que você está usando no computador local.  
  
-   Você pode iniciar o depurador remoto na linha de comando com o **/Allow \<nome de usuário >** parâmetro: `msvsmon /allow <username@computer>`  
  
-   Você pode adicionar o usuário para permissões de usuário do depurador remoto (na janela do depurador remoto, **ferramentas / permissões**).  
  
-   Se você não pode usar os métodos nas etapas anteriores, você pode permitir que qualquer usuário faça a depuração remota. Na janela do depurador remoto, vá para o **/Options ferramentas** caixa de diálogo. Quando você seleciona **sem autenticação**, em seguida, você pode verificar **permitem que qualquer usuário depure**. No entanto, você deve usar essa opção somente se você não tem escolha, ou se você estiver usando uma rede privada.  
  
## <a name="the-firewall-on-the-remote-machine-doesnt-allow-incoming-connections-to-the-remote-debugger"></a>O firewall no computador remoto não permite conexões de entrada para o depurador remoto  
 O firewall no computador do Visual Studio e o firewall no computador remoto devem ser configurados para permitir a comunicação entre o Visual Studio e o depurador remoto. Para obter informações sobre as portas que o depurador remoto está usando, consulte [as atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md). Para obter informações sobre como configurar o firewall do Windows, consulte [configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md).  
  
## <a name="anti-virus-software-is-blocking-the-connections"></a>Um software antivírus está bloqueando as conexões  
 Software de antivírus do Windows permite conexões do depurador remoto, mas alguns softwares antivírus de terceiros podem bloqueá-los. Verifique a documentação do seu software antivírus saber como permitir que essas conexões.  
  
## <a name="network-security-policy-is-blocking-communication-between-the-remote-machine-and-visual-studio"></a>Política de segurança de rede está bloqueando a comunicação entre o computador remoto e o Visual Studio  
 Revise a segurança de sua rede para certificar-se de que ele não está bloqueando a comunicação. Para obter mais informações sobre a política de segurança de rede do Windows, consulte [gerenciamento de segurança](https://msdn.microsoft.com/library/windows/desktop/ms721855\(v=vs.85\).aspx).  
  
## <a name="the-network-is-too-busy-to-support-remote-debugging"></a>A rede está muito ocupada para dar suporte à depuração remota  
 Você talvez precise fazer a depuração remota em um momento diferente ou reagendar o trabalho na rede para um momento diferente.  
  
## <a name="more-help"></a>Mais ajuda  
 Para obter ajuda de depurador remota mais, incluindo opções de linha de comando, abra o seguinte em um navegador:  
  
 **res://C:\Program%20Files\Microsoft%20Visual%20Studio%2014.0\Common7\IDE\Remote%20Debugger\x64\msvsmon.exe/help.htm**  
  
## <a name="see-also"></a>Consulte também  
 [Depuração remota](../debugger/remote-debugging.md)




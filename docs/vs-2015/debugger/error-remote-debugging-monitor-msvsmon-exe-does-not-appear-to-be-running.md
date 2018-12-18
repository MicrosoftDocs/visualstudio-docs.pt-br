---
title: 'Erro: o Monitor de Depuração Remota do Microsoft Visual Studio (MSVSMON.EXE) parece não estar sendo executado no computador remoto. | Microsoft Docs'
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
- vs.debug.error.server_machine_no_default
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 86db9931-50e3-4095-b161-802ed8ef39c9
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 252ed59b5e2ace61e3529743d2d01afb4a4fb360
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51746334"
---
# <a name="error-the-microsoft-visual-studio-remote-debugging-monitor-msvsmonexe-does-not-appear-to-be-running-on-the-remote-computer"></a>Erro: o Monitor de Depuração Remota do Microsoft Visual Studio (MSVSMON.EXE) parece não estar sendo executado no computador remoto.
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa mensagem de erro significa que o Visual Studio não pôde localizar a instância correta do Visual Studio Remote Debugging Monitor no computador remoto. O Visual Studio Remote Debugging Monitor deve ser instalado para depuração remota funcione. Para obter informações sobre como baixar e configurar o depurador remoto, consulte [definir configurar as ferramentas remotas no dispositivo](http://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c).  
  
> [!IMPORTANT]
>  Se você acredita ter recebido esta mensagem devido a um bug do produto, relate esse problema para o Visual Studio [enviar um Smiley](http://msdn.microsoft.com/library/5cc9b67a-54d0-41b0-aa8f-80dff4475a6b). Se você precisar de mais ajuda, consulte [Fale conosco](../ide/talk-to-us.md) maneiras de entrar em contato com a Microsoft.  
  
## <a name="i-got-this-message-while-i-was-debugging-in-visual-studio-2010-or-earlier"></a>Recebi a seguinte mensagem enquanto eu estava depurando no Visual Studio 2010 ou anterior  
 Se a versão do Visual Studio que você está usando é o Visual Studio 2010 ou anterior, você também poderá receber esse erro se o compartilhamento de arquivo e impressora não está habilitado. Para obter mais informações sobre esse problema, consulte a versão do Visual Studio 2010 desta documentação: [erro: O Microsoft Visual Studio Monitor de depuração remota (MSVSMON. EXE) parece não estar em execução no computador remoto. -Visual Studio 2010](https://msdn.microsoft.com/library/ms164726\(v=vs.100\).aspx)  
  
## <a name="i-got-this-message-while-i-was-debugging-locally"></a>Recebi a seguinte mensagem enquanto eu estava depurando localmente  
 Se você estiver recebendo essa mensagem enquanto você estiver depurando localmente, o software antivírus ou um firewall de terceiros pode ser a causa. Visual Studio é um aplicativo de 32 bits, portanto, ele usa a versão de 64 bits do depurador remoto para depurar aplicativos de 64 bits. Os dois processos se comunicam usando a rede local no computador local. Nenhum tráfego deixa o computador, mas é possível que o software de segurança de terceiros pode bloquear a comunicação.  
  
 As seções a seguir listam alguns outros motivos por que você pode ter recebido essa mensagem e o que você pode fazer para corrigir o problema.  
  
## <a name="the-remote-machine-is-not-reachable"></a>O computador remoto não está acessível  
 Tentar [ping](https://technet.microsoft.com/library/ee624059\(v=ws.10\).aspx) o computador remoto. Se ele não responder ao ping, as ferramentas remotas não será capazes de se conectar a qualquer um. Tente reiniciar o computador remoto e caso contrário, certificando-se de que ele está configurado corretamente na rede.  
  
## <a name="the-version-of-the-remote-debugger-doesnt-match-the-version-of-visual-studio"></a>A versão do depurador remoto não corresponde à versão do Visual Studio  
 A versão do Visual Studio que você estiver executando localmente precisa corresponder à versão do monitor de depuração remota que está em execução no computador remoto. Para corrigir esse problema, baixe e instale a versão correspondente do monitor de depuração remota. Vá para o [Centro de Download](http://www.microsoft.com/download) para localizar a versão correta do depurador remoto.  
  
## <a name="the-local-and-remote-machines-have-different-authentication-modes"></a>As máquinas locais e remotas têm diferentes modos de autenticação  
 As máquinas locais e remotas precisam usar o mesmo modo de autenticação. Para corrigir esse problema, certifique-se de que ambos os computadores estão usando o mesmo modo de autenticação. Para obter mais informações sobre modos de autenticação, consulte [visão geral da autenticação do Windows](https://technet.microsoft.com/library/hh831472.aspx).  
  
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
 Para obter ajuda de depurador remota mais, incluindo opções de linha de comando, clique em **ajuda / uso** na janela do depurador remoto. Se você não tivê-lo abrir você pode ver a página da web, copie a seguinte linha para um **Explorador de arquivos** janela. (Você precisa substituir \<diretório de instalação do Visual Studio > com o local de instalação do Visual Studio.)  
  
 res: / /*\<diretório de instalação do Visual Studio >* \Common7\IDE\Remote%20Debugger\x64\msvsmon.exe/help.htm  
  
## <a name="see-also"></a>Consulte também  
 [Erros e solução de problemas de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)




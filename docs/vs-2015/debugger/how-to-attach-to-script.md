---
title: 'Como: anexar ao Script | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- script debugging, attaching to script
- script, attaching to
- processes, attaching to script
- remote debugging, attaching to script
ms.assetid: 82013e9a-ef53-4fd2-b451-a6891cdc6307
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c71364905e121ab32c9f5108717acdca32e1354e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51790052"
---
# <a name="how-to-attach-to-script"></a>Como anexar ao script
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico explica como anexar manualmente o depurador do Visual Studio para um arquivo de script para depuração.  
  
### <a name="to-attach-to-a-running-process"></a>Para anexar a um processo em execução  
  
1. Sobre o **Debug** menu, escolha **anexar ao processo**. (Se nenhum projeto estiver aberto, escolha **anexar ao processo** sobre o **ferramentas** menu.)  
  
2. No **anexar ao processo** caixa de diálogo, examine o **processos disponíveis** lista e localizar o script do processo que você deseja anexar. Você pode identificar os processos de script, observando os **tipo** coluna.  
  
   1.  Se o processo que você quiser depurar estiver sendo executado em outro computador, você primeiro deverá selecionar o computador remoto. Para obter mais informações, consulte [como: selecionar um computador remoto](http://msdn.microsoft.com/en-us/4332ba8e-2f0b-4f62-b96a-e762b9f3c3ba).  
  
   2.  Se o processo está em execução em uma conta de usuário diferente, selecione a **Mostrar processos de todos os usuários** caixa de seleção.  
  
   3.  Se você estiver conectado por meio **Conexão de área de trabalho remota**, selecione o **Mostrar processos em todas as sessões** caixa de seleção.  
  
3. Clique no processo ao qual você quer anexar.  
  
4. No **anexar** caixa, você deverá ver **código do Script** ou **automático: código do Script**. Se você encontrar algo além disso, siga estas etapas:  
  
   1.  Clique em **selecionar**.  
  
   2.  No **Selecionar tipo de código** caixa de diálogo, clique em **depurar esses tipos de código** e selecione **Script**.  
  
   3.  Clique em **OK**.  
  
5. Clique em **Anexar**.  
  
    Neste momento, você pode ver um aviso informando que a depuração de scripts está desabilitada no Internet Explorer. Se isso ocorrer, consulte [Aviso: desabilitado de depuração de Script](../debugger/warning-script-debugging-disabled.md).  
  
   O **processos disponíveis** lista é exibida automaticamente quando você abrir o **processos** caixa de diálogo. Os processos podem iniciar e parar em segundo plano quando a caixa de diálogo está aberta. Consequentemente, o conteúdo pode não estar atualizado. Você pode atualizar a lista a qualquer momento para ver a lista atual de processos pressionando o **Refresh** botão.  
  
   Você pode estar associado a vários programas enquanto depura, mas somente um programa está ativo no depurador em um determinado momento. Você pode definir o programa ativo na barra de ferramentas Local de Depuração. Para obter mais informações, consulte [como: definir o processo atual](http://msdn.microsoft.com/en-us/7e1d7fa5-0e40-44cf-8c41-d3dba31c969e).  
  
   Todos os **depurar** comandos de menu de execução afetam o programa ativo. Você pode interromper qualquer programa depurado da caixa de diálogo processos. Ver [usando pontos de interrupção](../debugger/using-breakpoints.md).  
  
> [!NOTE]
>  Se você tentar anexar a um processo de propriedade de uma conta de usuário não confiável, aparecerá uma confirmação da caixa de diálogo de aviso de segurança. Para obter mais informações, consulte [aviso de segurança: anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou você não tiver certeza, não anexe a esse processo](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user-can-be-dangerous-if-the-following-information-looks-suspicious-or-you-are-unsure-do-not-attach-to-this-process.md).  
  
 Em alguns casos, quando você está depurando em uma sessão dos Serviços de Terminal (Área de Trabalho Remota), a lista Processos Disponíveis não exibirá todos os processos disponíveis. Em [!INCLUDE[WinXPSvr](../includes/winxpsvr-md.md)] ou em versões posteriores, se você estiver executando o Visual Studio como um usuário limitado, a lista de Processos Disponíveis não mostrará os processos que estão em execução na sessão 0, usada para serviços e outros processos de servidor, incluindo w3wp.exe. Você pode resolver o problema executando o Visual Studio em uma conta de administrador ou executando o Visual Studio de console do servidor em vez de uma sessão de Terminal Services. Se nenhuma dessas soluções alternativas for possível, uma terceira opção é anexar ao processo digitando vsjitdebugger.exe -p ProcessId na linha de comando do Windows. Você pode determinar o ID do processo usando tlist.exe. Para obter tlist.exe, baixar e instalar a depuração de ferramentas para Windows, disponível em [Windows Hardware Developer Central](http://go.microsoft.com/fwlink/?linkid=1651).  
  
## <a name="see-also"></a>Consulte também  
 [Depuração de Script do lado do cliente](../debugger/client-side-script-debugging.md)   
 [Anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [Aviso de segurança: anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou você não tiver certeza, não anexe a esse processo](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user-can-be-dangerous-if-the-following-information-looks-suspicious-or-you-are-unsure-do-not-attach-to-this-process.md)   
 [Segurança do depurador](../debugger/debugger-security.md)




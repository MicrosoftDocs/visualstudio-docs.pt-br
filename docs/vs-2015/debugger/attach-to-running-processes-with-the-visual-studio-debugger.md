---
title: Anexar a processos em execução com o depurador do Visual Studio | Microsoft Docs
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
- vs.debug.processes.attach
- vs.debug.process
- vs.debug.programs
- vs.debug.detaching
- vs.debug.processes
- vs.debug.error.attach
- vs.debug.remotemachine
dev_langs:
- C++
- CSharp
- FSharp
- VB
- c++
helpviewer_keywords:
- remote debugging, attaching to programs
- processes, attaching to running processes
- Attach to Process dialog box
- debugging [Visual Studio], attaching to processes
- debugger, processes
ms.assetid: 27900e58-090c-4211-a309-b3e1496d5824
caps.latest.revision: 62
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5ca0b2e1ada7e91f5f32f29aba8e89ffc26ac629
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51783064"
---
# <a name="attach-to-running-processes-with-the-visual-studio-debugger"></a>Anexar aos processos em execução com o Depurador do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode anexar o depurador do Visual Studio para um processo em execução em um computador local ou remoto. Depois que o processo está em execução, clique em **depurar / anexar ao processo** (ou pressione **CTRL + ALT + P**) para abrir o **anexar ao processo** caixa de diálogo. 

Você pode usar esse recurso para depurar aplicativos em execução em um computador local ou remoto, depurar vários processos simultaneamente ou depurar um aplicativo que não foi criado no Visual Studio. Geralmente é útil quando você deseja depurar um aplicativo, mas (por qualquer motivo) você não iniciou o aplicativo do Visual Studio com o depurador anexado. Por exemplo, se você estiver executando o aplicativo sem o depurador e atingir uma exceção, você pode, em seguida, anexar ao processo de execução do aplicativo para iniciar a depuração.

> [!TIP]
> Não sabe se é necessário usar **anexar ao processo** para seu cenário de depuração? Ver [comum de cenários de depuração](#BKMK_Scenarios). Se você quiser depurar aplicativos ASP.NET que foi implantado no IIS, consulte [ASP.NET de depuração remota em um computador remoto do IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md).

##  <a name="BKMK_Attach_to_a_running_process"></a> Anexar a um processo em execução no computador local  
 Para anexar a um processo, você deve saber o nome do processo (consulte [comum de cenários de depuração](#BKMK_Scenarios) para alguns nomes comuns do processo).
  
1.  No Visual Studio, selecione **depurar / anexar ao processo** (ou pressione **CTRL + ALT + P**).
  
2.  No **anexar ao processo** diálogo caixa, localize o programa que você deseja anexar a partir de **processos disponíveis** lista.  

     Para selecionar rapidamente o processo que você deseja, digite a primeira letra do nome do processo. Se você não souber o nome do processo, consulte [comum de cenários de depuração](#BKMK_Scenarios).
     
     ![DBG_Basics_Attach_To_Process](../debugger/media/dbg-basics-attach-to-process.png "DBG_Basics_Attach_To_Process") 
  
     Se o processo está em execução em uma conta de usuário diferente, selecione a **Mostrar processos de todos os usuários** caixa de seleção.
  
3.  No **anexar a** caixa, certifique-se de que o tipo de código que será depurado está listado. O padrão **automática** configuração tenta determinar que tipo de código que você deseja depurar. Para definir o tipo de código manualmente, faça o seguinte  
  
    1.  No **anexar** , clique em **selecione**.  
  
    2.  No **Selecionar tipo de código** caixa de diálogo, clique em **depurar esses tipos de código** e selecione os tipos para depurar.  
  
    3.  Clique em **OK**.  
  
4.  Clique em **Anexar**.

##  <a name="BKMK_Attach_to_a_process_on_a_remote_computer"></a> Anexar a um processo em um computador remoto  
 Para anexar a um processo, você deve saber o nome do processo (consulte [comum de cenários de depuração](#BKMK_Scenarios) para alguns nomes comuns do processo). Para obter orientação mais completa para aplicativos ASP.NET que foi implantado no IIS, consulte [ASP.NET de depuração remota em um computador remoto do IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md). Para outros aplicativos, você poderá localizar o nome do processo no Gerenciador de tarefas.
  
 Quando você usa o **anexar ao processo** caixa de diálogo, você pode selecionar outro computador que foi configurado para depuração remota. Para obter mais informações, consulte [depuração remota](http://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c). Quando você tiver selecionado um computador remoto, poderá exibir uma lista de processos disponíveis que estão em execução no computador e anexá-la a um ou mais processos para depuração.
  
 **Para selecionar um computador remoto:**  

1. No Visual Studio, selecione **depurar / anexar ao processo** (ou pressione **CTRL + ALT + P**).

2. No **anexar ao processo** caixa de diálogo, selecione a conexão apropriada de tipo dos **transporte** lista. **Padrão** é a configuração correta para a maioria dos casos.

   O **transporte** configuração persiste entre as sessões de depuração. 
  
3. Use o **qualificador** caixa de listagem para escolher o nome do computador remoto por um dos seguintes métodos:  
  
   1. Digite o nome na **qualificador** caixa de listagem.
    
      >**Observação** se, em etapas posteriores, você não pode se conectar usando o nome do computador remoto, use o endereço IP. (O número da porta pode aparecer automaticamente depois de selecionar o processo. Você também pode inseri-lo manualmente. Na ilustração abaixo, 4020 é a porta padrão para o depurador remoto.)  
  
   2. Clique na seta suspensa anexada para o **qualificador** caixa de listagem e selecione o nome do computador na lista suspensa.  
  
   3. Clique o **encontrar** lado a **qualificador** lista para abrir o **Selecionar Conexão de depurador remoto** caixa de diálogo. O **Selecionar Conexão de depurador remoto** caixa de diálogo lista todos os dispositivos que estão em sua sub-rede local e qualquer dispositivo que está diretamente conectado ao computador por um cabo Ethernet. Clique no computador ou dispositivo que você deseja e, em seguida, clique em **selecionar**. 
  
      O **qualificador** configuração persiste entre as sessões de depuração somente se uma conexão de depuração bem-sucedida ocorre com o qualificador.
     
4. Clique em **Refresh**.

     O **processos disponíveis** lista é exibida automaticamente quando você abrir o **processos** caixa de diálogo. Os processos podem iniciar e parar em segundo plano quando a caixa de diálogo está aberta. No entanto, o conteúdo nem sempre será atual. Você pode atualizar a lista a qualquer momento para ver a lista atual de processos clicando **Refresh**. 
     
5. No **anexar ao processo** diálogo caixa, localize o programa que você deseja anexar a partir de **processos disponíveis** lista.  
  
    Se o processo está em execução em uma conta de usuário diferente, selecione a **Mostrar processos de todos os usuários** caixa de seleção.
     
6. Clique em **Anexar**.  

## <a name="additional-info"></a>Informações adicionais

Você pode estar associado a vários programas enquanto depura, mas somente um programa está ativo no depurador em um determinado momento. Você pode definir o programa ativo na **local de depuração** barra de ferramentas ou o **processos** janela. Para obter mais informações, consulte [como: definir o programa atual](http://msdn.microsoft.com/en-us/7e1d7fa5-0e40-44cf-8c41-d3dba31c969e).  
  
Se você tentar anexar a um processo de propriedade de uma conta de usuário não confiável, aparecerá uma confirmação da caixa de diálogo de aviso de segurança. Para obter mais informações, consulte [aviso de segurança: anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou você não tiver certeza, não anexe a esse processo](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user-can-be-dangerous-if-the-following-information-looks-suspicious-or-you-are-unsure-do-not-attach-to-this-process.md).  
  
Em alguns casos, quando você depura em uma sessão de área de trabalho remota (serviços de Terminal), o **processos disponíveis** lista não exibirá todos os processos disponíveis. Se você estiver executando o Visual Studio como um usuário que tenha uma conta de usuário limitado, o **processos disponíveis** lista não mostrará processos em execução na sessão 0, que é usado para serviços e outros processos do servidor, incluindo w3wp.exe. Você pode resolver o problema executando o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] em uma conta de administrador ou executando o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] no console do servidor em vez de uma sessão de Serviços de Terminal. Se nenhuma dessas soluções alternativas for possível, uma terceira opção é anexar ao processo executando `vsjitdebugger.exe -p` *ProcessId* da linha de comando do Windows. Você pode determinar a ID do processo usando tlist.exe. Para obter tlist.exe, baixar e instalar a depuração de ferramentas para Windows, disponível em [downloads do WDK e WinDbg](http://go.microsoft.com/fwlink/?LinkId=168279).

## <a name="BKMK_Scenarios"></a> Cenários comuns de depuração

Para ajudá-lo a identificar se você precisa usar **anexar ao processo** e qual processo anexar, alguns cenários comuns de depuração são mostrados aqui (a lista não é exaustiva). Onde obter mais instruções estiverem disponíveis, fornecemos links.

Para alguns tipos de aplicativo (como aplicativos da Windows Store), não anexe diretamente a um nome de processo, mas usar o **depurar pacote do aplicativo instalado** em vez disso, a opção de menu (consulte a tabela).

> [!NOTE]
> Para obter informações sobre depuração básica no Visual Studio, consulte [Introdução ao depurador](../debugger/getting-started-with-the-debugger.md).

|Cenário|Depurar o método|Nome do Processo|Observações e Links|
|-|-|-|-|
|Depurar um aplicativo gerenciado ou nativo na máquina local|Use anexar ao processo ou [depuração padrão](../debugger/getting-started-with-the-debugger.md)|*appname*.exe|Para acessar rapidamente a caixa de diálogo, use **CTRL + ALT + P** e, em seguida, digite a primeira letra do nome do processo.|
|Depurar aplicativos ASP.NET no computador local depois de iniciar o aplicativo sem o depurador|Use anexar ao processo|iiexpress.exe|Isso pode ser útil para fazer com que seu aplicativo carregar mais rápido, como (por exemplo) ao criar o perfil. |
|Depuração remota ASP.NET 4 ou 4.5 em um servidor IIS|Usar as ferramentas remotas e anexar ao processo|W3wp.exe|Consulte [ASP.NET de depuração remota em um computador remoto do IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|Depuração remota do ASP.NET Core em um servidor IIS|Usar as ferramentas remotas e anexar ao processo|dnx.exe|Para implantação de aplicativo, consulte [publicar no IIS](https://docs.asp.net/en/latest/publishing/iis.html). Para depuração, consulte [ASP.NET de depuração remota em um computador remoto do IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|Depurar outros tipos de aplicativos com suporte em um processo do servidor|Usar as ferramentas remotas (se o servidor for remoto) e anexar ao processo|Iexplore.exe ou outros processos|Se necessário, use o Gerenciador de tarefas para ajudar a identificar o processo. Ver [depuração remota](../debugger/remote-debugging.md) e seções posteriores neste tópico|
|Depuração remota de um aplicativo de desktop do Windows|F5 e as ferramentas remotas|N/A| Consulte [depuração remota](../debugger/remote-debugging.md)|
|Remoto depurar um aplicativo Universal do Windows (UWP), OneCore, HoloLens ou IoT|Depurar pacote do aplicativo instalado|N/A|Use **Debug / outros destinos de depuração / depurar pacote do aplicativo instalado** em vez de **anexar ao processo**|
|Depurar um aplicativo Universal do Windows (UWP), OneCore, HoloLens ou IoT que você não iniciou no Visual Studio|Depurar pacote do aplicativo instalado|N/A|Use **Debug / outros destinos de depuração / depurar pacote do aplicativo instalado** em vez de **anexar ao processo**|
  
> [!WARNING]
>  Para anexar a um aplicativo Universal do Windows que é escrito em JavaScript, você deve primeiro habilitar a depuração para o aplicativo. Ver [anexar o depurador](../debugger/start-a-debugging-session-for-store-apps-in-visual-studio-javascript.md#BKMK_Attach_the_debugger) no Centro de desenvolvimento do Windows.  
  
> [!NOTE]
>  Para que o depurador se anexe ao código escrito em C++, o código precisa emitir `DebuggableAttribute`. Você pode adicionar isso ao seu código automaticamente por meio da vinculação com o [/ASSEMBLYDEBUG](http://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982) a opção de vinculador.

## <a name="what-debugger-features-can-i-use"></a>Quais recursos do depurador pode usar?

Para usar os recursos completos do depurador do Visual Studio (como usar pontos de interrupção) ao anexar a um processo, o executável deve corresponder exatamente ao seu local de origem e símbolos (ou seja, o depurador deve ser capaz de carregar o correto [(.pbd) arquivos de símbolo ](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)). Por padrão, isso requer uma compilação de depuração.

Para cenários de depuração remota, você deve ter o código-fonte (ou uma cópia do código-fonte) estiver aberto no Visual Studio. Os binários do aplicativo compilado no computador remoto devem vir da mesma compilação, como no computador local.

Em alguns cenários de depuração locais, você pode depurar no Visual Studio sem acesso à fonte de se os arquivos de símbolos corretos estão presentes com o aplicativo (por padrão, isso requer uma compilação de depuração). Para obter mais informações, consulte [arquivos de origem e especificar o símbolo](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).
  
##  <a name="BKMK_Troubleshoot_attach_errors"></a> Solucionar problemas de erros de anexo  
 Quando o depurador é anexado a um processo em execução, o processo pode conter um ou mais tipos de código. Os tipos de código, o depurador pode se anexar são exibidos e selecionados na **Select Code Type** caixa de diálogo.  
  
 Às vezes, o depurador pode ser anexado com êxito a um tipo de código, mas não a outro tipo de código. Isso pode ocorrer se você estiver tentando anexar a um processo que esteja sendo executado em um computador remoto. O computador remoto pode ter componentes de depuração remota instalados para alguns tipos de código mas não para outros. Isso também pode ocorrer se você tentar anexar a dois ou mais processos para depuração direta de banco de dados. A depuração de SQL dá suporte à anexação de apenas um único processo.  
  
 Se o depurador puder se conectar a alguns, mas não a todos os tipos de código, você verá uma mensagem identificando quais tipos não conseguiram estabelecer conexão.  
  
 Se o depurador for anexado com êxito a pelo menos um tipo de código, você poderá depurar o processo. Você poderá depurar apenas os tipos de código que foram anexados com êxito. A mensagem do exemplo anterior mostra que o tipo de código de script não foi anexado. Portanto, você não pode depurar o código do script dentro do processo. O código de script no processo ainda seria executado, mas você não poderia definir pontos de interrupção, exibir dados ou executar outras operações de depuração no script.  
  
 Se você desejar informações mais específicas sobre por que o depurador não foi anexado a um tipo de código, tente reanexar somente àquele tipo de código.  
  
 **Para obter informações específicas sobre por que um tipo de código falha ao anexar**  
  
1. Desanexe do processo. Sobre o **Debug** menu, clique em **desanexar tudo**.  
  
2. Anexe o processo novamente, selecionando apenas um único tipo de código.  
  
   1. No **anexar ao processo** caixa de diálogo, selecione o processo na **processos disponíveis** lista.  
  
   2. Clique em **selecionar**.  
  
   3. No **Selecionar tipo de código** caixa de diálogo, selecione **depurar esses tipos de código** e o tipo de código que não foi anexado. Limpe qualquer outro código.  
  
   4. Clique em **OK**. O **Select Code Type** caixa de diálogo é fechada.  
  
   5. No **anexar ao processo** caixa de diálogo, clique em **Attach**.  
  
      Desta vez, o anexo falhará completamente e você receberá uma mensagem de erro específica.  
  
## <a name="see-also"></a>Consulte também  
 [Depurar vários processos](../debugger/debug-multiple-processes.md)   
 [Depuração Just-In-Time](../debugger/just-in-time-debugging-in-visual-studio.md)   
 [Depuração remota](../debugger/remote-debugging.md)




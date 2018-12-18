---
title: Depurar vários processos | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.programs
- vs.debug.processes.attaching
- vs.debug.activeprogram
- vs.debug.attaching
- vs.debug.attachedprocesses
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: bde37134-66af-4273-b02e-05b3370c31ab
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0b306bcca4ac8cc0568fc609ec25c8b335d18010
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305644"
---
# <a name="debug-multiple-processes"></a>Depurar vários processos

O Visual Studio pode depurar uma solução que tem vários processos. Você pode iniciar e alternar entre processos, interromper, continuar e percorrer o código-fonte, interromper a depuração e end ou desanexar dos processos individuais.  

##  <a name="start-debugging-with-multiple-processes"></a>Iniciar a depuração com vários processos 

Quando mais de um projeto em uma solução do Visual Studio pode executar de forma independente, você pode selecionar quais projetos o depurador é iniciado. O projeto de inicialização atual é exibido em negrito no **Gerenciador de soluções**. 

Para alterar o projeto de inicialização, no **Gerenciador de soluções**, um projeto diferente com o botão direito e selecione **definir como projeto de inicialização**.

Para iniciar a depuração de um projeto a partir **Gerenciador de soluções** sem torná-lo o projeto de inicialização, clique com botão direito no projeto e selecione **Debug** > **iniciar nova instância** ou **intervir em nova instância**. 

**Para definir o projeto de inicialização ou vários projetos da solução de propriedades:**

1. Selecione a solução no **Gerenciador de soluções** e, em seguida, selecione o **Properties** ícone na barra de ferramentas ou clique com botão direito a solução e selecione **propriedades**.  
   
1. Sobre o **propriedades** página, selecione **propriedades comuns** > **projeto de inicialização**.
   
   ![Alterando o tipo de inicialização para um projeto](../debugger/media/dbg_execution_startmultipleprojects.png "DBG_Execution_StartMultipleProjects")  
   
1. Selecione **seleção atual**, **único projeto de inicialização** e um arquivo de projeto, ou **vários projetos de inicialização**. 

   Se você selecionar **vários projetos de inicialização**, você pode alterar a ordem de inicialização e a ação a ser tomada para cada projeto: **inicie**, **iniciar sem depuração**, ou **Nenhum**.  
   
1. Selecione **Apply**, ou **Okey** para aplicar e fechar a caixa de diálogo. 

###  <a name="BKMK_Attach_to_a_process"></a> Anexar a um processo  

O depurador também pode *anexar* para aplicativos executados em processos fora do Visual Studio, incluindo em dispositivos remotos. Depois de anexar a um aplicativo, você pode usar o depurador do Visual Studio. Recursos de depuração podem ser limitado. Ele depende se o aplicativo foi compilado com informações de depuração, se você tem acesso ao código-fonte do aplicativo e se o compilador JIT está controlando as informações de depuração.  
  
Para obter mais informações, consulte [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
**Para anexar a um processo em execução:**  
  
1. Com o aplicativo em execução, selecione **Debug** > **anexar ao processo**. 

   ![Anexar a caixa de diálogo processar](../debugger/media/dbg_attachtoprocessdlg.png "anexar à caixa de diálogo de processo")  
  
1. No **anexar ao processo** caixa de diálogo, selecione o processo da **processos disponíveis** lista e, em seguida, selecione **Attach**.  
  
>[!NOTE]
>O depurador não é anexado automaticamente a um processo filho que é inicializado por um processo depurado, mesmo se o projeto filho estiver na mesma solução. Para depurar um processo filho, anexar ao processo filho depois de ter começado, ou configurar o Editor do registro do Windows para iniciar o processo filho em uma nova instância do depurador.  
  
###  <a name="BKMK_Automatically_start_an_process_in_the_debugger"></a> Use o Editor do registro para iniciar automaticamente um processo no depurador  

Às vezes, talvez você precise depurar o código de inicialização para um aplicativo que é iniciado por outro processo. Os exemplos incluem serviços e ações de configuração personalizada. Você pode ter o depurador a iniciar e anexar automaticamente ao aplicativo. 

1. Inicie o Editor de registro do Windows executando *regedit.exe*.  
   
1. No Editor do registro, navegue até **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options**.  
  
1. Selecione a pasta do aplicativo que você deseja iniciar o depurador.  
   
   Se o aplicativo não estiver listado como uma pasta filho, clique com botão direito **Image File Execution Options**, selecione **New** > **chave**e digite o nome do aplicativo. Ou, clique com botão direito na árvore, selecione a nova chave **Renomear**e, em seguida, insira o nome do aplicativo. 
   
1. Clique com botão direito na árvore e selecione a nova chave **New** > **valor de cadeia de caracteres**.  
   
1. Altere o nome do novo valor de **novo valor #1** para `debugger`.  
   
1. Clique com botão direito **depurador** e selecione **modificar**.  
   
   ![Editar caixa de diálogo de cadeia de caracteres](../debugger/media/dbg_execution_automaticstart_editstringdlg.png "caixa de diálogo Editar cadeia de caracteres")  
   
1. No **Editar cadeia de caracteres** caixa de diálogo, digite `vsjitdebugger.exe` no **dados do valor** caixa e, em seguida, selecione **Okey**.  
   
   ![Depurador automático começar a entrada em regedit.exe](../debugger/media/dbg_execution_automaticstart_result.png "depurador automático começar a entrada em regedit.exe")  
   
##  <a name="BKMK_Switch_processes__break_and_continue_execution__step_through_source"></a> Depurar com vários processos 
<a name="BKMK_Configure_the_execution_behavior_of_multiple_processes"></a> 

Quando estiver depurando um aplicativo com vários processos, os comandos do depurador mais recentes, passo a passo e continuando afetam todos os processos por padrão. Por exemplo, quando um processo é suspenso em um ponto de interrupção, a execução de todos os outros processos também é suspenso. Você pode alterar esse comportamento padrão para obter mais controle sobre os destinos dos comandos de execução.  

**Para alterar se todos os processos serão suspensas quando um processo for interrompido:**

- Sob **ferramentas** (ou **Debug**) > **opções** > **depuração** > **geral**, marque ou desmarque as **interromper todos os processos quando um processo for interrompido** caixa de seleção.  
  
###  <a name="BKMK_Break__step__and_continue_commands"></a> Comandos de interromper, depurar e continuar  
  
A tabela a seguir descreve os comportamentos de depuração de comandos quando o **interromper todos os processos quando um processo for interrompido** caixa de seleção é marcada ou desmarcada:

|**Comando**|Selecionado|Desmarcado|  
|-|-|-|  
|**Depurar**  > **interromper tudo**|Todos os processos são interrompidos.|Todos os processos são interrompidos.|  
|**Depurar** > **continuar**|Todos os processos são retomados.|Todos os processos suspensos são retomados.|  
|**Depurar** > **intervir**, **Step Over**, ou **depuração circular**|Todos os processos estão em execução durante as etapas de processo atual. <br />Em seguida, todos os processos são interrompidos.|Etapas de processo atual. <br />Retomada de processos suspensos. <br />Executando a continuação dos processos.|  
|**Depurar** > **etapa no processo atual**, **etapa ao longo do processo atual**, ou **sair do processo atual**|N/D|Etapas de processo atual.<br />Outros processos mantém o estado existente (suspenso ou em execução).|  
|Janela de origem **ponto de interrupção**|Todos os processos são interrompidos.|Somente quebras do processo da janela de origem.|  
|Janela de origem **executar até o cursor**<br />A janela de origem deve estar no processo atual.|Todos os processos estão em execução enquanto o processo da janela de origem executa ao cursor e depois interrompe.<br />Em seguida, todos os outros processos não interrompidos.|O processo da janela de origem é executado para o cursor.<br />Outros processos mantém o estado existente (suspenso ou em execução).|  
|**Processos** Janela > **interromper processo**|N/D|Quebras selecionadas do processo.<br />Outros processos mantém o estado existente (suspenso ou em execução).|  
|**Processos** Janela > **continuar processo**|N/D|O processo selecionado é retomado.<br />Outros processos mantém o estado existente (suspenso ou em execução).|  

###  <a name="BKMK_Find_the_source_and_symbol___pdb__files"></a> Localize a fonte e os arquivos de símbolo (.pdb)  
Para navegar no código de origem de um processo, o depurador precisa acessar seus arquivos de origem e arquivos de símbolo. Para obter mais informações, confira [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).  
  
Se você não pode acessar os arquivos para um processo, você pode navegar usando o **desmontagem** janela. Para obter mais informações, consulte [como: usar a janela de desmontagem](../debugger/how-to-use-the-disassembly-window.md).  

###  <a name="BKMK_Switch_between_processes"></a> Alternar entre processos  

Você pode anexar a vários processos quando você está depurando, mas somente um processo está ativo no depurador em um determinado momento. Você pode definir o processo ativo *atual* ou na barra de ferramentas do **Localização de Depuração** ou na janela **Processos**. Para alternar entre processos, ambos os processos devem estar no modo de interrupção.  
  
**Para definir o processo atual da barra de ferramentas local de depuração:**  
  
1. Para abrir o **local de depuração** barra de ferramentas, selecione **exibição** > **barras de ferramentas** > **local de depuração**.  
   
1. Durante a depuração, diante a **local de depuração** barra de ferramentas, selecione o processo que você deseja definir como o processo atual do **processo** lista suspensa.  
  
   ![Alternar entre processos](../debugger/media/dbg_execution_switchbetweenmodules.png "DBG_Execution_SwitchBetweenModules")  
  
**Para definir o processo atual da janela de processos:**  
  
1. Para abrir o **processos** janela, durante a depuração, selecione **Debug** > **Windows** > **processos**. 

1. No **processos** janela, o processo atual é marcada por uma seta amarela. Clique duas vezes o processo que você deseja definir como o processo atual.  
  
   ![Janela de processos](../debugger/media/dbg_processeswindow.png "DBG_ProcessesWindow")  

Alternar para um processo define como o processo atual para fins de depuração. Janelas do depurador mostrará o estado para o processo atual e comandos das etapas afetarão somente o processo atual.  
  
## <a name="stop-debugging-with-multiple-processes"></a>Parar a depuração com vários processos  
  
Por padrão, quando você seleciona **Debug** > **parar depuração**, o depurador encerra ou desanexado de todos os processos. 
  
- Se o processo atual foi iniciado no depurador, o processo será encerrado.  
  
- Se você já anexou o depurador ao processo atual, o depurador será desanexado do processo e o deixará em execução.  
  
Se você iniciar a depuração de um processo de uma solução do Visual Studio, em seguida, anexar a outro processo já está em execução e, em seguida, escolha **parar depuração**, o término da sessão de depuração. Encerra o processo que foi iniciado no Visual Studio, enquanto o processo anexado ao continua em execução. 

Para controlar a maneira que **parar depuração** afeta a um processo individual, o **processos** janela, um processo, com o botão direito e, em seguida, marque ou desmarque o **desanexar quando a depuração for interrompida** caixa de seleção.  
  
>[!NOTE]
>O **interromper todos os processos quando um processo for interrompido** opção de depurador não afeta parando, finalizando ou desconectando processos.  
  
###  <a name="stop-terminate-and-detach-commands"></a>Parar, finalizar e desanexar comandos  
  
A tabela a seguir descreve os comportamentos de parar o depurador, finalizar e desanexar comandos com vários processos: 

|**Comando**|**Descrição**|  
|-|-| 
|**Depurar** > **parar a depuração**|A menos que o comportamento mudou a **processos** , processos iniciados pelo depurador são finalizados, e processos anexados são separados.|  
|**Depurar** > **finalizar tudo**|Todos os processos são encerrados.|  
|**Depurar** > **desanexar tudo**|O depurador desanexa todos os processos.|  
|**Processos** Janela > **desanexar processo**|O depurador dispara do processo selecionado.<br />Outros processos mantém o estado existente (suspenso ou em execução).|  
|**Processos** Janela > **encerrar processo**|O processo selecionado será encerrado.<br />Outros processos mantém o estado existente (suspenso ou em execução).|  
|**Processos** Janela > **desanexar ao parar a depuração**|Se selecionado, **Debug** > **parar depuração** dispara do processo selecionado. <br />Se não estiver selecionada, **Debug** > **parar depuração** termina o processo selecionado. |  
## <a name="see-also"></a>Consulte também  
 [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [Anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [Navegar pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md)   
 [Depuração Just-In-Time](../debugger/just-in-time-debugging-in-visual-studio.md)   
 [Depurar aplicativos multi-threaded](../debugger/debug-multithreaded-applications-in-visual-studio.md)
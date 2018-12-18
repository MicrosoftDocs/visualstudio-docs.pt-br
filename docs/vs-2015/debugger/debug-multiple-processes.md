---
title: Depurar vários processos | Microsoft Docs
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
- vs.debug.programs
- vs.debug.processes.attaching
- vs.debug.activeprogram
- vs.debug.attaching
- vs.debug.attachedprocesses
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: bde37134-66af-4273-b02e-05b3370c31ab
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 56982a3b5c0a0d8a5cb0b682ab67b6f5eb133dd1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51793042"
---
# <a name="debug-multiple-processes"></a>Depurar vários processos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Veja como iniciar processos de depuração, alternar entre processos, interromper e continuar a execução, percorrer o código-fonte, interromper a depuração e terminar ou desanexar dos processos.  
  
##  <a name="BKMK_Contents"></a> Conteúdo  
 [Configurar o comportamento de execução de vários processos](#BKMK_Configure_the_execution_behavior_of_multiple_processes)  
  
 [Localizar a origem e o símbolo arquivos (. PDB)](#BKMK_Find_the_source_and_symbol___pdb__files)  
  
 [Iniciar vários processos em uma solução VS, anexar a um processo, iniciar automaticamente um processo no depurador](#BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger)  
  
 [Alternar entre processos, interromper e continuar a execução, percorrer o código-fonte](#BKMK_Switch_processes__break_and_continue_execution__step_through_source)  
  
 [Parar a depuração, finalizar ou desanexar dos processos](#BKMK_Stop_debugging__terminate_or_detach_from_processes)  
  
##  <a name="BKMK_Configure_the_execution_behavior_of_multiple_processes"></a> Configurar o comportamento de execução de vários processos  
 Por padrão, quando vários processos são executados no depurador, os comandos de quebra, avanço e interrupção do depurador geralmente afetam todos os processos. Por exemplo, quando um processo é suspenso em um ponto de interrupção, a execução de todos outros processos é suspendida também. Você pode alterar esse comportamento padrão para obter mais controle sobre os destinos dos comandos de execução.  
  
1. Sobre o **Debug** menu, escolha **opções e configurações**.  
  
2. Sobre o **Debugging**, **geral** página, desmarque o **interromper todos os processos quando um processo for interrompido** caixa de seleção.  
  
   ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
##  <a name="BKMK_Find_the_source_and_symbol___pdb__files"></a> Localizar a origem e o símbolo arquivos (. PDB)  
 Para navegar no código-fonte de um processo, o depurador precisa acessar os arquivos de origem e os arquivos do símbolo do processo. Confira [Especificar arquivos de símbolo (.pdb) e de origem no Depurador do Visual Studio](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).  
  
 Se você não conseguir acessar arquivos para um processo, poderá navegar usando a janela de desmontagem. Consulte [como: usar a janela de desmontagem](../debugger/how-to-use-the-disassembly-window.md)  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
##  <a name="BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger"></a> Iniciar vários processos em uma solução VS, anexar a um processo, iniciar automaticamente um processo no depurador  
  
-   [Iniciar a depuração de vários processos em uma solução do Visual Studio](#BKMK_Start_debugging_multiple_processes_in_a_Visual_Studio_solution) • [alterar o projeto de inicialização](#BKMK_Change_the_startup_project) • [iniciar um projeto específico em uma solução](#BKMK_Start_a_specific_project_in_a_solution) • [iniciar projetos múltiplos em uma solução](#BKMK_Start_multiple_projects_in_a_solution) • [anexar a um processo](#BKMK_Attach_to_a_process) • [iniciar automaticamente um processo no depurador](#BKMK_Automatically_start_an_process_in_the_debugger)  
  
> [!NOTE]
>  O depurador não é anexado automaticamente a um processo filho que é inicializado por um processo depurado, mesmo se o projeto filho estiver na mesma solução. Para depurar um processo filho:  
> 
> - Anexar ao processo filho depois que for iniciado.  
> 
>   -ou-  
>   -   Configurar o Windows para iniciar automaticamente o processo filho em uma nova instância do depurador.  
  
###  <a name="BKMK_Start_debugging_multiple_processes_in_a_Visual_Studio_solution"></a> Iniciar a depuração de vários processos em uma solução do Visual Studio  
 Quando você tiver mais de um projeto em uma solução do Visual Studio que pode executar de forma independente (projetos que são executados em processos separados), será possível selecionar quais projetos o depurador inicia.  
  
 ![Alterando o tipo de inicialização para um projeto](../debugger/media/dbg-execution-startmultipleprojects.png "DBG_Execution_StartMultipleProjects")  
  
####  <a name="BKMK_Change_the_startup_project"></a> Alterar o projeto de inicialização  
 Para alterar o projeto de inicialização para uma solução, selecione o projeto no Gerenciador de soluções e, em seguida, escolha **definir como projeto de inicialização** no menu de contexto.  
  
####  <a name="BKMK_Start_a_specific_project_in_a_solution"></a> Iniciar um projeto específico em uma solução  
 Para iniciar um projeto para uma solução sem alterar o projeto de inicialização padrão, selecione o projeto no Gerenciador de soluções e, em seguida, escolha **depurar** no menu de contexto. Em seguida, você pode escolher **iniciar nova instância** ou **intervir nova instância**.  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [iniciar vários processos em uma solução VS, anexar a um processo, iniciar automaticamente um processo no depurador](../debugger/debug-multiple-processes.md#BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger)  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
####  <a name="BKMK_Start_multiple_projects_in_a_solution"></a> Iniciar vários projetos em uma solução  
  
1. Selecione a solução no Gerenciador de soluções e, em seguida, escolha **propriedades** no menu de contexto.  
  
2. Selecione **propriedades comuns**, **projeto de inicialização** sobre o **propriedades** caixa de diálogo.  
  
3. Para cada projeto que você deseja alterar, escolha **inicie**, **iniciar sem depuração**, ou **None**.  
  
   ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [iniciar vários processos em uma solução VS, anexar a um processo, iniciar automaticamente um processo no depurador](../debugger/debug-multiple-processes.md#BKMK_Start_multiple_processes_in_a_VS_solution__attach_to_a_process__automatically_start_a_process_in_the_debugger)  
  
   ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
###  <a name="BKMK_Attach_to_a_process"></a> Anexar a um processo  
 O depurador também pode ser *anexar* para programas que são executados em processos fora do Visual Studio, incluindo programas que estão sendo executados em um dispositivo remoto. Após vincular-se a um programa, você poderá usar comandos de execução do depurador, inspecionar o estado do programa e assim por diante. A capacidade de inspecionar o programa pode ser limitada se o programa foi criado com informações de depuração, se você tem acesso ao código-fonte do programa, e se o compilador just-in-time (JIT) do Common Language Runtime está controlando as informações de depuração.  
  
 Ver [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md) para obter mais informações.  
  
 **Anexar a um processo que está em execução no computador local**  
  
 Escolher **Debug**, **anexar ao processo**. Sobre o **anexar ao processo** caixa de diálogo, selecione o processo da **processos disponíveis** lista e, em seguida, escolha **anexar**.  
  
 ![Anexar a caixa de diálogo processar](../debugger/media/dbg-attachtoprocessdlg.png "DBG_AttachToProcessDlg")  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
###  <a name="BKMK_Automatically_start_an_process_in_the_debugger"></a> Iniciar automaticamente um processo no depurador  
 Às vezes, pode ser necessário depurar o código de inicialização para um programa que foi iniciado por outro processo. Os exemplos incluem serviços e ações de configuração personalizada. Nesses cenários, você poderá fazer com que o depurador seja iniciado e automaticamente anexado quando seu aplicativo iniciar.  
  
1. Inicie o Editor do registro (**regedit.exe**).  
  
2. Navegue até a **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options** pasta.  
  
3. Selecione a pasta do aplicativo que você deseja iniciar o depurador.  
  
    Se o nome do aplicativo não estiver listado como uma pasta filho, selecione **Image File Execution Options** e, em seguida, escolha **New**, **chave** no menu de contexto. Selecione a nova chave, escolha **Renomear** no menu de atalho e, em seguida, insira o nome do aplicativo.  
  
4. No menu de contexto da pasta do aplicativo, escolha **New**, **valor de cadeia de caracteres**.  
  
5. Altere o nome do novo valor de **novo valor** para `debugger`.  
  
6. No menu de contexto da entrada do depurador, escolha **modificar**.  
  
7. Na caixa de diálogo Editar cadeia de caracteres, digite `vsjitdebugger.exe` no **dados de valor** caixa.  
  
    ![Editar caixa de diálogo de cadeia de caracteres](../debugger/media/dbg-execution-automaticstart-editstringdlg.png "DBG_Execution_AutomaticStart_EditStringDlg")  
  
   ![Depurador automático começar a entrada em regedit.exe](../debugger/media/dbg-execution-automaticstart-result.png "DBG_Execution_AutomaticStart_Result")  
  
   ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
##  <a name="BKMK_Switch_processes__break_and_continue_execution__step_through_source"></a> Alternar entre processos, interromper e continuar a execução, percorrer o código-fonte  
  
-   [Alternar entre processos](#BKMK_Switch_between_processes) • [2&gt;interromper, depurar e continuar comandos](#BKMK_Break__step__and_continue_commands)  
  
###  <a name="BKMK_Switch_between_processes"></a> Alternar entre processos  
 Você pode conectar-se a vários processos quando está depurando, mas somente um processo está ativo no depurador em um determinado momento. Você pode definir o ativo ou *atual* processo na barra de ferramentas Depurar local ou na **processos** janela. Para alternar entre processos, ambos os processos devem estar no modo de interrupção.  
  
 **Para definir o processo atual**  
  
- Na barra de ferramentas local de depuração, escolha **processo** para exibir o **processo** caixa de listagem. Selecione o processo que você deseja designar como o processo atual.  
  
   ![Alternar entre processos](../debugger/media/dbg-execution-switchbetweenmodules.png "DBG_Execution_SwitchBetweenModules")  
  
   Se o **local de depuração** barra de ferramentas não estiver visível, escolha **ferramentas**, **personalizar**. Sobre o **barras de ferramentas** guia, escolha **local de depuração**.  
  
- Abra o **processos** janela (atalho **Ctrl + Alt + Z**), localize o processo que você deseja definir como o processo atual e clique duas vezes nele.  
  
   ![Janela de processos](../debugger/media/dbg-processeswindow.png "DBG_ProcessesWindow")  
  
   O processo atual é marcado por uma seta amarela.  
  
  Alternar para um projeto o torna o processo atual para fins de depuração. Qualquer janela do depurador que você exibir mostrará o estado do processo atual e todos os comandos das etapas afetarão somente o processo atual.  
  
  ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [alternar entre processos, interromper e continuar a execução, percorrer o código-fonte](../debugger/debug-multiple-processes.md#BKMK_Switch_processes__break_and_continue_execution__step_through_source)  
  
  ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
###  <a name="BKMK_Break__step__and_continue_commands"></a> Interromper, depurar e continuar comandos  
  
> [!NOTE]
>  Por padrão, os comandos interromper, continuar e avançar depurador afetam todos os processos que estão sendo depurados. Para alterar esse comportamento, consulte [configurar o comportamento de execução de vários processos](#BKMK_Configure_the_execution_behavior_of_multiple_processes)  
  
||||  
|-|-|-|  
|**Comando**|**Interromper todos os processos quando um processo for interrompido**<br /><br /> Verificado (Padrão)|**Interromper todos os processos quando um processo for interrompido**<br /><br /> Limpo|  
|**Depurar** menu:<br /><br /> -   **Interromper tudo**|Todos os processos são interrompidos.|Todos os processos são interrompidos.|  
|**Depurar** menu:<br /><br /> -   **Continuar**|Todos os processos são retomados.|Todos os processos suspensos são retomados.|  
|**Depurar** menu:<br /><br /> -   **Intervir**<br />-   **Depuração parcial**<br />-   **Depuração circular**|Todos os processos estão em execução durante as etapas de processo atual.<br /><br /> Em seguida, todos os processos são interrompidos.|Etapas de processo atual.<br /><br /> Retomada de processos suspensos.<br /><br /> Executando a continuação dos processos.|  
|**Depurar** menu:<br /><br /> -   **Etapa no processo atual**<br />-   **Etapa ao longo do processo atual**<br />-   **Sair do processo atual**|N/D|Etapas de processo atual.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
|Janela de origem<br /><br /> -   **Ponto de interrupção**|Todos os processos são interrompidos.|Somente quebras do processo da janela de origem.|  
|Menu de contexto da janela de origem:<br /><br /> -   **Executar até o cursor**<br /><br /> A janela de origem deve estar no processo atual.|Todos os processos estão em execução enquanto o processo da janela de origem executa ao cursor e depois interrompe.<br /><br /> Em seguida, todos os outros processos não interrompidos.|O processo da janela de origem é executado para o cursor.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
|**Processos** menu de contexto da janela:<br /><br /> -   **Interromper processo**|N/D|Quebras selecionadas do processo.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
|**Processos** menu de contexto da janela:<br /><br /> -   **Continuar processo**|N/D|O processo selecionado é retomado.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [alternar entre processos, interromper e continuar a execução, percorrer o código-fonte](../debugger/debug-multiple-processes.md#BKMK_Switch_processes__break_and_continue_execution__step_through_source)  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
##  <a name="BKMK_Stop_debugging__terminate_or_detach_from_processes"></a> Parar a depuração, finalizar ou desanexar dos processos  
  
- [Parar, finalizar e desanexar comandos](#BKMK_Stop__terminate__and_detach_commands)  
  
  Por padrão, quando você escolhe **Debug**, **parar depuração** quando vários processos estão abertos no depurador, o depurador encerra ou dispara de todos os processos, dependendo de como o processo foi aberto no depurador:  
  
- Se o processo atual foi iniciado no depurador, esse processo é finalizado.  
  
- Se você já anexou o depurador ao processo atual, o depurador será desanexado do processo e o deixará em execução.  
  
  Por exemplo, se você iniciar a depuração de um processo de uma solução do Visual Studio, anexe a outro processo já está em execução e, em seguida, escolha **parar depuração**, a sessão de depuração termina, o processo que foi iniciado no Visual Studio é finalizado, enquanto o processo que você anexou permanecerá em execução. Você pode usar os seguintes procedimentos para controlar a maneira que você interrompe a depuração.  
  
> [!NOTE]
>  O **interromper todos os processos quando um processo for interrompido** opção não afeta a interrupção de depuração ou encerramento e desanexação dos processos.  
  
 **Para alterar como a depuração de parada afeta um processo individual**  
  
-   Abra o **processos** janela (atalho **Ctrl + Alt + Z**). Selecione um processo e, em seguida, marque ou desmarque a **desanexar quando a depuração for interrompida** caixa de seleção.  
  
###  <a name="BKMK_Stop__terminate__and_detach_commands"></a> Parar, finalizar e desanexar comandos  
  
|||  
|-|-|  
|**Comando**|**Descrição**|  
|**Depurar** menu:<br /><br /> -   **Parar a depuração**|A menos que o comportamento será alterado pela **processos** janela **desanexar ao parar a depuração** opção:<br /><br /> 1.  Processos iniciados pelo depurador terminaram.<br />2.  Os processos anexados são separados do depurador.|  
|**Depurar** menu:<br /><br /> -   **Finalizar tudo**|Todos os processos são encerrados.|  
|**Depurar** menu:<br /><br /> -   **Desanexar tudo**|O depurador desanexa todos os processos.|  
|**Processos** menu de contexto da janela:<br /><br /> -   **Desanexar processo**|O depurador dispara do processo selecionado.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
|**Processos** menu de contexto da janela:<br /><br /> -   **Encerrar processo**|O processo selecionado é finalizado.<br /><br /> Outros processos mantém o estado existente (suspenso ou em execução).|  
|**Processos** menu de contexto da janela:<br /><br /> -   **Desanexar ao parar a depuração**|Alterna o comportamento de **Debug**, **parar depuração** do processo selecionado:<br /><br /> -Checked: O depurador dispara do processo.<br />-Limpo: O processo é encerrado.|  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [parar a depuração, finalizar ou desanexar dos processos](../debugger/debug-multiple-processes.md#BKMK_Stop_debugging__terminate_or_detach_from_processes)  
  
 ![Voltar ao início](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Conteúdo](#BKMK_Contents)  
  
## <a name="see-also"></a>Consulte também  
 [Especifique o símbolo (. PDB) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [Anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [Navegar pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md)   
 [Depuração Just-In-Time](../debugger/just-in-time-debugging-in-visual-studio.md)   
 [Depurar aplicativos multi-threaded](../debugger/debug-multithreaded-applications-in-visual-studio.md)




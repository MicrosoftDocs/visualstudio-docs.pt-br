---
title: Depurando código de GPU | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: c7e77a5a-cb57-4b11-9187-ecc89acc8775
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0c0fdab78364eaf4c0f9fd86753b8ca1c4178415
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670182"
---
# <a name="debugging-gpu-code"></a>Depurando código de GPU
Você pode depurar código C++ que está sendo executado na unidade de processamento gráfico (GPU). O suporte à depuração de GPU no Visual Studio inclui a detecção de concorrência, início de processos e anexação a eles, e a integração nas janelas de depuração.  
  
## <a name="supported-platforms"></a>Plataformas compatíveis  
 A depuração tem suporte no [!INCLUDE[win7](../debugger/includes/win7_md.md)], no [!INCLUDE[win8](../debugger/includes/win8_md.md)], no [!INCLUDE[winsvr08_r2](../debugger/includes/winsvr08_r2_md.md)] e no [!INCLUDE[winserver8](../debugger/includes/winserver8_md.md)]. Para depurar no emulador de software, é necessário o [!INCLUDE[win8](../debugger/includes/win8_md.md)] ou [!INCLUDE[winserver8](../debugger/includes/winserver8_md.md)]. Para depurar no hardware, você deve instalar os drivers para a sua placa gráfica. Nem todos os fornecedores de hardware implementam todos os recursos do depurador. Consulte a documentação do fornecedor para conhecer as restrições.  
  
> [!NOTE]
>  Fornecedores de hardware independentes que desejam oferecer suporte à depuração de GPU no Visual Studio devem criar uma DLL que implementa a interface do VSD3DDebug e destinam-se a seus próprios drivers.  
  
## <a name="configuring-gpu-debugging"></a>Configurando a depuração de GPU  
 O depurador não pode interromper no código de CPU e no código de GPU na mesma execução do aplicativo. Por padrão, o depurador será interrompido no código da CPU. Para depurar o código de GPU, use uma destas duas etapas:  
  
-   No **tipo de depuração** lista os **padrão** barra de ferramentas, escolha **somente GPU**.  
  
-   Na **Gerenciador de soluções**, no menu de atalho para o projeto, escolha **propriedades**. No **páginas de propriedades** caixa de diálogo, selecione **depuração**e, em seguida, selecione **somente GPU** no **tipo de depurador** lista.  
  
## <a name="launching-and-attaching-to-applications"></a>Iniciando e anexando a aplicativos  
 Você pode usar os comandos de depuração do Visual Studio para iniciar e interromper a depuração de GPU. Para obter mais informações, veja [Navegação pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md). Você também pode anexar o depurador de GPU a um processo em execução, mas somente se esse processo executar o código de GPU. Para obter mais informações, consulte [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
## <a name="run-current-tile-to-cursor-and-run-to-cursor"></a>Executar o bloco atual até o cursor e executar até o cursor  
 Quando você estiver depurando no GPU, terá duas opções para executar até o local do cursor. Os comandos para as duas opções estão disponíveis no menu de atalho do editor de códigos.  
  
1.  O **executar até o Cursor** comando executa seu aplicativo até atingir o local do cursor e, em seguida, interrompe. Isso não significa que o thread atual é executado até o cursor; significa que o primeiro thread que alcançar o ponto do cursor dispara a interrupção. Consulte [navegar pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md)  
  
2.  O **executar bloco atual até o Cursor** comando executa seu aplicativo até que todos os threads no quadro atual atinjam o cursor e, em seguida, quebras.  
  
## <a name="debugging-windows"></a>Janelas de depuração  
 Ao usar determinadas janelas de depuração, você pode examinar, sinalizar e congelar threads de GPU. Para obter mais informações, consulte:  
  
-   [Usando a janela Pilhas Paralelas](../debugger/using-the-parallel-stacks-window.md)  
  
-   [Usando a janela Tarefas](../debugger/using-the-tasks-window.md)  
  
-   [Como usar a janela Inspeção Paralela](../debugger/how-to-use-the-parallel-watch-window.md)  
  
-   [Depurar Threads e processos](../debugger/debug-threads-and-processes.md) (barra de ferramentas do local de depuração)  
  
-   [Como usar a janela Threads da GPU](../debugger/how-to-use-the-gpu-threads-window.md)  
  
## <a name="data-synchronization-exceptions"></a>Exceções de sincronização de dados  
 O depurador pode identificar várias condições de sincronização de dados durante a execução. Quando uma condição for detectada, o depurador entrará no estado de interrupção. Você tem duas opções —**quebrar** ou **continuar**. Usando o **exceções** caixa de diálogo, você pode configurar se o depurador detecta essas condições e também quais condições ele interromperá. Para obter mais informações, consulte [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md). Você também pode usar o **opções** caixa de diálogo para especificar que o depurador deve ignorar exceções se os dados gravados não alterarem o valor dos dados. Para obter mais informações, consulte [geral, depuração, caixa de diálogo Opções](../debugger/general-debugging-options-dialog-box.md).  
  
## <a name="troubleshooting"></a>Solução de problemas  
  
### <a name="specifying-an-accelerator"></a>Especificando um acelerador  
 Pontos de interrupção no código de GPU serão atingidos apenas se o código está em execução no [accelerator::direct3d_ref](/cpp/parallel/amp/reference/accelerator-class#direct3d_ref) accelerator (REF). Se você não especificar um acelerador em seu código, o acelerador REF será selecionado automaticamente como o **tipo de acelerador de depuração** nas propriedades do projeto. Se seu código selecionar explicitamente um acelerador, o acelerador REF não será usado durante a depuração e os pontos de interrupção não serão atingidos a menos que seu hardware de GPU tiver suporte à depuração. Você pode solucionar isso escrevendo seu código de forma que use um acelerador REF durante a depuração. Para obter mais informações, consulte as propriedades do projeto e [usando objetos accelerator e accelerator_view](/cpp/parallel/amp/using-accelerator-and-accelerator-view-objects) e [configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md).  
  
### <a name="conditional-breakpoints"></a>Pontos de interrupção condicionais  
 Os pontos de interrupção condicionais no código de GPU têm suporte, mas nem todas as expressões podem ser avaliadas no dispositivo. Quando uma expressão não pode ser avaliada no dispositivo, ela será avaliada no depurador. O depurador provavelmente será executado com mais lentidão do que no dispositivo.  
  
### <a name="error-there-is-a-configuration-issue-with-the-selected-debugging-accelerator-type"></a>Erro: problema de configuração no Tipo de Acelerador de Depuração.  
 Esse erro ocorre quando há uma inconsistência entre as configurações de projeto e a configuração do PC no qual você está depurando. Para obter mais informações, consulte [configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md).  
  
### <a name="error-the-debug-driver-for-the-selected-debugging-accelerator-type-is-not-installed-on-the-target-machine"></a>Erro: o driver de depuração do Tipo de Acelerador de Depuração selecionado não está instalado no computador de destino.  
 Esse erro ocorrerá se você estiver depurando em um PC remoto. O depurador não poderá determinar até o tempo de execução se os drivers estiverem instalados no PC remoto. Os drivers estão disponíveis com o fabricante da placa gráfica.  
  
### <a name="error-timeout-detection-and-recovery-tdr-must-be-disabled-at-the-remote-site"></a>Erro: a TDR (Detecção de Tempo Limite e Recuperação) deve ser desabilitada no site remoto.  
 É possível que as computações de C++ AMP excedam o intervalo de tempo padrão que é definido pela detecção de tempo limite do Windows e pelo processo de recuperação (TDR). Quando isso acontecer, a computação será cancelada e os dados serão perdidos. Para obter mais informações, consulte [manipulando TDRs em C++ AMP](http://go.microsoft.com/fwlink/p/?LinkId=249154).  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Depurando um aplicativo C++ AMP](/cpp/parallel/amp/walkthrough-debugging-a-cpp-amp-application)   
 [Configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)   
 [Iniciar a depuração de GPU no Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=255381)
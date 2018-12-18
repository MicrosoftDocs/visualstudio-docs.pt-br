---
title: Usar arquivos de despejo no depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 11/05/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.crashdump
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- dumps, about dumps
- crash dumps
- dump files
- dumps
ms.assetid: b71be6dc-57e0-4730-99d2-b540a0863e49
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3e30f9d29ba3c922d70c8acdf7d4db5d8a1670fd
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53066948"
---
# <a name="dump-files-in-the-visual-studio-debugger"></a>Arquivos de despejo no depurador do Visual Studio

<a name="BKMK_What_is_a_dump_file_"></a> Um *arquivo de despejo* é um instantâneo que mostra o processo que estava em execução e os módulos que foram carregados para um aplicativo em um ponto no tempo. Um despejo com informações de heap também inclui um instantâneo de memória do aplicativo neste ponto. 

Abrir um arquivo de despejo com um heap no Visual Studio é algo como parar em um ponto de interrupção em uma sessão de depuração. Embora você não pode continuar a execução, você pode examinar as pilhas, threads e valores de variáveis do aplicativo no momento do despejo.

Despejos de memória são usados principalmente para depurar problemas de máquinas que os desenvolvedores não têm acesso ao. Quando você não pode reproduzir uma falha ou suspensão em seu próprio computador, você pode usar um arquivo de despejo de uma máquina do cliente. Os testadores também criarem despejos para salvar a crash ou dados a serem usados para testar mais de suspensão. 

O depurador do Visual Studio pode salvar arquivos de despejo para código gerenciado ou nativo. Ele pode depurar arquivos de despejo criados pelo Visual Studio ou por outros aplicativos que salvam arquivos na *minidespejo* formato.

##  <a name="BKMK_Requirements_and_limitations"></a> Requisitos e limitações

-   Para depurar arquivos de despejo de computadores de 64 bits, o Visual Studio deve estar executando em um computador de 64 bits.

-   O Visual Studio pode depurar arquivos de despejo de aplicativos nativos em dispositivos ARM. Ele também pode depurar despejos de aplicativos gerenciados em dispositivos ARM, mas somente no depurador nativo.

-   Para depurar [modo de kernel](/windows-hardware/drivers/debugger/kernel-mode-dump-files) arquivos de despejo ou usar o [SOS. dll](/dotnet/framework/tools/sos-dll-sos-debugging-extension) depuração extensão no Visual Studio, baixe as ferramentas de depuração para Windows no [Windows Driver Kit (WDK)](/windows-hardware/drivers/download-the-wdk).

-   Visual Studio não pode depurar arquivos de despejo salvos na antiga [despejo completo do usuário-modo](/windows/desktop/wer/collecting-user-mode-dumps) formato. Um despejo completo do modo de usuário não é o mesmo que um despejo com heap.

-   Depurar arquivos de despejo de código otimizado pode ser confuso. Por exemplo, as funções embutidas do compilador podem resultar em pilhas de chamadas inesperadas, e outras otimizações podem alterar o tempo de vida de variáveis.

##  <a name="BKMK_Dump_files__with_or_without_heaps"></a> Arquivos de despejo com ou sem heaps

Arquivos de despejo podem ou não ter informações de heap.

-   **Arquivos de despejo com heaps** contêm um instantâneo da memória do aplicativo, incluindo os valores das variáveis, no momento do despejo. O Visual Studio também salva os binários de módulos nativos carregados em um arquivo de despejo com um heap, o que pode tornar a depuração muito mais fácil. Visual Studio pode carregar símbolos de um arquivo de despejo com um heap, mesmo se ele não é possível localizar um aplicativo binário. 

-   **Arquivos de despejo sem heaps** são muito menor do que despejos com heaps, mas o depurador deve carregar os binários de aplicativo para localizar informações de símbolo. Os binários carregados devem corresponder exatamente aqueles em execução durante a criação de despejo. Arquivos de despejo sem heaps salvar os valores das variáveis de pilha apenas.

##  <a name="BKMK_Create_a_dump_file"></a> Criar um arquivo de despejo

Enquanto você estiver depurando um processo no Visual Studio, você pode salvar um despejo de memória quando o depurador foi interrompido em um ponto de interrupção ou exceção. 

Com o [depuração Just-in-](../debugger/just-in-time-debugging-in-visual-studio.md) habilitado, você pode anexar o depurador do Visual Studio a um processo travado fora do Visual Studio e, em seguida, salve um arquivo de despejo do depurador. Ver [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).

**Para salvar um arquivo de despejo:**

1. Enquanto estiver parado em um ponto de interrupção ou um erro durante a depuração, selecione **Debug** > **Salvar despejo como**. 

1. No **Salvar despejo como** caixa de diálogo **Salvar como tipo**, selecione **minidespejo** ou **minidespejo com Heap** (o padrão).

1. Procure um caminho, selecione um nome para o arquivo de despejo e, em seguida, selecione **salvar**. 

>[!NOTE]
>Você pode criar arquivos de despejo com qualquer programa que ofereça suporte ao formato de minidespejo do Windows. Por exemplo, o utilitário de linha de comando **Procdump** do [Windows Sysinternals](http://technet.microsoft.com/sysinternals/default) pode criar arquivos de despejo de memória do processo com base em gatilhos ou sob demanda. Ver [requisitos e limitações](../debugger/using-dump-files.md#BKMK_Requirements_and_limitations) para obter informações sobre como usar outras ferramentas para criar arquivos de despejo.

##  <a name="BKMK_Open_a_dump_file"></a> Abrir um arquivo de despejo

1. No Visual Studio, selecione **arquivo** > **abra** > **arquivo**.

1. Na caixa de diálogo **Abrir Arquivo**, localize e selecione o arquivo de despejo. Geralmente, ele terá uma extensão *.dmp*. Selecione **OK**.

   O **resumo de arquivo de minidespejo** janela mostra o resumo e módulo de informações para o arquivo de despejo e ações você pode tomar.

   ![Página de resumo de minidespejo](../debugger/media/dbg_dump_summarypage.png "página de resumo de minidespejo")

1. Sob **ações**:
   - Para definir os locais de carregamento de símbolo, selecione **definir caminhos de símbolo**.
   - Para iniciar a depuração, selecione **depurar com somente gerenciado**, **depurar somente com nativo**, **depurar com misto**, ou **depurar com memória gerenciada**.

##  <a name="BKMK_Find_binaries__symbol___pdb__files__and_source_files"></a> Localizar .exe,. PDB e arquivos de origem

Para usar o total de recursos em um arquivo de despejo de depuração Visual Studio precisa de:

- O *.exe* arquivo o despejo foi criado para e outros binários (dll, etc.) que o processo de despejo usado.
- Arquivos de símbolo (*.pdb*) para o *.exe* e outros binários.
- O *.exe* e *. PDB* arquivos que correspondem exatamente a versão e compilação dos arquivos na criação de despejo.
- Arquivos de origem para os módulos relevantes. Se você não encontrar os arquivos de origem, você pode usar a desmontagem dos módulos.

Se o despejo tem dados de heap, o Visual Studio poderá lidar com binários ausentes para alguns módulos, mas deverá ter binários para módulos suficientes de modo a gerar pilhas de chamadas válidas. 

### <a name="search-paths-for-exe-files"></a>Caminhos de pesquisa para arquivos .exe

Esses locais para o Visual Studio pesquisa automaticamente *.exe* arquivos que não estão incluídos no arquivo de despejo:

1. A pasta que contém o arquivo de despejo.
2. O caminho do módulo que especifica o arquivo de despejo, o que é o caminho do módulo no computador que o despejo de coletadas.
3. Os caminhos de símbolo especificados na **ferramentas** (ou **Debug**) > **opções** > **depuração**  >  **Símbolos**. Você também pode abrir o **símbolos** página da **ações** painel da **resumo do arquivo de despejo** janela. Nessa página, você pode adicionar mais locais para pesquisa.

### <a name="use-the-no-binary-no-symbols-or-no-source-found-pages"></a>Use as páginas nenhum binário, nenhum símbolo ou nenhuma origem encontrada

Se o Visual Studio não é possível localizar os arquivos ele precisa depurar um módulo no despejo, ele mostra uma **nenhum binário encontrado**, **nenhum símbolo encontrado**, ou **nenhuma origem encontrada** página. Essas páginas fornecem informações detalhadas sobre a causa do problema e fornecem links de ação que podem ajudá-lo a localizar os arquivos. Confira [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="see-also"></a>Consulte também

- [Depuração Just-In-Time](../debugger/just-in-time-debugging-in-visual-studio.md)
- [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [IntelliTrace](../debugger/intellitrace.md)
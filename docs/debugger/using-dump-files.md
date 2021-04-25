---
title: Usar arquivos de despejo no depurador | Microsoft Docs
description: Um arquivo de despejo é um instantâneo de um aplicativo em execução e de módulos carregados. Considere a criação de um arquivo de despejo para situações em que você não tenha acesso de depuração ao aplicativo.
ms.custom: SEO-VS-2020, seodec18
ms.date: 11/05/2018
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f3b72db232e5e83a0d83fbab1d1223da507054d9
ms.sourcegitcommit: 925db7adb9cb554b081c7e727d09680d4863feed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2021
ms.locfileid: "107941117"
---
# <a name="dump-files-in-the-visual-studio-debugger"></a>Arquivos de despejo no depurador do Visual Studio

<a name="BKMK_What_is_a_dump_file_"></a> Um *arquivo de despejo* é um instantâneo que mostra o processo que estava em execução e os módulos que foram carregados para um aplicativo em um ponto no tempo. Um despejo com informações de heap também inclui um instantâneo da memória do aplicativo nesse ponto.

Abrir um arquivo de despejo com um heap no Visual Studio é algo como parar em um ponto de interrupção em uma sessão de depuração. Embora não seja possível continuar a execução, você pode examinar as pilhas, os threads e os valores de variáveis do aplicativo no momento do despejo.

Os despejos são usados principalmente para depurar problemas de computadores aos quais os desenvolvedores não têm acesso. Você pode usar um arquivo de despejo da máquina de um cliente quando não puder reproduzir um programa de falha ou sem resposta em seu próprio computador. Os testadores também criam despejos para salvar dados de programas sem resposta ou com falhas para serem usados em mais testes.

O depurador do Visual Studio pode salvar arquivos de despejo para código gerenciado ou nativo. Ele pode depurar arquivos de despejo criados pelo Visual Studio ou por outros aplicativos que salvam arquivos no formato de *minidespejo* .

## <a name="requirements-and-limitations"></a><a name="BKMK_Requirements_and_limitations"></a> Requisitos e limitações

- Para depurar arquivos de despejo de computadores de 64 bits, o Visual Studio deve estar em execução em um computador de 64 bits.

::: moniker range=">= vs-2019"
- O Visual Studio pode depurar arquivos de despejo de aplicativos gerenciados do SO Linux. 
::: moniker-end

- O Visual Studio pode depurar arquivos de despejo de aplicativos nativos em dispositivos ARM. Ele também pode depurar despejos de aplicativos gerenciados de dispositivos ARM, mas apenas no depurador nativo.

- Para depurar arquivos de despejo no [modo kernel](/windows-hardware/drivers/debugger/kernel-mode-dump-files) ou usar a extensão de depuração [SOS.dll](/dotnet/framework/tools/sos-dll-sos-debugging-extension) no Visual Studio, baixe as ferramentas de depuração para Windows no [Windows Driver Kit (WDK)](/windows-hardware/drivers/download-the-wdk).

- O Visual Studio não pode depurar arquivos de despejo salvos no formato de [despejo do modo de usuário completo](/windows/desktop/wer/collecting-user-mode-dumps) mais antigo. Um despejo de modo de usuário completo não é o mesmo que um despejo com heap.

- Depurar arquivos de despejo de código otimizado pode ser confuso. Por exemplo, as funções embutidas do compilador podem resultar em pilhas de chamadas inesperadas, e outras otimizações podem alterar o tempo de vida de variáveis.

## <a name="dump-files-with-or-without-heaps"></a><a name="BKMK_Dump_files__with_or_without_heaps"></a> Arquivos de despejo com ou sem heaps

Arquivos de despejo podem ou não ter informações de heap.

- **Arquivos de despejo com heaps** contêm um instantâneo da memória do aplicativo, incluindo os valores das variáveis, no momento do despejo. O Visual Studio também salva os binários de módulos nativos carregados em um arquivo de despejo com um heap, o que pode tornar a depuração muito mais fácil. O Visual Studio pode carregar símbolos de um arquivo de despejo com um heap, mesmo que ele não encontre um binário do aplicativo.

- **Arquivos de despejo sem heaps** são muito menores do que despejos com heaps, mas o depurador deve carregar os binários do aplicativo para localizar informações de símbolo. Os binários carregados devem corresponder exatamente àqueles em execução durante a criação do despejo. Arquivos de despejo sem heaps salvam apenas os valores das variáveis de pilha.

## <a name="create-a-dump-file"></a><a name="BKMK_Create_a_dump_file"></a> Criar um arquivo de despejo

Enquanto você estiver depurando um processo no Visual Studio, poderá salvar um despejo quando o depurador for interrompido em uma exceção ou ponto de interrupção.

Com a [depuração Just-in-time](../debugger/just-in-time-debugging-in-visual-studio.md) habilitada, você pode anexar o depurador do Visual Studio a um processo que falhou fora do Visual Studio e, em seguida, salvar um arquivo de despejo do depurador. Consulte [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).

**Para salvar um arquivo de despejo:**

1. Ao parar em um erro ou ponto de interrupção durante a depuração, selecione **depurar**  >  **despejo de depuração como**.

1. Na caixa de diálogo **Salvar despejo como** , em **salvar como tipo**, selecione **minidespejo** ou **minidespejo com heap** (o padrão).

1. Navegue até um caminho e selecione um nome para o arquivo de despejo e, em seguida, selecione **salvar**.

>[!NOTE]
>Você pode criar arquivos de despejo com qualquer programa que dê suporte ao formato de minidespejo do Windows. Por exemplo, o utilitário de linha de comando **Procdump** do [Windows Sysinternals](/sysinternals/) pode criar arquivos de despejo de memória do processo com base em gatilhos ou sob demanda. Consulte [requisitos e limitações](../debugger/using-dump-files.md#BKMK_Requirements_and_limitations) para obter informações sobre como usar outras ferramentas para criar arquivos de despejo.

## <a name="open-a-dump-file"></a><a name="BKMK_Open_a_dump_file"></a> Abrir um arquivo de despejo

1. No Visual Studio, selecione **arquivo**  >  **abrir**  >  **arquivo**.

1. Na caixa de diálogo **Abrir Arquivo**, localize e selecione o arquivo de despejo. Normalmente, ele terá uma extensão *. dmp* . Selecione **OK**.

   A janela **Resumo do arquivo de minidespejo** mostra informações de resumo e módulo para o arquivo de despejo e as ações que você pode executar.

   ![Página de resumo do minidespejo](../debugger/media/dbg_dump_summarypage.png "Página de resumo do minidespejo")

1. Em **ações**:
   - Para definir locais de carregamento de símbolos, selecione **definir caminhos de símbolo**.
   - Para iniciar a depuração, selecione **depurar com somente gerenciado**, **Depurar somente nativo**, **depurar com misto** ou **depurar com memória gerenciada**.

## <a name="find-exe-pdb-and-source-files"></a><a name="BKMK_Find_binaries__symbol___pdb__files__and_source_files"></a> Localizar arquivos. exe,. PDB e de origem

Para usar recursos de depuração completos em um arquivo de despejo, o Visual Studio precisa:

- O arquivo *. exe* do qual o despejo foi criado e outros binários (DLLs, etc.) que o processo de despejo usou.
- Arquivos de símbolo (*. pdb*) para o *. exe* e outros binários.
- Os arquivos *. exe* e *. pdb* que correspondem exatamente à versão e à compilação dos arquivos na criação de despejo.
- Arquivos de origem para os módulos relevantes. Você pode usar a desmontagem dos módulos se não conseguir localizar os arquivos de origem.

Se o despejo tiver dados de heap, o Visual Studio poderá lidar com binários ausentes para alguns módulos, mas deve ter binários para módulos suficientes para gerar pilhas de chamadas válidas.

### <a name="search-paths-for-exe-files"></a>Caminhos de pesquisa para arquivos. exe

O Visual Studio pesquisa automaticamente esses locais para arquivos *. exe* que não estão incluídos no arquivo de despejo:

1. A pasta que contém o arquivo de despejo.
2. O caminho do módulo que o arquivo de despejo especifica, que é o caminho do módulo no computador que coletou o despejo.
3. Os caminhos de símbolo especificados em **ferramentas** (ou **depuração**) > **Opções** de  >  **depuração** de  >  **símbolos**. Você também pode abrir a página **símbolos** no painel **ações** da janela **Resumo do arquivo de despejo** . Nessa página, você pode adicionar mais locais para pesquisa.

### <a name="use-the-no-binary-no-symbols-or-no-source-found-pages"></a>Use as páginas nenhum binário, nenhum símbolo ou nenhuma fonte encontrada

Se o Visual Studio não conseguir localizar os arquivos necessários para depurar um módulo no despejo, ele mostrará um **binário não encontrado**, **nenhum símbolo encontrado** ou **nenhuma página de origem encontrada** . Essas páginas fornecem informações detalhadas sobre a causa do problema e fornecem links de ação que podem ajudá-lo a localizar os arquivos. Consulte [especificar símbolo (. pdb) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="see-also"></a>Confira também

- [Como depurar um despejo de memória gerenciado com analisadores de diagnóstico do .NET](../debugger/how-to-debug-managed-memory-dump.md)
- [Depuração Just-in-time](../debugger/just-in-time-debugging-in-visual-studio.md)
- [Especificar o símbolo (. pdb) e os arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [IntelliTrace](../debugger/intellitrace.md)
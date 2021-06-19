---
title: Usar arquivos de despejo no arquivo de depurador | Microsoft Docs
description: Um arquivo de despejo é um instantâneo de um aplicativo em execução e módulos carregados. Considere criar um arquivo de despejo para situações em que você não tem acesso de depuração ao aplicativo.
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 1496c50d6a4022083a5cd093a0682ef36c70bbaa
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389222"
---
# <a name="dump-files-in-the-visual-studio-debugger"></a>Despejar arquivos no Visual Studio depurador

<a name="BKMK_What_is_a_dump_file_"></a> Um *arquivo de despejo* é um instantâneo que mostra o processo que estava em execução e os módulos que foram carregados para um aplicativo em um ponto no tempo. Um despejo com informações de heap também inclui um instantâneo da memória do aplicativo nesse ponto.

Abrir um arquivo de despejo com um heap Visual Studio é algo como parar em um ponto de interrupção em uma sessão de depuração. Embora não seja possível continuar a execução, você pode examinar as pilhas, threads e valores variáveis do aplicativo no momento do despejo.

Despejos são usados principalmente para depurar problemas de máquinas aos que os desenvolvedores não têm acesso. Você pode usar um arquivo de despejo do computador de um cliente quando não é possível reproduzir um programa com falha ou sem resposta em seu próprio computador. Os testadores também criam despejos para salvar dados de programa com falha ou sem resposta a ser usado para mais testes.

O depurador do Visual Studio pode salvar arquivos de despejo para código gerenciado ou nativo. Ele pode depurar arquivos de despejo criados por Visual Studio ou por outros aplicativos que salvam arquivos no *formato de minidump.*

## <a name="requirements-and-limitations"></a><a name="BKMK_Requirements_and_limitations"></a> Requisitos e limitações

- Para depurar arquivos de despejo de máquinas de 64 bits, Visual Studio deve estar em execução em um computador de 64 bits.

::: moniker range=">= vs-2019"
- Visual Studio pode depurar arquivos de despejo de aplicativos gerenciados do sistema operacional Linux. 
::: moniker-end

- O Visual Studio pode depurar arquivos de despejo de aplicativos nativos em dispositivos ARM. Ele também pode depurar despejos de aplicativos gerenciados de dispositivos ARM, mas somente no depurador nativo.

- Para depurar [arquivos](/windows-hardware/drivers/debugger/kernel-mode-dump-files) de despejo no modo kernel ou usarSOS.dllextensão de depuração do [Visual Studio,](/dotnet/framework/tools/sos-dll-sos-debugging-extension) baixe as ferramentas de depuração para Windows no [WDK (Kit de Driver do Windows (WDK)).](/windows-hardware/drivers/download-the-wdk)

- Visual Studio pode depurar arquivos de despejo salvos no formato de despejo de modo [de](/windows/desktop/wer/collecting-user-mode-dumps) usuário completo mais antigo. Um despejo de modo de usuário completo não é o mesmo que um despejo com heap.

- Depurar arquivos de despejo de código otimizado pode ser confuso. Por exemplo, as funções embutidas do compilador podem resultar em pilhas de chamadas inesperadas, e outras otimizações podem alterar o tempo de vida de variáveis.

## <a name="dump-files-with-or-without-heaps"></a><a name="BKMK_Dump_files__with_or_without_heaps"></a> Arquivos de despejo com ou sem heaps

Os arquivos de despejo podem ou não ter informações de heap.

- **Os arquivos de despejo com heaps** contêm um instantâneo da memória do aplicativo, incluindo os valores de variáveis, no momento do despejo. Visual Studio também salva os binários dos módulos nativos carregados em um arquivo de despejo com um heap, o que pode facilitar muito a depuração. Visual Studio pode carregar símbolos de um arquivo de despejo com um heap, mesmo que ele não possa encontrar um binário do aplicativo.

- **Os arquivos de despejo sem heaps** são muito menores do que despejos com heaps, mas o depurador deve carregar os binários do aplicativo para encontrar informações de símbolo. Os binários carregados devem corresponder exatamente aos executados durante a criação do despejo. Os arquivos de despejo sem heaps salvam apenas os valores de variáveis de pilha.

## <a name="create-a-dump-file"></a><a name="BKMK_Create_a_dump_file"></a> Criar um arquivo de despejo

Enquanto estiver depurando um processo no Visual Studio, você poderá salvar um despejo quando o depurador for interrompido em uma exceção ou ponto de interrupção.

Com a [Depuração Just-In-Time](../debugger/just-in-time-debugging-in-visual-studio.md) habilitada, você pode anexar o depurador Visual Studio a um processo com problema fora do Visual Studio e salvar um arquivo de despejo do depurador. Consulte [Anexar a processos em execução.](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)

**Para salvar um arquivo de despejo:**

1. Enquanto estiver parado em um erro ou ponto de interrupção durante a depuração, selecione **Depurar**  >  **Salvar Despejo como**.

1. Na caixa de diálogo Salvar **Despejo como,** em **Salvar como tipo**, selecione **Minidump** ou **Minidump com Heap** (o padrão).

1. Navegue até um caminho, selecione um nome para o arquivo de despejo e, em seguida, **selecione Salvar**.

>[!NOTE]
>Você pode criar arquivos de despejo com qualquer programa que dá suporte ao formato de minidump do Windows. Por exemplo, o utilitário de linha de comando **Procdump** do [Windows Sysinternals](/sysinternals/) pode criar arquivos de despejo de memória do processo com base em gatilhos ou sob demanda. Consulte [Requisitos e limitações para](../debugger/using-dump-files.md#BKMK_Requirements_and_limitations) obter informações sobre como usar outras ferramentas para criar arquivos de despejo.

## <a name="open-a-dump-file"></a><a name="BKMK_Open_a_dump_file"></a> Abrir um arquivo de despejo

1. No Visual Studio, selecione **Arquivo**  >  **Aberto**  >  **arquivo**.

1. Na caixa de diálogo **Abrir Arquivo**, localize e selecione o arquivo de despejo. Normalmente, ele terá uma *extensão .dmp.* Selecione **OK**.

   A **janela Resumo do Arquivo de Minidump** mostra informações de resumo e módulo para o arquivo de despejo e as ações que você pode tomar.

   ![Página de resumo do minidump](../debugger/media/dbg_dump_summarypage.png "Página de resumo do minidump")

1. Em **Ações**:
   - Para definir locais de carregamento de símbolos, selecione **Definir caminhos de símbolo.**
   - Para iniciar a depuração, selecione **Depurar** com Somente Gerenciado, **Depurar** com Somente Nativo, **Depurar** com Misto ou **Depurar com Memória Gerenciada.**

## <a name="find-exe-pdb-and-source-files"></a><a name="BKMK_Find_binaries__symbol___pdb__files__and_source_files"></a> Encontrar .exe, .pdb e arquivos de origem

Para usar recursos completos de depuração em um arquivo de despejo, Visual Studio precisa:

- O *.exe* arquivo para o que o despejo foi criado e outros binários (DLLs, etc.) usados pelo processo de despejo.
- Arquivos symbol (*.pdb*) para o *.exe* e outros binários.
- Os *arquivos.exe* e *.pdb* que exatamente corresponderem à versão e ao build dos arquivos na criação do despejo.
- Arquivos de origem para os módulos relevantes. Você poderá usar a desmontagem dos módulos se não conseguir encontrar os arquivos de origem.

Se o despejo tiver dados de heap, Visual Studio poderá lidar com binários ausentes para alguns módulos, mas deve ter binários para módulos suficientes para gerar pilhas de chamada válidas.

### <a name="search-paths-for-exe-files"></a>Caminhos de pesquisa para .exe arquivos

Visual Studio pesquisa automaticamente esses locais.exe *arquivos* que não estão incluídos no arquivo de despejo:

1. A pasta que contém o arquivo de despejo.
2. O caminho do módulo especificado pelo arquivo de despejo, que é o caminho do módulo no computador que coletou o despejo.
3. Os caminhos de símbolo especificados em **Ferramentas** (ou **Depurar**) > **símbolos**  >  **de depuração.**  >   Você também pode abrir a **página Símbolos** no painel **Ações** da janela Resumo **do Arquivo de** Despejo. Nesta página, você pode adicionar mais locais para pesquisar.

### <a name="use-the-no-binary-no-symbols-or-no-source-found-pages"></a>Use as páginas Sem Binário, Sem Símbolos ou Nenhuma Fonte Encontrada

Se Visual Studio puder encontrar os arquivos **necessários** para depurar um módulo no despejo, ele mostrará uma página Nenhum Binário **Encontrado,** Nenhum Símbolo Encontrado ou Nenhuma Fonte **Encontrada.** Essas páginas fornecem informações detalhadas sobre a causa do problema e fornecem links de ação que podem ajudá-lo a localizar os arquivos. Consulte [Especificar arquivos de símbolo (.pdb) e de origem.](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)

## <a name="see-also"></a>Confira também

- [Como depurar um despejo de memória gerenciado com analisadores de diagnóstico do .NET](../debugger/how-to-debug-managed-memory-dump.md)
- [Depuração Just-In-Time](../debugger/just-in-time-debugging-in-visual-studio.md)
- [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [IntelliTrace](../debugger/intellitrace.md)
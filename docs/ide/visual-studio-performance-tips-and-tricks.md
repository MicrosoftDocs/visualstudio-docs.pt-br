---
title: Dicas para melhorar o desempenho
ms.date: 08/14/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e1c4e55fe6275d750d3bc3b03fb8f0ac5eec2751
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672919"
---
# <a name="visual-studio-performance-tips-and-tricks"></a>Dicas e truques de desempenho do Visual Studio

As recomendações de desempenho do Visual Studio destinam-se a situações de baixa memória, o que podem ocorrer em casos raros. Nessas situações, é possível otimizar determinados recursos do Visual Studio que você talvez não esteja usando. As dicas a seguir não devem ser consideradas como as recomendações gerais.

> [!NOTE]
> Se você estiver tendo dificuldades para usar o produto devido a problemas de memória, conte para nós pela [ferramenta de comentários](../ide/how-to-report-a-problem-with-visual-studio-2017.md).

## <a name="use-a-64-bit-os"></a>Usar um sistema operacional de 64 bits

Se você atualizar seu sistema de uma versão de 32 bits do Windows para uma versão de 64 bits, expanda a quantidade de memória virtual disponível para o Visual Studio de 2 GB para 4 GB. Isso permite que o Visual Studio lide com cargas de trabalho significativamente maiores, mesmo sendo um processo de 32 bits.

Para obter mais informações, consulte [Limites de memória](/windows/desktop/Memory/memory-limits-for-windows-releases#memory_limits) e [Usar /LARGEADDRESSAWARE no Windows de 64 bits](https://blogs.msdn.microsoft.com/oldnewthing/20050601-24/?p=35483/).

## <a name="disable-automatic-file-restore"></a>Desabilitar a restauração de arquivo automática

O Visual Studio reabre automaticamente os documentos que foram deixados abertos na sessão anterior. Isso pode prolongar o tempo necessário para carregar uma solução em até 30% ou mais, dependendo do tipo de projeto e dos documentos sendo abertos. Designers como o Windows Forms e o XAML e alguns arquivos JavaScript e typescript, podem demorar para abrir.

O Visual Studio notifica você em uma barra amarela quando a restauração automática de documentos está fazendo com que a solução seja carregada de maneira significativamente mais lenta. Você pode desabilitar a reabertura de arquivo automática seguindo estas etapas:

1. Selecione **Ferramentas** > **Opções** para abrir a caixa de diálogo **Opções**.

1. Na página **Projetos e Soluções** > **Geral**, desmarque a opção **Reabrir documentos ao carregar a solução**.

Caso você desabilite a restauração automática de arquivos, uma maneira rápida de navegar para os arquivos que deseja abrir é usar um dos comandos [Ir para](../ide/go-to.md):

- Para a funcionalidade **Ir para** general, selecione **Editar** > **Ir para** > **Ir para Todos** ou pressione **Ctrl**+**T**.

- No Visual Studio 2017 versão 15.8 e posterior, você pode pular para o local da última edição em uma solução usando **Editar** > **Ir para** > **Ir para Local da Última Edição** ou pressionando **Ctrl**+**Shift**+**Backspace**.

- No Visual Studio 2017 versão 15.8 e posteriores, use **Ir para Arquivo Recente** para ver uma lista de arquivos visitados recentemente em uma solução. Selecione **Editar** > **Ir para** > **Ir para Arquivo Recente** ou pressione **Ctrl**+**1**, **Ctrl**+**R**.

## <a name="configure-debugging-options"></a>Configurar as opções de depuração

Se você tem ficado com pouca memória durante as sessões de depuração normalmente, você pode otimizar o desempenho fazendo uma ou mais alterações de configuração.

- **Habilitar Apenas Meu Código**

    A otimização mais simples é habilitar o recurso **Apenas Meu Código**, que só carrega símbolos para o seu projeto. Habilitar esse recurso pode resultar em uma economia significativa de memória para depurar aplicativos gerenciados (.NET). Esta opção já fica habilitada por padrão em alguns tipos de projeto.

    Para habilitar o **Apenas Meu Código**, escolha **Ferramentas** > **Opções** > **Depuração** > **Geral** e selecione **Habilitar Apenas Meu Código**.

- **Especificar os símbolos a serem carregados**

    Para depuração nativa, o carregamento de arquivos de símbolo (*.pdb*) é caro em termos de recursos de memória. Você pode definir as configurações de símbolo de depuração para economizar memória. Normalmente, você pode configurar a solução para carregar somente os módulos do seu projeto.

    Para especificar o carregamento de símbolos, escolha **Ferramentas** > **Opções** > **Depuração** > **Símbolos**.

    Defina as opções para **Somente os módulos especificados** em vez de **Todos os módulos** e, em seguida, especifique quais módulos você deseja carregar. Durante a depuração, você também pode clicar com o botão direito do mouse em módulos específicos na janela **Módulos** para incluir explicitamente um módulo no carregamento de símbolo. (Para abrir a janela durante a depuração, escolha **Depuração** > **Janelas** > **Módulos**.)

    Para obter mais informações, consulte [Noções básicas sobre arquivos de símbolo](https://blogs.msdn.microsoft.com/visualstudioalm/2015/01/05/understanding-symbol-files-and-visual-studios-symbol-settings/).

- **Desabilitar Ferramentas de Diagnóstico**

    É recomendável desabilitar a criação de perfil de CPU após o uso. Esse recurso pode consumir grandes quantidades de recursos. Quando a criação de perfil de CPU está habilitada, esse estado é mantido nas sessões de depuração subsequentes, por isso vale a pena desativá-lo explicitamente após terminar. Você pode economizar alguns recursos desabilitando as ferramentas de diagnóstico durante a depuração se você não precisar dos recursos fornecidos.

    Para desabilitar as **Ferramentas de Diagnóstico**, inicie uma sessão de depuração, escolha **Ferramentas** > **Opções** > **Habilitar Ferramentas de Diagnóstico** e desmarque a opção.

    Para obter mais informações, consulte [Ferramentas de Criação de Perfil](../profiling/profiling-feature-tour.md).

## <a name="disable-tools-and-extensions"></a>Desabilitar ferramentas e extensões

Algumas ferramentas ou extensões podem ser desabilitadas para melhorar o desempenho.

> [!TIP]
> Geralmente, é possível isolar problemas de desempenho desativando as extensões, uma por vez e verificando novamente o desempenho.

### <a name="managed-language-service-roslyn"></a>Serviço de linguagem gerenciado (Roslyn)

Para obter mais informações sobre as considerações de desempenho do .NET Compiler Platform (“Roslyn"), consulte [Considerações de desempenho para grandes soluções](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions).

- **Desabilitar análise completa da solução**

    O Visual Studio executa a análise em toda a sua solução para proporcionar uma experiência avançada sobre os erros antes de invocar um build. Esse recurso é útil para identificar erros assim que possível. No entanto, para soluções grandes, esse recurso pode consumir recursos significativos de memória. Se você estiver tendo problemas semelhantes ou pressão de memória, desabilite essa experiência para liberar esses recursos. Por padrão, essa opção é habilitada para o Visual Basic e desabilitada para C#.

    Para desabilitar a **Análise Completa da Solução**, escolha **Ferramentas** > **Opções** > **Editor de Texto** e selecione **Visual Basic** ou **C#**. Escolha **Avançado** e desmarque **Habilitar análise de solução completa**.

- **Desabilitar CodeLens**

    O Visual Studio executa uma tarefa **Localizar todas as referências** em cada método como exibido. O CodeLens fornece recursos como a exibição embutida do número de referências. O trabalho é executado em um processo separado como *ServiceHub.RoslynCodeAnalysisService32*. Em soluções grandes ou em sistemas com recursos restritos, esse recurso pode afetar significativamente o desempenho. Se estiver enfrentando problemas de memória, por exemplo, ao carregar uma solução grande em um computador de 4 GB, ou alta utilização da CPU para esse processo, você poderá desabilitar o CodeLens para liberar recursos.

    Para desabilitar o **CodeLens**, escolha **Ferramentas** > **Opções** > **Editor de Texto** > **Todas as Linguagens** > **CodeLens** e desmarque o recurso.

    > [!NOTE]
    > O CodeLens está disponível nas edições Professional e Enterprise do Visual Studio.

### <a name="other-tools-and-extensions"></a>Outras ferramentas e extensões

- **Desabilitar extensões**

    Extensões são componentes de software adicionais acrescentados ao Visual Studio que fornecem uma funcionalidade nova ou estendem a funcionalidade existente. Extensões geralmente podem ser uma fonte de problemas de recursos de memória. Se você estiver tendo problemas de recursos de memória, tente desabilitar as extensões, uma por vez, para ver como ele afeta o cenário ou o fluxo de trabalho.

    Para desabilitar as extensões, acesse **Ferramentas** > **Extensões e Atualizações** e desabilite uma extensão específica.

- **Desabilitar o XAML Designer**

    O Designer XAML está habilitado por padrão, mas só consome recursos se um arquivo *.xaml* é aberto. Se você trabalha com arquivos XAML, mas não quer usar a funcionalidade do designer, desabilite esse recurso para liberar memória.

    Para desabilitar o **Designer XAML**, acesse **Ferramentas** > **Opções** > **Designer XAML** > **Habilitar o Designer XAML** e desmarque a opção.

- **Remover as cargas de trabalho**

    Você pode usar o Instalador do Visual Studio para remover as cargas de trabalho que não são mais usadas. Esta ação pode simplificar o custo de inicialização e do tempo de execução ignorando pacotes e assemblies que não são mais necessários.

## <a name="force-a-garbage-collection"></a>Forçar uma coleta de lixo

O CLR usa um sistema de gerenciamento de memória de coleta de lixo. Nesse sistema, às vezes a memória é usada pelos objetos que não são mais necessários. Esse estado é temporário. O coletor de lixo liberará esta memória com base em seu desempenho e a heurística de uso de recursos. Você pode forçar o CLR a coletar a memória não utilizada usando uma tecla de atalho no Visual Studio. Se houver uma quantidade significativa de lixo aguardando a coleta e você forçar uma coleta de lixo, você deverá ver o uso de memória do processo *devenv.exe* ser deixado no **Gerenciador de Tarefas**. Raramente é necessário usar esse método. No entanto, após uma operação cara (como um build completo, sessão de depuração ou um evento de abertura de solução), ele pode ajudar a determinar a quantidade de memória que realmente está sendo usado pelo processo. Como o Visual Studio é misto (gerenciado e nativo), geralmente é possível que o alocador nativo e o coletor de lixo disputem pelos recursos de memória limitada. Em condições de alto uso de memória, pode ser útil forçar o coletor de lixo a ser executado.

Para forçar uma coleta de lixo, use a tecla de acesso: **Ctrl**+**Alt**+**Shift**+**F12**, **Ctrl**+**Alt**+**Shift**+**F12** (pressione-a duas vezes).

Se forçar a coleta de lixo de forma confiável faz seu cenário funcionar, relate isso na ferramenta de comentários do Visual Studio, pois esse comportamento provavelmente trata-se de um bug.

Para ver uma descrição detalhada do coletor de lixo CLR, consulte [Noções básicas da coleta de lixo](/dotnet/standard/garbage-collection/fundamentals).

## <a name="see-also"></a>Consulte também

- [Otimizar o desempenho do Visual Studio](../ide/optimize-visual-studio-performance.md)
- [Load solutions faster (Carregar soluções mais rapidamente) (blog do Visual Studio)](https://blogs.msdn.microsoft.com/visualstudio/2018/04/04/load-solutions-faster-with-visual-studio-2017-version-15-6/)
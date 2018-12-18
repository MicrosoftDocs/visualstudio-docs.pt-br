---
title: Depurando código em Python
description: Um passo a passo dos recursos de depuração no Visual Studio, especificamente para código Python, incluindo pontos de interrupção, passo a passo, inspeção dos valores, observação de exceções e depuração na janela interativa.
ms.date: 10/10/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 52869de661d9818252b68271c089f6b04a0b9f00
ms.sourcegitcommit: 40b6438b5acd7e59337a382c39ec711b9e99cc8a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49101154"
---
# <a name="debug-your-python-code"></a>Depurar o código do Python

O Visual Studio fornece uma experiência de depuração abrangente para o Python, incluindo a anexação a processos em execução, avaliação de expressões nas janelas **Inspeção** e **Imediata**, inspeção de variáveis locais, pontos de interrupção, instruções intervir/depuração parcial/depuração circular, comando **Definir Próxima Instrução** e muito mais.

Veja também os seguintes artigos sobre depuração específicos ao cenário:

- [Depuração remota do Linux](debugging-python-code-on-remote-linux-machines.md)
- [Depuração de modo misto do Python/C++](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)
- [Símbolos para a depuração do modo misto](debugging-symbols-for-mixed-mode-c-cpp-python.md)

|   |   |
|---|---|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo (Microsoft Virtual Academy)](https://mva.microsoft.com/en-US/training-courses-embed/python-tools-for-visual-studio-2017-18121/Video-Debugging-Python-Ep5dp5LWE_3805918567) para uma demonstração da depuração do Python (3min32s).|

<a name="debugging-without-a-project"></a>

> [!Tip]
> O Python no Visual Studio dá suporte à depuração sem um projeto. Com um arquivo independente do Python aberto, clique com o botão direito do mouse no editor, selecione **Iniciar com Depuração** e o Visual Studio iniciará o script com o ambiente global padrão (confira [Ambientes do Python](managing-python-environments-in-visual-studio.md)) sem nenhum argumento. Mas daí em diante, você tem suporte completo à depuração.
>
> Para controlar o ambiente e os argumentos, crie um projeto para o código, o que é feito facilmente com o modelo de projeto [Do código Python Existente](managing-python-projects-in-visual-studio.md#create-a-project-from-existing-files).

<a name="debugging-with-a-project"></a>

## <a name="basic-debugging"></a>Depuração básica

O fluxo de trabalho básico de depuração envolve a definição de pontos de interrupção, a execução do código em etapas, a inspeção de valores e o tratamento de exceções, conforme descrito nas próximas seções.

Uma sessão de depuração é iniciada com o comando **Depurar** > **Iniciar Depuração**, o botão **Iniciar** na barra de ferramentas ou a tecla **F5**. Essas ações abrirão o arquivo de inicialização do projeto (mostrado em negrito no **Gerenciador de Soluções**) com o ambiente ativo do projeto e os argumentos de linha de comando ou os caminhos de pesquisa especificados em **Propriedades do Projeto** (confira [Opções de depuração de projeto](#project-debugging-options)). O **Visual Studio 2017 versão 15.6** e posterior alerta se você não tiver um arquivo de inicialização definido; as versões anteriores podem abrir uma janela de saída com o interpretador do Python em execução ou a janela de saída brevemente aparece e desaparece. De qualquer forma, clique com o botão direito do mouse no arquivo apropriado e selecione **Definir como Arquivo de Inicialização**.

> [!Note]
> O depurador sempre é iniciado com o ambiente ativo do Python para o projeto. Para alterar o ambiente, torne outro ambiente ativo, conforme descrito em [Selecionar um ambiente do Python para um projeto](selecting-a-python-environment-for-a-project.md).

### <a name="breakpoints"></a>Pontos de interrupção

Os pontos de interrupção interrompem a execução de código em um ponto marcado, para que você possa inspecionar o estado do programa. Defina pontos de interrupção clicando na margem esquerda do editor de códigos ou clicando com o botão direito do mouse em uma linha de código e selecionando **Ponto de Interrupção** > **Inserir Ponto de Interrupção**. Um ponto vermelho é exibido em cada linha com um ponto de interrupção.

![Pontos de interrupção no Visual Studio](media/debugging-breakpoints.png)

Se você clicar no ponto vermelho ou clicar com o botão direito do mouse na linha de código e selecionar **Ponto de Interrupção** > **Excluir Ponto de Interrupção**, o ponto de interrupção será removido. Desabilite-o também sem removê-lo usando o comando **Ponto de Interrupção** > **Desabilitar Ponto de Interrupção**.

> [!Note]
> Alguns pontos de interrupção no Python podem ser surpreendentes para desenvolvedores que trabalharam com outras linguagens de programação. No Python, todo o arquivo é um código executável, para que o Python execute o arquivo quando ele é carregado para processar as definições de classe ou de função de nível superior. Se um ponto de interrupção tiver sido definido, você poderá descobrir que o depurador está interrompendo uma declaração de classe parcialmente. Esse comportamento é correto, mesmo que às vezes seja surpreendente.

É possível personalizar as condições nas quais um ponto de interrupção é disparado, como a interrupção somente quando uma variável é configurada para um determinado valor ou intervalo de valores. Para definir condições, clique com o botão direito do mouse no ponto vermelho do ponto de interrupção, selecione **Condição** e, em seguida, crie expressões usando o código do Python. Para obter detalhes completos sobre esse recurso no Visual Studio, confira [Condições de ponto de interrupção](../debugger/using-breakpoints.md#breakpoint-conditions).

Ao configurar condições, também é possível definir **Ação** e criar uma mensagem a ser registrada na janela de saída, opcionalmente, continuando a execução automaticamente. Registrar uma mensagem cria o que é chamado de *tracepoint* sem adicionar código de log ao aplicativo diretamente:

![Criando um tracepoint com um ponto de interrupção](media/debugging-tracepoint.png)

### <a name="step-through-code"></a>Percorrer o código

Depois de interromper em um ponto de interrupção, você tem várias maneiras para executar o código em etapas ou executar blocos de código antes de interromper novamente. Esses comandos estão disponíveis em vários locais, incluindo a barra de ferramentas de depuração na parte superior, o menu **Depuração**, o menu de contexto acionado ao clicar com o botão direito do mouse no editor de códigos e por meio de atalhos de teclado (embora nem todos os comandos estejam em todos os locais):

| Recurso | Pressionamento de tecla | Descrição |
| --- | --- | --- |
| **Continue** | **F5** | Executa o código até chegar ao próximo ponto de interrupção. |
| **Intervir** | **F11** | Executa a próxima instrução e para. Se a próxima instrução for uma chamada a uma função, o depurador parará na primeira linha da função que está sendo chamada. |
| **Depuração Parcial** | **F10** | Executa a próxima instrução, incluindo fazer uma chamada a uma função (executando todo o código) e aplicar qualquer valor retornado. A depuração parcial permite ignorar facilmente as funções que não precisam ser depuradas. |
| **Depuração Circular** | **Shift**+**F11** | Executa o código até o final da função atual e, em seguida, executa em etapas até a instrução de chamada.  Esse comando é útil quando não é necessário depurar o restante da função atual. |
| **Executar até o cursor** | **Ctrl**+**F10** | Executa o código até a localização do cursor no editor. Esse comando permite ignorar facilmente um segmento de código que não precisa ser depurado. |
| **Definir Próxima Instrução** | **Ctrl**+**Shift**+**F10** | Altera o ponto de execução atual no código para a localização atual do cursor. Esse comando permite omitir a execução de um segmento de código, como nos casos em que você sabe que o código tem uma falha ou produz um efeito colateral indesejado. |
| **Mostrar Próxima Instrução** | **Alt**+**Num** **&#42;**| Retorna à próxima instrução a ser executada. Esse comando é muito útil se você está procurando em várias partes do código e não se lembra em qual parte o depurador foi interrompido. |

### <a name="inspect-and-modify-values"></a>Inspecionar e modificar valores

Quando estiver parado no depurador, é possível inspecionar e modificar os valores das variáveis. Use também a janela **Inspeção** para monitorar variáveis individuais, bem como expressões personalizadas. (Confira [Inspecionar variáveis](../debugger/getting-started-with-the-debugger.md#inspect-variables-with-the-autos-and-locals-windows) para obter detalhes gerais.)

Para exibir um valor usando **DataTips**, basta passar o mouse sobre qualquer variável no editor. É possível clicar no valor para alterá-lo:

![DataTips no depurador](media/debugging-quick-tips.png)

A janela **Automáticos** (**Depurar** > **Janelas** > **Automáticos**) contém variáveis e expressões que estão próximas à instrução atual. Clique duas vezes na coluna de valor ou selecione e pressione **F2** para editar o valor:

![Janela Automáticos no depurador](media/debugging-autos-window.png)

A janela **Locais** (**Depurar** > **Janelas** > **Locais**) exibe todas as variáveis que estão no escopo atual, que podem ser editadas novamente:

![Janela Locais no depurador](media/debugging-locals-window.png)

Para obter mais informações sobre como usar **Automáticos** e **Locais**, confira [Inspecionar variáveis nas janelas Automáticos e Locais](../debugger/autos-and-locals-windows.md).

A janela **Inspeção** (**Depurar** > **Janelas** > **Inspeção** > **Inspecionar 1-4**) permite inserir expressões arbitrárias do Python e exibir os resultados. As expressões são reavaliadas para cada etapa:

![Janela Inspeção no depurador](media/debugging-watch-window.png)

Para obter mais informações sobre como usar a janela **Inspeção**, confira [Definir uma inspeção em variáveis usando as janelas Inspeção e QuickWatch](../debugger/watch-and-quickwatch-windows.md).

Ao inspecionar um valor de cadeia de caracteres (`str`, `unicode`, `bytes` e `bytearray` são considerados cadeias de caracteres para essa finalidade), um ícone de lupa é exibido no lado direito do valor. Se você clicar no ícone, o valor de cadeia de caracteres sem aspas será exibido em uma caixa de diálogo pop-up, com encapsulamento e rolagem, o que é útil para cadeias de caracteres longas. Além disso, selecionar a seta suspensa no ícone permite que você selecione visualizações de texto sem formatação, HTML, XML e JSON:

![Visualizadores de cadeia de caracteres](media/debugging-string-visualizers.png)

As visualizações de HTML, XML e JSON são exibidas em janelas pop-up separadas com modos de exibição de árvore e realce de sintaxe.

### <a name="exceptions"></a>Exceções

Se ocorrer um erro no programa durante a depuração, mas você não tiver um manipulador de exceção para ele, o depurador interromperá no ponto da exceção:

![Pop-up de exceção](media/debugging-exception-popup.png)

Neste ponto, é possível inspecionar o estado do programa, incluindo a pilha de chamadas. No entanto, se você tentar executar o código em etapas, a exceção continuará sendo gerada até que ela seja tratada ou o programa seja encerrado.

O comando de menu **Depurar** > **Janelas** > **Configurações de Exceção** abre uma janela na qual é possível expandir **Exceções do Python**:

![Janela Exceções](media/debugging-exception-settings.png)

A caixa de seleção de cada exceção controla se o depurador *sempre* interrompe quando é acionado. Marque essa caixa quando desejar interromper com mais frequência para uma exceção específica.

Por padrão, a maioria das exceções interromperá quando um manipulador de exceção não puder ser encontrado no código-fonte. Para alterar esse comportamento, clique com o botão direito do mouse em qualquer exceção e modifique a opção **Continuar Quando Não For Tratada no Código do Usuário**. Desmarque essa caixa quando desejar interromper com menos frequência para uma exceção.

Para configurar uma exceção que não aparece nessa lista, clique no botão **Adicionar** para adicioná-la. O nome deve corresponder ao nome completo da exceção.

## <a name="project-debugging-options"></a>Opções de depuração de projeto

Por padrão, o depurador inicia o programa com o inicializador padrão do Python, sem argumentos de linha de comando e sem nenhum outro caminho ou condição especial. As opções de inicialização são alteradas por meio das propriedades de depuração do projeto, acessadas no **Gerenciador de Soluções** clicando com o botão direito do mouse no projeto selecionando **Propriedades** e a guia **Depuração**.

![Propriedades de depuração de projeto](media/debugging-project-properties.png)

### <a name="launch-mode-options"></a>Opções de modo de inicialização

| Opção | Descrição |
| --- | --- |
| **Inicializador padrão do Python** | Usa o código de depuração escrito no Python portátil que é compatível com o CPython, IronPython e variantes como o Stackless Python. Fornece a melhor experiência de depuração de código puro do Python. Quando você o anexa a um processo *python.exe* em execução, esse inicializador é usado. Esse iniciador também fornece a [depuração de modo misto](debugging-mixed-mode-c-cpp-python-in-visual-studio.md) para o CPython, permitindo a execução em etapas direta entre o código do C/C++ e o código do Python. |
| **Inicializador da Web** | Inicia o navegador padrão na inicialização e habilita a depuração de modelos. Consulte a seção [Depuração de modelos da Web](python-web-application-project-templates.md#debugging) para obter mais informações. |
| **Inicializador da Web do Django** | Idêntico ao inicializador da Web e mostrado apenas para compatibilidade com versões anteriores. |
| **Inicializador do IronPython (.NET)** | Usa o depurador do .NET, que funciona somente com o IronPython, mas que permite a execução em etapas entre qualquer projeto de linguagem .NET, incluindo C# e VB. Esse inicializador é usado se você se anexa a um processo em execução do .NET que hospeda o IronPython. |

### <a name="run-options-search-paths-startup-arguments-and-environment-variables"></a>Opções de execução (caminhos de pesquisa, argumentos de inicialização e variáveis de ambiente)

| Opção | Descrição |
| --- | --- |
| **Caminhos de Pesquisa** | Esses valores correspondem ao que é mostrado no nó **Caminhos de Pesquisa** do projeto no **Gerenciador de Soluções**. É possível modificar esse valor aqui, mas é mais fácil usar o **Gerenciador de Soluções**, que permite procurar pastas e converter os caminhos automaticamente no formato relativo. |
| **Argumentos de Script** | Esses argumentos são adicionados ao comando usado para iniciar o script, aparecendo após o nome de arquivo do script. O primeiro item aqui está disponível para o script como `sys.argv[1]`, o segundo como `sys.argv[2]` e assim por diante. |
| **Argumentos do Interpretador** | Esses argumentos são adicionados à linha de comando do inicializador antes do nome do script. Os argumentos comuns aqui são `-W ...` para controlar avisos, `-O` para otimizar o programa ligeiramente e `-u` para usar o E/S não armazenado em buffer. Provavelmente, os usuários do IronPython usarão esse campo para passar opções `-X`, como `-X:Frames` ou `-X:MTA`. |
| **Caminho do Interpretador** | Substitui o caminho associado ao ambiente atual. O valor pode ser útil para iniciar o script com um interpretador não padrão. |
| **Variáveis de ambiente** | Nessa caixa de texto multilinha, adicione entradas com o formato \<NAME>=\<VALUE>. Como essa configuração é aplicada por último, com base nas variáveis de ambiente globais existentes e depois que `PYTHONPATH` é definido de acordo com a configuração de **Caminhos de Pesquisa**, ela pode ser usada para substituir qualquer um dos outros valores manualmente. |

## <a name="immediate-and-interactive-windows"></a>Janelas imediatas e interativas

Há duas janelas interativas que podem ser usadas durante uma sessão de depuração: a janela **Imediata** padrão do Visual Studio e a janela **Interativa de Depuração do Python**.

A janela **Imediata** (**Depurar** > **Janelas** > **Imediata**) é usada para avaliação rápida de expressões do Python e para inspeção ou atribuição de variáveis no programa em execução. Confira o artigo geral [Janela Imediata](../ide/reference/immediate-window.md) para obter detalhes.

A janela **Interativa de Depuração do Python** (**Depurar** > **Janelas** > **Interativa de Depuração do Python**) é mais avançada, pois disponibiliza toda a experiência de [REPL Interativo](python-interactive-repl-in-visual-studio.md) durante a depuração, incluindo a escrita e a execução de código. Ela se conecta automaticamente a qualquer processo iniciado no depurador usando o inicializador Padrão do Python (incluindo os processos anexados por meio de **Depurar** > **Anexar ao Processo**). No entanto, ela não está disponível ao usar a depuração de modo misto do C/C++.

![Janela Interativa de Depuração do Python](media/debugging-interactive.png)

A janela **Interativa de Depuração** dá suporte a metacomandos especiais, além dos [comandos REPL padrão](python-interactive-repl-in-visual-studio.md#meta-commands):

| Comando | Arguments | Descrição |
| --- | --- | --- |
| `$continue`, `$cont`, `$c` | Inicia a execução do programa da instrução atual. |
| `$down`, `$d` | Move o quadro atual um nível para baixo no rastreamento de pilha. |
| `$frame` | | Exibe a ID de quadro atual.
| `$frame` | ID de quadro | Muda a ID de quadro atual para a ID de quadro especificada.
| `$load` | Carrega comandos do arquivo e os executa até a conclusão |
| `$proc` |  | Exibe a ID de processo atual. |
| `$proc` | ID de processo | Muda a ID de processo atual para a ID de processo especificada. |
| `$procs` | | Lista os processos que estão sendo depurados no momento. |
| `$stepin`, `$step`, `$s` | Intervém na próxima chamada de função, se possível. |
| `$stepout`, `$return`, `$r` | Encaminha-se para fora da função atual. |
| `$stepover`, `$until`, `$unt` | Depura parcialmente a próxima chamada de função. |
| `$thread` | | Exibe a ID de thread atual. |
| `$thread` | ID de thread | Muda a ID de thread atual para a ID de thread especificada. |
| `$threads` | | Lista os threads que estão sendo depurados no momento. |
| `$up`, `$u` | | Move o quadro atual um nível para cima no rastreamento de pilha. |
| `$where`, `$w`, `$bt` | Lista os quadros do thread atual. |

Observe que as janelas padrão do depurador, como **Processos**, **Threads** e **Pilha de Chamadas**, não são sincronizadas com a janela **Interativa de Depuração**. A alteração do processo ativo, do thread ou do quadro na janela **Interativa de Depuração** não afeta as outras janelas do depurador. Da mesma forma, a alteração do processo, do thread ou do quadro ativo nas outras janelas do depurador não afeta a janela **Interativa de Depuração**.

A janela **Interativa de Depuração** tem seu próprio conjunto de opções, que pode ser acessado por meio de **Ferramentas** > **Opções** > **Ferramentas Python** > **Janela Interativa de Depuração**. Ao contrário da janela **Interativa do Python** normal, que tem uma instância separada para cada ambiente do Python, há apenas uma janela **Interativa de Depuração** e ela sempre usa o interpretador do Python do processo que está sendo depurado. Consulte [Opções – Opções de depuração](python-support-options-and-settings-in-visual-studio.md#debugging-options).

![Opções da Janela Interativa de Depuração](media/debugging-interactive-options.png)

<a name="use-the-experimental-debugger"></a>

## <a name="use-the-legacy-debugger"></a>Usar o depurador herdado

O Visual Studio 2017 versões 15.8 e posteriores usam um depurador com base no ptvsd versão 4.1 ou superior. Esta versão do ptvsd é compatível com o Python 2.7 e o Python 3.5 ou superior. Se você estiver usando o Python 2.6, 3.1 a 3.4 ou o IronPython, o Visual Studio mostrará o erro **O depurador não dá suporte a este ambiente do Python**:

![Erro: o depurador não dá suporte a esse ambiente do Python, quando o depurador é usado](media/debugging-experimental-incompatible-error.png)

Nesses casos, você precisa usar o depurador mais antigo (o que é o padrão no Visual Studio 2017 versões 15.7 e anteriores). Selecione o comando de menu **Ferramentas** > **Opções**, navegue até **Python** > **Depuração** e selecione a opção **Usar depurador herdado**.

Se você tiver instalado uma versão mais antiga do ptvsd no ambiente atual (como uma versão 4.0.x anterior ou uma versão 3.x necessária para a depuração remota), o Visual Studio poderá mostrar um erro ou aviso.

O erro **Não foi possível carregar o pacote do depurador** será exibido se você tiver instalado o ptvsd 3.x:

![Erro: o pacote do depurador não pôde ser carregado, quando o depurador é usado](media/debugging-experimental-version-error.png)

Nesse caso, selecione **Usar o depurador herdado** para definir a opção **Usar depurador herdado** e reinicie o depurador.

O aviso **O pacote do depurador está desatualizado** será exibido se você tiver instalado uma versão 4.x anterior do ptvsd:

![Aviso: o pacote do depurador está desatualizado, quando o depurador é usado](media/debugging-experimental-version-warning.png)

> [!Important]
> Embora você possa optar por ignorar o aviso em algumas versões do ptvsd, o Visual Studio poderá não funcionar corretamente.

Para gerenciar a instalação do ptvsd:

1. Navegue até a guia **Pacotes** na janela **Ambientes do Python**.

1. Insira "ptvsd" na caixa de pesquisa e examine a versão do ptvsd instalada:

    ![Verificando a versão do ptvsd na janela Ambientes do Python](media/debugging-experimental-check-ptvsd.png)

1. Se a versão for inferior à 4.1.1a9 (a versão empacotada com o Visual Studio), selecione o **X** à direita do pacote para desinstalar a versão mais antiga. Assim, o Visual Studio passará a usar a versão empacotada. (Você também pode desinstalar com o PowerShell usando `pip uninstall ptvsd`.)

1. Como alternativa, você pode atualizar o pacote ptvsd para a última versão seguindo as instruções da seção [Solução de problemas](#troubleshooting).

## <a name="troubleshooting"></a>Solução de problemas

Se você tiver problemas com o depurador, primeiro atualize a versão do ptvsd da seguinte maneira:

1. Navegue até a guia **Pacotes** na janela **Ambientes do Python**.

1. Insira `ptvsd --upgrade` na caixa de pesquisa, em seguida, selecione **Executar o comando: pip install ptvsd --upgrade**. (Você também pode usar o mesmo comando no PowerShell).

    ![Como fornecer o comando ptvsd upgrade na janela Ambientes do Python](media/debugging-experimental-upgrade-ptvsd.png)

Se o problema persistir, registre um problema no [Repositório GitHub do PTVS](https://github.com/Microsoft/ptvs/issues).

### <a name="enable-debugger-logging"></a>Habilitar registro em log do depurador

Ao investigar um problema do depurador, a Microsoft pode solicitar que você habilite e colete logs de depurador para ajudar no diagnóstico.

As seguintes etapas habilitam a depuração na sessão atual do Visual Studio:

1. Abra uma janela de comando no Visual Studio usando o comando de menu **Exibir** > **Outras Janelas** > **Janela de Comando**.

1. Insira o seguinte comando:

    ```ps
    DebugAdapterHost.Logging /On
    ```

1. Inicie a depuração e percorra todas as etapas são necessárias para reproduzir o problema. Durante esse tempo, os logs de depuração aparecem na janela **Saída** em **Log de Host do Adaptador de Depuração**. Em seguida, você poderá copiar os logs dessa janela e colá-los em um problema do GitHub, em um email etc.

    ![Saída de log do depurador na janela Saída](media/debugger-logging-output.png)

1. Se o Visual Studio parar de funcionar ou se não for possível acessar a janela **Saída**, reinicie o Visual Studio, abra uma janela de comando e digite o seguinte comando:

    ```ps
    DebugAdapterHost.Logging /On /OutputWindow
    ```

1. Inicie a depuração e reproduza o problema novamente. Os logs de depurador podem ser encontrados em `%temp%\DebugAdapterHostLog.txt`.

## <a name="see-also"></a>Consulte também

Para obter detalhes completos sobre o depurador do Visual Studio, consulte [Depuração no Visual Studio](../debugger/debugger-feature-tour.md).

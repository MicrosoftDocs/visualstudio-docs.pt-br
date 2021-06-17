---
title: Janela interativa do Python (REPL)
description: Use a janela interativa (REPL) para desenvolvimento rápido de código Python no Visual Studio.
ms.date: 02/11/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 21115673a41e26b2f1685442d2ed0ad93a147990
ms.sourcegitcommit: 4908561809ad397c99cf204f52d5e779512e502c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112254882"
---
# <a name="work-with-the-python-interactive-window"></a>Trabalhar com a janela Interativa do Python

O Visual Studio fornece uma janela interativa REPL (leitura-avaliação-impressão-loop) para cada um dos ambientes do Python, que é uma melhoria do REPL obtido com *python.exe* na linha de comando. A janela **Interativa** (aberta com os comandos de menu **Exibir** > **Outras Janelas Interativas** > **&lt;do ambiente&gt;**) permite que você insira o código Python arbitrário e veja resultados imediatos. Esse modo de codificação ajuda a você aprender e experimentar com APIs e bibliotecas e a desenvolver de forma interativa o código funcional para incluir em seus projetos.

![Janela interativa do Python](media/interactive-window.png)

O Visual Studio tem diversos modos REPL do Python à sua disposição:

| REPL | Descrição | Edição | Depuração | Imagens |
| --- | --- | --- | --- | --- |
| Standard | REPL padrão, que se comunica com o Python diretamente | Edição padrão (várias linhas etc.). | Sim, por meio de `$attach` | Não |
| Depurar | REPL padrão, que se comunica com o processo depurado do Python | Edição padrão | Somente depuração | Não |
| IPython | O REPL se comunica com o back-end do IPython | Comandos do IPython, funcionalidades do Pylab | Não | Sim, embutido no REPL |
| IPython sem Pylab | O REPL se comunica com o back-end do IPython | IPython padrão | Não | Sim, em uma janela separada |

Este artigo descreve os modos REPL **Padrão** e **Depuração**. Para obter detalhes sobre os modos do IPython, confira [Usar o REPL do IPython](interactive-repl-ipython.md).

Para ver um passo a passo detalhado com exemplos, incluindo as interações com o editor, como **Ctrl** Enter, consulte Etapa 3 do Tutorial: Usar a +  [janela REPL Interativa](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md).

## <a name="open-an-interactive-window"></a>Abrir uma janela Interativa

Há várias maneiras de abrir a janela **Interativa** de um ambiente.

Primeiro, alternar para a janela Ambientes do Python **(** Exibir Outros Ambientes python do Windows ou  >    >   **Ctrl** + **K**  >  **Ctrl**) + **`**  e selecione o comando ou botão Abrir Janela Interativa para um ambiente escolhido.

![Link Janela Interativa na janela Ambientes do Python](media/interactive-window-opening.png)

Em segundo lugar, próximo à parte inferior do menu Exibir Outras Janelas, há um comando janela interativa do Python para seu ambiente padrão, bem como um comando para alternar para  >   a **janela Ambientes:** 

![Itens de menu da Janela Interativa em Exibir > Outras Janelas](media/interactive-window-menu.png)

Em terceiro lugar,  você pode abrir uma janela Interativa no arquivo de inicialização em seu projeto ou para um arquivo autônomo, selecionando o comando de menu **Depurar** Executar no  >  **\<Project | File> Python Interativo** (**Shift** + **Alt** + **F5**):

![Executar Projeto no menu Python Interativo](media/interactive-execute-project.png)

Por fim, é possível marcar o código no arquivo e usar o [comando **Enviar código para Interativa**](#send-to-interactive-command) descrito abaixo.

## <a name="interactive-window-options"></a>Opções da janela interativa

Você pode controlar vários aspectos da janela **Interativa** por meio de **Ferramentas** > **Opções** > **Python** > **Janelas Interativas** (confira [Opções](python-support-options-and-settings-in-visual-studio.md)):

![Opções da janela interativa do Python](media/options-interactive-windows.png)

## <a name="use-the-interactive-window"></a>Usar a Janela Interativa

Depois que **a janela** Interativa for aberta, você poderá começar a inserir o código linha por linha no **\>\>\>** prompt. A **janela** Interativa executa cada linha conforme você a insinte, o que inclui a importação de módulos, a definição de variáveis e assim por diante:

![Janela interativa do Python](media/interactive-window.png)

A exceção é quando as linhas de código adicionais são necessárias para fazer uma instrução completa, como quando uma instrução `for` termina em dois pontos como mostrado acima. Nesses casos, o prompt de linha muda para **...**, indicando que é necessário inserir linhas adicionais no bloco, conforme mostrado na quarta e quinta linhas do gráfico acima. Ao pressionar **Enter** em uma linha em branco, a janela **Interativa** fecha o bloco e o executa no interpretador.

> [!Tip]
> A **janela** Interativa melhora a experiência comum de REPL de linha de comando do Python recuando automaticamente instruções que pertencem a um escopo ao redor. Seu histórico (recuperado com a seta para cima) também fornece itens de várias linhas, enquanto o REPL de linha de comando fornece somente linhas individuais.

<a name="meta-commands"></a> A janela **Interativa** também dá suporte a vários metacomandos. Todos os metacomandos começam com `$` e é possível digitar `$help` para obter uma lista dos metacomandos e `$help <command>` para obter detalhes de uso de um comando específico.

:::moniker range="<=vs-2017"

| Metacomando | Descrição |
| --- | --- |
| `$$` | Insere um comentário, que é útil para comentar o código ao longo da sessão. |
| `$attach` | Anexa o depurador do Visual Studio ao processo da janela REPL para habilitar a depuração. |
| `$cls`, `$clear` | Limpa o conteúdo da janela do editor, deixando intactos o histórico e o contexto de execução. |
| `$help` | Exibe uma lista de comandos ou a ajuda sobre um comando específico. |
| `$load` | Carrega comandos do arquivo e os executa até a conclusão. |
| `$mod` | Muda o escopo atual para o nome de módulo especificado. |
| `$reset` | Redefine o ambiente de execução com o estado inicial, mas mantém o histórico. |
| `$wait` | Aguarda, pelo menos, o número especificado de milissegundos. |

:::moniker-end

:::moniker range=">=vs-2019"

| Metacomando | Descrição |
| --- | --- |
| `$$` | Insere um comentário, que é útil para comentar o código ao longo da sessão. |
| `$cls`, `$clear` | Limpa o conteúdo da janela do editor, deixando intactos o histórico e o contexto de execução. |
| `$help` | Exibe uma lista de comandos ou a ajuda sobre um comando específico. |
| `$load` | Carrega comandos do arquivo e os executa até a conclusão. |
| `$mod` | Muda o escopo atual para o nome de módulo especificado. |
| `$reset` | Redefine o ambiente de execução com o estado inicial, mas mantém o histórico. |
| `$wait` | Aguarda, pelo menos, o número especificado de milissegundos. |

:::moniker-end

Os comandos também são extensíveis pelas extensões do Visual Studio implementando e exportando `IInteractiveWindowCommand` ([exemplo](https://github.com/Microsoft/PTVS/blob/master/Python/Product/PythonTools/PythonTools/Repl/InteractiveWindowCommands.cs#L85)).

## <a name="switch-scopes"></a>Mudar escopos

Por padrão, a janela **Interativa** de um projeto tem como escopo o arquivo de inicialização do projeto, como se ele fosse executado no prompt de comando. Para um arquivo independente, ele tem esse arquivo como escopo. No entanto, a qualquer momento durante a sessão de REPL, o menu suspenso na parte superior da janela **Interativa** permite alterar o escopo:

![Escopos da janela interativa](media/interactive-scopes.png)

Ao importar um módulo, como digitando `import importlib`, você verá opções na lista suspensa para mudar para qualquer escopo nesse módulo. Uma mensagem na janela **Interativa** também indica o novo escopo, portanto, é possível acompanhar como você chegou a um determinado estado durante sua sessão.

A inserção de `dir()` em um escopo exibe os identificadores válidos no escopo, incluindo nomes de função, classes e variáveis. Por exemplo, o uso de `import importlib` seguido por `dir()` mostra o seguinte:

![Janela interativa no escopo de importlib](media/interactive-importlib-scope.png)

## <a name="send-to-interactive-command"></a>Comando Enviar para Interativa

Além de trabalhar  diretamente na janela Interativa, você pode selecionar o código  no editor, clicar com o botão direito do mouse e escolher Enviar para Interativo ou pressionar **Ctrl** + **Enter**.

![Comando de menu Enviar para interativa](media/interactive-send-to.png)

Esse comando é útil para o desenvolvimento de código iterativo ou evolucionário, incluindo o teste do código durante o desenvolvimento. Por exemplo, depois de enviar um trecho  de código para a janela Interativa e ver sua saída, você pode pressionar a seta para cima para mostrar o código novamente, modificá-lo e testá-lo rapidamente pressionando **Ctrl** + **Enter**. (Pressionar **Enter** no final da entrada o executa, mas pressionar **Enter** no meio da entrada insere uma nova linha.) Depois de ter o código que deseja, você pode copiá-lo facilmente de volta para o arquivo de projeto.

> [!Tip]
> Por padrão, Visual Studio remove **>>>** e **...** O REPL solicita ao colar o código da **janela** Interativa no editor. Você pode alterar esse comportamento na **guia** Ferramentas Opções Editor de Texto Python Avançado usando a  >    >    >    >   opção **Colar remove prompts REPL.** Consulte [Opções – Opções diversas.](python-support-options-and-settings-in-visual-studio.md#miscellaneous-options)

<!-- After 15.3 is released, you can also press **Undo** after pasting to restore prompts. Press **Undo** a second time to remove the pasted code entirely. -->

## <a name="work-with-code-cells"></a>Trabalhar com células de código

As células de código podem ser usadas na análise de dados e são compatíveis com diversos editores de texto.

Por exemplo, ao usar um arquivo de código como um bloco de rascunho, geralmente você tem um pequeno bloco de código que você deseja enviar de uma só vez. Para agrupar códigos, marque o código como uma *célula de código* adicionando um comentário começando com `#%%` ao início da célula, que termina a anterior. As células de código podem ser recolhidas e expandidas e o uso de **Ctrl** + **Enter** dentro de uma célula de código envia a célula inteira para a janela **interativa** e move para a próxima.

O Visual Studio também detecta células de código começando com comentários como `# In[1]:`, que é o formato que você obtém ao exportar um bloco de anotações do Jupyter como um arquivo do Python. Essa detecção facilita a execução de um bloco de anotações do [Azure notebooks](https://notebooks.azure.com/) baixando como um arquivo Python, abrindo no Visual Studio e usando **Ctrl** + **Enter** para executar cada célula.

![Células de código interativas](media/interactive-code-cells.png)

## <a name="intellisense-behavior"></a>Comportamento do IntelliSense

A janela **Interativa** inclui o IntelliSense baseado nos objetos dinâmicos, ao contrário do editor de código, no qual o IntelliSense é baseado apenas na análise de código-fonte. Essas sugestões estão mais corretas na janela **interativa** , especialmente com código gerado dinamicamente. A desvantagem é que as funções com efeitos colaterais (como mensagens de log) podem afetar sua experiência de desenvolvimento.

Se esse comportamento for um problema, altere as configurações em **ferramentas**  >  **Opções**  >  **Python**  >  **Interactive Windows** no grupo **modo de conclusão** , conforme descrito em opções [– opções interativas do Windows](python-support-options-and-settings-in-visual-studio.md#interactive-windows-options).

---
title: Etapa 3 do Tutorial do Python no Visual Studio, REPL interativo
titleSuffix: ''
description: Etapa 3 de um passo a passo básico das funcionalidades do Python no Visual Studio, abordando a janela REPL interativa do Python.
ms.date: 01/28/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: e82073b77231f84452ba51402f407904142bbf8e
ms.sourcegitcommit: 925db7adb9cb554b081c7e727d09680d4863feed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2021
ms.locfileid: "107941091"
---
# <a name="step-3-use-the-interactive-repl-window"></a>Etapa 3: usar a janela interativa REPL

**Etapa anterior: [Gravar e executar código](tutorial-working-with-python-in-visual-studio-step-02-writing-code.md)**

A janela **interativa** do Visual Studio para Python fornece uma experiência de repl (Read-Evaluate-Print-loop) rica que reduz muito o ciclo de edição de compilação e depuração usual. A janela **Interativa** fornece todos os recursos da experiência de REPL da linha de comando do Python. Ela também facilita a troca de código com arquivos de origem no editor do Visual Studio, o que seria difícil com a linha de comando.

> [!NOTE]
> Para problemas com REPL, verifique se os pacotes `ipython` e `ipykernel` estão instalados e, para obter ajuda na instalação dos pacotes, confira a [guia de pacotes de ambientes Python](./python-environments-window-tab-reference.md#packages-tab).

1. Abra a janela **Interativa** clicando com o botão direito do mouse no ambiente de projeto do Python no **Gerenciador de Soluções** (como **Python 3.6 (32 bits)**, mostrado em um gráfico anterior) e selecionando **Abrir Janela Interativa**. Como alternativa, você pode selecionar **Exibir**  >  **outras**  >  **janelas interativas do Python** do Windows no menu principal do Visual Studio.

1. A janela **Interativa** abre-se abaixo do editor com o prompt padrão de REPL do Python **>>>**. A lista suspensa **Ambiente** permite selecionar um intérprete específico com o qual trabalhar. Se você também quiser deixar a janela **Interativa** maior, arraste o separador entre as duas janelas:

    ![Janela interativa Python: arrastando para redimensionar](media/vs-getting-started-python-11-interactive1b.png)

    > [!Tip]
    > Você pode redimensionar todas as janelas no Visual Studio, arrastando os separadores de bordas. Você também pode arrastar e retirar janelas para fora do quadro do Visual Studio e reorganizá-las da forma que quiser dentro do quadro. Para obter detalhes completos, confira [Personalizar layouts de janela](../ide/customizing-window-layouts-in-visual-studio.md).

1. Insira algumas instruções, como `print("Hello, Visual Studio")`, e expressões, como `123/456`, para ver resultados imediatos:

    ![Resultados imediatos da janela interativa do Python](media/vs-getting-started-python-12-interactive2.png)

1. Quando você começa a gravar uma instrução de várias linhas, como uma definição de função, a janela **interativa** mostra o prompt do Python **...** para as linhas contínuas, que, ao contrário da repl de linha de comando, fornece recuo automático. Para adicionar uma nova linha **...** , pressione `Shift+Enter` :

    ![Janela interativa do Python com continuação de instrução](media/vs-getting-started-python-13-interactive3.png)

1. A janela **interativa** fornece um histórico completo de tudo que você inseriu e melhora o repl de linha de comando com itens de Histórico multilinha. Por exemplo, com facilidade, é possível cancelar toda a definição da função `f` como uma única unidade e alterar o nome para `make_double`, em vez de recriar a função linha por linha.

1. O Visual Studio pode enviar várias linhas de código de uma janela do editor para a janela **Interativa**. Essa capacidade permite que você mantenha o código em um arquivo de origem e envie facilmente partes específicas dele para a janela **Interativa**. Assim, você poderá trabalhar com esses fragmentos de código no ambiente REPL rápido em vez de ter que executar o programa inteiro. Para ver esse recurso, primeiro substitua o loop `for` no arquivo *PythonApplication1.py* pelo seguinte:

    ```python
    # Create a string with spaces proportional to a cosine of x in degrees
    def make_dot_string(x):
        return ' ' * int(20 * cos(radians(x)) + 20) + 'o'
    ```

1. Selecione as `import` `from` instruções de função, e `make_dot_string` no arquivo *. py* . Clique com o botão direito do mouse no texto selecionado e escolha **Enviar para interativo** (ou pressione **Ctrl** + **Enter**). O fragmento de código será imediatamente colado na janela **Interativa** e executado. Como o código definiu uma função, você pode testar rapidamente essa função chamando-a algumas vezes:

    ![Enviando o código para a janela interativa e testando-o](media/vs-getting-started-python-14-interactive4.png)

    > [!Tip]
    > Usar **Ctrl** + **Enter** no editor *sem* uma seleção executa a linha atual do código na janela **interativa** e coloca automaticamente o cursor na linha seguinte. Com esse recurso, pressionar **Ctrl** + **Enter** repetidamente fornece uma maneira conveniente de percorrer o código que não é possível apenas com a linha de comando do Python. Isso também permitirá que você percorra o código sem executar o depurador e sem, necessariamente, começar desde o início do programa.

1. Você também pode copiar e colar várias linhas de código de qualquer fonte na janela **Interativa**, como no snippet a seguir, o que é difícil fazer com o REPL da linha de comando do Python. Ao colar, a janela **Interativa** executa o código como se você o tivesse digitado:

    ```python
    for i in range(360):
        s = make_dot_string(i)
        print(s)
    ```

    ![Colando várias linhas de código usando o comando Enviar para Interativa](media/vs-getting-started-python-15-interactive5.png)

1. Como você pode ver, esse código funciona bem, mas a saída não é muito interessante. Um valor de etapa diferente no loop `for` mostraria mais da curva do cosseno. Felizmente, como todo o loop `for` está no histórico do REPL como uma única unidade, é fácil voltar e fazer as alterações desejadas e, em seguida, testar a função novamente. Pressione a seta para cima para, primeiro, recuperar o loop `for`. Em seguida, pressione as setas à esquerda ou direita para iniciar a navegação no código (até que você faça isso, as setas para baixo e para cima continuam a percorrer o histórico). Navegue até a especificação `range` e altere-a para `range(0, 360, 12)`. Em seguida, pressione **Ctrl** + **Enter** (em qualquer lugar no código) para executar a instrução inteira novamente:

    ![Edição de uma declaração anterior na janela interativa](media/vs-getting-started-python-16-interactive6.png)

1. Repita o processo para fazer experiências com configurações de etapas diferentes, até encontrar um valor que você mais goste. Você também pode fazer a curva se repetir, aumentando o intervalo, por exemplo, `range(0, 1800, 12)`.

1. Quando estiver satisfeito com o código que você escreveu na janela **interativa** , selecione-o. Em seguida, clique com o botão direito do mouse no código e escolha **copiar código** (**Ctrl** + **Shift** + **C**). Por fim, Cole o código selecionado no editor. Observe como esse recurso especial do Visual Studio omite automaticamente qualquer saída, bem como os prompts `>>>` e `...`. Por exemplo, a imagem abaixo mostra o uso do comando **Copiar Código** em uma seleção que inclui os prompts e a saída:

    ![Comando copiar código da janela interativa em uma seleção com prompts e saída](media/vs-getting-started-python-17-interactive7.png)

    Ao colar no editor, você obtém somente o código:

    ```python
    for i in range(0, 1800, 12):
        s = make_dot_string(i)
        print(s)
    ```

    Se quiser copiar o conteúdo exato da janela **Interativa**, incluindo os prompts e a saída, basta usar o comando **Copiar** padrão.

1. O que você acabou de fazer é usar o ambiente de REPL rápido da janela **Interativa** para trabalhar em detalhes de uma pequena parte de código e adicionou convenientemente esse código ao arquivo de origem do seu projeto. Ao executar o código novamente com **Ctrl** + **F5** (ou **depurar**  >  **Iniciar sem depuração**), você verá os resultados exatos desejados.

## <a name="next-step"></a>Próxima etapa

> [!div class="nextstepaction"]
> [Executar o código no depurador](tutorial-working-with-python-in-visual-studio-step-04-debugging.md)

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Usar a Janela Interativa](python-interactive-repl-in-visual-studio.md)
- [Usar o IPython REPL](interactive-repl-ipython.md)
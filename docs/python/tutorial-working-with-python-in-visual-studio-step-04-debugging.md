---
title: Etapa 4 do Tutorial do Python no Visual Studio, depuração
titleSuffix: ''
description: Etapa 4 de um passo a passo básico das funcionalidades do Python no Visual Studio, abordando como executar o código Python no depurador.
ms.date: 01/28/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 13080f69de9a8bfc6b1da35a7126f1f0c89a64c7
ms.sourcegitcommit: 4908561809ad397c99cf204f52d5e779512e502c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112254856"
---
# <a name="step-4-run-code-in-the-debugger"></a>Etapa 4: Executar o código no depurador

**Etapa anterior: [usar a janela interativa REPL](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md)**

Além de gerenciar projetos, fornecer uma experiência de  edição rica e a janela Interativa, o Visual Studio fornece depuração completa para código Python. No depurador, você pode executar seu código passo a passo, incluindo cada iteração de um loop. Você também pode pausar o programa sempre que determinadas condições são verdadeiras. A qualquer momento em que o programa estiver em pausa no depurador, você poderá examinar todo o estado do programa e alterar o valor de variáveis. Essas ações são essenciais para a localização de bugs do programa e também fornecem recursos muito úteis para seguir com cuidado o fluxo exato do programa.

1. Substitua o código no arquivo *PythonApplication1.py* pelo seguinte. Essa variação do código expande o `make_dot_string` para que você possa examinar as etapas distintas no depurador. Ela também coloca o loop `for` em uma função `main` e executa-o explicitamente, chamando essa função:

    ```python
    from math import cos, radians

    # Create a string with spaces proportional to a cosine of x in degrees
    def make_dot_string(x):
        rad = radians(x)                             # cos works with radians
        numspaces = int(20 * cos(rad) + 20)          # scale to 0-40 spaces
        st = ' ' * numspaces + 'o'                   # place 'o' after the spaces
        return st

    def main():
        for i in range(0, 1800, 12):
            s = make_dot_string(i)
            print(s)

    main()
    ```

1. Verifique se o código funciona corretamente pressionando **F5** ou selecionando o comando de menu **Depurar** > **Iniciar Depuração**. Esse comando executa o código no depurador, mas como você não fez nada para pausar o programa enquanto ele está em execução, ele apenas imprime um padrão de onda para algumas iterações. Pressione qualquer tecla para fechar a janela de saída.

    > [!Tip]
    > Para fechar a janela de saída automaticamente quando o programa for concluído, selecione o comando de menu Opções de Ferramentas, expanda o nó  >   **Python,** selecione **Depuração** e, em seguida, desfaça a opção Aguardar entrada quando o processo for fechado **normalmente:**
    >
    > ![Opção de depuração do Python para fechar a Janela de Saída na saída normal do programa](media/vs-getting-started-python-22-debugging5.png)
    >
    > Para obter informações adicionais sobre depuração, incluindo tarefas como definir argumentos de script e interpretador, consulte [Depurar seu código Python](debugging-python-in-visual-studio.md).

1. De definir um ponto de interrupção na instrução clicando uma vez na margem cinza por essa linha ou colocando o sinal de segurança nessa linha e usando o comando `for` **Depurar**  >  **Alternar** Ponto de Interrupção (**F9**). Um ponto vermelho é exibido na margem cinza para indicar o ponto de interrupção (conforme indicado pela seta abaixo):

    ![Definindo um ponto de interrupção](media/vs-getting-started-python-18-debugging1.png)

1. Inicie o depurador novamente (**F5**) e veja se a execução do código é interrompida na linha com esse ponto de interrupção. Aqui você pode inspecionar a pilha de chamadas e examinar variáveis. As variáveis que estão no escopo aparecem na janela **Autos** quando elas estão definidas. Você também pode alternar para a exibição **Locais** na parte inferior dessa janela para mostrar todas as variáveis que o Visual Studio localiza no escopo atual (incluindo funções), antes mesmo que elas sejam definidas:

    ![Experiência de interface do usuário do ponto de interrupção para o Python](media/vs-getting-started-python-19-debugging2b.png)

1. Observe a barra de ferramentas de depuração (mostrada abaixo) na parte superior da janela do Visual Studio. Essa barra de ferramentas fornece acesso rápido aos comandos de depuração mais comuns (que também podem ser encontrados no menu **Depurar**):

    ![Botões da barra de ferramentas de depuração essenciais](media/vs-getting-started-python-20-debugging3.png)

    Os botões, da esquerda para a direita, são os seguintes:
    - **Continuar** (**F5**) executa o programa, até o próximo ponto de interrupção ou até a conclusão do programa.
    - **Interromper Tudo** (**Ctrl** + **Alt** + **Break**) pausa um programa de execução longa.
    - **Parar Depuração** (**Shift** F5 ) interrompe o programa onde quer que ele + esteja e sai do depurador.
    - **Reiniciar** (**Ctrl**+**Shift**+**F5**) interrompe o programa no ponto em que está e o reinicia no depurador.
    - **Mostrar Próxima Instrução** ( + **Alt Num** **&#42;**) alterna para a próxima linha de código a ser executado. Isso é mais útil quando você navega em seu código durante uma sessão de depuração e deseja retornar rapidamente ao ponto em que o depurador está em pausa.
    - **Step Into** (**F11**) executa a próxima linha de código, inserindo em funções chamadas.
    - **Step Over** (**F10**) executa a próxima linha de código sem entrar em funções chamadas.
    - **Step Out** (**Shift** + **F11**) executa o restante da função atual e pausa no código de chamada.

1. Contorne a instrução `for` usando **Contornar**. *Passo a passo* significa que o depurador executa a linha de código atual, incluindo todas as chamadas de função e, em seguida, imediatamente entra em pausa outra vez. Observe como a variável `i` agora está definida nas janelas **Locais** e **Autos**.

1. Contorne a próxima linha de código, que chama `make_dot_string` e entra em pausa. **Passar por** aqui especificamente significa que o depurador executa todo o `make_dot_string` e pausa quando retorna. O depurador não é interrompido dentro dessa função, a menos que exista nela outro ponto de interrupção.

1. Continue depurando o código passo a passo mais algumas vezes e observe como os valores na janela **Locais** ou **Autos** se alteram.

1. Na janela **Locais** ou **Autos**, clique duas vezes na coluna **Valor** das variáveis `i` ou `s` para editar o valor. Pressione **Enter** ou clique em qualquer área fora desse valor para aplicar as alterações.

1. Continuar percorrendo o código passo a passo, usando **Intervir**. **Entrar significa** que o depurador entra dentro de qualquer chamada de função para a qual ele tem informações de depuração, como `make_dot_string` . Uma vez dentro do `make_dot_string`, você pode examinar as variáveis locais e percorrer o código especificamente.

1. Continue avançando **com Entrar** e observe que, quando você chegar ao final do , a próxima etapa retornará ao loop com o novo valor `make_dot_string` de retorno na `for` `s` variável. Conforme você entra novamente na `print` instrução , observe que **Entrar** em não entra `print` nessa função. Isso ocorre porque `print` não está escrita em Python, mas é código nativo dentro do runtime do Python.

1. Continue usando **o Step Into** até que você esteja novamente parcialmente no `make_dot_string` . Então, use **Sair** e observe que você retornará ao loop `for`. Com **Step Out**, o depurador executa o restante da função e, em seguida, pausa automaticamente no código de chamada. Isso é muito útil quando você percorreu algumas partes de uma função longa que deseja depurar, mas não deseja percorrer o restante e não quer definir um ponto de interrupção explícito no código de chamada.

1. Para continuar executando o programa até que o próximo ponto de interrupção seja atingido, use **Continuar** (**F5**). Como há um ponto de interrupção no loop `for`, você interrompe na próxima iteração.

1. Percorrer centenas de iterações de um loop pode ser entediante, portanto, o Visual Studio permite que você adicione uma *condição* a um ponto de interrupção. Assim, o depurador só pausa o programa no ponto de interrupção quando a condição é satisfeita. Por exemplo, você pode usar uma condição com o ponto de interrupção na instrução `for` para que ele faça uma pausa somente quando o valor de `i` exceder 1600. Para definir essa condição, clique com o botão direito do mouse no ponto de interrupção e selecione **Condições** (**Alt**+**F9** > **C**). Na janela pop-up **Configurações de Ponto de Interrupção** exibida, insira `i > 1600` como a expressão e selecione **Fechar**. Pressione **F5** para continuar e observe que o programa executa muitas ierções antes da próxima quebra.

    ![Configurando uma condição de ponto de interrupção](media/vs-getting-started-python-21-debugging4.png)

1. Para executar o programa até a conclusão, desabilite o ponto de interrupção clicando com o botão direito do mouse no ponto na margem e selecionando Desabilitar ponto de interrupção **(** **Ctrl** + **F9**). Em **seguida, selecione** Continuar (ou **pressione F5**) para executar o programa. Quando o programa for finalizado, o Visual Studio interromperá a sessão de depuração e retornará para o modo de edição. Observe que você também pode excluir o ponto de interrupção selecionando seu ponto ou clicando com o botão direito do mouse no ponto e selecionando Excluir ponto de interrupção, mas isso também exclui qualquer condição que você definiu.

> [!Tip]
> Em algumas situações, como uma falha ao iniciar o interpretador do Python em si, a janela de saída poderá aparecer apenas rapidamente e fechar-se automaticamente, sem dar uma oportunidade de ver as mensagens de erros. Se isso acontecer, clique com o botão direito do mouse no projeto **no** Gerenciador de Soluções , selecione Propriedades **,** selecione a guia **Depurar** e adicione ao campo `-i` **Argumentos do** Interpretador. Esse argumento faz com que o interpretador entre no modo interativo após a conclusão de um programa, mantendo a janela aberta até que você **insira Ctrl** + **Z**  >  **Enter** para sair.

## <a name="next-step"></a>Próxima etapa

> [!div class="nextstepaction"]
> [Instalar pacotes no ambiente do Python](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Depuração](debugging-python-in-visual-studio.md)
- [Depuração no Visual Studio](../debugger/debugger-feature-tour.md) oferece uma documentação completa sobre os recursos de depuração do Visual Studio.

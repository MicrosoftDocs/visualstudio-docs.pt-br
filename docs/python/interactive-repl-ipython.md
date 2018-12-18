---
title: REPL (janela interativa) do IPython
description: Usando a janela interativa do Visual Studio no modo IPython para um ambiente de desenvolvimento interativo e amigável com recursos de Computação Paralela Interativa.
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: b5429ccc963923a049d54ad3fbaa409586c0f772
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219244"
---
# <a name="use-ipython-in-the-interactive-window"></a>Usar o IPython na janela Interativa

A janela **Interativa** do Visual Studio no modo do IPython é um ambiente avançado de desenvolvimento interativo, porém amigável, que contém funcionalidades de Computação Paralela Interativa. Este artigo descreve o uso do IPython na janela **Interativa** do Visual Studio, na qual todas as funcionalidades normais da [janela Interativa](python-interactive-repl-in-visual-studio.md) também estão disponíveis.

Para esse passo a passo, você deve ter o ambiente [Anaconda](https://www.continuum.io) instalado, que inclui o IPython e as bibliotecas necessárias.

> [!Note]
> O IronPython não dá suporte ao IPython, apesar do fato de ser possível selecioná-lo no formulário **Opções Interativas**. Para obter mais informações, confira a [solicitação de recurso](https://github.com/Microsoft/PTVS/issues/84).

1. Abra o Visual Studio, alterne para a janela **Ambientes do Python** (**Exibir** > **Outras Janelas** > **Ambientes do Python**) e selecione um ambiente do Anaconda.

2. Examine a guia **Pacotes (Conda)** (que pode ser exibida como **pip** ou **Pacotes**) nesse ambiente para verificar se `ipython` e `matplotlib` estão listados. Caso contrário, instale-os nessa localização. (Confira [Janelas dos Ambientes do Python – guia Pacotes](python-environments-window-tab-reference.md).)

3. Selecione a guia **Visão Geral** e **Usar o modo interativo do IPython**. (No Visual Studio 2015, selecione **Configurar opções interativas** para abrir a caixa de diálogo **Opções** e, em seguida, defina o **Modo Interativo** como **IPython** e selecione **OK**).

4. Selecione **Abrir janela interativa** para exibir a janela **Interativa** no modo do IPython. Talvez seja necessário redefinir a janela se você acabou de mudar para o modo interativo. Talvez também seja necessário pressionar **Enter** se apenas um prompt >>> for exibido, para obter um prompt como **Em [2]**.

    ![A janela interativa no modo IPython](media/ipython-repl-03.png)

5. Insira o seguinte código:

   ```python
   import matplotlib.pyplot as plt
   import numpy as np
  
   x = np.linspace(0, 5, 10)
   y = x ** 2
   plt.plot(x, y, 'r', x, x ** 3, 'g', x, x ** 4, 'b')
   ```

6. Depois de inserir a última linha, você deverá ver um grafo embutido (que pode ser redimensionado arrastando o canto inferior direito, se desejado).

    ![Gráfico embutido na janela interativa](media/ipython-repl-04.png)

7. Em vez de digitar no REPL, você pode escrever o código no editor, selecioná-lo, clicar com o botão direito do mouse e selecionar o comando **Enviar para Interativa** (ou pressionar **Ctrl**+**Enter**). Tente colar o código abaixo em um novo arquivo no editor, selecionando-o com **Ctrl**+**A** e, em seguida, enviando-o para a janela **Interativa**. (O visual Studio envia o código como uma unidade para evitar a necessidade de gráficos intermediários ou parciais. Além disso, se você não tiver um projeto do Python aberto com outro ambiente selecionado, o Visual Studio abrirá uma janela **Interativa** para o ambiente selecionado como padrão na janela **Ambientes do Python**.)

    ```python
    from mpl_toolkits.mplot3d import Axes3D
    import matplotlib.pyplot as plt
    import numpy as np
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    for c, z in zip(['r', 'g', 'b', 'y'], [30, 20, 10, 0]):
        xs = np.arange(20)
        ys = np.random.rand(20)
        # You can provide either a single color or an array. To demonstrate this,
        # the first bar of each set is colored cyan.
        cs = [c] * len(xs)
        cs[0] = 'c'
        ax.bar(xs, ys, zs=z, zdir='y', color=cs, alpha=0.8)

    ax.set_xlabel('X')
    ax.set_ylabel('Y')
    ax.set_zlabel('Z')
    plt.show()
    ```

    ![Enviando o código do editor para a janela interativa](media/ipython-repl-05.png)

8. Para ver os grafos fora da janela **Interativa**, execute o código em vez de usar o comando **Depurar** > **Iniciar sem Depuração**.

O IPython tem muitos outros recursos úteis, como escape para o shell do sistema, substituição de variáveis, captura de saída etc. Consulte a [documentação do IPython](http://ipython.org/documentation.html) para obter mais informações.

### <a name="see-also"></a>Consulte também

- Para usar o Jupyter facilmente e sem instalação, experimente o [serviço hospedado dos Notebooks do Azure](https://notebooks.azure.com/) que permitem que você mantenha e compartilhe seus blocos de anotações com outras pessoas.

- A [Máquina Virtual de Ciência de Dados do Azure](/azure/machine-learning/data-science-virtual-machine/overview) também é pré-configurada para executar Jupyter notebooks, juntamente com uma ampla variedade de outras ferramentas de ciência de dados.

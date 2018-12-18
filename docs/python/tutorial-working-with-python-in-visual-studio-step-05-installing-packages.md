---
title: Tutorial sobre como trabalhar com o Python, etapa 5, instalar pacotes
description: Etapa 5 de um passo a passo básico das funcionalidades do Python no Visual Studio, demonstrando os recursos do Visual Studio para gerenciar pacotes em um ambiente Python.
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: tutorial
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 82cb54eb64d0864ba3b1d326d68f7303d3f2d882
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220502"
---
# <a name="step-5-install-packages-in-your-python-environment"></a>Etapa 5: Instalar pacotes no ambiente do Python

**Etapa anterior: [executar o código no depurador](tutorial-working-with-python-in-visual-studio-step-04-debugging.md)**

A comunidade de desenvolvedores do Python produziu milhares de pacotes úteis que você pode incorporar em seus próprios projetos. O Visual Studio oferece uma interface do usuário para gerenciar pacotes em seus ambientes do Python.

1. Selecione o comando de menu **Exibir** > **Outras Janelas** > **Ambientes do Python**. A janela **Ambientes de Python** será aberta como um par com o **Gerenciador de Soluções** e mostrará os diferentes ambientes disponíveis para você. A lista inclui os ambientes em que você instalou usando o instalador do Visual Studio e os que você instalou separadamente. O ambiente em negrito é o ambiente padrão, que é usado para novos projetos.

   ![Janela Ambientes do Python](media/environments-default-view-blue.png)

2. A guia **Visão geral** proporciona acesso rápido a uma janela **Interativa** do ambiente, junto com a pasta de instalação e os interpretadores desse ambiente. Por exemplo, escolha **Abrir janela Interativa** e uma janela **Interativa** desse ambiente específico será exibida no Visual Studio.

3. Selecione a guia **Pacotes** e você verá uma lista dos pacotes que estão atualmente instalados no ambiente.

   ![Pacotes instalados em um ambiente](media/environments-installed-packages-blue.png)

4. Para instalar o `matplotlib`, digite seu nome no campo de pesquisa e, em seguida, escolha **instalação do pip**

   ![Instalação do matplotlib no ambiente](media/environments-add-matplotlib1.png)

5. Dê permissão para a elevação, se for solicitado.

6. Depois de instalar o pacote, ele aparecerá na janela **Ambientes de Python**. O **X** à direita do pacote serve para desinstalá-lo.

   ![Conclusão da instalação do matplotlib no ambiente](media/environments-add-matplotlib2.png)

   Uma pequena barra de progresso pode ser exibida sob o ambiente para indicar que o Visual Studio está criando o banco de dados do IntelliSense para o pacote recém-instalado. A guia **IntelliSense** também mostra mais informações detalhadas. Observe que, até que o banco de dados seja concluído, os recursos do IntelliSense, como preenchimento automático e verificação de sintaxe, não estarão ativos no editor para esse pacote.

   Observe que o **Visual Studio 2017 versão 15.6** e posterior usa um método diferente e mais rápido para trabalhar com o IntelliSense e exibe uma mensagem para esse efeito na guia **IntelliSense**.

7. Crie um novo projeto com **Arquivo** > **Novo**  > **Projeto**, escolhendo o modelo **Aplicativo do Python**. No arquivo de código que é exibido, cole o código a seguir, que cria uma curva de cosseno como nas etapas anteriores do tutorial, só que plotada graficamente desta vez:

    ```python
    from math import radians
    import numpy as np     # installed with matplotlib
    import matplotlib.pyplot as plt

    def main():
        x = np.arange(0, radians(1800), radians(12))
        plt.plot(x, np.cos(x), 'b')
        plt.show()

    main()
    ```

8. Execute o programa com (**F5**) ou sem o depurador (**Ctrl**+**F5**) para ver a saída:

   ![Saída de exemplo de matplotlib](media/environments-add-matplotlib3.png)

## <a name="next-step"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Trabalhar com o Git](tutorial-working-with-python-in-visual-studio-step-06-working-with-git.md)

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Ambientes do Python](managing-python-environments-in-visual-studio.md)

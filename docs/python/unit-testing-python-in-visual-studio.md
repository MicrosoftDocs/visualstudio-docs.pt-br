---
title: Testes de unidade para Python
description: Configurando o teste de unidade para o código Python no Visual Studio a fim de aproveitar ao máximo os recursos do Gerenciador de Testes para descobrir, executar e depurar testes.
ms.date: 11/12/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: e8a3a61b7c77031033c9cdc988753437f25166a1
ms.sourcegitcommit: 6a955a2d179cd0e137942389f940d9fcbbe125de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607569"
---
# <a name="set-up-unit-testing-for-python-code"></a>Configurar o teste de unidade para o código do Python

Testes de unidade são partes do código que testam outras unidades de código em um aplicativo, normalmente, funções isoladas, classes e assim por diante. Quando um aplicativo é aprovado em todos os seus testes de unidade, pelo menos, é possível confiar que sua funcionalidade de baixo nível está correta.

O Python usa testes de unidade extensivamente para validar cenários durante a criação de um programa. O suporte do Python no Visual Studio inclui a descoberta, a execução e a depuração de testes de unidade no contexto do processo de desenvolvimento, sem precisar executar os testes separadamente.

Este artigo fornece uma breve descrição das funcionalidades de teste de unidade no Visual Studio com o Python. Para obter mais informações sobre testes de unidade em geral, consulte [Executar um teste de unidade no código](../test/unit-test-your-code.md).

|   |   |
|---|---|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo (Microsoft Virtual Academy)](https://mva.microsoft.com/en-US/training-courses-embed/python-tools-for-visual-studio-2017-18121/Video-Testing-Python-hb46k6LWE_405918567) sobre o teste de unidade no Python (2min31s). |

## <a name="discover-and-view-tests"></a>Descobrir e exibir testes

Por convenção, o Visual Studio identifica os testes como métodos cujos nomes começam com `test`. Para ver esse comportamento, faça o seguinte:

1. Abra um [projeto Python](managing-python-projects-in-visual-studio.md) carregado no Visual Studio, clique com o botão direito do mouse no projeto, escolha **Adicionar** > **Novo Item** e escolha **Teste de Unidade do Python** seguido por **Adicionar**.

1. Isso cria um arquivo *test1.py* com um código que importa o módulo `unittest` padrão, deriva uma classe de teste de `unittest.TestCase` e invoca `unittest.main()` se o script é executado diretamente:

    ```python
    import unittest

    class Test_test1(unittest.TestCase):
        def test_A(self):
            self.fail("Not implemented")

    if __name__ == '__main__':
        unittest.main()
    ```

1. Salve o arquivo se necessário e, em seguida, abra o **Gerenciador de Testes** com o comando de menu **Teste** > **Windows** >  **Gerenciador de Testes**.

1. O **Gerenciador de Testes** pesquisa os testes no projeto e os exibe conforme mostrado abaixo. Se você clicar duas vezes em um teste, seu arquivo de origem será aberto.

    ![Gerenciador de Testes mostrando o test_A padrão](media/unit-test-A.png)

1. Conforme você adiciona mais testes ao projeto, é possível organizar a exibição no **Gerenciador de Testes** usando o menu **Agrupar por** na barra de ferramentas:

    ![Menu da barra de ferramentas Agrupar Por do Gerenciador de Testes](media/unit-test-group-menu.png)

1. Também é possível inserir um texto no campo **Pesquisar** para filtrar os testes por nome.

Para obter mais informações sobre o módulo `unittest` e sobre como escrever testes, consulte a [documentação do Python 2.7](https://docs.python.org/2/library/unittest.html) ou a [documentação do Python 3.4](https://docs.python.org/3/library/unittest.html) (python.org).

## <a name="run-tests"></a>Executar testes

No **Gerenciador de Testes**, é possível executar testes de várias maneiras:

- **Executar Todos** claramente executa todos os testes mostrados (sujeito a filtros).
- O menu **Executar** fornece comandos para executar testes com falha, aprovados ou não executados como um grupo.
- É possível selecionar um ou mais testes, clicar com o botão direito do mouse e selecionar **Executar Testes Selecionados**.

Os testes são executados em segundo plano e o **Gerenciador de Testes** atualiza o status de cada teste conforme ele é concluído:

- Os testes aprovados mostram um tique verde e o tempo necessário para executar o teste:

    ![Status do test_A aprovado](media/unit-test-A-pass.png)

- Os testes com falha mostram uma cruz vermelha com um link **Saída** que mostra a saída do console e a saída `unittest` da execução de teste:

    ![Status do test_A com falha](media/unit-test-A-fail.png)

    ![test_A com falha com motivo](media/unit-test-A-fail-reason.png)

## <a name="debug-tests"></a>Depurar testes

Como os testes de unidade são partes do código, eles estão sujeitos a bugs, assim como qualquer outro código e, ocasionalmente, precisam ser executados em um depurador. No depurador é possível definir pontos de interrupção, examinar variáveis e executar o código em etapas. O Visual Studio também fornece ferramentas de diagnóstico para testes de unidade.

Para iniciar a depuração, defina um ponto de interrupção inicial no código, clique com o botão direito do mouse no teste (ou em uma seleção) no **Gerenciador de Testes** e escolha **Depurar Testes Selecionados**. O Visual Studio inicia o depurador do Python como faria com o código do aplicativo.

![Depurando um teste](media/unit-test-debugging.png)

Também é possível usar os comandos **Analisar Cobertura de Código nos Testes Selecionados** e **Teste de Perfil**, dependendo da versão do Visual Studio (consulte a [Matriz de recursos](overview-of-python-tools-for-visual-studio.md#features-matrix)).

### <a name="known-issues"></a>Problemas conhecidos

- Ao iniciar a depuração, o Visual Studio parece iniciar e interromper a depuração e, em seguida, iniciá-la novamente. Esse comportamento é esperado.
- Quando estiver depurando vários testes, cada um deles será executado de forma independente, o que interromperá a sessão de depuração.
- O Visual Studio falha intermitentemente ao iniciar um teste durante a depuração. Normalmente, a tentativa de depurar o teste novamente tem êxito.
- Durante a depuração, é possível executar a depuração circular de um teste na implementação `unittest`. Normalmente, a próxima etapa é executada ao final do programa e interrompe a depuração.

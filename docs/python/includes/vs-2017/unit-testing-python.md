---
title: Teste de unidade do código Python
description: A configuração do teste de unidade para o código Python no Visual Studio aproveita ao máximo as funcionalidades do Gerenciador de Testes para descobrir, executar e depurar testes.
ms.date: 09/18/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 032732f19855b9ba5c97c2e5281e8385f9ace3be
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535313"
---
## <a name="discover-and-view-tests"></a>Descobrir e exibir testes

Por convenção, o Visual Studio identifica os testes como métodos cujos nomes começam com `test`. Para ver esse comportamento, faça o seguinte:

1. Abra um [projeto Python](../../managing-python-projects-in-visual-studio.md) carregado no Visual Studio, clique com o botão direito do mouse no projeto, escolha **Adicionar** > **Novo Item** e escolha **Teste de Unidade do Python** seguido por **Adicionar**.

1. Isso cria um arquivo *test1.py* com um código que importa o módulo `unittest` padrão, deriva uma classe de teste de `unittest.TestCase` e invoca `unittest.main()` se o script é executado diretamente:

    ```python

    import unittest

    class Test_test1(unittest.TestCase):
        def test_A(self):
            self.fail("Not implemented")

    if __name__ == '__main__':
        unittest.main()
    ```

1. Salve o arquivo se necessário e, em seguida, abra o **Gerenciador de Testes** com o comando de menu **Teste** > **Windows** > ** Gerenciador de Testes**.

1. O **Gerenciador de testes** pesquisa o projeto em busca de testes e os exibe conforme mostrado abaixo. Se você clicar duas vezes em um teste, seu arquivo de origem será aberto.

    ![Gerenciador de Testes mostrando o test_A padrão](../../media/unit-test-A.png)

1. Conforme você adiciona mais testes ao seu projeto, pode organizar o modo de exibição no **Gerenciador de testes** usando o menu **Agrupar por** na barra de ferramentas:

    ![Menu da barra de ferramentas Agrupar Por do Gerenciador de Testes](../../media/unit-test-group-menu.png)

1. Você também pode inserir texto no campo de **pesquisa** para filtrar os testes por nome.

Para obter mais informações sobre o `unittest` módulo e escrever testes, consulte a [documentação do Python 2,7](https://docs.python.org/2/library/unittest.html) ou a documentação do [Python 3,7](https://docs.python.org/3/library/unittest.html) (Python.org).

## <a name="run-tests"></a>Executar testes

No **Gerenciador de testes** , você pode executar testes de várias maneiras:

- **Executar Todos** claramente executa todos os testes mostrados (sujeito a filtros).
- O menu **executar** fornece comandos para execução de testes com falha, aprovação ou não execução como um grupo.
- É possível selecionar um ou mais testes, clicar com o botão direito do mouse e selecionar **Executar Testes Selecionados**.

Testes executados em segundo plano e **Test Explorer** atualiza o status de cada teste à medida que ele é concluído:

- Os testes aprovados mostram um tique verde e o tempo necessário para executar o teste:

    ![Status do test_A aprovado](../../media/unit-test-A-pass.png)

- Os testes com falha mostram uma cruz vermelha com um link **Saída** que mostra a saída do console e a saída `unittest` da execução de teste:

    ![Status do test_A com falha](../../media/unit-test-A-fail.png)

    ![test_A com falha com motivo](../../media/unit-test-A-fail-reason.png)

## <a name="debug-tests"></a>Depurar testes

Como os testes de unidade são partes do código, eles estão sujeitos a bugs, assim como qualquer outro código e, ocasionalmente, precisam ser executados em um depurador. No depurador é possível definir pontos de interrupção, examinar variáveis e executar o código em etapas. O Visual Studio também fornece ferramentas de diagnóstico para testes de unidade.

Para iniciar a depuração, defina um ponto de interrupção inicial em seu código, clique com o botão direito do mouse no teste (ou uma seleção) no **Gerenciador de testes** e selecione **depurar testes selecionados**. O Visual Studio inicia o depurador do Python como faria com o código do aplicativo.

![Depurando um teste](../../media/unit-test-debugging.png)

Você também pode usar a **cobertura de código de análise para testes selecionados**. Para obter mais informações, confira [Usar a cobertura de código para determinar quanto do código está sendo testado](../../../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).

### <a name="known-issues"></a>Problemas conhecidos

- Ao iniciar a depuração, o Visual Studio parece iniciar e interromper a depuração e, em seguida, iniciá-la novamente. O comportamento é esperado.
- Quando estiver depurando vários testes, cada um deles será executado de forma independente, o que interromperá a sessão de depuração.
- O Visual Studio falha intermitentemente ao iniciar um teste durante a depuração. Normalmente, a tentativa de depurar o teste novamente tem êxito.
- Durante a depuração, é possível executar a depuração circular de um teste na implementação `unittest`. Normalmente, a próxima etapa é executada ao final do programa e interrompe a depuração.

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
ms.openlocfilehash: 6b611657db104a4b74e784df8925627ff41f3c33
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535312"
---
## <a name="select-the-test-framework-for-a-python-project"></a>Selecione a estrutura de teste para um projeto Python

O Visual Studio dá suporte a duas estruturas de teste para Python, [UnitTest](https://docs.python.org/3/library/unittest.html) e [pytest](https://pytest.org/en/latest/) (disponível no Visual Studio 2019 a partir da versão 16,3). Por padrão, nenhuma estrutura é selecionada quando você cria um projeto Python. Para especificar uma estrutura, clique com o botão direito do mouse no nome do projeto em Gerenciador de Soluções e selecione a opção **Propriedades** . Isso abre o designer de projeto, que permite que você configure testes por meio da guia **teste** . Nessa guia, você pode selecionar a estrutura de teste que deseja usar para seu projeto. 

* Para a estrutura **UnitTest** , o diretório raiz do projeto é usado para a descoberta de teste. Esse local, bem como o padrão de texto para identificar os testes, podem ser modificados na guia **teste** para valores especificados pelo usuário.
* Para a estrutura **pytest** , as opções de teste, como local de teste e padrões de nome de arquivo, são especificadas usando o arquivo de configuração padrão pytest. ini. Consulte a [documentação de referência do pytest](https://docs.pytest.org/en/latest/reference.html#ini-options-ref) para obter mais detalhes.

Depois de salvar as configurações e a seleção da estrutura, a descoberta de testes será iniciada no Gerenciador de testes. Se a janela Gerenciador de testes ainda não estiver aberta, navegue até a barra de ferramentas e selecione **testar**  >  **Gerenciador de testes**.

## <a name="configure-testing-for-python-without-a-project"></a>Configurar testes para Python sem um projeto
O Visual Studio permite executar e testar o código Python existente sem um projeto, [abrindo uma pasta](../../quickstart-05-python-visual-studio-open-folder.md) com código Python. Sob essas circunstâncias, você precisará usar um **PythonSettings.jsno** arquivo para configurar o teste. 
1. Abra o código Python existente usando a opção **abrir uma pasta local** . 

   ![A tela de inicialização do Visual Studio](../../media/quickstart-open-folder/01-open-local-folder.png)

1. Na janela Gerenciador de Soluções, clique no ícone **Mostrar todos os arquivos** para mostrar todos os arquivos na pasta atual.

   ![Botão Mostrar todos os arquivos](../../media/unit-test-show-files.png)

1. Navegue até o **PythonSettings.jsno** arquivo na pasta **configurações locais** . Se você não vir esse arquivo na pasta **configurações locais** , crie-o manualmente.
   
1. Adicione o campo **TestFrameWork** ao arquivo de configurações e defina-o como **pytest** ou **UnitTest** dependendo da estrutura de teste que você deseja usar.

    ```json
    {
    "TestFramework": "unittest",
    "UnitTestRootDirectory": "testing",
    "UnitTestPattern": "test_*.py"
    }
    ```

    > [!Note]
    > Para a estrutura **UnitTest** , se os campos **UnitTestRootDirectory** e **UnitTestPattern** não forem especificados no PythonSettings.jsno arquivo, eles serão adicionados e atribuídos valores padrão "." e "Test *. py", respectivamente.

1. Se sua pasta contiver um diretório **src** separado da pasta que contém seus testes, especifique o caminho para a pasta **src** usando o campo **SearchPaths** em seu **PythonSettings.jsno** arquivo.

    ```json
    {
    "TestFramework": "unittest",
    "UnitTestRootDirectory": "testing",
    "UnitTestPattern": "test_*.py",
    "SearchPaths": [ ".\\src"]
    }
    ```

1. Salve suas alterações no PythonSettings.jsno arquivo para iniciar a descoberta de teste para a estrutura especificada. 
   > [!Note]
   > Se a janela Gerenciador de testes já estiver aberta **Ctrl**  +  **R, uma** também disparará A descoberta.

## <a name="discover-and-view-tests"></a>Descobrir e exibir testes

Por padrão, o Visual Studio identifica os testes **UnitTest** e **pytest** como métodos cujos nomes começam com `test` . Para ver a descoberta de teste, faça o seguinte:

1. Abra um [projeto do Python](../../managing-python-projects-in-visual-studio.md).

1. Depois que o projeto for carregado no Visual Studio, clique com o botão direito do mouse em seu projeto no Gerenciador de Soluções e selecione a estrutura **UnitTest** ou **Pytest** na guia **teste** de propriedades.
   > [!Note]
   > Se você usar a estrutura pytest, poderá especificar o local de teste e os padrões de nome de arquivo usando o arquivo de configuração padrão pytest. ini. Por padrão, a pasta de trabalho/projeto é usada, com um padrão de `test_*py` e `*_test.py` . Consulte a [documentação de referência do pytest](https://docs.pytest.org/en/latest/reference.html#ini-options-ref) para obter mais detalhes.

1. Depois que a estrutura for selecionada, clique com o botão direito do mouse no projeto novamente e selecione **Adicionar**  >  **novo item**, em seguida, selecione **teste de unidade do Python** seguido por **Adicionar**.

1. Essa ação cria um arquivo *test_1. py* com código que importa o `unittest` módulo padrão, deriva uma classe de teste de `unittest.TestCase` e invoca `unittest.main()` se você executa o script diretamente:

    ```python
    import unittest

    class Test_test1(unittest.TestCase):
        def test_A(self):
            self.fail("Not implemented")

    if __name__ == '__main__':
        unittest.main()
    ```

1. Salve o arquivo, se necessário, abra o **Gerenciador de testes** com o comando de menu **Test**  >  **Test Explorer** .

1. O **Gerenciador de testes** pesquisa o projeto em busca de testes e os exibe conforme mostrado abaixo. Se você clicar duas vezes em um teste, seu arquivo de origem será aberto.

    ![Gerenciador de Testes mostrando o test_A padrão](../../media/unit-test-a-2.png) 

1. Conforme você adiciona mais testes ao seu projeto, pode organizar o modo de exibição no **Gerenciador de testes** usando o menu **Agrupar por** na barra de ferramentas:

    ![Menu da barra de ferramentas Agrupar Por do Gerenciador de Testes](../../media/unit-test-group-menu-2.png) 

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

> [!Note]
> Por padrão, a depuração de teste usa o depurador do ptvsd 4 para o Visual Studio 2017 (versões 15,8 e posteriores) e o debugpy para Visual Studio 2019 (versões 16,5 e posteriores). Se você quiser usar o ptvsd 3, poderá selecionar a opção **usar depurador herdado** em opções **ferramentas**  >  **Options**  >  **Python**  >  **depuração**do Python. 

Para iniciar a depuração, defina um ponto de interrupção inicial em seu código, clique com o botão direito do mouse no teste (ou uma seleção) no **Gerenciador de testes** e selecione **depurar testes selecionados**. O Visual Studio inicia o depurador do Python como faria com o código do aplicativo.

![Depurando um teste](../../media/unit-test-debugging.png)

Você também pode usar a **cobertura de código de análise para testes selecionados**. Para obter mais informações, confira [Usar a cobertura de código para determinar quanto do código está sendo testado](../../../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).

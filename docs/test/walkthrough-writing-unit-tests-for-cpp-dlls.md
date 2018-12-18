---
title: Como gravar testes de unidade para DLLs em C++
ms.date: 11/04/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: mblome
manager: douge
ms.workload:
- cplusplus
author: mikeblome
ms.openlocfilehash: 9458fd6886243102f6479166fb9df21f9e4869fd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49877244"
---
# <a name="how-to-write-unit-tests-for-c-dlls"></a>Como gravar testes de unidade para DLLs em C++

Este passo a passo descreve como desenvolver uma DLL nativa em C++ usando a metodologia de teste primeiro. As etapas básicas são as seguintes:

1.  [Criar um projeto de teste nativo](#create_test_project). O projeto de teste está localizado na mesma solução que o projeto de DLL.

2.  [Criar um projeto de DLL](#create_dll_project). Essas instruções passo a passo descrevem a criação de uma nova DLL, mas o procedimento para testar uma DLL existente é semelhante.

3.  [Tornar as funções da DLL visíveis para os testes](#make_functions_visible).

4.  [Aumentar interativamente os testes](#iterate). Recomendamos o uso de um ciclo de "refatoração vermelho e verde", em que o desenvolvimento do código é conduzido pelos testes.

5.  [Depurar os testes com falha](#debug). Você pode executar testes no modo de depuração.

6.  [Refatorar mantendo os testes inalterados](#refactor). Refatorar significa melhorar a estrutura do código sem alterar o comportamento externo. Você pode fazer isso para melhorar o desempenho, a extensibilidade ou a legibilidade do código. Uma vez que a intenção é não alterar o comportamento, você não alterará os testes ao executar uma alteração de refatoração no código. Os testes ajudam a garantir que você não introduza bugs durante a refatoração.

7.  [Verificar a cobertura](using-code-coverage-to-determine-how-much-code-is-being-tested.md). Os testes de unidade são mais úteis quando eles exercitam mais o seu código. Você pode descobrir quais partes do seu código foram usadas pelos testes.

8.  [Isolar unidades de recursos externos](using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md). Normalmente, uma DLL é dependente de outros componentes do sistema que você está desenvolvendo, como outras DLLs, bancos de dados ou subsistemas remotos. É útil testar cada unidade em isolamento de suas dependências. Os componentes externos podem fazer com que os testes sejam executados lentamente. Durante o desenvolvimento, os outros componentes podem não ser concluídos.

##  <a name="create_test_project"></a> Criar um projeto de teste de unidade nativo

1.  No menu **Arquivo**, escolha **Novo** > **Projeto**.

     Na caixa de diálogo, expanda **Instalados** > **Modelos** > **Visual C++** > **Teste**.

     Escolha o modelo de **Projeto de Teste de Unidade Nativo** ou qualquer estrutura instalada de sua preferência. Se você escolher outro modelo, como Google Test ou Boost.Test, os princípios básicos são os mesmos, embora alguns detalhes serão diferentes.

     Nestas instruções passo a passo, o projeto de teste é chamado `NativeRooterTest`.

     ![Criando um projeto de teste de unidade em C++](../test/media/utecpp01.png)

2.  No novo projeto, inspecione **unittest1.cpp**

     ![Projeto de teste com TEST&#95;CLASS e TEST&#95;METHOD](../test/media/utecpp2.png)

     Observe que:

    -   Cada teste é definido usando `TEST_METHOD(YourTestName){...}`.

         Você não precisa gravar uma assinatura de função convencional. A assinatura é criada pela macro TEST_METHOD. A macro gera uma função de instância que retorna void. Também gera uma função estática que retorna informações sobre o método de teste. Essas informações permitem que o Gerenciador de Testes encontrem o método.

    -   Os métodos de teste são agrupados em classes usando `TEST_CLASS(YourClassName){...}`.

         Quando os testes são executados, uma instância de cada classe de teste é criada. Os métodos de teste são chamados em uma ordem não especificada. Você pode definir métodos especiais que são invocados antes e depois de cada módulo, classe ou método.

3.  Verifique se o testes são executados no Gerenciador de Testes:

    1.  Insira algum código de teste:

        ```cpp
        TEST_METHOD(TestMethod1)
        {
            Assert::AreEqual(1,1);
        }
        ```

         Observe que a classe `Assert` fornece vários métodos estáticos que você pode usar para verificar os resultados em métodos de teste.

    2.  No menu **Teste**, escolha **Executar** > **Todos os Testes**.

         O teste é compilado e executado.

         O **Gerenciador de Testes** é exibido.

         O teste aparece em **Testes Aprovados**.

         ![Gerenciador de Testes de Unidade com um teste aprovado](../test/media/utecpp04.png)

##  <a name="create_dll_project"></a> Criar um projeto de DLL

1.  Crie um projeto do **Visual C++** usando o modelo **Projeto Win32**.

     Nestas instruções passo a passo, o projeto é chamado `RootFinder`.

     ![Criando um projeto Win32 em C++](../test/media/utecpp05.png)

2.  Selecione **DLL** e **Exportar Símbolos** no Assistente de Aplicativo Win32.

     A opção **Exportar Símbolos** gera uma macro conveniente que você pode usar para declarar métodos exportados.

     ![Assistente do projeto C++ definido para DLL e Exportar Símbolos](../test/media/utecpp06.png)

3.  Declare uma função exportada no arquivo *.h* da entidade de segurança:

     ![Novo projeto de código de DLL e arquivo .h com macros de API](../test/media/utecpp07.png)

     O declarador `__declspec(dllexport)` faz com que os membros públicos e protegidos da classe fiquem visíveis fora da DLL. Para obter mais informações, consulte [Usando dllimport e dllexport em classes C++](/cpp/cpp/using-dllimport-and-dllexport-in-cpp-classes).

4.  No arquivo *.cpp* da entidade de segurança, adicione um corpo mínimo à função:

    ```cpp
        // Find the square root of a number.
        double CRootFinder::SquareRoot(double v)
        {
            return 0.0;
        }
    ```

##  <a name="make_functions_visible"></a> Acoplar o projeto de teste ao projeto de DLL

1. Adicione o projeto de DLL às referências de projeto do projeto de teste:

   1.  Abra as propriedades do projeto de teste e escolha **Propriedades Comuns** > **Estrutura e Referências**.

        ![Propriedades de projeto C++ | Estrutura e Referências](../test/media/utecpp08.png)

   2.  Escolha **Adicionar Nova Referência**.

        Na caixa de diálogo **Adicionar Referência**, selecione o projeto de DLL e escolha **Adicionar**.

        ![Propriedades de projeto C++ | Adicionar Nova Referência](../test/media/utecpp09.png)

2. No arquivo *.cpp* do teste de unidade da entidade de segurança, inclua o arquivo *.h* do código da DLL:

   ```cpp
   #include "..\RootFinder\RootFinder.h"
   ```

3. Adicione um teste básico que usa a função exportada:

   ```cpp
   TEST_METHOD(BasicTest)
   {
      CRootFinder rooter;
      Assert::AreEqual(
         // Expected value:
         0.0,
         // Actual value:
         rooter.SquareRoot(0.0),
         // Tolerance:
         0.01,
        // Message:
        L"Basic test failed",
        // Line number - used if there is no PDB file:
        LINE_INFO());
   }
   ```

4. Compile a solução.

    O novo teste é exibido no **Gerenciador de Testes**.

5. No **Gerenciador de Testes**, escolha **Executar Todos**.

    ![Gerenciador de Testes de Unidade &#8211; Teste básico aprovado](../test/media/utecpp10.png)

   Você configurou o teste e os projetos de código, além de ter verificado que pode executar testes que executam funções no projeto de código. Agora, você pode começar a escrever testes e códigos reais.

##  <a name="iterate"></a> Aumentar iterativamente os testes e fazer com que sejam aprovados

1.  Adicione um novo teste:

    ```cpp
    TEST_METHOD(RangeTest)
    {
      CRootFinder rooter;
      for (double v = 1e-6; v < 1e6; v = v * 3.2)
      {
        double actual = rooter.SquareRoot(v*v);
        Assert::AreEqual(v, actual, v/1000);
      }
    }
    ```

    > [!TIP]
    > É recomendável não alterar testes que tenham sido aprovados. Em vez disso, adicione um novo teste, atualize o código para que o teste seja aprovado e adicione outro teste, e assim por diante.
    >
    > Quando os usuários alterarem os respectivos requisitos, desabilite os testes que não estejam mais corretos. Escreva novos testes e faça-os funcionar, um por vez, da mesma maneira incremental.

2.  Compile a solução e, em seguida, no **Gerenciador de Testes**, escolha **Executar Todos**.

     Falha no novo teste.

     ![Falha de RangeTest](../test/media/ute_cpp_testexplorer_rangetest_fail.png)

    > [!TIP]
    > Verifique se os testes falham imediatamente após escrevê-los. Isso ajuda a impedir a facilidade de errar ao escrever um teste que nunca falha.

3.  Aprimore o código DLL para que o novo teste seja aprovado:

    ```cpp
    #include <math.h>
    ...
    double CRootFinder::SquareRoot(double v)
    {
      double result = v;
      double diff = v;
      while (diff > result/1000)
      {
        double oldResult = result;
        result = result - (result*result - v)/(2*result);
        diff = abs (oldResult - result);
      }
      return result;
    }
    ```

4.  Compile a solução e, no **Gerenciador de Testes**, escolha **Executar Todos**.

     Ambos os testes são aprovados.

     ![Gerenciador de Testes de Unidade &#8211; Teste de intervalo aprovado](../test/media/utecpp12.png)

    > [!TIP]
    > Desenvolva o código adicionando testes, um de cada vez. Verifique se todos os testes passaram após cada iteração.

##  <a name="debug"></a> Depurar um teste que falhou

1.  Adicione outro teste:

    ```cpp
    #include <stdexcept>
    ...
    // Verify that negative inputs throw an exception.
    TEST_METHOD(NegativeRangeTest)
    {
      wchar_t message[200];
      CRootFinder rooter;
      for (double v = -0.1; v > -3.0; v = v - 0.5)
      {
        try
        {
          // Should raise an exception:
          double result = rooter.SquareRoot(v);

          _swprintf(message, L"No exception for input %g", v);
          Assert::Fail(message, LINE_INFO());
        }
        catch (std::out_of_range ex)
        {
          continue; // Correct exception.
        }
        catch (...)
        {
          _swprintf(message, L"Incorrect exception for %g", v);
          Assert::Fail(message, LINE_INFO());
        }
      }
    }
    ```

2.  Compile a solução e escolha **Executar Todos**.

3.  Abra (ou clique duas vezes) no teste com falha.

     A asserção com falha é realçada. A mensagem de falha fica visível no painel de detalhes do **Gerenciador de Testes**.

     ![Falha de NegativeRangeTests](../test/media/ute_cpp_testexplorer_negativerangetest_fail.png)

4.  Para ver o motivo da falha do teste, percorra a função:

    1.  Defina o ponto de interrupção no início da função SquareRoot.

    2.  No menu de atalho do teste com falha, escolha **Depurar Testes Selecionados**.

         Quando a execução for interrompida no ponto de interrupção, percorra o código.

5.  Insira o código na função que você está desenvolvendo:

    ```cpp

    #include <stdexcept>
    ...
    double CRootFinder::SquareRoot(double v)
    {
        // Validate parameter:
        if (v < 0.0)
        {
          throw std::out_of_range("Can't do square roots of negatives");
        }

    ```

6.  Todos os testes agora foram aprovados.

     ![Todos os testes serão aprovados](../test/media/ute_ult_alltestspass.png)

> [!TIP]
> Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo com o botão de alternância ![UTE&#95;parallelicon&#45;small](../test/media/ute_parallelicon-small.png) na barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.


##  <a name="refactor"></a> Refatorar o código sem alterar os testes

1.  Simplifique o cálculo central na função SquareRoot:

    ```cpp
    // old code:
    //   result = result - (result*result - v)/(2*result);
    // new code:
         result = (result + v/result)/2.0;

    ```

2.  Compile a solução e escolha **Executar Todos** para verificar se você não introduziu nenhum erro.

    > [!TIP]
    > Um bom conjunto de testes de unidade garante que você não introduza bugs ao alterar o código.
    >
    > Mantenha a refatoração separada das outras alterações.

## <a name="next-steps"></a>Próximas etapas

-   **Isolamento.** A maioria das DLLs são dependentes de outros subsistemas, como bancos de dados e outras DLLs. Geralmente, esses outros componentes são desenvolvidos em paralelo. Para permitir que os testes de unidade sejam executados enquanto os outros componentes ainda não estiverem disponíveis, você precisará substituir o fictício ou

-   **Testes de aceitação do build.** Você pode executar testes no servidor de build da sua equipe em intervalos definidos. Isso garante que não sejam introduzidos bugs quando o trabalho de vários membros da equipe são integrados.

-   **Testes de check-in.** Você pode exigir que alguns testes sejam executadas antes de cada membro da equipe fazer check-in do código no controle do código-fonte. Normalmente, esse é um subconjunto do conjunto completo dos testes de aceitação do build.

     Você também pode exigir um nível mínimo de cobertura de código.

## <a name="see-also"></a>Consulte também

- [Adicionar testes de unidade a aplicativos C++ existentes](../test/unit-testing-existing-cpp-applications-with-test-explorer.md)
- [Usando Microsoft.VisualStudio.TestTools.CppUnitTestFramework](how-to-use-microsoft-test-framework-for-cpp.md)
- [Depurar código nativo](../debugger/debugging-native-code.md)
- [Passo a passo: Criando e usando uma biblioteca de vínculo dinâmico (C++)](/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp)
- [Importar e exportar](/cpp/build/importing-and-exporting)

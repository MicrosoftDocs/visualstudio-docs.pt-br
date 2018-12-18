---
title: Escrevendo testes de unidade para C-C++ com o Microsoft Unit Testing Framework para C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4f4b5f10-7314-4725-8c6e-e72f52eff918
caps.latest.revision: 16
ms.author: gewarren
manager: douge
ms.openlocfilehash: 180f970f35ed0bb3de70ba3a7b7b47dbe656ddf7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49904031"
---
# <a name="writing-unit-tests-for-cc-with-the-microsoft-unit-testing-framework-for-c"></a>Escrevendo teste de unidade para C/C++ com o Microsoft Unit Testing Framework para C++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode criar testes de unidade para código não gerenciado escrito em C++. O código não gerenciado é, às vezes, chamado de código nativo.  
  
 O procedimento a seguir contém as informações essenciais que servirão de introdução para você. As seções posteriores fornecem instruções passo a passo que descrevem as etapas com mais detalhes.  
  
### <a name="to-write-unit-tests-for-an-unmanaged-code-dll"></a>Para escrever testes de unidade para uma DLL de código não gerenciado  
  
1.  Use o modelo **Projeto de Teste Nativo** para criar um projeto separado do Visual Studio para os testes.  
  
     O projeto contém alguns códigos de teste de exemplo.  
  
2.  Disponibilize a DLL para o projeto de teste:  
  
    -   `#include` um arquivo `.h` que contém as declarações das funções acessíveis externamente da DLL.  
  
         O arquivo `.h` deve conter as declarações das funções marcadas com `_declspec(dllimport)`. Como opção, você pode exportar os métodos usando um arquivo DEF. Para obter mais informações, consulte [Importando e exportando](http://msdn.microsoft.com/library/7c44c2aa-2117-4cec-9615-a65bfd3f8f7b).  
  
         Os testes de unidade podem acessar apenas as funções exportadas da DLL em teste.  
  
    -   Adicione o projeto de DLL às Referências do projeto de teste:  
  
         Nas **Propriedades** do projeto de teste, expanda **Propriedades Comuns**, **Estrutura e Referências** e escolha **Adicionar Referência**.  
  
3.  No projeto de teste, crie classes e métodos de teste usando as macros TEST e a classe Assert da seguinte maneira:  
  
    ```cpp  
    #include "stdafx.h"  
    #include <CppUnitTest.h>  
    #include "..\MyProjectUnderTest\MyCodeUnderTest.h"  
    using namespace Microsoft::VisualStudio::CppUnitTestFramework;  
    TEST_CLASS(TestClassName)  
    {  
    public:  
      TEST_METHOD(TestMethodName)  
      {  
        // Run a function under test here.  
        Assert::AreEqual(expectedValue, actualValue, L"message", LINE_INFO());  
      }  
    }  
    ```  
  
    -   `Assert` contém várias funções estáticas que você pode usar para verificar o resultado de um teste.  
  
    -   O parâmetro `LINE_INFO()` é opcional. Nos casos em que não há nenhum arquivo PDB, ele permite ao executor de teste identificar o local de uma falha.  
  
    -   Você também pode escrever métodos de instalação e de limpeza de teste. Para obter mais informações, abra a definição da macro `TEST_METHOD` e leia os comentários em CppUnitTest.h  
  
    -   Não é possível aninhar as classes de teste.  
  
4.  Use o Gerenciador de Testes para executar os testes:  
  
    1.  No menu **Exibir**, escolha **Outras Janelas**, **Gerenciador de Testes**.  
  
    2.  Compile a solução do Visual Studio.  
  
    3.  No Gerenciador de Testes, escolha **Executar Todos**.  
  
    4.  Para investigar qualquer teste em mais detalhes no Gerenciador de Testes:  
  
        1.  Selecione o nome do teste para ver mais detalhes, como uma mensagem de falha e um rastreamento de pilha.  
  
        2.  Abra o nome do teste (por exemplo, clicando duas vezes) para acessar o local da falha ou o código do teste.  
  
        3.  No menu de atalho de um teste, escolha **Depurar Teste Selecionado** para executar o teste no depurador.  
  
##  <a name="walkthrough"></a> Instruções passo a passo: desenvolvendo uma DLL não gerenciada com o Gerenciador de Testes  
 Você pode adaptar estas instruções passo a passo para desenvolver a sua própria DLL. As etapas de entidade são as seguintes:  
  
1.  [Criar um projeto de teste nativo](#unitTestProject). Os testes são criados em um projeto separado da DLL que você está desenvolvendo.  
  
2.  [Criar um projeto de DLL](#createDllProject). Essas instruções passo a passo descrevem a criação de uma nova DLL, mas o procedimento para testar uma DLL existente é semelhante.  
  
3.  [Tornar as funções da DLL visíveis para os testes](#coupleProjects).  
  
4.  [Aumentar interativamente os testes](#iterate). Recomendamos o uso de um ciclo de "refatoração vermelho e verde", em que o desenvolvimento do código é conduzido pelos testes.  
  
5.  [Depurar os testes com falha](#debug). Você pode executar testes no modo de depuração.  
  
6.  [Refatorar mantendo os testes inalterados](#refactor). Refatorar significa melhorar a estrutura do código sem alterar o comportamento externo. Você pode fazer isso para melhorar o desempenho, a extensibilidade ou a legibilidade do código. Uma vez que a intenção é não alterar o comportamento, você não alterará os testes ao executar uma alteração de refatoração no código. Os testes ajudam a garantir que você não introduza bugs durante a refatoração. Com isso, você poderá fazer essas alterações com muito mais confiança como se você não tivesse os testes.  
  
7.  [Verificar a cobertura](https://msdn.microsoft.com/library/fc8hec9e.aspx). Os testes de unidade são mais úteis quando eles exercitam mais o seu código. Você pode descobrir quais partes do seu código foram usadas pelos testes.  
  
8.  [Isolar unidades de recursos externos](https://msdn.microsoft.com/library/hh549174.aspx). Normalmente, uma DLL é dependente de outros componentes do sistema que você está desenvolvendo, como outras DLLs, bancos de dados ou subsistemas remotos. É útil testar cada unidade em isolamento de suas dependências. Os componentes externos podem fazer com que os testes sejam executados lentamente. Durante o desenvolvimento, os outros componentes podem não ser concluídos.  
  
###  <a name="unitTestProject"></a> Criar um projeto de teste de unidade nativo  
  
1.  No menu **Arquivo**, escolha **Novo**, **Projeto**.  
  
     Na caixa de diálogo, expanda **Instalados**, **Modelos**, **Visual C++**, **Teste**.  
  
     Escolha o modelo **Projeto de Teste Nativo**.  
  
     Nestas instruções passo a passo, o projeto de teste é chamado `NativeRooterTest`.  
  
     ![Criando um projeto de teste de unidade C&#43;&#43;](../test/media/utecpp01.png "UteCpp01")  
  
2.  No novo projeto, inspecione **unittest1.cpp**  
  
     ![Projeto de teste com TEST&#95;CLASS e TEST&#95;METHOD](../test/media/utecpp2.png "UteCpp2")  
  
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
  
    2.  No menu **Teste**, escolha **Executar**, **Todos os Testes**.  
  
         O teste é compilado e executado.  
  
         O Gerenciador de Testes é exibido.  
  
         O teste aparece em **Testes Aprovados**.  
  
         ![Gerenciador de Testes de Unidade com um teste aprovado](../test/media/utecpp04.png "UteCpp04")  
  
###  <a name="createDllProject"></a> Criar um projeto de DLL não gerenciada  
  
1.  Crie um projeto do **Visual C++** usando o modelo **Projeto Win32**.  
  
     Nestas instruções passo a passo, o projeto é chamado `RootFinder`.  
  
     ![Criando um projeto Win32 C&#43;&#43;](../test/media/utecpp05.png "UteCpp05")  
  
2.  Selecione **DLL** e **Exportar Símbolos** no Assistente de Aplicativo Win32.  
  
     A opção **Exportar Símbolos** gera uma macro conveniente que você pode usar para declarar métodos exportados.  
  
     ![Assistente do projeto C&#43;&#43; definido para DLL e Exportar Símbolos](../test/media/utecpp06.png "UteCpp06")  
  
3.  Declare uma função exportada no arquivo .h da entidade de segurança:  
  
     ![Novo projeto de código de DLL e arquivo .h com macros de API](../test/media/utecpp07.png "UteCpp07")  
  
     O declarador `__declspec(dllexport)` faz com que os membros públicos e protegidos da classe fiquem visíveis fora da DLL. Para obter mais informações, consulte [Usando dllimport e dllexport em classes C++](http://msdn.microsoft.com/library/8d7d1303-b9e9-47ca-96cc-67bf444a08a9).  
  
4.  No arquivo .cpp da entidade de segurança, adicione um corpo mínimo para a função:  
  
    ```cpp  
    // Find the square root of a number.  
    double CRootFinder::SquareRoot(double v)  
    {  
      return 0.0;  
    }  
    ```  
  
###  <a name="coupleProjects"></a> Acoplar o projeto de teste ao projeto de DLL  
  
1. Adicione o projeto de DLL às referências de projeto do projeto de teste:  
  
   1.  Abra as propriedades do projeto de teste e escolha **Propriedades Comuns**, **Estrutura e Referências**.  
  
        ![Propriedades de projeto C&#43;&#43; &#45; Estrutura e Referências](../test/media/utecpp08.png "UteCpp08")  
  
   2.  Escolha **Adicionar Nova Referência**.  
  
        Na caixa de diálogo **Adicionar Referência**, selecione o projeto de DLL e escolha **Adicionar**.  
  
        ![Propriedades do projeto C&#43;&#43; &#45; Adicionar Nova Referência](../test/media/utecpp09.png "UteCpp09")  
  
2. No arquivo .cpp do teste de unidade da entidade de segurança, inclua o arquivo .h do código da DLL:  
  
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
  
    O novo teste aparece no Gerenciador de Testes.  
  
5. No Gerenciador de Testes, escolha **Executar Todos**.  
  
    ![Gerenciador de Testes de Unidade &#45; Teste básico aprovado](../test/media/utecpp10.png "UteCpp10")  
  
   Você configurou o teste e os projetos de código, além de ter verificado que pode executar testes que executam funções no projeto de código. Agora, você pode começar a escrever testes e códigos reais.  
  
###  <a name="iterate"></a> Aumentar iterativamente os testes e fazer com que sejam aprovados  
  
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
    >  É recomendável não alterar testes que tenham sido aprovados. Em vez disso, adicione um novo teste, atualize o código para que o teste seja aprovado e adicione outro teste, e assim por diante.  
    >   
    >  Quando os usuários alterarem os respectivos requisitos, desabilite os testes que não estejam mais corretos. Escreva novos testes e faça-os funcionar, um por vez, da mesma maneira incremental.  
  
2.  Compile a solução e, no Gerenciador de Testes, escolha **Executar Todos**.  
  
     Falha no novo teste.  
  
     ![Falha em RangeTest](../test/media/ute-cpp-testexplorer-rangetest-fail.png "UTE_Cpp_TestExplorer_RangeTest_Fail")  
  
    > [!TIP]
    >  Verifique se os testes falham imediatamente após escrevê-los. Isso ajuda a impedir a facilidade de errar ao escrever um teste que nunca falha.  
  
3.  Aprimore o código em teste para que o novo teste seja aprovado:  
  
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
  
4.  Compile a solução e, no Gerenciador de Testes, escolha **Executar Todos**.  
  
     Ambos os testes são aprovados.  
  
     ![Gerenciador de Testes de Unidade &#45; Teste de intervalo aprovado](../test/media/utecpp12.png "UteCpp12")  
  
    > [!TIP]
    >  Desenvolva o código adicionando testes, um de cada vez. Verifique se todos os testes passaram após cada iteração.  
  
###  <a name="debug"></a> Depurar um teste que falhou  
  
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
  
     A asserção com falha é realçada. A mensagem de falha fica visível no painel de detalhes do Gerenciador de Testes.  
  
     ![Falha em NegativeRangeTests](../test/media/ute-cpp-testexplorer-negativerangetest-fail.png "UTE_Cpp_TestExplorer_NegativeRangeTest_Fail")  
  
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
  
     ![Todos os testes foram aprovados](../test/media/ute-ult-alltestspass.png "UTE_ULT_AllTestsPass")  
  
> [!TIP]
>  Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo com o botão de alternância ![UTE&#95;parallelicon&#45;small](../test/media/ute-parallelicon-small.png "UTE_parallelicon-small") na barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.  
  
###  <a name="refactor"></a> Refatorar o código sem alterar os testes  
  
1.  Simplifique o cálculo central na função SquareRoot:  
  
    ```  
    // old code:  
    //   result = result - (result*result - v)/(2*result);  
    // new code:  
         result = (result + v/result)/2.0;  
  
    ```  
  
2.  Compile a solução e escolha **Executar Todos** para verificar se você não introduziu nenhum erro.  
  
    > [!TIP]
    >  Um bom conjunto de testes de unidade garante que você não introduza bugs ao alterar o código.  
    >   
    >  Mantenha a refatoração separada das outras alterações.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   **Isolamento.** A maioria das DLLs são dependentes de outros subsistemas, como bancos de dados e outras DLLs. Geralmente, esses outros componentes são desenvolvidos em paralelo. Para permitir que os testes de unidade sejam executados enquanto os outros componentes ainda não estiverem disponíveis, você precisará substituir o fictício ou  
  
-   **Testes de aceitação do build.** Você pode executar testes no servidor de build da sua equipe em intervalos definidos. Isso garante que não sejam introduzidos bugs quando o trabalho de vários membros da equipe são integrados.  
  
-   **Testes de check-in.** Você pode exigir que alguns testes sejam executadas antes de cada membro da equipe fazer check-in do código no controle do código-fonte. Normalmente, esse é um subconjunto do conjunto completo dos testes de aceitação do build.  
  
     Você também pode exigir um nível mínimo de cobertura de código.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionando testes de unidade a aplicativos do C++ existentes](../test/unit-testing-existing-cpp-applications-with-test-explorer.md)   
 [Usando Microsoft.VisualStudio.TestTools.CppUnitTestFramework](../test/using-microsoft-visualstudio-testtools-cppunittestframework.md)   
 [An Overview of Managed/Unmanaged Code Interoperability](http://msdn.microsoft.com/library/ms973872.aspx)  (Uma visão geral da interoperabilidade de código gerenciado/não gerenciado)  
 [Depurando código nativo](../debugger/debugging-native-code.md)   
 [Instruções passo a passo: criando e usando uma biblioteca de vínculo dinâmico (C++)](http://msdn.microsoft.com/library/3ae94848-44e7-4955-bbad-7d40f493e941)   
 [Importando e exportando](http://msdn.microsoft.com/library/7c44c2aa-2117-4cec-9615-a65bfd3f8f7b)




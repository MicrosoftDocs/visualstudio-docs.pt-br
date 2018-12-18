---
title: Executar o teste de unidade de uma DLL do Visual C++ para aplicativos da Store | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 24afc90a-8774-4699-ab01-6602a7e6feb2
caps.latest.revision: 15
author: alexhomer1
ms.author: gewarren
manager: robinr
ms.openlocfilehash: e3cce1fcda4ccc9a4e61b5a02d719e1ceaa1d77d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49816489"
---
# <a name="unit-testing-a-visual-c-dll-for-store-apps"></a>Executar o teste de unidade de uma DLL do Visual C++ para aplicativos da Store
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve uma maneira de criar testes de unidade para uma DLL em C++ para aplicativos da Windows Store. A DLL RooterLib demonstra memórias vagas da teoria de limite do cálculo implementando uma função que calcula uma estimativa da raiz quadrada de um determinado número. A DLL, em seguida, pode ser incluída em um aplicativo da Windows Store que mostra a um usuário as coisas divertidas que podem ser feitas com matemática.  
  
 Este tópico demonstra como usar teste de unidade como a primeira etapa do desenvolvimento. Nessa abordagem, primeiramente, você escreve um método de teste que verifique um comportamento específico no sistema que está sendo testado e, em seguida, escreve um código que passe no teste. Ao fazer alterações na ordem dos procedimentos a seguir, é possível reverter essa estratégia para primeiro escrever o código que deseja testar e depois escrever as unidades de teste.  
  
 Este tópico também cria uma única solução do Visual Studio e projetos separados para os testes de unidade e a DLL que você deseja testar. Também é possível incluir os testes de unidade diretamente no projeto de DLL ou criar soluções separadas para os testes de unidade e a .DLL. Consulte [Adicionar teste de unidade de aplicativos C++ existentes](../test/unit-testing-existing-cpp-applications-with-test-explorer.md) para obter dicas sobre a estrutura a ser usada.  
  
##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 Este tópico apresenta as seguintes tarefas:  
  
 [Criar a solução e o projeto de teste de unidade](#BKMK_Create_the_solution_and_the_unit_test_project)  
  
 [Verificar se o testes são executados no Gerenciador de Testes](#BKMK_Verify_that_the_tests_run_in_Test_Explorer)  
  
 [Adicione o projeto DLL à solução](#BKMK_Add_the_DLL_project_to_the_solution)  
  
 [Acoplar o projeto de teste ao projeto de dll](#BKMK_Couple_the_test_project_to_the_dll_project)  
  
 [Multiplicar os testes iterativamente e fazê-los passar](#BKMK_Iteratively_augment_the_tests_and_make_them_pass)  
  
 [Depurar um teste que falhou](#BKMK_Debug_a_failing_test)  
  
 [Refatorar o código sem alterar os testes](#BKMK_Refactor_the_code_without_changing_tests)  
  
##  <a name="BKMK_Create_the_solution_and_the_unit_test_project"></a> Criar a solução e o projeto de teste de unidade  
  
1.  No menu **Arquivo**, escolha **Novo** e, em seguida, **Novo Projeto**.  
  
2.  No diálogo Novo Projeto, expanda **Instalado** e **Visual C++** e, em seguida, escolha **Windows Store**. Em seguida, escolha **Biblioteca de Teste de Unidade (aplicativos da Windows Store)** na lista de modelos de projeto.  
  
     ![Cria um C&#43;&#43; biblioteca de teste de unidade](../test/media/ute-cpp-windows-unittestlib-create.png "UTE_Cpp_windows_UnitTestLib_Create")  
  
3.  Dê ao projeto o nome `RooterLibTests`; especifique o local, dê à solução o nome `RooterLib`; e certifique-se de que a opção **Criar diretório para solução** esteja selecionada.  
  
     ![Especifique o nome do projeto e solução e local](../test/media/ute-cpp-windows-unittestlib-createspecs.png "UTE_Cpp_windows_UnitTestLib_CreateSpecs")  
  
4.  No novo projeto, abra **unittest1.cpp**.  
  
     ![unittest1.cpp](../test/media/ute-cpp-windows-unittest1-cpp.png "UTE_Cpp_windows_unittest1_cpp")  
  
     Observe que:  
  
    -   Cada teste é definido usando `TEST_METHOD(YourTestName){...}`.  
  
         Você não precisa gravar uma assinatura de função convencional. A assinatura é criada pela macro TEST_METHOD. A macro gera uma função de instância que retorna void. Também gera uma função estática que retorna informações sobre o método de teste. Essas informações permitem que o Gerenciador de Testes encontrem o método.  
  
    -   Os métodos de teste são agrupados em classes usando `TEST_CLASS(YourClassName){...}`.  
  
         Quando os testes são executados, uma instância de cada classe de teste é criada. Os métodos de teste são chamados em uma ordem não especificada. Você pode definir métodos especiais que são invocados antes e depois de cada módulo, classe ou método. Para obter mais informações, consulte [Usando Microsoft.VisualStudio.TestTools.CppUnitTestFramework](../test/using-microsoft-visualstudio-testtools-cppunittestframework.md) na biblioteca MSDN.  
  
##  <a name="BKMK_Verify_that_the_tests_run_in_Test_Explorer"></a> Verificar se o testes são executados no Gerenciador de Testes  
  
1.  Insira algum código de teste:  
  
    ```cpp  
    TEST_METHOD(TestMethod1)  
    {  
        Assert::AreEqual(1,1);  
    }  
    ```  
  
     Observe que a classe `Assert` fornece vários métodos estáticos que você pode usar para verificar os resultados em métodos de teste.  
  
2.  No menu **Testar**, escolha **Executar** e **Executar Todos**.  
  
     O projeto de teste é compilado e executado. A janela Gerenciador de Testes é exibida e o teste é listado em **Testes Aprovados**. O painel Resumo, na parte inferior da janela, fornece mais detalhes sobre o teste selecionado.  
  
     ![Gerenciador de testes](../test/media/ute-cpp-testexplorer-testmethod1.png "UTE_Cpp_TestExplorer_TestMethod1")  
  
##  <a name="BKMK_Add_the_DLL_project_to_the_solution"></a> Adicione o projeto DLL à solução  
  
1.  No Gerenciador de Soluções, escolha o nome da solução. No menu de atalho, escolha **Adicionar** e então **Adicionar Novo Projeto**.  
  
     ![Criar o projeto RooterLib](../test/media/ute-cpp-windows-rooterlib-create.png "UTE_Cpp_windows_RooterLib_Create")  
  
2.  Na caixa de diálogo **Adicionar Novo Projeto**, escolha **DLL (aplicativos da Windows Store)**.  
  
3.  Adicione o código a seguir ao arquivo **RooterLib.h**:  
  
    ```cpp  
    // The following ifdef block is the standard way of creating macros which make exporting   
    // from a DLL simpler. All files within this DLL are compiled with the ROOTERLIB_EXPORTS  
    // symbol defined on the command line. This symbol should not be defined on any project  
    // that uses this DLL. This way any other project whose source files include this file see   
    // ROOTERLIB_API functions as being imported from a DLL, whereas this DLL sees symbols  
    // defined with this macro as being exported.  
    #ifdef ROOTERLIB_EXPORTS  
    #define ROOTERLIB_API  __declspec(dllexport)  
    #else  
    #define ROOTERLIB_API __declspec(dllimport)  
    #endif //ROOTERLIB_EXPORTS  
  
    class ROOTERLIB_API CRooterLib {  
    public:  
        CRooterLib(void);  
        double SquareRoot(double v);  
    };  
    ```  
  
     Os comentários explicam o bloco ifdef não apenas ao desenvolvedor da dll, mas também a qualquer pessoa que faça referência à DLL em seu projeto. Você pode adicionar o símbolo ROOTERLIB_EXPORTS à linha de comando usando as propriedades do projeto da DLL.  
  
     A classe `CRooterLib` declara um construtor e o método avaliador `SqareRoot`.  
  
4.  Adicione o símbolo ROOTERLIB_EXPORTS à linha de comando.  
  
    1.  No Gerenciador de Soluções, escolha o projeto **RooterLib** e escolha **Propriedades** no menu de atalho.  
  
         ![Adicionar uma definição de símbolo do pré-processador](../test/media/ute-cpp-windows-addpreprocessorsymbol.png "UTE_Cpp_windows_AddPreprocessorSymbol")  
  
    2.  Na caixa de diálogo Página de Propriedades de RooterLib, expanda **Propriedades de Configuração**, expanda **C++** e escolha **Pré-processador**.  
  
    3.  Escolha **\<<Editar...>** na lista **Definições do Pré-processador** e, em seguida, adicione `ROOTERLIB_EXPORTS` na caixa de diálogo Definições do Pré-processador.  
  
5.  Adicione implementações mínimas das funções declaradas. Abra **RooterLib.cpp** e adicione o seguinte código:  
  
    ```  
    // constructor  
    CRooterLib::CRooterLib()  
    {  
    }  
  
    // Find the square root of a number.  
    double CRooterLib::SquareRoot(double v)  
    {  
        return 0.0;  
    }  
  
    ```  
  
##  <a name="BKMK_Couple_the_test_project_to_the_dll_project"></a> Acoplar o projeto de teste ao projeto de dll  
  
1. Adicione RooterLib ao projeto RooterLibTests.  
  
   1.  No Gerenciador de Soluções, escolha o projeto **RooterLibTests** e, em seguida, **Referências...** no menu de atalho.  
  
   2.  Na caixa de diálogo Propriedades do Projeto RooterLib, expanda **Propriedades Comuns** e escolha **Estrutura e Referências**.  
  
   3.  Escolha **Adicionar nova referência...**  
  
   4.  Na caixa de diálogo **Adicionar Referência**, expanda **Solução** e, em seguida, escolha **Projetos**. Então selecione o item **RouterLib**.  
  
2. Inclua o arquivo de cabeçalho RooterLib em **unittest1.cpp**.  
  
   1.  Abra **unittest1.cpp**.  
  
   2.  Adicione esse código abaixo da linha `#include "CppUnitTest.h"`:  
  
       ```cpp  
       #include "..\RooterLib\RooterLib.h"  
       ```  
  
3. Adicione um teste que use a função importada. Adicione o seguinte código a **unittest1.cpp**:  
  
   ```  
   TEST_METHOD(BasicTest)  
   {  
       CRooterLib rooter;  
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
  
    O novo teste é exibido no Gerenciador de Testes, no nó **Não Executar Testes**.  
  
5. No Gerenciador de Testes, escolha **Executar Todos**.  
  
    ![Teste básico aprovado](../test/media/ute-cpp-testexplorer-basictest.png "UTE_Cpp_TestExplorer_BasicTest")  
  
   Você configurou o teste e os projetos de código, além de ter verificado que pode executar testes que executam funções no projeto de código. Agora, você pode começar a escrever testes e códigos reais.  
  
##  <a name="BKMK_Iteratively_augment_the_tests_and_make_them_pass"></a> Aumentar iterativamente os testes e fazer com que sejam aprovados  
  
1.  Adicione um novo teste:  
  
    ```  
    TEST_METHOD(RangeTest)  
    {  
        CRooterLib rooter;  
        for (double v = 1e-6; v < 1e6; v = v * 3.2)  
        {  
            double expected = v;  
            double actual = rooter.SquareRoot(v*v);  
            double tolerance = expected/1000;  
            Assert::AreEqual(expected, actual, tolerance);  
        }  
    };  
  
    ```  
  
    > [!TIP]
    >  É recomendável não alterar testes que tenham sido aprovados. Em vez disso, adicione um novo teste, atualize o código para que o teste seja aprovado e adicione outro teste, e assim por diante.  
    >   
    >  Quando os usuários alterarem os respectivos requisitos, desabilite os testes que não estejam mais corretos. Escreva novos testes e faça-os funcionar, um por vez, da mesma maneira incremental.  
  
2.  No Gerenciador de Testes, escolha **Executar Todos**.  
  
3.  O teste falhará.  
  
     ![Falha em RangeTest](../test/media/ute-cpp-testexplorer-rangetest-fail.png "UTE_Cpp_TestExplorer_RangeTest_Fail")  
  
    > [!TIP]
    >  Verifique se os testes falham imediatamente após escrevê-los. Isso ajuda a impedir a facilidade de errar ao escrever um teste que nunca falha.  
  
4.  Aprimore o código sob teste para que o novo teste seja aprovado. Adicione o seguinte ao **RooterLib.cpp**:  
  
    ```cpp  
    #include <math.h>  
    ...  
    // Find the square root of a number.  
    double CRooterLib::SquareRoot(double v)  
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
  
5.  Compile a solução e, no Gerenciador de Testes, escolha **Executar Todos**.  
  
     Ambos os testes são aprovados.  
  
> [!TIP]
>  Desenvolva o código adicionando testes, um de cada vez. Verifique se todos os testes passaram após cada iteração.  
  
##  <a name="BKMK_Debug_a_failing_test"></a> Depurar um teste que falhou  
  
1. Adicionar outro teste a **unittest1.cpp**:  
  
   ```  
   // Verify that negative inputs throw an exception.  
    TEST_METHOD(NegativeRangeTest)  
    {  
      wchar_t message[200];  
      CRooterLib rooter;  
      for (double v = -0.1; v > -3.0; v = v - 0.5)  
      {  
        try   
        {  
          // Should raise an exception:  
          double result = rooter.SquareRoot(v);  
  
          swprintf_s(message, L"No exception for input %g", v);  
          Assert::Fail(message, LINE_INFO());  
        }  
        catch (std::out_of_range ex)  
        {  
          continue; // Correct exception.  
        }  
        catch (...)  
        {  
          swprintf_s(message, L"Incorrect exception for %g", v);  
          Assert::Fail(message, LINE_INFO());  
        }  
      }  
   };  
  
   ```  
  
2. No Gerenciador de Testes, escolha **Executar Todos**.  
  
    O teste falhará. Escolha o nome do teste no Gerenciador de Testes. A asserção com falha é realçada. A mensagem de falha fica visível no painel de detalhes do Gerenciador de Testes.  
  
    ![Falha em NegativeRangeTests](../test/media/ute-cpp-testexplorer-negativerangetest-fail.png "UTE_Cpp_TestExplorer_NegativeRangeTest_Fail")  
  
3. Para ver o motivo da falha do teste, percorra a função:  
  
   1.  Defina o ponto de interrupção no início da função `SquareRoot`.  
  
   2.  No menu de atalho do teste com falha, escolha **Depurar Testes Selecionados**.  
  
        Quando a execução for interrompida no ponto de interrupção, percorra o código.  
  
   3.  Adicione código ao **RooterLib.cpp** para capturar a exceção:  
  
       ```  
       #include <stdexcept>  
       ...  
       double CRooterLib::SquareRoot(double v)  
       {  
           //Validate the input parameter:  
           if (v < 0.0)   
           {  
             throw std::out_of_range("Can't do square roots of negatives");  
           }  
       ...  
  
       ```  
  
   1.  No Gerenciador de Testes, escolha **Executar Tudo** para testar o método corrigido e ter certeza de que você não introduziu uma regressão.  
  
   Todos os testes agora foram aprovados.  
  
   ![Todos os testes foram aprovados](../test/media/ute-ult-alltestspass.png "UTE_ULT_AllTestsPass")  
  
##  <a name="BKMK_Refactor_the_code_without_changing_tests"></a> Refatorar o código sem alterar os testes  
  
1.  Simplifique o cálculo central na função `SquareRoot`:  
  
    ```  
    // old code  
    //result = result - (result*result - v)/(2*result);  
    // new code  
    result = (result + v/result) / 2.0;  
  
    ```  
  
2.  Escolha **Executar Tudo** para testar o método refatorado e ter certeza de que você não introduziu uma regressão.  
  
    > [!TIP]
    >  Um conjunto estável de testes de unidade aprovados garante que você não introduziu bugs quando alterou o código.  
    >   
    >  Mantenha a refatoração separada das outras alterações.




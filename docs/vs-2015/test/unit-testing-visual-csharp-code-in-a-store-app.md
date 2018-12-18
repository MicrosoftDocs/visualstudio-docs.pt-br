---
title: Teste de unidade de código Visual C# em um aplicativo da Store | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 23cb0d82-0451-464e-98ea-fa66e7010ead
caps.latest.revision: 21
author: alexhomer1
ms.author: gewarren
manager: robinr
ms.openlocfilehash: ae41a5a646860526cbc5b3f6e3c04bfbf7612e2b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49901548"
---
# <a name="unit-testing-visual-c-code-in-a-store-app"></a>Executar o teste de unidade de um código Visual C# em um aplicativo da Store
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve uma maneira de criar testes de unidade para uma classe Visual C# em um aplicativo da Windows Store. A classe Rooter demonstra memórias vagas da teoria de limite do cálculo implementando uma função que calcula uma estimativa da raiz quadrada de um determinado número. O aplicativo de matemática pode usar essa função para mostrar a um usuário as coisas divertidas que podem ser feitas com a matemática.  
  
 Este tópico demonstra como usar teste de unidade como a primeira etapa do desenvolvimento. Nessa abordagem, primeiramente, você escreve um método de teste que verifique um comportamento específico no sistema que está sendo testado e, em seguida, escreve um código que passe no teste. Ao fazer alterações na ordem dos procedimentos a seguir, é possível reverter essa estratégia para primeiro escrever o código que deseja testar e depois escrever as unidades de teste.  
  
 Este tópico também cria uma única solução do Visual Studio e projetos separados para os testes de unidade e a DLL que você deseja testar. Também é possível incluir os testes de unidade diretamente no projeto de DLL ou criar soluções separadas para os testes de unidade e a DLL.  
  
> [!NOTE]
>  A comunidade do Visual Studio, Enterprise. e Professional fornece recursos adicionais para teste de unidade.  
> 
> - Use um framework de teste de unidade de software livre e de terceiros que tenha criado um adaptador complementar para o gerenciador de testes da Microsoft. Também é possível analisar e exibir informações de cobertura de código para os testes.  
>   -   Execute os testes depois de cada compilação.  
>   -   O VS Enterprise também contém Microsoft Fakes, uma estrutura de isolamento para código gerenciado que ajuda a focar os testes no seu próprio código substituindo o código de teste para funcionalidade do sistema e de terceiros.  
> 
>   Para obter mais informações, confira [Verificação do código usando testes de unidade](http://msdn.microsoft.com/library/dd264975.aspx) na biblioteca MSDN.  
  
##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 [Criar a solução e o projeto de teste de unidade](#BKMK_Create_the_solution_and_the_unit_test_project)  
  
 [Verificar se o testes são executados no Gerenciador de Testes](#BKMK_Verify_that_the_tests_run_in_Test_Explorer)  
  
 [Adição da classe Rooter ao projeto Matemática](#BKMK_Add_the_Rooter_class_to_the_Maths_project)  
  
 [Como acoplar o projeto de teste ao projeto de aplicativo](#BKMK_Couple_the_test_project_to_the_app_project)  
  
 [Multiplicar os testes iterativamente e fazê-los passar](#BKMK_Iteratively_augment_the_tests_and_make_them_pass)  
  
 [Depurar um teste que falhou](#BKMK_Debug_a_failing_test)  
  
 [Como refatorar o código](#BKMK_Refactor_the_code_)  
  
##  <a name="BKMK_Create_the_solution_and_the_unit_test_project"></a> Criar a solução e o projeto de teste de unidade  
  
1.  No menu **Arquivo**, escolha **Novo** e, em seguida, **Novo Projeto**.  
  
2.  Na caixa de diálogo **Novo Projeto**, expanda **Instalado** e, em seguida, expanda **Visual C#** e escolha **Windows Store**. Escolha então **Aplicativo em Branco** na lista de modelos de projeto.  
  
3.  Dê ao projeto o nome `Maths` e verifique se a opção **Criar diretório para a solução** está selecionada.  
  
4.  No Gerenciador de Soluções, escolha o nome da solução, escolha **Adicionar** no menu de atalho e escolha **Novo Projeto**.  
  
5.  Na caixa de diálogo **Novo Projeto**, expanda **Instalado** e **Visual C#** e, em seguida, escolha **Windows Store**. Em seguida, escolha **Biblioteca de Teste de Unidade (aplicativos da Windows Store)** na lista de modelos de projeto.  
  
     ![Crie o projeto de teste de unidade](../test/media/ute-cs-windows-createunittestproject.png "UTE_Cs_windows_CreateUnitTestProject")  
  
6.  Abra UnitTest1.cs no editor do Visual Studio.  
  
    ```csharp  
  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using Microsoft.VisualStudio.TestPlatform.UnitTestFramework;  
    using Maths;  
  
    namespace RooterTests  
    {  
        [TestClass]  
        public class UnitTest1  
  
            [TestMethod]  
            public void TestMethod1()  
            {  
  
            }  
  
    ```  
  
     Observe que:  
  
    1.  Cada teste é definido usando o `[TestMethod]`. Um método de teste deve retornar void e não pode ter nenhum parâmetro.  
  
    2.  Os métodos de teste devem estar em uma classe decorada com o atributo `[TestClass]`.  
  
         Quando os testes são executados, uma instância de cada classe de teste é criada. Os métodos de teste são chamados em uma ordem não especificada.  
  
    3.  Você pode definir métodos especiais que são invocados antes e depois de cada módulo, classe ou método. Para obter mais informações, confira [Como usar membros Microsoft.VisualStudio.TestTools.UnitTesting em testes de unidade](../test/using-microsoft-visualstudio-testtools-unittesting-members-in-unit-tests.md) na biblioteca MSDN.  
  
##  <a name="BKMK_Verify_that_the_tests_run_in_Test_Explorer"></a> Verificar se o testes são executados no Gerenciador de Testes  
  
1.  Insira um código de teste em `TestMethod1` do arquivo **UnitTest1.cs**:  
  
    ```csharp  
  
    [TestMethod]  
    public void TestMethod1()  
    {  
        Assert.AreEqual(0, 0);  
    }  
  
    ```  
  
     Observe que a classe `Assert` fornece vários métodos estáticos que você pode usar para verificar os resultados em métodos de teste.  
  
2.  No menu **Testar**, escolha **Executar** e **Executar Todos**.  
  
     O projeto de teste é compilado e executado. A janela Gerenciador de Testes é exibida e o teste é listado em **Testes Aprovados**. O painel Resumo, na parte inferior da janela, fornece mais detalhes sobre o teste selecionado.  
  
     ![Gerenciador de testes](../test/media/ute-cpp-testexplorer-testmethod1.png "UTE_Cpp_TestExplorer_TestMethod1")  
  
##  <a name="BKMK_Add_the_Rooter_class_to_the_Maths_project"></a> Adição da classe Rooter ao projeto Matemática  
  
1.  No Gerenciador de Soluções, escolha o nome do projeto **Matemática**. Do menu de atalho, escolha **Adicionar** e, então, **Classe**.  
  
2.  Nomeie o arquivo de classe `Rooter.cs`  
  
3.  Adicione o código a seguir ao arquivo **Rooter.cs** da classe Rooter:  
  
    ```csharp  
  
    public Rooter()  
    {  
    }  
  
    // estimate the square root of a number  
    public double SquareRoot(double x)  
    {  
        return 0.0;  
    }  
  
    ```  
  
     A classe `Rooter` declara um construtor e o método avaliador `SqareRoot`.  
  
4.  O método `SqareRoot` é apenas uma implementação mínima, suficiente para testar a estrutura básica da configuração de teste.  
  
##  <a name="BKMK_Couple_the_test_project_to_the_app_project"></a> Como acoplar o projeto de teste ao projeto de aplicativo  
  
1. Adicione uma referência ao aplicativo Matemática para o projeto RooterTests.  
  
   1.  No Gerenciador de Soluções, escolha o projeto **RooterTests** e, em seguida, escolha **Adicionar Referência...** no menu de atalho.  
  
   2.  Na caixa de diálogo **Adicionar Referência - RooterTests**, expanda **Solução** e escolha **Projetos**. Então, selecione o item **Matemática**.  
  
        ![Adicione uma referência ao projeto Matemática](../test/media/ute-cs-windows-addreference.png "UTE_Cs_windows_AddReference")  
  
2. Adicione uma instrução Using ao arquivo UnitTest1.cs:  
  
   1.  Abra **UnitTest1.cs**.  
  
   2.  Adicione esse código abaixo da linha `using Microsoft.VisualStudio.TestPlatform.UnitTestFramework;`:  
  
       ```csharp  
       using Maths;  
       ```  
  
3. Adicione um teste que use a função Rooter. Adicione o seguinte código a **UnitTest1.cpp**:  
  
   ```csharp  
   [TestMethod]  
   public void BasicTest()  
   {  
       Maths.Rooter rooter = new Rooter();  
       double expected = 0.0;  
       double actual = rooter.SquareRoot(expected * expected);  
       double tolerance = .001;  
       Assert.AreEqual(expected, actual, tolerance);  
   }  
  
   ```  
  
4. Compile a solução.  
  
    O novo teste é exibido no Gerenciador de Testes, no nó **Não Executar Testes**.  
  
5. No Gerenciador de Testes, escolha **Executar Todos**.  
  
    ![Teste básico aprovado](../test/media/ute-cpp-testexplorer-basictest.png "UTE_Cpp_TestExplorer_BasicTest")  
  
   Você configurou o teste e os projetos de código, além de ter verificado que pode executar testes que executam funções no projeto de código. Agora, você pode começar a escrever testes e códigos reais.  
  
##  <a name="BKMK_Iteratively_augment_the_tests_and_make_them_pass"></a> Aumentar iterativamente os testes e fazer com que sejam aprovados  
  
1.  Adicione um novo teste:  
  
    ```csharp  
    [TestMethod]  
    public void RangeTest()  
    {  
        Rooter rooter = new Rooter();  
        for (double v = 1e-6; v < 1e6; v = v * 3.2)  
        {  
            double expected = v;  
            double actual = rooter.SquareRoot(v*v);  
            double tolerance = ToleranceHelper(expected);  
            Assert.AreEqual(expected, actual, tolerance);  
        }  
    }  
  
    ```  
  
    > [!TIP]
    >  É recomendável não alterar testes que tenham sido aprovados. Em vez disso, adicione um novo teste, atualize o código para que o teste seja aprovado e adicione outro teste, e assim por diante.  
    >   
    >  Quando os usuários alterarem os respectivos requisitos, desabilite os testes que não estejam mais corretos. Escreva novos testes e faça-os funcionar, um por vez, da mesma maneira incremental.  
  
2.  No Gerenciador de Testes, escolha **Executar Todos**.  
  
3.  O teste falhará.  
  
     ![Falha em RangeTest](../test/media/ute-cpp-testexplorer-rangetest-fail.png "UTE_Cpp_TestExplorer_RangeTest_Fail")  
  
    > [!TIP]
    >  Logo após escrevê-los, verifique se cada um deles falha. Isso ajuda a impedir a facilidade de errar ao escrever um teste que nunca falha.  
  
4.  Aprimore o código sob teste para que o novo teste seja aprovado. Altere a função `SqareRoot` em **Rooter.cs** para:  
  
    ```csharp  
    public double SquareRoot(double x)  
    {  
        double estimate = x;  
        double diff = x;  
        while (diff > estimate / 1000)  
        {  
            double previousEstimate = estimate;  
            estimate = estimate - (estimate * estimate - x) / (2 * estimate);  
            diff = Math.Abs(previousEstimate - estimate);  
        }  
        return estimate;  
    }  
  
    ```  
  
5.  Compile a solução e, no Gerenciador de Testes, escolha **Executar Todos**.  
  
     Os três testes agora foram aprovados.  
  
> [!TIP]
>  Desenvolva o código adicionando testes, um de cada vez. Verifique se todos os testes passaram após cada iteração.  
  
##  <a name="BKMK_Debug_a_failing_test"></a> Depurar um teste que falhou  
  
1. Adicione outro teste a **UnitTest1.cs**:  
  
   ```csharp  
   // Verify that negative inputs throw an exception.  
   [TestMethod]  
   public void NegativeRangeTest()  
   {  
       string message;  
       Rooter rooter = new Rooter();  
       for (double v = -0.1; v > -3.0; v = v - 0.5)  
       {  
           try  
           {  
               // Should raise an exception:  
               double actual = rooter.SquareRoot(v);  
  
               message = String.Format("No exception for input {0}", v);  
               Assert.Fail(message);  
           }  
           catch (ArgumentOutOfRangeException ex)  
           {  
               continue; // Correct exception.  
           }  
           catch (Exception e)  
           {  
               message = String.Format("Incorrect exception for {0}", v);  
               Assert.Fail(message);  
           }  
       }  
   }  
  
   ```  
  
2. No Gerenciador de Testes, escolha **Executar Todos**.  
  
    O teste falhará. Escolha o nome do teste no Gerenciador de Testes. A asserção com falha é realçada. A mensagem de falha fica visível no painel de detalhes do Gerenciador de Testes.  
  
    ![Falha em NegativeRangeTests](../test/media/ute-cpp-testexplorer-negativerangetest-fail.png "UTE_Cpp_TestExplorer_NegativeRangeTest_Fail")  
  
3. Para ver o motivo da falha do teste, percorra a função:  
  
   1.  Defina o ponto de interrupção no início da função `SquareRoot`.  
  
   2.  No menu de atalho do teste com falha, escolha **Depurar Testes Selecionados**.  
  
        Quando a execução for interrompida no ponto de interrupção, percorra o código.  
  
   3.  Adicione o código ao método Rooter para capturar a exceção:  
  
       ```csharp  
       public double SquareRoot(double x)  
       {  
           if (x < 0.0)  
           {  
               throw new ArgumentOutOfRangeException();  
       }  
  
       ```  
  
   1.  No Gerenciador de Testes, escolha **Executar Tudo** para testar o método corrigido e ter certeza de que você não introduziu uma regressão.  
  
   Todos os testes agora foram aprovados.  
  
   ![Todos os testes foram aprovados](../test/media/ute-ult-alltestspass.png "UTE_ULT_AllTestsPass")  
  
##  <a name="BKMK_Refactor_the_code_"></a> Como refatorar o código  
 **Simplifique o cálculo central na função SquareRoot.**  
  
1.  Altere a implementação do resultado  
  
    ```csharp  
    // old code  
    //result = result - (result*result - v)/(2*result);  
    // new code  
    result = (result + v/result) / 2.0;  
  
    ```  
  
2.  Escolha **Executar Tudo** para testar o método refatorado e ter certeza de que você não introduziu uma regressão.  
  
> [!TIP]
>  Um conjunto estável de testes de unidade aprovados garante que você não introduziu bugs quando alterou o código.  
  
 **Refatore o código de teste para eliminar o código duplicado.**  
  
 Observe que o método `RangeTest` não embute em código o denominador da variável de tolerância que é usado no método `Assert`. Se você pretende adicionar testes extras que usem o mesmo cálculo de tolerância, o uso de um valor embutido em código em vários locais poderá resultar em erros.  
  
1.  Adicione um método privado à classe Unit1Test para calcular o valor de tolerância e chame esse método.  
  
    ```csharp  
    private double ToleranceHelper(double expected)  
    {  
        return expected / 1000;  
    }  
  
    ...  
  
    [TestMethod]  
    public void RangeTest()  
    {  
        ...  
        // old code  
        // double tolerance = expected/1000;  
        // new code  
        double tolerance = ToleranceHelper(expected);  
        Assert.AreEqual(expected, actual, tolerance);  
    }  
    ...  
  
    ```  
  
2.  Escolha **Executar Tudo** para testar o método refatorado e verifique se você não introduziu um erro.  
  
> [!NOTE]
>  Para adicionar um método auxiliar a uma classe de teste, não adicione o atributo `[TestMethod]` ao método. O Gerenciador de Testes não registra o método a ser executado.




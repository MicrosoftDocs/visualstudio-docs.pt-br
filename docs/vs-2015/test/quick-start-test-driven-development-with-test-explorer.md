---
title: 'Início Rápido: desenvolvimento orientado por testes com Gerenciador de Testes | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5161b533-2127-4172-b473-d4ffc76ff05b
caps.latest.revision: 17
ms.author: gewarren
manager: douge
ms.openlocfilehash: a67f4f79688cb4cdbe482c90cd93b784349d748a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49831686"
---
# <a name="quick-start-test-driven-development-with-test-explorer"></a>Início rápido: desenvolvimento orientado por testes com o Gerenciador de Testes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É recomendável que você crie testes de unidade para ajudar a manter seu código funcionando corretamente muitas etapas incrementais de desenvolvimento. Há várias estruturas que você pode usar para escrever testes de unidade, incluindo alguns desenvolvidos por terceiros. Algumas estruturas de teste são especializadas para testes em diferentes idiomas ou plataformas. O Gerenciador de Testes fornece uma interface única para testes de unidade em qualquer uma dessas estruturas. Adaptadores estão disponíveis para as estruturas comumente usadas e você pode escrever seus próprios adaptadores para outras estruturas.  
  
 O Gerenciador de Testes substitui as janelas de teste de unidade encontradas em edições anteriores do Visual Studio. Suas vantagens incluem:  
  
-   Executar o .NET, não gerenciado, o banco de dados e outros tipos de testes usando uma única interface.  
  
-   Use a estrutura de teste de unidade de sua escolha, como NUnit ou MSTest estruturas.  
  
-   Consulte todas as informações que você precisa em uma janela.  
  
## <a name="using-test-explorer"></a>Usando o Gerenciador de Testes  
 ![Gerenciador de Testes de unidade mostrando o Botão Executar Todos](../test/media/unittestexplorer-beta.png "UnitTestExplorer(beta)")  
  
#### <a name="to-run-unit-tests-by-using-test-explorer"></a>Para executar testes de unidade usando o Gerenciador de Testes  
  
1. Crie testes de unidade que usam as estruturas de teste de sua escolha.  
  
    Por exemplo, para criar um teste que usa a estrutura MSTest:  
  
   1.  Criar um projeto de teste.  
  
        Na caixa de diálogo **Novo Projeto**, expanda **Visual Basic**, **Visual C#** ou **Visual C++** e escolha **Teste**.  
  
        Selecione **Projeto de teste de unidade**.  
  
   2.  Grave cada teste de unidade como um método. Prefixe cada método de teste com o atributo `[TestMethod]`.  
  
2. Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo com o botão de alternância ![UTE&#95;parallelicon&#45;small](../test/media/ute-parallelicon-small.png "UTE_parallelicon-small") na barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.  
  
3. Na barra de menus, escolha **Teste**, **Executar testes de unidade**, **Todos os testes**.  
  
    A solução é criada e os testes são executados.  
  
    O Gerenciador de Testes abre e exibe um resumo dos resultados.  
  
   **Para ver uma lista completa de testes,** escolha **Mostrar Tudo** em qualquer categoria.  
  
   **Para ver os detalhes de um resultado do teste:** selecione o teste no Gerenciador de Testes para exibir detalhes como mensagens de exceção no painel de detalhes.  
  
   **Para navegar para o código de um teste,** clique duas vezes no teste no Gerenciador de Testes ou escolha **Abrir Teste** no menu de atalho.  
  
   **Para depurar um teste,** abra o menu de atalho para um ou mais testes e escolha **Depurar Testes Selecionados**.  
  
> [!IMPORTANT]
>  Os resultados que são exibidos são para as execuções mais recentes. A barra colorida de resultados mostra somente os resultados dos testes que foram executados. Por exemplo, se você executar vários testes e alguns deles falharem e executar apenas os testes com sucesso, a barra de resultados mostrará todos na cor verde.  
  
> [!NOTE]
>  Se nenhum teste for exibido, certifique-se de que você tenha instalado um adaptador para conectar o Gerenciador de Testes a estruturas de teste que você está usando. Para obter mais informações, consulte [Usando diferentes estruturas de teste com o Gerenciador de Testes](#frameworks).  
  
##  <a name="walkthrough"></a> Passo a passo: Usando testes de unidade para desenvolver um método  
 Este passo a passo demonstra como desenvolver um método testado em C# usando a estrutura de teste de unidade da Microsoft. Você pode adaptá-lo facilmente para outros idiomas e usar outras estruturas de teste como NUnit. Para obter mais informações, consulte [Usando diferentes estruturas de teste](#frameworks).  
  
#### <a name="creating-the-test-and-method"></a>Criando o teste e o método  
  
1. Crie um projeto de biblioteca de classes do Visual C#. Esse projeto conterá o código que queremos fornecer. Neste exemplo, o nome usado é `MyMath`.  
  
2. Criar um projeto de teste.  
  
   -   Na caixa de diálogo **Novo Projeto**, escolha **Visual C#**, **Teste** e escolha **Projeto de Teste de Unidade**.  
  
        ![Novos projetos de código e teste](../test/media/unittestexplorerwalk1.png "UnitTestExplorerWalk1")  
  
3. Escreva um método de teste básico. Verifique o resultado obtido para uma entrada específica:  
  
   ```csharp  
  
   [TestMethod]  
   public void BasicRooterTest()  
   {  
     // Create an instance to test:  
     Rooter rooter = new Rooter();  
     // Define a test input and output value:  
     double expectedResult = 2.0;  
     double input = expectedResult * expectedResult;  
     // Run the method under test:  
     double actualResult = rooter.SquareRoot(input);  
     // Verify the result:  
     Assert.AreEqual(expectedResult, actualResult,  
         delta: expectedResult / 100);  
   }  
   ```  
  
4. Gere o método do teste.  
  
   1.  Coloque o cursor em `Rooter`, em seguida, no menu de atalho, escolha **Gerar**, **Novo Tipo**.  
  
   2.  Na caixa de diálogo **Gerar Novo Tipo**, defina **Projeto** para o projeto de biblioteca de classes. Neste exemplo, é `MyMath`.  
  
   3.  Coloque o cursor em `SquareRoot`, em seguida, no menu de atalho, escolha **Gerar**, **Stub do método**.  
  
5. Execute o teste de unidade.  
  
   1.  No menu **Teste**, escolha **Executar Testes de Unidade**, **Todos os Testes**.  
  
        A solução é criada e executada.  
  
        O Gerenciador de Testes abre e exibe os resultados.  
  
        Se um teste aparecer sob **Testes com Falha**.  
  
6. Selecione o nome do teste.  
  
    Os detalhes do teste são exibidos na parte inferior do Gerenciador de Testes.  
  
7. Selecione os itens em **Rastreamento de pilha** para ver onde o teste falhou.  
  
   ![Gerenciador de Testes de unidade mostrando teste com falha.](../test/media/unittestexplorerwalkthrough2.png "UnitTestExplorerWalkthrough2")  
  
   Neste ponto, você criou um teste e um stub que você modificará para que o teste seja aprovado.  
  
#### <a name="after-every-change-make-all-the-tests-pass"></a>Após cada alteração, faça todos os testes serem aprovados  
  
1.  Em `MyMath\Rooter.cs`, aprimore o código de `SquareRoot`:  
  
    ```csharp  
    public double SquareRoot(double input)  
     {  
       return input / 2;  
     }  
    ```  
  
2.  No Gerenciador de Testes, escolha **Executar Todos**.  
  
     Compila o código e o teste é executado.  
  
     O teste é aprovado.  
  
     ![Gerenciador de Testes de unidade mostrando teste com aprovação.](../test/media/unittestexplorerwalkthrough3.png "UnitTestExplorerWalkthrough3")  
  
#### <a name="add-tests-to-extend-the-range-of-inputs"></a>Adicionar testes para estender o intervalo de entradas  
  
1.  Para aumentar sua confiança que seu código funciona em todos os casos, adicione os testes que tente uma variedade maior de valores de entrada.  
  
    > [!TIP]
    >  Evite alterar testes existentes que foram aprovados. Em vez disso, adicione novos testes. Altere os testes existentes somente quando os requisitos de usuário forem alterados. Essa política ajuda a garantir que você não perde a funcionalidade existente enquanto você trabalha para estender o código.  
  
     Na classe de teste, adicione o seguinte teste, que tenta um intervalo de valores de entrada:  
  
    ```csharp  
    [TestMethod]  
    public void RooterValueRange()  
    {  
      // Create an instance to test:  
      Rooter rooter = new Rooter();  
      // Try a range of values:  
      for (double expectedResult = 1e-8;  
          expectedResult < 1e+8;  
          expectedResult = expectedResult * 3.2)  
      {  
        RooterOneValue(rooter, expectedResult);  
      }  
    }  
  
    private void RooterOneValue(Rooter rooter, double expectedResult)  
    {  
      double input = expectedResult * expectedResult;  
      double actualResult = rooter.SquareRoot(input);  
      Assert.AreEqual(expectedResult, actualResult,  
          delta: expectedResult / 1000);  
    }  
    ```  
  
2.  No Gerenciador de Testes, escolha **Executar Todos**.  
  
     O novo teste falha, embora o primeiro teste ainda seja aprovado.  
  
     Para localizar o ponto de falha, selecione o teste com falha e, em seguida, na parte inferior do Gerenciador de Testes, selecione o item superior do **Rastreamento de pilha**.  
  
3.  Inspecione o método sob teste para ver o que pode estar errado. Na classe `MyMath.Rooter`, reescreva o código:  
  
    ```  
    public double SquareRoot(double input)  
    {  
      double result = input;  
      double previousResult = -input;  
      while (Math.Abs(previousResult - result) > result / 1000)  
      {  
        previousResult = result;  
        result = result - (result * result - input) / (2 * result);  
      }  
      return result;  
    }  
    ```  
  
4.  No Gerenciador de Testes, escolha **Executar Todos**.  
  
     Ambos os testes agora foram aprovados.  
  
#### <a name="add-tests-for-exceptional-cases"></a>Adicionar testes para casos excepcionais  
  
1.  Adicione um teste para entradas negativas:  
  
    ```csharp  
    [TestMethod]  
     public void RooterTestNegativeInputx()  
     {  
         Rooter rooter = new Rooter();  
         try  
         {  
             rooter.SquareRoot(-10);  
         }  
         catch (ArgumentOutOfRangeException e)  
         {  
             return;  
         }  
         Assert.Fail();  
     }  
    ```  
  
2.  No Gerenciador de Testes, escolha **Executar Todos**.  
  
     O método sob teste é executado em loop e deve ser cancelado manualmente.  
  
3.  Escolha **Cancelar**.  
  
     O teste para após 10 segundos.  
  
4.  Corrija o código do método:  
  
    ```csharp  
  
    public double SquareRoot(double input)  
    {  
      if (input <= 0.0)   
      {  
        throw new ArgumentOutOfRangeException();  
      }   
    ...  
    ```  
  
5.  No Gerenciador de Testes, escolha **Executar Todos**.  
  
     Dessa vez os testes são aprovados.  
  
#### <a name="refactor-without-changing-tests"></a>Faça refatoração sem alterar os testes  
  
1.  Simplifique o código, mas não altere os testes.  
  
    > [!TIP]
    >  Uma *refatoração* é uma alteração que é destinada para fazer o código funcionar melhor ou para tornar o código mais fácil de entender. Não deve alterar o comportamento do código e, portanto, os testes não são alterados.  
    >   
    >  É recomendável que você execute etapas de refatoração separadamente das etapas que estendem a funcionalidade. Manter os testes inalterados proporciona confiança que você não acidentalmente introduziu bugs durante a refatoração.  
  
    ```csharp  
    public class Rooter  
    {  
      public double SquareRoot(double input)  
      {  
        if (input <= 0.0)   
        {  
          throw new ArgumentOutOfRangeException();  
        }  
        double result = input;  
        double previousResult = -input;  
        while (Math.Abs(previousResult - result) > result / 1000)  
        {  
          previousResult = result;  
          result = (result + input / result) / 2;  
          //was: result = result - (result * result - input) / (2*result);  
        }  
        return result;  
      }  
    }  
    ```  
  
2.  Escolha **Executar Todos**.  
  
     Todos os testes ainda são aprovados.  
  
     ![Gerenciador de Testes de unidade mostrando 3 testes com aprovação.](../test/media/unittestexplorerwalkthrough4.png "UnitTestExplorerWalkthrough4")




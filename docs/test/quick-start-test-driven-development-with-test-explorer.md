---
title: Passo a passo de desenvolvimento controlado por teste
description: Saiba como desenvolver um método testado em C# usando o Microsoft Test Framework, que você pode adaptar facilmente a outras linguagens ou estruturas de teste, como o NUnit.
ms.custom: SEO-VS-2020
ms.date: 07/24/2019
ms.topic: conceptual
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 294c99081668baa2ed19df00989ceac768979481
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683947"
---
# <a name="walkthrough-test-driven-development-using-test-explorer"></a>Walkthrough: desenvolvimento orientado por testes usando o Gerenciador de testes

Crie testes de unidade para ajudar a manter seu código funcionando corretamente por meio de alterações de código incrementais. Há várias estruturas que você pode usar para escrever testes de unidade, incluindo alguns desenvolvidos por terceiros. Algumas estruturas de teste são especializadas para testes em diferentes idiomas ou plataformas. O Gerenciador de Testes fornece uma interface única para testes de unidade em qualquer uma dessas estruturas. Para saber mais sobre como usar o **Gerenciador de Testes**, confira [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md) e [Perguntas Frequentes do Gerenciador de Testes](test-explorer-faq.md).

Este passo a passo demonstra como desenvolver um método testado em C# usando a MSTest (estrutura de teste da Microsoft). Você pode adaptá-lo facilmente para outros idiomas e usar outras estruturas de teste como a NUnit. Para obter mais informações, consulte [instalar estruturas de teste de unidade de](install-third-party-unit-test-frameworks.md)terceiros.

## <a name="create-a-test-and-generate-code"></a>Criar um teste e gerar código

1. Crie um projeto de **Biblioteca de Classes (.NET Standard)** do C#. Esse projeto conterá o código que queremos testar. Nomeie o projeto **MyMath**.

2. Na mesma solução, adicione um novo projeto de teste MSTest.

   A partir do Visual Studio 2019 versão 16,9, o nome do modelo de projeto MSTest alterado de **MSTest Test Project (.NET Core)** para o **projeto de teste de unidade**.

   Nomeie esse projeto de teste **MathTests**.

   ![Novos projetos de teste e código](../test/media/test-driven-development-ide.png)

3. Escreva um método de teste simples que verifique o resultado obtido para uma entrada específica. Adicione o código a seguir à classe `UnitTest1`:

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
     Assert.AreEqual(expectedResult, actualResult, delta: expectedResult / 100);
   }
   ```

4. Gere um tipo com base no código de teste.

   1. Coloque o cursor sobre `Rooter` e, no menu de lâmpada, escolha **gerar tipo ' raiz '**  >  **gerar novo tipo**.

      ![Ação rápida Gerar novo tipo](media/test-driven-development-generate-new-type.png)

   2. Na caixa de diálogo **Gerar Tipo**, defina **Projeto** para **MyMath**, o projeto de biblioteca de classes, depois escolha **OK**.

      ![Caixa de diálogo Gerar Tipo no Visual Studio 2019](media/test-driven-development-generate-type-dialog.png)

5. Gere um método com base no código de teste. Coloque o cursor sobre `SquareRoot` e, no menu de lâmpada, escolha **Gerar método 'Rooter.SquareRoot'**.

6. Execute o teste de unidade.

   1. Para abrir o **Gerenciador de Testes**, no menu **Teste**, escolha **Windows** > **Gerenciador de Testes**.

   2. No **Gerenciador de Testes**, escolha o botão **Executar Todos** para executar o teste.

   A solução é compilada, o teste é executado e falha.

7. Selecione o nome do teste.

   Os detalhes do teste aparecem no painel **Resumo dos Detalhes do Teste**.

   ![Resumo dos Detalhes do Teste no Gerenciador de Testes](media/test-driven-development-test-detail-summary.png)

8. Selecione o link superior em **Rastreamento de Pilha** para ir para o local em que o teste falhou.

Neste ponto, você criou um teste e um stub que você pode modificar para que o teste seja aprovado.

## <a name="verify-a-code-change"></a>Verificar uma alteração de código

1. No arquivo *Class1.cs*, melhore o código de `SquareRoot`:

    ```csharp
    public double SquareRoot(double input)
    {
        return input / 2;
    }
    ```

2. No **Gerenciador de Testes**, escolha **Executar Todos**.

   A solução é compilada, o teste é executado e passa.

   ![Gerenciador de Testes mostrando teste aprovado](../test/media/test-driven-development-passed-test.png)

## <a name="extend-the-range-of-inputs"></a>Estender o intervalo de entradas

Para aumentar nossa confiança que o código funciona em todos os casos, adicione testes que experimentem uma variedade maior de valores de entrada.

> [!TIP]
> Evite alterar testes existentes que foram aprovados. Em vez disso, adicione novos testes. Altere os testes existentes somente quando os requisitos de usuário forem alterados. Essa política ajuda a garantir que você não perca a funcionalidade existente enquanto trabalha para estender o código.

1. Na classe de teste, adicione o teste a seguir, que experimenta um intervalo de valores de entrada:

    ```csharp
    [TestMethod]
    public void RooterValueRange()
    {
        // Create an instance to test.
        Rooter rooter = new Rooter();

        // Try a range of values.
        for (double expected = 1e-8; expected < 1e+8; expected *= 3.2)
        {
            RooterOneValue(rooter, expected);
        }
    }

    private void RooterOneValue(Rooter rooter, double expectedResult)
    {
        double input = expectedResult * expectedResult;
        double actualResult = rooter.SquareRoot(input);
        Assert.AreEqual(expectedResult, actualResult, delta: expectedResult / 1000);
    }
    ```

2. No **Gerenciador de Testes**, escolha **Executar Todos**.

   O novo teste falha, embora o primeiro teste ainda tenha sido aprovado. Para encontrar o ponto de falha, selecione o teste com falha e examine os detalhes no painel **Resumo dos Detalhes do Teste**.

3. Inspecione o método sob teste para ver o que pode estar errado. Altere o código `SquareRoot` conforme demonstrado a seguir:

    ```csharp
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

4. No **Gerenciador de Testes**, escolha **Executar Todos**.

   Ambos os testes agora foram aprovados.

## <a name="add-tests-for-exceptional-cases"></a>Adicionar testes para casos excepcionais

1. Adicione um novo teste para entradas negativas:

    ```csharp
    [TestMethod]
    public void RooterTestNegativeInputx()
    {
        Rooter rooter = new Rooter();
        try
        {
            rooter.SquareRoot(-10);
        }
        catch (System.ArgumentOutOfRangeException)
        {
            return;
        }
        Assert.Fail();
    }
    ```

2. No **Gerenciador de Testes**, escolha **Executar Todos**.

   O método sob teste é executado em loop e deve ser cancelado manualmente.

3. Escolha **Cancelar** na barra de ferramentas do **Gerenciador de Testes**.

   A execução do teste é interrompida.

4. Corrija o código `SquareRoot` adicionando a seguinte instrução `if` no início do método:

    ```csharp
    public double SquareRoot(double input)
    {
        if (input <= 0.0)
        {
            throw new ArgumentOutOfRangeException();
        }
        ...
    ```

5. No **Gerenciador de Testes**, escolha **Executar Todos**.

   Dessa vez os testes são aprovados.

## <a name="refactor-the-code-under-test"></a>Refatorar o código em teste

Refatore o código, mas não altere os testes.

> [!TIP]
> Uma *refatoração* é uma alteração que é destinada para fazer o código funcionar melhor ou torná-lo mais fácil de entender. Não deve alterar o comportamento do código e, portanto, os testes não são alterados.
>
> É recomendável que você execute etapas de refatoração separadamente das etapas que estendem a funcionalidade. Manter os testes inalterados proporciona confiança que você não acidentalmente introduziu bugs durante a refatoração.

1. Altere a linha que calcula `result` no método `SquareRoot` da seguinte maneira:

    ```csharp
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
    ```

2. Escolha **Executar Tudo** e verifique se todos os testes ainda são aprovados.

   ![O Gerenciador de Testes mostrando três testes aprovados](../test/media/test-driven-development-three-passed-tests.png)

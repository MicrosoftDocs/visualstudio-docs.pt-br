---
title: Introdução ao teste de unidade
description: Use o Visual Studio para definir e executar testes de unidade para manter a integridade do código e para encontrar erros e falhas antes que seus clientes façam.
ms.custom: SEO-VS-2020
ms.date: 04/07/2020
ms.topic: tutorial
helpviewer_keywords:
- unit testing, create unit test plans
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1e1576f8865fc5945514ce6965cdba66a1cfda55
ms.sourcegitcommit: 3985d0ae8d6332f4682c82a10897763173d52961
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107386044"
---
# <a name="get-started-with-unit-testing"></a>Introdução ao teste de unidade

Use o Visual Studio para definir e executar testes de unidade para manter a integridade de código, assegurar a cobertura de código e localizar erros e falhas antes de seus clientes. Execute os testes de unidade frequentemente para ter certeza de que seu código está funcionando corretamente.

Neste artigo, o código e as ilustrações usam C#, mas os conceitos e recursos se aplicam às linguagens .NET, C++, Python, JavaScript e TypeScript.

## <a name="create-unit-tests"></a>Criar testes de unidade

Esta seção descreve como criar um projeto de teste de unidade.

1. Abra o projeto que você deseja testar no Visual Studio.

   Para fins de demonstração de um exemplo de teste de unidade, este artigo testa um projeto C# "Olá, Mundo" simples chamado **HelloWorldCore**. O código do exemplo para um projeto desse tipo é o seguinte:

   ```csharp
   namespace HelloWorldCore

      public class Program
      {
         public static void Main()
         {
            Console.WriteLine("Hello World!");
         }
      }
   ```

1. No **Gerenciador de Soluções**, selecione o nó da solução. Em seguida, na barra de menus superior, selecione **arquivo**  >  **Adicionar**  >  **novo projeto**.

1. Na caixa de diálogo novo projeto, localize um modelo de projeto de teste de unidade para a estrutura de teste que você deseja usar, como MSTest e selecione-o.

   A partir do Visual Studio 2017 versão 14,8, as linguagens .NET incluem modelos internos para NUnit e xUnit. Para o C++, você precisará selecionar uma estrutura de teste com suporte no idioma. Para o Python, consulte [Configurar o teste de unidade no código Python](../python/unit-testing-python-in-visual-studio.md) para configurar seu projeto de teste.

   > [!TIP]
   > Para o C#, você pode criar projetos de teste de unidade a partir do código usando um método mais rápido. Para obter mais informações, consulte [criar projetos de teste de unidade e métodos de teste](../test/unit-test-basics.md#create-unit-test-projects-and-test-methods). Para usar esse método com .NET Core ou .NET Standard, o Visual Studio 2019 é necessário.

   A ilustração a seguir mostra um teste de unidade MSTest, que tem suporte no .NET.

   ::: moniker range=">=vs-2019"

   ![Modelo de projeto de teste de unidade no Visual Studio 2019](media/vs-2019/add-new-test-project.png)

   Clique em **Avançar**, escolha um nome para o projeto de teste e, em seguida, clique em **Criar**.

   ::: moniker-end

   ::: moniker range="vs-2017"

   ![Modelo de projeto de teste de unidade no Visual Studio 2019](media/mstest-test-project-template.png)

   Escolha um nome para o projeto de teste, como HelloWorldTests e clique em **OK**.

   ::: moniker-end

   O projeto é adicionado à solução.

   ![Projeto de teste de unidade no Gerenciador de Soluções](media/vs-2019/solution-explorer.png)

1. No projeto de teste de unidade, adicione uma referência ao projeto que você deseja testar clicando com o botão direito do mouse em **Referências** ou **Dependências** e, em seguida, escolhendo **Adicionar Referência**.

1. Selecione o projeto que contém o código que você testará e clique em **OK**.

   ![Adicionar referência de projeto no Visual Studio](media/vs-2019/reference-manager.png)

1. Adicione código ao método de teste de unidade.

   Por exemplo, você pode usar o código a seguir selecionando a guia de documentação correta que corresponde à estrutura de teste: MSTest, NUnit ou xUnit (com suporte somente no .NET).

   ### <a name="mstest"></a>[MSTest](#tab/mstest)

   ```csharp
   using Microsoft.VisualStudio.TestTools.UnitTesting;
   using System.IO;
   using System;

   namespace HelloWorldTests
   {
      [TestClass]
      public class UnitTest1
      {
         private const string Expected = "Hello World!";
         [TestMethod]
         public void TestMethod1()
         {
            using (var sw = new StringWriter())
            {
               Console.SetOut(sw);
               HelloWorldCore.Program.Main();

               var result = sw.ToString().Trim();
               Assert.AreEqual(Expected, result);
            }
         }
      }
   }
   ```

   ### <a name="nunit"></a>[NUnit](#tab/nunit)

   ```csharp
   using NUnit.Framework;
   using System.IO;
   using System;

   namespace HelloWorldTests
   {
      public class Tests
      {
         private const string Expected = "Hello World!";

         [SetUp]
         public void Setup()
         {
         }
         [Test]
         public void TestMethod1()
         {
            using (var sw = new StringWriter())
            {
               Console.SetOut(sw);
               HelloWorldCore.Program.Main();

               var result = sw.ToString().Trim();
               Assert.AreEqual(Expected, result);
            }
         }
      }
   }
   ```

    ### <a name="xunit"></a>[xUnit](#tab/xunit)

    ```csharp
    using System;
    using Xunit;
    using System.IO;
    
    namespace HelloWorldTests
    {
        public class UnitTest1
        {
            private const string Expected = "Hello World!";
            [Fact]
            public void Test1()
            {
                using (var sw = new StringWriter())
                {
                    Console.SetOut(sw);
                    HelloWorldCore.Program.Main();
    
                    var result = sw.ToString().Trim();
                    Assert.Equal(Expected, result);
                }
            }
        }
    }
    ```

    ---

## <a name="run-unit-tests"></a>Executar testes de unidade

1. Abra o [Gerenciador de testes](../test/run-unit-tests-with-test-explorer.md).

   ::: moniker range=">=vs-2019"
   Para abrir o Gerenciador de testes, escolha **testar** > **Gerenciador** de testes na barra de menus superior (ou pressione **Ctrl** + **E**, **T**).
   ::: moniker-end
   ::: moniker range="vs-2017"
   Para abrir o Gerenciador de testes, escolha **testar** o >  > **Gerenciador de testes** do Windows na barra de menus superior.
   ::: moniker-end

1. Execute os testes de unidade clicando em **executar tudo** (ou pressione **Ctrl**  +  **R**, **V**).

   ![Executar testes de unidade no Gerenciador de Testes](media/vs-2019/test-explorer-run-all.png)

   Depois de concluir os testes, uma marca de seleção verde indica que houve aprovação em um teste. Um ícone "x" vermelho indica falha em um teste.

   ![Examine os resultados de teste de unidade no Gerenciador de Testes](media/vs-2019/unit-test-passed.png)

> [!TIP]
> Você pode usar o [Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md) para executar testes de unidade do framework de testes interno (MSTest) ou de estruturas de teste de terceiros. Você pode agrupar os testes em categorias, filtrar a lista de testes, criar, salvar e executar playlists de testes. Você também pode depurar testes e analisar um teste de desempenho e cobertura de código.

## <a name="view-live-unit-test-results-visual-studio-enterprise"></a>Exibir resultados de teste de unidade em tempo real (Visual Studio Enterprise)

Se estiver usando a estrutura de teste do MSTest, do xUnit ou do NUnit no Visual Studio de 2017 ou posterior, você poderá ver os resultados em tempo real de seus testes de unidade.

> [!NOTE]
> Para seguir essas etapas, Visual Studio Enterprise é necessário.

1. Ative o Live Unit Testing do menu **Teste**, escolhendo **Teste** > **Live Unit Testing** > **Iniciar**.

   ::: moniker range="vs-2017"

   ![Ativar o teste de unidade em tempo real](media/live-test-results-start.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Iniciar o Live Unit Testing no Visual Studio 2019](media/vs-2019/start-live-unit-testing.png)

   ::: moniker-end

1. Exiba os resultados dos testes dentro da janela do editor de código conforme você escreve e edita o código.

   ![Exibir os resultados dos testes](media/vs-2019/live-unit-testing-results.png)

1. Clique em um indicador de resultado do teste para obter mais informações, assim como os nomes dos testes que abordam esse método.

   ![Escolha os indicadores de resultados do teste](media/vs-2019/live-unit-testing-details.png)

Para obter mais informações sobre o Live Unit Testing, veja [Live Unit Testing](../test/live-unit-testing-intro.md).

## <a name="use-a-third-party-test-framework"></a>Usar uma estrutura de teste de terceiros

Você pode executar testes de unidade no Visual Studio usando estruturas de teste de terceiros, como Boost, Google e NUnit, dependendo da linguagem de programação. Para usar uma estrutura de terceiros:

- Use o **Gerenciador de Pacotes NuGet** para instalar o pacote do NuGet para a estrutura de sua escolha.

- Studio.net A partir do Visual Studio 2017 versão 14,6, o Visual Studio inclui modelos de projeto de teste pré-configurados para estruturas de teste NUnit e xUnit. Os modelos também incluem os pacotes NuGet necessários para habilitar o suporte.

- C No Visual Studio 2017 e versões posteriores, algumas estruturas, como Boost, já estão incluídas. Para obter mais informações, consulte [gravar testes de unidade para C/C++ no Visual Studio](../test/writing-unit-tests-for-c-cpp.md).

Para adicionar um projeto de teste de unidade:

1. Abra a solução que contém o código que você deseja testar.

2. Clique com o botão direito do mouse na solução no **Gerenciador de Soluções** e escolha **Adicionar** > **Novo Projeto**.

3. Selecione um modelo de projeto de teste de unidade.

   Neste exemplo, selecione [NUnit](https://nunit.org/)

   ::: moniker range=">=vs-2019"

   ![Modelo de projeto de teste NUnit no Visual Studio 2019](media/vs-2019/nunit-test-project-template.png)

   Clique em **Avançar**, nomeie o projeto e clique em **Criar**.

   ::: moniker-end

   ::: moniker range="vs-2017"

   Nomeie o projeto e clique em **OK** para criá-lo.

   ::: moniker-end

   O modelo de projeto inclui referências de NuGet a NUnit e NUnit3TestAdapter.

   ![Dependências de NuGet NUnit no Gerenciador de Soluções](media/vs-2019/nunit-nuget-dependencies.png)

4. Adicione uma referência do projeto de teste ao projeto que contém o código que você deseja testar.

   Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e selecione **Adicionar** > **Referência**. (Também é possível adicionar uma referência no menu do botão direito do nó **Referências** ou **Dependências**.)

5. Adicione código ao método de teste.

   ![Adicionar o código ao arquivo de código do teste de unidade](media/vs-2019/unit-test-method.png)

6. Execute o teste no **Test Explorer** ou clicando com o botão direito do mouse no código de teste e escolhendo **Executar teste (** ou **Ctrl**  +  **R**, **T**).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Noções básicas de teste de unidade](../test/unit-test-basics.md)

> [!div class="nextstepaction"]
> [Criar e executar testes de unidade para código gerenciado](walkthrough-creating-and-running-unit-tests-for-managed-code.md)

---
title: Unit Testing no Visual Studio
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, unit tests
- unit tests, verifying code with
- testing code, automated tests
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: e9bb75c6d7265ca66ccc0922e2d26deaa4d7857a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49874833"
---
# <a name="unit-test-your-code"></a>Efetue testes de unidade em seu código

Os testes de unidade fornecem aos desenvolvedores e testadores uma maneira rápida de procurar por erros lógicos nos métodos de classes em projetos do C#, do Visual Basic e do C++.

As ferramentas de testes de unidade incluem:

* **Gerenciador de Testes**&mdash;Você pode executar testes de unidade e ver seus resultados no **Gerenciador de Testes**. Você pode usar qualquer estrutura de teste de unidade, incluindo estruturas de terceiros, que tenha um adaptador para o **Gerenciador de Testes**.

* **Estrutura de teste de unidade da Microsoft para código gerenciado**&mdash;A estrutura de teste de unidade da Microsoft para código gerenciado é instalada com o Visual Studio e fornece uma estrutura para testar código .NET.

* **Estrutura de teste de unidade da Microsoft para C++**&mdash;A estrutura de teste de unidade da Microsoft para C++ é instalada como parte da carga de trabalho **Desenvolvimento para área de trabalho com C++**. Ela fornece uma estrutura para testar o código nativo. As estruturas do Google Test, Boost.Test e CTest também estão incluídas e adaptadores de terceiros estão disponíveis para estruturas de teste adicionais. Para obter mais informações, confira [Escrever testes de unidade para C/C++](../test/writing-unit-tests-for-c-cpp.md).

* **Ferramentas de cobertura de código**&mdash;É possível determinar a quantidade de código do produto que seus testes de unidade utilizam com um comando no Gerenciador de Testes.

* **Estrutura de isolamento do Microsoft Fakes**&mdash;A estrutura de isolamento do Microsoft Fakes pode criar classes e métodos substitutos para o código de produção e de sistema que criam dependências do código em teste. Ao implementar os delegados falsos para uma função, você controla o comportamento e a saída do objeto de dependência.

Você também pode usar o [IntelliTest](../test/generate-unit-tests-for-your-code-with-intellitest.md) para explorar seu código .NET para gerar dados de teste e um conjunto de testes de unidade. Para cada instrução no código, é gerada uma entrada de teste para executar essa instrução. Uma análise de caso é realizada para cada branch condicional do código.

## <a name="key-tasks"></a>Tarefas-chave

Use os tópicos a seguir como auxílio para entender e criar testes de unidades:

|Tarefas|Tópicos associados|
|-|-----------------------|
|**Guias de início rápido e passo a passo:** use os tópicos a seguir para aprender sobre teste de unidade no Visual Studio a partir de exemplos de código.|-   [Passo a passo: Criando e executando testes de unidade para código gerenciado](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)<br />-   [Início Rápido: desenvolvimento orientado por testes com o Gerenciador de Testes](../test/quick-start-test-driven-development-with-test-explorer.md)<br />-   [Adicionar testes de unidade a aplicativos C++ existentes](../test/unit-testing-existing-cpp-applications-with-test-explorer.md)|
|**Teste de unidade com o gerenciador de testes:** saiba como o gerenciador de testes pode ajudar a criar testes de unidade mais produtivos e eficientes.|-   [Noções básicas de teste de unidade](../test/unit-test-basics.md)<br />-   [Criação de um projeto de teste de unidade](../test/create-a-unit-test-project.md)<br />-   [Execução de testes de unidade com o gerenciador de testes](../test/run-unit-tests-with-test-explorer.md)<br />-   [Instalação de frameworks de teste de unidade de terceiros](../test/install-third-party-unit-test-frameworks.md)|
|**Teste de unidade de código C++**|-   [Escrever testes de unidade para C/C++ com o Microsoft Unit Testing Framework para C++](../test/writing-unit-tests-for-c-cpp-with-the-microsoft-unit-testing-framework-for-cpp.md)|
|**Isolamento de testes de unidade**|-   [Isolar o código em teste com o Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md)|
|**Uso da cobertura de código para identificar qual proporção do código do projeto é testada:** saiba mais sobre o recurso de cobertura de código das ferramentas de teste do Visual Studio.|-   [Usar a cobertura de código para determinar quanto do código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)|
|**Execução de análise de estresse e desempenho usando testes de carga:** você pode criar um teste de carga e adicionar seus testes de unidade a ele para ajudar a isolar os problemas de estresse e desempenho em seu aplicativo.|-   [Teste de carga (Azure Test Plans e TFS)](/azure/devops/test/load-test/index?view=vsts)|
|**Definição de restrições de qualidade:** você pode criar portões de qualidade para garantir que os testes sejam executados antes que o código seja verificado ou mesclado, para ajudar a garantir a qualidade do código.|-   [Políticas de check-in (TFVC do Azure Repos)](/azure/devops/repos/tfvc/add-check-policies?view=vsts)|
|**Definição de opções de teste:** por exemplo, você pode especificar onde os resultados dos testes são armazenados.|[Configurar testes de unidade usando um arquivo .runsettings](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)|

## <a name="api-reference-documentation"></a>Documentação de referência da API

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting> descreve o namespace UnitTesting, que fornece atributos, exceções, asserções e outras classes que oferecem suporte a testes de unidade.
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Web> descreve o namespace UnitTesting.Web, que estende o namespace UnitTesting dando suporte para o ASP.NET e a testes de unidade do serviço Web.

## <a name="see-also"></a>Consulte também

- [Melhorar a qualidade do código](../test/improve-code-quality.md)

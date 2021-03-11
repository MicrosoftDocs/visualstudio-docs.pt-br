---
title: Ferramentas de teste
description: Saiba como as ferramentas de teste do Visual Studio podem ajudá-lo e sua equipe a desenvolver e sustentar altos padrões de excelência de código.
ms.custom: SEO-VS-2020
ms.date: 03/16/2018
ms.topic: conceptual
helpviewer_keywords:
- testing tools [Visual Studio]
- unit tests [Visual Studio]
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 7efc8e5955f4d11004d8408cadf312e6cbcb43eb
ms.sourcegitcommit: f9ed9c4c6c166ef9826feb21dcb9c4d47ed14e1a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/10/2021
ms.locfileid: "102607399"
---
# <a name="first-look-at-testing-tools-in-visual-studio"></a>Primeiro, veja as ferramentas de teste no Visual Studio

As ferramentas de teste do Visual Studio podem ajudar você e sua equipe a desenvolver e manter altos padrões de excelência de código.

> [!NOTE]
> O teste de unidade está disponível em todas as edições do Visual Studio. Outras ferramentas de teste, como Live Unit Testing e IntelliTest, estão disponíveis apenas na edição Visual Studio Enterprise. Para obter mais informações sobre as edições, confira [Comparar IDEs do Visual Studio](https://visualstudio.microsoft.com/vs/compare/).

## <a name="test-explorer"></a>Gerenciador de Testes

A janela **Gerenciador de Testes** ajuda os desenvolvedores a criar, gerenciar e executar testes de unidade. Você pode usar a estrutura de teste de unidade da Microsoft ou uma das várias estruturas de software livre e de terceiros.

::: moniker range="vs-2017"
![Gerenciador de Testes do Visual Studio](media/devtest-testexplorer.png)
::: moniker-end

::: moniker range="vs-2019"
![Gerenciador de Testes do Visual Studio 16.2](media/vs-2019/test-explorer-16-2.PNG)
::: moniker-end

* [Introdução ao teste de unidade](unit-test-your-code.md)
* [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md)
* [Perguntas Frequentes sobre o Gerenciador de Testes](test-explorer-faq.md)
* [Instalar estruturas de teste de unidade de terceiros](install-third-party-unit-test-frameworks.md)

O Visual Studio também é extensível e abre a porta para adaptadores de teste de unidade de terceiros como o NUnit e o xUnit.net. Além disso, a capacidade de clone de código caminha lado a lado com o fornecimento de softwares de alta qualidade, ajudando você a identificar blocos de códigos semanticamente semelhantes que podem ser candidatos para correções de bugs comuns ou refatoração.

![Integração de teste de terceiros](media/devtest-thirdparty.png)

## <a name="live-unit-testing"></a>Live Unit Testing

O [Live Unit Testing](../test/live-unit-testing.md) executa testes de unidade automaticamente em segundo plano e exibe graficamente a cobertura de código e os resultados de teste no editor de código do Visual Studio.

> [!NOTE]
> O Live Unit Testing está disponível apenas no Enterprise Edition e só tem suporte para código .NET.

## <a name="intellitest"></a>IntelliTest

O IntelliTest gera automaticamente os testes de unidade e os dados de teste para o código gerenciado. O IntelliTest melhora a cobertura e reduz drasticamente o esforço para criar e manter os testes de unidade para código novo ou existente.

![IntelliTest em ação](media/devtest-intellitest.png)

> [!NOTE]
> O IntelliTest está disponível somente no Enterprise Edition. Há suporte para código C# destinado ao .NET Framework. No momento, não há suporte para .NET Core e .NET Standard.

* [Gerar testes de unidade para seu código com IntelliTest](generate-unit-tests-for-your-code-with-intellitest.md)
* [IntelliTest – um teste para controlar tudo](https://devblogs.microsoft.com/devops/intellitest-one-test-to-rule-them-all/)
* [Manual de referência do IntelliTest](intellitest-manual/index.md)

## <a name="code-coverage"></a>Cobertura de código

A [cobertura de código](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md) determina qual proporção do código do projeto está sendo testada de fato por testes codificados, como os testes de unidade. Para se proteger efetivamente contra bugs, os testes devem exercitar ou "cobrir" uma grande proporção de seu código.

> [!NOTE]
> A cobertura de código está disponível somente no Enterprise Edition.

A análise de cobertura de código pode ser aplicada a código gerenciado e não gerenciado (nativo).

A cobertura de código é uma opção quando você executa métodos de teste usando o Gerenciador de Testes. A tabela de resultados mostra a porcentagem do código que foi executada em cada assembly, classe e método. Além disso, o editor de código-fonte mostra que código foi testado.

* [Usar a cobertura de código para determinar quanto do código está sendo testado](using-code-coverage-to-determine-how-much-code-is-being-tested.md)
* [Teste de unidade, cobertura de código e análise de clone de código com o Visual Studio (laboratório)](https://azuredevopslabs.com/labs/devopsserver/liveunittesting)
* [Personalizar a análise de cobertura de código](customizing-code-coverage-analysis.md)

## <a name="microsoft-fakes"></a>Microsoft Fakes

O [Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md) ajuda a isolar o código que você está testando substituindo outras partes do aplicativo por stubs ou shims.

> [!NOTE]
> As falsificações da Microsoft estão disponíveis somente no Enterprise Edition e só são suportadas para código .NET.

## <a name="user-interface-testing-with-coded-ui-and-selenium"></a>Teste de interface do usuário com Selenium e IU Codificado

Os testes de IU codificados fornecem uma maneira de criar testes totalmente automatizados para validar a funcionalidade e o comportamento da interface do usuário do seu aplicativo. Eles podem automatizar o teste de interface do usuário em várias tecnologias, incluindo aplicativos UWP baseados em XAML, aplicativos de navegador e aplicativos SharePoint.

> [!NOTE]
> A interface do usuário codificada é um recurso preterido.

Se escolher um dos melhores testes de interface do usuário codificada ou testes de interface do usuário baseados em navegador genérico com o Selenium, o Visual Studio fornecerá todas as ferramentas que você precisa.

![Testes de interface do usuário com interface do usuário codificada](media/devtest-codeduitest.png)

* [Usar a automação da interface do usuário para testar o código](use-ui-automation-to-test-your-code.md)
* [Introdução à criação, edição e manutenção de um teste de interface do usuário codificado](walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
* [Testar aplicativos UWP com testes de IU codificados](test-uwp-app-with-coded-ui-test.md)
* [Introdução aos testes de IU codificados com o Visual Studio Enterprise (laboratório)](https://azuredevopslabs.com/labs/tfs/codedui)

## <a name="related-scenarios"></a>Cenários relacionados

* [Testes exploratórios e manuais (Azure Test Plans)](/azure/devops/test/index?view=vsts&preserve-view=true)
* [Teste de carga (Azure Test Plans)](/azure/devops/test/load-test/index?view=vsts&preserve-view=true)
* [Testes contínuos (Azure Test Plans)](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts&preserve-view=true)
* [Ferramentas de análise de código](../code-quality/code-analysis-for-managed-code-overview.md)

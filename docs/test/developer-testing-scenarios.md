---
title: Ferramentas de teste do desenvolvedor
ms.date: 05/02/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- unit testing, create unit tests
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 396bbfdb915d0e3ecc31f516d60eab80cca6a421
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295144"
---
# <a name="developer-testing-tools-scenarios-and-capabilities"></a>Recursos, cenários e ferramentas de teste do desenvolvedor

Mantenha a integridade do código com testes de unidade. O Visual Studio fornece uma grande variedade de técnicas e ferramentas avançadas para desenvolvedores usarem ao testar aplicativos.

## <a name="avoid-regressions-and-achieve-code-coverage-with-intellitest"></a>Evitar regressões e obter a cobertura de código com o IntelliTest

Em conjuntos de testes de unidade tradicionais, cada caso de teste representa um cenário de uso exemplar e as declarações incorporam a relação entre a entrada e a saída.  Verificar alguns desses cenários também pode ser suficiente, mas desenvolvedores experientes sabem que os bugs permanecem mesmo em códigos bem testados, quando testados, mas entradas não testadas provocam respostas erradas.

Melhore a cobertura e evite regressões com IntelliTest. O IntelliTest reduz drasticamente o esforço de criação e manutenção de testes de unidade para códigos novos ou existentes.

![IntelliTest em ação](media/devtest-intellitest.png)

* [Introduction to IntelliTest with Visual Studio](http://download.microsoft.com/download/6/2/B/62B60ECE-B9DC-4E8A-A97C-EA261BFB935E/Docs/Introduction%20to%20IntelliTest%20with%20Visual%20Studio%20Enterprise%202015.docx) (Introdução ao IntelliTest com o Visual Studio)
* [IntelliTest – um teste para controlar tudo](https://blogs.msdn.microsoft.com/devops/2015/07/05/intellitest-one-test-to-rule-them-all/)
* [Vídeos do IntelliTest](https://channel9.msdn.com/Series/Test-Tools-in-Visual-Studio)
* [Introdução ao IntelliTest](generate-unit-tests-for-your-code-with-intellitest.md)
* [Manual de referência do IntelliTest](intellitest-manual/index.md)

## <a name="user-interface-testing-with-coded-ui-and-selenium"></a>Teste de interface do usuário com Selenium e IU Codificado

Teste sua interface do usuário com o que há de melhor com teste de interface do usuário aprovado pela comunidade. Os testes de IU codificados fornecem uma maneira de criar testes totalmente automatizados para validar a funcionalidade e o comportamento da interface do usuário do seu aplicativo. Eles podem automatizar o teste de interface do usuário em várias tecnologias, incluindo aplicativos UWP baseados em XAML, aplicativos de navegador e aplicativos SharePoint.

O Visual Studio fornece todas as ferramentas necessárias seja para o que há de melhor em testes de IU codificados ou em testes de interface do usuário genéricos com base em navegador com o Selenium.

![Testes de interface do usuário com interface do usuário codificada](media/devtest-codeduitest.png)

* [Usar a automação de interface do usuário para testar seu código](use-ui-automation-to-test-your-code.md)
* [Introdução à criação, à edição, e à manutenção do teste de IU codificado](walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
* [Testar aplicativos UWP com testes de IU codificados](test-uwp-app-with-coded-ui-test.md)
* [Testar aplicativos do SharePoint com testes de IU codificados](testing-sharepoint-2010-applications-with-coded-ui-tests.md)
* [Introdução aos testes de IU codificados com o Visual Studio Enterprise (laboratório)](http://download.microsoft.com/download/6/2/B/62B60ECE-B9DC-4E8A-A97C-EA261BFB935E/Docs/Introduction%20to%20Coded%20UI%20Tests%20with%20Visual%20Studio%20Enterprise%202015.docx)

## <a name="effective-unit-testing-with-visual-studio-code-coverage"></a>Teste de unidade efetivo com a cobertura de código do Visual Studio

Para determinar que proporção do código do projeto está sendo testada de fato por testes codificados, como os testes de unidade, você pode usar o recurso de cobertura de código do Visual Studio. Para se proteger efetivamente contra bugs, os testes devem utilizar ou abranger uma grande proporção de seu código.

A análise de cobertura de código pode ser aplicada a código gerenciado e não gerenciado (nativo).

A cobertura de código é uma opção quando você executa métodos de teste usando o Gerenciador de Testes. A tabela de resultados mostra a porcentagem do código que foi executada em cada assembly, classe e método. Além disso, o editor de código-fonte mostra que código foi testado.

* [Usar a cobertura de código para determinar quanto do código está sendo testado](using-code-coverage-to-determine-how-much-code-is-being-tested.md)
* [Teste de unidade, cobertura de código e análise de clone de código com o Visual Studio (laboratório)](http://download.microsoft.com/download/6/2/B/62B60ECE-B9DC-4E8A-A97C-EA261BFB935E/Docs/Unit%20Testing,%20Code%20Coverage%20and%20Code%20Clone%20Analysis%20with%20Visual%20Studio%202015.docx)
* [Personalizar a análise de cobertura de código](customizing-code-coverage-analysis.md)

## <a name="test-explorer"></a>Gerenciador de Testes

O **Gerenciador de Testes** ajuda os desenvolvedores a criar, gerenciar e executar testes de unidade.

![Gerenciador de Testes do Visual Studio](media/devtest-testexplorer.png)

* [Introdução ao teste de unidade](unit-test-your-code.md)
* [Executar testes de unidade com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md)
* [Perguntas Frequentes sobre o Gerenciador de Testes](test-explorer-faq.md)
* [Instalar estruturas de teste de unidade de terceiros](install-third-party-unit-test-frameworks.md)

O Visual Studio também é extensível e abre a porta para adaptadores de teste de unidade de terceiros como o NUnit e o xUnit.net. Além disso, a capacidade de clone de código caminha lado a lado com o fornecimento de softwares de alta qualidade, ajudando você a identificar blocos de códigos semanticamente semelhantes que podem ser candidatos para correções de bugs comuns ou refatoração.

![Integração de teste de terceiros](media/devtest-thirdparty.png)

## <a name="see-also"></a>Consulte também

* [Introdução ao teste de unidade](getting-started-with-unit-testing.md)
* [Acelerar a execução de teste de unidade no Team Foundation Server](https://blogs.msdn.microsoft.com/devops/2015/07/30/speeding-up-unit-test-execution-in-tfs/)
* [Execução de teste de unidade paralela e sensível ao contexto](https://blogs.msdn.microsoft.com/devops/2016/02/08/parallel-and-context-sensitive-test-execution-with-visual-studio-2015-update-1/)
* [Teste de unidade, cobertura de código e análise de clone de código com o Visual Studio (laboratório)](http://download.microsoft.com/download/6/2/B/62B60ECE-B9DC-4E8A-A97C-EA261BFB935E/Docs/Unit%20Testing,%20Code%20Coverage%20and%20Code%20Clone%20Analysis%20with%20Visual%20Studio%202015.docx)
* [Escrevendo Testes de Unidade para C/C++](writing-unit-tests-for-c-cpp.md)

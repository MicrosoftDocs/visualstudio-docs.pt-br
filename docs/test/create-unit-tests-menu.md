---
title: Criar stubs de método de teste de unidade
ms.date: 04/24/2020
ms.topic: how-to
helpviewer_keywords:
- unit testing, create unit tests
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5b2712210d4761edb90414e2a27beba74a3bacbf
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288657"
---
# <a name="create-unit-test-method-stubs-with-the-create-unit-tests-command"></a>Criar stubs de método de teste de unidade com o comando Criar Testes de Unidade

O comando **Criar Testes de Unidade** cria os stubs de método de teste de unidade. Esse recurso permite a configuração fácil de um projeto de teste, da classe de teste e do stub do método de teste dentro dele.

::: moniker range="vs-2017"
> [!NOTE]
> O comando de menu **criar testes de unidade** só está disponível para código C# destinado a .NET Framework (mas não ao .NET Core).
::: moniker-end
::: moniker range=">=vs-2019"
> [!NOTE]
> O comando de menu **criar testes de unidade** só está disponível para código C#.
::: moniker-end

O comando de menu **Criar Testes de Unidade** é extensível e pode ser usado para gerar testes para MSTest, MSTest V2, NUnit e xUnit.

## <a name="get-started"></a>Introdução

Para começar, selecione um método, um tipo ou um namespace no editor de código no projeto que você deseja testar, clique com o botão direito do mouse e escolha **Criar Testes de Unidade**. A caixa de diálogo **Criar Testes de Unidade** se abre e, nela, você pode configurar como você deseja que os testes sejam criados.

![Usando o comando Criar testes de unidade](media/createunittestcommand.png)

## <a name="set-unit-test-traits"></a>Configurar características do teste de unidade

Caso pretenda executar esses testes como parte do processo de automação de teste, considere a criação do teste em outro projeto de teste (a segunda opção na caixa de diálogo acima) e a configuração das características do teste de unidade para o teste de unidade. Isso permite que você inclua ou exclua com mais facilidade esses testes específicos como parte de um pipeline de integração contínua ou implantação contínua. As características são definidas pela adição de metadados ao teste de unidade diretamente, conforme mostrado abaixo.

![Configurando as características do teste de unidade](media/createunittest.png)

## <a name="use-third-party-unit-test-frameworks"></a>Usar estruturas de teste da unidade de terceiros

Para gerar automaticamente os testes de unidade para o NUnit ou o xUnit, instale uma das seguintes extensões de estrutura de teste do Visual Studio Marketplace:

* [Extensão NUnit para geradores de teste](https://marketplace.visualstudio.com/items?itemName=NUnitDevelopers.TestGeneratorNUnitextension)
* [Extensão xUnit.net para geradores de teste](https://marketplace.visualstudio.com/items?itemName=BradWilson.xUnitnetTestExtensions)

## <a name="when-should-i-use-this-feature"></a>Quando devo usar esse recurso?

Use esse recurso sempre que precisar criar testes de unidade, mas especialmente quando estiver testando um código existente que tem pouca ou nenhuma cobertura de teste e nenhuma documentação. Em outras palavras, onde há uma especificação de código limitada ou inexistente. Ela implementa efetivamente uma abordagem semelhante aos [Testes de unidade inteligentes](https://devblogs.microsoft.com/devops/introducing-smart-unit-tests/) que caracteriza o comportamento observado do código.

No entanto, esse recurso é igualmente aplicável quando um desenvolvedor começa escrevendo um pouco de código e o usa para inicializar testes de unidade. Dentro do fluxo de codificação, o desenvolvedor talvez queira criar rapidamente um stub de método de teste de unidade (com uma classe de teste adequada e um projeto de teste adequado) para uma determinada parte do código.

## <a name="see-also"></a>Veja também

- [Como criar stubs de método de teste de unidade com "Criar Testes de Unidade"](https://devblogs.microsoft.com/devops/creating-unit-test-method-stubs-with-create-unit-tests/)
- [Postagens no blog sobre testes de unidade](https://devblogs.microsoft.com/devops/?s=unit+testing)

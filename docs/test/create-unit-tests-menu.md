---
title: Criar stubs de método de teste de unidade
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- unit testing, create unit tests
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e8ddc4e7a44aa0d5d42a64556092874413e3a3b2
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2019
ms.locfileid: "57982760"
---
# <a name="create-unit-test-method-stubs-with-the-create-unit-tests-command"></a>Criar stubs de método de teste de unidade com o comando Criar Testes de Unidade

O comando **Criar Testes de Unidade** do Visual Studio fornece a capacidade de criar stubs de método de teste de unidade. Esse recurso permite a configuração fácil de um projeto de teste, da classe de teste e do stub do método de teste dentro dele.

## <a name="availability-and-extensions"></a>Disponibilidade e extensões

O comando de menu **Criar Testes de Unidade**:

* Está disponível nas edições Community, Professional e Enterprise do Visual Studio 2015 e posteriores.

* Dá suporte apenas ao código C# destinado ao .NET Framework.

* É extensível e dá suporte à emissão de testes nos formatos MSTest, MSTest V2, NUnit e xUnit.

* Ainda não disponível em projetos .NET Core.

## <a name="get-started"></a>Introdução

Para começar, selecione um método, um tipo ou um namespace no editor de código no projeto que você deseja testar, abra o menu de atalho e escolha **Criar Testes de Unidade**. A caixa de diálogo **Criar Testes de Unidade** será aberta, na qual as opções de criação para os novos testes de unidade podem ser selecionadas.

![Usando o comando Criar testes de unidade](media/createunittestcommand.png)

## <a name="set-unit-test-traits"></a>Configurar características do teste de unidade

Caso pretenda executar esses testes como parte do processo de automação de teste, considere a criação do teste em outro projeto de teste (a segunda opção na caixa de diálogo acima) e a configuração das características do teste de unidade para o teste de unidade. Isso permite que você inclua ou exclua com mais facilidade esses testes específicos como parte de um pipeline de integração contínua ou implantação contínua. As características são definidas pela adição de metadados ao teste de unidade diretamente, conforme mostrado abaixo.

![Configurando as características do teste de unidade](media/createunittest.png)

## <a name="use-third-party-unit-test-frameworks"></a>Usar estruturas de teste da unidade de terceiros

Com o Visual Studio, você pode facilmente criar testes de unidade usando qualquer estrutura de teste. Para instalar outras estruturas de teste:

::: moniker range="vs-2017"

1. Escolha **Ferramentas** > **Extensões e Atualizações**.

::: moniker-end

::: moniker range=">=vs-2019"

1. Escolha **Extensões** > **Gerenciar Extensões**.

::: moniker-end

2. Expanda **Online** > **Visual Studio Marketplace** > **Ferramentas** e, em seguida, escolha **Testes**.

![Usando estruturas de teste de terceiros](media/createunittestfx.png)

As extensões da estrutura de teste também estão disponíveis no Visual Studio Marketplace:

* [Extensão do NUnit para os geradores de teste](https://marketplace.visualstudio.com/items?itemName=NUnitDevelopers.TestGeneratorNUnitextension)
* [Extensão do xUnit.net para os geradores de teste](https://marketplace.visualstudio.com/items?itemName=BradWilson.xUnitnetTestExtensions)

## <a name="when-should-i-use-this-feature"></a>Quando devo usar esse recurso?

Use esse recurso sempre que precisar criar testes de unidade, mas especialmente quando estiver testando um código existente que tem pouca ou nenhuma cobertura de teste e nenhuma documentação. Em outras palavras, onde há uma especificação de código limitada ou inexistente. Ela implementa efetivamente uma abordagem semelhante aos [Testes de unidade inteligentes](https://devblogs.microsoft.com/devops/introducing-smart-unit-tests/) que caracterizam o comportamento observado do código.

No entanto, esse recurso é igualmente aplicável para a situação em que o desenvolvedor começa escrevendo um código e o usa para inicializar a disciplina de teste de unidade. Dentro do fluxo de codificação, o desenvolvedor talvez queira criar rapidamente um stub de método de teste de unidade (com uma classe de teste adequada e um projeto de teste adequado) para uma determinada parte do código.

## <a name="see-also"></a>Consulte também

- [Criar stubs de método de teste de unidade com "Criar testes de unidade"](https://devblogs.microsoft.com/devops/creating-unit-test-method-stubs-with-create-unit-tests/)
- [Postagens de blog sobre testes de unidade](https://devblogs.microsoft.com/devops/?s=unit+testing)

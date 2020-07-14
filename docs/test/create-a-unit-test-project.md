---
title: Crie um projeto de teste de unidade
ms.date: 01/29/2019
ms.topic: how-to
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: ffa19fb9dc49d6286ef3f54c51d89043445f18ba
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288709"
---
# <a name="create-a-unit-test-project"></a>Crie um projeto de teste de unidade

Geralmente, os testes de unidade refletem a estrutura do código que está sendo testado. Por exemplo, um projeto de teste de unidade será criado para cada projeto de código do produto. O projeto de teste pode estar na mesma solução que o código de produção ou em uma solução separada. É possível ter vários projetos de teste de unidade em uma solução.

> [!NOTE]
> O local dos testes de unidade para o código nativo e a estrutura do projeto de teste podem ser diferentes da estrutura descrita neste artigo. Para obter mais informações, consulte [escrevendo testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md).

## <a name="to-create-a-unit-test-project"></a>Para criar um projeto de teste de unidade

1. No menu **Arquivo**, escolha **Novo** > **Projeto** ou pressione **Ctrl**+**Shift**+**N**.

::: moniker range="vs-2017"

2. Na caixa de diálogo **Novo Projeto**, expanda o nó **Instalado**, escolha a linguagem que deseja usar para o projeto de teste e clique em **Testar**.

3. Selecione o modelo de projeto para a estrutura de teste que você deseja usar, por exemplo, **Projeto de teste do MSTest** ou **Projeto de teste do NUnit**. Nomeie o projeto e, em seguida, escolha **OK**.

   ![Modelos de projeto de teste no Visual Studio 2017](media/test-project-templates.png)

::: moniker-end

::: moniker range=">=vs-2019"

2. Na página **Criar um novo projeto**, digite **teste de unidade** na caixa de pesquisa. Selecione o modelo de projeto para a estrutura de teste que você deseja usar, por exemplo, **Projeto de teste do MSTest** ou **Projeto de teste do NUnit** e escolha **Avançar**.

   ![Modelos de projeto de teste no Visual Studio 2019](media/vs-2019/test-project-templates.png)

3. Na página **Configurar seu novo projeto**, insira um nome para o projeto e escolha **Criar**.

::: moniker-end

4. No projeto de teste de unidade, adicione uma referência ao código que está sendo testado. Para adicionar uma referência a um projeto de código na mesma solução:

   1. Selecione o projeto de teste no **Gerenciador de Soluções**.

   2. No menu **Projeto**, escolha **Adicionar Referência**.

   3. Na **Gerenciador de Referências**, selecione o nó **Solução** sob **Projetos**. Selecione o projeto de código que você deseja testar e, em seguida, selecione **OK**.

   Se o código que você deseja testar estiver em outro local, consulte [Gerenciando referências em um projeto](../ide/managing-references-in-a-project.md) para obter informações sobre como adicionar uma referência.

## <a name="next-steps"></a>Próximas etapas

Consulte uma das seguintes seções:

**Escrevendo testes de unidade**

- [Teste de unidade em seu código](../test/unit-test-your-code.md)

- [Escrevendo testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md)

- [Usar a estrutura do MSTest em testes de unidade](using-microsoft-visualstudio-testtools-unittesting-members-in-unit-tests.md)

**Executando testes de unidade**

- [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md)

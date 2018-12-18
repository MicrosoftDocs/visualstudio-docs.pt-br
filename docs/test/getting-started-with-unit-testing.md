---
title: Introdução ao teste de unidade
ms.date: 05/02/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- unit testing, create unit test plans
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 171d329ed852bf6a27f20f12ae0f5421103820ff
ms.sourcegitcommit: 3dd15e019cba7d35dbabc1aa3bf55842a59f5278
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46370800"
---
# <a name="get-started-with-unit-testing"></a>Introdução ao teste de unidade

Use o Visual Studio para definir e executar os testes de unidade para manter a integridade de código, certificar-se da cobertura de código e localizar erros e falhas antes de seus clientes.

## <a name="create-unit-tests"></a>Criar testes de unidade

Crie testes de unidade e execute-os frequentemente para ter certeza de que seu código está funcionando corretamente.

1. Crie um projeto de teste de unidade.

   ![Adicionar um projeto de teste de unidade à sua solução](media/createunittest1.png)

1. Nomeie o projeto.

   ![Modelo de projeto de teste de unidade](media/createunittest2.png)

   O projeto é adicionado à solução.

   ![Projeto de teste de unidade no Gerenciador de Soluções](media/createunittest5.png)

1. No projeto de teste de unidade, adicione uma referência ao projeto que deseja testar.

   ![Adicionar uma referência ao seu projeto de teste de unidade](media/createunittest6.png)

1. Selecione o projeto que contém o código que você testará.

   ![Selecionar a referência a ser adicionada](media/createunittest7.png)

1. Codifique seu teste de unidade.

   ![Adicionar código ao teste de unidade](media/createunittest8.png)

Você também pode criar stubs de método de teste de unidade com o[comando](create-unit-tests-menu.md) **Criar Testes de Unidade**.

![Usando o comando Criar testes de unidade](media/createunittestcommand2.png)

## <a name="run-unit-tests"></a>Executar testes de unidade

1. Abra o **Gerenciador de Testes**.

   ![No menu Teste, abra o Gerenciador de testes](media/rununittest1.png)

1. Execute os testes de unidade.

   ![Executar testes de unidade no Gerenciador de Testes](media/rununittest2.png)

   Você pode ver os testes de unidade que foram aprovados ou falharam no **Gerenciador de Testes**.

   ![Examine os resultados de teste de unidade no Gerenciador de Testes](media/rununittest3.png)

## <a name="view-live-unit-test-results"></a>Exibir resultados de teste de unidade em tempo real

Se estiver usando a estrutura de teste do MSTest, do xUnit ou do NUnit no Visual Studio de 2017 ou posterior, você poderá ver os resultados em tempo real de seus testes de unidade.

> [!NOTE]
> O Live Unit Testing está disponível somente no Visual Studio 2017 Enterprise Edition.

1. Ative o teste de unidade em tempo real no menu **Teste**.

   ![Ativar o teste de unidade em tempo real](media/live-test-results-start.png)

1. Exiba os resultados dos testes dentro da janela do editor de código conforme você escreve e edita o código.

   ![Exibir os resultados dos testes](media/live-test-results-ui.png)

1. Escolha os indicadores de resultados do teste para obter mais informações.

   ![Escolha os indicadores de resultados do teste](media/live-test-results-details.png)

Para obter mais detalhes, consulte [Live unit testing](../test/live-unit-testing-intro.md) (Testes de unidade dinâmicos).

## <a name="generate-unit-tests-with-intellitest"></a>Gerar testes de unidade com IntelliTest

Quando executa o IntelliTest, você pode ver facilmente quais testes estão falhando e adicionar o código que for necessário para corrigi-los. É possível selecionar quais dos testes gerados serão salvos em um projeto de teste para oferecer um pacote de regressão. Conforme você alterar seu código, execute novamente o IntelliTest para manter os testes gerados em sincronia com as alterações do código. Para saber como, confira [Gerar testes de unidade para seu código com o IntelliTest](../test/generate-unit-tests-for-your-code-with-intellitest.md).

![Gerando testes de unidade com IntelliTest](media/intellitest.png)

## <a name="run-unit-tests-with-test-explorer"></a>Executar testes de unidade com o Gerenciador de Testes

Use o **Gerenciador de Testes** para executar testes de unidade do Visual Studio ou projetos de teste de unidade de terceiros, agrupar testes em categorias, filtre a lista de testes, criar, salvar e executar as listas de reprodução de testes. Você também pode depurar testes e analisar um teste de desempenho e cobertura de código. Para saber como, consulte [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md).

![Executando testes de unidade com o Gerenciador de Testes](media/testexplorer.png)

## <a name="use-code-coverage-to-determine-how-much-code-is-being-tested"></a>Usar a cobertura de código para determinar quanto do código está sendo testado

Para determinar que proporção do código do projeto está sendo testada de fato por testes codificados, como os testes de unidade, você pode usar o recurso de cobertura de código do Visual Studio. Para se proteger efetivamente contra bugs, os testes devem usar uma grande proporção do seu código. Para saber como, confira [Usar a cobertura de código para determinar quanto do código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).

## <a name="use-a-different-unit-test-framework"></a>Usar uma estrutura de teste de unidade diferente

Você pode executar testes de unidade no Visual Studio usando estruturas de teste de terceiros, como Boost, Google e NUnit. Use o plug-in para essa estrutura para que o executor de teste do Visual Studio possa funcionar com ela.

Veja a seguir as etapas para habilitar estruturas de teste de terceiros:

1. Na barra de menus, escolha **Ferramentas** > **Extensões e Atualizações**.

1. Na caixa de diálogo **Extensões e Atualizações**, expanda a categoria **Online** e escolha **Visual Studio Marketplace**. Em seguida, escolha **Ferramentas** > **Testes**.

   ![Visual Studio Marketplace](media/extensions-and-updates-testing.png)

1. Selecione a estrutura ou adaptador que deseja instalar e, em seguida, escolha **Baixar**.

1. Crie um projeto de biblioteca de classes e adicione-o à sua solução.

   ![Atribua um nome ao projeto de biblioteca de classes e adicione-o](media/create3rdpartyunittest3.png)

1. Instale o plug-in. No **Gerenciador de Soluções**, selecione o projeto de biblioteca de classes e, em seguida, escolha **Gerenciar pacotes NuGet** no menu de contexto ou clicando com o botão direito do mouse.

   ![Gerenciar pacotes NuGet para instalar o plug-in](media/create3rdpartyunittest3a.png)

   O [NuGet](https://www.nuget.org/) é uma extensão do Visual Studio que pode ser usada para adicionar e atualizar bibliotecas e ferramentas dos seus projetos.

1. Na janela do **Gerenciador de Pacotes NuGet**, pesquise e selecione o plug-in e, em seguida, escolha **Instalar**.

   ![Instalar a estrutura de terceiros](media/create3rdpartyunittest4.png)

   A estrutura é referenciada no seu projeto.

   ![A referência para a estrutura de teste de unidade de terceiros é adicionada à solução](media/create3rdpartyunittest6.png)

1. No nó **Referências** do projeto de biblioteca de classes, selecione **Adicionar Referência**.

   ![Adicionar uma referência ao projeto](media/createunittest6.png)

1. Na caixa de diálogo **Gerenciador de Referências**, selecione o projeto que contém o código que você testará.

   ![Selecione o projeto de código para testar](media/createunittest7.png)

1. Codifique seu teste de unidade.

   ![Adicionar código ao teste de unidade](media/create3rdpartyunittest7.png)

## <a name="see-also"></a>Consulte também

* [Criar comando de Testes de Unidade](create-unit-tests-menu.md)
* [Gerar testes com IntelliTest](generate-unit-tests-for-your-code-with-intellitest.md)
* [Executar testes com o Gerenciador de Testes](run-unit-tests-with-test-explorer.md)
* [Determinar a cobertura de código](using-code-coverage-to-determine-how-much-code-is-being-tested.md)
* [Melhorar a qualidade do código](improve-code-quality.md)
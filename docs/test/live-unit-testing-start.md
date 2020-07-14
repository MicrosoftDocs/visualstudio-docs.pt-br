---
title: Saiba como testar códigos com o Live Unit Testing
ms.date: 04/03/2020
ms.topic: how-to
helpviewer_keywords:
- Live Unit Testing
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ef0fbd5c422d16df4e361ff95f4ac8deabdd5bae
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287006"
---
# <a name="get-started-with-live-unit-testing"></a>Introdução ao Live Unit Testing

Quando você habilita Live Unit Testing em uma solução do Visual Studio, ele representa visualmente a cobertura do teste e o status de seus testes. O Live Unit Testing também executa testes dinamicamente sempre que você modifica seu código e notifica imediatamente quando as alterações causam falha nos testes.

Live Unit Testing pode ser usado para testar soluções direcionadas a .NET Framework ou .NET Core. Neste tutorial, você aprenderá a usar Live Unit Testing criando uma biblioteca de classes simples que tem como alvo .NET Standard, e criará um projeto MSTest que tem como alvo o .NET Core para testá-lo.

A solução C# completa pode ser baixada do repositório [MicrosoftDocs/visualstudio-docs](https://github.com/MicrosoftDocs/visualstudio-docs/tree/master/docs/test/samples/csharp/UtilityLibraries/) no GitHub.

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial requer que você tenha instalado o Visual Studio Enterprise Edition com a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** .

## <a name="create-the-solution-and-the-class-library-project"></a>Criar a solução e o projeto de biblioteca de classes

Comece criando uma solução do Visual Studio denominada UtilityLibraries que consiste em um único projeto de biblioteca de classes de .NET Standard, StringLibrary.

A solução é apenas um contêiner para um ou mais projetos. Para criar uma solução em branco, abra o Visual Studio e faça o seguinte:

1. Selecione **arquivo**  >  **novo**  >  **projeto** no menu do Visual Studio de nível superior.

1. Digite **Solução** na caixa de pesquisa de modelo e selecione o modelo **Solução em Branco**. Nomeie o projeto **UtilityLibraries**.

   ::: moniker range="vs-2017"

   ![A caixa de diálogo **Novo Projeto**](./media/lut-start/new-solution.png)

   ::: moniker-end

1. Conclua a criação da solução.

Agora que você criou a solução, criará uma biblioteca de classes chamada StringLibrary que contém vários métodos de extensão para trabalhar com cadeias de caracteres.

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução UtilityLibraries e selecione **Adicionar**  >  **novo projeto**.

::: moniker range="vs-2017"

2. Na caixa de diálogo **Adicionar Novo Projeto** selecione o nó C# e, em seguida, selecione **.NET Standard**.

   > [!NOTE]
   > Como nossa biblioteca tem como destino .NET Standard em vez de uma implementação .NET específica, ela pode ser chamada de qualquer implementação do .NET que dê suporte a essa versão do .NET Standard. Para obter mais informações, confira [.NET Standard](/dotnet/standard/net-standard).

3. Selecione o modelo **biblioteca de classes (.net Standard)** no painel direito e digite **StringLibrary** na caixa de texto **nome** , como mostra a ilustração a seguir:

   ![Caixa de diálogo **Adicionar Novo Projeto**](./media/lut-start/add-project-cs.png)

4. Selecione **OK** para criar o projeto.

::: moniker-end

::: moniker range=">=vs-2019"

2. Digite **biblioteca de classes** na caixa de pesquisa de modelo e selecione o modelo **Biblioteca de Classes (.NET Standard)**. Clique em **Avançar**.

   > [!NOTE]
   > Como nossa biblioteca tem como destino .NET Standard em vez de uma implementação .NET específica, ela pode ser chamada de qualquer implementação do .NET que dê suporte a essa versão do .NET Standard. Para obter mais informações, confira [.NET Standard](/dotnet/standard/net-standard).

3. Nomeie o projeto **StringLibrary**.

4. Clique em **Criar** para criar o projeto.

::: moniker-end

5. Substitua todo o código existente no editor de código pelo código a seguir:

   [!code-csharp[StringLibrary source code](samples/csharp/utilitylibraries/stringlibrary/class1.cs)]

   StringLibrary tem três métodos estáticos:

   - `StartsWithUpper` retornará `true` se uma cadeia de caracteres começar com um caractere maiúsculo, caso contrário, retornará `false`.

   - `StartsWithLower` retornará `true` se uma cadeia de caracteres começar com um caractere minúsculo, caso contrário, retornará `false`.

   - `HasEmbeddedSpaces` retornará `true` se uma cadeia de caracteres contiver um caractere de espaço em branco inserido, caso contrário, retornará `false`.

6. Selecione **criar**  >  **solução de compilação** no menu do Visual Studio de nível superior. A compilação deve ter sucesso.

## <a name="create-the-test-project"></a>Criar um projeto de teste

A próxima etapa é criar o projeto de teste de unidade para testar a biblioteca StringLibrary. Crie testes de unidade, executando as seguintes etapas:

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução UtilityLibraries e selecione **Adicionar**  >  **novo projeto**.

::: moniker range="vs-2017"

2. Na caixa de diálogo **Adicionar Novo Projeto** selecione o nó C# e, em seguida, selecione **.NET Core**.

   > [!NOTE]
   > Você não precisa escrever os testes de unidade na mesma linguagem da biblioteca de classes.

3. Selecione o modelo **projeto de teste de unidade (.NET Core)** no painel direito e digite **StringLibraryTests** na caixa de texto **nome** , como mostra a ilustração a seguir:

   ![A caixa de diálogo **Adicionar Novo Projeto** do projeto de teste de unidade](./media/lut-start/add-unit-test-cs.png)

4. Selecione **OK** para criar o projeto.

::: moniker-end

::: moniker range=">=vs-2019"

2. Digite **teste de unidade** na caixa de pesquisa de modelo e selecione o modelo de **projeto de teste MSTest (.NET Core)** . Clique em **Avançar**.

3. Nomeie o projeto **StringLibraryTests**.

4. Clique em **Criar** para criar o projeto.

::: moniker-end

   > [!NOTE]
   > Este tutorial de introdução usa o Live Unit Testing com o framework de teste do MSTest. Você também pode usar as estruturas de teste xUnit e NUnit.

5. O projeto de teste de unidade não pode acessar automaticamente a biblioteca de classes que ele está testando. Forneça acesso à biblioteca de teste adicionando uma referência ao projeto de biblioteca de classes. Para fazer isso, clique com o botão direito do mouse no `StringLibraryTests` projeto e selecione **Adicionar**  >  **referência**. Na caixa de diálogo **Gerenciador de referências** , verifique se a guia **solução** está selecionada e selecione o projeto StringLibrary, conforme mostrado na ilustração a seguir.

   ![A caixa de diálogo **Gerenciador de Referências**](./media/lut-start/add-reference.png)

6. Substitua o código de teste de unidade clichê que o modelo fornece pelo código a seguir:

   [!code-csharp[StringLibraryTest source code](samples/snippets/csharp/lut-start/unittest1.cs)]

7. Salve o projeto selecionando o ícone **Salvar** na barra de ferramentas.

   Como o código de teste de unidade inclui alguns caracteres não-ASCII, você verá a caixa de diálogo a seguir para avisar que alguns caracteres serão perdidos se você salvar o arquivo em seu formato ASCII padrão.

8. Escolha o botão **Salvar com Outra Codificação**.

   ![Escolha uma codificação de arquivo](media/lut-start/ascii-encoding.png)

9. Na lista suspensa **codificação** da caixa de diálogo **Opções de salvamento avançado** , escolha **Unicode (UTF-8 sem assinatura)-CodePage 65001**, como mostra a ilustração a seguir:

   ![Escolhendo a codificação UTF-8](media/lut-start/utf8-encoding.png)

10. Compile o projeto de teste de unidade selecionando **criar**  >  **solução de recompilação** no menu do Visual Studio de nível superior.

Você criou uma biblioteca de classes e também alguns testes de unidade para ela. Agora você terminou as etapas preliminares necessárias para usar o Live Unit Testing.

## <a name="enable-live-unit-testing"></a>Habilitar o Live Unit Testing

Até agora, embora você tenha escrito os testes para a biblioteca de classes StringLibrary, você não os executou. O Live Unit Testing executa-os automaticamente ao ser habilitado. Para isso, faça o seguinte:

1. Opcionalmente, selecione a janela Editor de código que contém o código para StringLibrary. Isso é *Class1.cs* para um projeto em C# ou *Class1. vb* para um projeto Visual Basic. (Essa etapa permite inspecionar visualmente o resultado de seus testes e a extensão de sua cobertura de código depois que você habilita o Live Unit Testing.)

1. Selecione **testar**  >  **Live Unit Testing**  >  **Iniciar** no menu de nível superior do Visual Studio.

1. O Visual Studio inicia o Live Unit Testing, que executa automaticamente todos os seus testes.

::: moniker range="vs-2017"
Quando ele termina de executar os testes, o **Gerenciador de Testes** exibe os resultados gerais e o resultado dos testes individuais. Além disso, a janela Editor de código exibe graficamente a cobertura do código de teste e o resultado de seus testes. Como mostra a ilustração a seguir, todos os três testes foram executados com êxito. Ela também mostra que nossos testes cobriram todos os caminhos de código no método `StartsWithUpper` e que todos esses testes foram executados com êxito (o que é indicado pela marca de verificação verde "✓"). Por fim, ele mostra que nenhum dos outros métodos em StringLibrary tem cobertura de código (que é indicada por uma linha azul, "➖").

![O Gerenciador de testes e a janela do editor de código depois de iniciar o Live Unit Test](media/lut-start/lut-results-cs.png)
::: moniker-end
::: moniker range=">=vs-2019"
Quando terminar de executar seus testes, **Live Unit Testing** exibirá os resultados gerais e o resultado de testes individuais. Além disso, a janela Editor de código exibe graficamente a cobertura do código de teste e o resultado de seus testes. Como mostra a ilustração a seguir, todos os três testes foram executados com êxito. Ela também mostra que nossos testes cobriram todos os caminhos de código no método `StartsWithUpper` e que todos esses testes foram executados com êxito (o que é indicado pela marca de verificação verde "✓"). Por fim, ele mostra que nenhum dos outros métodos em StringLibrary tem cobertura de código (que é indicada por uma linha azul, "➖").

![O Live Test Explorer e a janela do editor de código depois de iniciar o Live Unit Test](media/lut-start/vs-2019/lut-results-cs.png)
::: moniker-end

Você também pode obter informações mais detalhadas sobre a cobertura de teste e os resultados de teste selecionando um ícone de cobertura de código específico na janela Editor de código. Para examinar este detalhe, faça o seguinte:

1. Clique na marca de verificação verde na linha em que está escrito `if (String.IsNullOrWhiteSpace(s))` no método `StartsWithUpper`. Como mostra a ilustração a seguir, Live Unit Testing indica que três testes abrangem essa linha de código e que todos foram executados com êxito.

   ![Cobertura de código para a instrução condicional 'if'](media/lut-start/code-coverage-cs1.png)

1. Clique na marca de verificação verde na linha em que está escrito `return Char.IsUpper(s[0])` no método `StartsWithUpper`. Como mostra a ilustração a seguir, Live Unit Testing indica que apenas dois testes cobrem a linha de código e que todos foram executados com êxito.

   ![Cobertura de código para a instrução return](media/lut-start/code-coverage-cs2.png)

A questão mais importante que o Live Unit Testing identifica é uma cobertura de código incompleta. Isso será abordado na próxima seção.

## <a name="expand-test-coverage"></a>Expandir a cobertura do teste

Nesta seção, você estenderá os testes de unidade para o método `StartsWithLower`. Enquanto você estiver fazendo isso, o Live Unit Testing continuará a testar o código dinamicamente.

Para estender a cobertura de código para o método `StartsWithLower`, faça o seguinte:

1. Adicione os seguintes métodos `TestStartsWithLower` e `TestDoesNotStartWithLower` no arquivo de código-fonte do teste do projeto:

    [!code-csharp[StringLibraryTest source code](samples/snippets/csharp/lut-start/unittest2.cs#1)]

1. Modifique o `DirectCallWithNullOrEmpty` método adicionando o código a seguir imediatamente após a chamada para o [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.isfalse) método.

    [!code-csharp[StringLibraryTest source code](samples/snippets/csharp/lut-start/unittest2.cs#2)]

1. O Live Unit Testing executa automaticamente os testes novos e modificados quando você modifica o código-fonte. Como mostra a ilustração a seguir, todos os testes, incluindo os dois que você adicionou e o que você modificou foram bem-sucedidos.

   ::: moniker range="vs-2017"
   ![O Gerenciador de testes após expandir a cobertura de teste](media/lut-start/test-dynamic.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![O Live Test Explorer após expandir a cobertura de teste](media/lut-start/vs-2019/test-dynamic.png)
   ::: moniker-end

1. Alterne para a janela que contém o código-fonte da classe StringLibrary. Agora, o Live Unit Testing mostra que a cobertura de código foi estendida para o método `StartsWithLower`.

    ![Cobertura de código do método StartsWithLower](media/lut-start/lut-extended-cs.png)

Em alguns casos, testes bem-sucedidos no **Gerenciador de testes** podem estar esmaecidos. Isso indica que um teste está em execução no momento ou que o teste não foi executado novamente porque não houve alterações de código que afetem o teste desde que ele foi executado pela última vez.

Até agora, todos os nossos testes tiveram êxito. Na próxima seção, vamos examinar como você pode tratar uma falha de teste.

## <a name="handle-a-test-failure"></a>Lidar com uma falha de teste

Nesta seção, você vai explorar como é possível usar o Live Unit Testing para identificar, corrigir e solucionar problemas de falhas de teste. Você fará isso expandindo a cobertura do teste para o método `HasEmbeddedSpaces`.

1. Adicione o seguinte método ao arquivo de teste:

    [!code-csharp[The TestHasEmbeddedSpaces test method](samples/snippets/csharp/lut-start/unittest2.cs#3)]

1. Quando o teste é executado, Live Unit Testing indica que o `TestHasEmbeddedSpaces` método falhou, como mostra a ilustração a seguir:

   ::: moniker range="vs-2017"
   ![O Gerenciador de testes relatando um teste com falha](media/lut-start/test-failure.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![O Live Test Explorer relatando um teste com falha](media/lut-start/vs-2019/test-failure.png)
   ::: moniker-end

1. Selecione a janela que exibe o código da biblioteca. O Live Unit Testing expandiu a cobertura de código para o `HasEmbeddedSpaces` método. Ele também relata uma falha de teste adicionando um "🞩" vermelho nas linhas cobertas por testes com falha.

1. Passe o mouse sobre a linha com a assinatura do método `HasEmbeddedSpaces`. Live Unit Testing exibe uma dica de ferramenta que relata que o método é coberto por um teste, como mostra a ilustração a seguir:

   ![Live Unit Testing informações sobre um teste com falha](media/lut-start/test-failure-info-cs.png)

1. Selecione o teste **TestHasEmbeddedSpaces**. Live Unit Testing fornece algumas opções, como a execução de todos os testes e a depuração de todos os testes, como mostra a ilustração a seguir:

   ::: moniker range="vs-2017"
   ![Opções de Live Unit Testing para um teste com falha](media/lut-start/test-failure-options.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![Opções de Live Unit Testing para um teste com falha](media/lut-start/vs-2019/test-failure-options.png)
   ::: moniker-end

1. Selecione **depurar tudo** para depurar o teste com falha.

1. O Visual Studio executa o teste no modo de depuração.

   O teste atribui cada cadeia de caracteres em uma matriz a uma variável chamada `phrase` e a passa para o `HasEmbeddedSpaces` método. A execução do programa fica em pausa e invoca o depurador na primeira vez em que a expressão assert é `false`. A caixa de diálogo de exceção que resulta do valor inesperado na [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.istrue) chamada do método é mostrada na ilustração a seguir.

   ![Caixa de diálogo Live Unit Testing exceção](media/lut-start/exception-dialog-cs.png)

   Além disso, todas as ferramentas de depuração que o Visual Studio fornece estão disponíveis para nos ajudar a solucionar nosso teste com falha, como mostra a ilustração a seguir:

   ![Ferramentas de depuração do Visual Studio](media/lut-start/debugging-tools-cs.png)

   Observe que na janela **Autos** o valor da variável `phrase` é "Name\tDescription", que é o segundo elemento da matriz. O método de teste espera que `HasEmbeddedSpaces` retorne `true` ao receber essa cadeia de caracteres, mas ele retorna `false`. Evidentemente, ele não reconhece "\t", o caractere de tabulação, como um espaço inserido.

1. Selecione **depurar**  >  **continuar**, pressione **F5**ou clique no botão **continuar** na barra de ferramentas para continuar executando o programa de teste. Como ocorreu uma exceção sem tratamento, o teste foi encerrado.
Isso fornece informações suficientes para uma investigação preliminar do bug. Ou `TestHasEmbeddedSpaces` (a rotina de teste) fez uma suposição incorreta ou `HasEmbeddedSpaces` não reconhece corretamente todos os espaços inseridos.

1. Para diagnosticar e corrigir o problema, comece com o `StringLibrary.HasEmbeddedSpaces` método. Examine a comparação no método `HasEmbeddedSpaces`. Ele considera um espaço inserido como U+0020. No entanto, o padrão Unicode inclui vários outros caracteres de espaço. Isso sugere que o código da biblioteca testou um caractere de espaço em branco incorretamente.

1. Substitua a comparação de igualdade por uma chamada para o método <xref:System.Char.IsWhiteSpace%2A?displayProperty=fullName>:

    [!code-csharp[The TestHasEmbeddedSpaces test method](samples/snippets/csharp/lut-start/program2.cs#1)]

1. Live Unit Testing executa automaticamente o método de teste com falha.

   Live Unit Testing mostra que os resultados atualizados são exibidos, que também aparecem na janela Editor de código.

## <a name="see-also"></a>Veja também

- [Live Unit Testing no Visual Studio](live-unit-testing.md)
- [Perguntas frequentes sobre o Live Unit Testing](live-unit-testing-faq.md)

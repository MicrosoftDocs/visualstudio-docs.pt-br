---
title: Saiba como testar seu código com o Live Unit Testing no Visual Studio 2017 | Microsoft Docs
ms.date: 08/31/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio ALM
- Live Unit Testing
author: rpetrusha
ms.author: ronpet
ms.workload:
- dotnet
ms.openlocfilehash: 83507060295c294747f279dd32f96fe8b0a358fa
ms.sourcegitcommit: 96a6d1f16d06ca28d309d05b6e9fbd52f628cdbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40008415"
---
# <a name="get-started-with-live-unit-testing-in-visual-studio"></a>Introdução ao Live Unit Testing no Visual Studio

Quando você habilita o Live Unit Testing em uma solução do Visual Studio, ele representa visualmente a cobertura do teste e o status dos testes. Ele também executa testes dinamicamente sempre que você modifica o código e imediatamente notifica quando suas alterações causam falhas de teste.

O Live Unit Testing pode ser usado para testar soluções direcionadas ao .NET Framework ou ao .NET Core. Neste tutorial, você aprenderá a usar o Live Unit Testing, criando uma biblioteca de classes simples direcionada ao .NET Standard e criará um projeto do MSTest direcionado ao .NET Core para testá-lo.

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
A solução C# completa pode ser baixada do repositório [MicrosoftDocs/visualstudio-docs](https://github.com/MicrosoftDocs/visualstudio-docs/tree/master/docs/test/samples/csharp/UtilityLibraries/) no GitHub.
# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
A solução completa do Visual Basic pode ser baixada do repositório [MicrosoftDocs/visualstudio-docs](https://github.com/MicrosoftDocs/visualstudio-docs/tree/master/docs/test/samples/visual-basic/UtilityLibraries/) no GitHub.

---

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial requer que o Visual Studio 2017 Enterprise Edition versão 15.3 esteja instalado com a carga de trabalho do .NET Core 2.0.

## <a name="create-the-solution-and-the-class-library-project"></a>Criar a solução e o projeto de biblioteca de classes

Comece criando uma solução do Visual Studio chamada `UtilityLibraries` que consiste em um único projeto de biblioteca de classes do .NET Standard `StringLibrary`. Você pode escrever a `StringLibrary` em C# ou Visual Basic.

A solução é apenas um contêiner para um ou mais projetos. Para criar a solução, abra o Visual Studio 2017 e faça o seguinte:

1. Selecione **Arquivo** > **Novo** > **Projeto** no menu de nível superior do Visual Studio.

1. Na caixa de diálogo **Novo Projeto**, expanda o nó **Outros Tipos de Projeto** e selecione **Soluções do Visual Studio**. Selecione o modelo **Solução em Branco** no painel à direita e insira `UtilityLibraries` na caixa de texto **Nome**, como mostra a figura a seguir:

   ![A caixa de diálogo **Novo Projeto**](./media/lut-start/new-solution.png)

1. Selecione **OK** para criar a solução.

Agora que já criou a solução, você criará uma biblioteca de classes chamada `StringLibrary` que contém vários métodos de extensão para trabalhar com cadeias de caracteres.

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução `UtilityLibraries` e selecione **Adicionar** > **Novo Projeto**.

1. Na caixa de diálogo **Adicionar Novo Projeto** selecione o nó C# e, em seguida, selecione **.NET Standard**.

   > [!NOTE]
   > Como nossa biblioteca é direcionada ao .NET Standard e não a uma implementação específica do .NET, ela pode ser chamada de qualquer implementação do .NET que dê suporte a essa versão do .NET padrão. Para obter mais informações, confira [.NET Standard](/dotnet/standard/net-standard).

1. Selecione o modelo **Biblioteca de Classes (.NET Standard)** no painel à direita e insira `StringLibrary` na caixa de texto **Nome**, como mostra a figura a seguir:

   ![Caixa de diálogo **Adicionar Novo Projeto**](./media/lut-start/add-project-cs.png)

1. Selecione **OK** para criar o projeto.

1. Substitua todo o código existente na janela de código pelo código a seguir:

   [!code-csharp[StringLibrary source code](samples/csharp/utilitylibraries/stringlibrary/class1.cs)]

   `StringLibrary` tem três métodos estáticos:

      - `StartsWithUpper` retornará `true` se uma cadeia de caracteres começar com um caractere maiúsculo, caso contrário, retornará `false`.

      - `StartsWithLower` retornará `true` se uma cadeia de caracteres começar com um caractere minúsculo, caso contrário, retornará `false`.

      - `HasEmbeddedSpaces` retornará `true` se uma cadeia de caracteres contiver um caractere de espaço em branco inserido, caso contrário, retornará `false`.

1.  Selecione **Compilar** > **Compilar Solução** no menu de nível superior do Visual Studio. O Visual Studio deverá compilar a biblioteca com êxito.

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução `UtilityLibraries` e selecione **Adicionar** > **Novo Projeto**.

1. Na caixa de diálogo **Adicionar Novo Projeto** selecione o nó Visual Basic e, em seguida, selecione **.NET Standard**.

   > [!NOTE]
   > Como nossa biblioteca é direcionada ao .NET Standard e não a uma implementação específica do .NET, ela pode ser chamada de qualquer implementação do .NET que dê suporte a essa versão do .NET padrão. Para obter mais informações, confira [.NET Standard](/dotnet/standard/net-standard).

1. Selecione o modelo **Biblioteca de Classes (.NET Standard)** no painel à direita e insira `StringLibrary` na caixa de texto **Nome**, como mostra a figura a seguir:

   ![Caixa de diálogo **Adicionar Novo Projeto**](./media/lut-start/add-project-vb.png)

1. Selecione **OK** para criar o projeto.

1. Substitua todo o código existente na janela de código pelo código a seguir:

   [!code-vb[StringLibrary source code](samples/visual-basic/utilitylibraries/stringlibrary/class1.vb)]

   `StringLibrary` tem três métodos estáticos:

      - `StartsWithUpper` retornará `true` se uma cadeia de caracteres começar com um caractere maiúsculo, caso contrário, retornará `false`.

      - `StartsWithLower` retornará `true` se uma cadeia de caracteres começar com um caractere minúsculo, caso contrário, retornará `false`.

      - `HasEmbeddedSpaces` retornará `true` se uma cadeia de caracteres contiver um caractere de espaço em branco inserido, caso contrário, retornará `false`.

1. Clique com o botão direito do mouse no projeto StringLibrary no **Gerenciador de Soluções** e selecione **Propriedades**. Na guia **Aplicativo**, exclua o texto na caixa de texto **Namespace raiz**, como mostra a figura a seguir. O namespace raiz é definido pela [Instrução namespace](/dotnet/visual-basic/language-reference/statements/namespace-statement) no código-fonte.

   ![A caixa de diálogo Propriedades do Projeto de um projeto Visual Basic](./media/lut-start/vb-properties.png)

1.  Selecione **Compilar** > **Compilar Solução** no menu de nível superior do Visual Studio. O Visual Studio deverá compilar a biblioteca com êxito.

---

## <a name="create-the-test-project"></a>Criar um projeto de teste

A próxima etapa é criar o projeto de teste de unidade para testar a biblioteca `StringLibrary`. Crie testes de unidade, executando as seguintes etapas:

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução `UtilityLibraries` e selecione **Adicionar** > **Novo Projeto**.

1. Na caixa de diálogo **Adicionar Novo Projeto** selecione o nó C# e, em seguida, selecione **.NET Core**.

   > [!NOTE]
   > Você não precisa escrever os testes de unidade na mesma linguagem da biblioteca de classes.

1. Selecione o modelo **Projeto de Teste de Unidade (.NET Core)** no painel direito e insira `StringLibraryTests` na caixa de texto **Nome**, como mostra a figura a seguir:

   ![A caixa de diálogo **Adicionar Novo Projeto** do projeto de teste de unidade](./media/lut-start/add-unit-test-cs.png)

1. Selecione **OK** para criar o projeto.

   > [!NOTE]
   > Este tutorial de introdução usa o Live Unit Testing com o framework de teste do MSTest. Você também pode usar as estruturas de teste xUnit e NUnit.

1. O projeto de teste de unidade não pode acessar automaticamente a biblioteca de classes que ele está testando. Forneça acesso à biblioteca de teste adicionando uma referência ao projeto de biblioteca de classes. Para fazer isso, clique com o botão direito do mouse no projeto `StringLibraryTests` e selecione **Adicionar** > **Referência**. Na caixa de diálogo **Gerenciador de Referências**, verifique se a guia **Solução** está selecionada e selecione o projeto `StringLibrary`, conforme é mostrado na figura a seguir.

   ![A caixa de diálogo **Gerenciador de Referências**](./media/lut-start/add-reference.png)

1. Substitua o código de teste de unidade clichê que o modelo fornece pelo código a seguir:

   [!code-csharp[StringLibraryTest source code](samples/snippets/csharp/lut-start/unittest1.cs)]

1. Salve o projeto selecionando o ícone **Salvar** na barra de ferramentas.

1. Como o código de teste de unidade inclui alguns caracteres não ASCII, o Visual Studio exibe a caixa de diálogo a seguir para avisar que alguns caracteres serão perdidos se o arquivo for salvo em seu formato ASCII padrão. Escolha o botão **Salvar com Outra Codificação**.

   ![Escolha uma codificação de arquivo](media/lut-start/ascii-encoding.png)

1. Na lista suspensa **Codificação** da caixa de diálogo **Opções Avançadas de Salvamento**, escolha **Unicode (UTF-8 sem assinatura) – página de código 65001**, como mostra a figura a seguir:

   ![Escolhendo a codificação UTF-8](media/lut-start/utf8-encoding.png)

1. Compile o projeto de teste de unidade selecionando **Compilar** > **Recompilar Solução** no menu de nível superior do Visual Studio.

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução `UtilityLibraries` e selecione **Adicionar** > **Novo Projeto**.

1. Na caixa de diálogo **Adicionar Novo Projeto** selecione o nó Visual Basic e, em seguida, selecione **.NET Core**.

   > [!NOTE]
   > Você não precisa escrever os testes de unidade na mesma linguagem da biblioteca de classes.

1. Selecione o modelo **Projeto de Teste de Unidade (.NET Core)** no painel direito e insira `StringLibraryTests` na caixa de texto **Nome**, como mostra a figura a seguir:

   ![A caixa de diálogo **Adicionar Novo Projeto** do teste de unidade](./media/lut-start/add-unit-test-vb.png)

1. Selecione **OK** para criar o projeto.

   > [!NOTE]
   > Este tutorial de introdução usa o Live Unit Testing com o framework de teste do MSTest. Você também pode usar as estruturas de teste xUnit e NUnit.

1. O projeto de teste de unidade não pode acessar automaticamente a biblioteca de classes que ele está testando. Forneça acesso à biblioteca de teste adicionando uma referência ao projeto de biblioteca de classes. Para fazer isso, clique com o botão direito do mouse no projeto `StringLibraryTests` e selecione **Adicionar** > **Referência**. Na caixa de diálogo **Gerenciador de Referências**, verifique se a guia **Solução** está selecionada e selecione o projeto `StringLibrary`, conforme é mostrado na figura a seguir.

   ![A caixa de diálogo **Gerenciador de Referências**](./media/lut-start/add-reference.png)

1. Substitua o código de teste de unidade clichê que o modelo fornece pelo código a seguir:

   [!code-vb[StringLibraryTest source code](samples/snippets/visual-basic/lut-start/unittest1.vb)]

1. Salve o projeto selecionando o ícone **Salvar** na barra de ferramentas.

1. Como o código de teste de unidade inclui alguns caracteres não ASCII, o Visual Studio exibe a caixa de diálogo a seguir para avisar que alguns caracteres serão perdidos se o arquivo for salvo em seu formato ASCII padrão. Escolha o botão **Salvar com Outra Codificação**.

   ![Escolha uma codificação de arquivo](media/lut-start/ascii-encoding.png)

1. Na lista suspensa **Codificação** da caixa de diálogo **Opções Avançadas de Salvamento**, escolha **Unicode (UTF-8 sem assinatura) – página de código 65001**, como mostra a figura a seguir:

   ![Escolhendo a codificação UTF-8](media/lut-start/utf8-encoding.png)

1. Compile o projeto de teste de unidade com **Compilar** > **Recompilar Solução** no menu de nível superior do Visual Studio.

---

Você criou uma biblioteca de classes e também alguns testes de unidade para ela. Agora você terminou as etapas preliminares necessárias para usar o Live Unit Testing.

## <a name="enable-live-unit-testing"></a>Habilitar o Live Unit Testing

Até agora, embora você já tenha escrito os testes para a biblioteca de classes `StringLibrary`, eles ainda não foram executados. O Live Unit Testing executa-os automaticamente ao ser habilitado. Para isso, faça o seguinte:

1. Opcionalmente, selecione a janela de código que contém o código da `StringLibrary`. O código é *Class1.cs* para um projeto C# ou *Class1.vb* para um projeto Visual Basic. (Esta etapa permite inspecionar visualmente o resultado dos testes e a extensão da cobertura de código depois de habilitar o Live Unit Testing.)

1. Selecione **Teste** > **Live Unit Testing** > **Iniciar** no menu de nível superior do Visual Studio.

1. O Visual Studio inicia o Live Unit Testing, que executa automaticamente todos os seus testes.

Quando ele termina de executar os testes, o **Gerenciador de Testes** exibe os resultados gerais e o resultado dos testes individuais. Além disso, a janela de código exibe graficamente a cobertura de código de teste e o resultado dos testes. Como mostra a figura a seguir, os três testes foram executados com êxito. Ela também mostra que nossos testes cobriram todos os caminhos de código no método `StartsWithUpper` e que todos esses testes foram executados com êxito (o que é indicado pela marca de verificação verde "✓"). Finalmente, ele mostra que nenhum dos outros métodos da `StringLibrary` têm cobertura de código (o que é indicado por uma linha azul, "").

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
![O Gerenciador de Testes e a janela de código depois que o Service Fabric Explorer é iniciado](media/lut-start/lut-results-cs.png)

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
![O Gerenciador de Testes e a janela de código depois que o Service Fabric Explorer é iniciado](media/lut-start/lut-results-vb.png)

---

Você também pode obter informações mais detalhadas sobre a cobertura do teste e os resultados de teste selecionando um ícone de cobertura de código específico na janela de código. Para examinar este detalhe, faça o seguinte:

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. Clique na marca de verificação verde na linha em que está escrito `if (String.IsNullOrWhiteSpace(s))` no método `StartsWithUpper`. Como mostra a figura a seguir, o Live Unit Testing indica que três testes cobrem essa linha de código e que todos foram executadas com êxito.

   ![Cobertura de código para a instrução condicional 'if'](media/lut-start/code-coverage-cs1.png)

1. Clique na marca de verificação verde na linha em que está escrito `return Char.IsUpper(s[0])` no método `StartsWithUpper`. Como mostra a figura a seguir, o Live Unit Testing indica que somente dois cobrem essa linha de código e que todos foram executadas com êxito.

   ![Cobertura de código para a instrução return](media/lut-start/code-coverage-cs2.png)

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. Clique na marca de verificação verde na linha em que está escrito `If (String.IsNullOrWhiteSpace(s)) Then` no método `StartsWithUpper`. Como mostra a figura a seguir, o Live Unit Testing indica que três testes cobrem essa linha de código e que todos foram executadas com êxito.

   ![Cobertura de código para a instrução condicional 'if'](media/lut-start/code-coverage-vb1.png)

1. Clique na marca de verificação verde na linha em que está escrito `Return Char.IsUpper(s(0))` no método `StartsWithUpper`. Como mostra a figura a seguir, o Live Unit Testing indica que somente dois cobrem essa linha de código e que todos foram executadas com êxito.

   ![Cobertura de código para a instrução return](media/lut-start/code-coverage-vb2.png)

---

A questão mais importante que o Live Unit Testing identifica é uma cobertura de código incompleta. Isso será abordado na próxima seção.

## <a name="expand-test-coverage"></a>Expandir a cobertura do teste

Nesta seção, você estenderá os testes de unidade para o método `StartsWithLower`. Enquanto você estiver fazendo isso, o Live Unit Testing continuará a testar o código dinamicamente.

Para estender a cobertura de código para o método `StartsWithLower`, faça o seguinte:

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. Adicione os seguintes métodos `TestStartsWithLower` e `TestDoesNotStartWithLower` no arquivo de código-fonte do teste do projeto:

    [!code-csharp[StringLibraryTest source code](samples/snippets/csharp/lut-start/unittest2.cs#1)]

1. Modifique o método `DirectCallWithNullOrEmpty` adicionando o seguinte código imediatamente após a chamada de método [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.isfalse).

    [!code-csharp[StringLibraryTest source code](samples/snippets/csharp/lut-start/unittest2.cs#2)]

1. O Live Unit Testing executa automaticamente os testes novos e modificados quando você modifica o código-fonte. Como mostra a figura a seguir do **Gerenciador de Testes**, todos os testes, incluindo os dois que você adicionou e o que você modificou, tiveram êxito.

   ![O Gerenciador de Testes após a expansão da cobertura do teste.](media/lut-start/test-dynamic.png)

1. Alterne para a janela que contém o código-fonte da classe `StringLibrary`. Agora, o Live Unit Testing mostra que a cobertura de código foi estendida para o método `StartsWithLower`.

    ![Cobertura de código do método StartsWithLower](media/lut-start/lut-extended-cs.png)

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. Adicione os seguintes métodos `TestStartsWithLower` e `TestDoesNotStartWithLower` no arquivo de código-fonte do teste do projeto:

    [!code-vb[StringLibraryTest source code](samples/snippets/visual-basic/lut-start/unittest2.vb#1)]

1. Modifique o método `DirectCallWithNullOrEmpty` adicionando o seguinte código imediatamente após a chamada de método [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.isfalse).

    [!code-vb[StringLibraryTest source code](samples/snippets/visual-basic/lut-start/unittest2.vb#2)]

1. O Live Unit Testing executa automaticamente os testes novos e modificados quando você modifica o código-fonte. Como mostra a figura a seguir do **Gerenciador de Testes**, todos os testes, incluindo os dois que você adicionou e o que você modificou, tiveram êxito.

   ![O Gerenciador de Testes após a expansão da cobertura do teste.](media/lut-start/test-dynamic.png)

1. Alterne para a janela que contém o código-fonte da classe `StringLibrary`. Agora, o Live Unit Testing mostra que a cobertura de código foi estendida para o método `StartsWithLower`.

    ![Cobertura de código do StartsWithLower](media/lut-start/lut-extended-vb.png)

---

Em alguns casos, os testes com êxito no **Gerenciador de Testes** pode ficar esmaecidos. Isso indica que um teste está em execução no momento ou que o teste não foi executado novamente porque não houve nenhuma alteração no código que pudesse afetá-lo desde sua última execução.

Até agora, todos os nossos testes tiveram êxito. Na próxima seção, vamos examinar como você pode tratar uma falha de teste.

## <a name="handle-a-test-failure"></a>Lidar com uma falha de teste

Nesta seção, você vai explorar como é possível usar o Live Unit Testing para identificar, corrigir e solucionar problemas de falhas de teste. Você fará isso expandindo a cobertura do teste para o método `HasEmbeddedSpaces`.

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. Adicione o seguinte método ao arquivo de teste:

    [!code-csharp[The TestHasEmbeddedSpaces test method](samples/snippets/csharp/lut-start/unittest2.cs#3)]

1. Quando o teste for executado, o Live Unit Testing indicará que o método `TestHasEmbeddedSpaces` falhou, como mostra a figura a seguir:

   ![O Gerenciador de Testes relatando um teste com falha.](media/lut-start/test-failure.png)

1. Selecione a janela que exibe o código da biblioteca. Observe que o Live Unit Testing expandiu cobertura de código para o método `HasEmbeddedSpaces`. Ele também relata uma falha de teste adicionando um "🞩" vermelho nas linhas cobertas por testes com falha.

1. Passe o mouse sobre a linha com a assinatura do método `HasEmbeddedSpaces`. O Live Unit Testing exibe uma dica de ferramenta que relata que o método está coberto por um teste, como mostra a figura a seguir:

   ![Informações do Live Unit Testing sobre um teste com falha.](media/lut-start/test-failure-info-cs.png)

1. Selecione o teste **TestHasEmbeddedSpaces**. Observe que o Live Unit Testing oferece várias opções, como executar todos os testes, executar testes selecionados, depurar todos os testes e depurar testes selecionados, como mostra a figura a seguir:

   ![Opções do Live Unit Testing para um teste com falha.](media/lut-start/test-failure-options.png)

1. Selecione **Depurar Selecionado** para depurar o teste com falha.

1. O Visual Studio executa o teste no modo de depuração. Nosso teste atribui cada cadeia de caracteres em uma matriz a uma variável chamada `phrase` e a passa o método `HasEmbeddedSpaces`. A execução do programa fica em pausa e invoca o depurador na primeira vez em que a expressão assert é `false`. A caixa de diálogo de exceção que resulta do valor inesperado na chamada de método [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.istrue) é mostrada na figura a seguir.

   ![Caixa de diálogo de exceção do Live Unit Testing.](media/lut-start/exception-dialog-cs.png)

   Além disso, todas as ferramentas de depuração que o Visual Studio fornece estão disponíveis para ajudar a solucionar problemas de testes com falha, como mostra a figura a seguir:

   ![Ferramentas depuração do Visual Studio.](media/lut-start/debugging-tools-cs.png)

   Observe que na janela **Autos** o valor da variável `phrase` é "Name\tDescription", que é o segundo elemento da matriz. O método de teste espera que `HasEmbeddedSpaces` retorne `true` ao receber essa cadeia de caracteres, mas ele retorna `false`. Evidentemente, ele não reconhece "\t", o caractere de tabulação, como um espaço inserido.

1. Selecione **Depurar** > **Continuar**, pressione **F5** ou clique no botão **Continuar** na barra de ferramentas para continuar executando o programa de teste. Como ocorreu uma exceção sem tratamento, o teste foi encerrado.

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. Adicione o seguinte método ao arquivo de teste:

    [!code-vb[The TestHasEmbeddedSpaces test method](samples/snippets/visual-basic/lut-start/unittest2.vb#3)]

1. Quando o teste for executado, o Live Unit Testing indicará que o método `TestHasEmbeddedSpaces` falhou, como mostra a figura a seguir:

   ![O Gerenciador de Testes relatando um teste com falha.](media/lut-start/test-failure.png)

1. Selecione a janela que exibe o código da biblioteca. Observe que o Live Unit Testing expandiu cobertura de código para o método `HasEmbeddedSpaces`. Ele também relata uma falha de teste adicionando um "🞩" vermelho nas linhas cobertas por testes com falha.

1. Passe o mouse sobre a linha com a assinatura do método `HasEmbeddedSpaces`. O Live Unit Testing exibe uma dica de ferramenta que relata que o método está coberto por um teste, como mostra a figura a seguir:

   ![Informações do Live Unit Testing sobre um teste com falha.](media/lut-start/test-failure-info-vb.png)

1. Selecione o teste **TestHasEmbeddedSpaces**. Observe que o Live Unit Testing oferece várias opções, como executar todos os testes, executar testes selecionados, depurar todos os testes e depurar testes selecionados, como mostra a figura a seguir:

   ![Opções do Live Unit Testing para um teste com falha.](media/lut-start/test-failure-options.png)

1. Selecione **Depurar Selecionado** para depurar o teste com falha.

1. O Visual Studio executa o teste no modo de depuração. Nosso teste atribui cada cadeia de caracteres em uma matriz a uma variável chamada `phrase` e a passa o método `HasEmbeddedSpaces`. A execução do programa fica em pausa e invoca o depurador na primeira vez em que a expressão assert é `false`. A caixa de diálogo de exceção que resulta do valor inesperado na chamada de método [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.istrue) é mostrada na figura a seguir.

   ![Caixa de diálogo de exceção do Live Unit Testing.](media/lut-start/exception-dialog-vb.png)

   Além disso, todas as ferramentas de depuração que o Visual Studio fornece estão disponíveis para ajudar a solucionar problemas de testes com falha, como mostra a figura a seguir:

   ![Ferramentas depuração do Visual Studio.](media/lut-start/debugging-tools-vb.png)

   Observe que na janela **Autos** o valor da variável `phrase` é "Name" + vbTab + "Description", que é o segundo elemento da matriz. O método de teste espera que `HasEmbeddedSpaces` retorne `true` ao receber essa cadeia de caracteres, mas ele retorna `false`. Evidentemente, ele não reconhece o caractere de tabulação como um espaço inserido.

1. Selecione **Depurar** > **Continuar**, pressione **F5** ou clique no botão **Continuar** na barra de ferramentas para continuar executando o programa de teste. Como ocorreu uma exceção sem tratamento, o teste foi encerrado.

---

Isso fornece informações suficientes para uma investigação preliminar do bug. Ou `TestHasEmbeddedSpaces` (a rotina de teste) fez uma suposição incorreta ou `HasEmbeddedSpaces` não reconhece corretamente todos os espaços inseridos. Para diagnosticar e corrigir o problema, comece com o método `StringLibrary.HasEmbeddedSpaces`:

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
1. Examine a comparação no método `HasEmbeddedSpaces`. Ele considera um espaço inserido como U+0020. No entanto, o padrão Unicode inclui vários outros caracteres de espaço. Isso sugere que o código da biblioteca testou um caractere de espaço em branco incorretamente.

1. Substitua a comparação de igualdade por uma chamada para o método <xref:System.Char.IsWhiteSpace%2A?displayProperty=fullName>:

    [!code-csharp[The TestHasEmbeddedSpaces test method](samples/snippets/csharp/lut-start/program2.cs#1)]

1. O Live Unit Testing executa novamente o método de teste com falha e atualiza os resultados na janela de código e no **Gerenciador de Testes** automaticamente, como mostra a figura a seguir:

    ![O teste de HasEmbeddedSpaces com êxito.](media/lut-start/test-success-cs.png)

# <a name="visual-basictabvisual-basic"></a>[Visual Basic](#tab/visual-basic)
1. Examine a comparação no método `HasEmbeddedSpaces`. Ele considera um espaço inserido como U+0020. No entanto, o padrão Unicode inclui vários outros caracteres de espaço. Isso sugere que o código da biblioteca testou um caractere de espaço em branco incorretamente.

1. Substitua a comparação de igualdade por uma chamada para o método <xref:System.Char.IsWhiteSpace%2A?displayProperty=fullName>:

    [!code-vb[The TestHasEmbeddedSpaces test method](samples/snippets/visual-basic/lut-start/class2.vb#1)]

1. O Live Unit Testing executa novamente o método de teste com falha e atualiza os resultados na janela de código e no **Gerenciador de Testes** automaticamente, como mostra a figura a seguir:

    ![O teste de HasEmbeddedSpaces com êxito.](media/lut-start/test-success-vb.png)

---

## <a name="see-also"></a>Consulte também
- [Live Unit Testing no Visual Studio](live-unit-testing.md)
- [Perguntas frequentes sobre o Live Unit Testing](live-unit-testing-faq.md)

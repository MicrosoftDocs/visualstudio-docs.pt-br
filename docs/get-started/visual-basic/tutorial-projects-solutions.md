---
title: 'Tutorial: Projetos e soluções usando Visual Basic'
description: Saiba como criar uma solução e um projeto no Visual Studio como um Visual Basic desenvolvedor.
ms.date: 12/12/2018
ms.technology: vs-ide-general
ms.custom:
- get-started
- SEO-VS-2020
ms.topic: tutorial
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 4f27973fcfb76d019cff31787b117f05f8266ad8
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308175"
---
# <a name="learn-about-projects-and-solutions-using-visual-basic"></a>Saiba mais sobre projetos e soluções usando Visual Basic

Neste artigo introdutório, exploraremos o que significa criar uma *solução* e um *projeto* no Visual Studio. Uma solução é um contêiner usado para organizar um ou mais projetos de código relacionados, por exemplo, um projeto de biblioteca de classes e um projeto de teste correspondente. Vamos examinar as propriedades de um projeto e alguns dos arquivos que ele pode conter. Também criaremos uma referência de um projeto a outro.

::: moniker range="vs-2017"

> [!TIP]
> Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2019"

> [!TIP]
> Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2022"

> [!TIP]
> Se você ainda não tiver instalado o Visual Studio Preview, acesse a página de downloads do [Visual Studio 2022 Preview](https://visualstudio.microsoft.com/vs/preview/vs2022) para instalá-lo gratuitamente.

::: moniker-end

Desenvolveremos uma solução e um projeto do zero como um exercício educacional para compreendermos o conceito de um projeto. Em seu uso geral do Visual Studio, você provavelmente usará alguns dos vários *modelos* de projeto oferecidos pelo Visual Studio quando estiver criando um projeto.

> [!NOTE]
> As soluções e os projetos não precisam desenvolver aplicativos no Visual Studio. Você também pode apenas abrir uma pasta que contém o código e começar a codificar, compilar e depurar. Por exemplo, se você clonar um repositório [GitHub,](https://github.com/) ele poderá não conter Visual Studio e soluções. Para obter mais informações, consulte [Desenvolver código no Visual Studio sem projetos nem soluções](../../ide/develop-code-in-visual-studio-without-projects-or-solutions.md).

## <a name="solutions-and-projects"></a>Soluções e projetos

Apesar do nome, uma solução não é uma "resposta". Uma solução é apenas um contêiner usado pelo Visual Studio para organizar um ou mais projetos relacionados. Quando você abre uma solução no Visual Studio, ele carrega automaticamente todos os projetos que a solução contém.

### <a name="create-a-solution"></a>Criar uma solução

Vamos iniciar nossa exploração criando uma solução vazia. Depois de se familiarizar com o Visual Studio, provavelmente, você não precisará criar soluções vazias com muita frequência. Quando você cria um projeto, o Visual Studio cria automaticamente uma solução para hospedar o projeto, caso não haja uma solução já aberta.

::: moniker range="vs-2017"

1. Abra o Visual Studio.

1. Na barra de menus, escolha **Arquivo** > **Novo** > **Projeto**.

   A caixa de diálogo **Novo Projeto** será aberta.

1. No painel esquerdo, expanda a opção **Outros Tipos de Projetos** e, então, selecione **Soluções do Visual Studio**. No painel central, escolha o modelo **Solução em Branco**. Chame sua solução de **QuickSolution** e escolha **OK**.

   ![Modelo de solução em branco no Visual Studio](../media/tutorial-projects-new-solution.png)

   A **Página Inicial** é fechada e uma solução é exibida no **Gerenciador de Soluções** do lado direito da janela do Visual Studio. Você provavelmente usará o **Gerenciador de Soluções** muitas vezes para navegar pelo conteúdo de seus projetos.

::: moniker-end

::: moniker range=">=vs-2019"

1. Abra o Visual Studio.

2. Na janela inicial, escolha **Criar um novo projeto.**

3. Na página **Criar um novo projeto**, insira **solução em branco** na caixa de pesquisa, selecione o modelo **Solução em Branco** e escolha **Avançar**.

   ![Modelo de Solução em branco no Visual Studio 2019](../media/vs-2019/tutorial-projects-blank-solution-template.png)

4. Nomeie a solução como **QuickSolution** e escolha **Criar**.

   A solução aparece no **Gerenciador de Soluções** do lado direito da janela do Visual Studio. Você provavelmente usará o **Gerenciador de Soluções** muitas vezes para navegar pelo conteúdo de seus projetos.

::: moniker-end

### <a name="add-a-project"></a>Adicionar um projeto

Agora vamos adicionar nosso primeiro projeto à solução. Vamos começar com um projeto vazio e adicionar os itens necessários ao projeto.

::: moniker range="vs-2017"

1. No menu de contexto ou clique com o botão direito do mouse da Solução **'QuickSolution'** **no Gerenciador de Soluções**, escolha **Adicionar** > **Novo Projeto**.

   A caixa de diálogo **Adicionar Novo Projeto** é aberta.

1. No painel esquerdo, expanda **Visual Basic** e escolha **Área de Trabalho do Windows**. Em seguida, no painel central, selecione o modelo **Projeto Vazio (.NET Framework)**. Nomeia o **projeto QuickDate** e, em seguida, escolha o **botão OK.**

   Um projeto chamado QuickDate aparece abaixo da solução no **Gerenciador de Soluções**. Atualmente, ele contém um único arquivo chamado *App.config*.

   > [!NOTE]
   > Se a opção **Visual Basic** não for exibida no painel esquerdo da caixa de diálogo, você precisará instalar a *carga de trabalho***Desenvolvimento para desktop com .NET** do Visual Studio. O Visual Studio usa a instalação baseada em carga de trabalho para instalar somente os componentes necessários para o tipo de desenvolvimento realizado. Uma maneira fácil de instalar uma nova carga de trabalho é escolher o link **Abrir Instalador do Visual Studio** no canto inferior esquerdo da caixa de diálogo **Adicionar Novo Projeto**. Após o início do Instalador do Visual Studio, escolha a carga de trabalho **Desenvolvimento para área de trabalho em .NET** e, em seguida, o botão **Modificar**.
   >
   > ![Abrir o link do Instalador do Visual Studio](media/tutorial-projects-open-installer-vb.png)

::: moniker-end

::: moniker range=">=vs-2019"

1. No menu de contexto ou clique com o botão direito do mouse da Solução **'QuickSolution'** **no Gerenciador de Soluções**, escolha **Adicionar** > **Novo Projeto**.

   Uma caixa de diálogo é aberta com o título **Adicionar um novo projeto**.

1. Insira o texto **vazio** na caixa de pesquisa na parte superior e, em seguida, selecione **Visual Basic** em **Idioma**.

1. Selecione o modelo **Projeto Vazio (.NET Framework)** e, em seguida, **Avançar**.

1. Nomeie o projeto **QuickDate** e, em seguida, escolha **Criar**.

   Um projeto chamado QuickDate aparece abaixo da solução no **Gerenciador de Soluções**. Atualmente, ele contém um único arquivo chamado *App.config*.

   > [!NOTE]
   > Se você não vir o modelo **Projeto Vazio (.NET Framework)**, será necessário instalar a **carga de trabalho** do Visual Studio de *desenvolvimento para área de trabalho do .NET*. O Visual Studio usa a instalação baseada em carga de trabalho para instalar somente os componentes necessários para o tipo de desenvolvimento realizado. Uma maneira fácil de instalar uma nova carga de trabalho ao criar um projeto é escolher o link **Instalar mais ferramentas e recursos** no texto que informa **Não encontra o que você está procurando?**. Após o início do Instalador do Visual Studio, escolha a carga de trabalho **Desenvolvimento para área de trabalho em .NET** e, em seguida, o botão **Modificar**.
   >
   > ![Link do instalador no Visual Studio 2019](../media/vs-2019/tutorial-projects-open-installer.png)

::: moniker-end

## <a name="add-an-item-to-the-project"></a>Adicionar um item ao projeto

Temos um projeto vazio. Vamos adicionar um arquivo de código.

1. No menu de clique com o botão direito do mouse ou de contexto do projeto **QuickDate** no **Gerenciador de Soluções**, escolha **Adicionar** > **Novo Item**.

   A **caixa de diálogo Adicionar Novo** Item é aberta.

1. Expanda **Itens Comuns** e, em seguida, escolha **Código**. No painel central, escolha o modelo de item **Classe**. Nomeia a **classe Calendar** e, em seguida, escolha o **botão** Adicionar.

   Um arquivo chamado *Calendar.vb* é adicionado ao projeto. O *.vb* no final é a extensão de arquivo fornecida a arquivos de código Visual Basic. O arquivo é exibido na hierarquia do projeto visual no **Gerenciador de Soluções** e seu conteúdo é aberto no editor.

1. Substitua o conteúdo do arquivo *Calendar.vb* pelo seguinte código:

   ```vb
   Class Calendar
       Public Shared Function GetCurrentDate() As Date
           Return DateTime.Now.Date
       End Function
   End Class
   ```

   A classe `Calendar` contém uma única função, `GetCurrentDate`, que retorna a data atual.

1. Abra as propriedades do projeto clicando duas vezes em **Meu Projeto** no **Gerenciador de Soluções**. Na guia **Aplicativo**, altere **Tipo de aplicativo** para **Biblioteca de Classes**. Essa etapa é necessária compilar o projeto com êxito.

1. Compile o projeto clicando com o botão direito do mouse em **QuickDate** no **Gerenciador de Soluções** e escolhendo **Compilar**. Você deverá ver uma mensagem de build bem-sucedido na Janela de **Saída**.

## <a name="add-a-second-project"></a>Adicionar um segundo projeto

É comum que as soluções contenham mais de um projeto e que, geralmente, esses projetos referenciem uns aos outros. Alguns projetos em uma solução podem ser bibliotecas de classes, alguns aplicativos executáveis e outros podem ser projetos de teste de unidade ou sites.

Vamos adicionar um projeto de teste de unidade em nossa solução. Desta vez, começaremos com um modelo de projeto, de modo que não precisemos adicionar outro arquivo de código ao projeto.

1. Ao clicar com o botão direito do mouse ou no menu de contexto da **Solução ‘QuickSolution’** no **Gerenciador de Soluções**, escolha **Adicionar** > **Novo Projeto**.

::: moniker range="Vs-2017"

2. No painel esquerdo, expanda a opção **Visual Basic** e escolha a categoria **Teste**. No painel central, escolha o modelo de projeto **Projeto de Teste de Unidade (.NET Framework)**. Nomeie o projeto **QuickTest** e escolha **OK**.

   Um segundo projeto é adicionado ao **Gerenciador de Soluções** e um arquivo chamado *UnitTest1.vb* é aberto no editor.

   ![Gerenciador de Soluções do Visual Studio com dois projetos](media/tutorial-projects-solution-explorer-vb.png)

::: moniker-end

::: moniker range=">=vs-2019"

2. Na caixa de diálogo **Adicionar um novo projeto**, insira o texto **teste de unidade** na caixa de pesquisa na parte superior e, em seguida, selecione **Visual Basic** em **Idioma**.

3. Escolha o modelo de **Projeto de Teste de Unidade (.NET Framework)** e escolha **Avançar**.

4. Nomeie o projeto **QuickTest** e escolha **Criar**.

   Um segundo projeto é adicionado ao **Gerenciador de Soluções** e um arquivo chamado *UnitTest1.vb* é aberto no editor.

::: moniker-end

## <a name="add-a-project-reference"></a>Adicionar uma referência ao projeto

Vamos usar o novo projeto de teste de unidade para testar nosso método no projeto **QuickDate**. Portanto, precisamos adicionar uma referência a esse projeto. Isso cria uma *dependência de build* entre os dois projetos, o que significa que quando a solução é criada, **QuickDate** é criado antes dependência **QuickTest**.

1. Escolha o **nó Referências** no projeto **QuickTest** e, no menu de contexto ou clique com o botão direito do mouse, **escolha Adicionar Referência**.

   ![Adicionar menu de referência](media/tutorial-projects-add-reference-vb.png)

   A caixa de diálogo **Gerenciador de Referências** é aberta.

1. No painel esquerdo, expanda **Projetos** e escolha **Solução**. No painel central, escolha a caixa de seleção ao lado de **QuickDate** e, em seguida, escolha o botão **OK**.

   Uma referência ao projeto **QuickDate** será adicionada.

## <a name="add-test-code"></a>Adicionar código de teste

1. Agora vamos adicionar o código de teste para o arquivo de código do Visual Basic. Substitua o conteúdo do *UnitTest1.vb* pelo seguinte código.

   ```vb
   <TestClass()> Public Class UnitTest1

       <TestMethod()> Public Sub TestGetCurrentDate()
           Assert.AreEqual(Date.Now.Date, QuickDate.Calendar.GetCurrentDate())
       End Sub

   End Class
   ```

   Você verá uma linha sinuosa vermelha em alguns dos códigos. Nós corrigiremos esse erro ao tornar o projeto de teste um [assembly amigável](/dotnet/visual-basic/programming-guide/concepts/assemblies-gac/friend-assemblies) para o projeto **QuickDate**.

1. De volta ao projeto **QuickDate**, abra o arquivo *Calendar.vb* caso ele ainda não esteja aberto e adicione a [instrução Imports](/dotnet/visual-basic/language-reference/statements/imports-statement-net-namespace-and-type) a seguir e o atributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> para resolver o erro no projeto de teste.

   ```vb
   Imports System.Runtime.CompilerServices

   <Assembly: InternalsVisibleTo("QuickTest")>
   ```

   O arquivo de código deve ter esta aparência:

   ![código do Visual Basic](media/tutorial-projects-code-vb.png)

## <a name="project-properties"></a>Propriedades do projeto

A linha no arquivo *Calendar.vb* que contém o atributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> referencia o nome do assembly (nome de arquivo) do projeto **QuickTest**. O nome do assembly pode não ser sempre o mesmo que o nome do projeto. Para localizar o nome do assembly de um projeto, abra as propriedades do projeto.

1. No **Gerenciador de Soluções**, selecione o projeto **QuickTest**. Ao clicar com o botão direito do mouse ou no menu de contexto, selecione **Propriedades** ou pressione **Alt**+**Enter**. (Você também pode clicar duas vezes em **Meu Projeto** no **Gerenciador de Soluções**.)

   As *páginas de propriedades* do projeto são abertas na **guia** Aplicativo. As páginas de propriedades contêm várias configurações para o projeto. Observe que o nome do assembly do projeto **QuickTest** é, de fato, “QuickTest”. Caso deseje alterá-lo, este é o local em que você poderá fazer isso. Assim, quando você compilar o projeto de teste, o nome do arquivo binário resultante será alterado de *QuickTest.dll* para o que você escolher.

   ![Propriedades do projeto](../media/tutorial-projects-properties.png)

1. Explore algumas das outras guias das páginas de propriedades do projeto, como **Compilar** e **Configurações**. Essas guias são diferentes para diferentes tipos de projetos.

## <a name="optional-run-the-test"></a>(Opcional) Executar o teste

Se você quiser verificar se o teste de unidade está funcionando, escolha **Executar** Todos os Testes na  >    >   barra de menus. Uma janela chamada **Gerenciador de Testes** será aberta e você verá que o teste **TestGetCurrentDate** será aprovado.

![Gerenciador de Testes no Visual Studio mostrando a aprovação no teste](../media/tutorial-projects-test-explorer.png)

> [!TIP]
> Se o **Gerenciador de Testes** não abrir automaticamente, abra-o escolhendo **Teste** > **Windows** > **Gerenciador de Testes** na barra de menus.

## <a name="next-steps"></a>Próximas etapas

Caso deseje explorar ainda mais o Visual Studio, considere a possibilidade de criar um aplicativo seguindo um dos [tutoriais do Visual Basic](index.yml).

## <a name="see-also"></a>Confira também

- [Criar projetos e soluções](../../ide/creating-solutions-and-projects.md)
- [Gerenciar propriedades do projeto e da solução](../../ide/managing-project-and-solution-properties.md)
- [Gerenciar referências em um projeto](../../ide/managing-references-in-a-project.md)
- [Desenvolver código no Visual Studio sem projetos nem soluções](../../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)
- [Visão geral do IDE do Visual Studio](../../get-started/visual-studio-ide.md)

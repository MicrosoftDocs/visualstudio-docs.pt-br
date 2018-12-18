---
title: Introdução a projetos e soluções
ms.date: 12/11/2017
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: tutorial
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4a4967f687f214e544aa65526144803ce31e99d7
ms.sourcegitcommit: 0cdd8e8a53fb4fd5e869f07c35204419fa12783d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53159328"
---
# <a name="learn-about-projects-and-solutions"></a>Saiba mais sobre projetos e soluções

Neste artigo introdutório, exploraremos o que significa criar uma *solução* e um *projeto* no Visual Studio. Uma solução é um contêiner que é usado para organizar um ou mais projetos de código relacionados, por exemplo, uma biblioteca de classes e um projeto de teste correspondente. Vamos examinar as propriedades de um projeto e alguns dos arquivos que ele pode conter. Também criaremos uma referência de um projeto a outro.

Se você ainda não tiver instalado o Visual Studio, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) para instalá-lo gratuitamente.

Desenvolveremos uma solução e um projeto do zero como um exercício educacional para compreendermos o conceito de um projeto. Em seu uso geral do Visual Studio, você provavelmente usará alguns dos vários *modelos* de projeto oferecidos pelo Visual Studio quando estiver criando um projeto.

> [!NOTE]
> As soluções e os projetos não precisam desenvolver aplicativos no Visual Studio. Você também pode apenas abrir uma pasta que contém o código e começar a codificar, compilar e depurar. Por exemplo, se você clonar um repositório [GitHub](https://github.com/), ele poderá não conter projetos nem soluções do Visual Studio. Para obter mais informações, consulte [Desenvolver código no Visual Studio sem projetos nem soluções](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md).

## <a name="solutions-and-projects"></a>Soluções e projetos

As soluções são contêineres usados pelo Visual Studio para organizar um ou mais projetos relacionados. Quando você abre uma solução no Visual Studio, ele automaticamente carrega todos os projetos que ela contém.

### <a name="create-a-solution"></a>Criar uma solução

Vamos iniciar nossa exploração criando uma solução vazia. Depois de se familiarizar com o Visual Studio, provavelmente, você não precisará criar soluções vazias com muita frequência. Quando você cria um projeto, o Visual Studio cria automaticamente uma solução para hospedar o projeto, caso não haja uma solução já aberta.

1. Abra o Visual Studio.

1. Na barra de menus, que é a linha de menus, como **Arquivo** e **Editar**, escolha **Arquivo** > **Novo** > **Projeto**.

   A caixa de diálogo **Novo Projeto** é aberta.

1. No painel esquerdo, expanda a opção **Outros Tipos de Projetos** e, então, selecione **Soluções do Visual Studio**. No painel central, escolha o modelo **Solução em Branco**. Nomeie a solução **QuickSolution** e, em seguida, escolha o botão **OK**.

   ![Modelo de solução em branco no Visual Studio](media/tutorial-projects-new-solution.png)

   A **Página Inicial** é fechada e uma solução é exibida no **Gerenciador de Soluções** do lado direito da janela do Visual Studio. Você provavelmente usará o **Gerenciador de Soluções** muitas vezes para navegar pelo conteúdo de seus projetos.

### <a name="add-a-project"></a>Adicionar um projeto

Agora vamos adicionar nosso primeiro projeto à solução. Vamos começar com um projeto vazio e adicionar os itens necessários ao projeto.

1. Ao clicar com o botão direito do mouse ou no menu de contexto da **Solução ‘QuickSolution’** do **Gerenciador de Soluções**, escolha **Adicionar** > **Novo Projeto**.

   A caixa de diálogo **Adicionar Novo Projeto** é aberta.

1. No painel esquerdo, expanda **Visual C#** e escolha **Área de Trabalho do Windows**. Em seguida, no painel central, selecione o modelo **Projeto Vazio (.NET Framework)**. Nomeie o projeto **QuickDate** e, em seguida, escolha o botão **OK**.

   Um projeto chamado QuickDate é exibido abaixo da solução no **Gerenciador de Soluções**. Atualmente, ele contém um único arquivo chamado *App.config*.

   > [!NOTE]
   > Se a opção **Visual C#** não for exibida no painel esquerdo da caixa de diálogo, será necessário instalar a *carga de trabalho* **Desenvolvimento para desktop do .NET**. O Visual Studio usa a instalação baseada em carga de trabalho para instalar somente os componentes necessários para o tipo de desenvolvimento realizado. Uma maneira fácil de instalar uma nova carga de trabalho é escolher o link **Abrir Instalador do Visual Studio** no canto inferior esquerdo da caixa de diálogo **Adicionar Novo Projeto**. Depois que o Instalador do Visual Studio for iniciado, escolha a carga de trabalho **Desenvolvimento para desktop do .NET** e, em seguida, o botão **Modificar**.

   ![Abrir o link do Instalador do Visual Studio](media/tutorial-projects-open-installer.png)

## <a name="add-an-item-to-the-project"></a>Adicionar um item ao projeto

Temos um projeto vazio. Vamos adicionar um arquivo de código.

1. No menu de clique com o botão direito do mouse ou de contexto do projeto **QuickDate** no **Gerenciador de Soluções**, escolha **Adicionar** > **Novo Item**.

   A caixa de diálogo **Adicionar Novo Item** é aberta.

1. Expanda a opção **Itens do Visual C#** e, em seguida, escolha **Código**. No painel central, escolha o modelo de item **Classe**. Nomeie a classe **Calendar** e, em seguida, escolha o botão **Adicionar**.

   Um arquivo chamado *Calendar.cs* é adicionado ao projeto. O *.cs* no final é a extensão de arquivo que é fornecida aos arquivos de código C#. O arquivo é exibido na hierarquia do projeto visual no **Gerenciador de Soluções** e seu conteúdo é aberto no editor.

1. Substitua o conteúdo do arquivo *Calendar.cs* pelo seguinte código:

   ```csharp
   using System;

   namespace QuickDate
   {
       internal class Calendar
       {
           static void Main(string[] args)
           {
               DateTime now = GetCurrentDate();
               Console.WriteLine($"Today's date is {now}");
               Console.ReadLine();
           }

           internal static DateTime GetCurrentDate()
           {
               return DateTime.Now.Date;
           }
       }
   }
   ```

   Você não precisa entender o que o código faz, mas se quiser, execute o programa pressionando **Ctrl**+**F5** e veja que ele imprime a data de hoje na janela do console (ou na saída padrão).

## <a name="add-a-second-project"></a>Adicionar um segundo projeto

É comum que as soluções contenham mais de um projeto e que, geralmente, esses projetos façam referência uns aos outros. Alguns projetos em uma solução podem ser bibliotecas de classes, alguns aplicativos executáveis e outros podem ser projetos de teste de unidade ou sites.

Vamos adicionar um projeto de teste de unidade em nossa solução. Desta vez, começaremos com um modelo de projeto, de modo que não precisemos adicionar outro arquivo de código ao projeto.

1. Ao clicar com o botão direito do mouse ou no menu de contexto da **Solução ‘QuickSolution’** do **Gerenciador de Soluções**, escolha **Adicionar** > **Novo Projeto**.

   A caixa de diálogo **Adicionar Novo Projeto** é aberta.

1. No painel esquerdo, expanda a opção **Visual Basic** e escolha a categoria **Teste**. No painel central, escolha o modelo de projeto **Projeto de Teste de Unidade (.NET Framework)**. Nomeie o projeto **QuickTest** e, em seguida, escolha o botão **OK**.

   Um segundo projeto é adicionado ao **Gerenciador de Soluções** e um arquivo chamado *UnitTest1.vb* é aberto no editor. O *.vb* é a extensão de arquivo que é fornecida aos arquivos de código do Visual Basic.

   ![Gerenciador de Soluções do Visual Studio com dois projetos](media/tutorial-projects-solution-explorer.png)

## <a name="add-a-project-reference"></a>Adicionar uma referência ao projeto

Vamos usar o novo projeto de teste de unidade para testar nosso método no projeto **QuickDate**. Portanto, precisamos adicionar uma referência a esse projeto. Isso cria uma *dependência de build* entre os dois projetos, o que significa que quando a solução é criada, **QuickDate** é criado antes dependência **QuickTest**.

1. Escolha o nó **Referências** no projeto **QuickTest** e, ao clicar com o botão direito do mouse ou no menu de contexto, escolha **Adicionar Referência**.

   ![Adicionar menu de referência](media/tutorial-projects-add-reference.png)

   A caixa de diálogo **Gerenciador de Referências** é aberta.

1. No painel esquerdo, expanda **Projetos** e escolha **Solução**. No painel central, escolha a caixa de seleção ao lado de **QuickDate** e, em seguida, escolha o botão **OK**.

   Uma referência ao projeto **QuickDate** será adicionada.

## <a name="add-test-code"></a>Adicionar código de teste

1. Agora vamos adicionar o código de teste para o arquivo de código do Visual Basic. Substitua o conteúdo do *UnitTest1.vb* pelo seguinte código.

   ```vb
   <TestClass()> Public Class UnitTest1

       <TestMethod()> Public Sub TestGetCurrentDate()
           Assert.AreEqual(DateTime.Now.Date, QuickDate.Calendar.GetCurrentDate())
       End Sub

   End Class
   ```

   Você verá uma linha sinuosa vermelha em alguns dos códigos. Nós corrigiremos esse erro ao tornar o projeto de teste um [assembly amigável](/dotnet/csharp/programming-guide/concepts/assemblies-gac/friend-assemblies) para o projeto **QuickDate**.

1. De volta ao projeto **QuickDate**, abra o arquivo *Calendar.cs*, caso ele ainda não esteja aberto, e adicione a [instrução using](/dotnet/csharp/language-reference/keywords/using-statement) a seguir e o atributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> na parte superior do arquivo, para resolver o erro no projeto de teste.

   ```csharp
   using System.Runtime.CompilerServices;

   [assembly: InternalsVisibleTo("QuickTest")]
   ```

   O arquivo de código deve ter esta aparência:

   ![Código CSharp](media/tutorial-projects-cs-code.png)

## <a name="project-properties"></a>Propriedades de projeto

A linha no arquivo *Calendar.cs* que contém o atributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> referencia o nome do assembly (nome de arquivo) do projeto **QuickTest**. O nome do assembly pode não ser sempre o mesmo que o nome do projeto. Para localizar o nome do assembly de um projeto, abra as propriedades do projeto.

1. No **Gerenciador de Soluções**, selecione o projeto **QuickTest**. Ao clicar com o botão direito do mouse ou no menu de contexto, selecione **Propriedades** ou pressione **Alt**+**Enter**.

   As *páginas de propriedades* do projeto são abertas na guia **Aplicativo**. As páginas de propriedades contêm várias configurações para o projeto. Observe que o nome do assembly do projeto **QuickTest** é, de fato, “QuickTest”. Caso deseje alterá-lo, este é o local em que você poderá fazer isso. Assim, quando você compilar o projeto de teste, o nome do arquivo binário resultante será alterado de *QuickTest.dll* para o que você escolher.

   ![Propriedades de projeto](media/tutorial-projects-properties.png)

1. Explore algumas das outras guias das páginas de propriedades do projeto, como **Compilar** e **Configurações**. Essas guias são diferentes para diferentes tipos de projetos.

## <a name="next-steps"></a>Próximas etapas

Se você quiser verificar se seu teste de unidade está funcionando, selecione **Teste** > **Executar** > **Todos os Testes** na barra de menus. Uma janela chamada **Gerenciador de Testes** será aberta e você verá que o teste **TestGetCurrentDate** será aprovado.

![Gerenciador de Testes no Visual Studio mostrando a aprovação no teste](media/tutorial-projects-test-explorer.png)

> [!TIP]
> Se o **Gerenciador de Testes** não abrir automaticamente, abra-o escolhendo **Teste** > **Windows** > **Gerenciador de Testes** na barra de menus.

## <a name="see-also"></a>Consulte também

- [Criar projetos e soluções](../ide/creating-solutions-and-projects.md)
- [Gerenciar propriedades do projeto e da solução](../ide/managing-project-and-solution-properties.md)
- [Gerenciar referências em um projeto](../ide/managing-references-in-a-project.md)
- [Desenvolver código no Visual Studio sem projetos ou soluções](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)
- [Visão geral do IDE do Visual Studio](../get-started/visual-studio-ide.md)

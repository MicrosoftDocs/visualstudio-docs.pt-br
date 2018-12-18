---
title: Criar soluções e projetos no Visual Studio
ms.date: 02/06/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.openprojectfromweb
- vs.newproject
- VS.ToolsOptionsPages.Projects.General
- SolutionItemsProject
helpviewer_keywords:
- solutions [Visual Studio], creating
- projects [Visual Studio], creating
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a912534b9e0212e68a947fa892395a233f263a87
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349631"
---
# <a name="create-solutions-and-projects"></a>Criar soluções e projetos

*Projetos* são contêineres lógicos no Visual Studio que contêm os itens necessários para criar seu aplicativo, como arquivos de código-fonte, bitmaps, ícones e referências de componente e serviço. Quando você cria um novo projeto, o Visual Studio cria uma *solução* para contê-lo. Você poderá, então, adicionar projetos novos ou existentes à solução, se desejar. As soluções também podem conter arquivos não conectados a nenhum projeto específico.

![Hierarquia de projeto/solução](./media/vside-proj-soln.png)

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Criar projetos no Visual Studio para Mac](/visualstudio/mac/create-new-projects).

Você pode exibir suas soluções e projetos em uma janela de ferramentas chamada **Gerenciador de Soluções**. A captura de tela a seguir mostra uma solução de exemplo no **Gerenciador de Soluções** (**BikeSharing.Xamarin-UWP**) que contém dois projetos: **BikeSharing.Clients.Core** e **BikeSharing.Clients.Windows**. Cada projeto contém vários arquivos, pastas e referências. O nome do projeto em negrito é o *projeto de inicialização*, ou seja, o projeto que é iniciado quando você executa o aplicativo. Você pode especificar qual projeto é o projeto de inicialização.

![Gerenciador de Soluções com projetos](./media/vside-solution-explorer-projects.png)

Embora você possa construir um projeto por conta própria, adicionando nele os arquivos necessários, o Visual Studio oferece uma seleção de modelos de projeto para lhe proporcionar um ponto de partida. A criação de um novo projeto com base em um modelo oferece um projeto com o que é essencial para aquele tipo de projeto e você pode renomear os arquivos ou adicionar código, novo ou existente, ao projeto, bem como adicionar outros recursos, conforme a necessidade.

Dito isso, soluções e projetos não são necessários para desenvolver aplicativos no Visual Studio. Você também pode simplesmente abrir código clonado do Git ou baixado em outro lugar. Para obter mais informações, consulte [Desenvolver código no Visual Studio sem projetos nem soluções](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md).

> [!NOTE]
> As descrições deste tópico baseiam-se na edição Visual Studio Community. As caixas de diálogo e comandos de menu que você vê podem ser diferentes dos descritos aqui, dependendo de suas configurações ou da edição Visual Studio. Para alterar as configurações, por exemplo, para configurações **Gerais** ou do **Visual C++**, escolha **Ferramentas** > **Importar e Exportar Configurações** e, em seguida, escolha **Redefinir todas as configurações**.

## <a name="to-create-a-project-from-a-project-template"></a>Para criar um projeto com base em um modelo de projeto

1. Há várias maneiras de criar um novo projeto no Visual Studio. Na **Página Inicial**, digite o nome de um modelo de projeto na caixa **Pesquisar modelos de projeto** ou escolha o link **Criar novo projeto** para abrir a caixa de diálogo **Novo Projeto**. Você também pode escolher **Arquivo** > **Novo** > **Projeto** na barra de menus ou clicar no botão **Novo Projeto** na barra de ferramentas.

   ![Página inicial](./media/vside-newproject1.png)

   Na caixa de diálogo **Novo Projeto**, os modelos de projeto disponíveis aparecem em uma lista sob a categoria **Modelos**. Os modelos são organizados por linguagem de programação e tipo de projeto, como Visual C#, JavaScript e Azure Data Lake.

   ![Caixa de diálogo Novo Projeto](./media/vside-newproject-templates-list.png)

   > [!NOTE]
   > A lista de linguagens e modelos de projeto disponíveis que é exibida depende da versão do Visual Studio que você está executando e das cargas de trabalho que estão instaladas. Para saber mais sobre como instalar cargas de trabalho adicionais, consulte [Modificar o Visual Studio 2017 adicionando ou removendo cargas de trabalho e componentes](../install/modify-visual-studio.md).

2. Para mostrar a lista de modelos da linguagem de programação que você deseja usar, escolha o triângulo próximo do nome da linguagem e, em seguida, escolha um tipo de projeto.

   O exemplo a seguir mostra os modelos de projeto disponíveis para projetos .NET Core do Visual C#.

   ![Modelos de projeto](./media/new-project-dialog-net-core.png)

3. Digite um nome para o novo projeto na caixa **Nome**. Você pode optar por salvar o projeto no local padrão em seu sistema ou escolher o botão **Procurar** para encontrar outro local.

   Você também pode optar por alterar o nome da solução ou adicionar o novo projeto a um repositório Git, escolhendo **Adicionar ao Controle do Código-Fonte**.

4. Escolha o botão **OK** para criar a solução e o projeto.

5. Se você quiser adicionar mais um projeto à solução, escolha o nó da solução no **Gerenciador de Soluções** e, na barra de menus, escolha **Projeto** > **Adicionar novo item**.

## <a name="create-a-project-from-existing-code-files"></a>Criar um projeto com base em arquivos de código existentes

Se você tem uma coleção de arquivos de origem de código, é possível adicioná-los facilmente a um projeto.

1. No menu, escolha **Arquivo** > **Novo** > **Projeto de Código Existente**.

1. No assistente **Criação de Projeto de Arquivos de Código Existentes**, escolha o tipo de projeto que você deseja na caixa de listagem suspensa **Que tipo de projeto deseja criar?** e, em seguida, escolha o botão **Avançar**.

1. No assistente, navegue até o local dos arquivos e, em seguida, insira um nome para o novo projeto na caixa **Nome**. Quando terminar, escolha o botão **Concluir**.

> [!NOTE]
> Essa opção funciona melhor para uma coleção relativamente simples de arquivos. Atualmente, somente os tipos de projeto do Visual C++, Apache Cordova, Visual Basic e C# são compatíveis.

## <a name="add-files-to-a-solution"></a>Adicionar arquivos a uma solução

Se você tem um arquivo que se aplica a vários projetos, como um arquivo Leiame para a solução ou outros arquivos que pertençam de forma lógica ao nível da solução e não a um projeto específico, é possível adicioná-los à própria solução. Para adicionar um item a uma solução, no menu de contexto (clicar com o botão direito do mouse) do nó da solução no **Gerenciador de Soluções**, escolha **Adicionar** > **Novo Item** ou **Adicionar** > **Item existente**.

## <a name="create-a-net-project-that-targets-a-specific-version-of-the-net-framework"></a>Criar um projeto .NET que direciona uma versão específica do .NET Framework

Ao criar um projeto, você pode determinar uma versão específica do .NET Framework que você deseja que o projeto use. Para especificar uma versão do .NET Framework, escolha o menu suspenso da **Framework** na caixa de diálogo **Novo Projeto**.

![A lista suspensa Estrutura na caixa de diálogo Novo Projeto](./media/vside-newproject-framework.png)

> [!NOTE]
> É necessário ter o .NET Framework 3.5 instalado em seu sistema para acessar as versões do .NET Framework anteriores à versão 4.

## <a name="create-empty-solutions"></a>Criar soluções vazias

Você também pode criar soluções vazias que não tenham projetos. Isso é preferível em casos em que você deseja criar a solução e os projetos do zero.

### <a name="to-create-an-empty-solution"></a>Para criar uma solução vazia

1. No menu, escolha **Arquivo** > **Novo** > **Projeto**.

1. No painel esquerdo (**Modelos**), escolha **Outros Tipos de Projetos** > **Soluções do Visual Studio** na lista expandida.

1. No painel central, selecione **Solução em Branco**.

1. Insira os valores **Nome** e **Local** da sua solução e, em seguida, clique em **OK**.

Depois de criar uma solução vazia, é possível adicionar projetos novos ou existentes ou itens a ele ao selecionar **Adicionar Novo Item** ou **Adicionar Item Existente** no menu **Projeto**.

Como mencionado anteriormente, você também pode abrir arquivos de código sem precisar de um projeto ou solução. Para saber mais sobre como desenvolver código dessa forma, consulte [Desenvolver código no Visual Studio sem projetos ou soluções](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md).

## <a name="create-a-temporary-project-c-and-visual-basic"></a>Criar um projeto temporário (C# e Visual Basic)

Se você criar um projeto com base em .NET sem especificar um local de disco, ele será um projeto temporário. Os projetos temporários permitem fazer experimentos com projetos do .NET. A qualquer momento, enquanto você está trabalhando com um projeto temporário, é possível escolher salvá-lo ou descartá-lo.

Para criar um projeto temporário, primeiro acesse **Ferramentas** > **Opções** > **Projetos e Soluções** > **Geral** e desmarque a caixa de seleção **Salvar novos projetos quando criados**. Em seguida, abra a caixa de diálogo **Novo projeto** como de costume.

## <a name="delete-a-solution-project-or-item"></a>Excluir uma solução, um projeto ou um item

Você pode excluir as soluções e seu conteúdo permanentemente, mas não usando o IDE do Visual Studio. A exclusão de itens dentro do Visual Studio somente os remove da solução ou do projeto atual. Para excluir permanentemente do sistema uma solução ou outro componente, use o Explorador de Arquivos para excluir a pasta que contém os arquivos de solução *.sln* e *.suo*. No entanto, antes de excluir permanentemente uma solução, é recomendável que você faça backup de todos os projetos ou arquivos, caso sejam necessários novamente.

> [!NOTE]
> O arquivo *.suo* é um arquivo oculto que não é exibido com as configurações padrão do Explorador de Arquivos. Para mostrar arquivos ocultos, no menu **Exibir** do Explorador de Arquivos, marque a caixa de seleção **Itens Ocultos**.

### <a name="to-permanently-delete-a-solution"></a>Para excluir permanentemente uma solução

1. No **Gerenciador de Soluções**, no menu de contexto da solução que você deseja excluir, selecione **Abrir Pasta no Explorador de Arquivos**.

1. No Gerenciador de Arquivos, navegue um nível acima.

1. Escolha a pasta que contém a solução e pressione a tecla **Delete**.

## <a name="see-also"></a>Consulte também

- [Soluções e Projetos](../ide/solutions-and-projects-in-visual-studio.md)
- [Repositórios de software livre da Microsoft no GitHub](https://github.com/Microsoft)
- [Exemplos de código para desenvolvedores](https://code.msdn.microsoft.com/)
- [Criar projetos (Visual Studio para Mac)](/visualstudio/mac/create-new-projects)
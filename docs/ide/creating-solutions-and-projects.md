---
title: Criar & usar os projetos do Visual Studio & soluções
description: Saiba mais sobre a diferença entre soluções e projetos e como usá-los no Visual Studio.
ms.custom: SEO-VS-2020, contperf-fy21q2
ms.date: 06/14/2021
ms.topic: how-to
f1_keywords:
- vs.openprojectfromweb
- VS.ToolsOptionsPages.Projects.General
- SolutionItemsProject
helpviewer_keywords:
- solutions [Visual Studio], creating
- projects [Visual Studio], creating
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7971226767fe114e3618e9dfc6a161a50d5374ee
ms.sourcegitcommit: 40646cd90ca0701c034311931f026cf67edb74de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2021
ms.locfileid: "112500897"
---
# <a name="create-work-with-and-delete-visual-studio-projects-and-solutions"></a>Criar, trabalhar com e excluir projetos e soluções do Visual Studio

Neste artigo, você aprenderá a criar e usar projetos do Visual Studio do zero para armazenar os artefatos necessários para criar seus aplicativos.  Se você não estiver familiarizado com projetos no Visual Studio, consulte esta visão geral de [projetos e soluções](solutions-and-projects-in-visual-studio.md).  Para saber como criar rapidamente um projeto a partir de um modelo, consulte [criar um projeto de um modelo](create-new-project.md).

Os *projetos* armazenam os itens necessários para criação do aplicativo no Visual Studio, como arquivos de código-fonte, bitmaps, ícones e referências de componente e serviço. Quando você cria um novo projeto, o Visual Studio cria uma *solução* para contê-lo. Você poderá, então, adicionar projetos novos ou existentes à solução, se desejar. As soluções também podem conter arquivos não conectados a nenhum projeto específico.

![Diagrama mostrando a solução e a hierarquia do projeto.](./media/vside-proj-soln.png)

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Criar projetos no Visual Studio para Mac](/visualstudio/mac/create-new-projects).

Você pode exibir suas soluções e projetos em uma janela de ferramentas chamada **Gerenciador de Soluções**. A captura de tela a seguir mostra uma solução de exemplo no **Gerenciador de Soluções** (**BikeSharing.Xamarin-UWP**) que contém dois projetos: **BikeSharing.Clients.Core** e **BikeSharing.Clients.Windows**. Cada projeto contém vários arquivos, pastas e referências. O nome do projeto em negrito é o *projeto de inicialização*, ou seja, o projeto que é iniciado quando você executa o aplicativo. Você pode especificar qual projeto é o projeto de inicialização.

![Captura de tela de Gerenciador de Soluções com dois projetos.](./media/vside-solution-explorer-projects.png)

Embora você possa construir um projeto por conta própria, adicionando nele os arquivos necessários, o Visual Studio oferece uma seleção de modelos de projeto para lhe proporcionar um ponto de partida. A criação de um novo projeto com base em um modelo oferece um projeto com o que é essencial para aquele tipo de projeto e você pode renomear os arquivos ou adicionar código, novo ou existente, ao projeto, bem como adicionar outros recursos, conforme a necessidade.

Dito isso, soluções e projetos não são necessários para desenvolver aplicativos no Visual Studio. Você também pode simplesmente abrir código clonado do Git ou baixado em outro lugar. Para obter mais informações, consulte [Desenvolver código no Visual Studio sem projetos nem soluções](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md).

## <a name="create-a-project-from-a-project-template"></a>Criar um projeto com base em um modelo de projeto

Para obter informações sobre como selecionar um modelo para criar um novo projeto, consulte [criar um novo projeto no Visual Studio](create-new-project.md). E, para obter um exemplo de projeto e solução que é criado do zero, completo com instruções passo a passo e código de exemplo, consulte [introdução aos projetos e soluções](../get-started/tutorial-projects-solutions.md).

## <a name="create-a-project-from-existing-code-files"></a>Criar um projeto com base em arquivos de código existentes

Se você tem uma coleção de arquivos de origem de código, é possível adicioná-los facilmente a um projeto.

1. No menu, selecione **arquivo**  >  **novo**  >  **projeto do código existente**.

1. No Assistente para **criar projeto a partir de arquivos de código existentes** , selecione o tipo de projeto desejado na caixa de listagem suspensa **que tipo de projeto você deseja criar?** e, em seguida, selecione o botão **Avançar** .

1. No assistente, navegue até o local dos arquivos e, em seguida, insira um nome para o novo projeto na caixa **Nome**. Quando terminar, selecione o botão **concluir** .

> [!NOTE]
> Essa opção funciona melhor para uma coleção relativamente simples de arquivos. Atualmente, há suporte apenas para os tipos de projeto C++, Apache Cordova, Visual Basic e C#.

## <a name="add-files-to-a-solution"></a>Adicionar arquivos a uma solução

Se você tem um arquivo que se aplica a vários projetos, como um arquivo Leiame para a solução ou outros arquivos que pertençam de forma lógica ao nível da solução e não a um projeto específico, é possível adicioná-los à própria solução. Para adicionar um item a uma solução, no menu de contexto (clique com o botão direito do mouse) do nó da solução no **Gerenciador de soluções**, selecione **Adicionar**  >  **novo item** ou **Adicionar**  >  **Item existente**.

> [!TIP]
> Um arquivo de solução é uma estrutura para organizar projetos no Visual Studio. Ele contém o estado dessas informações em dois arquivos: um arquivo *. sln* (baseado em texto, compartilhado) e um arquivo *. suo* (opções de solução binária, oculta e específica do usuário). Portanto, uma solução não é algo que deve ser copiado e renomeado; em vez disso, é melhor criar uma nova solução e adicionar itens existentes a ela.

## <a name="create-a-net-project-that-targets-a-specific-version-of-the-net-framework"></a>Criar um projeto .NET que direciona uma versão específica do .NET Framework

Ao criar um projeto .NET Framework, você pode determinar uma versão específica do .NET Framework que deseja usar no projeto. (Ao criar um projeto .NET Core, você não especifica uma versão de estrutura.)

::: moniker range="vs-2017"

Para especificar uma versão .NET Framework, selecione o menu suspenso **estrutura** na caixa de diálogo **novo projeto** .

![Captura de tela da lista suspensa estrutura na caixa de diálogo novo projeto.](./media/vside-newproject-framework.png)

> [!NOTE]
> É necessário ter o .NET Framework 3.5 instalado em seu sistema para acessar as versões do .NET Framework anteriores à versão 4.

::: moniker-end

::: moniker range=">=vs-2019"

Para especificar uma versão .NET Framework, selecione o menu suspenso **estrutura** na página **criar um novo projeto** .

![Captura de tela do seletor de estrutura na caixa de diálogo ' Configurar novo projeto '.](media/vs-2019/configure-new-project-framework.png)

::: moniker-end

## <a name="create-empty-solutions"></a>Criar soluções vazias

Você também pode criar soluções vazias que não tenham projetos. Isso é preferível em casos em que você deseja criar a solução e os projetos do zero.

### <a name="to-create-an-empty-solution"></a>Para criar uma solução vazia

1. Na barra de menus, selecione **arquivo**  >  **novo**  >  **projeto**.

::: moniker range="vs-2017"

2. No painel esquerdo (**modelos**), selecione **outros tipos de projeto** > **soluções do Visual Studio** na lista expandida.

3. No painel central, selecione **Solução em Branco**.

4. Insira os valores de **nome** e **local** para sua solução e, em seguida, selecione **OK**.

::: moniker-end

::: moniker range=">=vs-2019"

2. Na página **Criar um novo projeto**, digite **solução** na caixa de pesquisa.

3. Selecione o modelo **solução em branco** e clique em **Avançar**.

4. Insira os valores de **nome** e **local** para sua solução e, em seguida, selecione **criar**.

::: moniker-end

Depois de criar uma solução vazia, é possível adicionar projetos novos ou existentes ou itens a ele ao selecionar **Adicionar Novo Item** ou **Adicionar Item Existente** no menu **Projeto**.

Como mencionado anteriormente, você também pode abrir arquivos de código sem precisar de um projeto ou solução. Para saber mais sobre como desenvolver código dessa forma, consulte [Desenvolver código no Visual Studio sem projetos ou soluções](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md).

::: moniker range="vs-2017"

## <a name="create-a-temporary-project"></a>Criar um projeto temporário

(somente C# e Visual Basic)

Se você criar um projeto com base em .NET sem especificar um local de disco, ele será um projeto temporário. Os projetos temporários permitem fazer experimentos com projetos do .NET. A qualquer momento, enquanto você está trabalhando com um projeto temporário, é possível escolher salvá-lo ou descartá-lo.

Para criar um projeto temporário, primeiro vá para **ferramentas**  >  **Opções**  >  **projetos e soluções**  >  **geral** e desmarque a caixa de seleção **salvar novos projetos quando criados** . Em seguida, abra a caixa de diálogo **Novo projeto** como de costume.

::: moniker-end

## <a name="delete-a-solution-project-or-item"></a>Excluir uma solução, um projeto ou um item

Você pode usar o menu de contexto de clique com o botão direito do mouse para excluir ou remover soluções, projetos ou itens no Visual Studio, mas isso só os remove da solução ou do projeto atual.

Para excluir permanentemente uma solução ou outros componentes do seu sistema, use o **Explorador de arquivos** no Windows para excluir a pasta que contém os arquivos de solução *. sln* e *. suo* . (Antes de excluir uma solução, talvez você queira fazer backup de seus projetos e arquivos caso precise deles novamente.)

> [!NOTE]
> O arquivo *. suo* é um arquivo oculto que não é exibido sob as configurações padrão do explorador de arquivos. Para mostrar arquivos ocultos, no menu **Exibir** do Explorador de Arquivos, marque a caixa de seleção **Itens Ocultos**.

### <a name="permanently-delete-a-solution"></a>Excluir uma solução permanentemente

Você pode acessar o explorador de arquivos no Windows usando Gerenciador de Soluções no Visual Studio. Veja aqui como fazer isso.

1. No **Gerenciador de soluções**, no menu do botão direito do mouse (menu de contexto) da solução que você deseja excluir, selecione **abrir pasta no explorador de arquivos**.

1. No Gerenciador de Arquivos, navegue um nível acima.

1. Selecione a pasta que contém a solução e pressione a tecla **delete** .

## <a name="see-also"></a>Confira também

- [Introdução a projetos e soluções](../get-started/tutorial-projects-solutions.md)
- [Gerenciar propriedades do projeto e da solução](managing-project-and-solution-properties.md)
- [Soluções filtradas no Visual Studio](filtered-solutions.md)
- [Repositórios de software livre da Microsoft no GitHub](https://github.com/Microsoft)
- [Exemplos de código do desenvolvedor](https://code.msdn.microsoft.com/)
- [Recursos para solução de problemas de erros do IDE do Visual Studio](./reference/resources-for-troubleshooting-integrated-development-environment-errors.md)

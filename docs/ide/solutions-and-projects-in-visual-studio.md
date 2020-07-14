---
title: Soluções e projetos
ms.date: 06/26/2020
ms.topic: conceptual
f1_keywords:
- vs.addnewitem
- vs.addnewsolutionitem
- vs.openproject
- vs.addexistingitem
- vs.addexistingsolutionitem
- vs.environment.projects
- vs.environment.solutions
- VS.SolutionExplorer
- VS.SolutionExplorer.Solutions
helpviewer_keywords:
- solutions [Visual Studio]
- projects [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ad0ee64afa78a962271d2b702ee525287c5b2457
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468724"
---
# <a name="solutions-and-projects-in-visual-studio"></a>Soluções e projetos no Visual Studio

Esta página descreve o conceito de um *projeto* e uma *solução* no Visual Studio. Ele também aborda brevemente a janela de ferramentas de Gerenciador de Soluções e como criar um novo projeto.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Projetos e soluções no Visual Studio para Mac](/visualstudio/mac/projects-and-solutions).

## <a name="projects"></a>Projetos

Ao criar um aplicativo ou site no Visual Studio, você começa com um *projeto*do. Em um sentido lógico, um projeto contém todos os arquivos que são compilados em um executável, biblioteca ou site. Esses arquivos podem incluir código-fonte, ícones, imagens, arquivos de dados e assim por diante. Um projeto também contém as configurações de compilador e outros arquivos de configuração que podem ser necessários para diversos serviços ou componentes com os quais seu programa se comunica.

### <a name="project-file"></a>Arquivo de projeto

O Visual Studio usa o [MSBuild](../msbuild/msbuild.md) para compilar cada projeto em uma solução, e cada projeto contém um arquivo de projeto do MSBuild. A extensão de arquivo reflete o tipo de projeto, por exemplo, um projeto C# (. csproj), um projeto Visual Basic (. vbproj) ou um projeto de banco de dados (. dbproj). O arquivo de projeto é um documento XML que contém todas as informações e instruções de que o MSBuild precisa para criar seu projeto, incluindo conteúdo, requisitos de plataforma, informações de controle de versão, servidor Web ou configurações de servidor de banco de dados e tarefas a serem executadas.

Os arquivos de projeto são baseados no [esquema XML do MSBuild](../msbuild/msbuild-project-file-schema-reference.md). Para examinar o conteúdo dos arquivos de projeto mais recentes do [estilo SDK](../msbuild/how-to-use-project-sdk.md) no Visual Studio, clique com o botão direito do mouse no nó do projeto em **Gerenciador de soluções** e selecione **Editar \<projectname\> **. Para examinar o conteúdo de .NET Framework e outros projetos desse estilo, primeiro descarregue o projeto (clique com o botão direito do mouse no nó do projeto em **Gerenciador de soluções** e selecione **descarregar projeto**). Em seguida, clique com o botão direito do mouse no projeto e escolha **Editar \<projectname\> **.

> [!NOTE]
> Você não precisa usar soluções ou projetos no Visual Studio para editar, compilar e depurar código. Você pode simplesmente abrir a pasta que contém os arquivos de origem no Visual Studio e começar a editá-los. Para obter mais informações, consulte [Desenvolver código no Visual Studio sem projetos nem soluções](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md).

## <a name="solutions"></a>Soluções

Um projeto está contido dentro de uma *solução*. Apesar do nome, uma solução não é uma "resposta". Ela é apenas um contêiner de um ou mais projetos relacionados, juntamente com informações de build, configurações de janela do Visual Studio e arquivos diversos que não estão associados a nenhum projeto específico. Uma solução é descrita por um arquivo de texto (extensão *.sln*) com seu próprio formato exclusivo; não se destina à edição manual.

O Visual Studio usa dois tipos de arquivos (*.sln* e *.suo*) para armazenar configurações de soluções:

|Extensão|Name|Descrição|
|---------------|----------|-----------------|
|.sln|Solução do Visual Studio|Organiza projetos, itens de projeto e itens de solução na solução.|
|.suo|Opções do usuário da solução|Armazena configurações e personalizações no nível do usuário, como pontos de interrupção.|

## <a name="create-new-projects"></a>Criar novos projetos

A maneira mais fácil de criar um novo projeto é começar de um modelo de projeto para um tipo específico de aplicativo ou site. Um modelo de projeto consiste em um conjunto básico de arquivos de código, arquivos de configuração, ativos e configurações gerados previamente. Esses modelos estão disponíveis na caixa de diálogo em que você cria um novo projeto (**arquivo**  >  **novo**  >  **projeto**). Para saber mais, confira [Criar um novo projeto no Visual Studio](create-new-project.md) e [Criar soluções e projetos](../ide/creating-solutions-and-projects.md).

Se você geralmente personaliza seus projetos de uma determinada maneira, pode criar um modelo de projeto personalizado que você pode usar para criar novos projetos do. Para obter mais informações, confira [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md).

Quando você cria um novo projeto, ele é salvo por padrão em *%USERPROFILE%\source\repos*. Você pode alterar esse local na configuração **Locais do projeto** em **Ferramentas** > **Opções** > **Projetos e Soluções** > **Locais**. Para obter mais informações, consulte a [página Projetos e Soluções, caixa de diálogo Opções](../ide/reference/projects-and-solutions-options-dialog-box.md).

## <a name="solution-explorer"></a>Gerenciador de Soluções

Depois de criar um novo projeto, você pode usar o **Gerenciador de Soluções** para exibir e gerenciar o projeto, a solução e seus itens associados. A ilustração a seguir mostra o **Gerenciador de Soluções** com uma solução C# que contém dois projetos:

![Gerenciador de Soluções](../ide/media/vs2015_solution_explorer.png)

Muitos comandos de menu estão disponíveis no menu do botão direito em vários itens no **Gerenciador de Soluções**. Esses comandos incluem criar um projeto, gerenciar pacotes do NuGet, adicionar uma referência, renomear um arquivo e executar testes, apenas para citar alguns. A barra de ferramentas na parte superior do **Gerenciador de Soluções** possui botões para alternar de uma exibição de solução para uma exibição de pasta, mostrar arquivos ocultos, recolher todos os nós e muito mais.

> [!TIP]
> Se você fechou Gerenciador de soluções e deseja abri-lo novamente, escolha **Window**  >  o**layout da janela de redefinição** de janela na barra de menus.

Para projetos ASP.NET Core, você pode personalizar como os arquivos são aninhados no **Gerenciador de Soluções**. Para saber mais, confira [Personalizar o aninhamento de arquivos no Gerenciador de Soluções](file-nesting-solution-explorer.md).

E, para exibir uma lista de alguns ícones que aparecem no Gerenciador de Soluções, consulte os [ícones modo de exibição de classe e pesquisador de objetos](class-view-and-object-browser-icons.md).

## <a name="see-also"></a>Veja também

- [Visual Studio IDE](../get-started/visual-studio-ide.md)
- [Portar, migrar e atualizar projetos](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
- [Projetos e soluções (Visual Studio para Mac)](/visualstudio/mac/projects-and-solutions)
- [Adicionar e remover itens do projeto (Visual Studio para Mac)](/visualstudio/mac/add-and-remove-project-items)

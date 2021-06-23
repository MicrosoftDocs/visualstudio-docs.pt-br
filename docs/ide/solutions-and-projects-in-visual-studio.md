---
title: O que são as soluções do Visual Studio & projetos?
description: Saiba mais sobre projetos e soluções do Visual Studio, como criar novos projetos de um modelo e como exibir & gerenciar projetos no Gerenciador de Soluções.
ms.custom: SEO-VS-2020, contperf-fy21q2
ms.date: 12/31/2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 61cc760eb34df7f643bbdc16607f2316e92785bf
ms.sourcegitcommit: 40646cd90ca0701c034311931f026cf67edb74de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2021
ms.locfileid: "112500884"
---
# <a name="what-are-solutions-and-projects-in-visual-studio"></a>O que são soluções e projetos no Visual Studio?

Neste artigo, você aprenderá o que é um *projeto* e uma *solução* no Visual Studio. Ele também aborda brevemente a janela de ferramentas de Gerenciador de Soluções e como criar um novo projeto.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Projetos e soluções no Visual Studio para Mac](/visualstudio/mac/projects-and-solutions).

## <a name="projects"></a>Projetos

Ao criar um aplicativo ou site no Visual Studio, você começa com um *projeto* do. Em um sentido lógico, um projeto contém todos os arquivos que são compilados em um executável, biblioteca ou site. Esses arquivos podem incluir código-fonte, ícones, imagens, arquivos de dados e assim por diante. Um projeto também contém as configurações de compilador e outros arquivos de configuração que podem ser necessários para diversos serviços ou componentes com os quais seu programa se comunica.

### <a name="project-file"></a>Arquivo de projeto

O Visual Studio usa o [MSBuild](../msbuild/msbuild.md) para compilar cada projeto em uma solução, e cada projeto contém um arquivo de projeto do MSBuild. A extensão de arquivo reflete o tipo de projeto, por exemplo, um projeto C# (. csproj), um projeto Visual Basic (. vbproj) ou um projeto de banco de dados (. dbproj). O arquivo de projeto é um documento XML que contém todas as informações e instruções de que o MSBuild precisa para criar seu projeto, incluindo conteúdo, requisitos de plataforma, informações de controle de versão, servidor Web ou configurações de servidor de banco de dados e tarefas a serem executadas.

Os arquivos de projeto são baseados no [esquema XML do MSBuild](../msbuild/msbuild-project-file-schema-reference.md). Para examinar o conteúdo dos arquivos de projeto mais recentes do [estilo SDK](../msbuild/how-to-use-project-sdk.md) no Visual Studio, clique com o botão direito do mouse no nó do projeto em **Gerenciador de soluções** e selecione **Editar \<projectname\>**. Para examinar o conteúdo de .NET Framework e outros projetos desse estilo, primeiro descarregue o projeto (clique com o botão direito do mouse no nó do projeto em **Gerenciador de soluções** e selecione **descarregar projeto**). Em seguida, clique com o botão direito do mouse no projeto e escolha **Editar \<projectname\>**.

> [!NOTE]
> Você não precisa usar soluções ou projetos no Visual Studio para editar, compilar e depurar código. Você pode simplesmente abrir a pasta que contém os arquivos de origem no Visual Studio e começar a editá-los. Para obter mais informações, consulte [Desenvolver código no Visual Studio sem projetos nem soluções](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md).

### <a name="create-new-projects"></a>Criar novos projetos

A maneira mais fácil de criar um novo projeto é usar um modelo de projeto para o tipo de projeto desejado. Um modelo de projeto inclui um conjunto básico de arquivos de código gerados previamente, arquivos de configuração, ativos e configurações. Use **arquivo**  >  **novo**  >  **projeto** para selecionar um modelo de projeto. Para obter mais informações, consulte [criar um novo projeto](create-new-project.md).

Você também pode criar um modelo de projeto personalizado que pode ser usado para criar novos projetos do. Para obter mais informações, confira [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md).

Quando você cria um novo projeto, o Visual Studio o salva em seu local padrão, *%USERPROFILE%\source\repos*. Para alterar esse local, vá para **ferramentas**  >  **Opções**  >  **projetos e soluções**  >  **locais**. Para obter mais informações, consulte [caixa de diálogo opções: projetos e soluções > locais](./reference/projects-solutions-locations-options.md).

## <a name="solutions"></a>Soluções

Um projeto está contido dentro de uma *solução*. Apesar do nome, uma solução não é uma "resposta". Ela é apenas um contêiner de um ou mais projetos relacionados, juntamente com informações de build, configurações de janela do Visual Studio e arquivos diversos que não estão associados a nenhum projeto específico.

### <a name="solution-file"></a>Arquivo de solução

O Visual Studio usa dois tipos de arquivos (*.sln* e *.suo*) para armazenar configurações de soluções:

|Extensão|Name|Descrição|
|---------------|----------|-----------------|
|.sln|Solução do Visual Studio|Organiza projetos, itens de projeto e itens de solução na solução.|
|.suo|Opções do usuário da solução|Armazena configurações e personalizações no nível do usuário, como pontos de interrupção.|

> [!IMPORTANT]
> Uma solução é descrita por um arquivo de texto (extensão *.sln*) com seu próprio formato exclusivo; não se destina à edição manual. Por outro lado, o arquivo *. suo* é um arquivo oculto que não é exibido sob as configurações padrão do explorador de arquivos. Para mostrar arquivos ocultos, no menu **Exibir** do Explorador de Arquivos, marque a caixa de seleção **Itens Ocultos**.

### <a name="solution-folder"></a>Pasta da solução

Uma "pasta de solução" é uma pasta virtual que só está em **Gerenciador de soluções**, onde você pode usá-la para agrupar projetos em uma solução. Se você quiser localizar um arquivo de solução em um computador, vá para **ferramentas**  >  **Opções**  >  **projetos e soluções**  >  **locais**. Para obter mais informações, consulte [caixa de diálogo opções: projetos e soluções > locais](./reference/projects-solutions-locations-options.md).

> [!TIP]
> Para obter um exemplo de um projeto e uma solução criados a partir do zero, conclua com instruções passo a passo e código de exemplo, consulte [introdução aos projetos e soluções](../get-started/tutorial-projects-solutions.md).

## <a name="solution-explorer"></a>Gerenciador de Soluções

Depois de criar um novo projeto, você pode usar o **Gerenciador de Soluções** para exibir e gerenciar o projeto, a solução e seus itens associados. A ilustração a seguir mostra o **Gerenciador de Soluções** com uma solução C# que contém dois projetos:

::: moniker range="vs-2017"

![Captura de tela de Gerenciador de Soluções com dois projetos.](../ide/media/vs2015_solution_explorer.png)

A barra de ferramentas na parte superior do **Gerenciador de Soluções** possui botões para alternar de uma exibição de solução para uma exibição de pasta, mostrar arquivos ocultos, recolher todos os nós e muito mais.

::: moniker-end

::: moniker range=">=vs-2019"

![Captura de tela de Gerenciador de Soluções com dois projetos no Visual Studio.](../ide/media/solution-explorer.png)

A barra de ferramentas na parte superior de **Gerenciador de soluções** tem botões para alternar de uma exibição de solução para uma exibição de pasta, filtrar alterações pendentes, mostrar todos os arquivos, recolher todos os nós, exibir páginas de [Propriedades](managing-project-and-solution-properties.md) , Visualizar código no [Editor de códigos](writing-code-in-the-code-and-text-editor.md)e muito mais.

::: moniker-end

Muitos comandos de menu estão disponíveis no menu de contexto de clique com o botão direito do mouse em vários itens em **Gerenciador de soluções**. Esses comandos incluem criar um projeto, gerenciar pacotes do NuGet, adicionar uma referência, renomear um arquivo e executar testes, apenas para citar alguns.

Para projetos ASP.NET Core, você pode personalizar como os arquivos são aninhados no **Gerenciador de Soluções**. Para saber mais, confira [Personalizar o aninhamento de arquivos no Gerenciador de Soluções](file-nesting-solution-explorer.md).

> [!TIP]
> Se você fechou Gerenciador de soluções e deseja abri-lo novamente, escolha **Exibir**  >  **Gerenciador de soluções** na barra de menus ou pressione **Ctrl** + **ALT** + **L**. E, se você fechou as guias laterais e deseja restaurá-las para seus locais padrão, escolha o   >  **layout da janela de redefinição** de janela na barra de menus.

> [!NOTE]
> Para exibir as imagens e os ícones do aplicativo que aparecem no Visual Studio, baixe a [**biblioteca de imagens do Visual Studio**](https://www.microsoft.com/download/details.aspx?id=35825).

## <a name="see-also"></a>Confira também

- [Introdução a projetos e soluções](../get-started/tutorial-projects-solutions.md)
- [Gerenciar propriedades do projeto e da solução](managing-project-and-solution-properties.md)
- [Soluções filtradas no Visual Studio](filtered-solutions.md)
- [Portar, migrar e atualizar projetos](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
- [Recursos para solução de problemas de erros do IDE do Visual Studio](./reference/resources-for-troubleshooting-integrated-development-environment-errors.md)
- [Projetos e soluções (Visual Studio para Mac)](/visualstudio/mac/projects-and-solutions)

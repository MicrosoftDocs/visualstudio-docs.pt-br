---
title: Soluções e projetos
ms.date: 10/05/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.addnewsolutionitem
- vs.environment.projects
- vs.openproject
- vs.addnewitem
- vs.addexistingitem
- VS.SolutionExplorer
- vs.newproject
- vs.addexistingsolutionitem
- vs.environment.solutions
- VS.SolutionExplorer.Solutions
helpviewer_keywords:
- solution items [Visual Studio]
- solutions [Visual Studio]
- project items [Visual Studio]
- solutions [Visual Studio], designing
- projects [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 518479d92aa9b0ec51c4fda8b7484a03ce45a560
ms.sourcegitcommit: 0cdd8e8a53fb4fd5e869f07c35204419fa12783d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53159666"
---
# <a name="solutions-and-projects-in-visual-studio"></a>Soluções e projetos no Visual Studio

Este artigo descreve o conceito de um *projeto* e de uma *solução* no Visual Studio. Ele também aborda rapidamente a janela de ferramentas **Gerenciador de Soluções** e como criar um projeto.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Projetos e soluções no Visual Studio para Mac](/visualstudio/mac/projects-and-solutions).

## <a name="projects"></a>Projetos

Ao criar um aplicativo, um site, um plug-in, etc. no Visual Studio, você inicia um *projeto*. Logicamente, um projeto contém todos os arquivos de código-fonte, ícones, imagens, arquivos de dados, etc. que são compilados em um executável, biblioteca ou site. Um projeto também contém as configurações de compilador e outros arquivos de configuração que podem ser necessários para diversos serviços ou componentes com os quais seu programa se comunica.

> [!NOTE]
> Você não precisa usar soluções ou projetos no Visual Studio para editar, compilar e depurar o código. Você pode simplesmente abrir a pasta que contém os arquivos de origem no Visual Studio e começar a editá-los. Para obter mais informações, consulte [Desenvolver código no Visual Studio sem projetos nem soluções](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md).

Um projeto é definido em um arquivo XML com uma extensão, como *.vbproj*, *.csproj* ou *.vcxproj*. Este arquivo contém uma hierarquia de pasta virtual e os caminhos para todos os itens no projeto. Ele também contém as configurações de build.

> [!TIP]
> Para examinar o conteúdo de um arquivo de projeto no Visual Studio, primeiro descarregue o projeto selecionando o nome do projeto no **Gerenciador de Soluções** e escolhendo **Descarregar Projeto** no menu de contexto ou de clique com o botão direito do mouse. Em seguida, abra o menu de contexto novamente e escolha **Editar \<projectname\>**.

No Visual Studio, o arquivo de projeto é usado pelo **Gerenciador de Soluções** para exibir as configurações e o conteúdo do projeto. Quando você compila seu projeto, o mecanismo do MSBuild consome o arquivo de projeto para criar o executável. Você também pode personalizar os projetos para produzir outros tipos de saída.

## <a name="solutions"></a>Soluções

Um projeto está contido dentro de uma *solução*. Uma solução contém um ou mais projetos relacionados, juntamente com informações de build, configurações de janela do Visual Studio e arquivos diversos que não estão associados a nenhum projeto específico. Uma solução é descrita por um arquivo de texto (extensão *.sln*) com seu próprio formato exclusivo, que não se destina à edição manual.

O Visual Studio usa dois tipos de arquivos (*.sln* e *.suo*) para armazenar configurações de soluções:

|Extensão|Nome|Descrição|
|---------------|----------|-----------------|
|.sln|Solução do Visual Studio|Organiza projetos, itens de projeto e itens de solução na solução.|
|.suo|Opções do usuário da solução|Armazena configurações e personalizações no nível do usuário, como pontos de interrupção.|

## <a name="create-new-projects"></a>Criar novos projetos

A maneira mais fácil de criar um novo projeto é começar de um modelo de projeto para um tipo específico de aplicativo ou site. Um modelo de projeto consiste em um conjunto básico de arquivos de código, arquivos de configuração, ativos e configurações gerados previamente. Esses modelos são os que aparecem na caixa de diálogo **Novo Projeto** quando você escolhe **Arquivo** > **Novo** > **Projeto**. Para obter mais informações, confira [Criar soluções e projetos](../ide/creating-solutions-and-projects.md).

Também é possível criar modelos de item e de projeto personalizados. Para obter mais informações, confira [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md).

## <a name="manage-projects-in-solution-explorer"></a>Gerenciar projetos no Gerenciador de Soluções

Depois de criar um novo projeto, você pode usar o **Gerenciador de Soluções** para exibir e gerenciar o projeto, a solução e seus itens associados. A ilustração a seguir mostra o **Gerenciador de Soluções** com uma solução C# que contém dois projetos:

![Gerenciador de Soluções](../ide/media/vs2015_solution_explorer.png)

## <a name="see-also"></a>Consulte também

- [Visual Studio IDE](../get-started/visual-studio-ide.md)
- [Projetos e soluções (Visual Studio para Mac)](/visualstudio/mac/projects-and-solutions)
- [Adicionar e remover itens do projeto (Visual Studio para Mac)](/visualstudio/mac/add-and-remove-project-items)
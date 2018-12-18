---
title: Soluções e Projetos
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.savedeferredsaveprojectonclose
- vs.untrustedtemplateopeningdocuments
- Project Properties.FullPath
- vs.addnewsolutionitem
- vs.environment.projects
- vs.openproject
- vs.getopenfilename
- vs.addnewitem
- vs.encoding
- vs.addexistingitem
- Project Properties.URL
- VS.SolutionExplorer
- Project Properties.FileName
- SolutionProperties.Name
- VS.SaveChangesDlg
- vs.newproject
- VS.SolutionExplorer.Selection
- SolutionProperties.Path
- vs.getdirectoryname
- vs.addexistingsolutionitem
- SolutionProperties.Description
- vs.environment.solutions
- vs.saveordiscarddeferredsaveproject
- VS.SolutionExplorer.Solutions
helpviewer_keywords:
- vs.solutionpropertypages
- vs.solutionpropertypages.startupproject
- vs.solutionpropertypages.configurationsettings
- solution items, folder in Solution Explorer
- solution items, shared
- solutions [Visual Studio]
- project items [Visual Studio], about project items
- workspaces
- solutions [Visual Studio], designing
- projects [Visual Studio]
- solutions [Visual Studio], projects and
- vs.solutionpropertypages.projectdependencies
- applications [Visual Studio]
- projects [Visual Studio], setting up
- miscellaneous files
ms.assetid: aeaf56cb-c2dd-47f6-b012-23b84b7a7254
caps.latest.revision: 41
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 068fe27df565f83312040fa0bcf6412e4984d9fd
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53067136"
---
# <a name="solutions-and-projects-in-visual-studio"></a>Soluções e projetos no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você cria um app, aplicativo, site da Web, aplicativo Web, script, plug-in, etc no Visual Studio, você começa com um *projeto*. Em um sentido lógico, um projeto contém de todos os arquivos de código-fonte, ícones, imagens, arquivos de dados e qualquer outra coisa que será compilada em um programa executável ou site, ou o que mais for necessário para executar a compilação.  Um projeto também contém todas as configurações de compilador e outros arquivos de configuração que podem ser necessários para diversos serviços ou componentes com os quais seu programa se comunicará.

 Em um sentido literal, um projeto é um arquivo XML (*. vbproj, \*.csproj, \*.vcxproj) que define uma hierarquia de pasta virtual junto com os caminhos para todos os itens que ela "contém" e todas as configurações de build. No Visual Studio, o arquivo de projeto é usado pelo Gerenciador de Soluções para exibir as configurações e o conteúdo do projeto. Quando você compila seu projeto, o mecanismo do MSBuild consome o arquivo de projeto para criar o executável. Você também pode personalizar projetos para produzir outros tipos de saída.

 Um projeto está contido, em um sentido lógico e no sistema de arquivos, em uma *solução*; esta pode conter um ou mais projetos, juntamente com informações de build, configurações de janela do Visual Studio e arquivos diversos que não estão associados a nenhum projeto. Em um sentido literal, a solução é um arquivo de texto com seu próprio formato exclusivo; ele geralmente não se destina a ser editado manualmente.

 Uma solução tem um arquivo *.suo associado que armazena as configurações, preferências e informações de configuração de cada usuário que trabalhou no projeto.

 O diagrama a seguir mostra a relação entre projetos e soluções e os itens que eles contêm logicamente.

 ![Soluções e projetos do Visual Studio](../ide/media/vs2015-project-diagram.png "vs2015_project_diagram")

 Também é possível criar modelos de item e de projeto personalizados. Para obter mais informações, consulte [Criando modelos de item e de projeto](../ide/creating-project-and-item-templates.md).

## <a name="creating-new-projects"></a>Criando novos projetos
 A maneira mais fácil de criar um novo projeto é começar com um modelo de projeto predefinido, que consiste em um conjunto básico de arquivos de código, arquivos de configuração, configurações e ativos gerados previamente que permitem que você comece a criar um tipo específico de aplicativo ou site em uma linguagem de programação específica. Esses modelos são o que você vê na **caixa de diálogo Novo Projeto** quando você escolhe **Arquivo &#124; Novo &#124; Projeto** ou **Arquivo &#124; Novo &#124; Site** no menu principal e, em seguida, navega. Para obter mais informações, consulte [Criando soluções e projetos](../ide/creating-solutions-and-projects.md) e [NIB Criando projetos de modelos](http://msdn.microsoft.com/en-us/7c36d86a-6b79-4480-8228-0f925f1204b2).

## <a name="managing-projects-in-solution-explorer"></a>Gerenciamento de projetos no Gerenciador de Soluções
 Depois de criar um novo projeto, você usa o **Gerenciador de Soluções** para exibir e gerenciar projetos e soluções e seus itens associados. A ilustração a seguir mostra o Gerenciador de Servidores com uma solução em C# que contém dois projetos.

 ![Gerenciador de Soluções](../ide/media/vs2015-solution-explorer.png "vs2015_solution_explorer")

## <a name="in-this-section"></a>Nesta seção

-   [Criando soluções e projetos](../ide/creating-solutions-and-projects.md)

-   [Adicionando e removendo itens de projeto](../ide/adding-and-removing-project-items.md)

-   [Gerenciando propriedades de solução e de projeto](../ide/managing-project-and-solution-properties.md)

-   [Gerenciando referências em um projeto](../ide/managing-references-in-a-project.md)

-   [Propriedades do aplicativo](../ide/application-properties.md)

-   [Gerenciando Assinatura de Assembly e Manifesto](../ide/managing-assembly-and-manifest-signing.md)

-   [Como: Especificar um ícone do aplicativo (Visual Basic, C#)](../ide/how-to-specify-an-application-icon-visual-basic-csharp.md)

-   [Direcionamento de uma versão específica do .NET Framework](../ide/targeting-a-specific-dotnet-framework-version.md)

-   [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)

## <a name="see-also"></a>Consulte também
 [Visual Studio IDE](../ide/visual-studio-ide.md)

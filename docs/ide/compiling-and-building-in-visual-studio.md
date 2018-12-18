---
title: Compilando e criando no Visual Studio
ms.date: 07/14/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-compile
ms.topic: conceptual
helpviewer_keywords:
- builds [Visual Studio], about building in Visual Studio
- custom build steps, types of builds
ms.assetid: c7958821-285f-4e28-9e7a-b5d8b40336a1
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9d2ad9e3e6644f3f0ffc2d4fbf163968f16065f3
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349127"
---
# <a name="compile-and-build-in-visual-studio"></a>Compilar e criar no Visual Studio

Quando você compila o código-fonte, o mecanismo de build cria assemblies e aplicativos executáveis. De modo geral, o processo de compilação é muito semelhante entre vários tipos de projeto diferentes, como Windows, ASP.NET, aplicativos móveis e outros. O processo de build também é semelhante entre as linguagens de programação, como C#, Visual Basic, C++, e F#.

Compilando seu código com frequência, é possível identificar erros rapidamente em tempo de compilação, como sintaxe incorreta, palavras-chave com erros de ortografia e erros de digitação. Também é possível detectar e corrigir erros em tempo de execução, como erros lógicos e semânticos, ao compilar e executar versões de depuração do código.

Um build bem-sucedido valida que o código-fonte do aplicativo contém a sintaxe correta e que todas as referências estáticas a bibliotecas, assemblies e outros componentes podem ser resolvidas. É produzido um aplicativo executável que pode ser testado quanto ao funcionamento adequado em um [ambiente de depuração](../debugger/index.md) e por meio de uma variedade de testes manuais e automatizados para [validar a qualidade do código](../test/improve-code-quality.md). Depois que o aplicativo for completamente testado, você poderá compilar uma versão de lançamento a ser implantada em seus clientes. Para obter uma introdução a esse processo, veja [Passo a passo: Criação de um aplicativo](../ide/walkthrough-building-an-application.md).

Você pode usar qualquer um dos métodos a seguir para compilar um aplicativo: o IDE do Visual Studio, as ferramentas de linha de comando do MSBuild, e o Azure Pipelines:

| Método de build | Benefícios |
| --- |--- | --- |
| IDE |– Criar compilações imediatamente e testá-las em um depurador.<br />– Executar builds em multiprocessador para projetos C++ e C#.<br />– Personalizar diferentes aspectos do sistema de build. |
| Linha de comando do MSBuild| – Criar projetos sem instalar o Visual Studio.<br />– Executar builds em multiprocessador para todos os tipos de projeto.<br />– Personalizar a maioria das áreas do sistema de build.|
| Azure Pipelines | – Automatizar o processo de build como parte de um pipeline de integração contínua/entrega contínua.<br />– Aplicar testes automatizados com cada compilação.<br />– Empregar recursos baseados em nuvem praticamente ilimitados para processos de build.<br />– Modificar o fluxo de trabalho de compilação e, conforme necessário, criar atividades de compilação para realizar tarefas profundamente personalizadas.|

A documentação nesta seção detalha mais o processo de compilação baseado no IDE. Para obter mais informações sobre os outros métodos, confira [MSBuild](../msbuild/msbuild.md) e [Azure Pipelines](/azure/devops/pipelines/index?view=vsts), respectivamente.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Compilar e criar no Visual Studio para Mac](/visualstudio/mac/compiling-and-building).

## <a name="overview-of-building-from-the-ide"></a>Visão geral da compilação no IDE

Quando você cria um projeto, o Visual Studio cria configurações de compilação padrão para o projeto e para a solução que contém o projeto.  Essas configurações definem a maneira como as soluções e os projetos são criados e implantados. Configurações de projeto, em particular, são exclusivas a uma plataforma de destino (por exemplo, o Windows ou Linux) e tipo de build (por exemplo, depuração ou lançamento). Você pode editar essas configurações como quiser e também pode criar suas próprias configurações, conforme necessário.

Para obter uma introdução à compilação com o IDE, veja [Passo a passo: Criação de um aplicativo](walkthrough-building-an-application.md).

Em seguida, consulte [Compilando e limpando projetos e soluções no Visual Studio](building-and-cleaning-projects-and-solutions-in-visual-studio.md) para saber mais sobre as personalizações de diferentes aspectos que você pode fazer no processo. As personalizações incluem [alterar diretórios de saída](how-to-change-the-build-output-directory.md), [especificar eventos de build personalizados](specifying-custom-build-events-in-visual-studio.md), [gerenciar dependências do projeto](how-to-create-and-remove-project-dependencies.md), [gerenciar arquivos de log de build](how-to-view-save-and-configure-build-log-files.md) e [suprimir avisos do compilador](how-to-suppress-compiler-warnings.md).

A partir daí, você pode explorar uma variedade de outras tarefas:
- [Compreender configurações de build](understanding-build-configurations.md)
- [Compreender plataformas de build](understanding-build-platforms.md)
- [Gerenciar propriedades de solução e de projeto](managing-project-and-solution-properties.md).
- Especificar eventos de build em [C#](how-to-specify-build-events-csharp.md) e [Visual Basic](how-to-specify-build-events-visual-basic.md).
- [Definir opções de build](reference/options-dialog-box-projects-and-solutions-build-and-run.md)
- [Compilar vários projetos paralelamente](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md).

## <a name="see-also"></a>Consulte também

- [Criar (compilar) projetos de site](https://msdn.microsoft.com/Library/a9cbb88c-8fff-4c67-848b-98fbfd823193)
- [Compilar e criar (Visual Studio para Mac)](/visualstudio/mac/compiling-and-building)
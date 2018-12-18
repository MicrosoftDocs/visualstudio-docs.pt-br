---
title: Compilando e criando
description: Este artigo descreve como compilar e criar projetos e soluções no Visual Studio para Mac
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.assetid: FB253757-DB00-4889-A6BF-E44722E25BD1
ms.openlocfilehash: fece226d9e7fd7ba023369928171553c393b46d5
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51294312"
---
# <a name="compiling-and-building-in-visual-studio-for-mac"></a>Compilação e criação no Visual Studio para Mac

O Visual Studio para Mac pode ser usado para compilar aplicativos e criar assemblies durante o desenvolvimento do seu projeto. É importante compilar e criar seu código antecipadamente e com frequência para poder identificar tipos incompatíveis e outros erros do tempo de compilação.

## <a name="building-from-the-ide"></a>Compilando no IDE

Usar o Visual Studio para Mac permite criar e executar builds imediatamente, fornecendo ainda controle sobre a funcionalidade de build. O Visual Studio para Mac usa o MSBuild como o sistema de build subjacente.

Todos os Projetos e Soluções criados no IDE terão uma configuração de build padrão, que define o contexto para builds. Essas configurações podem ser editadas ou você pode criar suas próprias. Criar ou modificar essas configurações atualizará automaticamente o arquivo de projeto, que é usado pelo MSBuild para compilar o projeto.

Para obter mais informações sobre como compilar projetos e soluções no IDE, consulte o guia [Compilação e limpeza de Projetos e Soluções](building-and-cleaning-projects-and-solutions.md).

O Visual Studio para Mac também pode ser usado para fazer o seguinte:

* Alterar o caminho de saída. Isso é editado nas opções do Projeto:

    ![Alterar o caminho de saída](media/compiling-and-building-image4.png)

* Alterar o nível de detalhes da saída de build:

    ![Alterar o nível de detalhes de build](media/compiling-and-building-image5.png)

* Adicione comandos personalizados antes, durante ou depois da Compilação ou Limpeza:

    ![adicionar comandos personalizados](media/compiling-and-building-image6.png)

## <a name="building-from-command-line"></a>Compilação na linha de comando

É possível usar o Microsoft Build Engine para compilar aplicativos por meio da linha de comando.

Consulte o conteúdo do [MSBuild](/visualstudio/msbuild/msbuild) para ver mais informações sobre como usar o MSBuild.

## <a name="building-from-azure-pipelines"></a>Compilação no Azure Pipelines

* [Compilar seu aplicativo Xamarin](/vsts/pipelines/apps/mobile/xamarin?view=vsts&tabs=vsts)
* [Integração contínua com o Xamarin](https://developer.xamarin.com/guides/cross-platform/ci/)

## <a name="see-also"></a>Consulte também

- [Compilar e criar (Visual Studio no Windows)](/visualstudio/ide/compiling-and-building-in-visual-studio)
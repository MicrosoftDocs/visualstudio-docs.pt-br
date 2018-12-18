---
title: Compilando e Limpando Projetos e Soluções
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-compile
ms.topic: conceptual
f1_keywords:
- VS.BuildProjectPicker
- vs.batchbuild
helpviewer_keywords:
- Clean Solution command
- builds [Visual Studio], managing
- solution build configurations, starting
- Build Solution command
- project build configurations, starting
- build configurations, starting
- project build configurations, dependencies
- Rebuild Solution command
- solution build configurations, build order
- builds [Visual Studio], preparing
ms.assetid: 710891fd-379e-42c2-a84b-44a7af694ca0
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c96a3b6699428b156a23ad643eb7958cb438b994
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349264"
---
# <a name="build-and-clean-projects-and-solutions-in-visual-studio"></a>Criar e limpar projetos e soluções no Visual Studio

Usando os procedimentos neste tópico, é possível criar, recriar ou limpar todos ou alguns projetos ou itens de projeto em uma solução. Para ver um tutorial passo a passo, veja [Instruções passo a passo: criação de um aplicativo](../ide/walkthrough-building-an-application.md).

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Criar e limpar projetos e soluções no Visual Studio para Mac](/visualstudio/mac/building-and-cleaning-projects-and-solutions).

> [!NOTE]
> A interface do usuário na sua edição do Visual Studio pode ser diferente do que este tópico descreve, dependendo das suas configurações ativas. Para alterar as configurações, por exemplo, para configurações **Gerais** ou do **Visual C++**, escolha **Ferramentas** > **Importar e Exportar Configurações** e, em seguida, escolha **Redefinir todas as configurações**.

## <a name="to-build-rebuild-or-clean-an-entire-solution"></a>Para criar, recriar ou limpar uma solução inteira

1.  No **Gerenciador de Soluções**, escolha ou abra a solução.

2.  Na barra de menus, escolha **Compilar** e, em seguida, escolha um dos comandos a seguir:

    -   Escolha **Compilar** ou **Compilar Solução** para compilar somente esses componentes e arquivos de projeto e componentes que foram alterados desde o build mais recente.

        > [!NOTE]
        > O comando **Compilar** torna-se **Compilar Solução** quando uma solução inclui mais de um projeto.

    -   Escolha **Recompilar Solução** para "limpar" a solução e, em seguida, crie todos os arquivos de projeto e componentes.

    -   Escolha **Limpar Solução** para excluir arquivos de saída e intermediários. Com apenas os arquivos de projeto e de componente restantes, novas instâncias dos arquivos de saída e intermediários podem ser criadas.

## <a name="to-build-or-rebuild-a-single-project"></a>Para compilar ou recompilar um único projeto

1.  No **Gerenciador de Soluções**, escolha ou abra o projeto.

2.  Na barra de menus, escolha **Compilar** e, em seguida, escolha **Compilar** *ProjectName* ou **Recompilar** *ProjectName*.

    -   Escolha **Compilar** *ProjectName* para compilar somente os componentes de projeto alterados desde o build mais recente.

    -   Escolha **Recompilar** *ProjectName* para "limpar" o projeto e, em seguida, compile os arquivos de projeto e todos os componentes do projeto.

## <a name="to-build-only-the-startup-project-and-its-dependencies"></a>Para compilar apenas o projeto de inicialização e suas dependências

1.  Na barra de menus, escolha **Ferramentas** > **Opções**.

2.  Na caixa de diálogo **Opções**, expanda o nó **Projetos e Soluções** e, em seguida, escolha a página **Compilar e Executar**.

     A caixa de diálogo **Compilar e Executar** > **Projetos e Soluções** > **Opções** é aberta.

3.  Marque a caixa de seleção **Compilar apenas projetos de inicialização e dependências ao Executar**.

     Quando essa caixa de seleção estiver marcada, somente o projeto de inicialização atual e suas dependências serão compilados quando você executar qualquer uma das seguintes etapas:

    -   Na barra de menus, escolha **Depurar** > **Iniciar** (**F5**).

    -   Na barra de menus, escolha **Compilar** > **Compilar Solução** (**Ctrl**+**Shift**+**B**).

    Quando essa caixa de seleção estiver desmarcada, todos os projetos, suas dependências e os arquivos de solução serão compilados quando você executar um dos comandos anteriores. Por padrão, essa caixa de seleção está desmarcada.

## <a name="to-build-only-the-selected-visual-c-project"></a>Para compilar somente o projeto Visual C++ selecionado

Escolha um projeto [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] e, em seguida, na barra de menus, escolha **Compilar** > **Somente Projeto** e um dos seguintes comandos:

- **Somente build** *ProjectName*

- **Somente Recompilação** *ProjectName*

- **Somente Limpeza** *ProjectName*

- **Somente Vinculação** *ProjectName*

Esses comandos são aplicáveis somente ao projeto [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] escolhido, sem compilar, recompilar, limpar ou vincular as dependências do projeto ou os arquivos de solução. Dependendo da sua versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], o submenu **Somente Projeto** pode conter mais comandos.

## <a name="to-compile-multiple-c-project-items"></a>Para compilar vários itens de projeto C++

Em **Gerenciador de Soluções**, escolha vários arquivos que possam ter ações compiladas, abra o menu de atalho para um desses arquivos e, em seguida, escolha **Compilar**.

Se os arquivos tiverem dependências, os arquivos serão compilados em ordem de dependência. A operação de compilação falhará se os arquivos exigirem um cabeçalho pré-compilado que não está disponível quando você compila. A operação de compilação usa a configuração de solução ativa atual.

## <a name="to-stop-a-build"></a>Para interromper um build

Execute uma das seguintes etapas:

- Na barra de menus, selecione **Compilar** > **Cancelar**.

- Pressione **Ctrl**+**Interromper**.

## <a name="see-also"></a>Consulte também

- [Como exibir, salvar e configurar arquivos de log de build](../ide/how-to-view-save-and-configure-build-log-files.md)
- [Obter logs de build](../msbuild/obtaining-build-logs-with-msbuild.md)
- [Compilar e criar](../ide/compiling-and-building-in-visual-studio.md)
- [Noções sobre configurações de compilação](../ide/understanding-build-configurations.md)
- [Como definir configurações de depuração e versão](../debugger/how-to-set-debug-and-release-configurations.md)
- [Referência de compilação C/C++](/cpp/build/reference/c-cpp-building-reference)
- [Opções de linha de comando do Devenv](../ide/reference/devenv-command-line-switches.md)
- [Soluções e Projetos](../ide/solutions-and-projects-in-visual-studio.md)
- [Criar e limpar projetos e soluções (Visual Studio para Mac)](/visualstudio/mac/building-and-cleaning-projects-and-solutions)
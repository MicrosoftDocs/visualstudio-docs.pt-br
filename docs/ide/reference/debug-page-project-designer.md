---
title: Página de Depuração, Designer de Projeto
ms.date: 06/27/2018
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesDebug
helpviewer_keywords:
- Project Designer, Debug page
- Debug page in Project Designer
ms.assetid: ef11eae9-df96-4e20-aabd-2678ba317140
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 406b3ecdc0e4e3f0d45c22fc9201bd37c6031152
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418737"
---
# <a name="debug-page-project-designer"></a>Página de Depuração, Designer de Projeto

Use a página **Depurar** do **Designer de Projeto** para definir as propriedades do comportamento de depuração em um projeto do Visual Basic ou C#.

Para acessar a página **Depurar**, selecione um nó do projeto no **Gerenciador de Soluções**. No menu **projeto** , escolha ** \<ProjectName> Propriedades**. Quando o **Designer de Projeto** for exibido, clique na guia **Depurar**.

> [!NOTE]
> Este tópico não se aplica a aplicativos UWP. Confira [Iniciar uma sessão de depuração (VB, C#, C++ e XAML)](../../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md) para aplicativos UWP.

## <a name="configuration-and-platform"></a>Configuração e plataforma

As opções a seguir permitem selecionar a configuração e a plataforma a ser exibida ou modificada.

**Configuration**

Especifica quais definições de configuração exibir ou modificar. As configurações podem ser **Depurar** (padrão), **Versão** ou **Todas as Configurações**.

**Plataforma**

Especifica quais configurações de plataforma exibir ou modificar. As opções podem incluir **Qualquer CPU** (padrão), **x64** e **x86**.

## <a name="start-action"></a>Iniciar ação

A **ação iniciar** indica o item a ser iniciado quando o aplicativo é depurado: o projeto, um programa personalizado, uma URL ou nada. Por padrão, essa opção é definida como **Iniciar projeto**. A configuração **Iniciar ação** na página **Depurar** determina o valor da propriedade `StartAction`.

**Iniciar projeto**

Escolha esta opção para especificar que o executável (para projetos de aplicativos do Windows e aplicativos de console) deve ser iniciado quando o aplicativo for depurado. Essa opção é habilitada por padrão.

**Iniciar programa externo**

Escolha esta opção para especificar que um programa específico deve ser iniciado quando o aplicativo for depurado.

**Iniciar navegador com URL**

Escolha esta opção para especificar que uma URL específica deve ser acessada quando o aplicativo for depurado.

## <a name="start-options"></a>Opções de inicialização

**Argumentos de linha de comando**

Nesta caixa de texto, digite os argumentos de linha de comando a serem usados para depuração.

**Diretório de trabalho**

Nesta caixa de texto, insira o diretório do qual o projeto será inicializado. Ou clique no botão Procurar (**...**) para escolher um diretório.

**Usar computador remoto**

Para depurar o aplicativo de um computador remoto, marque esta caixa de seleção e insira o caminho para o computador remoto na caixa de texto.

## <a name="debugger-engines"></a>Mecanismos do depurador

**Habilitar depuração de código nativo**

Esta opção especifica se a depuração de código nativo tem suporte. Marque esta caixa de seleção se você estiver fazendo chamadas para objetos COM ou se iniciar um programa personalizado escrito em código nativo que chama o seu projeto e você precisar depurar o código nativo. Desmarque esta caixa de seleção para desabilitar a depuração de código não gerenciado. Essa caixa de seleção é desmarcada por padrão.

**Habilitar depuração do SQL Server**

Marque ou desmarque esta caixa de seleção para habilitar ou desabilitar a depuração de procedimentos SQL de seu aplicativo do Visual Basic. Essa caixa de seleção é desmarcada por padrão.

## <a name="see-also"></a>Veja também

- [Introdução ao depurador](../../debugger/debugger-feature-tour.md)
- [Definições do projeto para configurações de depuração do C#](../../debugger/project-settings-for-csharp-debug-configurations.md)
- [Definições do projeto para uma configuração de depuração do Visual Basic](../../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [Proteger aplicativos ClickOnce](../../deployment/securing-clickonce-applications.md)
- [Como: criar e editar configurações](../../ide/how-to-create-and-edit-configurations.md)

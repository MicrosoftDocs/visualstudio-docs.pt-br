---
title: Página de Depuração, Designer de Projeto | Microsoft Docs
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
- vb.ProjectPropertiesDebug
helpviewer_keywords:
- Project Designer, Debug page
- Debug page in Project Designer
ms.assetid: ef11eae9-df96-4e20-aabd-2678ba317140
caps.latest.revision: 37
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f16abf5fbf21678187a22efc9a368df7785057ab
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49271356"
---
# <a name="debug-page-project-designer"></a>Página de Depuração, Designer de Projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
> [!WARNING]
>  Este tópico não se aplica a aplicativos da Windows Store. Consulte [Iniciar uma sessão de depuração (VB, C#, C++ e XAML)](../../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md) no Centro de Desenvolvimento do Windows.  
  
 Use a página **Depurar** do **Designer de Projeto** para definir as propriedades do comportamento de depuração em um projeto do Visual Basic ou C#.  
  
 Para acessar a página **Depurar**, selecione um nó do projeto no **Gerenciador de Soluções**. No menu **Projeto**, escolha _ProjectName_**Propriedades**. Quando o **Designer de Projeto** for exibido, clique na guia **Depurar**.  
  
## <a name="configuration-and-platform"></a>Configuração e plataforma  
 As opções a seguir permitem selecionar a configuração e a plataforma a ser exibida ou modificada.  
  
 **Configuração**  
 Especifica quais definições de configuração exibir ou modificar. As configurações podem ser **Depurar** (padrão), **Versão** ou **Todas as Configurações**. Para obter mais informações, consulte [Configurações de projeto de depuração e versão](http://msdn.microsoft.com/en-us/0440b300-0614-4511-901a-105b771b236e).  
  
 **Plataforma**  
 Especifica quais configurações de plataforma exibir ou modificar. As opções podem incluir **Qualquer CPU** (padrão), **x64** e **x86**. Para obter mais informações, consulte [Configurações de projeto de depuração e versão](http://msdn.microsoft.com/en-us/0440b300-0614-4511-901a-105b771b236e).  
  
## <a name="start-action"></a>Iniciar ação  
 **Iniciar ação** indica o item a ser iniciado quando o aplicativo for depurado: o projeto, um programa personalizado, uma URL ou nada. Por padrão, essa opção é definida como **Iniciar projeto**. A configuração **Iniciar ação** na página **Depurar** determina o valor da propriedade `StartAction`.  
  
 **Iniciar projeto**  
 Escolha esta opção para especificar que o executável (para projetos de aplicativos do Windows e aplicativos de console) deve ser iniciado quando o aplicativo for depurado. Essa opção é habilitada por padrão.  
  
 **Iniciar programa externo**  
 Escolha esta opção para especificar que um programa específico deve ser iniciado quando o aplicativo for depurado.  
  
 **Iniciar Navegador com URL**  
 Escolha esta opção para especificar que uma URL específica deve ser acessada quando o aplicativo for depurado.  
  
## <a name="start-options"></a>Opções de Inicialização  
 **Argumentos de linha de comando**  
 Nesta caixa de texto, digite os argumentos de linha de comando a serem usados para depuração.  
  
 **Diretório de trabalho**  
 Nesta caixa de texto, insira o diretório do qual o projeto será inicializado. Ou clique no botão Procurar (**...**) para escolher um diretório.  
  
 **Usar computador remoto**  
 Para depurar o aplicativo de um computador remoto, marque esta caixa de seleção e insira o caminho para o computador remoto na caixa de texto.  
  
## <a name="enable-debuggers"></a>Habilitar Depuradores  
 **Habilitar depuração de código não gerenciado**  
 Esta opção especifica se a depuração de código nativo tem suporte. Marque esta caixa de seleção se você estiver fazendo chamadas para objetos COM ou se iniciar um programa personalizado escrito em código nativo que chama o seu projeto e você precisar depurar o código nativo. Desmarque esta caixa de seleção para desabilitar a depuração de código não gerenciado. Por padrão, a caixa de seleção fica desmarcada.  
  
 **Habilitar depuração do SQL Server**  
 Marque ou desmarque esta caixa de seleção para habilitar ou desabilitar a depuração de procedimentos SQL de seu aplicativo do Visual Basic. Por padrão, a caixa de seleção fica desmarcada.  
  
 **Habilitar o processo de hospedagem do Visual Studio**  
 Marque esta caixa de seleção para habilitar o processo de hospedagem do Visual Studio. Por padrão, a caixa de seleção fica marcada. Para obter mais informações, consulte [Processo de hospedagem (vshost.exe)](../../ide/hosting-process-vshost-exe.md).  
  
 Para depurar em uma zona de segurança, você precisa habilitar essa opção e **Depurar este aplicativo com o conjunto de permissões selecionado** na [Caixa de diálogo Configurações de Segurança Avançadas](../../ide/reference/advanced-security-settings-dialog-box.md).  
  
## <a name="see-also"></a>Consulte também  
 [Depurando no Visual Studio](../../debugger/debugging-in-visual-studio.md)   
 [Configurações do projeto para configurações de depuração de C#](../../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Configurações do projeto para uma configuração de depuração do Visual Basic](../../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [Gerenciando propriedades de depuração](http://msdn.microsoft.com/en-us/92474d16-e7fe-4fac-9287-6bd6b3a7eb68)   
 [Como depurar um aplicativo ClickOnce com permissões restritas](../../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)   
 [Como criar e editar configurações](../../ide/how-to-create-and-edit-configurations.md)




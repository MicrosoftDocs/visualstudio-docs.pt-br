---
title: Configurações do projeto para um C# configuração de depuração | Microsoft Docs
ms.custom: seodec18
ms.date: 11/21/2018
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debug configurations, C#
- project settings [Visual Studio], debug configurations
- debug builds, project settings
- projects [Visual Studio], debug configurations
- project configurations, debug
- debugging [C#], debugger settings
ms.assetid: e30ca810-66e9-4d6e-9cf6-9f285cd0b100
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 6de7bfd547516b227063c0d3143b508bcbd9ddfd
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53059266"
---
# <a name="project-settings-for--c-debug-configurations"></a>Configurações do projeto para configurações de depuração do C#

Você pode alterar C# configurações de depuração no projeto do [guia de depuração](#debug-tab) e [guia Build](#build-tab) das páginas de propriedades de projeto. 

Para abrir as páginas de propriedades, selecione o projeto no **Gerenciador de soluções** e, em seguida, selecione o **Properties** ícone, ou clique com botão direito no projeto e selecione **propriedades**.

Para obter mais informações, confira [Configurações de depuração e lançamento](how-to-set-debug-and-release-configurations.md). 

>[!IMPORTANT]
>Essas configurações não se aplicam a aplicativos .NET Core, ASP.NET ou UWP. Para definir configurações de depuração para aplicativos UWP, consulte [iniciar uma sessão de depuração para um aplicativo UWP](start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md).  
  
## <a name="debug-tab"></a>Guia Depurar  
  
|Configuração|Descrição|
|-------------------------------------| - |
| **Configuração** | Define o modo para compilar o aplicativo. Selecione **ativa (depuração)**, **Debug**, **versão**, ou **todas as configurações de** na lista suspensa. |
| **Iniciar ação** | Especifica a ação quando você seleciona **iniciar** em uma configuração de depuração.<br />- **Iniciar projeto** é o padrão e inicia o projeto de inicialização para depuração. Para obter mais informações, consulte [escolha o projeto de inicialização](/previous-versions/visualstudio/visual-studio-2010/0s590bew(v=vs.100)).<br />- **Iniciar programa externo** inicia e anexa a um aplicativo que não é parte de um [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] projeto. Para obter mais informações, consulte [anexar a processos em execução com o depurador](attach-to-running-processes-with-the-visual-studio-debugger.md).<br />- **Iniciar navegador com URL** permite depurar um aplicativo web. |
| **Opções de inicialização** > **argumentos de linha de comando** | Especifica argumentos de linha de comando para o aplicativo que está sendo depurado. O nome do comando é o nome do aplicativo especificado na **Iniciar programa externo**. |
| **Opções de inicialização** > **diretório de trabalho** | Especifica o diretório de trabalho do aplicativo que está sendo depurado. No C#, é o diretório de trabalho *\bin\debug* por padrão.
| **Opções de inicialização** > **usar computador remoto**|Para depuração remota, selecione essa opção e digite o nome do destino de depuração remoto, ou um [nome do servidor Msvsmon](../debugger/remote-debugging.md). <br />O local de um aplicativo no computador remoto é especificado pela **caminho de saída** propriedade no **Build** guia. O local deve ser um diretório compartilhável no computador remoto. 
| **Mecanismo de depuração** > **habilitar a depuração de código não gerenciado** | Depura chamadas para código nativo do Win32 (não gerenciado) de aplicativo gerenciado. |
| **Mecanismo de depuração** > **depuração de habilitar o SQL Server** | Depura o objetos de banco de dados do SQL Server. |
  
## <a name="build-tab"></a>Guia Compilação  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**Gerais** > **símbolos de compilação condicional**|Se selecionado, defina as constantes DEBUG e TRACE.<br /><br /> Essas constantes habilitam a compilação condicional da [Classe Debug](/dotnet/api/system.diagnostics.debug) e da [Classe Trace](/dotnet/api/system.diagnostics.trace). Com essas constantes definidas, os métodos da classe Debug e Trace geram saída para a [Janela de Saída](../ide/reference/output-window.md). Sem essas constantes, os métodos da classe Debug e Trace não são compilados e nenhuma saída será gerada.<br /><br />Geralmente, DEBUG é definido na versão de depuração de um build e indefinida na versão de lançamento. RASTREAMENTO é definido em versões de depuração e versão.|  
|**Gerais** > **otimizar código**|A menos que um bug aparece apenas em código otimizado, deixe essa configuração desmarcada para compilações de depuração. Código otimizado é mais difícil de depurar, porque as instruções não correspondem diretamente às instruções no código-fonte.|  
|**Saída** > **caminho de saída**|Normalmente definido para *bin\Debug* para depuração.|
|**Advanced** botão|Para obter informações sobre opções avançadas de depuração, consulte [caixa de diálogo Configurações avançadas de compilação (C#)](../ide/reference/advanced-build-settings-dialog-box-csharp.md). O formato portátil para o símbolo (*. PDB*) arquivos é um formato recente de plataforma cruzada para aplicativos .NET Core. 
  
## <a name="see-also"></a>Consulte também  
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)
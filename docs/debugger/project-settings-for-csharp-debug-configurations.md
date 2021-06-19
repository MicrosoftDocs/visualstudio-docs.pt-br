---
title: Configurações do projeto para uma configuração de depuração em C# | Microsoft Docs
description: Entenda como alterar as configurações de projeto para uma configuração de depuração C# no Visual Studio, usando a guia Depurar e a guia Build das páginas de propriedades do projeto.
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
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
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 3377187412f95e090c7403ddd6f898a18f6cec9f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386495"
---
# <a name="project-settings-for--c-debug-configurations"></a>Configurações do projeto para configurações de depuração do C#

Você pode alterar as configurações de depuração do projeto C# na guia [Depurar](#debug-tab) e [na guia Build](#build-tab) das páginas de propriedades do projeto.

Para abrir as páginas de  propriedades, selecione o projeto  no Gerenciador de Soluções, selecione o ícone Propriedades ou clique com o botão direito do mouse no projeto e selecione **Propriedades**.

Para obter mais informações, consulte [Configurações de depuração e versão.](how-to-set-debug-and-release-configurations.md)

>[!IMPORTANT]
>Essas configurações não se aplicam a aplicativos .NET Core, ASP.NET ou UWP. Para definir as configurações de depuração para aplicativos UWP, consulte Iniciar uma [sessão de depuração para um aplicativo UWP](start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md).

## <a name="debug-tab"></a>Guia de depuração

|Configuração|Descrição|
|-------------------------------------| - |
| **Configuração** | Define o modo para criar o aplicativo. Selecione **Ativo (Depurar),** **Depurar**, **Liberar** ou Todas **as Configurações** na lista suspenso. |
| **Iniciar ação** | Especifica a ação quando você seleciona Iniciar **em** uma configuração de Depuração.<br />- **Iniciar projeto** é o padrão e inicia o projeto de inicialização para depuração. Para obter mais informações, consulte [Escolher o projeto de inicialização](/previous-versions/visualstudio/visual-studio-2010/0s590bew(v=vs.100)).<br />- **Iniciar programa externo** é iniciado e anexado a um aplicativo que não faz parte de um [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] projeto. Para obter mais informações, consulte [Anexar a processos em execução com o depurador](attach-to-running-processes-with-the-visual-studio-debugger.md).<br />- **Iniciar navegador com URL** permite depurar um aplicativo Web. |
| **Opções de início**  >  **Argumentos de linha de comando** | Especifica argumentos de linha de comando para o aplicativo que está sendo depurado. O nome do comando é o nome do aplicativo especificado em **Iniciar programa externo.** |
| **Opções de início**  >  **Diretório de trabalho** | Especifica o diretório de trabalho do aplicativo que está sendo depurado. Em C#, o diretório de trabalho *é \bin\debug* por padrão.
| **Opções de início**  >  **Usar computador remoto**|Para depuração remota, selecione essa opção e insira o nome do destino de depuração remota ou um nome de servidor [Msvsmon](../debugger/remote-debugging.md). <br />O local de um aplicativo no computador remoto é especificado pela propriedade **Caminho** de Saída na **guia Build.** O local deve ser um diretório compartilhável no computador remoto.
| **Mecanismo do depurador**  >  **Habilitar a depuração de código nãomanageda** | Depura chamadas para código Win32 nativo (não gerenciado) do aplicativo gerenciado. |
| **Mecanismo do depurador**  >  **Habilitar SQL Server depuração** | Depura SQL Server de banco de dados. |

## <a name="build-tab"></a>Guia Compilação

|Configuração|Descrição|
|-------------|-----------------|
|**Geral**  >  **Símbolos de compilação condicional**|Defina as constantes DEBUG e TRACE se selecionadas.<br /><br /> Essas constantes habilitam a compilação condicional da [Classe Debug](/dotnet/api/system.diagnostics.debug) e da [Classe Trace](/dotnet/api/system.diagnostics.trace). Com essas constantes definidas, os métodos da classe Debug e Trace geram saída para a [Janela de Saída](../ide/reference/output-window.md). Sem essas constantes, os métodos da classe Debug e Trace não são compilados e nenhuma saída será gerada.<br /><br />Normalmente, DEBUG é definido na versão de depuração de um build e indefinido na versão de lançamento. TRACE é definido nas versões Depurar e Versão.|
|**Geral**  >  **Otimizar o código**|A menos que um bug apareça apenas no código otimizado, deixe essa configuração desseleção para builds de depuração. O código otimizado é mais difícil de depurar, pois as instruções não correspondem diretamente às instruções no código-fonte.|
|**Saída**  >  **Caminho de saída**|Normalmente definido como *bin\Debug para* depuração.|
|**Botão** Avançado|Para obter informações sobre opções avançadas de depuração, consulte Caixa de [diálogo Configurações de build avançadas (C#)](../ide/reference/advanced-build-settings-dialog-box-csharp.md). O formato portátil para arquivos de símbolo (*.pdb*) é um formato recente de plataforma cruzada para aplicativos .NET Core.

## <a name="see-also"></a>Confira também
- [Configurações e preparação do depurador](../debugger/debugger-settings-and-preparation.md)
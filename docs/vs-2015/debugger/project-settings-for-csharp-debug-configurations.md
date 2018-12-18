---
title: Configurações do projeto para configurações de depuração do c# | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debug configurations, C#
- debugging [J#], debugger settings
- project settings [Visual Studio], debug configurations
- debug builds, project settings
- projects [Visual Studio], debug configurations
- project configurations, debug
- debugging [C#], debugger settings
- debug configurations, J#
ms.assetid: e30ca810-66e9-4d6e-9cf6-9f285cd0b100
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 07da36adc1615217315d5ebb23f8ef62db59f5c7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51721174"
---
# <a name="project-settings-for--c-debug-configurations"></a>Definições do projeto para configurações de depuração do C#
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode alterar as configurações de projeto para uma configuração de depuração c# na **páginas de propriedades** janela, conforme discutido na [Debug and Release Configurations](../debugger/how-to-set-debug-and-release-configurations.md). As tabelas a seguir mostram onde localizar configurações relacionadas ao depurador na **páginas de propriedade** janela.  
  
> [!WARNING]
>  Este tópico não se aplica a aplicativos da Windows Store. Consulte [iniciar uma sessão de depuração (VB, c#, C++ e XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)  
  
##  <a name="BKMK_Debug_tab"></a> Guia depurar  
  
|**Configuração**|**Descrição**|  
|-----------------|---------------------|  
|**Configuração**|Define o modo para compilar o aplicativo. Escolher entre **ativa (depuração)**, **Debug**, **versão**, **todas as configurações de**.|  
|**Iniciar ação**|Esse grupo de controles especifica a ação que ocorrerá quando você escolhe Iniciar do menu Depurar.<br /><br /> -   **Iniciar projeto** é o padrão e inicia o projeto de inicialização para depuração. Para obter mais informações, consulte [escolhendo o projeto de inicialização](http://msdn.microsoft.com/en-us/222e3f32-a6fe-4941-bf37-6b2a921129fd).<br />-   **Iniciar programa externo** permite que você inicie e anexe a um programa que não faz parte de um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto. Para obter mais informações, consulte [anexar a um programa em execução](http://msdn.microsoft.com/en-us/636d0a52-4bfd-48d2-89ad-d7b9ca4dc4f4).<br />-   **Inicie o navegador na URL** permite que você depure um aplicativo da Web.|  
|**Argumentos de linha de comando**|Especifica argumentos de linha de comando para o programa ser depurado. O nome do comando é o nome do programa especificado em Iniciar programa externo. Se Iniciar Ação for definida para iniciar URL, os argumentos de linha de comando não podem ser especificados.|  
|**Diretório de trabalho**|Especifica o diretório de trabalho do programa que está sendo depurado. No [!INCLUDE[csprcs](../includes/csprcs-md.md)], o diretório de trabalho é o diretório a partir do qual o aplicativo é iniciado de \bin\debug por padrão.|  
|**Usar computador remoto**|O nome de um computador remoto no qual o aplicativo executará para fins de depuração ou um [nome do servidor Msvsmon](http://msdn.microsoft.com/library/55b60ce7-834b-4e83-a10e-fe4248260a4c). O local do EXE no computador remoto é especificado pela propriedade Caminho da Saída na pasta Propriedades de Configuração, categoria Compilação. O local deve ser um diretório compartilhável no computador remoto.|  
|**Habilitar depuração de código não gerenciado**|Permite depurar chamadas para código Win32 nativo (não gerenciado) a partir do seu aplicativo gerenciado.|  
|**Habilitar depuração do SQL Server**|Permite depuração de objetos de banco de dados do SQL Server.|  
  
##  <a name="BKMK_Build_tab"></a> Guia compilação  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**Símbolos de compilação condicional:**|As constantes DEBUG e TRACE são definidas aqui.<br /><br /> Essas constantes habilitam a compilação condicional do [classe Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx) e [classe Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx). Com essas constantes definidas, depurar e métodos de classe de rastreamento geram saída para o [janela de saída](../ide/reference/output-window.md). Sem essas constantes, os métodos da classe Debug e Trace não são compilados e nenhuma saída será gerada.<br /><br /> -Debug normalmente é definido na versão de depuração de um programa e indefinida na versão de lançamento.<br />-Rastreamento geralmente é definido em versões de depuração e versão.|  
|**Otimizar código**|A menos que você encontre um bug que apareça somente no código otimizado, deverá deixar essa configuração desativada na versão de Depuração. O código otimizado é mais difícil de depurar porque as instruções não correspondem diretamente a instruções em suas janelas de origem.|  
|**Caminho de saída:**|Normalmente definido para bin\Debug para depuração.|  
  
## <a name="see-also"></a>Consulte também  
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)




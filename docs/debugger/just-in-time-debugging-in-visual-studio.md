---
title: Desabilitar o depurador Just-In-Time | Microsoft Docs
ms.custom: ''
ms.date: 05/23/18
ms.technology: vs-ide-debug
ms.topic: troubleshooting
helpviewer_keywords:
- debugging [Visual Studio], Just-In-Time
- Just-In-Time debugging
ms.assetid: 14972d5f-69bc-479b-9529-03b8787b118f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 147e16bab14a6a038622804cf9c57e5fdc92bf02
ms.sourcegitcommit: c5e72875206b8c5737c29d5b1ec7b86eec747303
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49382773"
---
# <a name="disable-the-just-in-time-debugger"></a>Desabilitar o depurador Just-In-Time 

A caixa de diálogo do depurador Just-in-pode abrir quando ocorre um erro em um aplicativo em execução e impedir que o aplicativo continue. 

O depurador Just-in-lhe dá a opção de iniciar o Visual Studio para depurar o erro. Você deve ter [Visual Studio](http://visualstudio.microsoft.com) ou outro depurador selecionado instalado para exibir informações detalhadas sobre o erro ou tente depurá-lo. 

Se você for um usuário do Visual Studio e deseja tentar depurar o erro, consulte [depurar usando o depurador Just-in-](../debugger/debug-using-the-just-in-time-debugger.md). Se você não pode corrigir o erro, ou para manter o depurador Just-in-seja aberto, você pode [Just-In-Time de desabilitar a depuração do Visual Studio](debug-using-the-just-in-time-debugger.md#BKMK_Enabling). 

Se você tiver instalado o Visual Studio, mas não há mais não, talvez você precise [Just-In-Time de desabilitar a depuração do registro do Windows](debug-using-the-just-in-time-debugger.md#disable-just-in-time-debugging-from-the-windows-registry). 

Se você não tiver instalado o Visual Studio, você pode impedir que ao desabilitar a depuração de script ou a depuração do lado do servidor de depuração Just-In-Time. 

- Se você estiver tentando executar um aplicativo web, desabilite depuração de script:
  
  No Windows **painel de controle** > **rede e Internet** > **opções da Internet**, selecione **Disable (depuração de script Internet Explorer)** e **Desabilitar depuração de scripts (outros)**. As configurações e as etapas exatas dependem de sua versão do Windows e do navegador.
  
  ![As opções de Internet de JIT](../debugger/media/jitinternetoptions.png "opções da internet do JIT")
  
- Se você estiver hospedando um aplicativo da web ASP.NET no IIS, desabilite a depuração do lado do servidor:

  1. No Gerenciador do IIS **exibição de recursos**, sob o **ASP.NET** seção, clique duas vezes em **compilação do .NET**, ou selecione-o e, em seguida, selecione **abrir recurso**no **ações** painel. 
  1. Sob **comportamento** > **depurar**, selecione **False**. As etapas são diferentes em versões anteriores do IIS.

Depois de desabilitar a depuração Just-In-Time, o aplicativo pode ser capaz de tratar o erro e executado normalmente. 

Se o aplicativo ainda tem um erro sem tratamento, você poderá ver uma mensagem de erro ou o aplicativo pode falhar ou travar. O aplicativo não será executado normalmente até que o erro seja corrigido. Você pode tentar contatar o proprietário do aplicativo e peça para corrigi-lo.


---
title: Localizar o processo ASP.NET em execução | Microsoft Docs
ms.date: 11/04/2018
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- ASP.NET debugging, ASP.NET process
- ASP.NET process
ms.assetid: 931a7597-b0f0-4a28-931d-46e63344435f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: c14067d58289dd0b41fa526937a0553c10934ea7
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349601"
---
# <a name="find-the-name-of-the-aspnet-process"></a>Localizar o nome do processo do ASP.NET

Para depurar um aplicativo em execução [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] , o depurador do Visual Studio deve ser anexado ao [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] processo pelo nome.

**Para descobrir qual processo está executando um aplicativo ASP.NET:**

1. Com o aplicativo em execução, no Visual Studio, selecione **depurar**  >  **anexar ao processo**.

1. Na caixa de diálogo **anexar ao processo** , digite as primeiras letras dos nomes dos processos na lista a seguir ou insira-os na caixa de pesquisa. Aquele que está em execução é aquele que executa o aplicativo ASP.NET. Anexe a esse processo para depurar o aplicativo.

    - O *w3wp.exe* é o IIS 6,0 e posterior.
    - *aspnet_wp.exe* são versões anteriores do IIS.
    - *iisexpress.exe* é IISExpress.
    - *dotnet.exe* ASP.NET Core.
    - *inetinfo.exe* são aplicativos ASP mais antigos em execução no processo.

>[!NOTE]
>O Visual Studio 2012 e o [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] código anterior podem estar no sistema de arquivos e ser executados no servidor de teste *WebDev.WebServer.exe* ou *WebDev.WebServer40.exe*. Nesse caso, para a depuração local, anexe ao *WebDev.WebServer.exe* ou *WebDev.WebServer40.exe* em vez do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] processo.

**Consulte também:**

- [Anexar a um processo em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [Pré-requisitos para depuração remota de aplicativos Web](remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)
- [Requisitos do sistema](../debugger/aspnet-debugging-system-requirements.md)
- [Depurar aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md)
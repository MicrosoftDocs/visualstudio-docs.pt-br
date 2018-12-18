---
title: Localize o processo do ASP.NET em execução | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
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
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: 6bbb2aed6f7218170e26b736d82ba0f3d88b2fae
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51751779"
---
# <a name="find-the-name-of-the-aspnet-process"></a>Localizar o nome do processo do ASP.NET

Para depurar um execução [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] aplicativo, o depurador do Visual Studio deve anexar o [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] processos por nome.

**Para descobrir qual processo está em execução em um aplicativo ASP.NET:**

1. Com o aplicativo em execução no Visual Studio, selecione **Debug** > **anexar ao processo**. 
   
1. No **anexar ao processo** caixa de diálogo, digite as primeiras letras do processo de nomes na lista a seguir ou insira-os na caixa de pesquisa. O que está executando é aquele que executa o aplicativo ASP.NET. Anexe ao processo em questão para depurar o aplicativo. 
   
    - *W3wp.exe* é o IIS 6.0 e posterior. 
    - *aspnet_wp.exe* é versões anteriores do IIS.
    - *iisexpress.exe* é IISExpress.
    - *dotnet.exe* é ASP.NET Core.
    - *Inetinfo.exe* é aplicativos ASP antigos em execução no processo. 

>[!NOTE]
>Visual Studio 2012 e anterior [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] código pode ser no sistema de arquivos e executado no servidor de teste *WebDev.WebServer.exe* ou *WebDev.WebServer40.exe*. Nesse caso, para depuração local, anexar a *WebDev.WebServer.exe* ou *WebDev.WebServer40.exe* em vez do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] processo. 

**Consulte também:**

 [Anexar a um processo em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)  
 [Pré-requisitos para a depuração remota de aplicativos da web](../debugger/prerequistes-for-remote-debugging-web-applications.md)   
 [Requisitos do sistema](../debugger/aspnet-debugging-system-requirements.md)   
 [Depurar aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md)
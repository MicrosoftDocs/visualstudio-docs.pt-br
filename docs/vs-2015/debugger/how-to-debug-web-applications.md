---
title: 'Como: depurar aplicativos Web | Microsoft Docs'
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
- Web services, debugging
- ASP.NET Web Forms, debugging
- ASP.NET, debugging Web applications
- debugging ASP.NET Web applications, during development
ms.assetid: 6440d12e-6b29-42c5-a958-99aeaaff480f
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d2a5110a6801aafb6eaf98cb4fb4164b045b2408
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51793627"
---
# <a name="how-to-debug-web-applications"></a>Como depurar aplicativos Web
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] é a principal tecnologia para o desenvolvimento de aplicativos Web no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. O depurador do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] fornece ferramentas avançadas para depurar aplicativos Web do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] localmente ou em um servidor remoto. Este tópico descreve como depurar um [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] projeto durante o desenvolvimento. Para obter informações sobre como depurar um [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] já implantado em um servidor de produção do aplicativo Web, consulte [Depurando aplicativos de Web implantado](../debugger/debugging-deployed-web-applications.md).  
  
 Para depurar um aplicativo do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]:  
  
-   Você deve ter as permissões necessárias. Para obter mais informações, consulte [System Requirements](../debugger/aspnet-debugging-system-requirements.md).  
  
-   [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] a depuração deve ser habilitada no **propriedades do projeto**.  
  
-   O arquivo de configuração do aplicativo (Web.config) deve ser definido para o modo de depuração. O modo de depuração faz com que o [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] gere símbolos para arquivos gerados dinamicamente e permite que o depurador se anexe ao aplicativo [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] define isso automaticamente quando você inicia a depuração, caso você tenha criado o projeto do modelo Projetos Web.  
  
-   Para obter mais informações, consulte [como: habilitar a depuração para aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md).  
  
### <a name="to-debug-a-web-application-during-development"></a>Para depurar um aplicativo Web durante o desenvolvimento  
  
1.  Sobre o **depurar** menu, clique em **iniciar** para iniciar a depuração do aplicativo Web.  
  
     O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] cria o projeto de aplicativo Web, implanta o aplicativo se for necessário, inicia o ASP.NET Development Server se você estiver depurando localmente e anexa ao processo de trabalho do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)].  
  
2.  Use o depurador para definir e desmarcar pontos de interrupção, depurar e executar outras operações de depuração, como faria para qualquer aplicativo.  
  
     Para obter mais informações, consulte [Noções básicas do depurador](../debugger/debugger-basics.md).  
  
3.  No **Debug** menu, clique em **parar depuração** ao final, a sessão de depuração, ou, no **arquivo** menu no Internet Explorer, clique em **fechar**.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando aplicativos Web e script](../debugger/debugging-web-applications-and-script.md)   
 [Depurando aplicativos ASP.NET e AJAX](../debugger/debugging-aspnet-and-ajax-applications.md)   
 [Instruções: habilitar a depuração para aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md)




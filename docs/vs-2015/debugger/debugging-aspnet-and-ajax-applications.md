---
title: Depurando aplicativos ASP.NET e AJAX | Microsoft Docs
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
- debugging, WCF
- debugging ASP.NET Web applications
- debugging [ASP.NET], about ASP.NET debugging
- WCF, debugging
ms.assetid: 9d531913-541b-47b8-864d-138021fca0c6
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d3a600059f29d7e0034e4e64239798c32d721a1f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51785918"
---
# <a name="debugging-aspnet-and-ajax-applications"></a>Depurando aplicativos ASP.NET e AJAX
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Depurar aplicativos Web do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] é semelhante a depurar o Windows Form ou qualquer outro aplicativo do Windows porque ambos os tipos de aplicativos envolvem controles e eventos. No entanto, também há diferenças básicas entre os dois tipos de aplicativos:  
  
-   Controlar o estado é mais complexo em um aplicativo Web.  
  
-   Em um aplicativo do Windows, o código a ser depurado está na maioria das vezes em um local; em um aplicativo Web, o código pode estar no cliente e no servidor. Embora o código do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] esteja todo no servidor, pode haver também código JavaScript ou código do [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] no cliente.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Preparando para depurar ASP.NET](../debugger/preparing-to-debug-aspnet.md)  
 Descreve as etapas necessárias para habilitar a depuração de aplicativos do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)].  
  
 [Depurando aplicativos Web](../debugger/debugging-web-applications.md)  
 Discute como depurar um aplicativo do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], incluindo aplicativos de script habilitados para AJAX.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md)  
 Explica por que apenas Just My Code deve ser habilitado para depurar exceções do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)].  
  
 [Visão geral de aplicativos Ajax de rastreamento e depuração](http://msdn.microsoft.com/library/92684ea0-7bb4-4a34-9203-3aa6394ce375)  
 Discute algumas técnicas e ferramentas que podem ajudar a depurar seu código AJAX.  
  
 [IntelliTrace](../debugger/intellitrace.md)  
 Depure seu código mais rápido com IntelliTrace para registrar e examinar um histórico do estado do aplicativo sem reiniciar o aplicativo com tanta frequência. Você pode ver informações sobre os eventos e as chamadas que ocorrem durante a execução do aplicativo e começar a depuração a partir desses pontos no tempo. Exige o Visual Studio Ultimate.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Depurando aplicativos Web e script](../debugger/debugging-web-applications-and-script.md)   
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)   
 [Noções básicas do depurador](../debugger/debugger-basics.md)




---
title: 'Erro: Não é possível intervir automaticamente no servidor | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.error.causality_no_server_response
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- remote debugging, notification error
ms.assetid: 9a370ccc-d358-429c-b285-9b6c0649bc68
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fca696fe9afc979d6775c5b2e97eebb5d82c266c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51747825"
---
# <a name="error-unable-to-automatically-step-into-the-server"></a>Erro: não é possível intervir automaticamente no servidor
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O erro é:  
  
 Não é possível realizar a depuração completa do servidor automaticamente. O depurador não foi notificado antes do procedimento remoto ter sido executado  
  
 Esse erro pode ocorrer quando você está tentando entrar em um serviço web (consulte [passo a passo em um serviço Web XML](http://msdn.microsoft.com/en-us/8e67de38-bf5f-41cc-a457-1b88ce63d764)). Pode ocorrer sempre que o [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] não estiver configurado corretamente.  
  
 Possíveis causas:  
  
-   O arquivo Web. config para seu [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] aplicativo não definiu a depuração como "true" (consulte [modo de depuração em aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md)).  
  
-   Uma versão do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] foi instalado depois que o Visual Studio foi instalado. [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] deve ser instalado antes do Visual Studio. Para corrigir esse problema, use o Windows **painel de controle**, **programas e recursos** para reparar a instalação do Visual Studio.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas e erros de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Depuração remota](../debugger/remote-debugging.md)




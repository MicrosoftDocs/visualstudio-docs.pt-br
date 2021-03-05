---
title: Não é possível entrar automaticamente no servidor | Microsoft Docs
description: Não é possível realizar a depuração completa do servidor automaticamente. O depurador não foi notificado antes da execução do procedimento remoto.
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.causality_no_server_response
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- remote debugging, notification error
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a374afef2dea92fbad72c45e35ca06904d75cbbe
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146477"
---
# <a name="error-unable-to-automatically-step-into-the-server"></a>Erro: não é possível intervir automaticamente no servidor
O erro indica:

 Não é possível realizar a depuração completa do servidor automaticamente. O depurador não foi notificado antes do procedimento remoto ter sido executado

 Esse erro pode ocorrer quando você está tentando entrar em um serviço Web (confira [Entrar em um serviço Web XML](/previous-versions/zc57803s(v=vs.100))). Pode ocorrer sempre que o [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] não estiver configurado corretamente.

 Causas possíveis:

- O arquivo web.config do aplicativo [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] não define a depuração como “true” em (confira [Modo de depuração em aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md)).

- Uma versão do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] foi instalada depois que o Visual Studio foi instalado. [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] deve ser instalado antes do Visual Studio. Para corrigir esse problema, use o **Painel de Controle, Programas e Recursos do Windows** para reparar a instalação do Visual Studio.

## <a name="see-also"></a>Confira também
- [Erros de depuração remota e solução de problemas](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [Depuração remota](../debugger/remote-debugging.md)

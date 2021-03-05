---
description: Esse erro ocorre quando o usuário que está tentando executar o Monitor de Depuração Remota do Visual Studio (msvsmon) não tem uma conta no computador local.
title: O Monitor de Depuração Remota do Microsoft Visual Studio no computador remoto não tem permissão para se conectar a este computador
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.access_denied_oncallback
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- remote debugging, Windows version error
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f35db1d84d0f44eedbc8bf09f1e5ff9a6f49e5f2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146724"
---
# <a name="error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-does-not-have-permission-to-connect-to-this-computer"></a>Erro: o Monitor de Depuração Remota do Microsoft Visual Studio no computador remoto não tem permissão para se conectar a este computador

Esse erro ocorre quando o usuário que está tentando executar o Monitor de Depuração Remota do Visual Studio (msvsmon) não tem uma conta no computador local. Esse erro pode ocorrer quando a depuração remota está usando o mecanismo de depuração herdado.

## <a name="to-fix-this-problem"></a>Para corrigir esse problema

- Adicione uma conta de usuário ao computador host do depurador do Visual Studio, com o mesmo nome e senha que a conta usuário que está executando msvsmon no computador remoto,

   \- ou –

- Execute msvsmon como um usuário que tem permissão para chamar no computador local. Isso significa que o usuário deve ser usuário de domínio e administrador no computador de msvsmon. Você pode especificar a conta de usuário para executar msvsmon de uma de duas maneiras:

  - Clique com o botão direito do mouse no ícone de msvsmon e escolha **Executar como** no menu de atalho

    \- ou –

  - No prompt de comando, execute `runas.exe`.

## <a name="see-also"></a>Confira também

- [Erros de depuração remota e solução de problemas](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [Depuração remota](../debugger/remote-debugging.md)

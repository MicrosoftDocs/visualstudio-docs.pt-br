---
title: Erro-firewall sem autenticação | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.firewall.noauth
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 199e3b203ff73397a49c19a736a447f5823e5422
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460759"
---
# <a name="error-firewall-no-authentication"></a>Erro: firewall sem autenticação
O firewall de conexão da internet no computador remoto não está configurado para permitir a depuração remota. Para a depuração remota com `No Authentication`, o msvsmon.exe deve ser adicionado à lista de exceções. Abrir algumas portas de IPSEC pode ser necessário também.

> [!NOTE]
> O depurador remoto pode configurar automaticamente o Firewall do Windows. Ao usar um firewall diferente do Firewall do Windows como, por exemplo, o firewall do software de terceiros ou um firewall de hardware, o firewall deve ser configurado manualmente para permitir a depuração remota. Para fazer isso, permita o tráfego em portas TCP/IP no qual o msvsmon.exe está escutando. Por padrão, essas são as portas 4018 e 4019, onde 4018 é usado em todos os sistemas operacionais, e 4019 é usado apenas no Windows x64 para permitir depurar os processos x86.

 Para obter mais informações, consulte [depuração remota](../debugger/remote-debugging.md).
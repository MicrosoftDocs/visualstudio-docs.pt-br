---
title: Firewall no computador local | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.firewall.localmachine
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d5f3e57bbac1d2c293c5a9f910beca5484db06cc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99871587"
---
# <a name="error-firewall-on-local-machine"></a>Erro: firewall na máquina local
O firewall de conexão da Internet no computador local, o computador no qual você está executando o Visual Studio, não está configurado para permitir a depuração remota. Para a depuração remota gerenciada ou nativa com o transporte padrão, a porta TCP 135 deve estar aberta para o tráfego de DCOM. O compartilhamento de arquivos e impressoras deve ser aberto e o devenv.exe deve ser adicionado à lista de exceções. Abrir algumas portas de IPSEC pode ser necessário também.

 Para obter mais informações, consulte [depuração remota](../debugger/remote-debugging.md).
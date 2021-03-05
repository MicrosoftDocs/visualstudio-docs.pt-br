---
description: Um erro DCOM ocorreu quando o computador remoto tentou se comunicar com o computador local.
title: O computador remoto não pôde iniciar as comunicações DCOM | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.unmarshal_callback_failed
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
ms.openlocfilehash: 86d6c46f338d789d6b113551ac9d99c681290526
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146776"
---
# <a name="error-remote-computer-could-not-initiate-dcom-communications"></a>Erro: o computador remoto não conseguiu iniciar a comunicação DCOM
Um erro DCOM ocorreu quando o computador remoto tentou se comunicar com o computador local. O computador local é o computador que está

 executando o Visual Studio. Esse erro pode ocorrer por várias razões:

- O computador local tem um firewall habilitado.

- A autenticação do Windows do computador remoto para o computador local não está funcionando.

### <a name="to-correct-this-error"></a>Para corrigir este erro

1. Se o computador local tiver o Firewall do Windows habilitado, consulte [depuração remota](../debugger/remote-debugging.md) para obter instruções sobre como configurar o firewall para depuração local.

2. Teste a autenticação do Windows tentando abrir um compartilhamento de arquivos no computador local do servidor remoto.

3. Para restaurar a autenticação do Windows, tente reiniciar os dois computadores. Examine os logs de eventos nos computadores local e remoto para encontrar erros de Kerberos e entre em contato com os administradores de domínio para problemas conhecidos.

## <a name="see-also"></a>Confira também
 [Depuração remota](../debugger/remote-debugging.md)

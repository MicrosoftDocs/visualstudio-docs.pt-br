---
description: Se o computador remoto não aparecer na caixa de diálogo conexões remotas, verifique as causas comuns a seguir.
title: O computador remoto não aparece em uma caixa de diálogo conexões remotas | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
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
ms.openlocfilehash: 407b33fdcc79b5ff51f34670c91bfd52ec522dac
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146763"
---
# <a name="error-remote-machine-does-not-appear-in-a-remote-connections-dialog"></a>Erro: o computador remoto não aparece em uma caixa de diálogo Conexões Remotas
Se o computador remoto não aparecer na caixa de diálogo conexões remotas, verifique as causas comuns a seguir.

 Se você estiver usando o modo de compatibilidade gerenciado, consulte a documentação do Visual Studio 2010: [solução de problemas de depuração remota-Visual Studio 2010](/previous-versions/visualstudio/visual-studio-2010/2ys11ead(v=vs.100)).

### <a name="common-causes-for-this-error"></a>Causas comuns desse erro

- O computador remoto está em execução em um computador que está em uma sub-rede diferente. Para corrigir isso, digite manualmente o nome do computador ou o endereço IP na caixa de diálogo qualificador

- O depurador remoto não está em execução no computador remoto. Para corrigir isso, inicie o depurador remoto.

- O firewall está bloqueando a comunicação entre o Visual Studio e o computador remoto. Para corrigir isso, configure o firewall para permitir que o Visual Studio e o depurador remoto (msvsmon) se comuniquem.

- O software antivírus está bloqueando a comunicação entre o Visual Studio e o computador remoto. Para corrigir isso, configure o software antivírus para permitir que o Visual Studio e o o depurador remoto (msvsmon) se comuniquem.

## <a name="see-also"></a>Confira também
- [Depuração remota](../debugger/remote-debugging.md)

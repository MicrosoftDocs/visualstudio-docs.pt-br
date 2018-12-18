---
title: 'Erro: O computador remoto não aparece em uma caixa de diálogo conexões remotas | Microsoft Docs'
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
ms.assetid: 5fd98a5b-2cf3-4438-8b0f-6f1a742a62ce
caps.latest.revision: 5
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 929072304e462e08a45a29c84ab9ce1e20043c49
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51739615"
---
# <a name="error-remote-machine-does-not-appear-in-a-remote-connections-dialog"></a>Erro: O computador remoto não aparece em uma caixa de diálogo conexões remotas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se o computador remoto não aparecer na caixa de diálogo conexões remotas, verifique as seguintes causas comuns.  
  
 Se você estiver usando o modo de compatibilidade gerenciado, verifique a documentação do Visual Studio 2010: [solução de problemas de depuração remota - Visual Studio 2010](https://msdn.microsoft.com/library/2ys11ead\(v=vs.100\).aspx) .  
  
### <a name="common-causes-for-this-error"></a>Causas comuns desse erro  
  
-   O computador remoto está em execução em um computador que está em uma sub-rede diferente. Para corrigir isso, digite manualmente o nome do computador ou endereço IP na caixa de diálogo de qualificador  
  
-   O depurador remoto não está em execução no computador remoto. Para corrigir esse problema, inicie o depurador remoto.  
  
-   O firewall está bloqueando a comunicação entre o Visual Studio e o computador remoto. Para corrigir esse problema, configure o firewall para permitir que o Visual Studio e o depurador remoto (msvsmon) para se comunicar.  
  
-   Software antivírus está bloqueando a comunicação entre o Visual Studio e o computador remoto. Para corrigir esse problema, configure o software antivírus para permitir que o Visual Studio e o depurador remoto (msvsmon) para se comunicar.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar as ferramentas remotas no dispositivo](http://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)




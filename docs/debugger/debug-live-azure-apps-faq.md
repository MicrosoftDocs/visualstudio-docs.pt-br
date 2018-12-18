---
title: Perguntas frequentes sobre depuração de instantâneos | Microsoft Docs
ms.date: 11/07/2017
ms.technology: vs-ide-debug
ms.topic: reference
helpviewer_keywords:
- debugger
ms.assetid: 944f1eb0-a74b-4d28-ae2b-a370cd869add
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 13b35746a7b0d639d4c954c8ef1a5221973e1abc
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39154340"
---
# <a name="frequently-asked-questions-for-snapshot-debugging-in-visual-studio"></a>Perguntas frequentes para instantâneo de depuração no Visual Studio

Aqui está uma lista de perguntas que podem surgir durante a depuração de aplicativos dinâmicos do Azure usando o depurador de instantâneo.

#### <a name="what-is-the-performance-cost-of-taking-a-snapshot"></a>O que é o custo de desempenho de tirar um instantâneo?

Quando o depurador de instantâneo captura um instantâneo do seu aplicativo, ele é bifurcação de processo do aplicativo e suspender a cópia bifurcada. Quando você depura um instantâneo, você está depurando em relação a cópia bifurcada do processo. Esse processo leva apenas 10 a 20 milissegundos, mas não copia o heap completas do aplicativo. Em vez disso, ele copia apenas a tabela de página e define páginas para a cópia na gravação. Se algum dos objetos do seu aplicativo sobre a alteração de heap, as respectivas páginas de, em seguida, são copiadas. Portanto, cada instantâneo tem um pequeno custo de memória (na ordem de centenas de kilobytes para a maioria dos aplicativos). 

#### <a name="what-happens-if-i-have-a-scaled-out-azure-app-service-multiple-instances-of-my-app"></a>O que acontece se eu tiver um serviço de aplicativo do Azure expandido (várias instâncias do meu aplicativo)?

Quando você tiver várias instâncias do seu aplicativo, os snappoints serão aplicadas a cada instância única. Somente o primeiro snappoint atingir com as condições especificadas cria um instantâneo. Se você tiver vários snappoints, instantâneos subsequentes são fornecidos pela mesma instância que criou o primeiro instantâneo. Logpoints enviadas para janela de saída mostrará apenas as mensagens de uma instância, enquanto logpoints enviados para os logs de aplicativo enviar mensagens de todas as instâncias. 

#### <a name="how-does-the-snapshot-debugger-load-symbols"></a>Como o depurador de instantâneo carregar símbolos?

O depurador de instantâneo requer que você tenha os símbolos correspondentes para seu aplicativo local ou implantado ao serviço de aplicativo do Azure. (PDBs inseridos no momento, não têm suporte.) O depurador de instantâneo automaticamente baixa símbolos de seu serviço de aplicativo do Azure. A partir do Visual Studio 2017 versão 15.2, implantando no serviço de aplicativo do Azure também implanta os símbolos do seu aplicativo.

#### <a name="does-the-snapshot-debugger-work-against-release-builds-of-my-application"></a>O depurador de instantâneo funciona em compilações de versão do meu aplicativo?

Sim – o depurador de instantâneo destina-se para funcionar em builds de versão. Quando um snappoint for colocado em uma função, a função é recompilada para uma versão de depuração, tornando depurável. Quando você interrompe o depurador de instantâneo, as funções são retornadas ao seu build de versão. 

#### <a name="can-logpoints-cause-side-effects-in-my-production-application"></a>Logpoints pode causar efeitos colaterais no meu aplicativo de produção?

Não - quaisquer mensagens de log que você adiciona ao seu aplicativo são avaliadas virtualmente. Eles não podem causar efeitos colaterais em seu aplicativo. No entanto, algumas propriedades nativas não podem ser acessadas com logpoints. 

#### <a name="does-the-snapshot-debugger-work-if-my-server-is-under-load"></a>O depurador de instantâneo funciona se meu servidor está sob carga?

Sim, a depuração de instantâneo pode trabalhar para servidores sob carga. O depurador de instantâneo limita e capturar instantâneos em situações em que há uma quantidade pequena de memória livre em seu servidor.

#### <a name="how-do-i-uninstall-the-snapshot-debugger"></a>Como desinstalo o depurador de instantâneo?

Você pode desinstalar a extensão de site do depurador de instantâneos no serviço de aplicativo com as seguintes etapas:

1. Desativar seu aplicativo de serviço por meio do Gerenciador de nuvem no portal do Azure ou o Visual Studio.
1. Navegue até o site do Kudu do serviço de aplicativo (ou seja, yourappservice. **SCM**. azurewebsites.net) e navegue até **extensões de Site**.
1. Clique no X na extensão de site do depurador de instantâneos para removê-lo.

## <a name="see-also"></a>Consulte também

[Depurando no Visual Studio](../debugger/index.md)  
[Depurar aplicativos ASP.NET dinâmicos usando o depurador de instantâneo](../debugger/debug-live-azure-applications.md)  
[Solução de problemas e problemas conhecidos para depuração de instantâneo](../debugger/debug-live-azure-apps-troubleshooting.md)

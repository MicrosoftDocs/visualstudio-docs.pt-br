---
title: Manter o foco ao percorrer meu aplicativo | Microsoft Docs
description: Use a depuração remota para impedir que o seu programa perca o foco quando você depurar um problema de ativação de janela.
ms.custom: SEO-VS-2020, seodec18
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.stepping
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], stepping
- focus, keeping
- stepping, focus
- windows, troubleshooting activation
ms.assetid: 11a30580-3a1a-4be8-a241-0abdc758302e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9700b5f62637cb70900845185578fbb272f5a22b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102155161"
---
# <a name="how-can-i-keep-focus-when-stepping-through-my-app"></a>Como posso manter o foco ao percorrer meu aplicativo?
## <a name="description"></a>Descrição
 Meu programa tem um problema de ativação de janela. Percorrer o programa com o depurador interfere em minha capacidade de reproduzir o problema, pois meu programa sempre perde o foco. Há alguma maneira de evitar isso?

## <a name="solution"></a>Solução
 Se você tiver um segundo computador, use a depuração remota. Você pode operar seu programa no computador remoto quando executar o depurador no host. Para obter mais informações, consulte [como: selecionar um computador remoto](/previous-versions/visualstudio/visual-studio-2010/w8wtw2f3(v=vs.100)).

## <a name="see-also"></a>Confira também
- [Perguntas frequentes sobre depuração de código nativo](../debugger/debugging-native-code-faqs.md)
- [Anexar aos processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [Depurando código nativo](../debugger/debugging-native-code.md)

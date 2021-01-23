---
title: Especificar opções de instrumentação adicionais | Microsoft Docs
description: Saiba como você pode instrumentar binários usando o IDE do Visual Studio ou usando ferramentas de linha de comando.
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.property.advanced
helpviewer_keywords:
- instrumentation, options
- profiling tools, session options
- performance sessions, options
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: aaa6a222ca320ff9e8e3d117c2218e170d67d683
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2021
ms.locfileid: "98721847"
---
# <a name="how-to-specify-additional-instrumentation-options"></a>Como especificar opções de instrumentação adicionais

Você pode instrumentar binários usando o IDE do Visual Studio ou usando ferramentas de linha de comando. Se você instrumentar um binário do IDE, será possível controlar o volume de dados coletados durante a instrumentação, especificando opções de instrumentação adicionais para a ferramenta [VSInstr](../profiling/vsinstr.md). Essas opções estão disponíveis no nível de sessão ou de destino. Por exemplo, para incluir ou excluir funções específicas durante o processo de instrumentação, use a opção adicional de instrumentação no nível de destino.

> [!IMPORTANT]
> Cada investigação que é inserida modifica ligeiramente o comportamento do programa original. Essa modificação gera sobrecarga no tempo de análise. Mesmo que uma aproximação dessa sobrecarga seja subtraída, ela ainda tem efeitos de temporização sutis em aplicativos com multithread. As opções de ferramenta [VSInstr](../profiling/vsinstr.md) ajudam a controlar a coleta de dados durante a criação de perfil.

## <a name="to-specify-additional-instrumentation-option"></a>Como especificar opções de instrumentação adicionais

1. No **Gerenciador de Desempenho**, selecione a **Sessão de Desempenho** e, em seguida, clique com o botão direito do mouse em **Propriedades**.

2. Nas **Páginas de Propriedades**, clique nas propriedades **Avançadas**.

3. Digite opções na caixa **Opções de instrumentação adicionais**.

     Por exemplo, use /CONTROL:THREAD para especificar o nível de criação de perfil. Para obter uma lista completa das opções, consulte [VSInstr](../profiling/vsinstr.md).

4. Clique em **OK**.

## <a name="see-also"></a>Confira também

[Configurar sessões](../profiling/configuring-performance-sessions.md) 
 de desempenho [Perfil da linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md)

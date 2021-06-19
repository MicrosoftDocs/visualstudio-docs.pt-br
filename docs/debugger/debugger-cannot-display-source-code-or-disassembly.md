---
title: O depurador não pode exibir o código-fonte ou a desmontagem
description: Consulte os motivos da mensagem "o depurador não pode exibir o código-fonte ou a desmontagem do local atual em que a execução foi interrompida".
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- disassembly code, errors
ms.assetid: 112d3ea3-fdd2-4bce-92b4-167a76258934
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bac2f04ab77e34186a4f0ee202fa8d16f6e45e38
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387340"
---
# <a name="debugger-cannot-display-source-code-or-disassembly"></a>O depurador não pode exibir o código-fonte ou a desmontagem
Este erro é:

 O depurador não pode exibir o código-fonte ou a desmontagem do local atual no qual a execução foi interrompida.

 Essa mensagem de erro pode ocorrer por várias razões:

- Você pode ter atingido um ponto de interrupção em um local para o qual não há o código-fonte, ao depurar uma linguagem que não oferece suporte a desmontagem. Abra a janela **pontos de interrupção** , localize o ponto de interrupção e exclua-o.

- Se você estiver depurando scripts, você pode ter atingido um ponto de interrupção enquanto não havia nenhum thread em seu programa. Escolha **Etapa** ou **Continuar** no menu **Depurar** para retomar a depuração.

- Os critérios de segurança podem ter impedido que o depurador lesse a pilha, o thread, o registro e outras informações de contexto do programa que você está depurando. É mais provável que isso ocorra se você estiver depurando um aplicativo Web e não tiver a permissão correta para acessar o diretório virtual. Defina a segurança do diretório virtual como Anônima e tente novamente.

## <a name="see-also"></a>Confira também
- [Depurando no Visual Studio](../debugger/index.yml)
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)
- [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)
---
title: Depurador não pode exibir código-fonte ou desmontagem
ms.custom: seodec18
ms.date: 11/04/2016
ms.technology: vs-ide-debug
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ea95a2bb4c29f8a23fd597173a10a838baca051c
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53063960"
---
# <a name="debugger-cannot-display-source-code-or-disassembly"></a>O depurador não pode exibir o código-fonte ou a desmontagem
Este erro é:  
  
 O depurador não pode exibir o código-fonte ou a desmontagem do local atual no qual a execução foi interrompida.  
  
 Essa mensagem de erro pode ocorrer por várias razões:  
  
-   Você pode ter atingido um ponto de interrupção em um local para o qual não há o código-fonte, ao depurar uma linguagem que não oferece suporte a desmontagem. Abra o **pontos de interrupção** , localize o ponto de interrupção e excluí-lo.  
  
-   Se você estiver depurando scripts, você pode ter atingido um ponto de interrupção enquanto não havia nenhum thread em seu programa. Escolha **Etapa** ou **Continuar** no menu **Depurar** para retomar a depuração.  
  
-   Os critérios de segurança podem ter impedido que o depurador lesse a pilha, o thread, o registro e outras informações de contexto do programa que você está depurando. É mais provável que isso ocorra se você estiver depurando um aplicativo Web e não tiver a permissão correta para acessar o diretório virtual. Defina a segurança do diretório virtual como Anônima e tente novamente.  
  
## <a name="see-also"></a>Consulte também  
 [Depuração no Visual Studio](../debugger/index.md) [tour pelos recursos do depurador](../debugger/debugger-feature-tour.md)   
 [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)
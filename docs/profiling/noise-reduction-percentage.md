---
title: Percentual de redução do ruído | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.filter
helpviewer_keywords:
- Concurrency Visualizer, Noise Reduction Percentage
ms.assetid: 1c10cd4c-2fdd-48c9-b562-a334b3b2df6c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 184a9b8e132ea1254edc7e9b88139386cc8cf36e
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31583990"
---
# <a name="noise-reduction-percentage"></a>Porcentagem de redução do ruído
Por padrão, o valor da configuração de Percentual de Redução do Ruído é 2. Somente as entradas que têm um percentual de tempo inclusivo maior ou igual a essa configuração são mostradas na árvore de chamadas. Ao alterar a configuração, é possível controlar a quantidade de entradas mostradas na árvore de chamadas. Por exemplo, alterar o valor para 10 mostrará apenas as entradas da árvore chamada que têm um tempo inclusivo maior ou igual a 10%. Ao aumentar o valor da configuração, é possível se concentrar em entradas que têm maior impacto sobre o desempenho do processo.
---
title: 'DA0004: alto uso de processador | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.performance.rules.DAHighProcessorUsage
- vs.performance.rules.DA0004
- vs.performance.DA0004
- vs.performance.4
ms.assetid: 2c4fb569-929e-4f1d-8c50-b590ee371351
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a942a26bb4cd8ccca94fd442250fe8a239cba4ed
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764038"
---
# <a name="da0004-high-processor-usage"></a>DA0004: uso do processador elevado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Id da regra | DA0004 |  
| Categoria | Uso das ferramentas de criação de perfil |  
| Métodos de criação de perfil | Amostragem de instrumentação |  
| Mensagem | O uso do processador está consistentemente acima de 75%. Considere usar o modo de amostragem para aplicativos associados à CPU. |  
| Tipo de regra | Informações |  
  
 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.  
  
## <a name="cause"></a>Causa  
 A utilização do processador (CPU) estava muito alta em dados de criação de perfil que foram coletados usando o método de instrumentação. Considere o uso do método de criação de perfil de amostragem ao criar o perfil de um aplicativo associado à CPU.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Durante essa execução de criação de perfil, os processadores estavam consistentemente muito ocupados. A alta utilização da CPU pode indicar um aplicativo associado à CPU. Geralmente, perfis instrumentados não são a maneira mais eficiente de investigar cenários de uso da CPU. Em geral, a amostragem é mais eficaz quando você está criando o perfil de aplicativos que gastam muito tempo para executar instruções no processador.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Considere uma nova criação de perfil do aplicativo usando o método de amostragem em vez do método de instrumentação, a menos que você precise de tempos de função ou esteja mais interessado em entender a entrada/saída do que os gargalos do processador.





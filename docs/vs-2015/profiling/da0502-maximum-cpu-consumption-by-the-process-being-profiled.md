---
title: 'DA0502: consumo máximo de CPU pelo processo do qual o perfil está sendo criado | Microsoft Docs'
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
- vs.performance.rules.DA0502
- vs.performance.DA0502
- vs.performance.502
ms.assetid: 1ee53df5-b0dc-4265-9d4f-527830d08725
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dd2665e9b8055812678fc1a17c0b9df0f0405e42
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51731244"
---
# <a name="da0502-maximum-cpu-consumption-by-the-process-being-profiled"></a>DA0502: consumo de CPU máximo pelo processo com perfil criado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Id da regra | DA0502 |  
| Categoria | Monitoramento de recursos |  
| Método de criação de perfil | Todos os |  
| Mensagem | Essa regra é apenas para fins informativos. O contador Processo()\\% de tempo do processador mede o consumo da CPU do processo do qual o perfil está sendo criado. O valor relatado é o máximo observado em todos os intervalos de medição. |  
| Tipo de regra | Informação |  
  
 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Essa mensagem relata o percentual máximo de tempo que um processador esteve ocupado executando instruções do aplicativo. O valor relatado é o valor máximo relatado entre todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo. O percentual pode ser maior que 100% em um computador com mais de um processador.  
  
## <a name="how-to-use-the-rule-data"></a>Como usar os dados de regra  
 Use o valor da regra para comparar o desempenho de diferentes versões ou compilações do programa ou para entender o desempenho do aplicativo em diferentes cenários de criação de perfil.




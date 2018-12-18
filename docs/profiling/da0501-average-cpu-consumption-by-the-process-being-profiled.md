---
title: 'DA0501: consumo de CPU médio pelo processo com perfil criado. | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DA0501
- vs.performance.DA0501
- vs.performance.501
ms.assetid: b01946b4-75e3-47d5-a1a1-cebfae66a3af
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f9612c895f7453d250b4f37c06e3630901602685
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49847104"
---
# <a name="da0501-average-cpu-consumption-by-the-process-being-profiled"></a>DA0501: consumo médio da CPU pelo processo que está sendo analisado.

|||  
|-|-|  
|ID de regra|DA501|  
|Categoria|Monitoramento de recursos|  
|Método de criação de perfil|Todos|  
|Mensagem|Consumo médio de CPU pelo Processo cujo perfil está sendo criado.|  
|Tipo de regra|Informações|  

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.  

## <a name="rule-description"></a>Descrição da regra  
 Essa mensagem relata o percentual de tempo que um processador esteve ocupado executando instruções do aplicativo. O valor relatado é a média de todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo. O valor do valor pode ser maior que 100% em um computador com mais de um processador.  

## <a name="how-to-use-rule-data"></a>Como usar dados de regra  
 Use o valor da regra para comparar o desempenho de diferentes versões ou compilações do programa ou para entender o desempenho do aplicativo em diferentes cenários de teste.
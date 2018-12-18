---
title: 'DA0503: conjunto de trabalho médio em bytes para o processo do qual o perfil está sendo criado | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.503
- vs.performance.DA0503
- vs.performance.rules.DA0503
ms.assetid: 9047a494-eaaf-4679-b422-c64e8bde77a4
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8b56588d829f482273fd1ab74d2ab2df70abea6e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49836314"
---
# <a name="da0503-average-working-set-in-bytes-for-the-process-being-profiled"></a>DA0503: conjunto de trabalho médio em bytes para o processo que está sendo analisado

|||  
|-|-|  
|ID de regra|DA0503|  
|Categoria|Monitoramento de recursos|  
|Método de criação de perfil|Todos|  
|Mensagem|Essas informações foram coletadas apenas para fins informativos. O contador Conjunto de trabalho do processo mede o uso de memória física do processo do qual está sendo criado o perfil. O valor relatado é a média calculada de todos os intervalos de medição.|  
|Tipo de regra|Informações|  

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.  

## <a name="rule-description"></a>Descrição da regra  
 Essa mensagem relata a quantidade média de memória física que o processo está usando em bytes (o conjunto de trabalho). O conjunto de trabalho do processo representa páginas do espaço de endereço do processo que atualmente residem na memória física.  

 O valor relatado inclui páginas residentes de segmentos de memória compartilhada referenciados pelo processo. DLLs compartilhadas que o processo referencia estão incluídas nos segmentos de memória compartilhada contados. O valor do conjunto de trabalho do processo pode ser maior que a quantidade de memória virtual que o processo alocou devido a segmentos de memória compartilhada.  

 O valor relatado é a média de todos os intervalos de medição em que o processo do qual o perfil está sendo criado estava ativo.  

 O tamanho do conjunto de trabalho do processo reflete a quantidade de memória virtual que o processo está usando de forma ativa. Ele também é afetado pela quantidade de memória física (ou RAM) disponível para executar o aplicativo e a contenção para a memória física de outros processos em execução. Se a memória física for restrita, o valor do conjunto de trabalho do processo estará apto a variar de forma considerável, conforme o sistema operacional tenta equilibrar o uso de memória entre os processos ativos cortando periodicamente as páginas razoavelmente inativas dos conjuntos de trabalho do processo.  

 Para obter mais informações sobre conjuntos de trabalho do processo, consulte [Conjunto de trabalho](http://go.microsoft.com/fwlink/?LinkId=177830) na documentação do Gerenciamento de memória do Windows do MSDN.  

## <a name="how-to-use-rule-data"></a>Como usar dados de regra  
 Use o valor da regra para comparar o desempenho de diferentes versões ou compilações do programa ou para entender o desempenho do aplicativo em diferentes cenários de criação de perfil.  

 Clique duas vezes na mensagem da janela Lista de Erros para navegar para a [Exibição de Marcas](../profiling/marks-view.md) dos dados de criação de perfil. Encontre as colunas **Processo\Conjunto de trabalho** e **Memória\Páginas/s**. Compare as duas colunas e determine se há fases específicas da execução do programa que parecem estar associadas a um aumento da atividade de E/S de paginação.
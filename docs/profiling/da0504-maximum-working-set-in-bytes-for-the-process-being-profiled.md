---
title: 'DA0504: conjunto de trabalho máximo em bytes para o processo do qual o perfil está sendo criado | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.DA0504
- vs.performance.504
- vs.performance.rules.DA0504
ms.assetid: 36e71603-ece7-4000-85fc-9da4eed61bf2
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 47b0c4494a4689983ed4fee62312d5085a31aa97
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49864693"
---
# <a name="da0504-maximum-working-set-in-bytes-for-the-process-being-profiled"></a>DA0504: conjunto de trabalho máximo em bytes para o processo com criação de perfil

|||  
|-|-|  
|ID de regra|DA0504|  
|Categoria|Gerenciamento de recursos|  
|Método de criação de perfil|Todos|  
|Mensagem|Essas informações foram coletadas apenas para fins informativos. O contador Conjunto de trabalho do processo mede o uso de memória física do processo do qual está sendo criado o perfil. O valor relatado é o máximo observado em todos os intervalos de medição.|  
|Tipo de regra|Informações|  

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.  

## <a name="rule-description"></a>Descrição da regra  
 Essa mensagem relata a quantidade máxima de memória física, em bytes, que o processo está usando. O conjunto de trabalho do processo representa páginas do espaço de endereço do processo que atualmente residem na memória física. Essa regra relata o valor máximo do conjunto de trabalho do processo enquanto a criação de perfil estava ativa.  

 O valor relatado inclui páginas residentes de segmentos de memória compartilhada referenciados pelo processo. DLLs compartilhadas que o processo referencia estão incluídas nos segmentos de memória compartilhada contados. O valor do Conjunto de Trabalho do processo pode ser maior que a quantidade de memória virtual que o processo alocou devido a segmentos de memória compartilhada.  

 O tamanho do conjunto de trabalho do processo reflete a quantidade de memória virtual que o processo está usando de forma ativa. Ele também é afetado pela quantidade de memória física (ou RAM) disponível para executar o aplicativo e a contenção para a memória física de outros processos em execução. Para obter mais informações sobre conjuntos de trabalho do processo, consulte [Conjunto de trabalho](http://go.microsoft.com/fwlink/?LinkId=177830) na documentação do Gerenciamento de memória do Windows do MSDN.  

## <a name="how-to-use-rule-data"></a>Como usar dados de regra  
 A regra coleta esses dados de medição do recurso de monitoramento de desempenho do Windows e o relata apenas para fins informativos. Use-a para comparar o desempenho de diferentes versões ou compilações do programa ou para entender o desempenho do aplicativo em diferentes cenários de teste.  

 Clique duas vezes na mensagem da janela Lista de Erros para navegar para a [Exibição de Marcas](../profiling/marks-view.md) dos dados de criação de perfil. Encontre as colunas dos contadores **Processo\Conjunto de trabalho** e **Memória\Páginas/s**. Em seguida, localize o valor máximo do **Processo\Conjunto de Trabalho** e compare-o com o valor de **Memória\Páginas/s**. Com frequência, o máximo do conjunto de trabalho é associado a um intervalo em que há atividade de E/S de paginação reduzida, especialmente se o computador tiver restrição de memória.
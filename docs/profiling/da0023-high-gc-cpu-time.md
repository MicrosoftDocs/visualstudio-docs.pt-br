---
title: 'DA0023: alto tempo de CPU no GC | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.DA0023
- vs.performance.23
- vs.performance.rules.DA0023
ms.assetid: aba875fe-9cbc-418d-a2c4-6eb47519a5bb
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7d13f1c0bc2a024d35611d81f4aba3694f3bc39e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49836255"
---
# <a name="da0023-high-gc-cpu-time"></a>DA0023: tempo de CPU GC alto

|||  
|-|-|  
|ID de regra|DA0023|  
|Categoria|Uso do .NET Framework|  
|Método de criação de perfil|Todos|  
|Mensagem|O % de tempo no GC é bem alto. Essa indicação de quantidade excessiva de sobrecarga de coleta de lixo pode estar afetando a capacidade de resposta do aplicativo. Você pode coletar dados de alocação de memória do .NET e informações de tempo de vida do objeto para entender o padrão de alocação de memória usado melhor pelo aplicativo.|  
|Tipo de regra|Informativo|  

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.  

## <a name="cause"></a>Causa  
 Os dados de desempenho do sistema coletados durante a criação de perfil indicam que a quantidade de tempo gasto na coleta de lixo é significativa em comparação com o tempo total de processamento do aplicativo.  

## <a name="rule-description"></a>Descrição da regra  
 O CLR (Common Language Runtime) do Microsoft .NET fornece um mecanismo de gerenciamento automático de memória que usa um coletor de lixo para recuperar a memória de objetos que não são mais usados pelo aplicativo. O coletor de lixo é orientado a geração, com base na suposição de que muitas alocações são de curta duração. Variáveis locais, por exemplo, devem ser de curta duração. Os objetos recém-criados iniciam na geração 0 (ger 0), em seguida, progridem para a geração 1 quando sobrevivem a uma execução da coleta de lixo e, por fim, fazem a transição para a geração 2 se ainda são usados pelo aplicativo.  

 Os objetos na geração 0 são coletados com frequência e de forma eficiente. Objetos na geração 1 são coletados com menos frequência e de forma menos eficiente. Por fim, objetos de longa duração na geração 2 devem ser coletados com uma frequência ainda menor. A coleta da geração 2, que é uma execução de coleta de lixo completa, também é a operação mais cara.  

 Essa regra é acionada quando o tempo gasto na coleta de lixo é significativo em comparação com o tempo total de processamento do aplicativo.  

> [!NOTE]
>  Quando a proporção de tempo gasto na coleta de lixo é excessivo em comparação com o tempo total de processamento do aplicativo, o aviso [DA0024: excesso de tempo de CPU no GC](../profiling/da0024-excessive-gc-cpu-time.md) é acionado em vez dessa regra.  

## <a name="how-to-investigate-a-warning"></a>Como investigar um aviso  
 Clique duas vezes na mensagem da janela Lista de Erros para navegar para a [Exibição de Marcas](../profiling/marks-view.md) dos dados de criação de perfil. Encontre a coluna **Memória do .NET CLR\\% de tempo no GC**. Determine se há fases específicas da execução do programa em que a sobrecarga da coleta de lixo de memória gerenciada é mais pesada do que em outras fases. Compare os valores do valor de % de tempo no GC com a taxa de coleta de lixo relatada nos valores **Nº de coletas da Ger 0**, **Nº de coletas da Ger 1** e **Nº de coletas da Ger 2**.  

 O valor de % de tempo no GC tenta relatar o tempo que um aplicativo gasta executando a coleta de lixo proporcional à quantidade total de processamento. Lembre-se de que há circunstâncias em que o valor de % de Tempo Gasto em GC pode relatar um valor alto, mas não devido a um excesso de coleta de lixo. Para obter mais informações sobre a maneira como o valor de % de tempo no GC é calculado, consulte a entrada [Difference Between Perf Data Reported by Different Tools – 4](http://go.microsoft.com/fwlink/?LinkId=177863) (Diferença entre dados de desempenho relatados por ferramentas diferentes – 4) do **Weblog do Maoni** no MSDN. Se ocorrerem falhas de página ou o aplicativo for impedido por outro trabalho de prioridade mais alta no computador durante a coleta de lixo, o contador % de tempo no GC refletirá esses atrasos adicionais.
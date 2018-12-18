---
title: 'DA0022: alta taxa de coletas de lixo da Ger 2 | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.DA0022
- vs.performance.rules.DA0022
- vs.performance.22
ms.assetid: f871a547-0e6f-4b11-b2d7-174d30fc2ed8
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3f310a099deb1106baa375996f50919e2ab1814c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49861638"
---
# <a name="da0022-high-rate-of-gen-2-garbage-collections"></a>DA0022: taxa alta de coletas de lixo Gen 2

|||  
|-|-|  
|ID de regra|DA0022|  
|Categoria|Uso do .NET Framework|  
|Método de criação de perfil|Todos|  
|Mensagem|Há uma taxa bem alta de coletas de lixo da Ger 2 ocorrendo. Se, por design, a maioria das estruturas de dados do programa for alocada e persistida por um longo tempo, normalmente, isso não será um problema. No entanto, se esse comportamento não for intencional, o aplicativo poderá estar fixando objetos. Se não tiver certeza, você poderá coletar dados de alocação de memória do .NET e informações de tempo de vida do objeto para entender o padrão de alocação de memória usado pelo aplicativo.|  
|Tipo de regra|Aviso|  

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.  

## <a name="cause"></a>Causa  
 Dados de desempenho do sistema que foram coletados durante a criação de perfil indicam que uma proporção significativa da memória dos objetos do .NET Framework foi recuperada na geração 2 de coleta de lixo em comparação com as coletas de lixo das gerações 0 e 1.  

## <a name="rule-description"></a>Descrição da regra  
 O CLR (Common Language Runtime) do Microsoft .NET fornece um mecanismo de gerenciamento automático de memória que usa um coletor de lixo para recuperar a memória de objetos que não são mais usados pelo aplicativo. O coletor de lixo é orientado a geração, com base na suposição de que muitas alocações são de curta duração. Variáveis locais, por exemplo, devem ser de curta duração. Os objetos recém-criados iniciam na geração 0 (ger 0), em seguida, progridem para a geração 1 quando sobrevivem a uma execução da coleta de lixo e, por fim, fazem a transição para a geração 2 se ainda são usados pelo aplicativo.  

 Objetos na geração 0 são coletados com frequência e, em geral, de forma muito eficiente. Objetos na geração 1 são coletados com menos frequência e de forma menos eficiente. Por fim, objetos de longa duração na geração 2 devem ser coletados com uma frequência ainda menor. A coleta da geração 2, que é uma execução de coleta de lixo completa, também é a operação mais cara.  

 Essa regra é acionada quando ocorre, proporcionalmente, um excesso de coletas de lixo da geração 2. Aplicativos do .NET Framework com bom funcionamento terão mais de 5 vezes mais coletas de lixo da geração 1 do que coletas de lixo da geração 2. (Provavelmente, um fator de 10x é ideal).  

## <a name="how-to-investigate-a-warning"></a>Como investigar um aviso  
 Clique duas vezes na mensagem da janela Lista de Erros para navegar para a [Exibição de Marcas](../profiling/marks-view.md) dos dados de criação de perfil. Encontre as colunas **Memória do .NET CLR\\Nº de coletas da Ger 0** e **Memória do .NET CLR\\Nº de coletas da Ger 1**. Determine se há fases específicas da execução do programa em que a coleta de lixo ocorre com mais frequência. Compare esses valores com a coluna **% de tempo no GC** para ver se o padrão de alocações de memória gerenciada está causando um excesso de sobrecarga de gerenciamento de memória.  

 Uma grande proporção de coletas de lixo da Geração 2 não é sempre um problema. Pode ser por design. Um aplicativo que aloca grandes estruturas de dados que devem permanecer ativas por longos períodos durante a execução pode disparar essa regra. Quando um aplicativo desse tipo estiver sob demanda de memória, ele poderá ser forçado a executar coletas de lixo frequentes. Se as coletas de lixo das gerações 0 e 1 mais baratas puderem recuperar apenas uma quantidade pequena de memória gerenciada, coletas de lixo da Geração 2 mais frequentes serão agendadas.  

 Há colunas de Memória do .NET CLR adicionais na Exibição de Marcas que podem ajudá-lo a identificar problemas de coleta de lixo. A coluna **% de tempo no GC** ajuda você a entender a quantidade de sobrecarga de gerenciamento de memória que está ocorrendo. Se seu aplicativo normalmente usar um número relativamente pequeno de objetos grandes mas persistentes, coletas frequentes da Geração 2 não deverão consumir quantidades excessivas de tempo da CPU. Se o aplicativo estiver sob demanda de memória porque uma quantidade maior de Memória Física (RAM) é necessária, regras relacionadas que avaliam os valores da coluna **Memória\Páginas/s** também poderão ser acionadas.  

 Para entender o padrão de uso de memória gerenciada do aplicativo, crie seu perfil novamente executando um perfil de alocação de Memória do .NET e selecione a opção de criação de perfil Tempo de Vida do Objeto.  

 Para obter informações sobre como melhorar o desempenho da coleta de lixo, consulte [Garbage Collector Basics and Performance Hints](http://go.microsoft.com/fwlink/?LinkId=148226) (Noções básicas sobre o coletor de lixo e dicas de desempenho) no site da Microsoft. Para obter informações sobre a sobrecarga de coleta de lixo automática, consulte [O que há por trás do heap de objetos grandes](http://go.microsoft.com/fwlink/?LinkId=177836).
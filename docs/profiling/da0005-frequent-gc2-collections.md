---
title: 'DA0005: coleções de GC2 frequentes | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.DA0005
- vs.performance.rules.DAManyGC2Collections
- vs.performance.5
- vs.performance.rules.DA0005
ms.assetid: 8d3f267c-8a74-4cf4-91a5-0b06a76dc2bd
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a5e3038f873895e38cf162e67316bc08f2fc007b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49849366"
---
# <a name="da0005-frequent-gc2-collections"></a>DA0005: coleções de GC2 frequentes

|||  
|-|-|  
|RuleId|DA0005|  
|Categoria|Uso do .NET Framework|  
|Método de criação de perfil|Memória do .NET|  
|Mensagem|Muitos dos seus objetos estão sendo coletados na coleta de lixo de geração 2.|  
|Tipo de mensagem|Aviso|  

## <a name="cause"></a>Causa  
 Um número alto de objetos de memória do .NET está sendo recuperado na coleta de lixo de geração 2.  

## <a name="rule-description"></a>Descrição da regra  
 O CLR (Common Language Runtime) do Microsoft .NET fornece um mecanismo de gerenciamento automático de memória que usa um coletor de lixo para recuperar a memória de objetos que não são mais usados pelo aplicativo. O coletor de lixo é orientado a geração, com base na suposição de que muitas alocações são de curta duração. Variáveis locais, por exemplo, devem ser de curta duração. Os objetos recém-criados iniciam na geração 0 (ger 0), em seguida, progridem para a geração 1 quando sobrevivem a uma execução da coleta de lixo e, por fim, fazem a transição para a geração 2 se ainda são usados pelo aplicativo.  

 Objetos na geração 0 são coletados com frequência e, em geral, de forma muito eficiente. Objetos na geração 1 são coletados com menos frequência e de forma menos eficiente. Por fim, objetos de longa duração na geração 2 devem ser coletados com uma frequência ainda menor. A coleta da geração 2, que é uma execução de coleta de lixo completa, também é a operação mais cara.  

 Essa regra é acionada quando ocorre, proporcionalmente, um excesso de coletas de lixo da geração 2. Se um excesso de objetos de duração relativamente curta sobreviverem à coleta da geração 1, mas conseguirem ser coletados em uma coleta completa da geração 2, o custo de gerenciamento de memória poderá se tornar excessivo. Para obter mais informações, consulte a postagem [Mid-life crisis](http://go.microsoft.com/fwlink/?LinkId=177835) (Crise de meia vida útil) em Performance Tidbits (Notícias sobre desempenho) de Rico Mariani no site do MSDN.  

## <a name="how-to-investigate-a-warning"></a>Como investigar um aviso  
 Examine os relatórios [Exibições de dados da memória do .NET](../profiling/dotnet-memory-data-views.md) para entender o padrão de alocação de memória do aplicativo. Use a [Exibição de Tempo de Vida do Objeto](../profiling/object-lifetime-view.md) para determinar quais objetos de dados do programa estão sobrevivendo na geração 2 e, em seguida, sendo recuperados dela. Use a [Exibição de Alocações](../profiling/dotnet-memory-allocations-view.md) para determinar o caminho de execução que resultou nessas alocações.  

 Para obter informações sobre como melhorar o desempenho da coleta de lixo, consulte [Garbage Collector Basics and Performance Hints](http://go.microsoft.com/fwlink/?LinkId=148226) (Noções básicas sobre o coletor de lixo e dicas de desempenho) no site da Microsoft. Para obter informações sobre a sobrecarga de coleta de lixo automática, consulte [O que há por trás do heap de objetos grandes](http://go.microsoft.com/fwlink/?LinkId=177836).
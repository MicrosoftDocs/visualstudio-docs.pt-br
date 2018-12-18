---
title: 'DA0005: coleções de GC2 frequentes | Microsoft Docs'
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
- vs.performance.DA0005
- vs.performance.rules.DAManyGC2Collections
- vs.performance.5
- vs.performance.rules.DA0005
ms.assetid: 8d3f267c-8a74-4cf4-91a5-0b06a76dc2bd
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 80b3f769a151974559f70d247696fd7abb794731
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745776"
---
# <a name="da0005-frequent-gc2-collections"></a>DA0005: coleções de GC2 frequentes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ID da regra | DA0005 |  
| Categoria de |. Uso do .NET Framework |  
| Método de criação de perfil |. Memória do .NET |  
| Mensagem | Muitos dos seus objetos estão sendo coletados na coleta de lixo de geração 2. |  
| Tipo de mensagem | Aviso |  
  
## <a name="cause"></a>Causa  
 Um número alto de objetos de memória do .NET está sendo recuperado na coleta de lixo de geração 2.  
  
## <a name="rule-description"></a>Descrição da Regra  
 O CLR (Common Language Runtime) do Microsoft .NET fornece um mecanismo de gerenciamento automático de memória que usa um coletor de lixo para recuperar a memória de objetos que não são mais usados pelo aplicativo. O coletor de lixo é orientado a geração, com base na suposição de que muitas alocações são de curta duração. Variáveis locais, por exemplo, devem ser de curta duração. Os objetos recém-criados iniciam na geração 0 (ger 0), em seguida, progridem para a geração 1 quando sobrevivem a uma execução da coleta de lixo e, por fim, fazem a transição para a geração 2 se ainda são usados pelo aplicativo.  
  
 Objetos na geração 0 são coletados com frequência e, em geral, de forma muito eficiente. Objetos na geração 1 são coletados com menos frequência e de forma menos eficiente. Por fim, objetos de longa duração na geração 2 devem ser coletados com uma frequência ainda menor. A coleta da geração 2, que é uma execução de coleta de lixo completa, também é a operação mais cara.  
  
 Essa regra é acionada quando ocorre, proporcionalmente, um excesso de coletas de lixo da geração 2. Se um excesso de objetos de duração relativamente curta sobreviverem à coleta da geração 1, mas conseguirem ser coletados em uma coleta completa da geração 2, o custo de gerenciamento de memória poderá se tornar excessivo. Para obter mais informações, consulte a postagem [Mid-life crisis](http://go.microsoft.com/fwlink/?LinkId=177835) (Crise de meia vida útil) em Performance Tidbits (Notícias sobre desempenho) de Rico Mariani no site do MSDN.  
  
## <a name="how-to-investigate-a-warning"></a>Como investigar um aviso  
 Examine os relatórios de [Exibições de dados da memória do .NET](../profiling/dotnet-memory-data-views.md) para entender o padrão do aplicativo de alocação de memória. Use a [Exibição de Tempo de Vida do Objeto](../profiling/object-lifetime-view.md) para determinar quais objetos de dados do programa estão sobrevivendo na geração 2 e, em seguida, sendo recuperados dela. Use a [Exibição de Alocações](../profiling/dotnet-memory-allocations-view.md) para determinar o caminho de execução que resultou nessas alocações.  
  
 Para obter informações sobre como melhorar o desempenho da coleta de lixo, consulte [Garbage Collector Basics and Performance Hints](http://go.microsoft.com/fwlink/?LinkId=148226) (Noções básicas sobre o coletor de lixo e dicas de desempenho) no site da Microsoft. Para obter informações sobre a sobrecarga de coleta de lixo automática, consulte [O que há por trás do heap de objetos grandes](http://go.microsoft.com/fwlink/?LinkId=177836).




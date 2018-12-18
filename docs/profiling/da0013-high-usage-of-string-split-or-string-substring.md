---
title: 'DA0013: alto uso de String.Split ou String.Substring | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.13
- vs.performance.rules.DAAvoidStringSubstr
- vs.performance.DA0013
- vs.performance.rules.DA0013
helpviewer_keywords:
- vs.performance.13
- vs.performance.rules.DA0013
ms.assetid: f501f423-bef9-4e08-bf96-c9ac9957e5a2
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 722277e65a30d8c40cc245123120650108ebc560
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49831452"
---
# <a name="da0013-high-usage-of-stringsplit-or-stringsubstring"></a>DA0013: uso alto de String.Split ou String.Substring

|||  
|-|-|  
|ID de regra|DA0013|  
|Categoria|Diretrizes de uso do .NET Framework|  
|Métodos de criação de perfil|Amostragem|  
|Mensagem|Considere a possibilidade de reduzir o uso das funções String.Split e String.Substring.|  
|Tipo de regra|Aviso|  

## <a name="cause"></a>Causa  
 Chamadas aos métodos System.String.Split ou System.String.Substring são uma proporção significativa dos dados de criação de perfil. Considere o uso de System.String.IndexOf ou System.String.IndexOfAny se estiver testando a existência de uma subcadeia de caracteres em uma cadeia de caracteres.  

## <a name="rule-description"></a>Descrição da regra  
 O método Split opera em um objeto String e retorna uma nova matriz de Strings que contém as subcadeias da original. A função aloca memória ao objeto de matriz retornado e aloca um novo objeto String a cada elemento de matriz encontrado. Da mesma forma, o método Substr funciona em um objeto String e retorna uma nova String equivalente à subcadeia de caracteres solicitada.  

 Se o gerenciamento de alocações de memória for crítico para seu aplicativo, considere o uso de alternativas aos métodos String.Split e String.Substr. Por exemplo, é possível usar o método IndexOf ou IndexOfAny para localizar uma subcadeia de caracteres específica em uma String de caracteres sem criar uma nova instância da classe String.  

## <a name="how-to-investigate-a-warning"></a>Como investigar um aviso  
 Clique duas vezes na mensagem na janela **Lista de Erros** para navegar até a [Exibição de Detalhes da Função](../profiling/function-details-view.md) dos dados de perfil de amostragem. Examine as funções de chamada para encontrar as seções do programa que fazem o uso mais frequente dos métodos System.String.Split ou System.String.Substr. Se possível, use o método IndexOf ou IndexOfAny para localizar uma subcadeia de caracteres específica em uma String de caracteres sem criar uma nova instância da classe String.
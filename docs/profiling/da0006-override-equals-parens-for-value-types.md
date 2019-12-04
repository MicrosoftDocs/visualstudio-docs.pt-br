---
title: 'DA0006: substituir Equals() para tipos de valor | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DAOverrideEquals
- vs.performance.6
- vs.performance.DA0006
- vs.performance.rules.DA0006
ms.assetid: 4d85bdd6-b571-47e0-afd6-ba3764e4eed5
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 9e097d6d8c9a7b82fac53fd37951644eb7eb5e59
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779526"
---
# <a name="da0006-override-equals-for-value-types"></a>DA0006: substituir Equals() para tipos de valor

|||
|-|-|
|Id da Regra|DA0006|
|Categoria|Uso do .NET Framework|
|Métodos de Criação de Perfil|Amostragem|
|Mensagem|Substituir Equals e operador de igualdade em tipos de valor.|
|Tipo de mensagens|Aviso|

## <a name="cause"></a>Causa
 Chamadas para o método Equals ou os operadores de igualdade de um tipo de valor público são uma parte significativa dos dados de criação de perfil. Considere a implementação de um método mais eficiente.

## <a name="rule-description"></a>Descrição da regra
 Para tipos de valor, a implementação herdada de Equals usa a biblioteca <xref:System.Reflection> e compara o conteúdo de todos os campos do tipo. Reflection é computacionalmente cara, e pode ser desnecessário comparar a igualdade de cada campo. Se você espera que os usuários comparem ou classifiquem instâncias ou as usem como chaves de tabela de hash, o tipo de valor deverá implementar Equals. Se a linguagem de programação der suporte à sobrecarga de operador, também é necessário fornecer uma implementação dos operadores de igualdade e desigualdade.

 Para obter mais informações sobre como substituir Equals e os operadores de igualdade, consulte [Diretrizes para Implementação de Equals e o Operador de Igualdade (= =)](/dotnet/standard/design-guidelines/equality-operators).

## <a name="how-to-investigate-a-warning"></a>Como investigar um aviso
 Para obter um exemplo de implementação de Equals e operadores de igualdade, consulte a regra de análise de código [CA1815: substituir Equals e operador Equals em tipos de valor](../code-quality/ca1815.md)

---
title: 'CA2226: os operadores devem ter sobrecargas simétricas | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OperatorsShouldHaveSymmetricalOverloads
- CA2226
helpviewer_keywords:
- OperatorsShouldHaveSymmetricalOverloads
- CA2226
ms.assetid: d202401a-ea14-4559-b15e-0ea4f5b68789
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 430a8d3cfd3b8ced45b60bd9dc70211711886d43
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540563"
---
# <a name="ca2226-operators-should-have-symmetrical-overloads"></a>CA2226: Operadores devem ter sobrecargas simétricas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|OperatorsShouldHaveSymmetricalOverloads|
|CheckId|CA2226|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo implementa o operador de igualdade ou de desigualdade e não implementa o operador oposto.

## <a name="rule-description"></a>Descrição da Regra
 Não há nenhuma circunstância em que igualdade ou desigualdade seja aplicável a instâncias de um tipo, e o operador oposto é indefinido. Normalmente, os tipos implementam o operador de desigualdade retornando o valor negado do operador de igualdade.

 O compilador C# emite um erro para violações dessa regra.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente os operadores de igualdade e desigualdade ou remova aquele que está presente.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. Seu tipo não funcionará de maneira consistente com o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] .

## <a name="related-rules"></a>Regras relacionadas
 [CA1046: Não sobrecarregar o operador equals em tipos de referência](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2225: Sobrecargas de operador têm alternativas nomeadas](../code-quality/ca2225-operator-overloads-have-named-alternates.md)

 [CA2224: Substituir equals ao sobrecarregar operador equals](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2218: Substituir GetHashCode ao substituir Equals](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

 [CA2231: Sobrecarregar operador equals ao substituir ValueType.Equals](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)

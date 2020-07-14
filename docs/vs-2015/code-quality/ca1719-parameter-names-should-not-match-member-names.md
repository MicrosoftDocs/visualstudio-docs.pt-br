---
title: 'CA1719: nomes de parâmetros não devem corresponder a nomes de membro | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ParameterNamesShouldNotMatchMemberNames
- CA1719
helpviewer_keywords:
- CA1719
- ParameterNamesShouldNotMatchMemberNames
ms.assetid: c6fea690-1659-4ee7-a1c5-125ad6754525
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5024d2ddb7f31593c8eaedfc2fb421b4a0e9b0a4
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545360"
---
# <a name="ca1719-parameter-names-should-not-match-member-names"></a>CA1719: Nomes de parâmetros não devem corresponder a nomes de membros
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ParameterNamesShouldNotMatchMemberNames|
|CheckId|CA1719|
|Categoria|Microsoft. Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O nome de um membro visível externamente corresponde a, em uma comparação que não diferencia maiúsculas de minúsculas, o nome de um de seus parâmetros.

## <a name="rule-description"></a>Descrição da Regra
 Um nome de parâmetro deve informar o significado de um parâmetro e um nome de membro deve informar o significado de um membro. Seria um design raro se eles fossem iguais. A nomenclatura de um parâmetro com o mesmo nome do membro não é intuitiva e dificulta o uso da biblioteca.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Selecione um nome de parâmetro que não corresponda ao nome do membro.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Para o novo desenvolvimento, nenhum cenário conhecido ocorre onde você deve suprimir um aviso dessa regra. Para as bibliotecas de envio, talvez seja necessário suprimir um aviso dessa regra.

## <a name="related-rules"></a>Regras relacionadas
 [CA1709: Identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708: Identificadores devem ser diferentes em algo além das maiúsculas e minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

 [CA1707: Identificadores não devem conter sublinhados](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)

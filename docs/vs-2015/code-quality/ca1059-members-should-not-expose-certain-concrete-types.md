---
title: 'CA1059: os membros não devem expor determinados tipos concretos | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1059
- MembersShouldNotExposeCertainConcreteTypes
helpviewer_keywords:
- MembersShouldNotExposeCertainConcreteTypes
- CA1059
ms.assetid: 59f61f52-8d6c-49cb-aefb-191910523a3c
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 792426615dd78241ade1d38a24ec1f4d5702cede
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545373"
---
# <a name="ca1059-members-should-not-expose-certain-concrete-types"></a>CA1059: Membros não devem expor determinados tipos concretos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|MembersShouldNotExposeCertainConcreteTypes|
|CheckId|CA1059|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um membro visível externamente é um determinado tipo concreto ou expõe determinados tipos concretos por meio de um de seus parâmetros ou valor de retorno. Atualmente, essa regra relata a exposição dos seguintes tipos concretos:

- Um tipo derivado de <xref:System.Xml.XmlNode?displayProperty=fullName> .

## <a name="rule-description"></a>Descrição da Regra
 Um tipo concreto é um tipo que tem uma implementação completa e, por isso, uma instância pode ser criada. Para permitir o uso generalizado do membro, substitua o tipo concreto pela interface sugerida. Isso permite que o membro aceite qualquer tipo que implemente a interface ou seja usado onde um tipo que implementa a interface é esperado.

 A tabela a seguir lista os tipos concretos direcionados e suas substituições sugeridas.

|Tipo concreto|Substituição|
|-------------------|-----------------|
|<xref:System.Xml.XPath.XPathDocument>|<xref:System.Xml.XPath.IXPathNavigable?displayProperty=fullName>.<br /><br /> O uso da interface dissocia o membro de uma implementação específica de uma fonte de dados XML.|

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o tipo concreto para a interface sugerida.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir uma mensagem dessa regra se a funcionalidade específica fornecida pelo tipo concreto for necessária.

## <a name="related-rules"></a>Regras relacionadas
 [CA1011: Considerar a passagem de tipos base como parâmetros](../code-quality/ca1011-consider-passing-base-types-as-parameters.md)

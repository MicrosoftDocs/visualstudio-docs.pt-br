---
title: 'CA1059: Membros não devem expor determinados tipos concretos'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- CA1059
- MembersShouldNotExposeCertainConcreteTypes
helpviewer_keywords:
- MembersShouldNotExposeCertainConcreteTypes
- CA1059
ms.assetid: 59f61f52-8d6c-49cb-aefb-191910523a3c
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0462317ff273b2cb7a967c7e093b16a695e547e2
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53825273"
---
# <a name="ca1059-members-should-not-expose-certain-concrete-types"></a>CA1059: Membros não devem expor determinados tipos concretos

|||
|-|-|
|NomeDoTipo|MembersShouldNotExposeCertainConcreteTypes|
|CheckId|CA1059|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um membro visível externamente é um determinado tipo concreto ou expõe determinados tipos concretos por meio de um de seus parâmetros ou valor de retorno. No momento, esta regra relata a exposição dos tipos concretos a seguir:

- Um tipo derivado de <xref:System.Xml.XmlNode?displayProperty=fullName>.

## <a name="rule-description"></a>Descrição da regra
 Um tipo concreto é um tipo que tem uma implementação completa e, por isso, uma instância pode ser criada. Para permitir o uso difundido do membro, substitua o tipo concreto a interface sugerida. Isso permite que o membro aceitar qualquer tipo que implementa a interface ou ser usado onde um tipo que implementa a interface é esperado.

 A tabela a seguir lista os tipos de concretos de destino e suas substituições sugeridas.

|Tipo concreto|Substituição|
|-------------------|-----------------|
|<xref:System.Xml.XPath.XPathDocument>|<xref:System.Xml.XPath.IXPathNavigable?displayProperty=fullName>.<br /><br /> Usando a interface separa o membro de uma implementação específica de uma fonte de dados XML.|

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, altere o tipo concreto para a interface sugerida.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir uma mensagem da regra se a funcionalidade específica fornecida pelo tipo concreto é necessária.

## <a name="related-rules"></a>Regras relacionadas
 [CA1011: Considerar passar tipos base como parâmetros](../code-quality/ca1011-consider-passing-base-types-as-parameters.md)
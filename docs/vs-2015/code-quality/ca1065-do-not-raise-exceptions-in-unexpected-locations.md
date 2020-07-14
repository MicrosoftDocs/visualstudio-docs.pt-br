---
title: 'CA1065: não gerar exceções em locais inesperados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1065
- DoNotRaiseExceptionsInUnexpectedLocations
helpviewer_keywords:
- DoNotRaiseExceptionsInUnexpectedLocations
- CA1065
ms.assetid: 4e1bade4-4ca2-4219-abc3-c7b2d741e157
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ddfc95d27179f48aef9444819cc0437a3143d5a0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539250"
---
# <a name="ca1065-do-not-raise-exceptions-in-unexpected-locations"></a>CA1065: Não acionar exceções em locais inesperados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotRaiseExceptionsInUnexpectedLocations|
|CheckId|CA1065|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método que não deve acionar exceções aciona uma exceção.

## <a name="rule-description"></a>Descrição da Regra
 Métodos que não devem lançar exceções podem ser categorizados da seguinte maneira:

- Métodos get da propriedade

- Métodos de acessadores de eventos

- Métodos iguais

- Métodos GetHashCode

- Métodos ToString

- Construtores estáticos

- Finalizadores

- Métodos Dispose

- Operadores de igualdade

- Operadores de conversão implícita

  As seções a seguir discutem esses tipos de método.

### <a name="property-get-methods"></a>Métodos get da propriedade
 As propriedades são basicamente campos inteligentes. Portanto, eles devem se comportar como um campo o máximo possível. Os campos não lançam exceções e nenhuma delas deve ser Propriedades. Se você tiver uma propriedade que gera uma exceção, considere torná-la um método.

 As exceções a seguir podem ser geradas de um método Get de propriedade:

- <xref:System.InvalidOperationException?displayProperty=fullName>e todos os derivativos (incluindo <xref:System.ObjectDisposedException?displayProperty=fullName> )

- <xref:System.NotSupportedException?displayProperty=fullName>e todos os derivativos

- <xref:System.ArgumentException?displayProperty=fullName>(somente de Get indexado)

- <xref:System.Collections.Generic.KeyNotFoundException>(somente de Get indexado)

### <a name="event-accessor-methods"></a>Métodos de acessadores de eventos
 Os acessadores de evento devem ser operações simples que não geram exceções. Um evento não deve gerar uma exceção quando você tenta adicionar ou remover um manipulador de eventos.

 As exceções a seguir podem ser geradas de um acessador de evento:

- <xref:System.InvalidOperationException?displayProperty=fullName>e todos os derivativos (incluindo <xref:System.ObjectDisposedException?displayProperty=fullName> )

- <xref:System.NotSupportedException?displayProperty=fullName>e todos os derivativos

- <xref:System.ArgumentException>e derivativos

### <a name="equals-methods"></a>Métodos iguais
 Os métodos **iguais** a seguir não devem gerar exceções:

- <xref:System.Object.Equals%2A?displayProperty=fullName>

- [M:IEquatable.Equals](https://msdn2.microsoft.com/library/ms131190(VS.80).aspx)

  Um método **Equals** deve retornar `true` ou `false` em vez de lançar uma exceção. Por exemplo, se Equals for passado dois tipos incompatíveis, ele deverá retornar apenas `false` em vez de lançar um <xref:System.ArgumentException> .

### <a name="gethashcode-methods"></a>Métodos GetHashCode
 Os seguintes métodos **GetHashCode** normalmente não devem gerar exceções:

- <xref:System.Object.GetHashCode%2A>

- [M:IEqualityComparer.GetHashCode (T)](https://msdn2.microsoft.com/library/system.collections.iequalitycomparer.gethashcode.aspx)

  **GetHashCode** sempre deve retornar um valor. Caso contrário, você pode perder itens na tabela de hash.

  As versões de **GetHashCode** que usam um argumento podem lançar um <xref:System.ArgumentException> . No entanto, **Object. GetHashCode** nunca deve gerar uma exceção.

### <a name="tostring-methods"></a>Métodos ToString
 O depurador usa <xref:System.Object.ToString%2A?displayProperty=fullName> para ajudar a exibir informações sobre objetos no formato de cadeia de caracteres. Portanto, **ToString** não deve alterar o estado de um objeto e não deve gerar exceções.

### <a name="static-constructors"></a>Construtores estáticos
 Lançar exceções de um construtor estático faz com que o tipo seja inutilizável no domínio do aplicativo atual. Você deve ter um bom motivo (como um problema de segurança) para lançar uma exceção de um construtor estático.

### <a name="finalizers"></a>Finalizadores
 Lançar uma exceção de um finalizador faz com que o CLR fail fast, que destrói o processo. Portanto, gerar exceções em um finalizador sempre deve ser evitado.

### <a name="dispose-methods"></a>Métodos Dispose
 Um <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> método não deve gerar uma exceção. Dispose é geralmente chamado como parte da lógica de limpeza em uma `finally` cláusula. Portanto, lançar explicitamente uma exceção de Dispose força o usuário a adicionar manipulação de exceção dentro da `finally` cláusula.

 O caminho do código **Dispose (false)** nunca deve gerar exceções, pois isso quase sempre é chamado de um finalizador.

### <a name="equality-operators--"></a>Operadores de igualdade (= =,! =)
 Como os métodos Equals, os operadores de igualdade devem retornar `true` ou `false` e não devem gerar exceções.

### <a name="implicit-cast-operators"></a>Operadores de conversão implícita
 Como o usuário geralmente não está ciente de que um operador de conversão implícita foi chamado, uma exceção gerada pelo operador de conversão implícita é completamente inesperada. Portanto, nenhuma exceção deve ser gerada de operadores de conversão implícitos.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para getters de propriedade, altere a lógica para que ela não precise mais lançar uma exceção ou altere a propriedade para um método.

 Para todos os outros tipos de método listados anteriormente, altere a lógica para que ela não deva mais lançar uma exceção.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se a violação tiver sido causada por uma declaração de exceção em vez de uma exceção gerada.

## <a name="related-rules"></a>Regras relacionadas
 [CA2219: Não acionar exceções em cláusulas de exceção](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md)

## <a name="see-also"></a>Consulte Também
 [Avisos de design](../code-quality/design-warnings.md)

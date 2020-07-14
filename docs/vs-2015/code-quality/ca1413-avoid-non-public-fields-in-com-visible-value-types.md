---
title: 'CA1413: Evite campos não públicos em tipos de valores visíveis COM | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1413
- AvoidNonpublicFieldsInComVisibleValueTypes
helpviewer_keywords:
- CA1413
- AvoidNonpublicFieldsInComVisibleValueTypes
ms.assetid: 1352e7eb-fefc-4239-8847-25edc7804a54
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1054330b26cf145ebcbc943a56dc699fe793999f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548454"
---
# <a name="ca1413-avoid-non-public-fields-in-com-visible-value-types"></a>CA1413: Evitar campos não públicos em tipos de valor visíveis no COM
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidNonpublicFieldsInComVisibleValueTypes|
|CheckId|CA1413|
|Categoria|Microsoft. Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo de valor marcado especificamente como visível para Component Object Model (COM) declara um campo de instância não pública.

## <a name="rule-description"></a>Descrição da Regra
 Os campos de instância não pública dos tipos de valor visíveis por COM permanecem visíveis para clientes COM. Examine o conteúdo do campo para obter informações que não devem ser expostas, ou que terão um efeito de design ou segurança indesejado.

 Por padrão, todos os tipos de valor público são visíveis para COM. No entanto, para reduzir os falsos positivos, essa regra requer que a visibilidade de COM do tipo seja explicitamente declarada. O assembly contentor deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> definido como `false` e o tipo deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute> definido como `true` .

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra e manter o campo oculto, altere o tipo de valor para um tipo de referência ou remova o <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributo do tipo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se a exposição pública do campo for aceitável.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-csharp[FxCop.Interoperability.NonpublicField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.NonpublicField/cs/FxCop.Interoperability.NonpublicField.cs#1)]
 [!code-vb[FxCop.Interoperability.NonpublicField#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.NonpublicField/vb/FxCop.Interoperability.NonpublicField.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1407: Evitar membros estáticos em tipos visíveis no COM](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

 [CA1017: Marcar assemblies com ComVisibleAttribute](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>Consulte Também
 Interoperação com tipos .NET qualificados de [código não gerenciado](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258) [para interoperabilidade](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)

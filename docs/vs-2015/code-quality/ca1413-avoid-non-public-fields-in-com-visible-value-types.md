---
title: 'CA1413: Evitar campos não públicos em tipos de valor visíveis COM | Microsoft Docs'
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 59ca3c5f53dee43bdd73eb706f03792458e71698
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691132"
---
# <a name="ca1413-avoid-non-public-fields-in-com-visible-value-types"></a>CA1413: Evitar campos não públicos em tipos de valor visíveis no COM
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AvoidNonpublicFieldsInComVisibleValueTypes|
|CheckId|CA1413|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo de valor é marcado especificamente como visível para COM Component Object Model () declara um campo de instância não públicos.

## <a name="rule-description"></a>Descrição da Regra
 Os campos de instância não pública dos tipos de valor visíveis por COM permanecem visíveis para clientes COM. Revise o conteúdo do campo para obter informações que não devem ser expostos ou que terá um efeito de design ou de segurança não intencional.

 Por padrão, todos os tipos de valor público são visíveis para COM. No entanto, para reduzir os falsos positivos, essa regra exige a visibilidade de COM do tipo a ser declarado explicitamente. O assembly que contém deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> definido como `false` e o tipo deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute> definido como `true`.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra e manter o campo ocultado, altere o tipo de valor para um tipo de referência ou remova o <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributo do tipo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra se pública exposição do campo for aceitável.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-csharp[FxCop.Interoperability.NonpublicField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.NonpublicField/cs/FxCop.Interoperability.NonpublicField.cs#1)]
 [!code-vb[FxCop.Interoperability.NonpublicField#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.NonpublicField/vb/FxCop.Interoperability.NonpublicField.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1407: Evitar membros estáticos em tipos visíveis COM](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

 [CA1017: Marcar assemblies com ComVisibleAttribute](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>Consulte também
 [Interoperação com código não gerenciado](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258) [qualificando tipos do .NET para interoperação](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)

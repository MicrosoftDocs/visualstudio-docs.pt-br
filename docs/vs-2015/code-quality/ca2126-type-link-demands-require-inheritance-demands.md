---
title: 'CA2126: Demandas de link de tipo exigem demandas de herança | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2126
- TypeLinkDemandsRequireInheritanceDemands
helpviewer_keywords:
- CA2126
- TypeLinkDemandsRequireInheritanceDemands
ms.assetid: 07b604e5-5579-4df9-a578-dadd0d8370a7
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 2fbf1a5f49e86cdc672f7b79207753d4d1949cf7
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58925487"
---
# <a name="ca2126-type-link-demands-require-inheritance-demands"></a>CA2126: As demandas de link de tipo exigem demandas de herança
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|TypeLinkDemandsRequireInheritanceDemands|
|CheckId|CA2126|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo sem lacre público é protegido com uma demanda de link tem um método substituível e nem o tipo nem o método é protegido com uma demanda de herança.

## <a name="rule-description"></a>Descrição da Regra
 Uma demanda de link em um método ou seu tipo declarativo requer que o chamador imediato do método para ter a permissão especificada. Uma exigência de herança em um método exige um método de substituição para ter a permissão especificada. Uma exigência de herança em um tipo requer uma classe derivada para ter a permissão especificada.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, proteja o tipo ou o método com uma demanda de herança para a mesma permissão como a demanda de link.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-cpp[FxCop.Security.TypesWithLinkDemands#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.TypesWithLinkDemands/cpp/FxCop.Security.TypesWithLinkDemands.cpp#1)]
 [!code-csharp[FxCop.Security.TypesWithLinkDemands#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TypesWithLinkDemands/cs/FxCop.Security.TypesWithLinkDemands.cs#1)]
 [!code-vb[FxCop.Security.TypesWithLinkDemands#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.TypesWithLinkDemands/vb/FxCop.Security.TypesWithLinkDemands.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2108: Revisar segurança declarativa em tipos de valor](../code-quality/ca2108-review-declarative-security-on-value-types.md)

 [CA2112: Tipos seguros não devem expor campos](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

 [CA2122: Não expor indiretamente métodos com demandas de link](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md)

 [CA2123: As demandas de link de substituição devem ser idênticas à base](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md)

## <a name="see-also"></a>Consulte também
 [Diretrizes de codificação segura](http://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [demandas de herança](http://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9) [demandas de Link](http://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) [demandas](http://msdn.microsoft.com/e5283e28-2366-4519-b27d-ef5c1ddc1f48)

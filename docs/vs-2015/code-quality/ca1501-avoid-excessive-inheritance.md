---
title: 'CA1501: evitar herança excessiva | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1501
- AvoidExcessiveInheritance
helpviewer_keywords:
- AvoidExcessiveInheritance
- CA1501
ms.assetid: 9e934746-1a4d-492a-91e4-085201abafa4
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: cf797ad67b7df2eb1f3ba1246e965ed6ebbd586d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547856"
---
# <a name="ca1501-avoid-excessive-inheritance"></a>CA1501: Evitar herança excessiva
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidExcessiveInheritance|
|CheckId|CA1501|
|Categoria|Microsoft. Maintainabilidade|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo está mais de quatro níveis abaixo na hierarquia de herança.

## <a name="rule-description"></a>Descrição da Regra
 As hierarquias de tipo profundamente aninhado podem ser difíceis de seguir, compreender e manter. Essa regra limita a análise a hierarquias no mesmo módulo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, derive o tipo de um tipo base que seja menos profundo na hierarquia de herança ou elimine alguns dos tipos base intermediários.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra. No entanto, o código pode ser mais difícil de manter. Observe que, dependendo da visibilidade dos tipos base, a resolução de violações dessa regra pode criar alterações significativas. Por exemplo, a remoção de tipos base públicos é uma alteração significativa.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-csharp[FxCop.Maintainability.ExcessiveInheritance#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.ExcessiveInheritance/cs/FxCop.Maintainability.ExcessiveInheritance.cs#1)]
 [!code-vb[FxCop.Maintainability.ExcessiveInheritance#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.ExcessiveInheritance/vb/FxCop.Maintainability.ExcessiveInheritance.vb#1)]

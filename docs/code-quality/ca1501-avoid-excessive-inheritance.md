---
title: 'CA1501: evitar herança excessiva'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1501
- AvoidExcessiveInheritance
helpviewer_keywords:
- AvoidExcessiveInheritance
- CA1501
ms.assetid: 9e934746-1a4d-492a-91e4-085201abafa4
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 0627d246fe9f9f72a95cded7daf8d2c94bf20b3a
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45546927"
---
# <a name="ca1501-avoid-excessive-inheritance"></a>CA1501: evitar herança excessiva

|||
|-|-|
|NomeDoTipo|AvoidExcessiveInheritance|
|CheckId|CA1501|
|Categoria|Microsoft.Maintainability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo está mais de quatro níveis abaixo na hierarquia de herança.

## <a name="rule-description"></a>Descrição da regra
 As hierarquias de tipo profundamente aninhado podem ser difíceis de seguir, compreender e manter. Essa regra limita a análise de hierarquias no mesmo módulo.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, derivar o tipo de um tipo base que é menos detalhado na hierarquia de herança ou eliminar alguns dos tipos de base intermediários.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra. No entanto, o código pode ser mais difícil de manter. Observe que, dependendo da visibilidade de tipos base, resolver as violações dessa regra pode criar alterações significativas. Por exemplo, a remoção de tipos de base públicos é uma alteração significativa.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-csharp[FxCop.Maintainability.ExcessiveInheritance#1](../code-quality/codesnippet/CSharp/ca1501-avoid-excessive-inheritance_1.cs)]
 [!code-vb[FxCop.Maintainability.ExcessiveInheritance#1](../code-quality/codesnippet/VisualBasic/ca1501-avoid-excessive-inheritance_1.vb)]
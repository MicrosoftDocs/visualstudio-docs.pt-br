---
title: 'CA1506: evitar acoplamento de classe excessiva | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidExcessiveClassCoupling
- CA1506
helpviewer_keywords:
- AvoidExcessiveClassCoupling
- CA1506
ms.assetid: 9f0943c0-e802-4e3f-8798-2ab8653ddc80
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 07f19cb9d4aa2ed118898a1816092479cbd16565
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545698"
---
# <a name="ca1506-avoid-excessive-class-coupling"></a>CA1506: Evitar acoplamento de classes excessivo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidExcessiveClassCoupling|
|CheckId|CA1506|
|Categoria|Microsoft. Maintainabilidade|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo ou método é combinado com muitos outros tipos.

## <a name="rule-description"></a>Descrição da Regra
 Esta regra mede o acoplamento de classes contando o número de referências de tipo exclusivas que um tipo ou um método contém.

 Tipos e métodos que têm um alto grau de acoplamento de classe podem ser difíceis de manter. É uma boa prática ter tipos e métodos que apresentam baixo acoplamento e alta coesão.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir essa violação, tente recriar o tipo ou o método para reduzir o número de tipos aos quais ele está acoplado.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Exclua este aviso quando o tipo ou método ainda for considerado passível de manutenção, apesar de seu grande número de dependências em outros tipos.

## <a name="see-also"></a>Consulte Também
 [Avisos de facilidade](../code-quality/maintainability-warnings.md) [de manutenção medindo a complexidade e a manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)

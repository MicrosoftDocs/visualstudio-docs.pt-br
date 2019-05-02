---
title: 'CA1506: Evite acoplamento de classes excessivo | Microsoft Docs'
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 1c5a5e070892f7efc096b0f8e24952bb9d139969
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58926335"
---
# <a name="ca1506-avoid-excessive-class-coupling"></a>CA1506: Evitar acoplamento de classes excessivo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AvoidExcessiveClassCoupling|
|CheckId|CA1506|
|Categoria|Microsoft.Maintainability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo ou método é acoplado com muitos outros tipos.

## <a name="rule-description"></a>Descrição da Regra
 Esta regra mede o acoplamento de classes contando o número de referências de tipo exclusivas que um tipo ou um método contém.

 Tipos e métodos que têm um alto grau de acoplamento de classes podem ser difícil de manter. É uma boa prática tem tipos e métodos que apresentam menor acoplamento e maior coesão.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir essa violação, tente recriar o tipo ou método para reduzir o número de tipos para o qual ele está acoplado.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Exclua esse aviso quando o tipo ou método ainda é considerado sustentável, apesar de seu grande número de dependências em outros tipos.

## <a name="see-also"></a>Consulte também
 [Avisos de facilidade de manutenção](../code-quality/maintainability-warnings.md) [medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)

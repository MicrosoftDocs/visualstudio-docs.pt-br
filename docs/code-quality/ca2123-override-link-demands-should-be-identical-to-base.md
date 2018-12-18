---
title: 'CA2123: as demandas de link de substituição devem ser idênticas à base'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2123
- OverrideLinkDemandsShouldBeIdenticalToBase
helpviewer_keywords:
- OverrideLinkDemandsShouldBeIdenticalToBase
- CA2123
ms.assetid: 4538ecd5-fc6f-4480-ab00-90b2ce4730db
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ebb37743f9259390aba400a5d89d24b5f41a0d49
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45546974"
---
# <a name="ca2123-override-link-demands-should-be-identical-to-base"></a>CA2123: as demandas de link de substituição devem ser idênticas à base

|||
|-|-|
|NomeDoTipo|OverrideLinkDemandsShouldBeIdenticalToBase|
|CheckId|CA2123|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método público ou protegido em um tipo público ou substitui um método implementa uma interface e não tem o mesmo [demandas de Link](/dotnet/framework/misc/link-demands) como a interface ou método virtual.

## <a name="rule-description"></a>Descrição da regra
 Esta regra compara um método ao método de base, que é uma interface ou um método virtual em outro tipo e, em seguida, compara as exigências de vínculo em cada um. Uma violação será relatada se o método ou o método base tem uma demanda de link e o outro não.

 Se essa regra for violada, um chamador mal-intencionado poderá ignorar a demanda de link simplesmente chamando o método não seguro.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, aplica a mesma demanda de link para o método de substituição ou implementação. Se isso não é possível marcar o método com uma demanda completa ou remova o atributo completamente.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra as diversas violações dessa regra.

 [!code-csharp[FxCop.Security.OverridesAndSecurity#1](../code-quality/codesnippet/CSharp/ca2123-override-link-demands-should-be-identical-to-base_1.cs)]

## <a name="see-also"></a>Consulte também

- [Diretrizes de codificação segura](/dotnet/standard/security/secure-coding-guidelines)
- [Demandas de link](/dotnet/framework/misc/link-demands)
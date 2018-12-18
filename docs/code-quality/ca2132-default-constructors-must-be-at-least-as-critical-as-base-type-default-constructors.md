---
title: 'CA2132: os construtores padrão devem ser pelo menos críticos como construtores padrão do tipo base'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2132
ms.assetid: e758afa1-8bde-442a-8a0a-bd1ea7b0ce4d
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 66e1f402e082eb1ee42faa3e04ea319dca3ed1d5
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45546766"
---
# <a name="ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors"></a>CA2132: os construtores padrão devem ser pelo menos críticos como construtores padrão do tipo base

|||
|-|-|
|NomeDoTipo|DefaultConstructorsMustHaveConsistentTransparency|
|CheckId|CA2132|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

> [!NOTE]
> Esse aviso só será aplicado ao código que está executando o CoreCLR (a versão do CLR que é específico para aplicativos web do Silverlight).

## <a name="cause"></a>Causa

O atributo de transparência do construtor padrão de uma classe derivada não é tão crítico quanto a transparência da classe base.

## <a name="rule-description"></a>Descrição da regra

Tipos e membros que têm o <xref:System.Security.SecurityCriticalAttribute> não pode ser usado pelo código do aplicativo do Silverlight. Os tipos de segurança crítica e os membros só podem ser usados por código confiável no .NET Framework para a biblioteca de classes do Silverlight. Como uma construção pública ou protegida em uma classe derivada deve ter a mesma transparência maior que sua classe base, uma classe em um aplicativo não pode ser derivada de uma classe marcada como SecurityCritical.

Para o código de plataforma do CoreCLR, se um tipo base tem um construtor público ou protegido padrão não transparente, em seguida, o tipo derivado deve obedecer as regras de herança do construtor padrão. O tipo derivado também deve ter um construtor padrão e esse construtor deve ser pelo menos construtor crítica do padrão do tipo base.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir a violação, remova o tipo ou não derivam de tipo não transparente de segurança.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Não suprima avisos dessa regra. As violações dessa regra pelo código do aplicativo resultará no CoreCLR se recusando a carregar o tipo com um <xref:System.TypeLoadException>.

### <a name="code"></a>Código

[!code-csharp[FxCop.Security.CA2132.DefaultConstructorsMustHaveConsistentTransparency#1](../code-quality/codesnippet/CSharp/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors_1.cs)]
---
title: 'CA1052: os tipos de suporte estático devem ser lacrados'
ms.date: 11/09/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- StaticHolderTypesShouldBeSealed
- CA1052
helpviewer_keywords:
- CA1052
- StaticHolderTypesShouldBeSealed
ms.assetid: 51a3165d-781e-4a55-aa0d-ea25fee7d4f2
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 937a5eba672eef928dd4f8c0e5356e504d769153
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51348652"
---
# <a name="ca1052-static-holder-types-should-be-sealed"></a>CA1052: os tipos de suporte estático devem ser lacrados

|||
|-|-|
|NomeDoTipo|StaticHolderTypesShouldBeSealed|
|CheckId|CA1052|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Um público ou protegido, não-abstrata tipo contém apenas membros estáticos e não é declarado com o [lacrado](/dotnet/csharp/language-reference/keywords/sealed) ([NotInheritable](/dotnet/visual-basic/language-reference/modifiers/notinheritable)) modificador.

## <a name="rule-description"></a>Descrição da regra

CA1052 regra pressupõe que um tipo que contém apenas membros estáticos não foi projetado para ser herdadas, pois o tipo não fornece nenhuma funcionalidade que pode ser substituída em um tipo derivado. Um tipo que não se destina a ser herdada que deve ser marcado com o `sealed` ou `NotInheritable` modificador para proibir o uso como um tipo base. Essa regra não é disparado para classes abstratas.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, marque o tipo como `sealed` ou `NotInheritable`. Se você estiver direcionando o .NET Framework 2.0 ou posterior, uma abordagem melhor é marcar o tipo como `static` ou `Shared`. Dessa forma, você não precisa declarar um construtor particular para impedir que a classe que está sendo criado.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Suprima um aviso nessa regra somente se o tipo foi projetado para ser herdada. A ausência do `sealed` ou `NotInheritable` modificador sugere que o tipo é útil como um tipo base.

## <a name="example-of-a-violation"></a>Exemplo de uma violação

O exemplo a seguir mostra um tipo que viola a regra.

[!code-csharp[FxCop.Design.StaticMembers#1](../code-quality/codesnippet/CSharp/ca1052-static-holder-types-should-be-sealed_1.cs)]
[!code-vb[FxCop.Design.StaticMembers#1](../code-quality/codesnippet/VisualBasic/ca1052-static-holder-types-should-be-sealed_1.vb)]
[!code-cpp[FxCop.Design.StaticMembers#1](../code-quality/codesnippet/CPP/ca1052-static-holder-types-should-be-sealed_1.cpp)]

## <a name="fix-with-the-static-modifier"></a>Corrigir com o modificador estático

O exemplo a seguir mostra como corrigir uma violação dessa regra, marcando o tipo com o `static` modificador em C#.

[!code-csharp[FxCop.Design.StaticMembersFixed#1](../code-quality/codesnippet/CSharp/ca1052-static-holder-types-should-be-sealed_2.cs)]

## <a name="related-rules"></a>Regras relacionadas

[CA1053: os tipos de suporte estático não devem ter construtores](../code-quality/ca1053-static-holder-types-should-not-have-constructors.md)
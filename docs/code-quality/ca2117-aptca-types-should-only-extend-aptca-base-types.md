---
title: 'CA2117: Tipos APTCA devem estender somente tipos base APTCA'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2117
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
helpviewer_keywords:
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
- CA2117
ms.assetid: c505b586-2f1e-47cb-98ee-a5afcbeda70f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 832d2c9fc1d4b9138a7cd1bc39868b3c4bf1b814
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232649"
---
# <a name="ca2117-aptca-types-should-only-extend-aptca-base-types"></a>CA2117: Tipos APTCA devem estender somente tipos base APTCA

|||
|-|-|
|NomeDoTipo|AptcaTypesShouldOnlyExtendAptcaBaseTypes|
|CheckId|CA2117|
|Categoria|Microsoft.Security|
|Alteração significativa|Quebra|

## <a name="cause"></a>Causa

Um tipo público ou protegido em um assembly com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> atributo é herdado de um tipo declarado em um assembly que não tem o atributo.

## <a name="rule-description"></a>Descrição da regra

Por padrão, os tipos públicos ou protegidos em assemblies com nomes fortes são implicitamente protegidos por um [InheritanceDemand](xref:System.Security.Permissions.SecurityAction#System_Security_Permissions_SecurityAction_InheritanceDemand) para confiança total. Os assemblies de nome forte marcados com <xref:System.Security.AllowPartiallyTrustedCallersAttribute> o atributo (APTCA) não têm essa proteção. O atributo desabilita a demanda de herança. Tipos expostos declarados em um assembly sem uma demanda de herança são herdáveis por tipos que não têm confiança total.

Quando o atributo APTCA está presente em um assembly totalmente confiável e um tipo no assembly é herdado de um tipo que não permite chamadores parcialmente confiáveis, uma exploração de segurança é possível. Se dois tipos `T1` e `T2` atenderem às seguintes condições, os chamadores mal-intencionados poderão usar `T1` o tipo para ignorar a demanda de herança de confiança `T2`total implícita que protege:

- `T1`é um tipo público declarado em um assembly totalmente confiável que tem o atributo APTCA.

- `T1`herda de um tipo `T2` fora de seu assembly.

- `T2`o assembly do não tem o atributo APTCA e, portanto, não deve ser herdável por tipos em assemblies parcialmente confiáveis.

Um tipo `X` parcialmente confiável pode herdar `T1`de, que fornece acesso a membros herdados declarados em. `T2` Como `T2` o não tem o atributo APTCA, seu tipo derivado imediato (`T1`) deve atender a uma demanda de herança para confiança total; `T1` tem confiança total e, portanto, satisfaz essa verificação. O risco de segurança é `X` porque o não participa da demanda de herança que protege `T2` contra subclasses não confiáveis. Por esse motivo, os tipos com o atributo APTCA não devem estender tipos que não tenham o atributo.

Outro problema de segurança, e talvez um mais comum, é que o tipo derivado (`T1`) pode, por meio de um erro do programador, expor membros protegidos do tipo que requer`T2`confiança total (). Quando essa exposição ocorre, chamadores não confiáveis têm acesso a informações que devem estar disponíveis somente para tipos totalmente confiáveis.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Se o tipo relatado pela violação estiver em um assembly que não requer o atributo APTCA, remova-o.

Se o atributo APTCA for necessário, adicione uma solicitação de herança para confiança total ao tipo. A demanda de herança protege contra herança por tipos não confiáveis.

É possível corrigir uma violação adicionando o atributo APTCA aos assemblies dos tipos base relatados pela violação. Não faça isso sem primeiro realizar uma revisão de segurança intensiva de todo o código nos assemblies e de todo o código que depende dos assemblies.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Para suprimir um aviso dessa regra com segurança, você deve garantir que os membros protegidos expostos pelo seu tipo não façam direta ou indiretamente que os chamadores não confiáveis acessem informações confidenciais, operações ou recursos que podem ser usados de maneira destrutiva.

## <a name="example"></a>Exemplo

O exemplo a seguir usa dois assemblies e um aplicativo de teste para ilustrar a vulnerabilidade de segurança detectada por essa regra. O primeiro assembly não tem o atributo APTCA e não deve ser herdável por tipos parcialmente confiáveis (representados por `T2` na discussão anterior).

[!code-csharp[FxCop.Security.NoAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_1.cs)]

O segundo assembly, representado pela `T1` na discussão anterior, é totalmente confiável e permite chamadores parcialmente confiáveis.

[!code-csharp[FxCop.Security.YesAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_2.cs)]

O tipo de teste, representado `X` pela na discussão anterior, está em um assembly parcialmente confiável.

[!code-csharp[FxCop.Security.TestAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_3.cs)]

Este exemplo gera a seguinte saída:

```txt
Meet at the shady glen 2/22/2003 12:00:00 AM!
From Test: sunny meadow
Meet at the sunny meadow 2/22/2003 12:00:00 AM!
```

## <a name="related-rules"></a>Regras relacionadas

[CA2116: Os métodos APTCA só devem chamar métodos APTCA](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)

## <a name="see-also"></a>Consulte também

- [Diretrizes de codificação segura](/dotnet/standard/security/secure-coding-guidelines)
- [Usando bibliotecas de código parcialmente confiável](/dotnet/framework/misc/using-libraries-from-partially-trusted-code)

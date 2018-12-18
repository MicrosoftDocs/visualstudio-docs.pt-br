---
title: 'CA2117: os tipos APTCA só devem estender tipos base APTCA'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8dac5acc0b7c7fff02862853bfd996362f80d1cc
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547494"
---
# <a name="ca2117-aptca-types-should-only-extend-aptca-base-types"></a>CA2117: os tipos APTCA só devem estender tipos base APTCA

|||
|-|-|
|NomeDoTipo|AptcaTypesShouldOnlyExtendAptcaBaseTypes|
|CheckId|CA2117|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Um tipo público ou protegido em um assembly com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> atributo herda de um tipo declarado em um assembly que não tem o atributo.

## <a name="rule-description"></a>Descrição da regra

Por padrão, os tipos de públicos ou protegidos em assemblies com nomes fortes implicitamente são protegidos por um [InheritanceDemand](xref:System.Security.Permissions.SecurityAction#System_Security_Permissions_SecurityAction_InheritanceDemand) para confiança total. Assemblies de nome forte é marcado com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> atributo (APTCA) não tem essa proteção. O atributo desabilita a exigência de herança. Declarado em um assembly sem uma exigência de herança de tipos expostos são herdados pelos tipos que não têm confiança total.

Quando o atributo APTCA estiver presente em um assembly totalmente confiável e um tipo no assembly for herdado de um tipo que não permita chamadores parcialmente confiáveis, será possível uma exploração de segurança. Se dois tipos `T1` e `T2` atendem às condições a seguir, chamadores mal-intencionados podem usar o tipo `T1` para ignorar a exigência de herança de confiança total implícito que protege `T2`:

- `T1` um tipo público é declarado em um assembly totalmente confiável que tem o atributo APTCA.

- `T1` herdado de um tipo `T2` fora do assembly.

- `T2`do assembly não tem o atributo APTCA e, portanto, não devem ser herdada por tipos em assemblies parcialmente confiáveis.

Um tipo parcialmente confiável `X` podem herdar de `T1`, que concede a ele acesso a membros herdados declarados em `T2`. Porque `T2` não tem o atributo APTCA, seu tipo derivado imediato (`T1`) deve atender uma demanda de herança de confiança total; `T1` tem confiança total e, portanto, satisfaz essa verificação. O risco de segurança é porque `X` não participa de satisfazer a demanda de herança que protege `T2` de criação de subclasses não confiável. Por esse motivo, os tipos com o atributo APTCA não devem estender tipos que não têm o atributo.

Outro problema de segurança e talvez um mais comum, é que o tipo derivado (`T1`) pode, por meio de erro do programador, expor os membros protegidos do tipo que requer confiança total (`T2`). Quando essa exposição ocorre, os chamadores não confiáveis obtém acesso a informações que devem estar disponíveis somente para tipos de totalmente confiáveis.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Se o tipo relatado pela violação de está em um assembly que não requer o atributo APTCA, removê-lo.

Se o atributo APTCA for necessário, adicione uma exigência de herança de confiança total para o tipo. A exigência de herança protege contra herança por tipos não confiáveis.

É possível corrigir uma violação, adicionando o atributo APTCA aos assemblies dos tipos base relatados pela violação. Fazer isso sem primeiro conduzir uma revisão de segurança com uso intensivo de todo o código nos assemblies e todo o código que depende dos assemblies.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Para suprimir com segurança um aviso nessa regra, você deve garantir que membros protegidos expostos pelo seu tipo não direta ou indiretamente permitem chamadores não-confiáveis acessar informações confidenciais, operações ou recursos que podem ser usados de forma destrutivas.

## <a name="example"></a>Exemplo

O exemplo a seguir usa dois assemblies e um aplicativo de teste para ilustrar a vulnerabilidade de segurança detectada por essa regra. O primeiro conjunto não tem o atributo APTCA e não devem ser herdado por tipos parcialmente confiáveis (representado por `T2` na discussão anterior).

[!code-csharp[FxCop.Security.NoAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_1.cs)]

O segundo conjunto, representado por `T1` na discussão anterior, é totalmente confiável e permite que os chamadores parcialmente confiáveis.

[!code-csharp[FxCop.Security.YesAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_2.cs)]

O tipo de teste, representado por `X` na discussão anterior, está em um assembly parcialmente confiável.

[!code-csharp[FxCop.Security.TestAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_3.cs)]

Este exemplo gera a seguinte saída:

```txt
Meet at the shady glen 2/22/2003 12:00:00 AM!
From Test: sunny meadow
Meet at the sunny meadow 2/22/2003 12:00:00 AM!
```

## <a name="related-rules"></a>Regras relacionadas

[CA2116: os métodos APTCA só devem chamar métodos APTCA](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)

## <a name="see-also"></a>Consulte também

- [Diretrizes de codificação segura](/dotnet/standard/security/secure-coding-guidelines)
- [Usando bibliotecas de código parcialmente confiável](/dotnet/framework/misc/using-libraries-from-partially-trusted-code)

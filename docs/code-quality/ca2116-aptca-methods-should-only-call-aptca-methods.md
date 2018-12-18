---
title: 'CA2116: os métodos APTCA só devem chamar métodos APTCA'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
helpviewer_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
ms.assetid: 8b91637e-891f-4dde-857b-bf8012270ec4
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7decf94644bdb055f38c267c945dc0dcc813550a
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547913"
---
# <a name="ca2116-aptca-methods-should-only-call-aptca-methods"></a>CA2116: os métodos APTCA só devem chamar métodos APTCA

|||
|-|-|
|NomeDoTipo|AptcaMethodsShouldOnlyCallAptcaMethods|
|CheckId|CA2116|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Um método em um assembly com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> atributo chama um método em um assembly que não tem o atributo.

## <a name="rule-description"></a>Descrição da regra

Por padrão, os métodos públicos ou protegidos em assemblies com nomes fortes implicitamente são protegidos por um [demandas de Link](/dotnet/framework/misc/link-demands) para confiança total; apenas totalmente confiável os chamadores podem acessar um assembly de nome forte. Assemblies de nome forte é marcado com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> atributo (APTCA) não tem essa proteção. O atributo desabilita a demanda de link, fazendo com que o assembly acessível aos chamadores que não têm confiança total, como o código em execução de uma intranet ou da Internet.

Quando o atributo APTCA estiver presente em um assembly totalmente confiável e o assembly executar código em outro assembly que não permita chamadores parcialmente confiáveis, será possível uma exploração de segurança. Se dois métodos `M1` e `M2` atendem às condições a seguir, chamadores mal-intencionados podem usar o método `M1` para ignorar a demanda de link de confiança total implícito que protege `M2`:

- `M1` um método público é declarado em um assembly totalmente confiável que tem o atributo APTCA.

- `M1` chama um método `M2` fora `M1`do assembly.

- `M2`do assembly não tem o atributo APTCA e, portanto, não devem ser executado por, ou em nome dos chamadores parcialmente confiáveis.

Um chamador parcialmente confiável `X` pode chamar o método `M1`, causando `M1` chamar `M2`. Porque `M2` não tem o atributo APTCA, seu chamador imediato (`M1`) deve atender uma demanda de link para confiança total; `M1` tem confiança total e, portanto, satisfaz essa verificação. O risco de segurança é porque `X` não participa de satisfazer a demanda de link que protege `M2` de chamadores não confiáveis. Portanto, os métodos com o atributo APTCA não devem chamar métodos que não têm o atributo.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Se o atributo APCTA for necessário, use uma demanda para proteger o método que chama o assembly de confiança total. As permissões exatas que você demanda dependerá a funcionalidade exposta pelo seu método. Se for possível, proteja o método com uma demanda de confiança total garantir que a funcionalidade subjacente não é exposta a chamadores parcialmente confiáveis. Se isso não for possível, selecione um conjunto de permissões que efetivamente protege a funcionalidade exposta.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Para suprimir com segurança um aviso nessa regra, você deve garantir que a funcionalidade exposta pelo seu método não direta ou indiretamente permite chamadores acessem informações confidenciais, operações ou recursos que podem ser usados de forma destrutivas.

## <a name="example-1"></a>Exemplo 1
 O exemplo a seguir usa dois assemblies e um aplicativo de teste para ilustrar a vulnerabilidade de segurança detectada por essa regra. O primeiro conjunto não tem o atributo APTCA e não deve ser acessível a chamadores parcialmente confiáveis (representado por `M2` na discussão anterior).

 [!code-csharp[FxCop.Security.NoAptca#1](../code-quality/codesnippet/CSharp/ca2116-aptca-methods-should-only-call-aptca-methods_1.cs)]

## <a name="example-2"></a>Exemplo 2
 O segundo conjunto é totalmente confiável e permite que os chamadores parcialmente confiáveis (representado por `M1` na discussão anterior).

 [!code-csharp[FxCop.Security.YesAptca#1](../code-quality/codesnippet/CSharp/ca2116-aptca-methods-should-only-call-aptca-methods_2.cs)]

## <a name="example-3"></a>Exemplo 3:
 O aplicativo de teste (representado por `X` na discussão anterior) é parcialmente confiável.

 [!code-csharp[FxCop.Security.TestAptcaMethods#1](../code-quality/codesnippet/CSharp/ca2116-aptca-methods-should-only-call-aptca-methods_3.cs)]

Este exemplo gera a seguinte saída:

```txt
Demand for full trust:Request failed.
ClassRequiringFullTrust.DoWork was called.
```

## <a name="related-rules"></a>Regras relacionadas

- [CA2117: os tipos APTCA só devem estender tipos base APTCA](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)

## <a name="see-also"></a>Consulte também

- [Diretrizes de codificação segura](/dotnet/standard/security/secure-coding-guidelines)
- [Usando bibliotecas de código parcialmente confiável](/dotnet/framework/misc/using-libraries-from-partially-trusted-code)
- [Demandas de link](/dotnet/framework/misc/link-demands)
- [Dados e modelagem](/dotnet/framework/data/index)
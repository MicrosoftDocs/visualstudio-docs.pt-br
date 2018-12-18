---
title: 'CA1046: não sobrecarregar igualdades de operador em tipos de referência'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotOverloadOperatorEqualsOnReferenceTypes
- CA1046
helpviewer_keywords:
- CA1046
- DoNotOverloadOperatorEqualsOnReferenceTypes
ms.assetid: c1dfbfe3-63f9-4005-a81a-890427b77e79
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3f0aeb519fdc22d3fb68812d24979c7aa6c23f85
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45551688"
---
# <a name="ca1046-do-not-overload-operator-equals-on-reference-types"></a>CA1046: não sobrecarregar igualdades de operador em tipos de referência

|||
|-|-|
|NomeDoTipo|DoNotOverloadOperatorEqualsOnReferenceTypes|
|CheckId|CA1046|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo de referência pública ou público aninhado sobrecarrega o operador de igualdade.

## <a name="rule-description"></a>Descrição da regra
 Para tipos de referência, a implementação padrão do operador de igualdade está quase sempre correta. Por padrão, duas referências só serão iguais se apontarem para o mesmo objeto.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, remova a implementação do operador de igualdade.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, quando o tipo de referência se comporta como um tipo de valor interno. Se for significativo para fazer a adição ou subtração em instâncias do tipo, é provavelmente correto implementar o operador de igualdade e suprimir a violação.

## <a name="example"></a>Exemplo
 O exemplo a seguir demonstra o comportamento padrão ao comparar duas referências.

 [!code-csharp[FxCop.Design.RefTypesNoEqualityOp#1](../code-quality/codesnippet/CSharp/ca1046-do-not-overload-operator-equals-on-reference-types_1.cs)]

## <a name="example"></a>Exemplo

O aplicativo a seguir compara algumas referências.

[!code-csharp[FxCop.Design.TestRefTypesNoEqualityOp#1](../code-quality/codesnippet/CSharp/ca1046-do-not-overload-operator-equals-on-reference-types_2.cs)]

Este exemplo gera a seguinte saída:

```txt
a = new (2,2) and b = new (2,2) are equal? No
c and a are equal? Yes
b and a are == ? No
c and a are == ? Yes
```

## <a name="related-rules"></a>Regras relacionadas

[CA1013: sobrecarregar operador Equals ao sobrecarregar adicionar e subtrair](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md)

## <a name="see-also"></a>Consulte também

- <xref:System.Object.Equals%2A?displayProperty=fullName>
- [Operadores de igualdade](/dotnet/standard/design-guidelines/equality-operators)
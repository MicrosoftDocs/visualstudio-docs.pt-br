---
title: 'CA2119: os métodos para lacrar que atendam a interfaces privadas'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SealMethodsThatSatisfyPrivateInterfaces
- CA2119
helpviewer_keywords:
- CA2119
- SealMethodsThatSatisfyPrivateInterfaces
ms.assetid: 483d02e1-cfaf-4754-a98f-4116df0f3509
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: aa207e85bcb7054b1a7b91ac8dd29ff45fe1091a
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45550590"
---
# <a name="ca2119-seal-methods-that-satisfy-private-interfaces"></a>CA2119: os métodos para lacrar que atendam a interfaces privadas

|||
|-|-|
|NomeDoTipo|SealMethodsThatSatisfyPrivateInterfaces|
|CheckId|CA2119|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público herdável fornece uma implementação de método substituível de uma `internal` (`Friend` no Visual Basic) interface.

## <a name="rule-description"></a>Descrição da regra
 Métodos de interface tem acessibilidade pública, que não pode ser alterada por tipo de implementação. Uma interface interna cria um contrato que não se destina a ser implementada fora do assembly que define a interface. Um tipo público que implementa um método de uma interface interna usando o `virtual` (`Overridable` no Visual Basic) modificador permite que o método a ser substituído por um tipo derivado que está fora do assembly. Se um segundo tipo no assembly de definição chama o método e espera que um contrato somente interno, o comportamento pode ficar comprometido quando, em vez disso, o método substituído no assembly externo é executado. Isso cria uma vulnerabilidade de segurança.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, impedir que o método que está sendo substituído fora do assembly usando um dos seguintes:

- Verifique o tipo de declaração `sealed` (`NotInheritable` no Visual Basic).

- Altere a acessibilidade do tipo declarativo para `internal` (`Friend` no Visual Basic).

- Remova todos os construtores públicos do tipo de declaração.

- Implementar o método sem usar o `virtual` modificador.

- Implemente o método explicitamente.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso desta regra se, depois de uma análise cuidadosa, há nenhum problema de segurança que pode ser explorável se o método for substituído fora do assembly.

## <a name="example-1"></a>Exemplo 1
 O exemplo a seguir mostra um tipo, `BaseImplementation`, que viola essa regra.

 [!code-cpp[FxCop.Security.SealMethods1#1](../code-quality/codesnippet/CPP/ca2119-seal-methods-that-satisfy-private-interfaces_1.cpp)]
 [!code-csharp[FxCop.Security.SealMethods1#1](../code-quality/codesnippet/CSharp/ca2119-seal-methods-that-satisfy-private-interfaces_1.cs)]
 [!code-vb[FxCop.Security.SealMethods1#1](../code-quality/codesnippet/VisualBasic/ca2119-seal-methods-that-satisfy-private-interfaces_1.vb)]

## <a name="example-2"></a>Exemplo 2
 O exemplo a seguir explora a implementação do método virtual do exemplo anterior.

 [!code-cpp[FxCop.Security.SealMethods2#1](../code-quality/codesnippet/CPP/ca2119-seal-methods-that-satisfy-private-interfaces_2.cpp)]
 [!code-csharp[FxCop.Security.SealMethods2#1](../code-quality/codesnippet/CSharp/ca2119-seal-methods-that-satisfy-private-interfaces_2.cs)]
 [!code-vb[FxCop.Security.SealMethods2#1](../code-quality/codesnippet/VisualBasic/ca2119-seal-methods-that-satisfy-private-interfaces_2.vb)]

## <a name="see-also"></a>Consulte também

- [Interfaces](/dotnet/csharp/programming-guide/interfaces/index)
- [Interfaces](/dotnet/visual-basic/programming-guide/language-features/interfaces/index)
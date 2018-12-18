---
title: 'CA1033: os métodos de interface devem ser chamáveis por tipos filho'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- InterfaceMethodsShouldBeCallableByChildTypes
- CA1033
helpviewer_keywords:
- CA1033
- InterfaceMethodsShouldBeCallableByChildTypes
ms.assetid: 9f171497-a5e3-4769-a77b-7aed755b2662
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b56cd055fa8413d7d98a1c0d6d8b538a8a858af6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49941315"
---
# <a name="ca1033-interface-methods-should-be-callable-by-child-types"></a>CA1033: os métodos de interface devem ser chamáveis por tipos filho

|||
|-|-|
|NomeDoTipo|InterfaceMethodsShouldBeCallableByChildTypes|
|CheckId|CA1033|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo visível externamente sem lacre fornece uma implementação de método explícita de uma interface pública e não fornece um método visível externamente alternativo com o mesmo nome.

## <a name="rule-description"></a>Descrição da regra
 Considere um tipo base que implementa explicitamente um método de interface pública. Um tipo derivado do tipo base pode acessar o método de interface herdada apenas por meio de uma referência à instância atual (`this` em c#) que é convertido para a interface. Se o tipo derivado (explicitamente) reimplementa o método de interface herdada, a implementação base não pode mais ser acessada. A chamada por meio de referência de instância atual invocará a implementação derivada; Isso causa recursão e um estouro de pilha eventual.

 Essa regra não relata uma violação para uma implementação explícita de <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> quando um visível externamente `Close()` ou `System.IDisposable.Dispose(Boolean)` método é fornecido.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, implemente um novo método que expõe a mesma funcionalidade e é visível para tipos derivados ou alterar para uma implementação não explícitas. Se uma alteração significativa é aceitável, uma alternativa é tornar o tipo selado.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, se um método visível externamente é fornecida que tem a mesma funcionalidade, mas o método implementado explicitamente um nome diferente.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo `ViolatingBase`, que viola a regra e um tipo, `FixedBase`, que mostra uma correção para a violação.

 [!code-csharp[FxCop.Design.ExplicitMethodImplementations#1](../code-quality/codesnippet/CSharp/ca1033-interface-methods-should-be-callable-by-child-types_1.cs)]

## <a name="see-also"></a>Consulte também
 [Interfaces](/dotnet/csharp/programming-guide/interfaces/index)
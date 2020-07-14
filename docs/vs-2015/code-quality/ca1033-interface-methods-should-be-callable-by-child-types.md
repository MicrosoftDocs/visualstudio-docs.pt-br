---
title: 'CA1033: métodos de interface devem ser chamados por tipos filho | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- InterfaceMethodsShouldBeCallableByChildTypes
- CA1033
helpviewer_keywords:
- CA1033
- InterfaceMethodsShouldBeCallableByChildTypes
ms.assetid: 9f171497-a5e3-4769-a77b-7aed755b2662
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 18629f8d5c63b652d6539db10c6e6dba5d621c24
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542292"
---
# <a name="ca1033-interface-methods-should-be-callable-by-child-types"></a>CA1033: Métodos de interface devem ser chamados por tipos filho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|InterfaceMethodsShouldBeCallableByChildTypes|
|CheckId|CA1033|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo visível externamente sem lacre fornece uma implementação de método explícita de uma interface pública e não fornece um método visível externamente alternativo com o mesmo nome.

## <a name="rule-description"></a>Descrição da Regra
 Considere um tipo base que implementa explicitamente um método de interface pública. Um tipo que deriva do tipo base pode acessar o método de interface herdado somente por meio de uma referência à instância atual ( `this` em C#) que é convertida para a interface. Se o tipo derivado reimplementar (explicitamente) o método de interface herdado, a implementação base não poderá mais ser acessada. A chamada por meio da referência de instância atual invocará a implementação derivada; Isso causa recursão e um estouro de pilha eventual.

 Essa regra não relata uma violação para uma implementação explícita de <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> quando um `Close()` método ou visível externamente `System.IDisposable.Dispose(Boolean)` é fornecido.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente um novo método que expõe a mesma funcionalidade e que seja visível para tipos derivados ou altere para uma implementação não explícita. Se uma alteração significativa for aceitável, uma alternativa é tornar o tipo lacrado.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se for fornecido um método externo visível que tenha a mesma funcionalidade, mas um nome diferente do método implementado explicitamente.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo, `ViolatingBase` , que viola a regra e um tipo, `FixedBase` , que mostra uma correção para a violação.

 [!code-csharp[FxCop.Design.ExplicitMethodImplementations#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExplicitMethodImplementations/cs/FxCop.Design.ExplicitMethodImplementations.cs#1)]

## <a name="see-also"></a>Consulte Também
 [Interfaces](https://msdn.microsoft.com/library/2feda177-ce11-432d-81b4-d50f5f35fd37)

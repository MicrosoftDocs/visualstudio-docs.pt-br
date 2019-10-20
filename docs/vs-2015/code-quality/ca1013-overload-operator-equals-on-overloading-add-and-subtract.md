---
title: 'CA1013: sobrecarga do operador Equals ao sobrecarregar adicionar e subtrair | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
helpviewer_keywords:
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
ms.assetid: 5bd28d68-c179-49ff-af47-5250b8b18a10
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dd1c144f04150e3965e2c0264b80147cbd9b8f19
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663205"
---
# <a name="ca1013-overload-operator-equals-on-overloading-add-and-subtract"></a>CA1013: sobrecarregar igualdades de operador em add e subtract de sobrecarga
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|OverloadOperatorEqualsOnOverloadingAddAndSubtract|
|CheckId|CA1013|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo público ou protegido implementa os operadores de adição ou subtração sem implementar o operador de igualdade.

## <a name="rule-description"></a>Descrição da Regra
 Quando instâncias de um tipo podem ser combinadas usando operações como adição e subtração, você quase sempre deve definir igualdade para retornar `true` para quaisquer duas instâncias que tenham os mesmos valores de constituintes.

 Você não pode usar o operador de igualdade padrão em uma implementação sobrecarregada do operador de igualdade. Isso causará um estouro de pilha. Para implementar o operador de igualdade, use o método Object. Equals em sua implementação. Consulte o exemplo a seguir.

```vb
If (Object.ReferenceEquals(left, Nothing)) Then
    Return Object.ReferenceEquals(right, Nothing)
Else
    Return left.Equals(right)
End If
```

```csharp
if (Object.ReferenceEquals(left, null))
    return Object.ReferenceEquals(right, null);
return left.Equals(right);
```

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente o operador de igualdade para que ele seja matematicamente consistente com os operadores de adição e subtração.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra quando a implementação padrão do operador de igualdade fornece o comportamento correto para o tipo.

## <a name="example"></a>Exemplo
 O exemplo a seguir define um tipo (`BadAddableType`) que viola essa regra. Esse tipo deve implementar o operador de igualdade para fazer com que as duas instâncias que têm os mesmos valores de campo testem `true` para igualdade. O tipo `GoodAddableType` mostra a implementação corrigida. Observe que esse tipo também implementa o operador de desigualdade e substitui <xref:System.Object.Equals%2A> para atender a outras regras. Uma implementação completa também implementará <xref:System.Object.GetHashCode%2A>.

 [!code-csharp[FxCop.Design.AddAndSubtract#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AddAndSubtract/cs/FxCop.Design.AddAndSubtract.cs#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir testa a igualdade usando instâncias dos tipos que foram definidos anteriormente neste tópico para ilustrar o comportamento padrão e correto para o operador de igualdade.

 [!code-csharp[FxCop.Design.TestAddAndSubtract#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestAddAndSubtract/cs/FxCop.Design.TestAddAndSubtract.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **Tipo inadequado: {2,2} {2,2} são iguais? Não há** 
**bom tipo: {3,3} {3,3} são iguais? Sim** 
**bom tipo: {3,3} 0 são = =?   Sim** 1**tipo inadequado: 3 4 são iguais? Não há** 5**bom tipo: 7 8 são = =?   Não**
## <a name="see-also"></a>Consulte também
 [Operadores de igualdade](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)

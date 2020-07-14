---
title: 'CA1402: evitar sobrecargas em interfaces visíveis COM | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidOverloadsInComVisibleInterfaces
- CA1402
helpviewer_keywords:
- AvoidOverloadsInComVisibleInterfaces
- CA1402
ms.assetid: 2724c1f9-d5d3-4704-b124-21c4d398e5df
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b5c1e3af0e35bf92d72e853948c455893b417998
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534934"
---
# <a name="ca1402-avoid-overloads-in-com-visible-interfaces"></a>CA1402: Evitar sobrecargas em interfaces visíveis no COM
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidOverloadsInComVisibleInterfaces|
|CheckId|CA1402|
|Categoria|Microsoft. Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Uma interface visível de Component Object Model (COM) declara métodos sobrecarregados.

## <a name="rule-description"></a>Descrição da Regra
 Quando os métodos sobrecarregados são expostos a clientes COM, apenas a primeira sobrecarga do método mantém seu nome. Sobrecargas subsequentes são renomeadas exclusivamente anexando ao nome um caractere de sublinhado ' _ ' e um inteiro que corresponde à ordem de declaração da sobrecarga. Por exemplo, considere os métodos a seguir.

```
void SomeMethod(int valueOne);
void SomeMethod(int valueOne, int valueTwo, int valueThree);
void SomeMethod(int valueOne, int valueTwo);
```

 Esses métodos são expostos a clientes COM como a seguir.

```
void SomeMethod(int valueOne);
void SomeMethod_2(int valueOne, int valueTwo, int valueThree);
void SomeMethod_3(int valueOne, int valueTwo);
```

 Os clientes COM Visual Basic 6 não podem implementar métodos de interface usando um sublinhado no nome.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, renomeie os métodos sobrecarregados para que os nomes sejam exclusivos. Como alternativa, torne a interface invisível para COM alterando a acessibilidade para `internal` ( `Friend` em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ) ou aplicando o <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> atributo definido como `false` .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma interface que viola a regra e uma interface que cumpre a regra.

 [!code-csharp[FxCop.Interoperability.OverloadsInterface#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.OverloadsInterface/cs/FxCop.Interoperability.OverloadsInterface.cs#1)]
 [!code-vb[FxCop.Interoperability.OverloadsInterface#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.OverloadsInterface/vb/FxCop.Interoperability.OverloadsInterface.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1413: Evitar campos não públicos em tipos de valor visíveis no COM](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

 [CA1407: Evitar membros estáticos em tipos visíveis no COM](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

 [CA1017: Marcar assemblies com ComVisibleAttribute](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>Consulte Também
 Interoperação com o [tipo de dados Long](https://msdn.microsoft.com/library/b4770c34-1804-4f8c-b512-c10b0893e516) [de código não gerenciado](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)

---
title: 'CA2119: métodos de lacre que atendem a interfaces privadas | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SealMethodsThatSatisfyPrivateInterfaces
- CA2119
helpviewer_keywords:
- CA2119
- SealMethodsThatSatisfyPrivateInterfaces
ms.assetid: 483d02e1-cfaf-4754-a98f-4116df0f3509
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0afa6950a6ad876cdcfdcc1a56dd143422b9d44f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544346"
---
# <a name="ca2119-seal-methods-that-satisfy-private-interfaces"></a>CA2119: Selar métodos que atendem a interfaces particulares
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|SealMethodsThatSatisfyPrivateInterfaces|
|CheckId|CA2119|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público herdável fornece uma implementação de método substituível de uma `internal` `Friend` interface (no Visual Basic).

## <a name="rule-description"></a>Descrição da Regra
 Os métodos de interface têm acessibilidade pública, que não pode ser alterada pelo tipo de implementação. Uma interface interna cria um contrato que não deve ser implementado fora do assembly que define a interface. Um tipo público que implementa um método de uma interface interna usando o `virtual` `Overridable` modificador (in Visual Basic) permite que o método seja substituído por um tipo derivado que está fora do assembly. Se um segundo tipo no assembly de definição chamar o método e esperar um contrato somente interno, o comportamento poderá ser comprometido quando, em vez disso, o método substituído no assembly externo for executado. Isso cria uma vulnerabilidade de segurança.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, impeça que o método seja substituído fora do assembly usando um dos seguintes:

- Crie o tipo declarativo `sealed` ( `NotInheritable` em Visual Basic).

- Altere a acessibilidade do tipo declarativo para `internal` ( `Friend` em Visual Basic).

- Remova todos os construtores públicos do tipo declarativo.

- Implemente o método sem usar o `virtual` modificador.

- Implemente o método explicitamente.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se, após a revisão cuidadosa, não existir nenhum problema de segurança que possa ser explorável se o método for substituído fora do assembly.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo, `BaseImplementation` , que viola essa regra.

 [!code-cpp[FxCop.Security.SealMethods1#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/cpp/FxCop.Security.SealMethods1.cpp#1)]
 [!code-csharp[FxCop.Security.SealMethods1#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/cs/FxCop.Security.SealMethods1.cs#1)]
 [!code-vb[FxCop.Security.SealMethods1#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods1/vb/FxCop.Security.SealMethods1.vb#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir explora a implementação do método virtual do exemplo anterior.

 [!code-cpp[FxCop.Security.SealMethods2#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/cpp/FxCop.Security.SealMethods2.cpp#1)]
 [!code-csharp[FxCop.Security.SealMethods2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/cs/FxCop.Security.SealMethods2.cs#1)]
 [!code-vb[FxCop.Security.SealMethods2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.SealMethods2/vb/FxCop.Security.SealMethods2.vb#1)]

## <a name="see-also"></a>Consulte Também
 [Interfaces](https://msdn.microsoft.com/library/2feda177-ce11-432d-81b4-d50f5f35fd37) [Interfaces de](https://msdn.microsoft.com/library/61b06674-12c9-430b-be68-cc67ecee1f5b) interfaces
